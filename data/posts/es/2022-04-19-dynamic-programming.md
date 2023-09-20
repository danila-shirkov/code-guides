---
title: ¿Qué es la programación dinámica?
subtitle:
description: Aprende cómo resolver problemas de manera eficiente sin un algoritmo eficaz
author: Valery Zhila
---

El trabajo de un desarrollador a menudo se puede comparar con resolver rompecabezas. Al igual que en un rompecabezas real, el desarrollador tiene que gastar recursos significativos no tanto en implementar una solución específica, sino en elegir el enfoque óptimo. A veces, el problema se resuelve fácil y eficientemente, pero a veces solo se puede resolver probando todas las posibles combinaciones. Este enfoque se conoce como solución ingenua. Tiene una desventaja significativa: lleva mucho tiempo.

Imaginemos a un hacker que intenta descifrar una contraseña probando todas las combinaciones de caracteres. Si la contraseña permite 10 dígitos, 26 letras minúsculas, 26 letras mayúsculas y 32 caracteres especiales (como el símbolo del dólar), entonces hay 94 candidatos para cada carácter de la contraseña. Esto significa que se necesitarán 94 intentos para descifrar una contraseña de un solo carácter. Si la contraseña tiene dos caracteres, habrá 94 candidatos para la primera posición y 94 candidatos para la segunda posición, lo que significa que se tendrán que probar 94 * 94 = 8836 posibles combinaciones. Para una contraseña de diez caracteres, se necesitará probar 94^10 combinaciones.

En general, para descifrar una contraseña de longitud N, se requieren O(94^N) operaciones. Estos costos se llaman "exponenciales": cada nueva posición aumenta el número de operaciones en un factor de 94. Descifrar una contraseña puede parecer algo exótico, pero los problemas que requieren probar todas las posibles combinaciones no son exóticos en absoluto, sino una realidad sombría.

El tiempo exponencial es largo. Incluso O(2^N) es simplemente demasiado largo. Tan largo que nadie se le ocurriría ejecutar un algoritmo similar incluso en datos simples, ya que resolver un problema con cien elementos requeriría miles, millones o miles de millones de años de cálculos. Y en la vida real, hay que resolver problemas con muchos más elementos. ¿Qué se puede hacer?

La clave está en que muchos problemas sin un algoritmo eficiente se pueden resolver en un tiempo razonable utilizando una técnica inteligente llamada programación dinámica.

## Programación dinámica

La programación dinámica es un enfoque especial para resolver problemas. No hay una definición única de programación dinámica, pero intentaremos formularla. La idea es que a menudo se puede encontrar la solución óptima al considerar todas las posibles formas de resolver un problema y elegir la mejor entre ellas.

El trabajo de la programación dinámica es muy similar a la recursión con memorización de soluciones intermedias, también conocida como memorización. Los algoritmos recursivos suelen dividir un problema grande en subproblemas más pequeños y resolverlos. Los algoritmos dinámicos dividen el problema en piezas y las calculan secuencialmente, aumentando las soluciones paso a paso. Por lo tanto, los algoritmos dinámicos se pueden ver como una recursión que funciona de abajo hacia arriba.

![recursion_vs_dynamic_prog](/assets/images/dynamic_programming/recursion_vs_dynamic_prog.png)

La magia de la programación dinámica radica en el manejo inteligente de las soluciones a los subproblemas. "Inteligente" en este contexto significa "no resolver el mismo subproblema dos veces". Para lograr esto, las soluciones a los subproblemas deben almacenarse en algún lugar. Para muchos algoritmos dinámicos reales, esta estructura de datos es una tabla.

En los casos más simples, esta tabla consistirá en una sola fila, similar a una matriz regular. Estos casos se llaman programación dinámica unidimensional y requieren O(n) memoria. Por ejemplo, el algoritmo eficiente para calcular los números de Fibonacci utiliza una matriz regular para almacenar los resultados intermedios calculados. El algoritmo recursivo clásico realiza mucho trabajo innecesario: calcula repetidamente lo que ya se ha calculado en ramas recursivas adyacentes.

