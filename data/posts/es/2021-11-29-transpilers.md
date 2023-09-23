---
title: Qué es la transpilación
subtitle:
description: Conceptos básicos sobre la transpilación, problemas que resuelve y una breve descripción de sus implementaciones
image: "/assets/images/transpilers/transpilers.png"
author: Igor Kazantsev
---

Para comprender qué son los transpiladores y cuál es su papel en la programación, veamos el siguiente ejemplo. Supongamos que estás desarrollando software para decodificadores de televisión y necesitas agregar una calculadora a todos los decodificadores de una determinada marca. Sin embargo, hay un problema: algunos decodificadores no se han actualizado en los últimos 7 años y solo pueden ejecutar la versión antigua del lenguaje en el que está escrita la calculadora. Aquí es donde entra en juego la elección:

- Desarrollar el programa para dos tipos de decodificadores: la versión antigua del lenguaje para aquellos que no se han actualizado y la versión nueva para los más modernos.

![transpilers, cover](/assets/images/transpilers/cover.png)

- Utilizar un "traductor" que convierta la versión del lenguaje que estás utilizando en una versión que funcione en todos los dispositivos.

Los transpiladores desempeñan el papel de ese traductor: convierten el código en el que escribimos en otro código que puede ser utilizado y ejecutado por el usuario final en cualquier dispositivo con cualquier versión del lenguaje de programación.

**La transpilación** es la transformación de un programa escrito en un lenguaje de programación en una versión equivalente de ese mismo lenguaje o en otro lenguaje de programación del mismo nivel de abstracción.

## ¿Cuándo se necesita la transpilación?

Veamos un ejemplo práctico en el que la transpilación sería útil. Tomemos como base el caso de la actualización de software en decodificadores de televisión, pero agreguemos más detalles.

La calculadora se ejecuta en el navegador incorporado del decodificador de televisión y está escrita en JavaScript en su última versión. Además, los decodificadores se lanzaron cada año con un período de soporte limitado, por lo que ahora tenemos muchos dispositivos con diferentes versiones del navegador (y, por lo tanto, diferentes versiones de código JavaScript admitidas). Además, el navegador del usuario no se ha actualizado en mucho tiempo y el código JavaScript que puede ejecutar es muy diferente a las versiones actuales del lenguaje.

En esta situación, la transpilación del código sería muy útil. Los transpiladores nos ayudarían a convertir el código escrito en la última versión de JavaScript en uno que funcione en todos los usuarios, independientemente del tiempo transcurrido desde la última actualización.

## ¿Cómo se utilizan los transpiladores?

Los transpiladores se utilizan ampliamente en muchos campos de la programación. En general, se pueden destacar dos áreas principales de aplicación:

- Transpilación de una versión del lenguaje a otra. Dado que los lenguajes de programación se actualizan constantemente, surgen situaciones en las que el desarrollador ya está escribiendo en la nueva versión del lenguaje, pero el entorno en el que se utiliza el código solo admite versiones anteriores. Por ejemplo, para las transiciones entre las versiones del estándar ECMAScript se utiliza Babel. Los transpiladores permiten convertir el código en la dirección opuesta: por ejemplo, ayudan a migrar un proyecto a una versión más nueva del lenguaje. Hacer esto manualmente lleva mucho tiempo y es doloroso. Por ejemplo, si un proyecto está escrito en Python 2.x, se puede convertir a Python 3 utilizando el transpilador 2to3.

- Transpilación entre diferentes lenguajes. Por ejemplo, la conversión de TypeScript a JavaScript. Hablaremos más sobre esto a continuación.

## ¿Cómo funcionan los transpiladores?

Tomemos como ejemplo el trabajo de un transpilador en la elevación al cuadrado de código JavaScript:

```
a ** b
```

Así es como se vería la misma transformación utilizando el objeto Math, que se utilizaba para las operaciones de elevación al cuadrado en versiones antiguas del lenguaje:

```
Math.pow(a, b)
```

En este caso, tenemos un estado inicial y un estado final deseado. Sabemos que para el transpilador no será difícil realizar esta transformación. Sin embargo, para nosotros, el mecanismo de su funcionamiento aún parece una caja negra. Es hora de profundizar en los detalles y comprender cómo funciona la transpilación.

### Transformación del código fuente en una forma abstracta

En la primera etapa, el transpilador crea una representación abstracta basada en el código. En general, esta transformación ocurre en dos etapas: primero, el programa realiza un análisis léxico y luego un análisis sintáctico.

- El análisis léxico toma el código "en bruto" y lo divide en partes aisladas llamadas tokens. Estos pueden ser números, signos de puntuación, etiquetas, operadores, cualquier cosa. En nuestro caso, los tokens serían el operador binario (que se aplica a dos operandos, por ejemplo, 2 + 2) y sus operandos:

![transpilers, tokens](/assets/images/transpilers/tokens.png)

- El análisis sintáctico construye un objeto que describe todos los tokens y sus relaciones entre sí. Se llama AST (abstract syntax tree o árbol de sintaxis abstracta). El operador de elevación al cuadrado es una expresión binaria dentro del programa (en nuestro caso, la única), y los operandos se convierten en identificadores en esta expresión:

![transpilers, AST](/assets/images/transpilers/AST.png)

### Transformación del AST

Después de la transformación en un modelo abstracto, se realiza una transformación que realiza todos los cambios necesarios en el AST para su posterior procesamiento.

En esta etapa, el árbol del paso anterior cambia: la transformación reemplaza el operador de multiplicación por una llamada a la expresión, y los operandos se convierten en argumentos de la expresión (Math.pow):

![transpilers, transformedAST](/assets/images/transpilers/transformed_AST.png)

### Generación de código final

Una vez que se han realizado todos los cambios, el transpilador toma el AST transformado del código y genera un nuevo código en base a él.

![transpilers, generate](/assets/images/transpilers/generate_result.png)

En resumen, el código pasa por una serie de transformaciones (análisis -> transformación -> generación) hasta llegar a su estado final, y este proceso se llama transpilación.

### Retroalimentación

Después de todas las transformaciones, obtenemos un código final que funciona en la versión del lenguaje que necesitamos. Pero supongamos que después de la transpilación, aparecen errores en nuestro programa. ¿Cómo podemos entender dónde está el error si hace referencia a algún lugar en el código transpilado (que puede ser muy diferente de lo que escribimos originalmente)?

El uso de transpiladores puede dificultar la depuración cuando necesitamos encontrar el lugar exacto donde se produce el error en el código fuente original a partir del código transpilado. En estos casos, se utilizan diversas herramientas que permiten relacionar el resultado de la transpilación con el código original. Por ejemplo, en JavaScript existe una utilidad llamada SourceMap, que crea un archivo de mapeo durante la generación del código final, y con su ayuda se puede vincular el código original y el código final.

## Herramientas (implementaciones) de transpilación de código

Para el desarrollo frontend, la principal herramienta de transpilación es Babel. No solo permite realizar la transpilación entre versiones que hemos visto anteriormente, sino también:

- Convertir código JSX a JavaScript al desarrollar con React.
- Transformar LESS/SCSS a CSS al utilizar preprocesadores CSS.
- Transpilar TypeScript a JS cuando se necesita utilizar tipado.

Entre los transpiladores que transforman el código en lenguajes de programación backend en código en otros lenguajes, se utilizan ampliamente:

- Haxe, que se utiliza para transpilar a Flash, JavaScript y Neko. Con el tiempo, Haxe se ha convertido en un conjunto de herramientas que admiten la transpilación a diferentes lenguajes y plataformas, incluyendo JavaScript, C++, C#, Java, JVM, Python, Lua, PHP y Flash.
- Lombok, una solución para aquellos que desean ampliar las capacidades de Java. Es un complemento que agrega nuevas "palabras clave" a Java y convierte las anotaciones en código Java. Reduce el tiempo de desarrollo y proporciona funcionalidad adicional.
- Bridge.NET permite utilizar el rendimiento de C# en JavaScript, así como las potentes herramientas de VisualStudio IDE y las herramientas estándar de .NET.
- Grumpy realiza la transpilación de código Python a representación en Go y permite ejecutar programas de Python sin problemas en un entorno de ejecución de Go.

## Conclusión

En un mundo con una gran cantidad de lenguajes de programación y múltiples versiones de los mismos, los transpiladores desempeñan un papel muy importante al hacer que el desarrollo sea más conveniente. Los programadores pueden escribir código en el lenguaje o versión del lenguaje que les resulte más cómodo o que tenga las funciones necesarias, y los transpiladores se encargan de entregar ese código al entorno de ejecución en la forma requerida.

En la actualidad, existen muchas implementaciones de transpiladores diferentes (Babel, Vala, Typescript transpiler, Bridge, entre otros), cada uno de ellos resuelve su tarea a su manera, pero el principio general de funcionamiento de los transpiladores es similar en todos ellos.

![transpilers, scheme](/assets/images/transpilers/scheme.png)

El código fuente se transforma en un árbol de sintaxis abstracta, luego el AST se transforma en una estructura que se relaciona con el código final, y a partir de esta estructura se genera el código que necesitamos.

## Recursos adicionales

- [Sitio web para construir AST](https://astexplorer.net/)
- [Traducción del proyecto The Super Tiny Compiler! (El Súper Pequeño Compilador)](https://github.com/jamiebuilds/the-super-tiny-compiler)
