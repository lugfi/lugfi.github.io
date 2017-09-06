
---
layout: post
title: Activar spellcheck en Atom 
description: Guia de como activar el spellcheck en Atom en sistemas GNU/Linux
authors: alexdaciuk 
tags: lugfi programacion 
---

Hace unos días estuve escribiendo un post para la pagina de LUGFI y en las revisiones lo que mas me marcaban era la falta de tildes, acepto que nunca las aprendí a poner, así que me puse en campaña para hacer funcionar el spellchecker de Atom.
 
### Spellchecker en Atom

Por defecto viene instalado el paquete `spell-check` en Atom, pero hace falta configurar un par de cosas e instalar un par de paquetes mas en el SO para que funcione

### Hunspell

Yo elegí usar `Hunspell` para los diccionarios, desconozco si se pueden usar otros (capaz se pueda usar `myspell`, pero no probe, si lo prueban, digan que onda en los comentarios), en su distro probablemente ya venga instalado el paquete `hunspell` por defecto, pero necesiten instalar los diccionarios de los idiomas que piensan usar, en Arch y Debian, el paquete en español e ingles son `hunspell-es` y `hunspell-en` respectivamente, si quieren otros, es cuestión que los busquen en sus repos, hunspell tiene una considerable cantidad de diccionarios.

### Configurando

En el paquete `spell-check` va a haber 3 cosas que vamos a querer configurar, `Grammars`, `Locales` y `Locale Paths`

#### Grammars

Lista de *scopes* en los cuales el `spell-check` va a estar funcionando, esto básicamente es la lista de lenguajes en los cuales se va a chequear ortografía, una lista detallada de scopes la pueden encontrar [acá](https://gist.github.com/idleberg/fca633438329cc5ae327)

#### Locales

Lista de idiomas que se van a usar para los diccionarios, **observación**, aunque la documentación diga usar nombres del estilo `idioma-PAIS`, como usamos hunspell, el formato que usa para los nombres es `idioma_PAIS`, así que si quieren español Argentina es `es_AR` y si quieren ingles de Estados Unidos es `en_US`, separados por una coma.

#### Locale Paths

Es el directorio donde están nuestros diccionarios, en Arch y Debian es `/usr/share/hunspell`



Si configuraron bien todo, ahora en los scopes tendrían que tener corrector ortográfico


Saludos Alex!



