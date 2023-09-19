---
title: Sistemas de numeración
description: En esta guía, aprenderemos qué son los sistemas de numeración, por qué los programadores utilizan formas inusuales de escribir números y cómo entenderlos
author: Mark Shevchenko
# redirect_from: /numeral-systems/
image: "/assets/images/numeral-systems/numeral-systems.png"
---

En esta guía, aprenderemos qué son los sistemas de numeración, por qué los programadores utilizan formas inusuales de escribir números y cómo entenderlos.

## Qué son los sistemas de numeración

Desde hace mucho tiempo, las personas han necesitado escribir números. En el comercio, los números son necesarios para saber cuántos productos hay en el almacén y cuánto dinero ha generado una transacción. Los registros de las posiciones de los cuerpos celestes ayudaron a los sumerios a crear el primer calendario, y el calendario, a su vez, fue útil para prepararse para la siembra y la cosecha. Los presupuestos de construcción, los censos de población, la distribución de herencias: los números resultaron ser muy demandados incluso en los estados más antiguos.

Así que las personas aprendieron a escribir números en tiempos inmemoriales. Los números pequeños se escribían fácilmente con muescas o marcas, pero si un número tenía varios dígitos, se necesitaba un sistema de escritura diferente. Este problema se resolvió de diferentes maneras en diferentes países.

Ahora llamamos a los diferentes métodos de escritura de números *sistemas de numeración*.

Se han inventado muchos sistemas de numeración, y hasta nuestros días utilizamos dos sistemas que se originaron en la antigüedad. De la antigua Roma nos llegó el *sistema de numeración romano*, en el que los dígitos se representan con letras del alfabeto latino. Los romanos tomaron como base la cantidad de dedos en una mano, que es 5, y en dos manos, que es 10. Los números 1, 5 y 10 en el sistema romano se representan con las letras I, V y X, y con ellas se puede escribir cualquier número del 1 al 49. Por ejemplo, VII es 7 y XIX es 19.

De los antiguos sumerios aprendimos a dividir las fracciones en sesenta partes. Es por eso que en nuestra hora hay 60 minutos y en un minuto hay 60 segundos. El sistema de numeración sumerio se llama *sexagesimal*. Pero, por supuesto, la forma más familiar de escribir números es la que se inventó en la antigua India. Ahora se llama sistema *decimal* o *arábigo*.

## De números decimales a binarios

Veamos cómo funciona el sistema decimal con un número grande arbitrario.

![1072](/assets/images/numeral-systems/example01.png)

Este es un número de cuatro dígitos porque consta de cuatro cifras. Y, dado que estamos hablando del sistema decimal, podemos usar diez dígitos diferentes.

![0123456789](/assets/images/numeral-systems/example02.png)

El valor que se oculta detrás de cada dígito depende de su posición, por lo que este sistema de numeración también se llama *posicional*. A la derecha, escribimos los valores más bajos, las *unidades*, a la izquierda de ellas, las *decenas*, luego las *centenas* y así sucesivamente. La escritura 1702 significa literalmente lo siguiente.

![1×1000+7×100+0×10+2×1](/assets/images/numeral-systems/example03.png)

Los dígitos escritos en posiciones adyacentes difieren en diez veces, y eso es lo que hace que sea un sistema decimal. Sin embargo, como mencionamos anteriormente, el sistema decimal que nos resulta familiar no es el único. Sin embargo, basándonos en él, nos resultará más fácil entender los principios de funcionamiento de otros sistemas de numeración. Por ejemplo, para escribir el mismo número 1702 en el sistema binario, debemos seguir las mismas reglas, pero en lugar de diez dígitos, solo necesitaremos dos: 0 y 1.

Los dígitos escritos en posiciones adyacentes diferirán no en diez veces, sino en dos. Es decir, donde en el sistema decimal vemos 1, 10, 100, 1,000, 10,000, en el sistema binario habrá números 1, 2, 4, 8, 16 y así sucesivamente.

![1×1024+1×512+0×256+ +1×128+0×64+1×32+0×16+ +0×8+1×4+1×2+0×1](/assets/images/numeral-systems/example04.png)