En los casos más comunes, esta tabla tendrá filas y columnas, similar a una tabla de Excel. Esto se llama programación dinámica bidimensional y requiere O(n*n) = O(n^2) memoria para n filas y n columnas. Por ejemplo, una tabla cuadrada de 10 filas y 10 columnas contendrá 100 celdas. A continuación, se analizará en detalle un problema de este tipo.

Existen problemas más complicados que utilizan tablas tridimensionales para su solución, pero son raros: resolver un problema utilizando una tabla tridimensional a menudo simplemente no es factible. Una pequeña tabla bidimensional con 1024 filas y 1024 columnas puede requerir varios megabytes de memoria. Una tabla tridimensional con los mismos parámetros ocupará varios gigabytes.

![1d_vs_2d_vs_3d](/assets/images/dynamic_programming/1d_vs_2d_vs_3d.png)


¿Qué se necesita para resolver un problema de manera dinámica, además de sus datos iniciales? Solo tres cosas:

* Una tabla en la que se almacenarán los resultados intermedios. Uno de ellos se seleccionará al final del algoritmo como la respuesta.
* Algunas reglas simples para llenar las celdas vacías de la tabla, basadas en los valores de las celdas ya llenas. No hay una receta universal y cada problema requiere su propio enfoque.
* Una regla para seleccionar la solución final después de llenar la tabla.

Analizaremos estos principios en un ejemplo.

## Ejemplo de resolución de un problema

El experimento demostrativo será el clásico problema de programación dinámica: la distancia de Levenshtein. A pesar de su nombre complicado, en realidad es un problema de transformar una palabra en otra mediante la adición, eliminación y reemplazo de letras con el menor número posible de operaciones.

Este problema se puede formular de la siguiente manera: encontrar la "distancia" mínima entre dos palabras. En este caso, la distancia es la cantidad mínima de operaciones que se deben realizar en la primera palabra para obtener la segunda (o viceversa).

Tenemos tres operaciones disponibles:

* insert: agregar una letra en cualquier lugar de la palabra, incluido el principio y el final
* delete: eliminar una letra de cualquier lugar de la palabra
* replace: reemplazar una letra en una posición específica por otra letra

Todas estas operaciones tienen el mismo costo: +1 a la distancia entre las palabras.

Tomemos dos palabras simples, MONEY y MONKEY. ¿Cuántas operaciones mínimas se necesitan para convertir MONEY en MONKEY? Un ojo humano ingenioso rápidamente se dará cuenta de que solo se necesita una operación: agregar la letra K entre la tercera y cuarta letra.

Ahora veamos un ejemplo más complicado. Intentemos convertir la palabra SUNDAY en la palabra SATURDAY y veremos que la cantidad de combinaciones que se deben probar puede ser muy grande. Si se resuelve por fuerza bruta, se pueden considerar todas las combinaciones posibles, al igual que en el ejemplo de descifrar una contraseña. En lugar de los 94 candidatos posibles para cada carácter, tenemos tres operaciones: insertar, eliminar y reemplazar. Tres combinaciones para la primera letra, 3 * 3 para las dos letras, 3 * 3 * 3 para las tres letras, 3^N para N letras. Una explosión combinatoria.

### Solución dinámica

Comencemos con la solución dinámica. Primero, creemos una tabla y coloquemos las palabras iniciales en los bordes, dejando un poco de espacio libre. Usaremos la segunda columna y la segunda fila para las cadenas vacías, que a menudo se denotan con el símbolo ε. Es similar a lo que quieres decir cuando usas una cadena vacía en tu lenguaje de programación: String eps = "".

|       |  ε   |  S   |  A   |  T   |  U   |  R   |  D   |  A   |  Y   |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| **ε** |      |      |      |      |      |      |      |      |      |
| **S** |      |      |      |      |      |      |      |      |      |
| **U** |      |      |      |      |      |      |      |      |      |
| **N** |      |      |      |      |      |      |      |      |      |
| **D** |      |      |      |      |      |      |      |      |      |
| **A** |      |      |      |      |      |      |      |      |      |
| **Y** |      |      |      |      |      |      |      |      |      |

