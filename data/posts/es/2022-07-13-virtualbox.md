---
title: Cómo instalar Linux utilizando Virtualbox
subtitle: Instrucciones para instalar Ubuntu Linux dentro de Windows utilizando VirtualBox.
description: Instrucciones para instalar Ubuntu Linux dentro de Windows utilizando VirtualBox.
author: Kirill Mokevnin
hidden: true
---

Si estás utilizando una versión de Windows anterior a la 10 o si deseas obtener un sistema operativo Linux aislado con un entorno gráfico, puedes utilizar un software gratuito de terceros llamado VirtualBox.

Información general sobre la tecnología de [virtualización](https://guides.hexlet.io/virtualization/)

Necesitarás:

* El instalador de Oracle VM VirtualBox para Windows Hosts
Enlace de descarga: [Descargar Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)

* La imagen del sistema operativo Ubuntu Linux en formato ISO
Enlace de descarga: [Descargar Ubuntu Desktop](https://www.ubuntu.com/download/desktop)

Para empezar, debes instalar y ejecutar la aplicación VirtualBox.

![Página principal de VirtualBox](/assets/images/virtualbox/virtualization_2.png)

Haz clic en el botón "Crear", selecciona el tipo de sistema operativo "Linux" de la lista y, si no tienes preferencias específicas sobre la distribución, elige la versión "Ubuntu" de 32 o 64 bits. Puedes introducir cualquier nombre.

![Creación de una máquina virtual en VirtualBox](/assets/images/virtualbox/virtualization_3.png)

Indica la cantidad de memoria RAM asignada al sistema virtual. Se recomienda asignar 1024 MB.

![Selección del tamaño de la memoria RAM en VirtualBox](/assets/images/virtualbox/virtualization_4.png)

Indica el espacio en disco asignado al sistema virtual. Se recomienda asignar 10 GB.

![Selección del disco duro en VirtualBox](/assets/images/virtualbox/virtualization_5.png)

Puedes dejar el tipo de disco duro virtual como está: VDI (VirtualBox Disk Image).

![Selección del tipo de disco duro en VirtualBox](/assets/images/virtualbox/virtualization_6.png)

Elige el formato de almacenamiento de datos según tus preferencias personales. Un disco duro virtual dinámico crecerá a medida que se llene, mientras que uno fijo se creará con el tamaño especificado en el paso anterior.

![Selección del formato de almacenamiento del disco duro en VirtualBox](/assets/images/virtualbox/virtualization_7.png)

Puedes dejar el nombre y el tamaño del archivo sin cambios y hacer clic en el botón "Crear".

![Selección del nombre y tamaño del disco duro en VirtualBox](/assets/images/virtualbox/virtualization_8.png)

Una vez finalizado, se creará una máquina virtual, pero aún no tendrá un sistema operativo. Para instalarlo, debes descargar Ubuntu Linux (32 bits o 64 bits, según lo seleccionado en el paso donde se eligió el tipo de sistema operativo).

Al hacer clic en el botón "Iniciar", debería aparecer un cuadro de diálogo que te pedirá que indiques la ubicación de la imagen ISO descargada. Hazlo y haz clic en el botón "Continuar".

![Selección del disco de arranque en VirtualBox](/assets/images/virtualbox/virtualization_9.png)

La máquina virtual realizará automáticamente parte del proceso, pero en algunas operaciones se requerirá la intervención del usuario.

Selecciona el soporte de idioma en la lista de la izquierda y haz clic en "Instalar Ubuntu".

![Instalación de Ubuntu - Selección de idioma](/assets/images/virtualbox/virtualization_10.png)

Puedes descargar actualizaciones durante el proceso de instalación.

![Instalación de Ubuntu - Descarga de actualizaciones](/assets/images/virtualbox/virtualization_11.png)

Selecciona "Borrar disco y instalar Ubuntu" sin preocupaciones y continúa.

![Instalación de Ubuntu - Borrado del disco](/assets/images/virtualbox/virtualization_12.png)

Si seleccionaste el idioma español en el primer paso de la instalación, se te ofrecerá el teclado español como opción adicional.

![Instalación de Ubuntu - Selección del diseño del teclado](/assets/images/virtualbox/virtualization_13.png)

Completa los campos y selecciona el modo de inicio de sesión.

![Instalación de Ubuntu - Introducción de información del usuario](/assets/images/virtualbox/virtualization_14.png)

A continuación, se iniciará el proceso de particionado del disco, transferencia de archivos, instalación de actualizaciones y otros procesos que no requerirán la intervención directa del usuario.

![Proceso de instalación de Ubuntu](/assets/images/virtualbox/virtualization_15.png)

Una vez finalizado, la máquina virtual se reiniciará y accederás al entorno de Ubuntu Linux ya instalado.

Pero eso no es todo. Es muy recomendable instalar las llamadas "Guest Additions". Estas contienen controladores y otros archivos del sistema necesarios para obtener el mejor rendimiento y proporcionar funciones adicionales entre el sistema operativo virtual y el anfitrión.

Selecciona el menú "Dispositivos" del programa VirtualBox, luego "Insertar imagen de las adiciones para invitados" y espera a que aparezca la opción de ejecutar la aplicación desde la unidad virtual.

![Conexión de la imagen de las adiciones para invitados en VirtualBox](/assets/images/virtualbox/virtualization_16.png)

El sistema operativo virtual Ubuntu Linux está instalado y listo para su uso.

Enlace a la documentación oficial: [Manual de usuario de Oracle VM VirtualBox](https://www.virtualbox.org/manual/)
