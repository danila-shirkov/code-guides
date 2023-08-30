---
title: ¿Qué es un Makefile y cómo empezar a usarlo?
subtitle: Guía básica sobre make y Makefile para usar en tus propios proyectos.
description: Esta guía te mostrará cómo el uso de la herramienta Makefile puede simplificar el proceso de configuración de un proyecto a unas pocas y comprensibles comandos.
image: "/assets/images/makefile/cover.jpg"
author: Kirill Mokevnin
---

## Introducción

En la vida de muchos desarrolladores, hay una historia sobre su primer día de trabajo en un nuevo proyecto. Después de clonar el repositorio principal del proyecto, llega el momento en el que tienes que ingresar una serie de comandos con ciertas banderas y en un orden específico. Sin una descripción de los comandos, en la mayoría de los casos, es imposible entender qué está sucediendo, por ejemplo:

```bash
# Bash
touch ~/.bash_history
ufw allow 3035/tcp || echo 'no se puede configurar ufw'
ufw allow http || echo 'no se puede configurar ufw'
docker run \
  -v /root/:/root/ \
  -v /etc:/etc \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /var/tmp:/var/tmp \
  -v /tmp:/tmp \
  -v $PWD:/app \
  --network host \
  -w /app \
  --env-file .env \
  ansible ansible-playbook ansible/development.yml -i ansible/development --limit=localhost -vv
grep -qxF 'fs.inotify.max_user_watches=524288' /etc/sysctl.conf || echo fs.inotify.max_user_watches=524288 | tee -a /etc/sysctl.conf || echo 'no se puede establecer max_user_watches' && sysctl -p
sudo systemctl daemon-reload && sudo systemctl restart docker
```

Estos comandos son solo una parte de lo que se debe hacer al configurar un proyecto. En el ejemplo anterior, se puede ver que los comandos en sí son largos, contienen muchas banderas y, por lo tanto, no solo es difícil recordarlos, sino también ingresarlos manualmente. A medida que el proyecto crece, se vuelve más difícil mantener la documentación actualizada y el umbral de entrada para los recién llegados se vuelve más alto, ya que nadie puede recordar todos los detalles del proyecto. Algunos de estos comandos deben usarse todos los días, e incluso más de una vez al día.

<Banner name="intensive-devops" />

Con el tiempo, se hace evidente que se necesita una herramienta que pueda combinar estos comandos, proporcionar atajos convenientes para ellos y documentar automáticamente el proyecto. Esa herramienta es el *Makefile* y la utilidad `make`. Esta guía te mostrará cómo el uso de estas herramientas puede simplificar el proceso de configuración de un proyecto a unas pocas y comprensibles comandos:

```bash
# Bash
make setup
make start
make test
```

## ¿Qué es `make` y *Makefile*?

*Makefile* es un archivo que se encuentra junto con el código en el repositorio. Por lo general, se coloca en la raíz del proyecto. Actúa como documentación y como código ejecutable. El Makefile oculta los detalles de implementación y organiza los comandos de manera clara, mientras que la utilidad `make` los ejecuta desde el Makefile que se encuentra en el directorio actual.

Inicialmente, `make` se diseñó para automatizar la compilación de programas y bibliotecas a partir del código fuente. Se incluyó de forma predeterminada en la mayoría de las distribuciones *nix, lo que llevó a su amplia adopción y uso generalizado. Más tarde, resultó que esta herramienta también es útil para el desarrollo de cualquier otro tipo de proyecto, ya que el proceso en su mayoría se reduce a las mismas tareas: automatización y compilación de aplicaciones.

