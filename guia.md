# Taller de cifrado GPG con Thunderbird/Icedove
###### Álvar D. Soler Rus

## Introducción
En este taller vamos a utilizar el gestor opensoruce de correo Thunderbird de Mozilla. Por temas de copyright, la versión de Debian se llama Icedove. Solo cambian el icono y el nombre del programa en la línea de comandos, por lo demás son similares.

### ¿Qué es el cifrado?
Cifrar un texto (o una imágen digital, que al fin y al cabo es una cadena de "texto" describiendo la imagen) es transformarlo utilizando una clave y un algoritmo a otro texto que solo puede ser "destransformado" aplicándole otro algoritmo con una clave en particular. De esta manera, ese texto solo podrá ser leído por quien posea esa clave y sepa qué algoritmo se aplicó.

### Cifrado asimétrico GnuPG
Hay diferentes tipos de cifrado, pero la aplicación que vamos a utilizar [GnuPG][2], que es una implementación libre de GPG para cifrar nuestro correo electrónico que utiliza **Cifrado asimétrico**. ¿Qué es el Cifrado asimétrico? De la wiki:
> "es el método criptográfico que usa **un par de claves** para el envío de mensajes. Las dos claves pertenecen a la misma persona que ha enviado el mensaje. Una clave es **pública y se puede entregar a cualquier persona**, **la otra clave es privada y el propietario debe guardarla de modo que nadie tenga acceso a ella**. Además, los métodos criptográficos garantizan que esa pareja de claves sólo se puede generar una vez, de modo que se puede asumir que no es posible que dos personas hayan obtenido casualmente la misma pareja de claves.
**Si el remitente usa la clave pública del destinatario para cifrar el mensaje, una vez cifrado, sólo la clave privada del destinatario podrá descifrar este mensaje, ya que es el único que la conoce. Por tanto se logra la confidencialidad del envío del mensaje, nadie salvo el destinatario puede descifrarlo**."

Aquí una imágen bastante descriptiva (a mi juicio) de cómo funciona, también de la Wiki.

![firmaAsimetrica]

> - David redacta un mensaje
> - David firma digitalmente el mensaje con su clave privada
> - David envía el mensaje firmado digitalmente a Ana a través de internet, ya sea por correo electrónico, mensajería instantánea o cualquier otro medio
> - Ana recibe el mensaje firmado digitalmente y comprueba su autenticidad usando la clave pública de David
> - Ana ya puede leer el mensaje con total seguridad de que ha sido David el remitente

De esta manera protegemos el contenido de nuestro mensaje y también garantizamos que es nuestro.

## Taller
### Instalar Thunderbird / Icedove
Si no se tiene instalado Thunderbird, se puede descargar [aquí][1]. Si utilizamos una distro GNU/Linux simplemente:
```shell
  sudo apt-get install icedove
```
Para instalar el complemento de idioma Castellano:

```shell
  sudo apt-get install icedove-l10n-es-es
```
### Instalar complemento Enigmail
En los repositorios de Debian tenemos Enigmail
```shell
  sudo apt-get install enigmail
```

### Configurar cuenta de correo
Ahora, si todavía no tenemos una cuenta de correo añadida a Thunderbird, deberemos introducir los datos. Thunderbird nos da la opción de crearnos un correo, pero en este taller usaremos la de la UCM.

![configEmail1]

El nombre es el que se mostrará como remitente de los emails que enviemos. Clicamos en Continue.

![configEmail2]

En esta ventana seleccionamos IMAP (si queremos que los correos no se descarguen en nuestra máquina, si no que accedemos a ellos de manera remota) o POP3 (que descargará todo el contenido de tu email en tu máquina). Yo elegí IMAP.

![configEmail3]


 ya tenemos nuestro correo electrónico configurado.

### Configuración de Enigmail
Enigmail nos facilita un asistente para la configuración de este. Menu -> Enigmail -> Asistente de configuración.

![enigmailAsist]

Elegimos la opción de usar el asistente. Ahora el asistente nos hará varías preguntas. La primera, si queremos que nuestros correos estén **cifrados** por defecto, si queremos que lo haga de manera automática o si queremos hacerlo manualmente. Vamos a elegir la tercera opción (no cifrar mis correos por defecto), ya que si ciframos todos los correos no los podrán leer quienes no tengan nuestra clave. La segunda pregunta es si queremos que nuestros correos estén **firmados**, ésto es que con nuestra clave se "marca" el correo para que se sepa que el destinatario somos realmente nosotros. Esto **no cifra** el contenido del correo, solo verifica que lo estamos enviando nosotros. Marcaremos que sí. Siempre es buena opción tener firmados nuestros correos. La tercera pregunta es si queremos que Enigmail configure nuestro correo electrónico de manera automática para que no existan problemas al firmar y codificar. Elegimos que sí.