Este es un número binario muy grande. Vamos a escribirlo en la forma familiar:

![1 1 0 1 0 1 0 0 1 1 0 1024 512 256 128 64 32 16 8 4 2 1](/assets/images/numeral-systems/example05.png)

Este número podría ser un número decimal muy grande porque consta de los mismos dígitos. Para distinguir los números binarios de los decimales, se indica la base del sistema de numeración, es decir, 2.

![11010100110₂](/assets/images/numeral-systems/example06.png)

Esto es especialmente importante cuando en el texto se encuentran números decimales y binarios al mismo tiempo.

![11010100110₂ = 1702](/assets/images/numeral-systems/example07.png)

## ¿Por qué se necesita el sistema binario?

El sistema binario se ve muy inusual y los números escritos en él son enormes. ¿Por qué se necesita en absoluto? ¿No pueden las computadoras trabajar con el sistema decimal que nos resulta familiar?

Resulta que alguna vez lo hicieron. La primera computadora ENIAC, desarrollada en 1945, almacenaba números en el sistema decimal. Para almacenar un solo dígito, se utilizaba un esquema llamado registro de anillo, que consistía en diez tubos de vacío.

Para escribir todos los números hasta un millón, del 0 al 999,999, se necesitan seis dígitos, lo que significa que se necesitan 60 tubos para almacenar tales números.

![Registro de anillo](/assets/images/numeral-systems/ring-counter.png)

Los ingenieros se dieron cuenta de que si codificaban los números en el sistema binario, solo necesitarían veinte tubos para almacenar números tan grandes, ¡tres veces menos!

La primera ventaja de los números binarios es la simplicidad de los esquemas. La segunda, y no menos importante, es la velocidad. La suma de números almacenados en un registro de anillo requiere hasta diez ciclos de reloj del procesador por operación. La suma de números binarios se puede realizar en un solo ciclo, es decir, diez veces más rápido.

Un grupo de ingenieros que crearon la primera computadora publicó un artículo en 1946 en el que justificaban la ventaja del sistema binario para representar números en computadoras. El primer autor mencionado en el artículo fue el matemático estadounidense John von Neumann. Por eso, ahora los principios de diseño de las computadoras se llaman arquitectura de von Neumann, aunque esto no es del todo justo con respecto a otros inventores de la computadora.

Cuando se desarrolla un programa con una representación binaria, es bastante difícil encontrarse con él: en la gran mayoría de los casos, la computadora convierte los números binarios en decimales y viceversa. Puede escribir código durante mucho tiempo sin siquiera sospechar que dentro de la computadora los datos se almacenan de alguna manera especial.

¿Por qué estudiar el sistema binario si la computadora hace todo el trabajo por nosotros? A veces, los programadores tienen que escribir programas que trabajan directamente con hardware. Por ejemplo, los desarrolladores de juegos deben saber cómo funcionan las tarjetas de video para hacer que los gráficos de computadora sean más rápidos. Y los desarrolladores de sistemas operativos entienden cómo funcionan los discos para almacenar datos de manera confiable.

Los programas que trabajan directamente con hardware se llaman programas de sistema o de bajo nivel. Para crearlos, el desarrollador debe entender cómo funciona la computadora. Por lo tanto, el estudio de los sistemas de numeración permite al programador ampliar su rango profesional y convertirse en un especialista de amplio perfil.

Por lo tanto, para escribir programas de sistema complejos, es necesario comprender cómo funciona el sistema binario.

## Cómo convertir números binarios a decimales

Veamos cómo convertir rápidamente números binarios en decimales. Para este ejemplo, necesitaremos un número binario bastante grande para que no podamos calcularlo con los dedos.

![11010](/assets/images/numeral-systems/example08.png)

Escribámoslo en notación matemática, recordando que en lugar de la base 10, usamos la base 2.

![1×16+1×8+0×4+1×2+0×1](/assets/images/numeral-systems/example09.png)

A partir de este ejemplo, se puede ver que todos los sumandos tienen solo dos factores: 0 y 1. Los sumandos con el factor 0 son iguales a cero, por lo que se pueden descartar, dejando solo los sumandos con el factor 1.

