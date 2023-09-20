---
title: ¿Qué es la criptografía?
subtitle: Qué es la criptografía y cómo se utiliza para proteger la información personal
description: Criptografía en seguridad de la información
author: Vasiliy Vasilyev
---

Puede que no sea obvio, pero nos encontramos con la criptografía todos los días. Por ejemplo, cuando pagamos nuestras compras con tarjeta, vemos videos en YouTube o llenamos el tanque de gasolina, la criptografía protege nuestra información. Puede parecer que la criptografía es algo exclusivo de los desarrolladores, hackers y corporaciones, y que el usuario común no necesita saber nada al respecto. Sin embargo, es útil no solo para los especialistas, sino también para todos aquellos que se preocupan por su propia seguridad. Esta guía te ayudará a entender qué es la criptografía y cómo se aplica en la vida cotidiana.

## ¿Cómo surgió la criptografía?

Desde los albores de la civilización humana, la información ha sido uno de nuestros activos más valiosos. Hace miles de años, nuestros antepasados se enfrentaron a la necesidad de transmitir información en el espacio (de un punto A a un punto B) o en el tiempo (por ejemplo, de un maestro a sus alumnos). La escritura ayudó a resolver este problema, pero luego surgió otro: ¿cómo proteger la información transmitida de los ojos de aquellos a quienes no debería llegar?

Hace unos 3500 años, los alfareros en Mesopotamia protegían los secretos de su oficio mediante el cifrado en tablillas de arcilla. Los políticos cifraban sus mensajes para mantenerlos en secreto.

¿Cómo se veía este cifrado? Lo veremos en el siguiente ejemplo:

Supongamos que queremos cifrar el mensaje "Hola". Una forma de hacerlo es desplazar las letras del alfabeto un número fijo de posiciones. Este método se llama cifrado de desplazamiento o **cifrado de César**.

En la siguiente imagen se muestra un desplazamiento de tres letras hacia adelante.

![alfabeto](/assets/images/cryptography/alphabet.png)

Un desplazamiento de tres letras significa que:

A ⇒ D
B ⇒ E
C ⇒ F

El mensaje "Hola" se convierte en "Krñd".

El cifrado se puede mejorar aplicando un método más avanzado. Imagina que después de cada uso, el algoritmo de cifrado cambia, es decir, el mismo mensaje repetido se verá completamente diferente. En otras palabras, si en el primer caso obtuvimos "Krñd", en el siguiente caso la misma palabra se cifrará como "Gñkz": ahora el desplazamiento se ha producido una letra hacia atrás.

## Métodos modernos de criptografía

La criptografía moderna no se parece en nada a la simple permutación de letras. Para cifrar y transmitir datos de manera segura, se utilizan algoritmos que son imposibles de "descifrar". Estos algoritmos se basan en transformaciones matemáticas, y solo una computadora puede trabajar con ellos. Ya no se puede hacer con un lápiz y papel. Los tres métodos criptográficos más comunes son los siguientes:

### Criptografía simétrica

Es uno de los tipos más simples de cifrado. La criptografía simétrica utiliza una clave secreta, que puede ser un número, una palabra o una cadena de caracteres, para cifrar y descifrar datos. La clave es conocida tanto por el remitente como por el destinatario. Este es uno de los métodos de cifrado más antiguos y comunes.

Este método generalmente no se utiliza para transmitir mensajes a través de Internet, ya que la clave debe transmitirse por separado. Si un tercero de alguna manera obtiene la clave, podrá ver los datos cifrados.

Es una especie de trampa: si quieres enviar un mensaje cifrado para ocultar su contenido de miradas indiscretas, primero debes enviar un mensaje sin cifrar que será completamente visible. Esto hace que este método sea extremadamente inseguro.

Es por eso que la criptografía simétrica generalmente se utiliza para cifrar bases de datos locales, como en un disco duro de servidor o en los datos de tu iPhone.

### Cifrado asimétrico

Es un método de cifrado en el que se utilizan dos claves: una clave pública y una clave privada. La clave pública se utiliza para cifrar la información y se puede transmitir a través de canales no seguros. La clave privada se utiliza para descifrar los datos cifrados con la clave pública. Las claves pública y privada son números muy grandes relacionados por una función específica, pero de tal manera que si conoces una clave, es extremadamente difícil calcular la otra.

