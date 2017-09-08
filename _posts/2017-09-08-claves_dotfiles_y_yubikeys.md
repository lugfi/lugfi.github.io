---
layout: post
title: Claves, dotfiles y yubikeys
description: Manejo de claves y dotfiles usando una Yubikey
authors: tinchou
tags: lugfi unix seguridad
---

# Claves, `dotfiles` y yubikeys

## Motivación

Luego de una charla (más o menos básica) sobre seguridad y manejo de passwords en mi trabajo, me di cuenta de que era hora de hacer algo al respecto.

Imagino que muchos se identificarán conmigo: tengo conocimiento técnico, entiendo en gran medida mis faltas a la hora de manejar mis contraseñas, pero aún así caigo en los mismos problemas que todo el mundo al poner la comodidad por sobre la seguridad.

Esta charla coincidió afortunadamente con otra de mis deudas técnicas: hace tiempo quería armar mi repositorio de `dotfiles`, un lugar donde centralizar la configuración de mis programas. Cuando mencionaron la posibilidad de usar la utilidad [pass][pass] para guardar las contraseñas, encriptadas usando una clave GPG privada, decidí poner manos a la obra.

## Yubikey

Uno de los aspectos claves de la seguridad de este método es el uso de una clave GPG privada. En mi caso, estoy haciendo uso de un dispositivo físico para su almacenamiento: una Yubikey. Esto implica que la única manera de desencriptar mis claves es teniendo acceso físico a este dispositivo, y también conociendo su PIN de seis dígitos, ya que a los pocos intentos de descifrarlo por fuerza bruta se bloquearía.

## Dotfiles

Estando estas claves encriptadas, es posible almacenarlas en cualquier repositorio, incluso en aquellos en que no se confíe. Dropbox, Google Drive, incluso en un repositorio público Git! Y si están usando Git, también es posible usar la Yubikey como almacenamiento de la clave SSH, pero eso queda para otro post.

Es en este punto donde la tarea de los `dotfiles` cobra sentido. El programa `pass` almacena las claves en una carpeta en `$HOME` llamada `.password-store`. Siguiendo un sencillo [ejemplo de cómo usar GNU Stow][tuto-stow] creé mi repositorio de `dotfiles`, moví allí mis claves encriptadas, y estoy listo para comenzar a generar contraseñas seguras y almacenarlas _bajo llave_. Una explicación más detallada sobre `dotfiles` también queda, lamentablemente, para un futuro post.

## Siguientes pasos

Lo próximo que querría lograr es tener acceso a mis claves en mi teléfono Android. Gracias a la encriptación de las claves usando GPG (más allá de estar también el teléfono encriptado), no es problema tener en él una copia del repositorio.

Si tuviera una Yubikey moderna (con NFC), el problema sería trivial ya que existe el software adecuado. Hice pruebas conectándola al puerto USB-C sin éxito, pero es posible que sea cuestión de encontrar la app que tenga soporte. Parece que [Yubico Authenticator][auth] ya estuvo trabajando en esto, y por lo tanto es posible. Imagino que voy a abrir un _issue_ en [OpenKeyChain][okc] para solicitar soporte, pero incluso en el peor de los casos sé que podría hacerlo yo mismo gracias a que ambas apps son Software Libre.


[pass]: https://www.passwordstore.org/
[tuto-stow]: http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html
[auth]: https://github.com/Yubico/yubioath-android/issues/30
[okc]: https://www.openkeychain.org/
