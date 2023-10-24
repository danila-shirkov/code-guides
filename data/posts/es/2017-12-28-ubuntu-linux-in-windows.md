---
title: Cómo trabajar con Linux utilizando Windows
subtitle: Instrucciones para instalar Ubuntu Linux dentro de Windows utilizando WSL.
description: Instrucciones para instalar Ubuntu Linux dentro de Windows utilizando WSL.
image: "/assets/images/ubuntu-linux-in-windows/virtualization_cover.png"
author: Kirill Mokevnin
---

Si estás comenzando tu camino como desarrollador y todavía estás utilizando un sistema operativo de la familia Microsoft Windows, seguramente te has encontrado con la situación en la que tus herramientas difieren de las que la mayoría de las personas en esta profesión utilizan. La mayoría de los problemas surgen al trabajar en la línea de comandos. El problema radica en que Windows no es un sistema operativo compatible con [POSIX](https://es.wikipedia.org/wiki/POSIX), por lo que carece de un conjunto básico de programas de aplicación necesarios para el desarrollo.

<Banner name="intensive-devops" />

A pesar de lo mencionado anteriormente, nuestra recomendación principal es instalar una distribución completa de Linux, como Ubuntu, e inmersión total en ella. La gran mayoría de los proyectos web se ejecutan en sistemas Linux. Y el uso constante de este sistema en tu computadora personal y de trabajo es equivalente a sumergirse en un entorno lingüístico al aprender idiomas extranjeros.

Para los principiantes, hay una forma más fácil y rápida: la virtualización. Vamos a hablar de eso.

## Ubuntu desde la Microsoft Store

Si estás utilizando una versión de Windows no inferior a la 10 con una arquitectura x64, puedes utilizar una solución integrada e instalar una capa de compatibilidad (Windows Subsystem for Linux) y luego una distribución basada en Ubuntu Linux a través de la tienda de aplicaciones de Microsoft Store.

El subsistema WSL se incluye con Windows, pero no está habilitado de forma predeterminada. Para activarlo, debes abrir PowerShell y ejecutar el siguiente comando:

```powershell
wsl --install
```

Este comando también descargará e instalará la distribución de Ubuntu Linux. Es posible que debas reiniciar tu computadora después de completar la instalación.

Después de reiniciar, busca la aplicación Ubuntu en el menú de inicio y ejecútala.

Es posible que la primera ejecución muestre un error `Error: 0x8007007e` y te ofrezca leer las instrucciones para solucionarlo en [https://aka.ms/wslinstall](https://aka.ms/wslinstall). Si quieres ahorrar tiempo, simplemente ejecuta PowerShell (no confundir con `cmd`) como administrador y ejecuta el siguiente comando:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Después de esto, tu computadora te pedirá que reinicies y luego debes volver a ejecutar la aplicación Ubuntu. Si la instalación fue exitosa, se abrirá el intérprete de línea de comandos y se te pedirá que ingreses un nombre de usuario y una contraseña. Se verá así:

```bash
Installing, this may take a few minutes...
Installation successful!
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username:
```

Los datos de inicio de sesión y contraseña no están relacionados con tu usuario de Windows, así que elige nuevos y no los olvides. Para cambiar la contraseña de Ubuntu en el futuro, necesitarás el comando `passwd`

Ten en cuenta las instrucciones oficiales de Microsoft, donde se explican no solo la instalación y configuración de WSL y Ubuntu, sino también la configuración del entorno de desarrollo (VSCode, Git)

* [Configuración del entorno de desarrollo de WSL](https://docs.microsoft.com/es-es/windows/wsl/setup/environment)
* [WSL + VSCode](https://docs.microsoft.com/es-es/windows/wsl/tutorials/wsl-vscode)

## Otros modos

Si no puedes instalar WSL, puedes utilizar otras opciones de virtualización para instalar Linux. Consulta nuestras otras guías:

* [VirtualBox](https://codica.la/guias/virtualbox)
* [Vagrant](https://codica.la/guias/vagrant)
