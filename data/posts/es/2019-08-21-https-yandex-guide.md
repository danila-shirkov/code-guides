---
title: Qué es el protocolo HTTPS y cómo te protege en Internet
subtitle: Guía de HTTPS
description: Una guía útil sobre el protocolo HTTPS, su relevancia, áreas de aplicación y difusión
image: "/assets/images/https/https-superhero.png"
author: Kirill Mokevnin
---

Esta guía ha sido reproducida del [blog de Yandex](https://yandex.ru/blog/company/77455) para la comodidad de los usuarios. En ella se habla sobre el protocolo HTTPS, su relevancia, áreas de aplicación y difusión.

Cada acción en Internet implica el intercambio de datos. Cada vez que reproduces un video, envías un mensaje en una red social o abres tu sitio web favorito, tu computadora envía una solicitud al servidor correspondiente y recibe una respuesta. Por lo general, el intercambio de datos se realiza a través del protocolo HTTP. Este protocolo no solo establece las reglas para el intercambio de información, sino que también sirve como transporte para la transferencia de datos, permitiendo que el navegador cargue el contenido del sitio en tu computadora o teléfono inteligente.

<Banner name="course-http" />

A pesar de la comodidad y popularidad del HTTP, tiene una desventaja: los datos se transmiten en texto plano y no están protegidos. En su camino desde el punto A al punto B, la información en Internet pasa por decenas de nodos intermedios, y si uno de ellos está bajo el control de un atacante, los datos pueden ser interceptados. Lo mismo puede ocurrir cuando utilizas una red Wi-Fi no segura, como en un café. Para establecer una conexión segura, se utiliza el protocolo [HTTPS](https://es.wikipedia.org/wiki/HTTPS) con cifrado.

![http y https](/assets/images/https/1.png)

## Aplicaciones de HTTPS
En algunos servicios, como los sistemas de pago en línea, la protección de datos es de vital importancia, por lo que solo se utiliza HTTPS. Este protocolo también se utiliza con frecuencia en otros servicios que manejan información privada, incluidos los datos personales. Muchos servicios de Yandex solo funcionan a través del protocolo HTTPS: Passport, Correo, Direct, Métrica, Taxi, Yandex.Money, así como todos los formularios de retroalimentación que manejan datos personales de los usuarios.

Todos los navegadores modernos admiten el protocolo HTTPS. No es necesario configurarlo manualmente, se activa automáticamente cuando es necesario y posible.

## Por qué HTTPS es seguro
La protección de datos en HTTPS es proporcionada por el protocolo criptográfico SSL/TLS, que cifra la información transmitida. Básicamente, este protocolo es una capa adicional sobre HTTP. Proporciona la encriptación de datos y los hace inaccesibles para terceros. El protocolo SSL/TLS es bueno porque permite a dos participantes desconocidos en una red establecer una conexión segura a través de un canal no seguro.

Supongamos que hoy es el último día del mes y te das cuenta de que debes pagar por tu conexión a Internet. Encuentras el enlace correcto en el sitio web de tu proveedor y accedes a tu cuenta personal. Seguramente querrás mantener en secreto toda la información transmitida, por lo que debe estar encriptada: esto incluye tu contraseña, la cantidad a pagar y el número de tarjeta de crédito. El problema es que inicialmente tu computadora estaba intercambiando datos con el servidor del proveedor a través de un canal no seguro, es decir, a través de HTTP. ¿Cómo se puede establecer una conexión segura a través de HTTPS en estas condiciones, suponiendo que el canal está siendo interceptado? Esto se logra mediante un simple truco matemático.

## Cómo funciona una conexión segura
Imagina que quieres enviar algo a otra persona. Lo pones en una caja y lo envías por correo. Y para evitar que el mensajero, u otra persona, lo robe, cierras la caja con un candado. El mensajero entrega la caja, pero el destinatario no puede abrirla, ya que no tiene la llave. Entonces, el destinatario coloca su propio candado en la caja y te la envía de vuelta. Recibes la caja con dos candados, quitas el tuyo y la envías nuevamente. Finalmente, el destinatario recibe la caja con solo su candado, la abre y saca lo que le enviaste.

![esquema de funcionamiento](/assets/images/https/2.png)

Esto fue necesario para intercambiar mensajes cifrados con tu interlocutor. En la caja, le enviaste la clave del cifrado, y ahora ambos la conocen. Ahora puedes intercambiar mensajes cifrados abiertamente, sin temor a que alguien los intercepte, ya que no se pueden entender sin la clave. ¿Por qué tanta complicación y por qué no se pudo enviar el paquete por separado de la llave del candado? Por supuesto, se podría hacer, pero en ese caso no habría garantía de que la llave no fuera interceptada y que el paquete no fuera abierto por otra persona.

El protocolo SSL/TLS funciona de manera similar. Al establecer una conexión segura a través de HTTPS, tu computadora y el servidor primero eligen una clave secreta compartida y luego intercambian información cifrada con esa clave. La clave secreta compartida se genera nuevamente para cada sesión de comunicación. No se puede interceptar y es prácticamente imposible de adivinar, generalmente es un número de más de 100 caracteres. Esta clave secreta de un solo uso se utiliza para cifrar toda la comunicación entre el navegador y el servidor. Parece ser un sistema perfecto que garantiza una conexión absolutamente segura. Sin embargo, para una seguridad completa, le falta una cosa: la garantía de que tu interlocutor es realmente quien dice ser.

## Por qué se necesitan certificados digitales
Imagina que tu paquete no llegó a su destinatario, sino que fue interceptado por otra persona. Esta persona coloca su propio candado en el paquete, falsifica la dirección del remitente y te lo envía. Cuando esta persona descubre la clave de cifrado de esta manera, se la comunica a tu destinatario en tu nombre. Como resultado, tú y tu interlocutor están seguros de que la clave de cifrado se transmitió de manera segura y se puede utilizar para intercambiar mensajes cifrados. Sin embargo, cualquier persona puede leer y interceptar fácilmente todos estos mensajes sin que tú te des cuenta. No es muy seguro.

De la misma manera, un tercero puede interferir en la conexión entre dos dispositivos en Internet y descifrar todos los mensajes sin ser detectado. Por ejemplo, pagaste por tu conexión a Internet a través de una conexión segura y el pago fue recibido. Pero un atacante interceptó el número y el código de verificación de autenticidad de tu tarjeta de crédito. Aún no lo sabes, y cuando te enteres, será demasiado tarde. Un certificado digital ayuda a evitar esta situación: es un documento electrónico que se utiliza para identificar un servidor.

![proceso de obtención de un certificado digital](/assets/images/https/3.png)

Como usuario, no necesitas un certificado, pero cualquier servidor (sitio web) que quiera establecer una conexión segura contigo debe tener uno. El certificado confirma dos cosas: 1) La entidad a la que se emitió realmente existe y 2) Controla el servidor especificado en el certificado. Los certificados son emitidos por autoridades de certificación, algo así como oficinas de pasaportes. Al igual que en un pasaporte, el certificado contiene datos sobre su propietario, incluido su nombre (o el nombre de la organización), así como una firma que certifica la autenticidad del certificado. La verificación de la autenticidad del certificado es lo primero que hace el navegador al establecer una conexión HTTPS segura. El intercambio de datos comienza solo si la verificación es exitosa.

