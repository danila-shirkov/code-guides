---
title: Varias versiones de Python en una máquina Linux
redirect_to: http://codica.la/blog/usando-varias-versiones-de-python-en-sistemas-operativos-unix
subtitle: Uso de varias versiones de Python en sistemas operativos tipo Unix.
description: Métodos posibles para instalar varias versiones del entorno de ejecución de Python en una máquina que ejecuta un sistema operativo tipo Unix. Solución de problemas de instalación de aplicaciones diseñadas para una versión específica de Python utilizando entornos virtuales.
image: "/assets/images/python-2-and-3-logo.png"
hidden: true
author: Kirill Mokevnin
---

### Uso de varias versiones de Python en sistemas operativos tipo Unix.


#### ¿Qué y por qué?

Python como lenguaje está en constante desarrollo. La rama Py2 pronto se declarará como no compatible. Sin embargo, todavía existen entornos donde es necesario utilizar Py2 e incluso una versión anterior a 2.7.x. Además, Python 3.x es ahora una gran familia de versiones, algunas de las cuales no son compatibles entre sí, incluso en términos de sintaxis. Por lo tanto, un desarrollador de Python con un perfil amplio debe entender cómo tener varias versiones del entorno de ejecución en una sola máquina. ¡Incluso si se utiliza Docker en producción!

![logo](/assets/images/python-2-and-3-logo.png)

#### Instalación de Python desde los repositorios de paquetes del sistema operativo.

Si tienes suerte, la versión de Python que necesitas estará disponible en los repositorios de paquetes del sistema operativo y podrás instalarla con un comando como `sudo apt-get install python3.5`. Sin embargo, las distribuciones antiguas del sistema operativo pueden no incluir las nuevas versiones de Python, y las distribuciones más nuevas pueden incluir versiones antiguas de Python. En casos especiales, el repositorio puede contener solo una versión del entorno de ejecución.


#### Compilación desde el código fuente.

CPython es un proyecto de código abierto. Tener acceso al código fuente de todas las versiones de CPython te permite compilar la versión que necesitas por ti mismo. Sin embargo, este es un proceso que, aunque está bien documentado, requiere comprender lo que necesitarás para compilar el código en tu sistema operativo.

Además, compilar desde el código fuente es la única opción para aquellos que desean realizar cambios en el código o compilar el intérprete para una plataforma exótica (sistemas integrados, hardware retro).


#### pyenv

