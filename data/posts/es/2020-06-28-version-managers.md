---
title: ¿Qué es un "Gestor de versiones"?
subtitle: Cómo gestionar las versiones de los lenguajes
description: Describimos un programa diseñado para gestionar las versiones de los lenguajes. Con él, puedes instalar las versiones necesarias y cambiar entre ellas.
image: "/assets/images/version-manager/title.png"
author: Kirill Mokevnin
---

## Instalación del sistema

Para ejecutar código en cualquier lenguaje, es necesario instalar su intérprete (o compilador). En diferentes sistemas operativos, esto se hace de diferentes maneras: algunos utilizan gestores de paquetes como *apt* o *yum*, mientras que otros descargan un instalador. Algunos lenguajes ya vienen preinstalados, como Python, que está ampliamente integrado en las distribuciones de Linux.

```bash
# Ubuntu
sudo apt install nodejs # instalará una versión no tan reciente
```

El método estándar de instalación funciona bien solo al principio, durante la configuración inicial. Con el tiempo, comienzan a surgir diferentes problemas. Por ejemplo, en algún momento se lanza una nueva versión del lenguaje que se debe agregar al proyecto. Por lo general, lleva algún tiempo antes de que el lenguaje esté disponible para su instalación a través de los gestores de paquetes. Y aquí tienes dos opciones: esperar, lo cual no siempre es deseable, o buscar otra forma de instalarlo. Esta última a menudo se convierte en un desafío serio, con horas de búsqueda en Google e instalación de bibliotecas adicionales. Todo esto termina por saturar el sistema y, a veces, incluso romperlo.

<Banner name="intensive-devops" />

Otro problema importante es la instalación de múltiples versiones de un mismo lenguaje. Esto es necesario cuando un desarrollador cambia entre diferentes proyectos que requieren diferentes versiones. ¿Con qué frecuencia ocurre esto? Muy a menudo. Cuanto más avanzada es la etapa de desarrollo, más opciones hay: diferentes proyectos en la empresa, proyectos propios, proyectos de código abierto.

*Es importante mencionar que todo esto no se aplica a aquellos que utilizan Docker y Docker Compose. Sin embargo, incluso en este caso, se necesitan lenguajes para trabajar con el código abierto.*

## Gestores de versiones

Para resolver estos problemas, los desarrolladores han ideado gestores de versiones. Un gestor de versiones es un programa especial diseñado para gestionar las versiones de un lenguaje. Con él, puedes instalar las versiones necesarias y cambiar entre ellas. A diferencia de los gestores de paquetes integrados en los sistemas operativos, los gestores de versiones siempre permiten instalar las últimas versiones de los lenguajes tan pronto como se lanzan (incluyendo versiones alfa y beta).

