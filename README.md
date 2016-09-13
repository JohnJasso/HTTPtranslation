#HTTP (HyperText Transfer Protocol)

##Basics

###Introduction

####The Web

El Internet (o la Web) es un sistema de información cliente/servidor distribuido masivo, tal como se muestre en el siguiente diagrama:

Muchas aplicaciones corren concurrentemente a través de la Web, tales como navegación o “surfeo” de la Web, e-mail, transferencia de archivos, transmisión de audio y video, y más. Para que se lleve a cabo una comunicación apropiada entre el cliente y el servidor, estas aplicaciones deben estar de acuerdo en un protocolo a nivel de aplicación, como lo son HTTP, FTP, SMTP, POP, etc.

####HyperText Transfer Protocol (HTTP)

HTTP (HyperText Transfer Protocol) es tal vez el más popular protocolo de aplicación usado en el Internet (o la Web).
* HTTP es un protocolo solicitud-respuesta, cliente-servidor asimétrico como se ilustra. Un cliente HTTP envía un mensaje de solicitud a un servidor HTTP. El servidor,en su turno, regresa un mensaje de respuesta.
En otras palabras, HTTP es un protocolo de llamada, el cliente “llama” información del servidor (en su lugar el servidor envía información al cliente).
* HTTP es un protocolo sin estados. En otras palabras, la solicitud actual no sabe lo que se ha hecho en solicitudes anteriores.
* HTTP permite la negociación y representación de datos, para permitir la construcción de sistemas independientemente de los datos que están siendo transferidos.
* Citando de RFC2616: “El Protocolo de Transferencia de Hipertexto (HTTP) es un protocolo de aplicación para sistemas de información distribuidos, colaborativos, y de hipermedia. Es un protocolo genérico y sin estados que puede ser usado para muchas tareas más allá de su uso para el hipertexto, tales como la asignación de nombre a servidores y sistemas de manejo de objetos distribuidos, a través de la extensión de sus métodos de solicitud, códigos de error, y cabeceras.”

####Browser

Cuando sea que emites una URL desde tu navegador para obtener un recurso web usando HTTP, p. ej. http://www.nowhere123.com/index.html, el navegador transforma la URL en un mensaje de solicitud y lo envía al servidor HTTP. El servidor HTTP interpreta este mensaje, y te regresa un mensaje de respuesta apropiado, el cual es o el recurso que solicitaste o un mensaje de error.
El proceso está ilustrado debajo:

####Uniform Resource Locator (URL)

Una URL (Localizador Uniforme de Recursos) es usada para identificar un recurso de manera única a través de la Web. URL tiene la siguiente sintaxis:

> protocol://hostname:port/path-and-file-name

Hay 4 partes en una URL:
1. Protocolo: El protocolo de aplicación usado por el cliente y el servidor, p. ej. HTTP, FTP, y telnet.
2. Hostname: El nombre del dominio DNS (p. ej. www.nowhere123.com) o la dirección IP (p. ej. 192.128.1.2) del servidor.
3. Port: El número del puerto TCP que el servidor está escuchando por solicitudes entrantes de los clientes.
4. Path-and-file-name: El nombre y la localización del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en la URL http://www.nowhere123.com/doc/index.html, el protocolo de comunicación es HTTP; el nombre del host es www.nowhere123.com. El numero del puerto no fue especificado en la URL y toma el numero de default, el cuál es el puerto TCP 80 para HTTP. La ruta y nombre del archivo para el localizar el recurso son “/docs/index.html”.

Otros ejemplos de URL son:
> ftp://www.ftp.org/docs/test.text
> mailto:user@test101.com
> news:soc.culture.Singapore
> telnet://www.nowhere123.com/

####Protocolo HTTP

Como fue mencionado, cuando tu introduces una URL en la caja de direcciones del navegador, el navegador traduce la URL en un mensaje de solicitud de acuerdo al protocolo especificado; y envia el mensaje al servidor.

Por ejemplo, el navegador tradujo la URL http://www.nowhere123.com/doc/index.html en el mensaje de solicitud siguiente:

