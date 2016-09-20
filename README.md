#HTTP (HyperText Transfer Protocol)

##Basics

###Introduction

####The Web

El Internet (o la Web) es un sistema de información cliente/servidor distribuido masivo, tal como se muestre en el siguiente diagrama:

![Alt](/images/screen1.png "Title")

Muchas aplicaciones corren concurrentemente a través de la Web, tales como navegación o “surfeo” de la Web, e-mail, transferencia de archivos, transmisión de audio y video, y más. Para que se lleve a cabo una comunicación apropiada entre el cliente y el servidor, estas aplicaciones deben estar de acuerdo en un protocolo a nivel de aplicación, como lo son HTTP, FTP, SMTP, POP, etc.

####HyperText Transfer Protocol (HTTP)

HTTP (HyperText Transfer Protocol) es tal vez el más popular protocolo de aplicación usado en el Internet (o la Web).
* HTTP es un protocolo solicitud-respuesta, cliente-servidor asimétrico como se ilustra. Un cliente HTTP envía un mensaje de solicitud a un servidor HTTP. El servidor,en su turno, regresa un mensaje de respuesta. En otras palabras, HTTP es un protocolo de llamada, el cliente “llama” información del servidor (en su lugar el servidor envía información al cliente).

![Alt](/images/screen2.png "Title")

* HTTP es un protocolo sin estados. En otras palabras, la solicitud actual no sabe lo que se ha hecho en solicitudes anteriores.
* HTTP permite la negociación y representación de datos, para permitir la construcción de sistemas independientemente de los datos que están siendo transferidos.
* Citando de RFC2616: “El Protocolo de Transferencia de Hipertexto (HTTP) es un protocolo de aplicación para sistemas de información distribuidos, colaborativos, y de hipermedia. Es un protocolo genérico y sin estados que puede ser usado para muchas tareas más allá de su uso para el hipertexto, tales como la asignación de nombre a servidores y sistemas de manejo de objetos distribuidos, a través de la extensión de sus métodos de solicitud, códigos de error, y cabeceras.”

####Browser

Cuando sea que emites una URL desde tu navegador para obtener un recurso web usando HTTP, p. ej. http://www.nowhere123.com/index.html, el navegador transforma la URL en un mensaje de solicitud y lo envía al servidor HTTP. El servidor HTTP interpreta este mensaje, y te regresa un mensaje de respuesta apropiado, el cual es o el recurso que solicitaste o un mensaje de error.
El proceso está ilustrado debajo:

![Alt](/images/screen3.png "Title")

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

![Alt](/images/screen4.png "Title")

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

![Alt](/images/screen5.png "Title")

####Mensaje HTTP de Solicitud

El formato de un mensaje HTTP de solicitud es como se muestra:

![Alt](/images/screen6.png "Title")

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

![Alt](/images/screen7.png "Title")

####Mensaje HTTP de Respuesta

El formato de un mensaje HTTP de respuesta es como sigue:

![Alt](/images/screen8.png "Title")

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

![Alt](/images/screen9.png "Title")

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

#### Solicitud GET de un Directorio

Suponga que un directorio llamado “testdir” está presente en el documento base “htdocs”.

Si el cliente emite una solicitud GET a “/testdir/“ (al directorio).

	1. El servidor regresará “/testdir/index.html” si el directorio contiene un archive “index.html”.
	2. De otra forma, el servidor regresa la lista de directorios, si la lista de directorios está habilitada en la configuración del servidor.
	3. De otra forma, el servidor regresa “404 Page Not Found”.

Es interesante tomar nota que si un cliente emite una solicitud GET a “/testdir” (sin especificar la ruta de directorio “/“), el servidor regresa “301 Move Permanently” con una nueva “Location” de “/testdir/“, como sigue.

> GET /testdir HTTP/1.1
> Host: 127.0.0.1
> (blank line)

> HTTP/1.1 301 Moved Permanently
> Date: Sun, 18 Oct 2009 13:19:15 GMT
> Server: Apache/2.2.14 (Win32)
> Location: http://127.0.0.1:8000/testdir/
> Content-Length: 238
> Content-Type: text/html; charset=iso-8859-1
>    
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <html><head>
> <title>301 Moved Permanently</title>
> </head><body>
> <h1>Moved Permanently</h1>
> <p>The document has moved <a href="http://127.0.0.1:8000/testdir/">here</a>.</p>
> 
> </body></html>

