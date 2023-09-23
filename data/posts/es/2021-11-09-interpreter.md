---
title: ¿Qué es un intérprete?
# subtitle:
description: En esta guía, entenderemos qué es un intérprete, para qué se utiliza y cómo funciona. Este material te ayudará a comprender cómo el ordenador ejecuta programas.
image: "/assets/images/interpreter/interpreter.png"
author: Mark Shevchenko
---

En esta guía, entenderemos qué es un intérprete, para qué se utiliza y cómo funciona. Este material te ayudará a comprender cómo el ordenador ejecuta programas.

## ¿Para qué se utiliza un intérprete?

En inglés, la palabra "computer" se traduce como "ordenador". Estamos acostumbrados a utilizar el ordenador para preparar documentos, leer noticias y ver películas. En la vida cotidiana, rara vez tenemos que realizar cálculos, por lo que esta definición puede parecer extraña.

Sin embargo, este nombre refleja con precisión la naturaleza del ordenador. Aunque no lo veamos, el ordenador solo puede trabajar con números: los documentos, las noticias y las películas son solo conjuntos de números para el ordenador. Lo mismo ocurre con los programas que ejecuta.

Cada comando tiene su propio código numérico, llamado código de máquina: gracias a él, el ordenador sabe qué hacer. Es difícil para los humanos escribir programas en códigos de máquina, pero al principio de la era de los ordenadores, los programadores lo hacían de esta manera. Así es como se veían sus programas:

```
102 184 0 0
102 185 100 0
102 1 200
102 73
102 131 249 0
117 245
```

{/*
https://defuse.ca/online-x86-assembler.htm

0:  66 b8 00 00             mov    ax,0x0
4:  66 b9 64 00             mov    cx,100
00000008 <loop>:
8:  66 01 c8                add    ax,cx
b:  66 49                   dec    cx
d:  66 83 f9 00             cmp    cx,0
11: 75 f5
*/}

Para facilitar su trabajo, los programadores inventaron lenguajes de programación: son más comprensibles para los humanos, por lo que es más fácil escribir programas en ellos. En esta etapa, surgió un problema: si el ordenador solo entiende comandos en forma de números, ¿cómo ejecutará los comandos escritos en un lenguaje de programación?

Existen dos tipos de programas que ayudan a resolver este problema: los *intérpretes* y los *compiladores*. Puedes leer sobre los compiladores [aquí](/compiler/), en este texto nos centraremos solo en los intérpretes.

En resumen, un *intérprete* es un programa que ejecuta comandos escritos en un lenguaje de programación. Por ejemplo, un intérprete de Python entiende los comandos del lenguaje Python, y un intérprete de JavaScript entiende los comandos del lenguaje JavaScript.

## Un vistazo a la historia