El cifrado asimétrico resuelve el problema principal de seguridad del cifrado simétrico, donde se utiliza la misma clave para cifrar y descifrar los datos. Por otro lado, los algoritmos asimétricos son mucho más lentos que los simétricos, por lo que a menudo se utilizan ambos métodos.

### Hashing

Destacaremos un método que convierte la información en un conjunto único de caracteres, pero no cifra los datos. En esencia, el hashing es transformar un mensaje en una cadena ilegible, no para ocultar el mensaje, sino para verificar su contenido. A menudo se utiliza al transferir archivos grandes.

Supongamos que necesitamos actualizar el software en nuestra computadora. El hashing es una buena manera de verificar los archivos descargados, como los archivos de Windows (.ISO) o Mac (.DMG). Cuando descargamos la actualización, junto con el archivo recibimos un hash de ese archivo. Nuestra computadora vuelve a aplicar el hash al archivo descargado y compara los hashes (el recibido y el calculado): si coinciden, significa que hemos recibido un archivo no dañado. Cualquier cambio, por más pequeño que sea, en el archivo descargado, ya sea debido a daños o intervención maliciosa, cambiará drásticamente el hash resultante. Solo después de verificar la integridad, la computadora puede continuar trabajando con el archivo.

## Principios de la criptografía

El objetivo de la criptografía es proteger la información. Se basa en cuatro principios:

### Autenticación

En pocas palabras, es el proceso que garantiza que las partes en ambos extremos de una conexión son realmente quienes dicen ser.

Al menos un tipo de autenticación se utiliza en Internet cada vez que utilizas un sitio web seguro. Por ejemplo, el sitio web interno de tu empresa o el sitio web de Hexlet.

Dependiendo del navegador que utilices, verás un candado cerrado o una URL verde (o ambos), lo que indica que el sitio al que te has conectado es el sitio que dice ser.

![hexlet](/assets/images/cryptography/hexlet.png)

Esto es especialmente importante cuando realizamos compras en línea, realizamos operaciones bancarias o pagamos facturas a través de Internet. Esto garantiza que no proporcionemos información sobre nuestras cuentas bancarias o tarjetas de crédito a los hackers.

Otro ejemplo de uso de la criptografía para la autenticación es Pretty Good Privacy, un paquete de software gratuito utilizado para cifrar y autenticar mensajes, firmas digitales, compresión de datos, así como correos electrónicos y sus archivos adjuntos.

### No repudio

Este concepto es especialmente importante para aquellos que utilizan o desarrollan aplicaciones financieras o de comercio electrónico.

En los primeros días de las transacciones financieras y el comercio electrónico en Internet, uno de los problemas graves era la prevalencia de usuarios que podían negar las transacciones después de haberlas realizado. Por ejemplo, un cliente bancario solicita transferir dinero a otra cuenta. Luego afirma que nunca hizo esa solicitud y exige que se le devuelva todo el monto a su cuenta.

Sin embargo, si el banco ha tomado medidas de seguridad utilizando criptografía, puede demostrar que la transacción fue realmente iniciada por el usuario.

### Integridad

La criptografía ayuda a asegurarse de que los datos no hayan sido vistos o modificados durante la transmisión o el almacenamiento.

Por ejemplo, el uso de un sistema criptográfico para garantizar la integridad de los datos garantiza que las empresas competidoras no puedan falsificar la correspondencia interna y los datos confidenciales de un competidor.

El método más común para garantizar la integridad de los datos mediante criptografía es el uso de hashes criptográficos, que se mencionaron anteriormente.

### Confidencialidad

En un mundo de filtraciones de información constantes y escándalos interminables relacionados con la confidencialidad, mantener la información privada es una de las principales tareas de la criptografía. De hecho, los sistemas criptográficos fueron desarrollados originalmente con el propósito de proteger la información.

Con las herramientas de cifrado adecuadas, los usuarios pueden proteger los datos confidenciales de la empresa, las comunicaciones personales o simplemente bloquear su computadora con una contraseña sencilla.