![1×16+1×8+1×2](/assets/images/numeral-systems/example10.png)

EPara los sumandos con multiplicador 1, puede omitirse el multiplicador.

![16+8+2](/assets/images/numeral-systems/example11.png)

Ahora resulta fácil calcular la suma.

![26](/assets/images/numeral-systems/example12.png)

Conclusión: el número binario 11010 es lo mismo que el número decimal 26.

![11010₂=26](/assets/images/numeral-systems/example13.png)

Repitamos cómo convertir un número binario en decimal.

- Escribir el número en notación matemática
- Descartar los sumandos con el factor 0
- Sumar el resultado

Los programadores a veces memorizan algunas potencias de dos para poder estimar el orden de los números binarios. Puedes echar un vistazo a esta tabla:

|                    Número binario                   |   Potencia de 2   | Número decimal |
|----------------------------------------------------:|-----------------:|----------------:|
|                                        1<sub>2</sub>|   2<sup>0</sup>|               1|
|                                       10<sub>2</sub>|   2<sup>1</sup>|               2|
|                                      100<sub>2</sub>|   2<sup>2</sup>|               4|
|                                     1000<sub>2</sub>|   2<sup>3</sup>|               8|
|                                   1 0000<sub>2</sub>|   2<sup>4</sup>|              16|
|                                  10 0000<sub>2</sub>|   2<sup>5</sup>|              32|
|                                 100 0000<sub>2</sub>|   2<sup>6</sup>|              64|
|                                1000 0000<sub>2</sub>|   2<sup>7</sup>|             128|
|                              1 0000 0000<sub>2</sub>|   2<sup>8</sup>|             256|
|                             10 0000 0000<sub>2</sub>|   2<sup>9</sup>|             512|
|                            100 0000 0000<sub>2</sub>|  2<sup>10</sup>|           1 024|
|                    1 0000 0000 0000 0000<sub>2</sub>|  2<sup>16</sup>|          65 536|
|          1 0000 0000 0000 0000 0000 0000<sub>2</sub>|  2<sup>24</sup>|      16 777 216|
|1 0000 0000 0000 0000 0000 0000 0000 0000<sub>2</sub>|  2<sup>32</sup>|   4 294 967 296|

Con esta tabla, puedes convertir números de binarios a decimales prácticamente "de memoria".

![11010₂=10000₂+1000₂+10₂=16+8+2=26](/assets/images/numeral-systems/example14.png)

## Cómo convertir números decimales a binarios

Este problema es similar a un acertijo matemático y se puede encontrar en una prueba para los escolares.

Para aprender a resolverlo, echemos otro vistazo a los primeros números naturales en notación binaria y decimal.

| Número decimal | Número binario |
|-----------------:|-----------------:|
|                1 |    1<sub>2</sub> |
|                2 |   10<sub>2</sub> |
|                3 |   11<sub>2</sub> |
|                4 |  100<sub>2</sub> |
|                5 |  101<sub>2</sub> |
|                6 |  110<sub>2</sub> |
|                7 |  111<sub>2</sub> |
|                8 | 1000<sub>2</sub> |
|                9 | 1001<sub>2</sub> |

Observamos la siguiente regularidad: todos los números pares, como 2, 4, 6 y 8, terminan en 0 en la notación binaria. Todos los números impares, como 1, 3, 5, 7 y 9, terminan en 1. Esto tiene una explicación simple: en la notación binaria, el número 2 es como 10 en la notación decimal. Si un número binario es divisible por dos, es redondo. Los matemáticos dicen que los números pares son divisibles por 2 sin resto y los impares son divisibles por 1:

- al dividir 4 por 2, el residuo es 0;
- al dividir 5 por 2, el residuo es 1;
- al dividir 6 por 2, el residuo es 0;
- al dividir 9 por 2, el residuo es 1.

Intentemos convertir el número decimal 26 en binario. Para hacer esto, usemos la división larga por 2.

![Convertir número decimal en binario](/assets/images/numeral-systems/example24.png)