La mayoría de los navegadores seguirán con otra solicitud a “/testdir/“. Por ejemplo, si se emite http://127.0.0.1:8000/testdir sin “/“ desde un navegador, se podría notar que “/“ fue añadido a la dirección después de que la respuesta fue dad. La moraleja de la historia es: se debería incluir el “/“ para que una solicitud de directorio guarde una solicitud GET adicional.

#### Emitir una Solicitud GET a través de un Servidor Proxy

Para enviar una solicitud GET a través de un servidor proxy, (a) establezca una conexión TCP al servidor proxy; (b) use una request-URI absoluta http://hostname:port/path/fileName al servidor objetivo.

EL siguiente rastro fue capturado usando telnet. Una conexión establecida con el servidor proxy, y una solicitud GET emitida. Una request-URI absoluta es usada en la linea de solicitud.

> GET http://www.amazon.com/index.html HTTP/1.1
> Host: www.amazon.com
> Connection: Close
> (blank line)

> HTTP/1.1 302 Found
> Transfer-Encoding: chunked
> Date: Fri, 27 Feb 2004 09:27:35 GMT
> Content-Type: text/html; charset=iso-8859-1
> Connection: close
> Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
> Set-Cookie: skin=; domain=.amazon.com; path=/; expires=Wed, 01-Aug-01 12:00:00 > GMT
> Connection: close
> Location: http://www.amazon.com:80/exec/obidos/subst/home/home.html
> Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
>    
> ed
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> <HTML><HEAD>
> <TITLE>302 Found</TITLE>
> </HEAD><BODY>
> <H1>Found</H1>
> The document has moved
> <A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
> here</A>.<P>
> </BODY></HTML>
>    
> 0

Tome nota de que la respuesta es regresada por pedazos.

### Método de Solicitud “HEAD”

La solicitud HEAD es similar a GET. Sin embargo, el servidor regresa solamente la cabecera de respuesta sin el cuerpo de respuesta, el cual contiene el documento en sí. La solicitud HEAD es útil para checar las cabeceras, tales como Last-Modified, Content-Type, Content-Length, anteved enviar una solicitud GET apropiada para obtener el documento.

La sintaxis de la solicitud HEAD es como sigue:
> HEAD request-URI HTTP-version
> (other optional request headers)
> (blank line)
> (optional request body)

##### Ejemplo

> HEAD /index.html HTTP/1.0
> (blank line)

> HTTP/1.1 200 OK
> Date: Sun, 18 Oct 2009 14:09:16 GMT
> Server: Apache/2.2.14 (Win32)
> Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
> ETag: "10000000565a5-2c-3e94b66c2e680"
> Accept-Ranges: bytes
> Content-Length: 44
> Connection: close
> Content-Type: text/html
> X-Pad: avoid browser bug

Note que la respuesta consiste de la cabecera únicamente sin el cuerpo, el cual contiene el documento en sí.

### Método de Solicitud “OPTIONS”

Un cliente puede usar un método de solicitud OPTIONS para consultar al servidor cuales métodos son soportados. La sintaxis para un mensaje de solicitud OPTIONS es:
> OPTIONS request-URI|* HTTP-version
> (other optional headers)
> (blank line)

“+” puede ser usado en lugar de una request-URI para indicar que la solicitud no se aplica a ningún recurso en particular.

##### Ejemplo

Por ejemplo, la siguiente solicitud OPTIONS es mandado a través de un servidor proxy:

> OPTIONS http://www.amazon.com/ HTTP/1.1
> Host: www.amazon.com
> Connection: Close
> (blank line)

> HTTP/1.1 200 OK
> Date: Fri, 27 Feb 2004 09:42:46 GMT
> Content-Length: 0
> Connection: close
> Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
> Allow: GET, HEAD, POST, OPTIONS, TRACE
> Connection: close
> Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
> (blank line)

Todos los servidores que permiten una solicitud GET permitirán una solicitud HEAD. A veces HEAD no es listada.


### Método de Solicitud “TRACE”

Un cliente puede enviar una solicitud TRACE para pedir al servidor regrese un rastro de diagnóstico.

La solicitud TRACE toma la siguiente sintaxis:
> TRACE / HTTP-version
> (blank line)

