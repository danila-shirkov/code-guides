---
title: |
  Bootstrap en pocas palabras: qué es, para qué sirve y cómo funciona el framework
header: ¿Qué es Bootstrap y cómo funciona?
subtitle: Framework de front-end para el desarrollo web rápido y sencillo.
description: Hablamos sobre el framework para crear y diseñar sistemas front-end que los maquetadores suelen utilizar con frecuencia.
image: "/assets/images/bootstrap/bootstrap.png"
author: Nikita Mikhaylov
---

El desarrollo de una página web desde la perspectiva de un maquetador es un proceso continuo de mejora y creación de nuevos bloques. Cuanto más grande es el proyecto, más frecuentes son las iteraciones de "idea - funcionalidad - maquetación". Al resolver los problemas del negocio, las etapas deben resolverse de manera rápida y de calidad. Si bien la calidad de la maquetación depende directamente del maquetador, la velocidad es un factor que depende del equipo.

<Banner name="profession-markup" />

Para resolver el problema de la velocidad, los desarrolladores constantemente inventan nuevas herramientas. En el mundo de los maquetadores, estas herramientas se conocen como frameworks CSS, que son conjuntos de bloques, clases y funciones internas listas para su uso, que permiten un desarrollo rápido y conveniente.

En 2010, en las oficinas de Twitter, surgió el proyecto Twitter Blueprint. Su objetivo era crear un sistema para desarrollar nuevos componentes dentro de la empresa. Twitter Blueprint tenía un conjunto de bloques básicos con un diseño predefinido que se utilizaba en la empresa. Esta solución se hizo popular dentro de la empresa debido a su simplicidad, ya que cualquier empleado con experiencia mínima en desarrollo podía crear un nuevo concepto de bloque y proponerlo para su posterior desarrollo.

Ese mismo año, durante la semana de hackeo de Twitter, el proyecto ganó popularidad. No solo fue reconocido dentro de la empresa, sino también fuera de ella. Esta solución no podía seguir siendo un desarrollo interno y en 2011 el proyecto se lanzó al público bajo el nombre de Bootstrap. Desde entonces, Bootstrap ha mantenido su liderazgo entre las herramientas de creación de sitios web. Según diversas estadísticas, el framework se utiliza en el 17% al 30% de todos los sitios web en Internet. El código de Bootstrap se puede encontrar en sitios web de proyectos como:

* Hexlet,
* GitHub,
* PayPal,
* Spotify,
* Twitter,
* Duolingo.

Esta no es una lista exhaustiva de proyectos que utilizan Bootstrap. Por lo tanto, Bootstrap no es solo una biblioteca para crear paneles de administración y prototipos, como se suele decir.

## Bootstrap como conjunto de elementos listos para usar

