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

* GET: Un cliente usa la solicitud GET para obtener un recurso web del servidor.
* HEAD: Un cliente usa la solicitud HEAD para obtener la cabecera que un GET habría obtenido. Ya que la cabecera contiene la fecha cuando se modificaron los datos por última vez, esto puede ser usado para verificar con la copia local de cache.
* POST: Usado para publicar datos en el servidor.
* PUT: Pide al servidor guardar datos.
* DELTE: Pide al servidor borrar datos.
* TRACE: Pide al servidor regrese un rastro de diagnóstico de las acciones que toma.
* OPTIONS: Pide al servidor regresar la lista de los métodos de solicitud que soporta.
* CONNECT: Usado para indicarle a un proxy que haga una conexión a otro servidor y simplemente responda el contenido, sin intentar guardar o analizarlo.
* Otros métodos de extensión.

### Método de Solicitud GET

GET es el método de solicitud HTTP más común. Un cliente usa GET para pedir (u obtener) una pieza de recurso de un servidor HTTP. Un mensaje de solicitud GET tiene la siguiente sintáxi:

> _**GET** request-URI HTTP-version
> (optional request headers)
> (blank line)
> (optional request body)_

* La palabra clave GET es sensible a mayúsculas, y debe estar en ellas.
* request-URI: especifica la ruta del recurso solicitado, la cual debe iniciar desde la raíz "/" del directorio base de documentos.
* HTTP-version: Ya sea HTTP/1.0 o HTTP/1.0. El cliente _negocia_ el protocolo que será usado en la sesión actual. Por ejemplo, el cliente tal vez solicite usar HTTP/1.1. Si el servidor no soporta HTTP/1.1, este informa al cliente el uso de HTTP/1.0.
* El cliente usa cabeceras de solicitud opcionales (como _Accept_, _Accept-language_, etc.) para negociar con el servidor y pedirle que entregue los contendidos preferidos (p.ej. en el lenguaje preferido por el cliente).
* El mensaje de solicitud GET tiene un cuerpo de solicitud opcional que contiene la cadena de consulta (a explicarse más tarde).

#### Probando Solicitudes HTTP

Hay muchas maneras de probar las solicitudes HTTP. Se pueden usar programas de utilidades como "telnet" o "hyperterm" (busque "telnet.exe" o "hyperterm.exe" bajo c:\windows), o escriba su propia programa de red para enviar un mensaje de solicitud en bruto a un servidor TTP para probar las varias solicitudes HTTP.

##### Telnet

"Telnet" es una utilidad de red muy útil. Se puede usar telnet para establecer una conexión TCP con un servidor; y emitir una solicitud HTTP. Por ejemplo, supongamos que se ha inciado el servidor HTTP en el servidor local (dirección IP 127.0.0.1) en el puerto 8000:

> **telnet**
> telnet> **help**
> ... telnet help menu ...
> telnet> **open 127.0.0.1 8000**
> Connecting To 127.0.0.1...
> **GET /index.html HTTP/1.0**
> (Hit enter twice to send the terminating blank line ...)
> ... HTTP response message ...

