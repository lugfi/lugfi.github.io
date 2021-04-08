---
layout: post
title:  "Presentación de yaml.ar"
author: colltoaction
categories: proyectos
---
# intro

hace diez años más o menos manijeo con la programación,
y en ese tiempo siempre me interesó
tanto la parte práctica de la ingeniería de software
como la parte teórica de la ciencia de la computación.

en este último año encerrado en cuarentena
aprendí mucho sobre programación funcional
incluyendo cálculo lambda, teoría de categorías
y categorías aplicadas a la programación.
al mismo tiempo, trabajando en Medallia
hice el paralelismo de la teoría
con mi propia práctica.

mi hipótesis es que yaml va a dar un salto
de lenguaje de configuración a lenguaje de programación.
esto se va a dar principalmente por:

- su ubicuidad
- lo fácil de interpretar como código su grafo de representación
- lo fácil que los programadores manipulan su flujo de presentación

hasta ahora todas mis pruebas de concepto fueron muy buenas y quiero seguir con esto.


# lisp

yo veo yaml como el mejor vehículo posible para transmitir lisp.
las listas tienen el formato más legible que vi:

```yaml
- lista
- de
- cuatro
- elementos
```

```yaml
[o, también, inline]
```

```yaml
- o
- - a
  - ni
  - [ da ]
  - da
```

es decir que todo código lisp, al estar basado en [S-expression]s,
tiene una representación en yaml de dichas expresiones.
no es casualidad que estos ejemplos sean muy legibles.
el modelo de presentación de yaml fue pensado para ser legible por humanos.

es trivial escribir un intérprete de yaml-lisp en muchos lenguajes
en que existen bibliotecas open source para ambos.
[el repositorio] contiene una implementación en rust usando serde y risp.

# cálculo lambda

ya vimos que yaml es legible y ejecutable como código lisp.
pasará lo mismo con el cálculo lambda?

esta rama de la matemática / computación nos da una herramienta más teórica
que un programa escrito en un lenguaje de programación de la industria.
en mi clase de programación funcional emulamos el cálculo lambda en clojure,
pero encuentro yaml mucho más legible:

```yaml
user=>
- println
- "What is this:"
- - +
  - 1
  - 2

What is this: 3
```

entonces implementé cosas en una sintaxis inventada,
y validaba si me parecía legible.
fue imposible no ver una semilla del lenguaje haskell
al empezar a encontrar papers y hacer mapeos desde la sintaxis de yaml.
en este punto me topé con [de bruijn] que todavía no sé bien cómo encaja.

# conclusiones

creo que lo más destacable es la efectividad del information model.
el [yaml representation graph] nos da un grafo acíclico dirigido
con la información necesaria para generar, por ejemplo, código.
el [presentation stream] nos permite a los humanos comprender y manipular yaml.

como me parece importante seguir investigando invito
de parte del grupo de software libre abierto de la fiuba
a todas y a todos a que se sumen.


[cálculo lambda]: https://en.wikipedia.org/wiki/Lambda_calculus
[yaml representation graph]: https://yaml.org/spec/1.2/spec.html#id2763754
[S-expression]: https://en.wikipedia.org/wiki/S-expression
[de bruijn]: https://www.cs.ru.nl/~james/RESEARCH/haskell2004.pdf
[presentation stream]: https://yaml.org/spec/1.2/spec.html#id2766150
[yaml.ar]: https://lugfi.github.io/proyectos/2021/02/27/propuesta-yaml-ar.html
[el repositorio]: https://github.com/lugfi/yaml.ar