##### Ejemplo

EL siguiente ejemplo muestra una solicitud TRACE emitida a través de un servidor proxy.

> TRACE http://www.amazon.com/ HTTP/1.1
> Host: www.amazon.com
> Connection: Close
> (blank line)

> HTTP/1.1 200 OK
> Transfer-Encoding: chunked
> Date: Fri, 27 Feb 2004 09:44:21 GMT
> Content-Type: message/http
> Connection: close
> Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
> Connection: close
> Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
>    
> 9d
> TRACE / HTTP/1.1
> Connection: keep-alive
> Host: www.amazon.com
> Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
> X-Forwarded-For: 155.69.185.59, 155.69.5.234
>    
> 0

(Para comparar la solicitud TRACE con la ruta de rastreo)

### Envío de Formulario de Datos HTML y Cadena de Consulta

En muchas aplicaciones de Internet, tales como comercio electrónico y motores de búsqueda, se requiere que los clientes envien información adicional al servidor (p.ej. el nombre, dirección, las palabras clave de búsqueda). Basados en los datos enviados, el servidor toma la acción apropiada y produce una respuesta personalizada.

Los clientes son presentados usualmente con un formulario (producido usando una etiqueta HTML <form>). Una vez que se completa la información solicitada y se presiona el botón de envío, el navegador empaqueta el formulario de datos y los envía al servidor, usando ya sea una solictud GET o POST.

Lo siguiente es una muestra de formulario HTML, el cual es producido el siguiente script HTML:

```
<html>
<head><title>A Sample HTML Form</title></head>
<body>
  <h2 align="left">A Sample HTML Data Entry Form</h2>
  <form method="get" action="/bin/process">
    Enter your name: <input type="text" name="username"><br />
    Enter your password: <input type="password" name="password"><br />
    Which year?
    <input type="radio" name="year" value="2" />Yr 1
    <input type="radio" name="year" value="2" />Yr 2
    <input type="radio" name="year" value="3" />Yr 3<br />
    Subject registered:
    <input type="checkbox" name="subject" value="e101" />E101
    <input type="checkbox" name="subject" value="e102" />E102
    <input type="checkbox" name="subject" value="e103" />E103<br />
    Select Day:
    <select name="day">
      <option value="mon">Monday</option>
      <option value="wed">Wednesday</option>
      <option value="fri">Friday</option>
    </select><br />
    <textarea rows="3" cols="30">Enter your special request here</textarea><br />
    <input type="submit" value="SEND" />
    <input type="reset" value="CLEAR" />
    <input type="hidden" name="action" value="registration" />
  </form>
</body>
</html>
```

![Alt](/images/screen10.png "Title")

Un formulario contiene campos. Los tipos de campo incluyen:
* Text Box: producido por `<input type="text">`.
* Password Box: producido por `<input type="password">`.
* Radio Button: producido por `<input type="radio">`.
* Checkbox: producido por `<input type="checkbox">`.
* Selection: producido por `<select>` y `<option>`.
* Text Area: producido por `<textarea>`.
* Submit Button: producido por `<input type="submit">`.
* Reset Button: producido por `<input type="reset">`.
* Hidden Field: producido por `<input type="hidden">`.
* Button: producido por `<input type="button">`.

Cada campo tiene un nombre y puede tomar 
un valor específico. Una vez que el cliente rellena los campos y presione el boton de envío, el navegador colecta cada uno de los nombres y valores de los campos, los empaqueta en pares "name=value", y concatena todos los camposjuntos usando "&" como un separador de campo. Esto es conocido como Cadena de Consulta. Enviará la cadena de consulta al servidor como parte de la solicitud.

> name1=value1&name2=value2&name3=value3&...

Caracteres especiales no son permitidos dentro de la cadena de consulta. Estos deben ser reemplazados por un "%" seguido del códigoASCII en hexadecimal, "~" es remplazado por "%7E", "#" por "%23" y así con los demás. Ya que el espacio en blanco es bastante común, este puede ser reemplazado ya sea por "%20" o "+" (el caracter "+" de ser reemplazado por "%2B"). Este proceso de reemplazo es llamado _URL-encoding_, y el resultado es una cadena de consulta URL-encoded. Por ejemplo, supongamos que hay 3 campos dentro de un formulario, con nombre/valor de "name=Peter Lee", "address=#123 Happy Ave" y "language=C++", la cadena de cosultado codificada en URL es:

