---
layout: post
title: Claves, dotfiles y yubikeys
description: Manejo de claves y dotfiles usando una Yubikey
authors: tinchou
tags: lugfi unix seguridad
---

# Claves, dotfiles y yubikeys

## Motivación

Luego de una charla (más o menos básica) sobre seguridad y manejo de passwords en mi trabajo, me di cuenta de que era hora de hacer algo al respecto.

Imagino que muchos se identificarán conmigo: tengo conocimiento técnico, entiendo en gran medida mis faltas a la hora de manejar mis contraseñas, pero aún así caigo en los mismos problemas que todo el mundo al poner la comodidad por sobre la seguridad.

Esta charla coincidió afortunadamente con otra de mis deudas técnicas: hace tiempo quería armar mi repositorio de `dotfiles`, un lugar donde centralizar la configuración de mis programas. Cuando mencionaron la posibilidad de usar la utilidad [pass][pass] para guardar las contraseñas, encriptadas usando una clave GPG privada, decidí poner manos a la obra.

## Yubikey

Uno de los aspectos claves de la seguridad de este método es el uso de una clave GPG privada. En mi caso, estoy haciendo uso de un dispositivo físico para su almacenamiento: una Yubikey. Esto implica que la única manera de desencriptar mis claves es teniendo acceso físico a este dispositivo, y también conociendo su PIN de seis dígitos, ya que a los pocos intentos de descifrarlo por fuerza bruta se bloquearía.

## Dotfiles

Estando estas claves encriptadas, es posible almacenarlas en cualquier repositorio, incluso en aquellos en que no se confíe. Dropbox, Google Drive, incluso en un repositorio público Git! Y si están usando Git, también es posible usar la Yubikey como almacenamiento de la clave SSH, pero eso queda para otro post.

Es en este punto donde la tarea de los `dotfiles` cobra sentido. El programa `pass` almacena las claves en una carpeta en `$HOME` llamada `.password-store`. Siguiendo un sencillo [ejemplo de cómo usar GNU Stow][tuto-stow] creé mi repositorio de `dotfiles`, moví allí mis claves encriptadas, y estoy listo para comenzar a generar contraseñas seguras y almacenarlas _bajo llave_. Una explicación más detallada sobre `dotfiles` también queda, lamentablemente, para un futuro post.

## Android

Cuando escribí la primera versión de este post, en un frenesí de hacer más seguro mi almacenamiento de contraseñas, creí que había perdido la habilidad de sincronizarlas y acceder a ellas desde mi teléfono Android. 

Si tuviera una Yubikey moderna (con NFC), ni habría dudado. Múltiples apps como [Yubico Authenticator][auth] o [OpenKeyChain][okc] afirman tener soporte para esto, pero ninguna hace explícita mención de soporte para conexiones USB (protocolo USB OTG, presente en muchos teléfonos). Revisando reportes en repositorios Github y haciendo pruebas, finalmente lo conseguí! Uno puede usar [Password Store][pass-store] para sincronizar el repositorio de claves, elegir OpenKeyChain como agente de autenticación, y habiendo configurado la Yubikey desencriptar las claves de forma transparente.

## En resumen

1. Guardamos las claves encriptadas con GPG en un repositorio Git
1. Para comunicarnos con la Yubikey y desencriptar las claves usamos:
    1. `gpg2` en Linux
    1. `OpenKeyChain` en Android
1. Para acceder al repositorio de claves de forma amigable usamos:
    1. `pass` en Linux
    1. `Password Store` en Android
1. Además, se necesita un adaptador USB para el teléfono (en mi caso USB-A a USB-C) en caso de no tener hardware con NFC


[pass]: https://www.passwordstore.org/
[tuto-stow]: http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html
[auth]: https://github.com/Yubico/yubioath-android/issues/30
[okc]: https://www.openkeychain.org/
[pass-store]: https://github.com/zeapo/Android-Password-Store