> GET /docs/index.html HTTP/1.1
> Host: www.nowhere123.com
> Accept: image/gif, image/jpeg, */*
> Accept-Language: en-us
> Accept-Encoding: gzip, deflate
> User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
> (blank line)

Cuando este mensaje llega al servidor, el servidor puede tomar cualquiera de estas acciones:

1. El servidor interpreta la solicitud recibida, marea la solicitud en un archivo bajo el directorio de documentos del servidor, ejecuta el programa, y regresa el resultado del programa al cliente.
2. El servidor interpreta la solicitud recibida, marea la solicitud en un programa guardado en el servidor, ejecuta el programa, y regresa el resultado del programa al cliente.
3. La solicitud no puede ser satisfecha, el servidor regresa un mensaje de error.

Un ejemplo de mensaje de respuesta de HTTP es como se muestra:

> HTTP/1.1 200 OK
> Date: Sun, 18 Oct 2009 08:56:53 GMT
> Server: Apache/2.2.14 (Win32)
> Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
> ETag: "10000000565a5-2c-3e94b66c2e680"
> Accept-Ranges: bytes
> Content-Length: 44
> Connection: close
> Content-Type: text/html
> X-Pad: avoid browser bug
>  
> <html><body><h1>It works!</h1></body></html>

El navegador recibe el mensaje de respuesta, interpreta el mensaje y muestra los contenidos del mensaje en la ventana del navegador de acuerdo al tipo de media del mensaje (como en la cabecera de respuesta de Tipo de Contenido). Tipos de media comunes incluyen “text/plain”, “text/html”, “image/gif”,”image/jpeg”, “audio/mpeg”, “video/mpeg”, “application/msword”, y “application/pdf”.

En su estado inactivo, un servidor HTTP no hace nada más que escuchar por las direcciones IP y puertos especificados en la configuración de la solicitud entrante. Cuando una solicitud llega, el servidor analiza la cabecera del mensaje, aplica reglas especificadas en la configuración, y toma la acción apropiada. El principal control del administrador de la red sobre el control de las acciones del servidor web es a través de la configuración, la cual será analizada a mayor detalle en secciones siguientes.

####HTTP a través de TCP/IP

HTTP es un protocolo de aplicación cliente-servidor. Típicamente corre a través de una conexión TCP/IP, como es ilustrado. (HTTP no necesita correr en TCP/IP. Solo es un transporte confiable. Cualquier protocolo de transporte que provea tales garantías puede ser usado.)

TCP/IP (Transmission Control Protocol/Interner Protocol) es un conjunto de protocolos de transporte y de red-capa para máquinas, para que se comuniquen entre sí a través de la red.

IP (Internet Protocolo) es un protocolo red-capa, se encarga del direccionamiento y orientación de red. En una red IP, cada máquina es asignada con una dirección IP única (p. ej. 165.1.2.3), y el software IP es responsable por orientar un mensaje desde la IP fuente a la IP destino. En IPv4 (IP version 4),la dirección IP consta de 4 bytes, cada uno va de 0 a 255, separados por puntos, lo cual es llamado la forma quad-dotted. Este esquema de numeración soporta direcciones 4G en la red. La última IPv6 (IP versión 6) soporta más direcciones. Ya que memorizar números es difícil para la mayoría de personas, un nombre de dominio parecido al lenguaje natural, como lo es www.nowhere123.com es usado en su lugar. El DNS (Domain Name Service) traduce el nombre de dominio a la dirección IP (via tablas lookup distribuidas). Una dirección IP especial 127.0.0.1 siempre se refiere a tu propia máquina. Su nombre de dominio es “localhost” y puede ser usada para un testeo de bucle.

TCP (Protocolo de Control de Transmisión) es un protocolo transporte-capa, responsable de establecer una conexión entre dos máquinas. TCP consiste de 2 protocolos, TCP y UDP (User Datagram Package). TCP es confiable, cada paquete tiene un número de secuencia, y un reconocimiento es esperado. Un paquete será retransmitido si no es recibido por el receptor. La entrega de los paquetes es garantizada en TCP. UDP no garantiza la entrega de los paquetes, y por eso no es confiable. Sin embargo, UDP tiene menos gastos de red puede ser usado para aplicaciones como transmisión de audio y video, donde la confiabilidad no es crítica.

TCP intercambia(multiplexa) las aplicaciones dentro de una máquina de IP. Para cada máquina IP, TCP soporta (multiplexa) hasta 65536 puertos (o sockets), desde el puerto numero 0 hasta el 65535.Un aplicación, como HTTP o FTP, corre (o escucha) en un puerto particular para solicitudes entrantes. Los puertos 0 al 1023 son pre—asignados a los protocolos populares, p.ej. HTTP en el 80, FTP en el 21, Telnet en el 23, SMTP en el 25, NNTP en el 119, y DNS en el 53. El puerto 1024 y superiores están disponibles para los usuarios.

Aunque el puerto TCP 80 es per-asignado a HTTP, como el puerto default de HTTP, esto no te prohibe de correr un servidor HTTP en cualquier otro puerto asignado por el usuario (1025-65535) tal como el 8000, 8080, especialmente para probar un servidor. También se podrían correr multiples servidores HTTP en la misma máquina en diferentes números de puertos. Cuando un cliente emite una URL sin definir el numero de puerto, p.ej. http://www.nowhere123.com/docs/index.html, el navegador conectará por default al puerto numero 80 del servidor www.nowhere123.com. Se necesita definir explícitamente el numero de puerto en la URL, p.ej. http:/ww.nowhere123.com:8000/docs/index.html si el servidor esta escuchando por el puerto 8000 y no por el predeterminado puerto 80.

En breve, para comunicarse a través de TCP/IP, se necesita saber (a) el nombre del host o dirección IP, (b) numero de puerto.

####Especificaciones HTTP

La especificación HTTP es mantenida por W3C(World-wide Web Consortium) y está disponible en http://www.w3.org/standards/techs/http. Actualmente hay dos versiones de HTTP, HTTP/1.0 y HTTP/1.1. La versión original HTTP/0.9 (1991), escrita por Tim Berners-Lee, es un protocolo simple para transferir datos sin procesar a través del Internet. HTTP/1.0 (1996) (definido en RFC 1945), mejoró el protocolo permitiendo mensajes parecidos a MIME. HTTP/1.0 no trata con los asuntos de prosees, caching, conexión persistente, hosts virtuales, y descarga distancia. Estas características fueron provistas en HTTP/1.1 (1999) (definido en RFC 2616).

###Servidor Apache HTTP o Servidor Apache Tomcat

Un servidor HTTP (tal como Servidor Apache HTTP o Servidor Apache Tomcat) es necesario para estudiar el protocolo HTTP.

Un Servidor Apache HTTP es un popular servidor de producción de potencia industrial, producido por Apache Software Foundation (ASF) en www.apache.org. ASF es una fundación de software libre. Lo que es decir, los servidores Apache HTTP son gratis, con código fuente.

El primer servidor HTTP es escrito por Tim Berners Lee en el CERN (Centro Europeo para la Investigación Nuclear) en Geneva, Suecia, quién también invento el HTML. Apache fue construido en servidor NCSA (National Center for Supercomputing Applications, USA) “httpd 1.3”, a principios de 1995. Apache probablemente obtiene su nombre del echo que consiste de algo de código original (de un servidor web NCSA httpd temprano) más algunos parches; o del nombre de la tribu india americana.

Lea “Apache How-To” en como instalar y configurar un servidor Apache HTTP; o “Tomcat How-To” para instalar e iniciarse con un servidor Apache Tomcat.

###Mensajes HTTP de Solicitud y Respuesta

Cliente y servidor HTTP se comunican enviando y recibiendo mensajes de texto. El cliente envía un mensaje de solicitud al servidor. El servidor, en su turno, regresa un mensaje de respuesta.

Un mensaje HTTP consiste de una cabecera de mensaje y un cuerpo de mensaje opcional, separados por un línea en blanco, como se ilustra debajo:

####Mensaje HTTP de Solicitud

El formato de un mensaje HTTP de solicitud es como se muestra:

#####Línea de Solicitud

La primera línea de la cabecera es llamada request line (línea de solicitud), seguida de request headers (cabeceras de solicitud).

La línea de solicitud tiene la sintaxis siguiente:
> request-method-name request-URI HTTP-version

* request-method-name: El Protocolo HTTP define un conjunto de métodos de solicitud, p.ej. GET, POST, HEAD, y OPTIONS. El cliente puede usar uno de estos métodos para enviar una solicitud al servidor.
* request-URI: Especifica el recurso solicitado.
* HTTP-version: Dos versiones están actualmente en uso: HTTP/1.0 y HTTP/1.1.

Ejemplos de una línea de solicitud son:

> GET /test.html HTTP/1.1
> HEAD /query.html HTTP/1.0
> POST /index.html HTTP/1.1

#####Cabeceras de Solicitud

Las cabeceras de solicitud están en la forma de pares nombre:valor. Valores multiples, separados por comas, pueden ser especificados.

> request-header-name: request-header-value1, request-header-value2, …

Ejemplos de cabeceras de solicitud son:
> Host: www.xyz.com
> Connection: Keep-Alive
> Accept: image/gif, image/jpeg, */*
> Accept-Language: us-en, fr, cn