`name=Peter+Lee&address=%23123+Happy+Ave&Language=C%2B%2B`

La cadena de cosulta puede ser mandada al servidor usando ya sea una solicitud HTTP con el método GET o POST, el cual es especificado en el atributo "method" de `<form>.

> <form method="get|post" action="url">

Si el método de solicitud GET es usado, la cadena de consulta URL-encoded será anexada detrás de la request-URI después de un caracter "?":

> GET request-URI?query-string HTTP-version
> (other optional request headers)
> (blank line)
> (optional request body)


El uso de la solicitud GET para enviar la cadena de consulta tiene los siguientes inconvenientes:

* La cantidad de datos que se podrían anexar detrás de la request-URI es limitada. Si esta cantidad es excede un límite específico al servidor, el servidor regresaría un error "414 Request URI too Large".
* La cadena de consulta URL-encoded aparecería en la barra de dirección del navegador.

El método de solicitud POST supera estos inconvenientes. Si POST es usado, la cadena de solicitud será enviada en el cuerpo del mensaje de solicitud, donde la cantidad no es limitada. Las cabeceras de solicitud Contet-Type y Conteny-Length son usadas para notificar al servidor del tipo y la longitud de la cadea de consulta. La cadena no aparecerá en la barra de dirección del navegador. El método POST será discutido más tarde.

#####Ejemplo

El siguiente formulario HTML es usado para colectar el nombre de usuario y contraseña en un menu de entrada.

```
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="get" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

![Alt](/images/screen11.png "Title")

El método de solicitud GET es usado para enviar la cadena de consulta. Supongamos que el usario introduce "Peter Lee" como el username, "123456" como contraseña; y hace click en el boton de enviar. La siguiente solicitud GET es:

```
GET /bin/login?user=Peter+Lee&pw=123456&action=login HTTP/1.1
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 127.0.0.1:8000
Connection: Keep-Alive
```

Nótese que aun sí la contraseña que se introduce no se muestra en la pantalla, es mostrada claramente en la barra de dirección del navegador. Nunca se debería enviar una contraseña sin la apropiada encriptación.

`http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login`

### URL y URI

#####URL (Uniform Resource Locator)

Una URL, definida en RFC 2396, es usada para identificar un recurso a través de la web de forma única. URL tiene la siguiente sintaxis:

> protocol://hostname:port/path-and-file-name

Hay 4 partes en una URL:
1. Protocol: El protocolo de aplicación usado por el cliente y el servidor, p.ej. HTTP, FTP, y telnet.
2. Hostname: El nombre de dominio DNS (p.ej. www.nowhere123.com) o dirección IP (p.ej. 192.128.1.2) del servidor.
3. Port: El numero de puerto TCP en que el servidor esta escuchando por solicitudes entrantes de los clientes.
4. Path-and-file-name: El nombre y locación del recurso solicitado, bajo el directorio de documentos del servidor.

Por ejemplo, en la URL _http://www.nowhere123.com/docs/index.html_, el protocolo de comunicación es HTTP; el nombre de servidor es www.nowhere123.com. El número de puerto no fue especificado en la URL, y toma el numero predeterminado, el cual es el puerto TCP 80 para HTTP [STD 2]. La ruta y el nombre de archivo para que el recurso sea localizado es "/docs/index.html".

Otros ejemplos de URL son:

```
ftp://www.ftp.org/docs/test.txt
mailto:user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```

#####URL Codificada

Una URL no puede contener carateres especiales, como espacios en blanco o tildes. Los caracteres especiales son codificados, en la forma de %xx, donde xx es el codigo ASCII en hexadecimal. Por ejemplo '~' es codificado como %7e; '+' es codificado como %2b. Un espacio en blanco puede ser codificado como %20 o '+'. La URL despuésde ser codificada es llamda encoded URL.

#####URI (Uniform Resource Identifier)

URI (Identificador Uniforme de Recurso), definida en RFC3986, es más general que la URL, la cual puede hasta localizar un fragmento dentro de un recurso. La sintaxis de la URI para el protocolo HTTP es:

> http://host:port/path?request-parameters#nameAnchor

