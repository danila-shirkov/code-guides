---
title: Lista de verificación de buenas prácticas de ingeniería en empresas
subtitle:
description: Hablamos sobre enfoques correctos para pruebas, implementación, desarrollo y procesos
image: "/assets/images/engineering-practice/check-list.png"
author: Kirill Mokevnin
---

El desarrollo de software es un proceso no trivial que tiende a complicarse significativamente a medida que aumenta el número de participantes. Cuantas más personas en el equipo, más comunicación y necesidad de sincronización (intercambio de conocimientos sobre partes del sistema y procesos en curso, seguimiento del negocio y sus requisitos). El costo de los errores aumenta, el sistema deja de caber en la cabeza de un solo desarrollador, los cambios en un lugar afectan a los cambios en otros lugares.

En estas condiciones, diferentes equipos se comportan de manera diferente. Algunos continúan manteniendo un ritmo de desarrollo alto y lanzan nuevas versiones regularmente. En otros equipos, los procesos se ralentizan significativamente: las negociaciones llevan más tiempo que el desarrollo, la calidad disminuye, lanzar una nueva versión se convierte en una fuente de estrés y aventura. La velocidad general de implementación de nuevas características en tales equipos puede diferir en gran medida e incluso en orden de magnitud.

<Banner name="intensive-devops" />

Hay muchas razones para esta diferencia catastrófica. Aquí hay algunos de ellos:

* Errores de alta dirección en el negocio. Si el negocio no hace lo que debe hacer, no importa cuán eficientemente lo haga, al final el negocio cerrará. Este tema está más allá del alcance de esta guía.
* Errores de alta dirección en los procesos. Si las cosas van mal a este nivel, todo lo demás es secundario. Incluso un sistema de bonificación incorrecto puede llevar a la discordia en el equipo y al bloqueo completo del desarrollo en última instancia.
* Factor humano. Las cualidades personales y los vicios humanos pueden crear problemas tanto para otros miembros del equipo como para todo el proyecto en general. El problema principal es que esta parte no se puede corregir con ningún proceso. Solo se puede cambiar el comportamiento. O separarse.
* Mal proceso de desarrollo. Este tema se aplica a todos los ingenieros sin excepción. Incluye todo, desde la interacción y el trabajo con tareas hasta las pruebas y la revisión de código.

Algunos problemas son difíciles o imposibles de influir (desde el nivel del desarrollador). Pero otros, especialmente relacionados con las prácticas de ingeniería, deben mejorarse y cambiarse constantemente. Los programadores deben participar activamente en esto.