Telnet es un protocolo basasdo en caracteres. Cada caracter insertado en el cliente telnet será enviado al servidor inmediatamente. Por esto, no se puede hacer erroes de tecleo cuando se introducen los comandos, ya que delete y backspace serán enviados al servidor. Puede que se tenga que habilitar la opción "local echo" para ver los carateres que se introducen. Cheque el manual telnet (busque Windows' help) para ver detalles en el uso de telnet.

##### Programa de Red

También se podría escribir su propio programa de red para emitir una solicitud HTTP en bruto a un servidor HTTP. El programa debe primero establecer una conexión TCP/IP con el servidor. Una vez que la conexión es establecida, se puede emitir la solicitud.

Un ejemplo de programa de red escrito en java es como se muestra (asumiendo que el servidor HTTP está corriendo en el servidor local (dirección IP 127.0.0.1) en el puerto 8000):

```
import java.net.*;
import java.io.*;
   
public class HttpClient {
   public static void main(String[] args) throws IOException {
      // The host and port to be connected.
      String host = "127.0.0.1";
      int port = 8000;
      // Create a TCP socket and connect to the host:port.
      Socket socket = new Socket(host, port);
      // Create the input and output streams for the network socket.
      BufferedReader in
         = new  BufferedReader(
              new InputStreamReader(socket.getInputStream()));
      PrintWriter out
         = new PrintWriter(socket.getOutputStream(), true);
      // Send request to the HTTP server.
      out.println("GET /index.html HTTP/1.0");
      out.println();   // blank line separating header & body
      out.flush();
      // Read the response and display on console.
      String line;
      // readLine() returns null if server close the network socket.
      while((line = in.readLine()) != null) {
         System.out.println(line);
      }
      // Close the I/O streams.
      in.close();
      out.close();
   }
}
```

#### Solicitud GET HTTP/1.0

Lo siguiente muestra la respuesta a una solicitud GET HTTP/1.0 (emitida via telnet o propio programa de red - asumiendo que se ha inicilizado un servidor HTTP):

> **GET /index.html HTTP/1.0**
> (enter twice to create a blank line)

> **HTTP/1.1 200 OK**
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
>   
> Connection to host lost.

En este ejemplo, el cliente emite una solicitud GET para pedir un documento llamado "/index.html"; y negocia el uso de HTTP/1.0. Se necesita una línea en blanco después de la cabecera de solicitud. Este mensaje de solicitud no contiene un cuerpo.

El servidor recibe el mensaje de solicitud, interpreta y mapea la _request-URI_ a un documento bajo el directorio de documentos. Si el documento solicitado está disponible, el servidor regresa el documento con un código de estatus "200 OK". Las cabeceras de respuesta proveen la descripción necesaria del documento recibido, como la última fecha de modificación (_Last-Modified_), el MIME type (Content-Type), y la longitud del documento (Content-length). El cuerpo de respuesta contiene el documento solicitado. El navegador formateará y mostrará el documento de acuerdo al tipo de media (p.ej. Texto simple, HTML, JPEG, GIF, etc.) y otra información obtenida de las cabeceras de respuesta.

Notas:
* El método de solicitud GET es sensible a mayúsculas, y debe estar en ellas.
* Si el nombre del método de solicitud no se escribiío correctamente, el servidor regresará un mensaje de error "405 Method Not Allowed". P.ej. DELETE es un nombre válido de método, pero puede no ser permitido (o implementado) por el servidor.
* Si el _request-URI_ no existe, el servidor regresará un mensaje de error "404 Not Found". Se tendrá que emitir una _request-URI_ correcta, empezando de la raíz "/". De otra manera, el servidor regresaría el mensaje de error "400 Bad Request".
* Si _HTTP-version_ no existe o es incorrecto, el servidor regresará un mensaje de error "400 Bad Request".
* En HTTP/1.0, por default, el servidor cierra la conexión TCP después que la respuesta es entregada. Si se usa telnet para conectarse al servidor, el mensaje "Conexión al servidor perdida" aparece inmediatamente después de que el cuerpo de respuesta es recibido. Se podría usar una cabecera opcional de solicitud "Connection: Keep-Alive" para solicitar una conexión persistente (o keep-alive), para que otra solicitud pueda ser enviada a través de la misma conexión TCP y conseguir una mejor eficiencia de red. Del otro lado, HTTP/1.1 usa conexiones keep-alive predeterminadamente.

#### Código de Estatus de Respuesta

La primera línea del mensaje de respuesta (la línea de estatus) contiene el código de estatus de respuesta, el cual es generado por el servidor para indicar el resultado de la solicitud.

El código de estaus es un número de 3 dígitos:
* 1xx (Información): Solicitud recibida, el servidor continua con el proceso.
* 2xx (Éxito): La solicitud fue exitosamente recibida, entendida, aceptada y servida.
* 3xx (Redirección): Se requieren más acciones para completar la solicitud.
* 4xx (Error de cliente): La solicitud contien mala sintaxis o no puede ser entendida.
* 5xx (Error de servidor): El servidor falló en cumplir una solicitud aparentemente válida.

Algunos códigos de estatus comunmente econtrados:
* 100 Continue: El servidor recibió la solicitud y está en el proceso de dar una respuesta.
* 200 OK: La solicitud fue cumplida.
* 301 Move Permanently: El recurso solicitado ha sido movido permanentemente a una nueva locación. La URLdela nueva locación es dada en la cabecera de respuesta llamada _Location_. El cliente debería emitir una nueva solicitud a la nueva locación. La aplicación debería actualizar todas las referencias a esta locación.
* 302 Found & Redirect (or Move Temporarily): Igual que 301, pero la nueva locación es temporal. El cliente debería emitir una neuva solicitud, pero la aplicación no debería actualizar las referencias.
* 304 Not Modified: En respuesta al condicional _If-Modified-Since_ de solicitud GET, el servidor notifica que el recurso solicitado no ha sido modificado.
* 400 Bad Request: El servidor no pudo interpretar o entender la solicitud, probablemente debido a un error de sintaxis en el mensaje de solicitud.
* 401 Authentication Required: El recurso solicitado está protegido,y requiere credenciales de cliente (username/password). El cliente debería reenviar la solicitud con sus credenciales.
* 403 Forbidden: El servidor se reúsa a proveer el recurso, sin importar la identidad del cliente.
* 404 Not Found: El recurso solicitado no puede ser encontrado en el servidor.
* 405 Method Not Allowed: El método de solicitud usado, p.ej., POST, PUT, DELETE, es un método válido. Sin embargo, el servidor no permite ese método para el recurso solicitado.
* 408 Request Timeout:
* 414 Request URI too Large:
* 500 Internal Server Error: El servidor está confundido, a menudo causado por un error en el lado del servidor del programa que responde a la solicitud.
* 501 Method Not Implemented: El método de solicitud es inválido (podría ser por un error de tecleo, p.ej., "GET" escrito como "Get").
* 502 Bad Gateway: Proxy o Gateway indica que recibe un mala respuesta del servidor.
* 503 Service Unavailable: El servidor no puede responder debido a sobrecarga o mantenimiento. El cliente puede intentar más tarde.
* 504 Gateway Timeout: Proxy o Gateway indica que recibe un receso del servidor.

#### Más ejemplos de Solicitud GET HTTP/1.0

##### Ejemplo: Método de Solicitud mal escrito
En la solicitud, "GET" está mal escrito como "get". El servidor regresa un error "501 Method Not Implemented". La cabecera de respuesta "Allow" indica al cliente los métodos permitidos.

> **get** /test.html HTTP/1.0
> (enter twice to create a blank line)

> HTTP/1.1 501 **Method Not Implemented**
> Date: Sun, 18 Oct 2009 10:32:05 GMT
> Server: Apache/2.2.14 (Win32)
> **Allow: GET,HEAD,POST,OPTIONS,TRACE**
> Content-Length: 215
> Connection: close
> Content-Type: text/html; charset=iso-8859-1
>   
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>501 Method Not Implemented</title>
> </head><body>
> <h1>Method Not Implemented</h1>
> <p>get to /index.html not supported.<br />
> </p>
> </body></html>

##### Ejemplo: 404 File Not Found:
In esta solicitud GET, la URL de solicitud "/t.html" no se puede encontrar bajo el directorio de documento del servidor. El servidor regresa un error "404 Not Found".

> GET **/t.html** HTTP/1.0
> (enter twice to create a blank line)


> HTTP/1.1 404 Not Found
> Date: Sun, 18 Oct 2009 10:36:20 GMT
> Server: Apache/2.2.14 (Win32)
> Content-Length: 204
> Connection: close
> Content-Type: text/html; charset=iso-8859-1
>    
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>404 Not Found</title>
> </head><body>
> <h1>Not Found</h1>
> <p>The requested URL /t.html was not found on this server.</p>
> </body></html>

##### Ejemplo: Número de Versión HTTP Incorrecto
En esta solicitud GET, la versión HTTP fue mal escrita, resultando en una mala sintaxis.El servidor regresa un erro "404B Bad Request". La version HTTP debería ser ya sea HTTP/1.0 o HTTP/1.1.

> GET /index.html **HTTTTTP/1.0**
> (enter twice to create a blank line)

> HTTP/1.1 **400 Bad Request**
> Date: Sun, 08 Feb 2004 01:29:40 GMT
> Server: Apache/1.3.29 (Win32)
> Connection: close
> Content-Type: text/html; charset=iso-8859-1
> 
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <HTML><HEAD>
> <TITLE>400 Bad Request</TITLE>
> </HEAD><BODY>
> <H1>Bad Request</H1>
> Your browser sent a request that this server could not understand.<P>
> The request line contained invalid characters following the protocol string.<P><P>
> </BODY></HTML>

Nota: El último Apache 2.2.14 ignora este error y regresa el documento con el código de estatus "200 OK".

##### Ejemplo: Request-URI Incorrecta
En la siguiente solicitud GET, la _request-URI_ no comenzó desde la raíz "/", resultando en "bad request".

> GET test.html HTTP/1.0
> (blank line)

> HTTP/1.1 **400 Bad Request**
> Date: Sun, 18 Oct 2009 10:42:27 GMT
> Server: Apache/2.2.14 (Win32)
> Content-Length: 226
> Connection: close
> Content-Type: text/html; charset=iso-8859-1
>    
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>400 Bad Request</title>
> </head><body>
> <h1>Bad Request</h1>
> <p>Your browser sent a request that this server could not understand.<br />
> </p>
> </body></html>

##### Ejemplo: Conexión Keep-Alive
Predeterminadamente, para solicitud GET HTTP/1.0, el servidor cierra la conexión TCP una vez que la respuesta es entregada. Se podría solicitar que la conexión TCP se mantenga, (para mandar otra solicitud usando la misma conexión TCP, y así mejorar la eficiencia de red), usando una cabecera opcional de solicitud "_Connection: Keep-Alive_". El servidor incluye una cabecera de respuesta de conexión Keep-Alive para informar al cliente que puede enviar otra solicitud usando esta conexión, antes del receso de keep-alive. Otra cabecara de respuesta, "_Keep-Alive: timeout=x, max=x_" indica al cliente el receso (en segundos) y el máximo número de solicitudes que pueden ser enviadas a través de esta conexión persistente.

> GET /test.html HTTP/1.0
> Connection: Keep-Alive
> (blank line)

> HTTP/1.1 200 OK
> Date: Sun, 18 Oct 2009 10:47:06 GMT
> Server: Apache/2.2.14 (Win32)
> Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
> ETag: "10000000565a5-2c-3e94b66c2e680"
> Accept-Ranges: bytes
> Content-Length: 44
> Keep-Alive: timeout=5, max=100
> Connection: Keep-Alive
> Content-Type: text/html
>    
> <html><body><h1>It works!</h1></body></html>

Notas:
* El mensaje "Connection to host lost" (para telnet) aparece después del receso "keep-alive".
* Antés de que el mensaje "Connection to host lost" aparezca (i.e. receso keep-alive), se puede enviar otra solicitud a través de la misma conexión TCP.
* La cabecera "Connection: Keep-Alive" no es sensible a mayúsculas. El espacio es opcional.
* Si una cabecera opcional está mal escrita o es inválida, será ignorada por el servidor.

##### Ejemplo: Acceso a un Recurso Protegido
La siguiente solicitud GET intento accesar un recurso protegido. El servidor regresa un error "403 Forbidden". En este ejemplo, el directorio "_htdocs\forbidden_" está configurado para denegar todo acceso en el archivo de configuración  "_httpd.conf_" del servidor HTTP Apache de la siguiente manera:

> <Directory "C:/apache/htdocs/forbidden">
>    Order deny,allow
>    deny from all
> </Directory>

> GET /forbidden/index.html HTTP/1.0
> (blank line)

> HTTP/1.1 403 Forbidden
> Date: Sun, 18 Oct 2009 11:58:41 GMT
> Server: Apache/2.2.14 (Win32)
> Content-Length: 222
> Keep-Alive: timeout=5, max=100
> Connection: Keep-Alive
> Content-Type: text/html; charset=iso-8859-1
>    
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>403 Forbidden</title>
> </head><body>
> <h1>Forbidden</h1>
> <p>You don't have permission to access /forbidden/index.html
> on this server.</p>
> </body></html>

#### Solicitud GET HTTP/1.1

Un servidor HTTP/1.1 soporta los llamados virtual hosts (servidores virtuales). Eso es, el mismo servidor físico podría tener varios servidores virtuales, con diferentes hostnames (p.ej. www.nowhere123.com y www.test909.com) y sus propios directorios raíz de documentos dedicados. Por tanto, en una solicitud HTTP/1.1, es obligatorio incluir una cabecera de solicitud llamada "Host", para seleccionar uno de los servidores virtuales.

##### Ejemplo: Solicitud GET HTTP/1.1
HTTP/1.1 mantiene conexión persistente (o keep-alive) de manera predeterminada para mejorar la eficiencia de red. Se puede usar una cabecera de solicitud "Connection: Close" para pedir al servidor cerrar la conexión TCP una vez que la respuesta fue entregada.

> GET /index.html HTTP/1.1
> **Host: 127.0.0.1**
> (blank line)

> HTTP/1.1 200 OK
> Date: Sun, 18 Oct 2009 12:10:12 GMT
> Server: Apache/2.2.14 (Win32)
> Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
> ETag: "10000000565a5-2c-3e94b66c2e680"
> Accept-Ranges: bytes
> Content-Length: 44
> Content-Type: text/html
>    
> <html><body><h1>It works!</h1></body></html>

##### Ejemplo: Cabecera de Servidor HTTP/1.1 Faltante
El siguiente ejemplo muestra que la cabecera "Host" es obligatoria en una solicitud HTTP/1.1. Si esta está faltante,el servidor regresa un error "400 Bad Request".

> GET /index.html HTTP/1.1
> (blank line)

> HTTP/1.1 400 Bad Request
> Date: Sun, 18 Oct 2009 12:13:46 GMT
> Server: Apache/2.2.14 (Win32)
> Content-Length: 226
> Connection: close
> Content-Type: text/html; charset=iso-8859-1
>    
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>400 Bad Request</title>
> </head><body>
> <h1>Bad Request</h1>
> <p>Your browser sent a request that this server could not understand.<br />
> </p>
> </body></html>

#### Solicitudes GET Condicionales

En todos los ejemplos anteriores, el servidor regresa el documento entero si la solicitud puede ser completada (incondicional). Se puede usar cabeceras de solicitud adicionales para emitir una "solicitud condicional". Por ejemplo, para pedir el documento basado en la fecha en que se modificó por última vez (para decidir si debería usar una copia local de cache o no), o para pedir por una porción del documento (o rango) en lugar del documento entero (útil para descargar documentos muy grandes).

Las cabeceras condicionales son:

* _If-Modified-Since_ (checa por el código de estatus de respuesta "304 Not Modified")
* _If-Unmodified-Since_
* _If-Match_
* _If-None-Match_
* _If-Range_

#### Cabeceras de Solicitud

Esta sección describe algunos de las cabeceras de solicitud usadas comúnmente. Refiérase a la Especificación HTTP para más detalles. La sintaxis del nombre de la cabecera es palabras con mayúscula inicial unidas con un guión (-), p.ej., _Content-Length_, _If-Modified-Since_.

**Host: domain-name** - HTTP/1.1 soporta servidores virtuales. Multiples nombres DNS (p.ej., www.nowhere123.com y www.nowhere456.com) pueden residir en el mismo servidor físico, con sus propios directorios raíz de documentos. La cabecera _Host_ es obligatoria en HTTP/1.1 para seleccionar uno de los servidores.

Las siguientes cabeceras pueden se usadas para "negociación de contenido" por el cliente para pedir al servidor que entregue el tipo preferido de documento (en términos del tipo de media, p.ej. JPEG vs.GIF, o el lenguaje usado p.ej. Inglés vs. Francés) si el servidor mantiene multiples versiones del mismo documento.

**Accept:mime-type-1, mime-type-2, ...** - EL cliente puede usar la cabecera _Accept_ para decirle al servidor los tipos MIME que puede soportar y que prefiere. Si el servidor tiene múltiples versiones  del documento solicitado (p.ej. una imagen GIF y JPEG, o un documento en TXT y PDF), puede checar esta cabecera para decidir cual versión entregar al cliente. (P.ej.,PNG es más avanzado que GIF, pero no todos los navegadores soportan PNG.) Este proceso es llamadado "Negociación de Tipo de Contenido".

**Accept-Charset: Charset-1, Charset-2, …** - Para la negociación del conjunto caracteres, el cliente puede usar esta cabecera para decir al servidor cual conjunto de caracteres puede soportar o prefiere. Ejemplos de conjuntos de caracteres son ISO-8859-1, ISO-8859-5, BIG5, UCS2, UCS4, UTF8.

**Accept-Enconding: encoding-method-1, encondig-method-2, …** - El cliente pude usar esta cabecera para decirle al servidor el tipo de codificación que soporta. Si el servidor tiene una versión codificada (o comprimida) del documento solicitado, puede regresar una versión codificado soportada por el cliente. El servidor también puede elegir codificaren documento antes de regresarlo al cliente para reducir el tiempo de transmisión. El servidor debe definir la cabecera de solicitud “Content-Encoding” para informar al cliente que el documento regresado está codificado. Métodos comunes de codificación son “x-gzip (.gz, .tgz)” y “x-compress (.Z)”.

**Connection: Close|Keep-Alive**  - El cliente puede usar esta cabecera para decirle al servidor su debe cerrar la conexión después de la solicitud, o si debe mantenerla viva para otra solicitud. HTTP/1.1 usa conexiones persistentes (keep-alive) de manera predeterminada. HTTP/1.0 cierra las conexiones.

**Referer: referer-URL** - El cliente puede usar esta cabecera para indicar el referente de la solicitud. If se hace click en un link de una página web 1 para visitar una página 2, la página 1 es el referente a la página 2. Todos los principales navegadores definen esta cabecera, la cual puede ser usada para rastrear de donde viene la solicitud (para publicidad web, o para personalización de contenido). De cualquier manera, esta cabecera no es confiable y puede ser fácilmente falsificada. Note que Referrer está mal escrito como “Referer” (desafortunadamente, se debe seguir también).

**User-Agent: browser-type** - Identifica el tipo de navegador usado para hacer la solicitud. El servidor puede usar esta información para regresar diferente documentación dependiendo del tipo de navegador.

**Content-Length: number-of-bytes** - Usado por la solicitud POST, para informar al servidor la longitud del cuerpo de solicitud.

**Content-Type: mime-type** - Usado por la solicitud POST, para ifnroamar al servidor el tipo de media del cuerpo de solicitud.

**Cache-Control: no-cache|…** - El cliente puede usar esta cabecera para especificar como las páginas deben ser guardadas en cache por el servidor proxy. “no-cache” requiere que el proxy obtenga un copia fresca del servidor original, aún cuando una copia local de cache está disponible. (Un servidor HTTP/1.0 no reconoce “Cache-Control: no-cache”. En su lugar, usa “Pragma: no-cache”. Incluya ambas cabeceras de solicitud si no se esta seguro de la visión del servidor.)

**Authorization:** Usada por el cliente para proveer sus credenciales (username/password) para accesar recursos protegidos. (Esta cabecera será descrita en un capítulo más avanzado en autenticación.

**Cookie: cookie-name-1=cookie-value-1, cookie-name-2=cookie-value-2, …** - El cliente usa esta cabecera para regresar las cookies de regreso al servidor, las cuales fueron antes definidas por el servidor para administración de estado. (Esta cabecera será discutida en un capítulo más adelante en administración de estado.)

**If-Modified-Since: date** - Dice al servidor que envíe la página sólo si ha sido modificada después de una fecha especifica.

#### Solicitud GET por un Directorio