Ahora llenemos la segunda columna y la segunda fila, siguiendo consideraciones completamente intuitivas: ¿cómo convertir una cadena vacía en una cadena? Por supuesto, agregando las letras necesarias. Por ejemplo, para convertir ε en SATU, se deben agregar las letras S, A, T y U. Cuatro operaciones. ¿Qué hacer con la conversión de ε a ε (segunda fila, segunda columna)? Es obvio: no se necesita hacer nada, cero operaciones.

|       |  ε   |  S   |  A   |  T   |  U   |  R   |  D   |  A   |  Y   |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |  3   |  4   |  5   |  6   |  7   |  8   |
| **S** |  1   |      |      |      |      |      |      |      |      |
| **U** |  2   |      |      |      |      |      |      |      |      |
| **N** |  3   |      |      |      |      |      |      |      |      |
| **D** |  4   |      |      |      |      |      |      |      |      |
| **A** |  5   |      |      |      |      |      |      |      |      |
| **Y** |  6   |      |      |      |      |      |      |      |      |

Ahora necesitamos un conjunto de reglas simples para llenar las celdas vacías de la tabla, basadas en los valores de las celdas ya llenas. La tabla se llamará D, y la primera fila y columna se mantendrán en los bordes. Trabajaremos con la tabla como si fuera una matriz bidimensional: D[0, 2] significa la celda en la intersección de la fila cero y la columna dos. En nuestro ejemplo, D[0, 2] = 2.

También llamaremos A a la palabra vertical y B a la palabra horizontal. Necesitamos esta pareja para tener acceso a las palabras originales en los bordes. Debido a las columnas adicionales para ε, los índices en A y B difieren de los índices en la tabla. Para ser más precisos, están desplazados en uno. A[0] = S, A[1] = U, A[2] = N, B[7] = Y, y así sucesivamente.

Finalmente, crearemos nuestra regla de llenado de la tabla. Para cada nueva celda, comprobamos las tres celdas vecinas: la de arriba, la de la izquierda y la de arriba a la izquierda en diagonal. De los tres números, se selecciona el más pequeño y se coloca en la nueva celda.

```
D[i, j] = minimum(
	D[i-1, j] + 1,                              // delete
	D[i, j-1] + 1,                              // insert
	D[i-1, j-1] + (A[i-1] == B[j-1] ? 1 : 0)    // replace
)
```

Este es un punto importante en la programación dinámica: las reglas pueden parecer sin sentido y puede ser difícil tener una imagen clara de lo que está sucediendo en la cabeza. Echemos un vistazo a un pequeño fragmento de la tabla, tal vez arroje algo de luz sobre algunos detalles.

|       |  ε   |  S   |  A   |
| :---: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |
| **S** |  1   |      |      |
| **U** |  2   |      |      |

¿Qué se debe escribir en la celda D[1,1] como resultado de la transición de S a S? Es intuitivo que no se necesita hacer nada para esto, cero operaciones. Escribamos un cero en la celda. ¿A qué se parece este valor, considerando que no se puede restar nada? Solo hay un cero entre los vecinos, en diagonal.

|       |  ε   |  S   |  A   |
| :---: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |
| **S** |  1   |  0   |      |
| **U** |  2   |      |      |

¿Qué se debe escribir en la celda D[2,1] como resultado de la transición de SU a S? Se debe eliminar la letra U, lo que significa que es una operación. Básicamente, el costo de la transición de SU a S será igual al costo de eliminar la letra U y la transición de S a S (cuyo costo ya se ha calculado y se encuentra en la celda D[1,1]).

|       |  ε   |  S   |  A   |
| :---: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |
| **S** |  1   |  0   |      |
| **U** |  2   |  1   |      |

Ahora veamos la celda D[1,2], la transición de S a SA. Sí, exactamente, el costo de la transición será igual al costo de agregar la letra A y la transición de S a S, un total de uno.

|       |  ε   |  S   |  A   |
| :---: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |
| **S** |  1   |  0   |  1   |
| **U** |  2   |  1   |      |

Finalmente, la celda D[2,2], la transición de SU a SA. La solución óptima sería reemplazar la letra U por la letra A, más el costo de la transición de S a S.

