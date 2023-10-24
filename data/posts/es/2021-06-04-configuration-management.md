---
title: ¿Qué es la "gestión de la configuración"?
# subtitle: Framework de front-end para el desarrollo web rápido y sencillo.
description: Hablamos sobre la configuración de servidores de forma automática, la importancia de la idempotencia y por qué los scripts de bash son malos.
# image: "/assets/images/bootstrap/bootstrap.jpeg"
author: Kirill Mokevnin
---

Los sitios web no solo son código, sino también infraestructura para su ejecución. En primer lugar, esto incluye servidores en los que se ejecuta el código, una base de datos y varios sistemas auxiliares. A veces, todo esto se coloca en un solo servidor, en situaciones más complejas, la cantidad de servidores se mide en miles, y se involucran equipos enteros de ingenieros (administradores de diferentes tipos). Independientemente del tamaño del sitio, los problemas de mantenimiento de la infraestructura son muy similares para todos. Hablemos de uno en particular: la configuración del servidor.

*Existen enfoques que permiten evitar la interacción directa con la infraestructura. No se consideran en este artículo, pero es útil conocerlos. Estos incluyen: alojamiento clásico con software preinstalado, servless, alojamiento de sitios estáticos, soluciones PaaS y Kubernetes (y sus análogos)*

<Banner name="intensive-devops" />