Por ejemplo, para Node.js existe [NVM](https://github.com/nvm-sh/nvm) (Node Version Manager):

```bash
# Instalación de NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
# La instalación no implica la activación. Después de la instalación, la versión activa seguirá siendo la misma que antes de la instalación
nvm install node # Instalar la última versión disponible de Node.js
nvm install 6.14.4 # o 10.10.0, 8.9.1, etc.
nvm ls-remote # lista de versiones disponibles
nvm use node # Activar la última versión instalada de Node.js
nvm use node 17 # Activar la versión deseada
```

Para facilitar el trabajo, los gestores de versiones suelen permitir crear un archivo especial dentro del proyecto que registra la versión deseada del lenguaje. En algunos casos, los gestores de versiones rastrean automáticamente este archivo y cambian la versión automáticamente.

```bash
echo "17" > .nvmrc
# Este comando detecta el archivo .nvmrc y utiliza la versión especificada allí
$ nvm use
Found '/path/to/project/.nvmrc' with version <17>
Now using node v17
```

En el mundo moderno, es difícil imaginar un lenguaje que no tenga un gestor de versiones. Además, algunos lenguajes, como Ruby, tienen múltiples gestores de versiones que compiten entre sí:

* go: gvm, g
* java: jabba
* ruby: rbenv, rvm, chruby
* php: phpenv, phpbrew
* python: pyenv

Los gestores de versiones han resuelto varios problemas importantes. Por lo general, cuando un programador interactúa con un lenguaje instalado directamente, tiene que usar *sudo* para instalar paquetes globales. Esto se debe a que el esquema de instalación estándar del lenguaje está diseñado para todos los usuarios a la vez. Por lo tanto, todos los archivos necesarios, incluidos los paquetes globales, se colocan en directorios compartidos que requieren permisos de administrador. Desde el punto de vista de la seguridad, esto es un agujero bastante grande que los desarrolladores de bibliotecas de código abierto pueden (y a veces lo hacen) aprovechar. Los gestores de versiones instalan todo en el directorio de inicio del usuario actual, donde ya tiene todos los permisos. Por un lado, esto evita la necesidad de ejecutar la instalación de paquetes en nombre del administrador, y por otro lado, no se satura el sistema. Eliminar un lenguaje y todos sus paquetes a través del gestor de versiones es extremadamente fácil. Basta con borrar el directorio (aunque es mejor hacerlo a través del propio gestor de versiones).

## Gestor universal

Al resolver algunos problemas, los gestores de versiones han creado otros. En primer lugar, hay demasiados de ellos y a veces cambian: uno se vuelve popular, luego otro. En segundo lugar, el proceso de instalación del gestor de versiones puede ser más complicado que la instalación del lenguaje en sí. El problema es que deben ser universales y funcionar en todas partes, lo cual es extremadamente difícil dada la diversidad de los ecosistemas modernos. Basta con echar un vistazo a la documentación de NVM para darse cuenta de la magnitud del desastre. En tercer lugar, todos estos gestores funcionan de manera diferente y tienen comandos diferentes. Esto complica el proceso de cambiar entre ellos al trabajar con diferentes lenguajes.

Todo esto llevó al siguiente paso lógico. Finalmente, apareció un gestor universal llamado [asdf](https://asdf-vm.com/), que, gracias a los complementos, puede trabajar con cualquier lenguaje. Aquí hay una lista incompleta de sus ventajas:

* Una sola utilidad de línea de comandos para trabajar con todos los lenguajes
* Una interfaz de interacción unificada para todos los lenguajes
* Cambio automático a la versión necesaria del lenguaje dentro de cada proyecto
* Un sistema de complementos sencillo que permite agregar cualquier lenguaje

Actualmente, *asdf* está ganando popularidad y gradualmente está reemplazando a todos los demás gestores de versiones (técnicamente, a menudo utiliza gestores específicos de cada lenguaje bajo el capó). Tiene un sistema de comandos un poco más complejo debido a la necesidad de admitir múltiples lenguajes, pero en general simplifica todo el proceso.

```bash
# asdf tiene una excelente documentación que muestra claramente cómo instalarlo
# y qué dependencias pueden ser necesarias en diferentes sistemas

# Instalación
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.11.1
# Luego, reinicia la terminal
echo '. $HOME/.asdf/asdf.sh' >> ~/.bashrc

# Activa los cambios realizados
source ~/.bashrc

# Para trabajar con un lenguaje específico, primero debes agregar el complemento correspondiente
# La lista de complementos disponibles se encuentra en el sitio web del proyecto
asdf plugin add nodejs

# Instalación del lenguaje
# En lugar de nodejs, debes usar el nombre del complemento con el que estás trabajando
asdf install nodejs latest # latest significa la última versión del lenguaje especificado

# Instalación de una versión específica
asdf install nodejs 18.7.0

# Establecer una versión específica del lenguaje como la versión predeterminada
asdf global nodejs 18.7.0

# Muestra las versiones actuales de los lenguajes instalados a través de asdf
asdf current
elixir         1.10.1-otp-22 (set by /Users/user/.tool-versions)
erlang         22.2.7   (set by /Users/user/.tool-versions)
nodejs         17.0.0   (set by /Users/user/.tool-versions)
php            7.4.5    (set by /Users/user/.tool-versions)
python         3.8.2 2.7.16 (set by /Users/user/.tool-versions)
ruby           2.7.0    (set by /Users/user/.tool-versions)
yarn           1.22.4   (set by /Users/user/.tool-versions)
```

## Conclusión

Trabajar con diferentes versiones de lenguajes es una tarea complicada que los gestores de versiones y Docker (para usuarios avanzados) resuelven. Entre todos los gestores, destaca *asdf*, que se está convirtiendo en una herramienta universal para gestionar cualquier lenguaje e incluso programas regulares.
