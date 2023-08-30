---
title: ¿Qué es la virtualización y para qué se utiliza?
subtitle: En qué consiste esta tecnología y qué tipos de virtualización existen.
description: Aprende cómo crear un entorno aislado dentro de una sola computadora.
image: "/assets/images/virtualization/virtualization.png"
author: Kirill Mokevnin
---

A veces, los usuarios de Linux o Mac necesitan ejecutar programas que solo funcionan en Windows, y los usuarios de Windows, especialmente los programadores, necesitan ejecutar Linux u otra versión de Windows. Un ejemplo clásico son los juegos o Photoshop.

<Banner name="intensive-devops" />

La forma más obvia de hacer esto es comprar otra computadora, pero eso es costoso. Otra opción es instalar Windows junto con su sistema operativo principal. Esta instalación generalmente puede causar problemas, pero si lo logras, podrás elegir qué sistema operativo cargar al iniciar la computadora. Pero hay una tercera opción: la **virtualización**.

## Virtualización

**La virtualización es la creación de entornos aislados dentro de un solo dispositivo físico** (en este caso, una computadora). Cada entorno se ve como una computadora independiente con sus propias características, como memoria disponible, procesador, etc. Este entorno se llama una máquina virtual.

*¡La virtualización te permite ejecutar un sistema operativo como un programa normal en tu computadora!*

El sistema operativo en el que se ejecuta otro sistema operativo se llama **sistema anfitrión** (host), y el sistema operativo que se ejecuta en el entorno virtual se llama **invitado** (guest).

Un programa especial (que también es un sistema operativo) llamado **hipervisor** se encarga de crear y administrar las máquinas virtuales. El hipervisor proporciona aislamiento entre los sistemas operativos, protección y seguridad, y divide los recursos entre los sistemas operativos en ejecución. Dependiendo del tipo de virtualización utilizada, el hipervisor puede funcionar directamente con el hardware sin un sistema operativo anfitrión, o a través del sistema operativo principal instalado en la máquina anfitriona. En el primer caso, se utiliza la **virtualización de hardware**, y en el segundo caso, la **virtualización de software**. En las computadoras domésticas, el segundo tipo es más común.

A diferencia de la instalación de dos sistemas operativos uno al lado del otro en una máquina, la virtualización es un método mucho más seguro. Puedes deshacer todo en cualquier momento y reinstalarlo. Puedes crear tantas máquinas virtuales como necesites.

### Virtualización de hardware

Como su nombre indica, la virtualización de hardware funciona gracias al soporte del hardware, es decir, del procesador. A diferencia de la virtualización de software, los sistemas operativos invitados son controlados directamente por el hipervisor sin la participación del sistema operativo anfitrión.

La virtualización de hardware es mucho más eficiente que la virtualización de software, ya que el hipervisor, a diferencia del sistema operativo anfitrión, crea una sobrecarga muy pequeña. Por otro lado, la virtualización de software se divide en varios subtipos, que se pueden leer más detalladamente en [Wikipedia](https://es.wikipedia.org/wiki/Virtualizaci%C3%B3n).

### Virtualización de contenedores

La **virtualización de contenedores** es un caso aparte. A diferencia de los tipos anteriores, no está relacionada con la ejecución de un sistema operativo en un entorno aislado. En la virtualización de contenedores, el aislamiento ocurre a nivel de proceso del sistema operativo.

Actualmente, este tipo de virtualización solo existe en Linux y está disponible gracias a dos características del kernel: cgroups y namespaces. Estas características permiten ejecutar solo un proceso como si se estuviera ejecutando en su propio mundo, con su propia red, disco, sistema de archivos, etc. Este tipo de virtualización se utiliza para servicios que forman parte de un producto de software. Los proyectos más conocidos son OpenVZ, Docker y LXC.

## Alojamiento

Cada máquina virtual recibirá los recursos que especifiques. Esto es especialmente útil para los proveedores de alojamiento (empresas que ofrecen servicios de alojamiento web). Básicamente, se crea una máquina virtual separada para cada usuario con cuotas que corresponden al plan seleccionado (limitaciones de memoria, procesador, etc.).

Además, la virtualización aísla las máquinas unas de otras, por lo que no tendrás que preocuparte si los usuarios intentan dañar el sistema o a otros usuarios. Este servicio generalmente se llama VPS (servidor virtual privado) y es bastante económico en su configuración básica.

Las máquinas virtuales permiten utilizar de manera más eficiente los recursos de una máquina física. Por lo general, no todos los usuarios necesitan la potencia del hardware que tiene el proveedor de alojamiento, y no están dispuestos a pagar por ella. Sin embargo, una máquina virtual solo utiliza una fracción de la potencia del hardware, lo que permite alojar a decenas de clientes (o incluso más) en una sola máquina. Esto beneficia tanto al usuario como al proveedor de alojamiento.

## Preguntas frecuentes

### ¿Qué hacer si el procesador no admite virtualización?

Esto es muy poco probable, pero incluso en ese caso, aún puedes ejecutar una máquina virtual. Sin embargo, el rendimiento será muy bajo, ya que en realidad estarás utilizando virtualización de software en lugar de virtualización de hardware. En ese caso, es mejor actualizar el hardware a uno más moderno.

## Otros tutoriales relacionados

1. [¿Qué es Vagrant?](/vagrant/). Vagrant te permite crear y configurar entornos de desarrollo livianos, reproducibles y portátiles en máquinas virtuales.
2. [Cómo trabajar con Linux utilizando Windows](/ubuntu-linux-in-windows/). Instrucciones para instalar Ubuntu Linux dentro de Windows utilizando diferentes tecnologías de virtualización.