Si dividimos 26 por 2, obtendremos 13 como resultado, con un residuo de 0. Continuemos:
- al dividir 13 por 2, obtendremos 6 como resultado, con un residuo de 1;
- al dividir 6 por 2, obtendremos 3 como resultado, con un residuo de 0;
- al dividir 3 por 2, obtendremos 1 como resultado, con un residuo de 1;
- al dividir 1 por 2, obtendremos 0 como resultado, con un residuo de 1;

A partir de los residuos 1, 1, 0, 1 y 0, se forma la representación binaria deseada.

![11010](/assets/images/numeral-systems/example25.png)

Los números binarios se pueden convertir en decimales y viceversa utilizando el mismo enfoque. Para convertir un número decimal en binario, use el método `toString()` y pase la base del sistema como parámetro.

Por lo general, en JavaScript, podemos llamar a un método en un objeto usando un punto. Por ejemplo, si hemos almacenado un número en la variable `i`, podemos obtener su representación hexadecimal llamando al método `i.toString(16)`. Pero no podemos llamar a un método en el número 2, `2.toString(16)`, porque en JavaScript, el punto en la notación de números separa la parte entera de la fraccionaria. Si la parte fraccionaria es cero, no es necesario escribirla, por lo que "2." significa lo mismo que "2.0".

En el ejemplo, verá tres formas correctas de evitar este problema y llamar al método `toString()` en el número 26.

```javascript
console.log((26).toString(2)) // => '11010'
console.log(26..toString(16)) // => '1a'
console.log(26 .toString(8)) // => '32'
```

## Sistema octal

El sistema octal solía usarse junto con el sistema hexadecimal. Por el nombre, se entiende que utiliza solo ocho dígitos: 0, 1, 2, 3, 4, 5, 6 y 7. El sistema octal es adecuado para representar números binarios de seis, nueve y doce dígitos.

Estos números no son frecuentes. Uno de los ejemplos más conocidos de uso de números octales son los permisos de acceso en el sistema operativo UNIX. Se escriben como un número binario de nueve dígitos, por ejemplo, 110100100 o 111101100. Es incómodo memorizar y transmitir tales números, por lo que los programadores prefieren el sistema octal y escriben los permisos de acceso como 644 o 754.

Los sistemas operativos populares Linux y MacOS tienen sus raíces en UNIX, por lo que también utilizan números octales para los permisos de acceso.

![stat y chmod](/assets/images/numeral-systems/stat-chmod.jpg)

Los usuarios de UNIX utilizan el comando `stat` para conocer los permisos de acceso y el comando `chmod` para cambiarlos. En la imagen, puede ver que los comandos `stat` y `chmod` utilizan números octales. Una descripción detallada de estos comandos está más allá del alcance de nuestro artículo. Puede obtener más información sobre los permisos de acceso y qué significan estos números estudiando la línea de comandos de Linux.

En resumen, se puede decir que los números octales se utilizan muy raramente en la actualidad. En la gran mayoría de los casos, los programadores utilizan la notación hexadecimal.

## Conversión de números en programas

Los lenguajes de programación pueden trabajar con números escritos en diferentes sistemas de numeración y convertirlos de uno a otro. Para el ejemplo, consideremos cómo funcionan diferentes sistemas de numeración en Python y JavaScript.

### Python

Para escribir un número binario en Python, agregue el *prefijo* **0b** antes de él. Para los números hexadecimales, use el prefijo **0x**, y para los octales, **0o**.

```python
print(0b11010) # => 26
print(0x1a) # => 26
print(0o32) # => 26
```

En todos los casos, para escribir el número, escribimos primero el dígito cero "0" y luego la letra que determina el sistema de numeración. La letra "b" es la primera en la palabra "binary" (binario), y la letra "o" es la primera en la palabra "octal" (octal). La letra "x" es una excepción a la regla general, es la tercera letra en la palabra "hexadecimal" (hexadecimal).

Las funciones `bin()`, `hex()` y `oct()` convierten un número a los sistemas binario, hexadecimal y octal, respectivamente.