|       |  ε   |  S   |  A   |
| :---: | :--: | :--: | :--: |
| **ε** |  0   |  1   |  2   |
| **S** |  1   |  0   |  1   |
| **U** |  2   |  1   |  1   |

La celda inferior derecha contiene el costo final de la transición de la palabra SU a la palabra SA. De manera similar, se puede llenar toda la tabla. A partir de la celda D[6,8], sabemos que la transición de la palabra SUNDAY a la palabra SATURDAY cuesta al menos tres operaciones. En negrita, resaltamos la ruta óptima.

Veamos paso a paso. La transición de S a S no cuesta nada. La transición de S a SA cuesta una operación. La transición de S a SAT cuesta dos operaciones. La transición de SU a SATU cuesta dos operaciones. La transición de SUN a SATUR cuesta tres operaciones. La transición de SUND a SATURD cuesta tres operaciones (el costo de la transición anterior más el costo cero de la transición de D a D). La transición de SUNDA a SATURDA cuesta tres operaciones. Finalmente, la transición de SUNDAY a SATURDAY requiere las mismas tres operaciones.

Por cierto, si observamos la tabla, podemos ver que hay varias soluciones óptimas: desde D[1,2] se puede pasar tanto a D[1,3] como a D[2,2]. En esta formulación del problema, solo nos interesa la cantidad mínima, no la lista de todas las posibles rutas de solución, por lo que esto no es relevante.

|       |  ε   |   S   |   A   |   T   |   U   |   R   |   D   |   A   |   Y   |
| :---: | :--: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **ε** |  0   |   1   |   2   |   3   |   4   |   5   |   6   |   7   |   8   |
| **S** |  1   | **0** | **1** | **2** |   3   |   4   |   5   |   6   |   7   |
| **U** |  2   |   1   |   1   |   2   | **2** |   3   |   4   |   5   |   6   |
| **N** |  3   |   2   |   2   |   2   |   3   | **3** |   4   |   5   |   6   |
| **D** |  4   |   3   |   3   |   3   |   3   |   4   | **3** |   4   |   5   |
| **A** |  5   |   4   |   3   |   4   |   4   |   4   |   4   | **3** |   4   |
| **Y** |  6   |   5   |   4   |   4   |   5   |   5   |   5   |   4   | **3** |

Así es como se ven la mayoría de las soluciones en el mundo de la programación dinámica. Por cierto, esta solución tiene un nombre: el algoritmo de Wagner-Fischer. Un hecho curioso: este algoritmo fue publicado casi simultáneamente por diferentes grupos de científicos desconocidos de diferentes partes del mundo en una época en la que aún no existía Internet. Los señores Wagner y Fischer, por cierto, no fueron los primeros en hacerlo.

Ahora veamos cuáles son las diferencias entre la aplicación de este algoritmo y la solución por fuerza bruta.

### Análisis de la solución

Como se mencionó anteriormente, la solución por fuerza bruta de este problema utilizando recursión simple tiene una complejidad temporal de O(3^n), pero no requiere memoria adicional, es decir, O(1) operaciones en memoria.

¿Cuáles son los costos de la solución dinámica? Supongamos que se comparan palabras de igual longitud, con n caracteres en cada palabra. La solución se reduce a llenar una tabla con n+1 filas (una para la cadena vacía ε) y n+1 columnas. Esto significa que se utilizan (n+1)^2 celdas. No vamos a contar los detalles, así que redondearemos el número de celdas a n^2. Para cada celda, comprobamos tres de sus vecinos, lo que requiere tiempo constante O(1). Por lo tanto, llenar toda la tabla requerirá O(n^2) operaciones.

¿Cuál será el costo en memoria? Para una tabla con n^2 celdas, se requiere O(n^2) memoria.

Si las palabras tienen longitudes diferentes, se puede considerar la palabra más larga o aumentar la complejidad de la fórmula. Por ejemplo, si la primera palabra tiene longitud n y la segunda tiene longitud m, se requerirá O(nm) tiempo y O(nm) memoria.

## Conclusión

