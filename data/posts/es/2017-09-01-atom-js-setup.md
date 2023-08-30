---
title: Cómo configurar Atom para el desarrollo de JavaScript
subtitle: Creando un entorno de trabajo cómodo.
description: Atom es un popular editor de código gratuito. Es fácil de configurar y ampliar para diferentes tareas y condiciones.
image: "/assets/images/atom-js-setup/atom.jpg"
hidden: true
author: Rahim Davletkaliyev
---

**[Atom](https://atom.io/) es un popular editor de código gratuito creado por los desarrolladores de GitHub para programadores. Se encuentra en constante desarrollo y cuenta con cientos de complementos, lo que lo hace fácilmente personalizable según tus necesidades.**

Atom está construido sobre la tecnología [Electron](https://electron.atom.io/), lo que significa que funciona en Windows, Linux y macOS. Algunas de las características básicas del editor, disponibles después de la instalación, son:

- Resaltado de sintaxis para varios lenguajes populares y formatos de archivo.
- Navegación conveniente.
- Vista previa integrada de [Markdown](/markdown/).
- Autocompletado inteligente.
- Gestor de paquetes integrado.

<Banner name="profession-frontend" />

El gestor de paquetes es necesario para instalar y desinstalar paquetes de extensión (complementos). Para facilitar el desarrollo de JavaScript tanto en el backend como en el frontend, es necesario instalar algunos paquetes.

![instalar paquete en atom](/assets/images/atom-js-setup/eslint.png)

Para instalar un nuevo paquete, ve a la configuración, selecciona la pestaña "Install", ingresa el nombre del paquete en la barra de búsqueda y haz clic en "Install".

## Estándares de codificación

**Eslint** es una utilidad que verifica los estándares de codificación en JavaScript. Es el estándar de facto en el mundo de JS.

![eslint atom](/assets/images/atom-js-setup/eslint-atom.png)

Primero, debes instalar eslint en tu sistema y luego instalar la extensión de Atom que utilizará el linter instalado. Hay diferentes formas de integrar el linter con la extensión. Vamos a ver cómo instalar el linter globalmente en el sistema.

1. Instala Node.js utilizando el [gestor de paquetes de tu sistema operativo](https://nodejs.org/en/download/package-manager/).
2. Instala eslint ejecutando el comando `npm install -g eslint`. Es posible que necesites usar `sudo`.
3. Instala los complementos que configuran `eslint`. Sin ellos (por defecto), `eslint` no realizará ninguna verificación.
	```shell
	npm install -g eslint-config-airbnb-base eslint-plugin-import
	```
4. eslint requiere un archivo de configuración. Crea un archivo `.eslintrc.yml` en la raíz de tu proyecto con el siguiente contenido:

	```yml
	extends:
	  - 'airbnb-base'
	env:
	  node: true
	  browser: true
	```
5. Instala la extensión "[linter-eslint](https://atom.io/packages/linter-eslint)" en Atom.
6. Marca la casilla *Use Global Eslint* en la configuración de la extensión (Settings -> Packages -> Linter Eslint).

## Autocompletado automático

El autocompletado integrado en el editor funciona mediante un análisis básico del contenido de los archivos. Con la ayuda de la utilidad externa "tern", puedes lograr un comportamiento más avanzado. "tern" puede:

- Sugerir argumentos de función.
- Determinar el tipo de expresión.
- Encontrar la definición de algo.
- Realizar refactorización automática.

![tern js](/assets/images/atom-js-setup/tern.png)

La extensión de Atom [atom-ternjs](https://atom.io/packages/atom-ternjs) no requiere la instalación de nada más y funciona por sí misma.

## Autocompletado de archivos y módulos

La útil extensión [autocomplete-modules](https://atom.io/packages/autocomplete-modules) completa automáticamente los nombres de archivos y módulos al importarlos.

![autocomplete-modules](/assets/images/atom-js-setup/autocomplete-modules.gif)

## Ir a la definición

[js-hyperclick](https://atom.io/packages/js-hyperclick) te permite ir rápidamente a la definición de una función o variable haciendo clic.

![js-hyperclick](/assets/images/atom-js-setup/js_hyperclick.png)