Sin embargo, en las condiciones modernas, estos métodos no pueden garantizar la seguridad de los sistemas masivos de comunicación electrónica o comercio. Ahora tenemos que trabajar no solo con casos específicos de almacenamiento o transmisión de información, sino también con volúmenes masivos de datos.

## Cómo los usuarios comunes pueden utilizar la criptografía?

Como se mencionó al principio del artículo, la criptografía es parte de la vida cotidiana. El pago de compras con tarjeta o simplemente conectarse a una red Wi-Fi requieren el uso de criptografía.

Aunque la mayoría de las operaciones en la vida cotidiana ya están protegidas por criptografía, hay áreas en las que se puede agregar un nivel adicional de seguridad a las acciones cotidianas.

### VPN

Una red privada virtual (VPN) cifra la conexión a Internet, evitando que terceros espíen tu actividad en línea.

Una VPN envuelve la conexión a Internet en un "túnel" de cifrado, similar a un túnel de metro. Aunque sabemos que hay trenes en el túnel, no podemos determinar dónde están, cuántos vagones hay en el tren y hacia dónde se dirigen.

**Virtual** significa que la VPN se crea de forma programática como una capa adicional sobre otra red. Para transmitir datos, se utiliza el enrutamiento en túnel, donde el tráfico se envuelve en un túnel separado que pasa por un canal de comunicación de nivel inferior. La información en el túnel VPN está cifrada de forma segura.
**Privada** significa que la VPN es una red interna en la que solo hay dispositivos de confianza.
**Red** significa que la conexión se realiza entre dos dispositivos: el cliente y el servidor VPN, que forman una red única.

Una VPN proporciona protección: nadie podrá saber qué sitios web visitas o qué archivos descargas.

En los últimos tiempos, las VPN se han convertido en una herramienta popular para los usuarios que desean proteger sus acciones en línea de la vigilancia externa.

### HTTPS

Las páginas HTTPS generalmente utilizan el protocolo SSL (Secure Sockets Layer) o TLS (Transport Layer Security) para aumentar la seguridad de las páginas que el usuario ve mediante el uso de claves públicas.

Este tipo de conexión cifra los mensajes enviados entre tu computadora y el sitio web que estás visitando para proteger los datos del usuario contra el robo. Esto es especialmente importante cuando se envía información personal importante o datos financieros.

HTTPS es una extensión de código abierto del navegador compatible con Chrome, Firefox y Opera. Con esta extensión, cualquier sitio web que visites se verá obligado a utilizar una conexión HTTPS en lugar de una conexión HTTP menos segura.

### BitLocker (para Windows) o FileVault2 (para Mac)

Un paso adicional (además de la contraseña de inicio de sesión) para proteger la seguridad de la información personal en tu computadora o portátil es instalar [BitLocker](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-overview) o [FileVault2](https://support.apple.com/en-us/HT204837).

Estos programas de cifrado de disco protegen los datos mediante el uso del algoritmo criptográfico AES, que cifra volúmenes enteros. Si eliges este software, asegúrate de anotar tus credenciales y guárdalas en un lugar seguro. Si pierdes estas credenciales, es casi seguro que perderás el acceso a toda la información cifrada.

## La criptografía no es perfecta

Hemos analizado cómo funciona la criptografía y cómo protege los datos. Si bien la criptografía puede proporcionar seguridad a la información, no puede garantizar una seguridad completa. Incluso los mejores algoritmos criptográficos no son perfectos.

Por lo tanto, debemos tener en cuenta que "más seguro" no significa "absolutamente seguro".

## Conclusión

Con un mayor entendimiento de los métodos de cifrado comunes y los algoritmos criptográficos utilizados en la actualidad, podremos protegernos mejor de posibles ciberataques.

Hay muchas formas de utilizar la criptografía y, quizás, la mejor manera de garantizar un nivel confiable de cifrado para las acciones en línea es utilizar una VPN de calidad.

Aunque la criptografía no es perfecta, es necesaria para garantizar la seguridad de la información personal.

## Otros guías relacionadas

1. [¿Qué es una API?](https://guides.hexlet.io/ru/http-api/)
