# Taller de cifrado GPG con Thunderbird/Icedove
###### Álvar D. Soler Rus

## Introducción
En este taller vamos a utilizar el gestor opensoruce de correo Thunderbird de Mozilla. Por temas de copyright, la versión de Debian se llama Icedove. Solo cambian el icono y el nombre del programa en la línea de comandos, por lo demás son similares.

### ¿Qué es el cifrado?
Cifrar un texto (o una imágen digital, que al fin y al cabo es una cadena de "texto" describiendo la imagen) es transformarlo utilizando una clave y un algoritmo a otro texto que solo puede ser "destransformado" aplicándole otro algoritmo con una clave en particular. De esta manera, ese texto solo podrá ser leído por quien posea esa clave y sepa qué algoritmo se aplicó.
### Cifrado asimétrico GnuPG
Hay diferentes tipos de cifrado, pero la aplicación que vamos a utilizar [GnuPG][2], que es una implementación libre de PGP para cifrar nuestro correo electrónico que utiliza **Cifrado asimétrico**. ¿Qué es el Cifrado asimétrico? De la wiki:
> "es el método criptográfico que usa **un par de claves** para el envío de mensajes. Las dos claves pertenecen a la misma persona que ha enviado el mensaje. Una clave es **pública y se puede entregar a cualquier persona**, **la otra clave es privada y el propietario debe guardarla de modo que nadie tenga acceso a ella**. Además, los métodos criptográficos garantizan que esa pareja de claves sólo se puede generar una vez, de modo que se puede asumir que no es posible que dos personas hayan obtenido casualmente la misma pareja de claves.
**Si el remitente usa la clave pública del destinatario para cifrar el mensaje, una vez cifrado, sólo la clave privada del destinatario podrá descifrar este mensaje, ya que es el único que la conoce. Por tanto se logra la confidencialidad del envío del mensaje, nadie salvo el destinatario puede descifrarlo**."

Aquí una imágen bastante descriptiva (a mi juicio) de cómo funciona, también de la Wiki.
![firmaAsimetrica]
> - David redacta un mensaje
- David firma digitalmente el mensaje con su clave privada
- David envía el mensaje firmado digitalmente a Ana a través de internet, ya sea por correo electrónico, mensajería instantánea o cualquier otro medio
- Ana recibe el mensaje firmado digitalmente y comprueba su autenticidad usando la clave pública de David
- Ana ya puede leer el mensaje con total seguridad de que ha sido David el remitente

De esta manera protegemos el contenido de nuestro mensaje y también garantizamos que es nuestro.

## Taller

### Instalar Thunderbird / Icedove
Si no se tiene instalado Thunderbird, se puede descargar [aquí][1]. Si utilizamos una distro GNU/Linux simplemente:
```shell
  sudo apt-get install icedove
```
### Crear claves

### Prueba práctica de que funciona

### Extras: cómo compartir tu clave pública (subirlo a servidores, enviarla a otra gente, anillo de confianza, firmar claves de otra gente...)

[firmaAsimetrica]: img/firmaDigitalAsimetrica.png
[1]: https://www.mozilla.org/es-ES/thunderbird/
[2]: https://www.gnupg.org/
