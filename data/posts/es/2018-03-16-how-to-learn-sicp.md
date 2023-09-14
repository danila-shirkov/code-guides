---
title: Cómo estudiar Estructura e Interpretación de Programas de Computadora (SICP)
subtitle: Por qué y cómo estudiar uno de los libros más importantes en informática
description: Una guía sobre cómo leer uno de los libros de referencia en ciencias de la computación para cualquier desarrollador: SICP
image: "/assets/images/sicp/sicp.png"
author: Kirill Mokevnin
---

**SICP es un libro y un curso de estudio legendario en el MIT (Instituto Tecnológico de Massachusetts).**

SICP no es un libro sobre lenguajes de programación o desarrollo de software, no es un libro sobre programación orientada a objetos, programación funcional o patrones de diseño.

SICP es un libro sobre ciencias de la computación. Trata sobre la percepción de las computadoras como máquinas abstractas utilizadas para manipular datos. A pesar de que el libro fue publicado por primera vez en 1979, todavía es relevante y lo seguirá siendo en el futuro. SICP ha estado constantemente en la lista de los mejores libros de programación durante décadas.

<Banner name="course-racket" />

> Este es uno de los grandes clásicos de la ciencia de la computación. Compré mi primer ejemplar hace 15 años y todavía siento que no he aprendido todo lo que el libro tiene para enseñar. *— Paul Graham*.

¿Vale la pena leerlo? Definitivamente, todos los desarrolladores de cualquier lenguaje de programación y nivel de experiencia deberían leerlo. SICP es un libro bastante complejo, por lo que se ha creado esta guía que estás leyendo ahora.

## Resumen muy breve

### Abstracción mediante funciones

1. Elementos de programas
    * Expresiones
    * Estrategias de evaluación
    * Modelo de sustitución de evaluación
1. Funciones y los procesos que generan
    * Recursión lineal y recursión iterativa
    * Recursión en estructura de árbol
1. Funciones de orden superior
    * Funciones como argumentos
    * Funciones como abstracciones
    * Funciones como valores de retorno

### Abstracción mediante datos

1. Introducción a la abstracción de datos
    * Barreras de abstracción
    * ¿Qué son los datos?
1. Datos jerárquicos y propiedad de cierre
    * Representación de secuencias
    * Estructuras jerárquicas
    * Secuencias como interfaces estándar
1. Datos simbólicos
    * Citas
1. Representaciones múltiples de datos abstractos
    * Etiquetado de datos
    * Programación dirigida por datos. Aditividad.

### Modularidad, Objetos y Estado

1. Asignación y estado local
    * Ventajas de la asignación
    * Desventajas de la asignación
1. Modelo con entornos
    * Reglas de evaluación
    * Aplicación
    * Marcos como repositorios de estado local
1. Modelado con datos mutables
    * Lista mutable
    * Representación de colas
    * Representación de tablas
1. Multitarea
1. Hilos

### Abstracciones de metalingüisticas

...

### Cálculo con máquinas de registro

...

---

## Recomendaciones

Lo primero que hay que entender es que SICP no es solo un libro. Es un curso universitario presentado en forma de libro. Es difícil y extenso, y no tiene sentido estudiarlo sin práctica. No tendrás que inventar la práctica. Después de cada capítulo, hay un conjunto de ejercicios que los autores te piden que completes. Algunos de ellos son puramente matemáticos (te piden que demuestres algo) o requieren una buena base matemática. Puedes y debes saltarte algunos de ellos, de lo contrario, puedes perder la motivación rápidamente.

### Cuánto leer

SICP se puede dividir en dos partes. La primera parte incluye los capítulos 1, 2 y 3. La segunda parte incluye los capítulos 4 y 5. La diferencia es que la segunda parte aborda temas más profundos y solo puede ser superada por alguien realmente apasionado. Por esta razón, Hexlet recomienda establecer como objetivo completar los primeros tres capítulos. El resto se puede dejar para más adelante sin problemas.

### Lenguaje

Para los ejemplos y prácticas en el libro se utiliza el lenguaje Scheme, creado por los autores del curso. Es uno de los dialectos de la familia Lisp. Como cualquier lenguaje Lisp, Scheme tiene una sintaxis primitiva que se puede aprender en pocas horas. Es muy diferente de los lenguajes más comunes, pero tiene varias ventajas importantes que se mencionan en el libro.

La elección de Scheme como lenguaje principal para el curso se justifica porque permite centrarse en la esencia de las cosas en lugar de en la sintaxis, y permite ver conceptos puros en su forma original. Scheme, al igual que cualquier Lisp, tiene una expresividad increíblemente alta debido a que todo en el lenguaje es una expresión y no hay instrucciones en absoluto.

La segunda razón es la homoiconicidad. Esta es una propiedad de los lenguajes en los que los datos y el código son lo mismo. Es difícil entender esta tesis con palabras, hay que experimentarla en la práctica. También hay una tercera razón: los macros, pero no se utilizan en el libro.

El lenguaje Scheme es, en primer lugar, un estándar de lenguaje y hay diferentes implementaciones de este estándar. En este momento, uno de los descendientes más desarrollados y en constante desarrollo de Scheme es el lenguaje [Racket](https://racket-lang.org/). Hexlet recomienda estudiar SICP con Racket. Específicamente para esta guía, hemos preparado un [repositorio](https://github.com/hexlet-boilerplates/sicp-racket) que se puede utilizar como base para el código. Te recomendamos que eches un vistazo al repositorio al menos para aprender cómo configurar Racket para que sea compatible con el estándar de Scheme utilizado en los ejemplos de código del libro: pocas implementaciones existentes de Scheme permiten recrear el "entorno" en sí mismo, ¡pero afortunadamente Racket puede hacerlo! No olvides configurar correctamente tu editor: los lenguajes Lisp requieren soporte del editor para trabajar cómodamente.

## Formato

En GitHub [puedes encontrar](https://github.com/search?q=sicp) muchos repositorios que contienen soluciones a los ejercicios de SICP en varios lenguajes de programación. Recomendamos encarecidamente hacer lo mismo: crear un repositorio en tu cuenta y subir todas tus soluciones allí. Idealmente, cada solución debería ir acompañada de [pruebas](https://docs.racket-lang.org/rackunit/). Este enfoque es beneficioso no solo porque te permite mejorar tus habilidades en Git y obtener motivación adicional, sino también porque tendrás código que puedes mostrar cuando busques trabajo. Además, es muy probable que el entrevistador conozca SICP. Esto te dará puntos extra y te permitirá tener una conversación productiva.

## Enlaces adicionales

* [Curso: Estructura e Interpretación de Programas de Computadora (SICP en ruso)](https://www.youtube.com/watch?v=bFMbqKRjU84&list=PLo6puixMwuSO8eB2uBH5lZy5kjNtdhTfT)

* [Servicio para rastrear el progreso de estudio del libro](https://sicp.hexlet.io/)

* [Conferencia de los autores del curso con subtítulos en español](https://www.youtube.com/playlist?list=PLc6AqfeLgwzPPK1H3XV1Wfb_CGvT6sXkC)

* [SICP en Amazon](https://www.amazon.com/-/es/Gerald-Sussman-Julie-Harold-Abelson/dp/8173715270)