El uso de Makefile en proyectos se ha convertido en un estándar para muchos desarrolladores, incluidos los proyectos grandes. Puedes encontrar ejemplos de Makefile en proyectos como [Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/build/root/Makefile), [Babel](https://github.com/babel/babel/blob/main/Makefile), [Ansible](https://github.com/ansible/ansible/blob/devel/Makefile) y, por supuesto, en todas partes en [Hexlet](https://github.com/Hexlet).

### Sintaxis de *Makefile*

`make` ejecuta objetivos del *Makefile*, que consisten en comandos:

```makefile
# Makefile
objetivo1: # nombre del objetivo, admite kebab-case y snake_case
	comando1 # se utiliza una tabulación para la sangría, este es un detalle importante
	comando2 # los comandos se ejecutarán secuencialmente y solo si el comando anterior tiene éxito
```

Pero no es suficiente simplemente comenzar a usar un Makefile en tu proyecto. Para obtener beneficios de su implementación, es necesario trabajar en la división de comandos en objetivos y darles nombres semánticamente apropiados. Al principio, mover los comandos al Makefile puede resultar en una mezcla de todos los comandos en un solo objetivo con un nombre "difuso":

```makefile
# Makefile
up: # configuración y ejecución
	cp -n .env.example .env
	touch database/database.sqlite
	composer install
	npm install
	php artisan key:generate
	php artisan migrate --seed
	heroku local -f Procfile.dev # ejecutar el proyecto
```

Aquí se realizan varias acciones a la vez: se crea un archivo con variables de entorno, se prepara la base de datos, se generan claves, se instalan dependencias y se ejecuta el proyecto. Esto no se puede entender a partir de los comentarios y el nombre del objetivo, por lo que es correcto dividir estos comandos independientes en diferentes objetivos:

```makefile
# Makefile
env-prepare: # crear el archivo .env para las variables de entorno
	cp -n .env.example .env

sqlite-prepare: # preparar la base de datos local
	touch database/database.sqlite

install: # instalar dependencias
	composer install
	npm install

key: # generar claves
	php artisan key:generate

db-prepare: # cargar datos en la base de datos
	php artisan migrate --seed

start: # iniciar la aplicación
	heroku local -f Procfile.dev
```

Ahora, cuando los comandos se dividen en objetivos, puedes instalar las dependencias por separado con el comando `make install` o iniciar la aplicación con `make start`. Pero los otros objetivos solo son necesarios durante la configuración inicial del proyecto y deben ejecutarse en un orden específico. En el lenguaje del Makefile, un objetivo tiene dependencias:

```makefile
# Makefile
objetivo1: objetivo2 # esta sintaxis indica una dependencia entre tareas: objetivo1 depende de objetivo2
	comando2 # el comando2 se ejecutará solo si el comando de objetivo2 tiene éxito

objetivo2:
	comando1
```

Las tareas se ejecutarán solo en el orden especificado y solo si la tarea anterior tiene éxito. Por lo tanto, puedes agregar el objetivo `setup` para combinar todas las acciones necesarias:

```makefile
# Makefile
setup: env-prepare sqlite-prepare install key db-prepare # puedes hacer referencia a objetivos definidos más abajo

env-prepare:
	cp -n .env.example .env

sqlite-prepare:
	touch database/database.sqlite

install:
	composer install
	npm install

key:
	php artisan key:generate

db-prepare:
	php artisan migrate --seed

start:
	heroku local -f Procfile.dev
```

Ahora, configurar y ejecutar el proyecto solo requiere dos comandos:

```bash
# Bash
make setup # ejecuta secuencialmente: env-prepare sqlite-prepare install key db-prepare
make start
```

Gracias al Makefile, los comandos del proyecto junto con las banderas se han convertido en un solo archivo. Proporciona el orden correcto de ejecución y no importa qué lenguajes y tecnologías estén involucrados.

## Uso avanzado

### Objetivo falso

El uso de `make` en un proyecto puede llevar a un error `make: <nombre-del-objetivo> is up to date.` aunque todo esté escrito correctamente. A menudo, esto ocurre cuando hay un directorio o archivo con el mismo nombre que el objetivo. Por ejemplo:

```makefile
# Makefile
test: # objetivo en el Makefile
	php artisan test
```

```bash
# Bash
$ ls
Makefile
test # hay un directorio en el sistema de archivos con el mismo nombre que el objetivo en el Makefile

$ make test # intento de ejecutar las pruebas
make: `test` is up to date.
```

Como se mencionó anteriormente, `make` se diseñó inicialmente para compilar desde el código fuente. Por lo tanto, busca un directorio o archivo con el nombre especificado y trata de compilar el proyecto a partir de él. Para cambiar este comportamiento, debes agregar el indicador `.PHONY` al final del Makefile:

```makefile
# Makefile
test:
	php artisan test

.PHONY: test
```

```bash
# Bash
$ make test
✓ ¡Todas las pruebas pasaron!
```

### Ejecución secuencial de comandos e ignorar errores

Puedes ejecutar comandos uno por uno: `make setup`, `make start`, `make test` o especificarlos en una cadena separada por espacios: `make setup start test`. El último método funciona como una dependencia entre tareas, pero sin describirla en el Makefile. Pueden surgir problemas si uno de los comandos devuelve un error que debe ignorarse. En los ejemplos anteriores, este comando fue la creación del archivo .env al configurar el proyecto:

```makefile
# Makefile
env-prepare:
	cp -n .env.example .env # si el archivo ya existe, volver a ejecutar este comando devolverá un error
```

La forma más sencilla (*pero no la única*) de "ignorar" el error es usar un operador OR en el Makefile:

```makefile
# Makefile
env-prepare:
	cp -n .env.example .env || true # ahora cualquier resultado de la ejecución del comando se considerará exitoso
```

Debes tener cuidado al agregar este tipo de soluciones para evitar problemas en casos más complejos.

### Variables

A menudo, los comandos requieren parámetros para la configuración, rutas, variables de entorno, y `make` también te permite controlar esto. Puedes especificar variables directamente en el comando dentro del Makefile y pasarlas al llamarlo:

```makefile
# Makefile
say:
	echo "Hola, $(HELLO)!"
```

```bash
# Bash
$ make say HELLO=Mundo
echo "Hola, Mundo!"
Hola, Mundo!

$ make say HELLO=Gatito
echo "Hola, Gatito!"
Hola, Gatito!
```

Las variables pueden ser opcionales y tener un valor predeterminado. Por lo general, se declaran al comienzo del Makefile.

```makefile
# Makefile
HELLO?=Mundo # el signo de interrogación indica que la variable es opcional. No es necesario especificar un valor después del signo de asignación.

say:
	echo "Hola, $(HELLO)!"
```

```bash
# Bash
$ make say
echo "Hola, Mundo!"
Hola, Mundo!

$ make say HELLO=Gatito
echo "Hola, Gatito!"
Hola, Gatito!
```

Algunas variables en el *Makefile* tienen nombres diferentes a las variables del sistema. Por ejemplo, `$PWD` se llama `$CURDIR` en el [Makefile](https://github.com/hexlet-basics/hexlet_basics/blob/3f4635bf629e2676efe547c9a01c22a2573eaebd/Makefile#L35-L39) de Hexlet:
```makefile
# Makefile
project-env-generate:
	docker run --rm -e RUNNER_PLAYBOOK=ansible/development.yml \
		-v $(CURDIR)/ansible/development:/runner/inventory \ # $(CURDIR) es lo mismo que $PWD en la terminal
		-v $(CURDIR):/runner/project \
		ansible/ansible-runner
```

## Conclusión

En esta guía, se han presentado las características básicas de *Makefile* y la utilidad `make`. Una mayor familiaridad con esta herramienta revelará muchas otras características útiles, como condiciones, bucles e inclusión de archivos. En empresas con múltiples proyectos desarrollados por diferentes equipos en diferentes momentos, el Makefile será una gran ayuda para estandarizar los comandos comunes: `setup start test deploy ...`.

La capacidad de describir comandos de varias líneas en el Makefile permite utilizarlo como un "pegamento universal" entre los administradores de lenguajes y otras utilidades. La amplia disponibilidad de esta herramienta y su simplicidad general permiten implementarla en tu proyecto fácilmente, sin necesidad de modificaciones. Sin embargo, un Makefile puede ser realmente grande y complejo, como se puede ver en ejemplos de proyectos reales:

* [Codebattle](https://github.com/hexlet-codebattle/codebattle/blob/master/Makefile)
* [Babel](https://github.com/babel/babel/blob/main/Makefile)
* [Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/build/root/Makefile)

### Recursos adicionales

{/*- [Makefile Tutorial](https://makefile.site/) - a "cheat sheet" from the official documentation in Russian; */}
* [Make Utility: A Useful Universal Tool for Programmers](https://www.youtube.com/watch?v=pK9mF5aK05Q) - video version of this guide.

Makefiles used in this guide:

* [Hexlet SICP](https://github.com/Hexlet/hexlet-sicp/blob/master/Makefile)
* [Hexlet Basics](https://github.com/hexlet-basics/hexlet_basics/blob/master/Makefile)