```python
print(bin(26)) # => '0b11010'
print(hex(26)) # => '0x1a'
print(oct(26)) # => '0o32'
```

Gracias a la notación de prefijo y las funciones `bin()`, `hex()` y `oct()`, podemos convertir números de cualquier sistema a cualquier otro.

```python
print(hex(0o32)) // >= '0x1a'
```

### JavaScript

En JavaScript, se utilizan los mismos prefijos que en Python. 0b11010, 0x1a y 0o32 son las representaciones del número 26 en los sistemas binario, hexadecimal y octal, respectivamente.

```javascript
console.log(0b11010) // => 26
console.log(0x1a) // => 26
console.log(0o32) // => 26
```

Para convertir números a otros sistemas de numeración, se debe llamar al método `toString()` y pasar la base del sistema como parámetro.

Por lo general, en JavaScript, podemos llamar a un método en un objeto usando un punto. Por ejemplo, si hemos almacenado un número en la variable `i`, podemos obtener su representación hexadecimal llamando al método `i.toString(16)`. Pero no podemos llamar a un método en el número 2, `2.toString(16)`, porque en JavaScript, el punto en la notación de números separa la parte entera de la fraccionaria. Si la parte fraccionaria es cero, no es necesario escribirla, por lo que "2." significa lo mismo que "2.0".

En el ejemplo, verá tres formas correctas de evitar este problema y llamar al método `toString()` en el número 26.

```javascript
console.log((26).toString(2)) // => '11010'
console.log(26..toString(16)) // => '1a'
console.log(26 .toString(8)) // => '32'
```

## Servicios de conversión de sistemas de numeración

Existen muchos servicios para convertir números de un sistema a otro. Incluso Google puede hacerlo.
Para convertir un número binario, por ejemplo, 11010, a decimal, debe ingresar la consulta **0b11010 decimal**.

![0b11010 decimal](/assets/images/numeral-systems/google01.png)

Para convertir un número decimal, por ejemplo, 26, a binario, debe ingresar la consulta **26 binary**.

![26 binary](/assets/images/numeral-systems/google02.png)

Ten en cuenta que Google utiliza el prefijo 0b para distinguir los números binarios de los decimales.

Para convertir un número decimal, por ejemplo, 137, a hexadecimal, ingrese la consulta **137 hex**.

![137 hex](/assets/images/numeral-systems/google03.png)

Para convertir un número hexadecimal, por ejemplo, 2BAD, a decimal, ingrese la consulta **0x2BAD decimal**.

![0x2BAD decimal](/assets/images/numeral-systems/google04.png)

Google utiliza el prefijo 0x para distinguir los números hexadecimales de los demás.
Para convertir el número 121 a octal, ingrese la consulta **121 octal**.

![121 octal](/assets/images/numeral-systems/google05.png)

Para convertir el número de vuelta, ingrese la consulta **0o171 decimal** en la barra de búsqueda.

![0o171 decimal](/assets/images/numeral-systems/google06.png)

Vemos que Google utiliza los mismos prefijos que vimos en los ejemplos de Python y JavaScript para representar números en los sistemas binario, hexadecimal y octal.

## Conclusión

Las personas inventaron diferentes formas de escribir números. Las llamamos sistemas de numeración. La forma familiar de escribir números se llama sistema decimal.

Las computadoras que funcionaban en el sistema decimal resultaron ser complicadas y lentas. Almacenar números en el sistema binario simplificó los esquemas y aceleró el trabajo de las computadoras.

Por lo general, no necesitamos saber cómo almacena la computadora los números, porque puede convertirlos a la forma que nos resulta familiar. Pero si queremos desarrollar programas que trabajen directamente con el hardware, como utilidades del sistema o juegos de computadora, debemos entender cómo funcionan los sistemas binario y hexadecimal.

Existen algoritmos que ayudan a convertir números de un sistema a otro, pero son bastante complicados. Es más fácil usar Google.

La representación binaria de los números es muy engorrosa, por lo que los programadores prefieren escribir números en el sistema hexadecimal. El sistema octal se usa muy raramente en la actualidad.

Puede convertir números de un sistema a otro en su lenguaje de programación favorito.