En la gran mayoría de los casos, los servidores se alquilan a empresas de alojamiento como [DigitalOcean](https://m.do.co/c/e702f9a99145) o AWS. Esto se hace en 5 minutos con solo presionar unos pocos botones. Se nos pedirá que elijamos las características del servidor, el sistema operativo y el centro de datos en el que se implementará. Como resultado, obtenemos una máquina (virtual) con un sistema operativo preinstalado y una dirección IP para acceder a través de SSH.

{/* image: DO */}

La nueva máquina solo contiene el sistema operativo básico con un conjunto pequeño de programas preinstalados. Antes de ejecutar cualquier servicio en ella, como un sitio web normal, será necesario instalar paquetes adicionales. El conjunto de paquetes depende de la pila de tecnología en la que esté escrito. Si el sitio web está "envuelto" en Docker, la configuración se simplifica significativamente y se reduce a la instalación de Docker en sí. En otros casos, se requerirá algún tiempo para la configuración y configuración. Además de los paquetes, a menudo es necesario configurar el sistema en sí, cambiar archivos de configuración, permisos de archivos y directorios, crear usuarios, etc.:

```shell
# Cómo podría ser
# Servidor en Ubuntu

# Acceder a la máquina remota
ssh root@ipaddress

# Crear un usuario para implementación
# En algún lugar aquí se copian las claves SSH
sudo adduser deploy

sudo apt install curl
# Instalar Node.js
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt install nodejs
# Instalar y configurar Nginx
sudo apt install nginx
vim /etc/nginx/default.conf

# Crear la estructura de directorios para el servicio
mkdir -p /opt/hexlet/versions/
```

El proceso de configuración inicial lleva horas e incluso días. Siempre habrá algo que ajustar, configurar e instalar. El ciclo se repetirá nuevamente cuando sea necesario actualizar las versiones de los paquetes. Nuevamente, tendrá que acceder al servidor, recordar qué y dónde se configuró y cómo actualizar sin romper nada. ¿Cuál es el problema con la configuración manual?

Los servidores pueden fallar y hacerlo de forma inesperada. ¿Cuánto tiempo llevará "implementar" un nuevo servidor? Prácticamente tanto tiempo como se tardó la primera vez. Nadie recordará el orden de las acciones y las configuraciones necesarias incluso una semana después de la configuración, y mucho menos después de meses. Además, ¿qué pasa si la persona que hizo la configuración inicial ya no trabaja en la empresa o está de vacaciones? ¿Entonces qué? Tendrás que disculparte durante mucho tiempo ante los usuarios por una larga interrupción, y lo mejor es que el negocio no se vea muy afectado.

La reinstalación del servidor no siempre está relacionada con circunstancias imprevistas. En empresas con una buena cultura de ingeniería, los servidores se cambian regularmente. Esto es importante al menos por razones de seguridad. Los sistemas operativos tienen vulnerabilidades que se solucionan con nuevos paquetes o versiones. Es bastante difícil estar al tanto de esto, por lo que es más fácil actualizar regularmente la infraestructura. Por otro lado, actualizar un servidor puede romper fácilmente una aplicación en funcionamiento y causar interrupciones en el trabajo. La única forma de garantizar un funcionamiento continuo durante la actualización es levantar otro servidor y configurarlo. Luego, el servicio simplemente se implementa en el nuevo servidor y se apaga el antiguo.

## Automatización

Sería bueno automatizar la configuración del servidor. Para esto, existen varios enfoques que veremos a continuación.

### Scripts de bash

En el caso más simple, esto se puede lograr con un simple script de bash al que se le agregan secuencialmente los comandos que solíamos ejecutar manualmente. Luego, todo se reduce a copiar el script en el servidor y ejecutarlo:

```shell
# Copiar al servidor usando scp
scp mybashscript.sh root@ipaddress:~/

# Acceder al servidor y ejecutar el script
ssh root@ipaddress
sh ~/mybashscript.sh
```

Si se transfieren los comandos al script de bash "tal cual", sin modificaciones, es probable que tengamos que estar constantemente atentos a la salida y no olvidar confirmar la instalación de paquetes, ya que este es el comportamiento predeterminado:

```shell
➜  ~ apt install golang
The following additional packages will be installed:
  golang-1.13 golang-1.13-doc golang-1.13-go golang-1.13-race-detector-runtime golang-1.13-src golang-doc golang-go
Need to get 63.5 MB of archives.
After this operation, 329 MB of additional disk space will be used.
Do you want to continue? [Y/n] # El script se detiene y espera una respuesta
```

La opción `-y` se agrega para responder automáticamente "sí". Otras comandos tienen sus propias opciones para suprimir la interacción con el usuario. Tendremos que tener en cuenta todas estas opciones.

```shell
apt install -y golang
```

Otro problema más serio está relacionado con el concepto de "idempotencia". ¿Qué sucederá si ejecutamos el comando para crear un directorio dos veces?

```shell
mkdir /hexlet
mkdir /hexlet # ?
```

El comando fallará con un error, no es idempotente. Es decir, las llamadas secuenciales al mismo comando dan como resultado diferentes resultados. La idempotencia es muy importante para la configuración del servidor. De lo contrario, la ejecución repetida del script de configuración dará como resultado un error. Y las ejecuciones repetidas son necesarias, por ejemplo, para depurar el propio script cuando lo estamos escribiendo y comprobando cómo funciona. En el caso del comando `mkdir`, es fácil lograr la idempotencia agregando la opción `-p`:

```shell
mkdir -p /hexlet
mkdir -p /hexlet # no habrá errores
```

Pero, lamentablemente, no todos los comandos admiten esta opción. Para muchas situaciones, es necesario garantizar la idempotencia por nuestra cuenta, lo que complicará significativamente el script. De un conjunto simple de comandos, se convertirá en un código real con construcciones condicionales. Y en algún momento, será muy difícil entenderlo. Muchos han pasado por esto, especialmente antes, cuando no había alternativa.

Pero el problema no es solo la idempotencia. Algunas tareas que eran fáciles de hacer manualmente se vuelven difíciles de automatizar. Imagina que para cambiar la configuración, necesitas modificar una línea específica dentro de un archivo. ¿Cómo se puede hacer esto fácilmente con un script de bash? No se puede, tendrás que reemplazar completamente el archivo copiando todo su contenido en el script de bash (o junto a él), o usar algo como sed para reemplazar una línea específica.

Y, por último, pero no menos importante, la limitación muy importante. El script de bash debe entregarse al servidor por sí mismo. Y si esto se puede automatizar para un solo servidor, se convierte en un problema cuando hay varios servidores. Es importante hacer esto de forma paralela, de lo contrario, la configuración se extenderá durante horas incluso si está completamente automatizada. Agregue a esto diferentes servidores con sus propios scripts que difieren de los demás.

En este punto, los scripts de bash dejan de ser útiles y es necesario pensar en algo más. Así es como comenzaron a aparecer herramientas especializadas para la configuración de servidores. Uno de los primeros proyectos fue Chef y Puppet. Ahora, Ansible ha ganado la mayor popularidad, ya que es mucho más fácil de aprender y usar.

## Ansible

Es un sistema de gestión de configuración (de servidores) que resuelve todos los problemas descritos anteriormente y, además, se puede utilizar no solo para la configuración, sino también para la implementación, es decir, la instalación y ejecución de un servicio. Para instalar Ansible, utilice uno de los [métodos propuestos](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

En su forma más básica, la configuración de Ansible se ve como dos archivos, uno es la descripción de los servidores y el otro son los comandos que queremos ejecutar. Ansible se conecta a los servidores remotos y ejecuta los comandos necesarios. Lo más importante es proporcionar acceso a estos servidores, por ejemplo, a través de claves SSH.

La descripción de los servidores se almacena en un archivo *inventory.ini*. Ansible lo utiliza para determinar las máquinas en las que se debe realizar la configuración.

```ini
; dirección de la máquina que estamos configurando
; para simplificar, le decimos a Ansible que use la computadora local
127.0.0.1 ansible_connection=local
```

Los comandos de configuración del servidor se registran en archivos llamados playbooks. Los playbooks se crean en formato YAML con cualquier nombre. Por ejemplo, playbook.yaml:

```yaml
# hosts: significa el grupo de máquinas en el que se ejecutará
# all: significa todas las máquinas descritas en inventory.ini
- hosts: all
  tasks: # conjunto de comandos que se deben ejecutar
    - ansible.builtin.file: # file: gestiona archivos y directorios
        name: /tmp/ansible_was_here
        state: touch # ejecuta el comando touch si el archivo no existe. Y esto es idempotencia
```

La estructura de archivos puede verse así:

```shell
tree # muestra el contenido del directorio
.
├── inventory.ini
└── playbook.yaml
```

Ahora ejecutamos:

```shell
# ¡La ejecución de Ansible se realiza en la máquina local!
# Debe ejecutarse en el mismo directorio donde se crearon los archivos
# -i significa inventory.ini
# https://github.com/hexlet-boilerplates/ansible
ansible-playbook -i inventory.ini playbook.yaml

PLAY [Server Setup] ***********************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************
ok: [127.0.0.1]

TASK [file] *******************************************************************************************************************
changed: [127.0.0.1]

PLAY RECAP ********************************************************************************************************************
127.0.0.1                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```

La salida indica que el playbook se ejecutó correctamente. Como resultado, se creará un archivo *ansible_was_here* en el directorio */tmp*. La ejecución repetida del playbook también se completará correctamente, pero la salida mostrará que no se realizarán cambios, ya que Ansible garantiza la idempotencia. En este caso, verificará si el archivo existe y omitirá el comando si el archivo existe. Si se especifican varias direcciones IP en *inventory.ini*, Ansible ejecutará el playbook en cada una de ellas, y lo hará en paralelo. Lo único que no debemos olvidar es agregar claves SSH a estas máquinas, de lo contrario, Ansible no podrá acceder a ellas.

![Ansible](/assets/images/configuration-management/ansible.png)

¿Qué es un playbook? Lo más importante en él es un conjunto de tareas (tasks) que queremos ejecutar. A diferencia de un script de bash, las tareas no son solo comandos de bash. Para cada tarea en Ansible, hay un módulo incorporado que maneja una parte específica del sistema. Por ejemplo, dentro de Ansible hay módulos para trabajar con git, administradores de paquetes, archivos, etc. En total, hay cientos de ellos para todos los casos de uso. Gracias a las integraciones listas para usar, Ansible sabe cómo funcionan diferentes partes del sistema, lo que le permite agregar verificaciones necesarias para garantizar la idempotencia. Algunos ejemplos:

```yaml
tasks:
  # Instalar PostgreSQL
  - name: Ensure postgresql is at the latest version
    ansible.builtin.apt: # módulo apt
      name: postgresql
      state: latest

  # Iniciar PostgreSQL
  - name: Ensure that postgresql is started
    ansible.builtin.service: # módulo service
      name: postgresql
      state: started # iniciar si no está iniciado
```

Como puedes ver, Ansible es lo suficientemente simple para comenzar, pero tiene muchas características que se pueden aprender a medida que te sumerges y la infraestructura se vuelve más compleja.

## Conclusión

La gestión de la configuración en el mundo moderno se realiza con herramientas especializadas que pueden conectarse a servidores remotos, configurarlos en paralelo y garantizar la idempotencia de las operaciones. Con este enfoque, es importante dejar de configurar servidores directamente. Cualquier cambio ahora debe hacerse a través de una herramienta de automatización, de lo contrario, todo volverá a los problemas iniciales. La gestión de la configuración a través del código aumenta la intercambiabilidad de las personas, permite rastrear fácilmente los cambios simplemente mirando el historial de git, y permite involucrar a otros miembros del equipo en la gestión de la infraestructura.

## Enlaces adicionales

* https://github.com/hexlet-boilerplates/ansible
* [Fundamentos de la automatización con Ansible](https://codica.la/cursos/ansible)