#####Ejemplo:

Los siguiente exhibe una muestra de un mensaje HTTP de solicitud:

####Mensaje HTTP de Respuesta

El formato de un mensaje HTTP de respuesta es como sigue:

#####Línea de Estatus

La primera línea es llamada la línea de estatus, seguida por las cabeceras de respuesta opcionales.

La línea de estatus tiene la siguiente sintaxis:

> HTTP-version status-code reason-phrase

* HTTP-version: La version de HTTP usada en esta sesión. Ya sea HTTP/1.0 o HTTP/1.1.
* status-code: Un numero de 3 dígitos generado por el servidor para reflejar el resultado de la solicitud.
* reason-phrase: Da una corta explicación al código de estatus.
* Códigos de estatus y frases de razón comunes son: “200 OK”, “404 Not Found”, “403 Forbidden”, “500 Internal Server Error”.

Ejemplos de línea de estatus son:
> HTTP/1.1 200 OK
> HTTP/1.0 404 Not Found
> HTTP/1.1 403 Forbidden

#####Cabeceras de Respuesta

Las cabeceras de respuesta están en la forma de pares nombre:valor:

> response-header-name: response-header-value1, response-header-value2, …

Ejemplos de cabeceras de respuesta son:
> Content-Type: text/html
> Content-Length: 35
> Connection: Keep-Alive
> Keep-Alive: timeout=15, max=100

EL cuerpo del mensaje de respuesta contiene los datos del recurso solicitado.

#####Ejemplo

Lo siguiente exhibe una muestra de mensaje de respuesta:

### Métodos de Solicitud HTTP

El protocolo HTTP define un conjunto de métodos de solicitud. Un cliente puede usar uno de estos métodos para enviar un mensaje de solicitud a un servidor HTTP. Los métodos son:

* GET: UN cliente usa la solicitud GET para obtener un recurso web del servidor.
* HEAD: Un cliente usa la solicitud HEAD para obtener la cabecera que un GET habría obtenido. Ya que la cabecera contiene la fecha cuando se modificaron los datos por última vez, esto puede ser usado para verificar con la copia local de cache.
* POST: Usado para publicar datos en el servidor.
* PUT: Pide al servidor guardar datos.
* DELTE: Pide al servidor borrar datos.
* TRACE: Pide al servidor regrese un rastro de diagnóstico de las acciones que toma.
* OPTIONS: Pide al servidor regresar la lista de los métodos de solicitud que soporta.
* CONNECT: Usado para indicarle a un proxy que haga una conexión a otro servidor y simplemente responda el contenido, sin intentar guardar o analizarlo.
* Otros métodos de extensión.

