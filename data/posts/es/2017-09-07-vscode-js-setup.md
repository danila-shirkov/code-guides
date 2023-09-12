---
title: Cómo configurar VS Code para el desarrollo de JavaScript
subtitle: Creando un entorno de trabajo cómodo.
description: VS Code es un editor de código gratuito de Microsoft. Es más rápido que Atom, está en constante desarrollo y se puede ampliar fácilmente con complementos.
image: "/assets/images/vscode-js-setup/vscode_eslint.png"
hidden: true
author: Rahim Davletkaliyev
---

**[Visual Studio Code](https://code.visualstudio.com/) es un popular editor de código gratuito creado por Microsoft para programadores. VS Code no está relacionado con Visual Studio. VS Code es más rápido que [Atom](https://atom.io/), está en constante desarrollo y se puede ampliar fácilmente con complementos.**

- Depurador de código
- Terminal integrado
- Herramientas convenientes para trabajar con Git
- Resaltado de sintaxis para muchos lenguajes populares y formatos de archivo
- Navegación conveniente
- Vista previa integrada de [Markdown](https://markdown.es/)
- Autocompletado inteligente
- Administrador de paquetes integrado

<Banner name="profession-frontend" />

El administrador de paquetes se utiliza para instalar y desinstalar paquetes de extensiones (complementos). Para facilitar el desarrollo de JavaScript tanto en el backend como en el frontend, es necesario instalar varios paquetes.

![instalar paquete en vs code](/assets/images/vscode-js-setup/vscode-install.png)

Para instalar un nuevo paquete, vaya al menú desplegable "View" en la pestaña "Extensions" e ingrese el nombre del paquete en el campo de búsqueda, luego haga clic en el botón "Install".

## Babel y ES6

VS Code tiene el concepto de "compilación de proyectos". Puede configurar el editor para que la compilación del proyecto JavaScript convierta el código de ES6 a ES5 legible con Source Maps utilizando Babel.

Agregue una tarea al archivo `tasks.json` en el directorio `.vscode` en la raíz de su proyecto:

```json
{
  "version": "2.0.0",
  "type": "shell",
  "tasks": [
      {
          "label": "watch",
          "command": "${workspaceRoot}/node_modules/.bin/babel src --out-dir dist -w --source-maps",
          "group": "build",
          "isBackground": true
      }
  ]
}
```

Ahora, la combinación de teclas `Shift+Ctrl+B` (Windows/Linux) o `Shift+CMD+B`(macOS) iniciará la compilación.

Puede obtener más información sobre las tareas en el sitio web de VS Code [aquí](https://code.visualstudio.com/docs/editor/tasks).

## Estándares de codificación

**Eslint** es una utilidad que verifica los estándares de codificación en JavaScript. Es el estándar de facto en el mundo de JS.

![eslint vscode](/assets/images/vscode-js-setup/vscode_eslint.png)

Primero, debe instalar eslint en su sistema y luego instalar la extensión de VS Code que utilizará el linter instalado. Hay diferentes formas de integrar el linter con la extensión. Veremos cómo instalar el linter globalmente en el sistema.

1. Instale Node.js utilizando el [administrador de paquetes de su sistema operativo](https://nodejs.org/en/download/package-manager/).
2. Instale eslint con el comando `npm install -g eslint`. Es posible que necesite usar `sudo`.
3. Instale los complementos que configuran `eslint`. Sin ellos (por defecto), `eslint` no realizará ninguna verificación.

    ```shell
    npm install -g eslint-config-airbnb-base eslint-plugin-import
    ```

4. eslint requiere un archivo de configuración. Cree un archivo `.eslintrc.yml` en la raíz de su proyecto con el siguiente contenido:

    ```yml
    extends:
    - 'airbnb-base'
    env:
    node: true
    browser: true
    ```

5. Instale la extensión "[linter-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)" en VS Code.

## Autocompletado

VS Code tiene un potente sistema de análisis de código para autocompletar y sugerencias: [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense).

![vs code intellisense](/assets/images/vscode-js-setup/javascript_javascript_intellisense.gif)

IntelliSense funciona de inmediato, pero para configurar los detalles, debe crear un archivo de configuración `jsconfig.json`.

### jsconfig.json

Si coloca un archivo de configuración `jsconfig.json` en el directorio raíz de su proyecto de JavaScript, VS Code utilizará esta configuración para trabajar con su proyecto. Aquí hay un ejemplo de dicho archivo:

```json
{
    "compilerOptions": {
        "target": "ES6"
    },
    "exclude": [
        "node_modules",
        "**/node_modules/*"
    ]
}
```

Aquí puede configurar, por ejemplo, qué directorios excluir del sistema de autocompletado IntelliSense. VS Code es compatible con node, webpack, bower, ember y otras herramientas populares. Puede encontrar la documentación completa sobre jsconfig [aquí en el sitio web de VS Code](https://code.visualstudio.com/docs/languages/jsconfig).

## Depuración

VS Code tiene un depurador de código integrado. Puede establecer puntos de interrupción y seguir el estado de la aplicación en tiempo real.

![vs code debugging](/assets/images/vscode-js-setup/javascript_debug_data_inspection.gif)

Para depurar el código del backend, las funciones integradas son suficientes. Para depurar el código del frontend, debe instalar un complemento para el navegador correspondiente:

- [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
- [Debugger for Firefox](https://marketplace.visualstudio.com/items?itemName=hbenl.vscode-firefox-debug)
- [Debugger for Edge](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-edge)

Puede obtener más información sobre la depuración en el sitio web de VS Code [aquí](https://code.visualstudio.com/docs/editor/debugging).

## Enlaces

[Curso](https://ru.hexlet.io/courses/js-setup-environment) sobre cómo configurar el entorno de trabajo para trabajar en el ecosistema moderno de JavaScript.
