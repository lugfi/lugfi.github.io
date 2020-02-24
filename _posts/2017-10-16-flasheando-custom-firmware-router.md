---
layout: post
title: Preocupado por KRACK? Mejorando seguridad en router hogareños con custom frimwares, pros y contras y mini howto install.
description: Guía básica de porque y como flashear firmware customs a routers hogareños.
authors: alexdaciuk
tags: krack routers unix seguridad
---

## El problema con los routers hogareños

Siendo 2017, quien más quien menos, tiene internet en su casa (ya sea un hermoso enlace de fibra o un horrendo ADSL). Para hacer la vida mas fácil de los usuarios, siempre entregan un router en situación de comodato. Esto tiene sus pros y sus contras.


**Pros:**

-   El usuario no tiene que preocuparse de comprar nada, eliminando la posibilidad de equivocarse en la compra y evitando gastar de más para tener el servicio.

-   La instalación del servicio no se cancela debido a falta de materiales: el técnico trae todo lo necesario para la instalación. Inclusive algunos servicios ADSL, como Arnet, traen un kit de auto-instalación, eliminando la necesidad de técnicos y la espera que eso conlleva.

-   El ISP se asegura de que los equipos entregados sean "totalmente compatibles" con el servicio.

-   Al usar hardware provisto por el ISP es más fácil obtener soporte técnico. No van a venir con la excusa de "el router que tenés no es totalmente compatible con el servicio".


**Contras:**

-   Normalmente el hardware provisto por el ISP es de mala calidad o segunda mano (compran el de la licitación mas barata, suerte con tu router ChunLang).

-   Aunque estén en comodato, el router tiene un cierto tiempo de garantía. Al pasar ese tiempo, cualquier recambio, ya sea por desgaste u otra razón, corre a bolsillo del usuario.

-   Los routers que entregan los ISPs suelen venir con un firmware capado y sin muchas opciones modificables por el usuario. Esto hace perder flexibilidad a la hora de configurarlo para las necesidades de cada persona.

-   Al ser routers que compran de oferta a China, no siempre tienen la ultima tecnología, llámese, WiFi AC o soporte para la banda de 5 GHz, entre otras cosas.

-   Mala configuración por defecto: muchos routers vienen configurados con contraseñas débiles para el acceso al router o para el WiFi (WEP o WPA), malos DNS por defecto.

-   Nulas actualizaciones: muchas veces estos routers viene con firmwares personalizados por el ISP, que no suelen sacar actualizaciones de esa personalización y, en muchos casos, inclusive bloqueando la posibilidad de reemplazarlo con el firmware oficial.


## Porque nos interesa tanto esto?

### Seguridad  

Teniendo en cuenta que por estos aparatos viaja toda nuestra información digital (ya sean contraseñas, números de tarjetas de crédito, etc), cualquiera en su sano juicio querría que estos aparatos estén con software actualizado con la menor cantidad de bugs de seguridad posibles.

