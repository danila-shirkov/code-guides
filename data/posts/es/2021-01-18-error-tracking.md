---
title: ¿Qué es el seguimiento de errores?
subtitle: Una forma rápida de encontrar errores en una aplicación de trabajo
description: |
  No hay programas sin errores. Lo mejor que podemos hacer es aprender a rastrear y corregir estos errores.
image: "/assets/images/error-tracking/error-tracking.png"
author: Kirill Mokevnin
---

No hay programas sin errores. Se puede reducir su cantidad utilizando sistemas de tipos, linters, pruebas o incluso un departamento de control de calidad completo, pero eliminarlos por completo es imposible. Esta es la realidad con la que vivimos y lo mejor que podemos hacer es aprender a rastrear y corregir estos errores de manera rápida.

## Cómo no trabajar con errores

Esto es lo que a menudo sucede en el desarrollo. Los programadores escriben algún código, lanzan una nueva versión del sitio web/aplicación y continúan con sus propias tareas. Mientras tanto, algunos usuarios encuentran problemas: algo se congela, los formularios no se envían, los datos se muestran incorrectamente, etc. Esto puede continuar durante mucho tiempo hasta que alguien enojado escriba un correo electrónico al servicio de soporte. Luego, este correo electrónico llega a los programadores, quienes intentan comprender quién cometió el error, dónde ocurrió y en qué circunstancias. Comienzan a investigar todos los detalles, posiblemente involucrando al cliente si está dispuesto a ayudar. Con este enfoque, una gran cantidad de errores pasan desapercibidos durante mucho tiempo y, lo más desagradable, los usuarios se van. ¿Se puede evitar esto? Resulta que sí.

<Banner name="intensive-devops" />

## Cómo trabajar con errores

Existen servicios llamados Rastreadores de Errores. Recopilan información sobre los errores que ocurren en tiempo real y notifican al equipo de desarrollo al respecto. Estos servicios funcionan con todas las plataformas existentes, desde televisores hasta aplicaciones móviles y sitios web (tanto el frontend como el backend).

![Panel de control de Rollbar](/assets/images/error-tracking/rollbar-dashboard.jpg)

Arriba se muestra un ejemplo del panel de control del servicio [rollbar.io](https://rollbar.io/), que se utiliza para todos los proyectos de Hexlet. El panel muestra la frecuencia de aparición de errores críticos en las últimas 24 horas en todos los proyectos. Este gráfico permite evaluar rápidamente las áreas que requieren mayor atención. A continuación se muestra la salida de errores de un proyecto específico. Según los íconos, la mayoría de los errores provienen de JavaScript en este momento.

![Proyecto de Rollbar](/assets/images/error-tracking/rollbar-project.jpg)

Cada uno de estos servicios proporciona bibliotecas para diferentes lenguajes y plataformas, que se integran en el código y se llaman cuando ocurren errores. Estas bibliotecas envían no solo el error en sí, sino también información sobre el entorno que puede ser útil. Esto puede incluir datos sobre el usuario, su navegador, la configuración de la aplicación, etc.

Idealmente, esta biblioteca se [integra](https://docs.rollbar.com/docs/rails) directamente en algún marco de trabajo, como Rails. Entonces no es necesario configurar casi nada, simplemente conecte la biblioteca como complemento al marco de trabajo y comenzará a recopilar errores por sí misma, sin intervención adicional. Si no hay una integración de este tipo, deberá escribir un poco de código para conectar su aplicación a la biblioteca. Para obtener más información sobre cómo hacer esto, consulte la documentación del servicio que elija. Aquí hay un [ejemplo](https://docs.rollbar.com/docs/react) de integración de Rollbar en React. Después de que todo esté configurado, el error capturado se verá más o menos así:

![Error de Rollbar](/assets/images/error-tracking/rollbar-error.jpg)

Observe el menú en la parte superior. Por los nombres de las pestañas, se puede ver cuánta información útil se extrae del error.

Pero atrapar el error es solo la mitad del trabajo. Luego, debe notificar al equipo de desarrollo de alguna manera, pero sin abrumarlos con spam. El problema es que los errores generalmente no ocurren una sola vez. Si el error es común y hay muchos usuarios, es posible capturar fácilmente el mismo error mil veces por minuto. Y si se enviara una notificación por cada ocurrencia (por correo electrónico o en Slack), ese servicio se desconectaría rápidamente de la fuente de energía.

![Error de Rollbar](/assets/images/error-tracking/rollbar-notifications.jpg)

Por lo tanto, estos rastreadores funcionan de manera inteligente. Cuando ocurre un error por primera vez, el servicio envía una notificación para que el equipo de desarrollo pueda reaccionar rápidamente al incidente. Si el error ocurre nuevamente, no se envían más notificaciones. Al menos no por cada ocurrencia. Por ejemplo, las notificaciones pueden enviarse en la primera, décima, centésima, milésima, etc. ocurrencia. Esta es la primera parte del mecanismo. Luego, cuando se implementa una nueva versión de la aplicación, los rastreadores marcan los errores como "corregidos". Esto facilita el seguimiento de los errores que se olvidaron corregir o que se corrigieron incorrectamente. Por lo tanto, generalmente después de la implementación, las notificaciones comienzan a llegar. Para que este mecanismo funcione, es necesario notificar al rastreador sobre las implementaciones. Puede encontrar más información al respecto en la [documentación](https://docs.rollbar.com/docs/deploy-tracking) del rastreador correspondiente.

## Conclusiones

Los rastreadores de errores no son un juguete, son una herramienta seria sin la cual no se puede imaginar ningún entorno de producción. Como rastreador, puede ser uno de los muchos servicios o un software especializado (como [Sentry](https://github.com/getsentry/sentry)) instalado en sus propios servidores en caso de requisitos de seguridad más altos.