Lisp resultó ser una invención exitosa. A lo largo de los años, las personas han inventado muchos lenguajes que resultaron ser innecesarios. Esto no se puede decir de Lisp, que sigue desarrollándose hasta el día de hoy. Aclararé que diferentes equipos se encargaron del desarrollo de los intérpretes de Lisp, por lo que obtuvieron diferentes versiones del lenguaje. Estas versiones del lenguaje se llaman *dialectos*. Además de Emacs Lisp, es posible que hayas oído hablar de [ClojureScript](https://github.com/HiroNakamura/curso-clojure), un dialecto de Lisp que a veces se utiliza en lugar de JavaScript para el desarrollo frontend.

Veamos un ejemplo de un programa en Lisp para comprender la diferencia entre el código de máquina y el "lenguaje casi humano":

```lisp
(defun sum (n)
    (if (= n 0)
        0
        (+ n (sum (- n 1)))))

(sum 100)
```

No es necesario conocer Lisp para ver que el programa tiene una estructura y comprender sus partes individuales. La accesibilidad para la comprensión es una ventaja significativa de los lenguajes de programación en comparación con el código de máquina.

Existen intérpretes para lenguajes de programación populares como Python y JavaScript. Son adecuados tanto para trabajar como para aprender a programar. Un factor importante en esto es que hay intérpretes disponibles para ellos, y más adelante entenderemos por qué.

## Ejemplo de intérprete de Python

Analizaremos en detalle cómo funciona un intérprete, escribiendo un programa sencillo que calculará la suma de los números del 1 al 100:

```python
sum = 0
for i in range(1, 101):
  sum = sum + i
print(sum) # => 5050
```

Ejecutaremos el intérprete de *python* y escribiremos el programa línea por línea.

![Ejemplo de trabajo del intérprete de Python](/assets/images/interpreter/example.png)

Vemos que al comienzo de cada línea, el intérprete muestra el indicador `>>>`. Cuando ingresamos el comando `for`, que consta de dos líneas, el indicador cambia a tres puntos `...`.

Al ejecutar el comando `print(sum)`, el intérprete imprime el resultado, que es el número 5050. Si cometemos un error, el intérprete nos indicará dónde se encuentra.

![Ejemplo de error en el programa](/assets/images/interpreter/error.png)

En el ejemplo anterior, olvidamos poner dos puntos después de la instrucción `for`, y el intérprete nos lo indica.

La respuesta inmediata del intérprete es muy importante al aprender un lenguaje. Los principiantes, al ver mensajes de error y probar diferentes opciones, rápidamente se familiarizan con la sintaxis desconocida. Es por eso que Python y JavaScript se utilizan a menudo para la enseñanza.

Los programadores experimentados también aprecian este enfoque *interactivo* de desarrollo, ya que les ayuda a probar rápidamente sus ideas.

Además, los lenguajes interpretados se utilizan a menudo para desarrollar prototipos de programas más grandes. En el modo interactivo, se ejecutan las mismas acciones una y otra vez: lee el comando del programador, lo ejecuta e imprime el resultado. Este modo se llama *bucle de lectura-evaluación-impresión*, o, en inglés, *Read-Evaluate-Print Loop* (REPL). Por lo general, se abrevia como REPL.

![Bucle de lectura-evaluación-impresión](/assets/images/interpreter/repl.png)

## Ejemplo de intérprete de JavaScript

El intérprete de JavaScript está integrado directamente en el navegador. Veamos cómo funciona en el navegador Chrome.

En la esquina superior derecha hay tres puntos verticales que abren el menú del navegador. Haz clic y selecciona "Herramientas adicionales" y luego "Herramientas de desarrollo".

![Herramientas de desarrollo de Chrome](/assets/images/interpreter/chrome-dev-tools.png)

Verás una nueva ventana llena de pestañas. Todas estas herramientas son útiles y vale la pena aprender a usarlas. Pero ahora solo necesitamos una pestaña: *Consola*. En la consola, podemos escribir comandos de JavaScript y ver de inmediato la respuesta del intérprete.

```javascript
a = 1; // => 1
b = 2; // => 2
3 * (a + b); // => 9
```

El intérprete guarda las variables `a` y `b` con los valores 1 y 2, luego calcula el valor de `3 * (a + b)` e imprime el resultado 9.

![Consola de Chrome](/assets/images/interpreter/chrome-console.png)

## Ejecución de un programa

El bucle REPL ayuda a desarrollar un programa, pero no es conveniente ingresar cada comando por separado: es mucho más rápido ingresarlos una vez y luego ejecutar el programa completo. Para hacer esto, crearemos un archivo de texto llamado *sum<span>.</span>py* y escribiremos los comandos allí:

```python
sum = 0

for i in range(1, 101):
  sum = sum + i

print(sum)
```

Para ejecutar el programa, simplemente necesitamos iniciar el intérprete de Python y especificar el nombre del archivo como parámetro:

```
> python sum.py
5050
```

El intérprete ejecuta los comandos uno por uno y luego finaliza su trabajo. Este modo de funcionamiento del intérprete se llama *modo por lotes*.

Por lo tanto, el intérprete puede funcionar en dos modos. El modo interactivo (REPL) nos ayuda a verificar ideas y encontrar soluciones a problemas. El modo por lotes ejecuta un programa completo.

## Estructura de un intérprete

Hay muchas formas de escribir un intérprete. No vamos a considerar todas las posibles opciones, sino que nos centraremos en la estructura general de los intérpretes. Un lenguaje de programación típico tiene varias docenas de comandos.

En el programa de Python que discutimos anteriormente, hay comandos de asignación, un bucle `for` y una llamada a la función `print`. Todos estos son comandos que el intérprete de Python entiende.
La estructura de un intérprete consta de un bloque de código para cada comando que el intérprete puede ejecutar.

La segunda parte importante de un intérprete es el analizador de texto. Cuando un programador ingresa texto, el analizador lo descompone en partes y comprende qué comando se está utilizando. Luego, pasa el control al bloque responsable de ejecutar ese comando.

Así es como funciona el intérprete en un bucle: analiza el comando ingresado, luego lo ejecuta, analiza el siguiente comando y lo ejecuta nuevamente. El análisis de texto no es una tarea trivial, pero tampoco es demasiado difícil, por lo que los intérpretes no son programas tan complejos en realidad.

![Cómo funciona un intérprete](/assets/images/interpreter/how-it-works.png)

## Ventajas y desventajas

Ventajas de los intérpretes:

* **Facilidad de aprendizaje.** REPL ayuda a verificar cómo funcionan las construcciones desconocidas y a aprender rápidamente la sintaxis del lenguaje.

* **Facilidad de programación.** Al igual que los compiladores, los intérpretes eliminan la necesidad de escribir programas en códigos de máquina.

* **Portabilidad.** Los intérpretes están diseñados para diferentes plataformas, como Mac, Windows y Linux, por lo que el programa que escribimos funcionará en todas las plataformas.

* **Mejora del programa a través del intérprete.** La velocidad de los programas depende no solo de la calidad del código, sino también de la velocidad del intérprete. Por ejemplo, los programadores de Google están constantemente mejorando el intérprete de JavaScript que se ejecuta en el navegador Chrome. Si escribimos un programa en JavaScript, con cada nueva versión de Chrome, funcionará más rápido, incluso si no cambiamos nada en él.

Desventajas de los intérpretes:

* **Baja velocidad.** Los programas interpretados funcionan más lentamente que los programas en códigos de máquina. Esto se debe a que el intérprete primero debe analizar el texto del comando y luego ejecutarlo. El programa en código de máquina es inmediatamente comprensible para el ordenador.

* **Dependencia del intérprete.** Un programa interpretado necesita un intérprete. En Windows, los programas en códigos de máquina tienen la extensión *.exe*. Puedes simplemente ejecutar un programa así, por ejemplo, el archivador 7-zip. Pero para ejecutar un programa en Python, necesitas el intérprete *python*.

* **Acceso al código fuente.** El código fuente en un lenguaje interpretado está disponible para el usuario del programa. El usuario puede ver lo que el autor del programa quería ocultar, como el método de cifrado de una contraseña o un algoritmo único.

* **Detección tardía de errores.** Los intérpretes ejecutan los programas comando por comando. Si hay un error en la sintaxis del comando, el intérprete no lo sabrá hasta que lo analice. En programas grandes, hay partes que se ejecutan con menos frecuencia que otras y es posible que haya errores que el programador no conozca. Para evitar errores que el usuario del programa verá, es necesario probarlo más a fondo.

## Conclusiones y recomendaciones

Un intérprete de un lenguaje de programación es un programa que ejecuta comandos escritos en ese lenguaje. Por ejemplo, decimos "intérprete de Python" o "intérprete de JavaScript".

El modo interactivo (REPL) ayuda a los programadores a aprender la sintaxis del lenguaje y a probar sus ideas.

Un intérprete consta de un analizador de texto y ejecutores de comandos individuales del lenguaje, como el bucle `for`, la comprobación `if` y la llamada a la función `print`, entre otros.

Las ventajas de los lenguajes interpretados incluyen la facilidad de aprendizaje. Es por eso que la programación a menudo se enseña utilizando lenguajes como Python y JavaScript.