* Los parámetros de solicitud, en la forma de pares nombre=valor, son separados de la URL por un '?'. Los pares name=value son separados por un '&'.
* EL #nameAnchor identifica un fragmento dentro del documento HTML, definido via la etiqueta de anclaje <a name="anchorName">...</a>.
* Reescritura de URL para administración de sesión, p.ej., "...;sessionID=xxxxxx".

### Método de Solicitud "POST"
El método POST es usado para "postear" datos adicionales al servidor (p.ej., envíode formulario de datos HTML o subir un archivo). Emitir una URL HTTP desde el navegador siempre acciona una solicitud GET. Para accionar una solicitud POST, se puede usar un formulario HTML con el atributo _method="post"_ o escribir un propio programa de red. Para enviar un formulario de datos HTML, la solicitud POST es lo mismo que GET excepto que la cadena de cosulta URL-codificada es enviada en el cuerpo de solicitud, en vez de anexarla detrás de la request-URI.

La solicitud POST toma la siguiente sintaxis:

> POST request-URI HTTP-version
> Content-Type: mime-type
> Content-Length: number-of-bytes
> (other optional request headers)
>   
> (URL-encoded query string)

Las cabeceras de solicitud Content-Type y Content-Length son necesarias en la solicitud POST para informar al servidor el tipo de media y la longitud del cuerpo de solicitud.

#####Ejemplo: Envío de Formulario de Datos usando el Método de Solicitud POST

Se usa el mismo script HTML que arriba, pero se cambia el metodo de solicitud a POST.

```
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="post" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

Supongamos que el usuario introduce "Peter Lee" como nombre de usuaruo y "123456" como contraseña, y hace click en el botón de enviar, la siguiente solicitud POST sería generada por el navegador:

```
POST /bin/login HTTP/1.1
Host: 127.0.0.1:8000
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 37
Connection: Keep-Alive
Cache-Control: no-cache
   
User=Peter+Lee&pw=123456&action=login
```

Nótese que la cabecera Content-Type informa al servidor que los datos son URL-encoded (con un tipo MIME especial _application/x-www-form-urlencoded_), y la cabecera Content-Length dice al servidor cuantos byts leer del cuerpo del mensaje.

##### POST vs GET para el Envío de Formularios de Datos

Como fue mencionado en la sección anterior, la solicitud POST tiene las siguientes ventajas comparada con GET en el envío de la cadena de consulta:
* La cantidad de datos que pueden ser publicados es ilimitada, ya que son guardados en el cuerpo de solicitud, el cual es a menudo enviado al servidor en una tranmisión de datos separada.
* La cadena de consulta no s mostrada en la barra de dirección del navegador.

Nótese que aunque la contraseña no es mostrada en la barra de dirección del navegador, es transimitida al servidor en texto claro, y sujeta a husmeo de red. Así que, enviar una contraseña usando una solicitud POST absolutamente no es seguro.

### Subida de Datos usando una Solicitud POST multipart/form-data.
 "RFC 1867: Form-based File upload in HTML" especifica como un archivo puede ser subido al servidor usando POST desde un formulario HTML. Un nuevo atributo _type="file"_ se añadió a la etiqueta <input> de <form>HTML para soportar la subida de archivos. Los datos POST de subida de archivos no son URL-encoded (en el estándar _application/x-www-form-urlencoded), pero usa un nuevo tipo MIME de _multipart/form-data_.

 ##### Ejemplo

 El siguiente formulario HTML puede ser usado para el envío de archivos:
 ```
 <html>
<head><title>File Upload</title></head>
<body>
  <h2>Upload File</h2>
  <form method="post" enctype="multipart/form-data" action="servlet/UploadServlet">
    Who are you: <input type="text" name="username" /><br />
    Choose the file to upload:
    <input type="file" name="fileID" /><br />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

![Alt](/images/screen12.png "Title")

Cuando el navegador encontró un etiqueta `<input>`con atributo _type="file"_, muestra una caja de texto y un botón "browse...", para permitir al usuario elegir el archivo a subir.

Cuando el usuario hace click en el botón de enviar, el navegador envía el formulario dedatos y el contenido del los arhivos seleccionados. El tipo de codificación anterior "application/x-www-form-urlencoded" es ineficiente para el envío de datos binarios y caracteres no-ASCII. Un nuevo tipo de media "multipart/form-data" es usado en su lugar.