Otra forma de obtener diferentes versiones del entorno de ejecución en una sola máquina es utilizar [pyenv](https://github.com/pyenv/pyenv). Es un "administrador de versiones" en el estilo de rbenv para Ruby, nvm para NodeJS, etc.

La misión de pyenv es administrar las versiones de Python instaladas y hacer que una versión en particular sea "activa". La versión activa se utiliza cuando ejecutas el comando `python` (y también `pip`), y diferentes proyectos pueden utilizar diferentes versiones activas e incluso más de una al mismo tiempo. Esta última propiedad es útil para los autores de bibliotecas que deben probarse en diferentes versiones de Python.

La instalación de pyenv es bastante sencilla, ya que es un conjunto de scripts de shell. Por eso, pyenv es muy compatible con diferentes plataformas. Sin embargo, esta compatibilidad tiene un costo: ¡cada versión del entorno de ejecución debe ser compilada desde el código fuente! Para compilar CPython, necesitarás un compilador de C (`gcc` en Linux y `clang` en MacOS) y los archivos de encabezado de las bibliotecas utilizadas por el intérprete. Tendrás que buscar una lista completa de los requisitos de compilación.


#### Instalación con el gestor de paquetes del sistema desde fuentes externas.

Para la mayoría de los sistemas tipo Unix, además de los repositorios oficiales, existen fuentes de paquetes no oficiales.

Para sistemas basados en Debian, como Ubuntu y sus derivados, estas fuentes de paquetes se llaman *PPA, Personal Package Archives*. Es bastante fácil agregar cualquier PPA, pero debes entender que al hacerlo, estás aceptando la instalación de paquetes de una fuente externa que no está sujeta a los autores del sistema operativo. ¡Solo agrega PPA que tengan una buena reputación, como los proporcionados por los propios autores del software que deseas instalar!

Para sistemas basados en Ubuntu, existe el [PPA del equipo "deadsnakes"](https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa). Esta es una fuente de paquetes confiable con muchas versiones diferentes de Python, tanto para las versiones más recientes del sistema operativo como para las versiones más antiguas.

La principal ventaja de instalar paquetes desde PPA confiables es que estos paquetes suelen estar optimizados para la distribución específica con muchas actualizaciones y correcciones. Estas compilaciones son más seguras y eficientes que las compiladas manualmente desde el código fuente.

Además, los paquetes en PPA populares se actualizan oportunamente, lo cual no se puede decir de los paquetes para versiones obsoletas del sistema operativo que ya no tienen soporte. Por supuesto, es mejor no utilizar esas versiones (¡no son seguras!), pero a veces no hay otra opción, y con PPA al menos tendrás versiones actualizadas del entorno de ejecución.


#### Alias `python`, `python2`, `python3`.

Históricamente, el intérprete de Python se ejecuta con el comando `python`. Pero en algún momento apareció Python3, con incompatibilidad hacia atrás, lo que causó cierto "caos y confusión". Para agregar cierta claridad, se presentó [PEP-394](https://www.python.org/dev/peps/pep-0394): *The "python" Command on Unix-Like Systems*. Sin embargo, incluso este PEP permite a los sistemas *elegir por sí mismos* si usar Py2 y Py3 juntos o elegir solo uno. Los sistemas solo deben asegurarse de que

- el comando `python2` llame a una versión de Python 2.x, si está disponible;
- el comando `python3` llame a una versión de Python 3.x, si está disponible;
- el comando `python` corresponda a `python2` o `python3` (pero no a alguna otra versión del tiempo de ejecución).

Sin embargo, no se garantiza que todos estos comandos estén presentes en un caso específico: en algunos lugares solo estará disponible el comando `python3`, en otros solo `python2`. El alias `python` debe estar presente solo en un entorno virtual y siempre debe corresponder a la versión del intérprete que se seleccionó al crear el entorno.

Esta "variedad" dificulta la vida de los desarrolladores de software, ¡especialmente de los autores de herramientas de desarrollo! Un desarrollador puede escribir un script para Py2 y especificar `#!/usr/bin/env python` en el [shebang](https://es.wikipedia.org/wiki/Shebang). Pero en algunos sistemas, el comando `python` simplemente no estará disponible y el script no se ejecutará, y en otros `python` se referirá a alguna versión de Python 3.8 y el script puede ejecutarse pero fallará durante la ejecución.

Incluso si el autor utiliza técnicas que permiten escribir código portátil ([six](https://pypi.org/project/six/), [3to2](https://pypi.org/project/3to2/)) que se puede ejecutar tanto en Py2 como en Py3, ¡sigue sin estar claro qué se debe especificar en el shebang!

El PEP mencionado anteriormente sugiere

- fijar la versión explícitamente (solo Py2 o solo Py3),
- requerir el uso de entornos virtuales (en un entorno virtual siempre estará disponible el comando `python`)
- no escribir el shebang manualmente, sino utilizar herramientas como setuptools u otro sistema de empaquetado que cree puntos de entrada dependiendo de la instalación del paquete (el shebang de los puntos de entrada será correcto).


### Instalación de poetry en sistemas con diferentes versiones de Python

En el momento de escribir este artículo, poetry (una herramienta que administra entornos virtuales, gestiona paquetes, etc., una "navaja suiza" para desarrolladores de Python) tenía problemas con las versiones del tiempo de ejecución: al instalarlo de la forma recomendada, el script de instalación fallaba o la instalación tenía éxito pero el programa no funcionaba.

El problema era que tanto en el script de instalación como en los puntos de entrada del programa, se usaba `python` en el shebang. El programa en sí funciona tanto en Py2 como en Py3, pero los autores asumieron que en el sistema de destino siempre habría un alias `python` que llamaría a uno u otro intérprete. En algunos sistemas, este comando no existe&#x2026;

Si utilizas pyenv, siempre proporcionará el comando `python` y poetry "simplemente funcionará". No hay problemas incluso en distribuciones antiguas donde Py2 aún no se ha eliminado por completo. Y, por supuesto, todo funciona en un entorno virtual. Veamos este enfoque con más detalle.


#### Instalación en un entorno virtual dedicado

Primero, necesitamos el entorno en sí. Supongamos que ya has instalado Python3 de alguna manera. Hacemos lo siguiente:

```shell
$ python3 -m venv $HOME/.poetry.venv
```

Luego, hacemos esto:

```shell
$ $HOME/.poetry.venv/bin/pip install poetry
```

Comprobamos:

```shell
$ $HOME/.poetry.venv/bin/poetry --version
Poetry 0.12.17
```

¡El programa está instalado! Ahora creamos un enlace simbólico al punto de entrada en una carpeta visible en `PATH`, por ejemplo, en `$HOME/.local.bin`:

```shell
$ ln -s $HOME/.poetry.venv/bin/poetry $HOME/.local/bin
```

Comprobamos:

```shell
$ poetry --version
Poetry 0.12.17
```

¡Funciona! En el futuro, puedes actualizar el programa utilizando `pip` (que está en el entorno). También puedes automatizar completamente el proceso de instalación de este tipo de software de Python utilizando [pipx](https://pipxproject.github.io/pipx/).


#### Consideraciones especiales al usar poetry instalado en un entorno virtual.

Poetry está diseñado para trabajar con una versión abstracta de Python. Por lo tanto, se lleva bien con pyenv: uno se encarga de las diferentes versiones de Python y el otro se encarga de los proyectos en esas versiones.

Pero esta dependencia del comando `python` dificulta un poco las cosas cuando poetry está instalado en su propio entorno virtual: en este entorno, Python ya es conocido y no se puede cambiar. Esta característica se menciona en la documentación de poetry, por lo que no es un error sino una característica. Sin embargo, hay una forma de evitar esta limitación: puedes inicializar el entorno manualmente con la versión de Python que necesitas y configurar poetry para que use ese entorno ya creado.

Para empezar, enseñamos a poetry a crear entornos en la carpeta del proyecto en lugar de su caché:

```shell
$ poetry config settings.virtualenvs.in-project true
```

A partir de ahora, para cada proyecto, el entorno virtual se creará en el subdirectorio `.venv`.

Luego, en el proyecto específico, inicializamos el entorno con el siguiente comando:

```shell
$ python3 -m venv .venv
```

(para Py2, el comando será diferente, ya que el módulo `venv` no se incluía con el entorno en ese momento).

Ahora puedes trabajar con poetry como de costumbre. Aunque Python en el proyecto puede ser diferente al tiempo de ejecución que ejecuta poetry.