### Crear claves
Ahora el asistente nos da la opción de usar un par de claves ya generadas o crear unas nuevas. Si ya tenemos un par de claves generadas, las seleccionamso y ya estaría nuestro correo preparado para cifrar emails con Thunderbird. Si no tenemos un par de claves ya generadas, elegiremos la opción de crear nuevas claves.  A continuación se muestra la generación de nuevas claves:

![generate1]

Introducimos una contraseña que ayudará a la codificación de nuestras claves. Se puede dejar en blanco, pero esto haría a nuestro par de claves más __débiles__.

![generate2]

A continuación se comenzarán a crear nuestras claves. Todos los clicks, movimientos de ratón o acciones que lleve a cabo la máquina aumentará la aleatoriedad de nuestras claves. Enigmail se sirve de estas acciones para generar una semilla más aleatoria.

![generate3]

Una vez generado nuestro par de claves, nos preguntará si queremos generar un certificado de revocación. Ésto nos sirve para revocar nuestra clave privada si la perdemos o cae en malas manos. **Es muy recomendable** crear este fichero y guardarlo en un sitio seguro, ya que si cae en malas manos alguien podría utilizarlo para revocar nuestra clave.

![generateCertif]

Y... ¡ya está! Ya tenemos todo configurado.
### Prueba práctica de que funciona
Ahora vamos a enviar un correo de prueba para comprobar que hemos hecho todo bien. Para enviar un correo cifrado simplemente debemos darle al botón de Write / Escribir, introducir el destinatario, asunto y mensaje que queramos enviar. Después, antes de enviar, le damos al botón de Enigmail y seleccionamos El mensaje se cifrará -> Force Encryption (si no hemos seleccionado en el Asistente la opción de cifrar todos nuestros correos). De ésta manera nos aseguramos que el correo se cifrará.

![mail1]

Nos pedirá la contraseña que introducimos a la hora de codificar nuestras claves y después se enviará.
Ahora, si abrimos ese email desde el navegador, veremos algo así:

![mail2]

Pero si lo abrimos desde Thunderbird...

![mail3]

El cual nos asegura que la firma del remitente es la correcta y nos muestra el mensaje ya decodificado.

## Compartir claves
Hay diferentes formas de hacer que la gente tenga nuestra clave pública para que se cercione de que somos nosotros quienes le enviamos los correos.

### Repositorios
Existen una serie de repositorios de claves públicas GPG donde se puede subir nuestra clave para que otra gente se la pueda descargar de ahí. Estos repositorios están conectados unos entre otros, actuando como nodos. En España existe la [RedIRIS][3], del Ministerio de Ciencia e Innovación, enfocado a los usuarios de la comunidad académica.

Para subir nuestra clave a este repositorio, vamos a las opciones de Enigmail, Administrar claves. Ahí seleccionamos la clave y seleccionamos la opción Subir claves públicas en el menú de Servidor de claves. Vienen varias por defecto, pero vamos a usar la de la RedIRIS: ``pgp.rediris.es``.

### Obtener la clave en texto plano
También podemos querer tener nuestra clave como un fichero de texto plano para enviarla por correo adjuntada (útil cuando no sabemos si el destinatario tendrá la clave) o subirla a un servidor. También en el menú de Administrar claves de Enigmail, hacemos click derecho en la clave que queramos exportar, y seleccionamos Exportar claves a un fichero. Ahí seleccionamos **solo** la clave pública, y después solo tenemos que seleccionar la carpeta destino.

También cuando vamos a escribir un correo nuevo, en el menú de Enigmail nos sale la opción de Adjuntar mi clave pública. Muy fácil y rápido.

### Firmar una clave de otra persona
Para firmar la clave pública de otra persona en nuestro nombre, es decir, validar que esa clave pertenece a esa persona física, es muy sencillo. En la ventana de Administración de claves de Enigmail, seleccionamos la clave con click derecho y seleccionamos Establecer confianza del propietario. Seleccionamos cuanta de confianza tenemos, y ¡ya está!.

## Links de interes

- [Construcción de un anillo de confianza][4]
- [Validar otras claves (más extenso)][5]
- [GPG Cheatsheet][6]
- [The GNU Privacy Handbook][7]

[firmaAsimetrica]: img/firmaDigitalAsimetrica.png
[configEmail1]: img/configEmail.png
[configEmail2]: img/configEmail2.png
[configEmail3]: img/configEmail3.png
[enigmailAsist]: img/enigmailAsist.png
[generate1]: img/generate.png
[generate2]: img/generate2.png
[generate3]: img/generate3.png
[generateCertif]: img/generateCertif.png
[mail1]: img/mail.png
[mail2]: img/mail2.png
[mail3]: img/mail3.png
[1]: https://www.mozilla.org/es-ES/thunderbird/
[2]: https://www.gnupg.org/
[3]: http://www.rediris.es/servicios/keyserver/requisitos.html
[4]: https://www.gnupg.org/gph/es/manual/x571.html
[5]: https://www.gnupg.org/gph/es/manual/x354.html
[6]: http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/
[7]: https://www.gnupg.org/gph/es/manual.html