Cada parte identifica el nombre de la entrada dentro del formulario HTML original, en el tipo de contenido si el medio es conocido, o como "application/octet-stream" de otra manera.

El archivo local original podría ser suministrado como un parámetro "filename", o en la cabecera "Content-Disposition: form-data".

Un ejemplo del mensaje POST para la subida de archivos es como sigue:

```
POST /bin/upload HTTP/1.1
Host: test101
Accept: image/gif, image/jpeg, */*
Accept-Language: en-us
Content-Type: multipart/form-data; boundary=---------------------------7d41b838504d8
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 342
Connection: Keep-Alive
Cache-Control: no-cache
   
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="username" 
Peter Lee
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="fileID"; filename="C:\temp.html" Content-Type: text/plain 
<h1>Home page on main server</h1> 
-----------------------------7d41b838504d8--
```

Servlet 3.0 provee soporte incluído para el procesamiento de la subida de archivos. Lea "Uploading Files in Servlet 3.0".

### Método de Solicitud "CONNECT"

La solicitud HTTP CONNECT es usada para pedir a un proxy que haga una conexión a otro servidor y simplemente transmita el contenido, en vez de tratar de analizar o guardar el mensaje. Esto es usado a menudopara hacer una conexión a través de un proxy.

### Otros Métodos de Solicitud

PUT: Pide al servidor que guarde datos.

DELETE: Pide al servidor que borre datos.

Por consideraciones de seguridad, PUT y DELETE no son soportados por la mayoría de los servidores de producción.

Métodos de extensión (también códigos de error y cabeceras) pueden ser definidos para extender la funcionalidad del protocolo HTTP.

### Negociación de Contenido

Como fue mencionado anteriormente, HTTP soporta la negociación de contenido entre el cliente y el servidor. Un ciente puede usar cabecera adicionales (como Accept, Accept-Language, Accept-Charset, Accept-Encoding) para decir al servidor qué puede manejar o qué contenido prefiere. Si el servidor posee multiples versiones del mismo documento en diferente formato, regresará el formato que el cliente prefiera. Este proceso es llamado _negociación de contenido_.

#### Negociación de Tipo de Contenido

El servidor usa un archivo de configuración MIME (llamado "conf\mime.types") para mapear la _extensión de archivo_ a un _tipo de media_, para así determinar el tipo de media del archivo mirando su extensión de archivo. Por ejemplo, extensiones de archivo ".htm", ".html" son asociadas con tipo de media MIME "text/html", extensiones de archivo ".jpg", ".jpeg" son asociadas con "image/jpg". Cuando un archivo es regresado al cliente, el servidor tiene que desplegar una cabecera de respuesta "Content-Type" para informar al cliente el tipo de media de los datos.

Para la negocición del tipo de contenido, supongamos que el cliente solicita un archivo llamdao "logo" sin especificar su tipo, y envía la cabecera "Accept: image/gif, image/jpeg,...". Si el servidor tiene 2 formatos de "logo": "logo.gif" y "logo.jpg", y la configuración MIME tiene las siguientes entradas:
```
image/gif 		gif
image/jpeg 		jpeg  jpg  jpe
```

El servidor regresará "logo.gif" al cliente, basado en la cabecera _Accept_ del cliente, y el mapeo MIME type/file. El servidor incluirá una cabecera "Content-type: image/gif" en su respuesta.

El rastro de mensaje es mostrado:
```
GET /logo HTTP/1.1
Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg,
  application/x-shockwave-flash, application/vnd.ms-excel, 
  application/vnd.ms-powerpoint, application/msword, */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```

```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:42:22 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.gif
Vary: negotiate,accept
TCN: choice
Last-Modified: Wed, 21 Feb 1996 19:45:52 GMT
ETag: "0-916-312b7670;404142de"
Accept-Ranges: bytes
Content-Length: 2326
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: image/gif
(blank line)
(body omitted)
```

Sin embargo, si el servidor tiene 3 archivos "logo.*", "logo.gif", "logo.html", "logo.jpg", y "Accept: */*" fue usado:
```
GET /logo HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```

```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:48:16 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.html
Vary: negotiate,accept
TCN: choice
Last-Modified: Fri, 20 Feb 2004 04:31:17 GMT
ETag: "0-10-40358d95;404144c1"
Accept-Ranges: bytes
Content-Length: 16
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
(blank line)
(body omitted)
```