Una de las características de Bootstrap es que se puede utilizar exclusivamente como un conjunto de elementos ya preparados. No se requieren conocimientos avanzados de HTML y CSS, solo es necesario saber cómo crear páginas básicas y leer la documentación. Por ejemplo, para crear un botón se utilizan dos clases, una para la estructura del botón y otra para el estilo. Este enfoque se llama **OOCSS** (CSS orientado a objetos). Puedes encontrar un artículo sobre este enfoque en el blog de Hexlet [aquí](https://ru.hexlet.io/blog/posts/oocss-basics).

``` html
<button class="btn btn-primary">Soy un botón azul</button>
```

El segundo enfoque que se utiliza en Bootstrap es el CSS atómico. Las utilidades en el framework se basan en este enfoque. **CSS atómico** es un enfoque en el que una clase utiliza una sola propiedad.

``` html
<section class="d-flex bg-white">
  <!-- Estructura HTML -->
</section>
```

En este ejemplo, la etiqueta `<section>` obtendrá dos propiedades:

1. `background-color: #fff;`
2. `display: flex;`.

El uso de utilidades requiere un conocimiento más profundo de CSS, ya que se asemeja al uso de reglas. Solo en lugar de escribir en un archivo CSS, se utilizan clases.

Los componentes y utilidades permiten crear proyectos de diferentes niveles de complejidad de manera muy rápida. La única limitación es la elección del diseño. Si no se modifican los componentes, la página se verá exactamente como en la documentación. Esto no es una desventaja, ya que Bootstrap es un framework moderno y su diseño no asusta a primera vista. Muchas pequeñas empresas utilizan este enfoque.

### Ventajas de utilizar Bootstrap como conjunto de elementos listos para usar

#### Velocidad

El proceso de desarrollo se acompaña de un trabajo continuo para agregar o eliminar funcionalidades en la página. Cuanto más grande es el proyecto, más frecuentes son estos procesos y la velocidad de implementación no depende en último término de cuán rápido la funcionalidad se "adapte" a la apariencia. Al utilizar componentes y utilidades predefinidos de Bootstrap, se puede agregar rápidamente nueva funcionalidad al sitio web y ofrecérsela a los usuarios. Esto resuelve uno de los problemas del ciclo "idea - funcionalidad - maquetación".

#### Compatibilidad entre navegadores

En el espacio web hay muchos navegadores diferentes: Chrome, Firefox, Edge, Opera, Safari, etc. Estos navegadores brindan a los usuarios una experiencia de navegación cómoda. Sin embargo, cada uno de estos navegadores puede interpretar HTML y CSS de manera ligeramente diferente, lo que obliga a los maquetadores a estandarizar los elementos estándar. Esta tarea requiere un enfoque meticuloso y conocimiento de los problemas y diferencias comunes entre los navegadores. Los componentes de Bootstrap tienen en cuenta las diferencias entre los navegadores y están optimizados para minimizar las diferencias entre ellos.

#### Adaptabilidad

Bootstrap tiene una cuadrícula de 12 columnas lista para usar en la que se pueden colocar componentes. La cuadrícula es el componente más popular de Bootstrap y es utilizado incluso por aquellos que son escépticos sobre el framework. La cuadrícula utiliza un enfoque que permite configurar la adaptabilidad de inmediato. Al utilizar componentes predefinidos, se puede estar seguro de que se verán bien en diferentes dispositivos.

#### Accesibilidad

Los desarrolladores prestan atención al uso de componentes por parte de personas con discapacidades. La documentación describe cómo hacer que los componentes sean accesibles. Pero incluso sin eso, los componentes tienen accesibilidad básica. Una de las clases más útiles relacionadas con la accesibilidad es `.sr-only`. Permite ocultar un elemento para todos los dispositivos excepto los lectores de pantalla. Esto es importante para organizar correctamente la maquetación de los formularios en el sitio web.

#### Baja barrera de entrada

Crear una página utilizando componentes no requiere un conocimiento experto de HTML y CSS. Esto permite que cualquier empleado de la empresa que tenga conocimientos básicos de maquetación pueda crear nuevos bloques. Por lo tanto, los desarrolladores pueden equipar una nueva solución con maquetación lista para usar utilizando el framework. Bootstrap también puede ser útil para pequeñas empresas que no están listas para gastar mucho dinero en el desarrollo de un sitio web. Bootstrap es una solución intermedia indispensable. Con el tiempo, es posible que decidan quedarse con él, como lo hemos hecho en Hexlet.

### Desventajas de utilizar Bootstrap como conjunto de elementos listos para usar

#### Tamaño del proyecto

El framework Bootstrap no solo proporciona un conjunto de clases, sino también componentes interactivos. Para su funcionamiento, se utilizan varias bibliotecas de JavaScript que aumentan el tamaño de los archivos que se cargan en la página. Bootstrap 4, junto con las bibliotecas de JavaScript, tiene un tamaño de ~ 300 KB. Esto puede ser un problema crítico en el desarrollo de aplicaciones móviles orientadas al uso en conexiones a Internet lentas. Ejemplos de tales aplicaciones pueden ser materiales de asistencia de emergencia, llamadas a servicios de rescate, etc.

#### Diseño

Los componentes estándar imponen restricciones al diseño. Estas restricciones se expresan en el hecho de que los componentes solo se pueden expandir hacia adentro, insertando unos dentro de otros. Modificar los componentes requerirá conocimientos de maquetación, ya que incluso los cambios menores deben ser probados en diferentes navegadores y resoluciones. A pesar de estas limitaciones, los componentes estándar de Bootstrap son concisos y ejemplares en términos de diseño. A pesar de su simplicidad, son funcionales y ayudan a presentar la información de manera adecuada. Incluso con estas limitaciones, se pueden crear sitios web hermosos y fáciles de usar gracias a un trabajo UI bien hecho.

#### Funcionalidad

Al igual que con el diseño, la funcionalidad de los bloques está predefinida y realizar cambios importantes puede requerir modificaciones significativas. Esto también se aplica a los elementos interactivos que utilizan código JavaScript. Los desarrolladores han agregado clases para estos elementos que ayudan a cambiar su comportamiento, pero esto no siempre es suficiente.

## Bootstrap como framework

Además de las herramientas de desarrollo, como el conjunto de componentes y utilidades, Bootstrap ofrece amplias posibilidades para crear componentes personalizados. Esto se logra gracias a la gran base de código en los archivos fuente.

¿Qué es un framework? Se puede imaginar como el esqueleto de una futura aplicación. Es una base especial en la que construiremos paredes, colocaremos ventanas y amueblaremos. Y eso es exactamente lo que es Bootstrap. Contiene docenas de funciones y mixins que permiten al maquetador crear su propio sistema de diseño. Esta funcionalidad es la más subestimada entre los desarrolladores y, por esta razón, Bootstrap ha adquirido una mala reputación.

Imagínate un nuevo componente que un desarrollador agrega a la página. Al utilizar Bootstrap, el desarrollo suele seguir el siguiente proceso:

* Se seleccionan componentes similares de la documentación.
* Se seleccionan nuevas clases para crear nuevos estilos.
* Se sobrescriben y agregan estilos adicionales para el bloque en un archivo CSS adicional.

Con este enfoque, incluso después de obtener los bloques necesarios, el desarrollador solo resuelve la tarea más cercana, pero puede tener dificultades a largo plazo. Todos ellos están relacionados con la falta de interacción entre el componente y el framework:

* Las actualizaciones del código base de Bootstrap no afectarán el comportamiento del componente. Los desarrolladores actualizan constantemente las versiones, realizando muchas mejoras y correcciones de errores.
* Cambiar la configuración no afectará al componente. Un caso común es cambiar el esquema de colores. Surge la necesidad de editar los colores de cada componente personalizado manualmente.
* La generación de nuevas utilidades se convierte en duplicación de código sin crear un sistema. Por lo tanto, se pueden crear nuevas utilidades para el color de fondo y el texto.

La creación de utilidades, a partir de Bootstrap 5, se resuelve mediante la adición de una nueva matriz que se pasa al procesador, lo que resulta en nuevas clases de salida. ¿Y cómo se crea un nuevo componente? En la mayoría de los casos, es suficiente revisar cuidadosamente el archivo _\_variables.scss_.

¿Qué se puede encontrar allí? Por ejemplo, colores que se utilizan como esquema de color:

```scss
$blue:     #0d6efd !default;
$green:    #198754 !default;
$cyan:     #0dcaf0 !default;
$yellow:   #ffc107 !default;
$red:      #dc3545 !default;
$gray-100: #f8f9fa !default;
$gray-600: #6c757d !default;
$gray-900: #212529 !default;

$primary:       $blue !default;
$secondary:     $gray-600 !default;
$success:       $green !default;
$info:          $cyan !default;
$warning:       $yellow !default;
$danger:        $red !default;
$light:         $gray-100 !default;
$dark:          $gray-900 !default;

$theme-colors: (
  "primary":    $primary,
  "secondary":  $secondary,
  "success":    $success,
  "info":       $info,
  "warning":    $warning,
  "danger":     $danger,
  "light":      $light,
  "dark":       $dark
) !default;
```

Hay muchos más colores en el archivo _\_variables.scss_, pero estos son los que forman el esquema de color base del proyecto. Puedes agregar nuevos colores, definirlos como base y después de la compilación, todos los componentes y utilidades obtendrán los nuevos valores. Es este comportamiento el que distingue al framework de un simple conjunto de componentes listos para usar.

Este tipo de trabajo con Bootstrap permite crear algo más que un simple prototipo, una página de destino o un panel de administración. En Hexlet, utilizamos Bootstrap en el tercer proyecto de maquetación para crear la apariencia de un chat completo.

![Aplicación de Bootstrap](/assets/images/bootstrap/bootstrap-chat.jpg)

Dado que Bootstrap es un conjunto de funciones y mixins, esto elimina las barreras para su uso junto con otras metodologías, como BEM. Esta es una opinión común de que es imposible usar Bootstrap junto con BEM. Echa un vistazo a los siguientes mixins disponibles para crear una cuadrícula:

```scss
@mixin make-container();
@mixin make-row();
@mixin make-col();
```

Si ya has trabajado con Bootstrap, encontrarás un esquema familiar en estos nombres: "Contenedor → Fila → Columna". Utilizando estos mixins, se puede agregar lógica del framework a cualquier proyecto y no estar limitado por la nomenclatura.

```scss
.search-form {
  @include make-container();

  &__content {
    @include make-row();
  }

  &__input,
  &__button {
    @include make-col-auto();
  }
}
```

De esta manera, se pueden agregar no solo elementos de la cuadrícula, sino también componentes y utilidades disponibles. Después de la compilación, no será necesario llevar consigo una gran cantidad de código que no se utiliza.

## Conclusiones

Aprender Bootstrap puede ayudar a desarrollarte como desarrollador. Además de escribir tu propio código, puedes estudiar el código de otras personas que ha sido creado y mantenido por miles de personas en todo el mundo. En el código, puedes encontrar soluciones interesantes, una estructura bien organizada y muchas funciones útiles. Gracias a esto, Bootstrap se puede utilizar en una variedad de escenarios, desde la creación de prototipos hasta la maquetación de diseños complejos, y la capacidad de utilizar partes individuales permite agregar un toque de Bootstrap a un proyecto sin tener que rehacer toda la estructura.

## Enlaces adicionales

* [Documentación de Bootstrap](https://getbootstrap.com/docs/5.0/getting-started/introduction/)
* [Repositorio de Bootstrap](https://github.com/twbs/bootstrap)
* [Bootstrap 5: Fundamentos de la maquetación](https://ru.hexlet.io/courses/bootstrap_basic)