Si volvemos a la analogía de la caja y los candados, el certificado digital te permite asegurarte de que el candado de tu interlocutor en la caja le pertenece a él. Que es una cerradura única que no se puede falsificar. Por lo tanto, si alguien intenta engañarte y te envía una caja con su propio candado, lo notarás fácilmente, ya que la cerradura será diferente.

## Difusión de HTTPS
Una de las recomendaciones más populares para cualquier servicio de Internet es utilizar siempre las últimas versiones de software. Si nunca te has preguntado por qué, aquí tienes una de las razones: el soporte de los últimos avances en seguridad.

La difusión de HTTPS y otras nuevas tecnologías en Internet depende en gran medida de la rapidez con la que se desarrolla la infraestructura para su uso. Por ejemplo, si la mitad de los usuarios de Internet no tuvieran navegadores que admitieran HTTPS, muchos sitios simplemente no podrían utilizarlo. Esto haría que un sitio web de un banco, que ha migrado completamente a HTTPS, no esté disponible para la mitad de sus clientes.

Además, en los protocolos criptográficos, incluido SSL/TLS, se encuentran regularmente vulnerabilidades que permiten la interceptación incluso de información cifrada. Para solucionar estas vulnerabilidades, los protocolos se actualizan regularmente y cada nueva versión suele ser más segura que la anterior. Por lo tanto, cuanto más personas instalen las versiones modernas de navegadores y otros programas importantes, más seguros estarán.

## Otros casos de uso de cifrado
En Internet, hay muchos protocolos de intercambio de datos además de HTTP y HTTPS, y también deben proporcionar protección. Por ejemplo, Outlook, Gmail, iOS y Yahoo admite el cifrado de correos electrónicos entrantes y salientes, como se puede leer en [el blog tecnológico de Kaspersky](https://latam.kaspersky.com/resource-center/preemptive-safety/how-to-encrypt-email). Nos preocupamos por la seguridad de nuestros usuarios y nos esforzamos por proteger sus datos en todos los lugares donde sea posible.