`Accept: */*`

Las siguientes directivas de configuración Apache son relevantes para la negociación de tipo de contenido:
* La directiva _TypeConfig_ puede ser usada para especificar la localización del archivo de mapeo MIME:
`TypeConfig conf/mime.types`
* La directiva _AddType_ puede ser usada para incluir mapeo de tipo de MIME adicional en la línea de configuración:
`AddType mime-type extension1 [extension2]`
* La directiva _DefaultType_ da al tipo de MIME de una extensión de archivo desconocida (en la cabecera de respuesta _Content-Type_)
`DefaultType text/plain`

#### Negociación de Lenguaje y "Options MultiView"

La directiva "Options MultiView" es una manera más simple de implementar negociación de lenguaje. Por ejemplo:

```
AddLanguage en .en
<Directory "C:/_javabin/Apache1.3.29/htdocs">
    Options Indexes MultiViews
</Directory>
```

Supongamos que el cliente solicita "index.html" y envía "Accept-Language: en-us". Si el servidor tiene "test.html", "test.html.en", y "test.html.cn", basado en las preferencias del cliente, "test.html" será regresado. ("en" incluye "en-us").

Un rastro de mensaje es como sigue:
```
GET /index.html HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```

```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 02:08:29 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: index.html.en
Vary: negotiate
TCN: choice
Last-Modified: Sun, 29 Feb 2004 02:07:45 GMT
ETag: "0-13-40414971;40414964"
Accept-Ranges: bytes
Content-Length: 19
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
Content-Language: en
(blank line)
(body omitted)
```

La directiva _AddLanguage_ se necesita para asociar un código de lenguaje con una extensión de archivo, similar al mapeo de tipo/archivo MIME.

Nótese que la directiva "Options All" no incluye la opción "MultiViews". Eso es, se tiene que explicitamente activar la opción MultiViews.

La directiva _LanguagePriority_ puede ser usada para especificar la preferencia de lenguaje en case de un empate durante la negociación de contenido o si el cliente no expresa una preferencia. Por ejemplo:
```
<IfModule mod_negotiation.c>
   LanguagePriority en da nl et fr de el it ja kr no pl pt pt-br
</IfModule>
```

####Negociación de Conjunto de Caracteres

Un cliente puede usar la cabecera de solicitud _Accept-Charset_ para negociar con el servidor por el conjunto de caracteres que prefiere.
> Accept-Charset: charset-1, charset-2, ...

Los conjuntos de caracteres comunmente encontrados incluyen: ISO-8859-1 (Latino-I), ISO-8859-2, ISO-8859-5, BIG5 (Chino Tradicional), GB2312 (Chino Simplificado), UCS2 (Unicode de 2 bytes), UCS4 (Unicode de 4 bytes), UTF8 (Unicode Codificado), etc.

Similarmete, la directiva _AddCharset_ es usado para asuciar la extensión de archivo con el conjunto de caracteres. Por ejemplo:

```
AddCharset ISO-8859-8   .iso8859-8
AddCharset ISO-2022-JP  .jis
AddCharset Big5         .Big5  .big5
AddCharset WINDOWS-1251 .cp-1251
AddCharset CP866        .cp866
AddCharset ISO-8859-5   .iso-ru
AddCharset KOI8-R       .koi8-r
AddCharset UCS-2        .ucs2
AddCharset UCS-4        .ucs4
AddCharset UTF-8        .utf8
```

#### Negociación de Codificación

Un cliente puede usar la cabecera _Accept-Encoding_ para decirle al servidor el tipo de codificación que soporta. Los esquemas comunes de codificación son: "x-gzip (.gz, .tgz)" y "x-compress (.Z)".

> Accept-Encoding: encoding-method-1, encoding-method-2, ...

Similarmente, la directiva _AddEncoding_ es usada para asociar la extensión de archivo con el esquema de codificación. Por ejemplo:

```
AddEncoding x-compress  .Z
AddEncoding x-gzip      .gz .tgz
```

### Conexiones Persistentes (o Keep-Alive)