Cualquiera que haya entrado a la interfaz "avanzada" de cualquier router comercial, puede ver que corren software bastante desactualizado. Sin ir más lejos, el ISP Telecentro, en 2016 entregaba [estos routers](http://uploads.tapatalk-cdn.com/20170124/1a86a430f5239d933726444229d0c648.jpg), que corrían kernel 2.6.35, en pleno 2016.

La mayoría de los routers (por no decir el 100 %), no reciben actualizaciones, ya sea porque el fabricante esta muy ocupado sacando más productos de los que podría mantener o directamente no le interesa.

La razón de este articulo justamente es [la vulnerabilidad descubierta en WPA2](https://arstechnica.com/information-technology/2017/10/severe-flaw-in-wpa2-protocol-leaves-wi-fi-traffic-open-to-eavesdropping/?amp=1), sin contar la [innumerable cantidad de agujeros de seguridad en el software de los fabricantes](https://routersecurity.org/bugs.php).


### Funcionalidades 

Muchos de los routers que instalan los ISPs vienen con muy pocas opciones de configuración, inclusive algunos ni te dejan cambiar los DNS o la IP de la red interna.

Firmwares como **LEDE / OpenWRT** o **DD-WRT** te permiten mucha mas flexibilidad a la hora de administrar el router, aparte de tener mucho mas software disponible para instalar, como dnscrypt, VPN, QoS, Samba, entre otras cosas.

También, la ventaja de tener software actualizado y totalmente abierto suma.


## Como solucionamos esto?

La mejor solución (aunque no la mas económica), es comprar un router WiFi común (que esté soportado por algún firmware custom, como OpenWRT / Lede, DD-WRT, Tomato WRT, etc), poner el router del ISP en modo **Bridge** y así dejar todo el trabajo al router nuestro que tiene software actualizado y con mas funcionalidades.


## Como me aseguro de comprar un router soportado por algún firmware custom copado?

Casi todos los fimrwares tienen una lista de hardware soportado

**LEDE:** <https://lede-project.org/toh/start>  
**OpenWRT:** <https://wiki.openwrt.org/toh/start>  
**DD-WRT:** <https://www.dd-wrt.com/wiki/index.php/Supported_Devices>  
**Asuswrt-Merlin:** <https://asuswrt.lostrealm.ca/about>  


**Notas**

-   **Asuswrt-Merlin** es un firmware custom basado en el firmware original de Asus (Asuswrt), así que no tiene muchos cambios radicales ni nuevas features.
-   **LEDE** sucesor de **OpenWRT**, activamente desarrollado y con actualizaciones constantes, es el más recomendado de la lista.
-   **DD-WRT** el precursor de todos los firmwares custom, no muy actualizado, aunque soporta routers viejos con menos de 4 MB de ROM.


## Notas varias sobre los firmwares custom en general

-   Primero que nada **cambiar el firmware del fabricante invalida tu garantía**, aunque reinstalando el firmware original, no creo que tengas problemas para reclamar garantía en cualquier caso.

-   Como todo firmware no oficial, puede traer problemas de estabilidad, aunque en mis años de usar DD-WRT, OpenWRT y LEDE, no tuve mayores problemas.

-   Al tener más funcionalidad y capacidad de personalización, requiere un poco mas de conocimiento técnico, aunque, si alguna vez configuraste un router comercial, no es nada del otro mundo. Ademas hay miles de tutoriales sobre como configurar estas cosas.

-   No todos los routers están soportados, al ser necesario que gente con conocimientos trabaje para poder portar un firmware custom, normalmente solo los modelos de marcas mas conocidas están soportados.

-   Cosas como ADSL o DOCSIS no están soportadas por falta de soporte por parte de los fabricantes.


## NOTAS ANTES DE INSTALAR

Antes de hacer cualquier cosa en su router, anoten datos necesarios del ISP (normalmente usuario/contraseña, depende del servicio) y una forma de volver atrás, modo de recovery o lo que tenga el router, para poder volver al firmware original por si algo sale mal.


## Como instalar un firmware customs

### LEDE / OpenWRT

Muchos dispositivos están soportados mediante el método **OEM Firmware**. Esto significa, flashear directamente desde la interfaz web del router, sin mucha más complicación.

Otros métodos, como ser, **Via Bootloader**, **Puerto Serie** y **JTAG** son un poco mas complicados y cambian de router a router, pero LEDE / OpenWRT tiene una Wiki bastante completa.

**Mas información :**  <https://wiki.openwrt.org/doc/howto/generic.flashing>


### DD-WRT

También soporta el método **OEM Firmware**, aunque al soportar routers mas viejos, no siempre es una opción.

**Mas información :** <http://www.dd-wrt.com/wiki/index.php/Installation>


## Asuswrt-Merlin

Al ser un firmware original modificado, el método de flasheo es mediante la interfaz web sin más complicaciones.

**Mas informacion :** <https://github.com/RMerl/asuswrt-merlin/wiki/Installation>


## Ya instalé, ahora qué?

Ahora, frente a toda la flexibilidad que estos firmwares ofrecen, uno puede sentirse perdido, sin saber que hacer. Cada firmware tiene una wiki bastante completa sobre las posibilidades que ofrecen. Pasarse por ahí suele ser buena opción.

Cosas copadas que se pueden hacer con estos firmwares, entre otras cosas, usar VPNs, dnscrypt, AdBlockers.

**Primeros pasos con LEDE / OpenWRT :** <https://wiki.openwrt.org/doc/howto/basic.config>

**Tutoriales DD-WRT :** <http://www.dd-wrt.com/wiki/index.php/Tutorials>

**Wiki Asuswrt-Merlin :** <https://github.com/RMerl/asuswrt-merlin/wiki>