* [Libros](https://codica.la/paginas/libros-recomendados)
    * Peopleware: Proyectos y equipos productivos
    * El mítico hombre-mes. Ensayos de ingeniería de Software
    * El limpiador de código. Código de conducta para programadores profesionales
    * La meta. Un proceso de mejora continua
* [Manifiesto por el Desarrollo Ágil de Software](https://agilemanifesto.org/iso/es/manifesto.html)
* [Bus Factor](https://es.wikipedia.org/wiki/Bus_factor)
* [Culto cargo](https://es.wikipedia.org/wiki/Culto_cargo)

Y aunque hay muchas prácticas, al final todo se reduce a qué tan rápido los clientes obtienen los resultados de su trabajo y qué tan satisfechos están con ellos. A continuación se muestra una lista de verificación que permite comprender si el equipo utiliza las prácticas de ingeniería que se consideran más exitosas.

_Cumplir con estas prácticas no garantiza que no haya problemas en la empresa. Puede ser un culto de carga o que los procesos estén tan formalizados que más obstaculicen que ayuden. Por otro lado, cada regla tiene excepciones y siempre habrá un proyecto en el que algo de la lista a continuación no sea aplicable. Y, finalmente, algunos de los enfoques mencionados pueden entrar en conflicto con los valores de alguien._

## Código

**Bien**

* [VCS](https://es.wikipedia.org/wiki/Control_de_versiones). El código está bajo control de versiones (generalmente Git).
* [Código compartido](https://es.wikipedia.org/wiki/Programaci%C3%B3n_extrema). Cualquier miembro del equipo puede cambiar cualquier parte del sistema en cualquier momento.
* [Estilo de código consistente](https://es.wikipedia.org/wiki/Programaci%C3%B3n_extrema). Todos en el equipo siguen los estándares de codificación establecidos para esa pila (lenguaje, plataforma).

**Mal**

* Falta de estilo consistente. Cada uno escribe código en el estilo al que está acostumbrado. No hay estándares comunes o, si los hay, son completamente diferentes de los aceptados en general.
* No se utiliza control de versiones. En su lugar, se utilizan copias de seguridad del código y los desarrolladores tienen que ponerse de acuerdo para no sobrescribir los cambios de los demás.
* El código tiene un "propietario". Los programadores protegen su parte del código de la interferencia de otros miembros.

**Enlaces**

* [Desarrollo basado en Trunk](https://trunkbaseddevelopment.com/)

## Entorno de desarrollo

**Bien**

* Entorno de desarrollo. El desarrollo se realiza en un entorno de desarrollo (dev) especial. Por lo general, es una máquina local (posiblemente utilizando Vagrant o Docker Compose). Este entorno es completamente propio de cada desarrollador y los cambios en un entorno no pueden afectar a otros entornos de desarrollo.
* La implementación del entorno está automatizada y se realiza con "un solo clic". Esto facilita la incorporación de nuevos miembros al proyecto, distribuir cambios de infraestructura rápidamente y de forma automática, trabajar sin miedo a romper algo, ya que es fácil de restaurar.
* Infraestructura como código. La propagación de cambios de configuración se realiza a través del código del proyecto. Solo es necesario ejecutar nuevamente la implementación del entorno de desarrollo (con nuevo código de proyecto) para que se apliquen todas las actualizaciones.
* El entorno de desarrollo es lo más similar posible a las condiciones de producción. Si el servicio se ejecuta en Linux, el desarrollo también se realiza en Linux. Lo mismo se aplica a otros aspectos.

**Mal**

* La implementación del entorno y la configuración se realiza mediante manuales o mediante "intento de ejecución, lectura del mensaje de error, búsqueda en Google, corrección". Es costoso e ineficiente. Los manuales se vuelven obsoletos casi de inmediato después de ser escritos. Una nueva persona puede pasar días implementando un entorno desde cero.
* Actualización manual de la configuración. Se envía una directiva a todos los desarrolladores para realizar cambios locales en la configuración del entorno (por ejemplo, agregar algo nuevo) para que el nuevo código funcione.
* Base de datos compartida para todos los desarrolladores. La carga de una persona afecta a todos. Una falla aleatoria también ralentiza a todos los demás.

## Calidad

**Bien**

* La base de código está cubierta por pruebas. Las pruebas aumentan la confianza en la funcionalidad del código. Las buenas pruebas tienen un impacto positivo en el diseño del código en sí. Por lo general, el código cubierto por pruebas es mejor que el código sin pruebas. Aunque hay una correlación.
* Una función parcialmente probada o incluso una función sin pruebas no se considera completa. Tener pruebas reduce significativamente la carga en todos los demás miembros del equipo y tiene un impacto positivo en la calidad de la solución del problema. Además, a menudo sucede que si no se escriben pruebas de inmediato, luego no habrá tiempo para ellas.
* El programador es responsable de la función hasta el final. La función se considera completa solo cuando funciona en producción. Cada persona en el equipo debe entender que el objetivo más importante es entregar valor al cliente. Mientras nadie esté utilizando las funciones, no importa si están escritas o no, porque el negocio se queda sin nada en ese momento.
* El equipo revisa el código de los demás (sin fanatismo). La revisión no solo es una forma de encontrar errores, sino también una forma de aprender unos de otros.
* [Programación en pareja](https://es.wikipedia.org/wiki/Programaci%C3%B3n_en_pareja). La técnica es efectiva no solo entre programadores. Es muy útil en parejas "programador y probador", "novato y experimentado".
* [Integración continua (CI)](https://es.wikipedia.org/wiki/Integraci%C3%B3n_continua). Los repositorios del proyecto están conectados a un servidor de integración continua, donde después de cada confirmación se verifica el estilo de codificación (a través de la ejecución de linters), se ejecutan pruebas y se realiza la construcción del proyecto (por ejemplo, compilación).
* En caso de incidentes, se realizan [post-mortem](https://kryptonsolid.com/realice-una-autopsia-de-incidente-para-la-mejora-continua-de-devops/).
* [Retrospectiva](https://openwebinars.net/blog/que-es-una-retrospectiva/). El proceso se mejora continuamente y cada miembro del equipo influye en los cambios.

**Mal**

* No hay pruebas. La funcionalidad nueva se verifica solo manualmente, haciendo clic. Las consecuencias son catastróficas: la velocidad de entrega es baja y es probable que la calidad del código sea insatisfactoria.
* No hay revisión de código. Diferentes estilos de codificación, aislamiento de los programadores entre sí, intercambio de experiencia deficiente, malas decisiones en producción.
* El programador considera que la función está completa cuando el código se fusiona en la rama principal. El nuevo código es una carga muerta y no aporta beneficios. Puede volverse obsoleto antes de que llegue al cliente.
* [KPI](https://es.wikipedia.org/wiki/Indicador_clave_de_rendimiento). Se utilizan activamente métricas cuantitativas: líneas de código, características lanzadas, errores cerrados. En lugar de orientarse a los resultados, los desarrolladores se esfuerzan por cumplir con los KPI. Incluso si esto va en contra de los objetivos del negocio.
* Alto nivel de formalización de los procesos. La velocidad disminuye, la motivación disminuye.

**Enlaces**

* [Programación Extrema](https://es.wikipedia.org/wiki/Programaci%C3%B3n_extrema)
* [Programación en pareja (presentación de Lucas Moy)](https://www.youtube.com/watch?v=odv-3GdPSys&ab_channel=ATLAcademy%28byLucasMoy%29)

## Proceso de desarrollo

**Bien**

* Los desarrolladores siguen los principios de [12 factores](https://www.aplyca.com/blog/12-factor-app-aplicaciones-exitosas-saas). Las aplicaciones son más fáciles de implementar, escalar y monitorear.
* Ejecutar una prueba individual toma fracciones de segundo. El desarrollo a través de pruebas implica una ejecución de pruebas muy frecuente durante el proceso de depuración. En tal situación, es muy importante que el inicio de una prueba específica sea lo suficientemente rápido como para que el desarrollador permanezca en contexto.
* Es fácil y agradable escribir pruebas. Esta es una prueba de fuego para determinar qué tan bien están las pruebas en el proyecto. Si tienes que obligarte a escribir pruebas, es probable que las pruebas estén escritas de manera deficiente (por ejemplo, con muchas simulaciones) y no sean suficientes.
* [Desarrollo guiado por pruebas (TDD)](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas). Si es posible, las pruebas se escriben antes del código. Hay varias razones por las que esto es importante:

    Las pruebas hacen que uno piense no en la implementación, sino en cómo se usará el código probado. Gracias a este enfoque, los programadores ven fallas en las interfaces en las primeras etapas.

    El código debe ser probado de todos modos. Si no hay pruebas, esto tendrá que hacerse manualmente.

* Antes de solucionar un error, primero se escribe una prueba que lo reproduce, luego se realiza la corrección. Solo en este caso, las pruebas realmente ayudan.

**Mal**

* Hay pruebas, pero tienes que obligarte a escribirlas porque son difíciles de escribir, tardan mucho en ejecutarse, a menudo fallan o tienes que reescribirlas constantemente.
* La ejecución de una prueba lleva segundos. Es difícil ejecutar una prueba así durante el desarrollo a través de pruebas y el tiempo total de ejecución de las pruebas se vuelve demasiado largo.
* El código se corrige directamente en producción (donde se ejecuta). Sin comentarios.

**Enlaces**

* [12 factores](https://12factor.net/es/)
* [Comenzando a escribir pruebas (correctamente)](https://codica.la/blog/how-to-test-code)

## Lanzamiento de nuevas versiones (más relevante para proyectos web)

El entorno de producción es la infraestructura (por ejemplo, servidores) en la que se implementa el proyecto. Proporciona acceso al proyecto a los usuarios finales.

La implementación (lanzamiento) es el proceso mediante el cual se actualiza el proyecto en el entorno de producción.

**Bien**

* Automatización. La implementación está automatizada y se realiza con un solo clic.
* Lanzamientos frecuentes y pequeños. La implementación es un evento común que puede ocurrir en cualquier momento cuando las funciones están listas, sin necesidad de distraer al equipo.
* Despliegue sin tiempo de inactividad. La actualización de la versión ocurre de manera transparente para los usuarios.
* La implementación técnica (es decir, todo está bien automatizado) puede realizar cualquier miembro del equipo.

**Mal**

* La implementación se realiza manualmente. Por ejemplo, a través del control directo desde el servidor. Este enfoque es el menos confiable y no escalable, propenso a errores y puede llevar mucho tiempo. Simplemente no funciona si hay varios servidores.
* La implementación del código va acompañada de tensión emocional y la participación de un gran número de participantes. En tal atmósfera, todos intentan implementar con menos frecuencia, lo que conduce a problemas aún mayores y perjudica directamente al negocio.
* El proceso de implementación lleva minutos u horas. Lo más probable es que esto signifique que el proceso de construcción del proyecto está integrado con la implementación en sí. Estas tareas deben realizarse de forma independiente.
* La implementación se realiza una vez a la semana o menos. Cuantos más cambios se implementen a la vez, mayor será la probabilidad de fallas. Y es más difícil rastrear el impacto de cada función en los indicadores comerciales. Además, se olvidan los cambios que se hicieron anteriormente y esperaron su momento para implementarse.
* Durante la implementación, se producen tiempos de inactividad prolongados. Los usuarios tienen que esperar a que se complete la implementación. Esta situación dificulta la implementación frecuente.
* La implementación la realiza una persona especializada. El conocimiento se almacena en una sola cabeza. Las vacaciones o enfermedades interrumpen todo el proceso. Otros programadores no entienden "cómo funciona allí".
* Implementación de configuración. Actualizar la configuración que no está directamente relacionada con la lógica del código requiere una nueva implementación. Por ejemplo, cambiar la contraseña de la base de datos o la dirección de la base. Estos parámetros son puramente infraestructurales y deben incluirse en el código según lo descrito en los 12 factores.

**Enlaces**

* [¿Qué es DevOps?](https://www.atlassian.com/es/devops)
* [Entornos de desarrollo. ¡Impleméntalos!](https://codica.la/blog/enviroment)