En HTTP/1.0, el servidor cierra la conexión TCP después de entregar la respuesta de forma predeterminada (Connection: Close). Eso es, cada conexión TCP sirve sólo una solicitud. Esto no es eficiente ya que muchas páginas HTML contienen hiperlinks (via la etiqueta `<a href="url">`) a otros recursos (como lo son imágenes, scripts - ya sean locales o desde un servidor remoto). Si se descarga una página que contiene 5 imágenes inline, el navegador tiene que establecer una conexión TCP 6 veces para el mismo servidor.

El cliente puede negociar con el servidor y pedir que no cierre la conexión después de entregar la respuesta, para que otra solicitud pueda ser enviada a través de la misma conexión. Esto es conocido como una **conexión persistenete** (o conexión keep-alive). Las conexiones persistentes aumenta de gran manera la eficiencia de la red. Para HTTP/1.0, la conexión predeterminada es no persistente. Para pedir un conexión persistente, el cliente debe incluir una cabecera de solicitud "Connection: Keep-alive" en el mensaje de solicitud para negociar con el servidor.

Para HTTP/1.1 la conexión predeterminada es persistente. El cliente no tiene que enviar la cabecera "Connection: Keep-alive". En vez de eso, el cliente podría desear enviar la cabecera "Connection: Close" para pedir al servidor que cierre la conexión después de entregar la respuesta.

Una conexión persistenete es extremadamente útilpara páginas web con pequeñas imágenes inline y otros datos asociados, ya que todos estos pueden ser descargados usando la misma conexión. Los beneficios de una conexión persistente son:
* Ahorro de tiempo y recursos de CPU en abrir y cerrar la conexión TCP en el cliente, proxy, compuertas, el servidor origen.
* Las solicitudes pueden ser "pipelined". Esto es, un cliente puede hacer varias solicitudes sin esperar por cada respuesta, para así usar la misma red de una manera más eficiente.
* Una respuesta más rápida ya que no se necesita tiempo para llevar a cabo la verificación de apertura de conexión TCP.

En un servidor HTTP Apache, varias directivas de configuración están relacionadas con las conexiones persistentes:

La directiva _KeeepAlive_ decide si soportar conexiones persistentes o no. Esto toma un valor de On u Off.
> KeepAlive On|Off

La directiva _MaxKeepAliveRequests_ determina el máximo número de solicitudes que pueden ser enviadas a través de la conexión persistente. Se puede definir en 0 para permitir un número ilimitadode solicitudes. Es recomendado definir un número alto para tener un mejor desempeño y eficiencia de red.
> MaxKeepAliveRequests 200

La directiva _KeepAliveTimeout_ define el receso en segundos para que una conexión persistente espere por la siguiente solicitud.
> KeepAliveTimeput 10

### Rango de Descarga
```
Accept-Ranges: bytes
Transfer-Encoding: chunked
```

### Control de Cache

El cliente puede enviar una cabecera de solicitud "Cache-control: no-cache" para decir al proxy que obtenga un nueva copia del servidor original, aún si hay una copia local guardada. Desafortunadamente, HTTP/1.0 no entiende esta cabecera, pero usa una antigua cabecera de solicitud "Pragma: no-cache". Se podrían incluir ambas cabeceras en la solicitud.
```
Pragma: no-cache
Cache-Control: no-cache
```
#### Referencias y Fuentes
* W3C HTTP specifications at http://www.w3.org/standards/techs/http.
* RFC 2616 "Hypertext Transfer Protocol HTTP/1.1", 1999 @ http://www.ietf.org/rfc/rfc2616.txt.
* RFC 1945 "Hypertext Transfer Protocol HTTP/1.0", 1996 @ http://www.ietf.org/rfc/rfc1945.txt.
* STD 2: "Assigned numbers", 1994.
* STD 5: "Internet Protocol (IP)", 1981.
* STD 6: "User Datagram Protocol (UDP)", 1980.
* STD 7: "Transmission Control Protocol (TCP)", 1983.
* RFC 2396: "Uniform Resource Identifiers (URI): Generic Syntax", 1998.
* RFC 2045: "Multipurpose Internet Mail Extension (MIME) Part 1: Format of Internet Message Bodies", 1996.
* RFC 1867: "Form-based File upload in HTML", 1995, (obsoleted by RFC2854).
* RFC 2854: "The text/html media type", 2000.
* Mutlipart Servlet for file upload @ www.servlets.com
















