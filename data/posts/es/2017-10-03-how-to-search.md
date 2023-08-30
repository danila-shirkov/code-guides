---
title: Cómo buscar información técnica
subtitle: Una pregunta bien formulada es la mitad del éxito.
description: La mayoría de los problemas a los que se enfrenta un principiante ya han sido resueltos y documentados. Solo necesitas aprender a encontrar esas soluciones y respuestas.
image: "/assets/images/how-to-search/how-to-search-title.png"
# redirect_from: /how-to-search/
author: Kirill Mokevnin
---

**Buscar respuestas a preguntas y solucionar problemas utilizando Google es una habilidad crucial para un programador. La mayoría de los problemas a los que se enfrenta un principiante ya han sido resueltos y documentados. Solo necesitas aprender a encontrar esas soluciones y respuestas.**

## Sitios web

Los principales sitios web con respuestas a preguntas son:

* [GitHub](https://github.com)
* [Stackoverflow](https://stackoverflow.com)

## Idioma

Según la práctica, al comienzo de su carrera, muchos programadores intentan encontrar respuestas formulando preguntas en el motor de búsqueda en ruso. A veces esto puede llevar a encontrar una respuesta, pero en la mayoría de los casos no. **El idioma principal de los programadores es el inglés**, ya que es el idioma que se habla en todo el mundo. La cantidad de información disponible en inglés es mucho mayor que en ruso, y además es más actualizada. Aprende a expresar tus pensamientos y, en el caso de la búsqueda, a escribir palabras clave en inglés. También te ayudará a aprender la terminología más rápidamente.

<Banner name="site-code-basics" />

## Motor de búsqueda

Esto está relacionado con el punto anterior. Debes buscar en Google. Aunque Yandex es bueno para ciertas tareas, el segmento en inglés no es su mercado principal y Google es mucho mejor en ese aspecto. Por ejemplo, notarás que después de un tiempo, Google se adaptará a tus consultas y comenzará a mostrar enlaces más relevantes. También es capaz de entender qué lenguaje de programación prefieres para mostrarte respuestas aplicables a ese lenguaje.

Otro punto importante es que Google es incluso mejor que las búsquedas específicas en sitios web particulares. Si necesitas encontrar algo en GitHub, es mejor formular una consulta adecuada en Google y obtener resultados más rápidos y precisos. A continuación, en la sección "Idioma de las consultas", se explica esto con más detalle.

## Idioma de las consultas

Cada motor de búsqueda tiene su propio lenguaje de consultas. Este lenguaje incluye operadores especiales que te permiten especificar con mayor precisión lo que estás buscando. Aquí hay algunas características importantes:

* `site:stackoverflow.com cómo probar código react` - la búsqueda se realizará solo en las páginas del sitio [Stackoverflow](https://stackoverflow.com/).
* `agregar clase a elemento -jquery` - el guion indica palabras clave que no deben aparecer en los resultados.
* `"immutable js"` - las comillas dobles indican que se debe buscar una coincidencia exacta.

Puedes encontrar una lista completa en [el sitio de soporte de Google](https://support.google.com/websearch/answer/2466433?visit_id=1-636424030566191968-2246914586&p=adv_operators&hl=en&rd=1).

## Búsqueda de bibliotecas

La gran mayoría de las bibliotecas se encuentran alojadas en [GitHub](https://github.com). Supongamos que necesitas encontrar una biblioteca para realizar solicitudes HTTP en JavaScript. Puedes formular la siguiente consulta: `github js cliente http`. Google te mostrará una docena de enlaces a diferentes repositorios. Por supuesto, también puedes usar el lenguaje de consultas: `site:github.com js cliente http`, pero en la mayoría de los casos, simplemente especificar `github` es suficiente.

La misma estrategia de búsqueda se puede utilizar para bibliotecas con nombres conocidos: `github express`.

## Búsqueda por mensaje de error

Antes de buscar por un mensaje de error, debes identificar dónde está el *mensaje de error*. A menudo, la salida de errores contiene mucha información que, aunque está relacionada con el problema, no describe el error en sí. Por ejemplo:

```shell
There was 1 failure:

1) App\SolutionTest::testResult with data set #2 (0, 2, 2, 1, 2)
Failed asserting that '1' matches expected 0.

/usr/src/app/tests/App/Tests/SolutionTest.php:15

FAILURES!
Tests: 3, Assertions: 3, Failures: 1.
Makefile:2: recipe for target 'test' failed
make: Leaving directory '/usr/src/app'
make: *** [test] Error 1
```

En esta salida hay mucho texto, pero el mensaje de error real es solo uno: `Failed asserting that '1' matches expected 0.`. En este caso, es más o menos claro qué salió mal y dónde buscar (el archivo y la línea se indican en la traza de la pila). Pero esto no siempre es así. Si logras identificar con precisión el mensaje de error, es útil hacer algo más. A menudo, estos mensajes son únicos. Contienen valores específicos de ciertos parámetros que son relevantes para tu entorno. Por ejemplo, rutas de archivos. Por lo tanto, si buscas en todo el texto del error, es probable que Google no encuentre nada. Por ejemplo, en el mensaje anterior, los parámetros son `'1'` y `0`. Si limpias la frase, obtendrás `Failed asserting that matches expected`. Eso es lo que debes buscar. También es útil agregar el nombre del lenguaje: `php Failed asserting that matches expected`.

## Búsqueda por comportamiento

A menudo, el mensaje de error no está presente o no puede conducir a una respuesta correcta (porque es una consecuencia, no una causa). En esta situación, debes ser creativo y formular una oración en inglés. También puedes usar un conjunto de palabras clave. Si la búsqueda no tiene éxito, es útil agregar `site:stackoverflow.com` a la frase de búsqueda. Stackoverflow es un lugar donde hay respuestas para casi todas estas preguntas.

Si sabes a qué biblioteca o programa se refiere el error, es útil encontrar su repositorio en GitHub y revisar la sección de Issues. Si el error es real y actual, es muy probable que alguien ya haya informado sobre él.

## Documentación oficial

La búsqueda es buena, pero nunca olvides la documentación oficial de las herramientas que estás utilizando (incluidos los lenguajes de programación). La documentación oficial (y no solo) generalmente se divide en varios tipos:

1. [Getting Started](https://guides.rubyonrails.org/getting_started.html) - una guía paso a paso (no siempre pequeña) para crear una versión mínima funcional. Esta es la primera cosa que debes buscar. Te permite comenzar rápidamente y ver la herramienta en acción.
1. [Guides](https://laravel.com/docs/5.5/routing) - descripciones de los componentes de la herramienta en cuestión. Están escritos en un estilo narrativo, lo que te permite leerlos de principio a fin. Los guías son útiles para estudiar bloques grandes.
1. [API](https://bit.ly/2uq98XM) - documentación detallada de todas las funciones posibles de la aplicación. Solo debes consultarla cuando busques respuestas a preguntas específicas.
1. [Tutorials](https://blog.codeship.com/an-introduction-to-apis-with-phoenix/) - a diferencia de las guías, se centran en diferentes formas de utilizar la herramienta.

---

*Kirill Mokevnin*