La idea principal de la programación dinámica debe ser evidente en el ejemplo presentado: sacrificamos una cantidad significativa de memoria (O(nm) en lugar de O(1)), pero obtenemos una ganancia de tiempo increíble (O(nm) en lugar de O(3^n)).

Enumeremos todas las características clave de la programación dinámica.

**Ventajas**:

* **Velocidad**: la principal ventaja de la programación dinámica. Los problemas insolubles se vuelven solubles en la mayoría de los casos en tiempo cuadrático. Una operación para llenar cada celda de la tabla y el problema está resuelto.

* **Universalidad**: One Ring to rule them all: la creación de un sistema compacto de reglas para llenar la tabla garantiza la solución del problema en cualquier conjunto de datos. Sin excepciones, sin casos límite, solo unas pocas líneas de código y el problema complejo está resuelto.

* **Precisión**: dado que el algoritmo de programación dinámica considera todas las posibles formas y escenarios de resolver un problema, encontrará la solución óptima. Sin pérdida de precisión, sin respuestas aproximadas. Si la solución existe, se encontrará.

**Desventajas**:

* **Memoria**: en la mayoría de los casos, los algoritmos de programación dinámica requieren tiempo para construir y llenar tablas. Las tablas consumen memoria. Esto puede ser un problema si las tablas en sí son muy grandes o si es necesario construir y mantener muchas tablas en memoria para resolver un problema.

* **Carga cognitiva**: resolver un problema complicado con un sistema compacto de reglas es una idea tentadora. Pero hay un inconveniente: para construir o incluso comprender estas reglas, es necesario aprender a "pensar en términos de programación dinámica". Esta es la razón por la cual la programación dinámica tiene una reputación controvertida.

## Áreas de aplicación

La programación dinámica no es una construcción teórica que se limite a los trabajos científicos. Es popular en muchas áreas aplicadas. Hay muchas de ellas: matemáticas aplicadas, ingeniería mecánica, teoría de control o pronóstico de datos financieros. Pero nos detendremos en una: la bioinformática.

Los científicos en este campo se dedican a "digitalizar" material biológico, así como a almacenar y analizar la información obtenida. Esta ciencia tiene cientos de aspectos fascinantes y plantea desafíos muy serios a los desarrolladores, ya que hay una cantidad increíble de datos. Por ejemplo, el genoma humano tiene alrededor de tres mil millones de pares de nucleótidos (los bloques de construcción del ADN). Por lo general, un par se codifica en un byte, lo que resulta en alrededor de tres mil millones de bytes de información para un solo genoma, tres gigabytes de datos para una sola persona.

Un solo genoma no presenta problemas graves, pero los genomas en sí mismos no son muy interesantes: para detectar mutaciones en el genoma de una persona en particular, primero debe "alinear" ese genoma con otros genomas de referencia (que ya están alineados y anotados). Puede haber muchas opciones posibles para esta alineación, pero debe encontrar la más probable. Por ejemplo, la opción con el menor número de mutaciones. Si tenemos en cuenta que el código genético generalmente se almacena como cadenas muy largas de diferentes letras, el ejemplo de la distancia de Levenshtein comienza a cobrar vida. Este problema, que potencialmente lleva a una explosión combinatoria (como probar todas las combinaciones posibles de caracteres para descifrar una contraseña), se resuelve maravillosamente con métodos de programación dinámica.

Si está interesado, lea sobre el [Alineamiento Múltiple de Secuencias (MSA)](https://es.wikipedia.org/wiki/Alineamiento_múltiple_de_secuencias)

Este es solo un ejemplo. La bioinformática vive y respira programación dinámica: aquí hay algunos ejemplos más:

* Construcción de árboles moleculares para determinar la secuencia de cambios evolutivos.
* Traducción eficiente de información genética (por ejemplo, de un trozo de piel) a una cadena larga en una base de datos.

Si hace 15 años, secuenciar un genoma completo tenía un costo de decenas de millones de dólares, hoy en día este servicio cuesta uno o dos mil dólares y sigue disminuyendo. Este salto se produjo no tanto debido al aumento de la potencia informática, sino debido a la aparición de algoritmos eficientes.
