---
title: Cómo configurar VS Code para desarrollar en PHP
subtitle: Creando un entorno de trabajo cómodo.
description: VS Code es un popular editor de código gratuito. Puede competir fácilmente con PHP Storm, ya que es gratuito y de código abierto.
image: "/assets/images/vscode-for-php-setup/vscode-php-cover.png"
hidden: true
author: Kirill Mokevnin
---

**[Visual Studio Code](https://code.visualstudio.com/) es un popular editor de código gratuito. Puede competir fácilmente con PhpStorm, ya que es gratuito y de código abierto.**

![Vscode](/assets/images/vscode-for-php-setup/screen.png)
_Así es como puede verse la interfaz del editor después de instalar las extensiones_

## Características principales

- Depurador de código
- Terminal integrado
- Herramientas convenientes para trabajar con Git
- Resaltado de sintaxis para muchos lenguajes populares y formatos de archivo
- Navegación conveniente
- Vista previa integrada de [Markdown](/markdown/)
- Autocompletado inteligente
- Administrador de paquetes integrado

VS Code tiene una gran cantidad de extensiones para desarrolladores. Para instalar un nuevo paquete, vaya a la pestaña "Extensions", escriba el nombre del paquete en la barra de búsqueda y haga clic en "Install".

![extension list](/assets/images/vscode-for-php-setup/recommended_extensions.png)

## EditorConfig para VS Code

[EditorConfig](https://editorconfig.org/) es un archivo de configuración y un conjunto de extensiones para muchos editores de código. Toma las configuraciones del archivo `.editorconfig`, que generalmente se encuentra en la raíz del proyecto.
La extensión configurará automáticamente las sangrías y los [saltos de línea](https://es.wikipedia.org/wiki/Salto_de_l%C3%ADnea) de manera uniforme para todos los desarrolladores que lo utilicen. El código PHP se ejecuta principalmente en sistemas *nix, por lo que es necesario utilizar el estándar.

<Banner name="profession-php" />

A continuación se muestra un ejemplo de archivo `.editorconfig` que se utiliza en Laravel:

```ini
root = true

# Configuraciones globales que se aplicarán a todos los archivos.
[*]
charset = utf-8
# En sistemas Unix, se utiliza lf para los saltos de línea.
# Esto también es un requisito del estándar PSR.
end_of_line = lf
insert_final_newline = true
indent_style = space
indent_size = 4
trim_trailing_whitespace = true

# Se pueden establecer configuraciones individuales para tipos de archivos específicos
# o archivos individuales por nombre.
[*.md]
trim_trailing_whitespace = false

[*.{yml,vue,js,html}]
indent_size = 2

[{package.json,.travis.yml}]
indent_style = space
indent_size = 2

[lib/**.js]
indent_style = space
indent_size = 2
```

## PHP Intelephense

El editor ya tiene soporte para la sintaxis y sugerencias de las funciones estándar del lenguaje. Pero sin una extensión especial, el editor no sugerirá las funciones personalizadas de otras partes del proyecto. Por lo tanto, para admitir el autocompletado, el análisis de código y la navegación a la ubicación donde se creó una función/clase/variable (usando el atajo `Alt+Click`), se utiliza la extensión [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)

Para evitar duplicar las sugerencias, es necesario desactivar el soporte de código PHP incorporado en el editor: `Extensions -> Buscar @builtin php -> PHP Language Features -> Desactivar`

![extension list](/assets/images/vscode-for-php-setup/intelliphense.gif)

![extension list](/assets/images/vscode-for-php-setup/intelliphense2.gif)

## PHP Debug

Durante el desarrollo, puede haber situaciones en las que las funciones de depuración y registro simples no sean suficientes. En ese caso, puede ser útil una herramienta especial: el depurador.
Para PHP, existe la extensión [xdebug](https://xdebug.org/), que permite establecer puntos de interrupción y ver el entorno en el lugar donde se produjo un error, ejecutando el código paso a paso hasta el siguiente punto.

Para utilizar [PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug), es necesario instalar XDebug por separado, ya que la extensión del editor no funcionará sin él. Después de instalar la extensión, es necesario agregar una configuración para PHP en la sección `Debug` del archivo `launch.json` que se creará en la raíz del proyecto después de seleccionar el lenguaje. La extensión creará el archivo con los parámetros predeterminados.

Para que XDebug se comunique con nuestro depurador, es necesario agregar configuraciones al archivo de configuración de PHP. Para encontrar este archivo, ejecute el comando `php --ini` en la terminal o ejecute un servidor web con el código `phpinfo()`.

En Linux, PHP carga no solo el archivo principal, sino también un archivo de esta carpeta. Por ejemplo, en Ubuntu, la ruta a la carpeta de archivos de configuración de PHP puede ser `/etc/php/7.3/cli/conf.d/`.
En esta carpeta, cree un archivo con los permisos necesarios (se requieren permisos de root):

```shell
$ sudo touch /etc/php/7.3/cli/conf.d/99-local.ini
$ sudo chmod 777 /etc/php/7.3/cli/conf.d/99-local.ini
```

El contenido del archivo:

```ini
xdebug.remote_enable=1
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000 ; El puerto que especificamos en launch.json
xdebug.idekey=code
xdebug.remote_autostart=1
```

Estas son configuraciones para el desarrollo local, cuando el proyecto se desarrolla y se ejecuta en la misma computadora, por ejemplo, en su máquina de trabajo.

![debug vscode](/assets/images/vscode-for-php-setup/xdebug2.gif)

![debug vscode](/assets/images/vscode-for-php-setup/xdebug1.gif)

![debug vscode](/assets/images/vscode-for-php-setup/xdebug3.gif)

## PHP Sniffer

En los lenguajes de programación, existe el concepto de _estilo de codificación_. Pero no todos los desarrolladores están al tanto de esto. El programa que se encarga de verificar si el código cumple con los estándares se llama linter. En PHP, se utilizan los estándares llamados [PSR](https://www.php-fig.org/psr/). Nos interesan los estándares PSR-1 y PSR-12, que se refieren a la codificación y las reglas de formato.

En PHP, se utiliza [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer#composer) como linter. Para que funcione, es necesario instalar el linter globalmente con `composer global require "squizlabs/php_codesniffer=*"` y la extensión [PHP Sniffer](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer).

Verifique que el linter se haya instalado correctamente:

```shell
$ phpcs --version
PHP_CodeSniffer version 3.4.2 (stable) by Squiz (https://www.squiz.net)
```

Puede ejecutar la verificación del código en la terminal utilizando el comando `phpcs`, especificando explícitamente el estándar que desea utilizar y la ruta a verificar:

```shell
$ phpcs --standard=PSR12 <dirname>
```

![vscode-phpcs](/assets/images/vscode-for-php-setup/phpcs-vscode.png)

![debug vscode](/assets/images/vscode-for-php-setup/phpcsfixer.gif)


## Semicolon Insertion Shortcut

PHP requiere que las instrucciones se separen con punto y coma. La extensión [Semicolon Insertion Shortcut](https://marketplace.visualstudio.com/items?itemName=chrisvltn.vs-code-semicolon-insertion) agrega el símbolo necesario al final de la línea con un atajo.
Si al presionar `[Ctrl] + ;` el símbolo no se inserta, verifique la lista de atajos de teclado y, si es necesario, asigne manualmente la combinación: `File -> Preferences -> Keyboard Shortcuts`

![semicolon-shortcut](/assets/images/vscode-for-php-setup/semicolon.png)

![semicolon-shortcut](/assets/images/vscode-for-php-setup/semicolon.gif)

## Extra

Aquí hay una lista de extensiones que se pueden utilizar no solo para PHP:

- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) — VS Code ya tiene soporte para Git. Pero cuando las funciones básicas no son suficientes, Gitlens puede ser de ayuda. Por ejemplo, una de las características útiles es `git blame` en la línea actual.

![gitlens](/assets/images/vscode-for-php-setup/current-line-blame.png)

- [Indent Rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) — colorea las sangrías en el código. Resalta las sangrías incorrectas. Puede cambiar el arco iris por tonos de gris.

![rainbow](/assets/images/vscode-for-php-setup/intend-rainbow.png)

- [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) — un complemento que permite sincronizar la configuración del editor entre diferentes computadoras. Utiliza Github Gists como almacenamiento en la nube. Puede descargar todas las configuraciones especificando el archivo de sincronización deseado.

- [Fira Code](https://github.com/tonsky/FiraCode) — una fuente monoespaciada que utiliza ligaduras (combina varios caracteres en uno) para combinaciones de caracteres comunes en programación. Una mejora visual para una lectura de código más cómoda.

![fira](/assets/images/vscode-for-php-setup/fira.gif)