# Arquitectura de node.js. Libuv y el bucle de eventos en Node.js.

Como se ha comentado anteriormente, para manejar la concurrencia Node.js utiliza una arquitectura dirigida por eventos, antes de adentrarnos en cómo se implementa este modelo en Node.js, es necesario conocer la estructura interna de Node.js, el papel que juega cada uno de sus componentes y cómo interactúan entre ellos.

# Componentes de Node.js.

En el siguiente gráfico se representan las diferentes piezas de tecnología utilizadas en Node.js del nivel más alto al nivel más bajo. Se puede dividir en tres capas principales: la capa inferior en el directorio “node\deps” donde se encuentran las dependencias de Node.js, una capa superior en el directorio “node\lib” donde se encuentra el código de la aplicación es decir los diferentes módulos disponibles en la API Node.js. Entre las dos capas existe un código de unión o puente, en el directorio “node\src” que sirve de enlace entre la capa superior y la capa inferior.
![[Pasted image 20250106173909.png]]

**API node.js**: En la parte superior, se encuentra los módulos nativos que componen el núcleo de la API de Node.js, escritos en JavaScript, esos módulos están directamente expuestos al desarrollador para que sean llamados desde el código de la aplicación Node.js. La ubicación de estos archivos JavaScript es el directorio **_node/lib._** El usuario puede acceder a ellos a través de “require()”.

**Bindings y Addons:** La capa intermedia es el código que sirve de pegamento entre API de node escrita en JavaScript, (capa superior) y la capa inferior que son librerías escritas en C/C++ que otorgan las diferentes funcionalidades, estas librerías pueden ser nativas de Node.js u otras externas que nos interese utilizar, en función del origen de estas librerías, (naturales de Node o externas), en la capa intermedia podemos hablar de **_“Bindings”_** o de **_“Addons”_**. Tanto “bindings” como “addons” es código C++ envuelto en la API de v8, (han de estar ligados a la librería V8, (#include <v8.h>)) y por regla general además hacen uso de la librería “libuv”.

- **Bindings**: también denominados módulos incorporados C++, son los archivos de código que sirven de puente o enlace entre la API del núcleo de Node.js, escrito en JavaScript, con las librerías internas centrales de Node.js, escritas en C/C++ (C-Ares, zlib, OpenSSL, http-parser etc..) estas librerías son dependencias de Node, las cuales están enlazadas estáticamente, podemos encontrar estas librerías en el directorio **_node/deps_**, los archivos “bindings” son el pegamento entre los diferentes lenguajes de programación, estos archivos los podemos encontrar dentro del directorio **_node/src_**, un ejemplo sería el archivo **_node_http_parser.cc_**
    
- **Add-ons**: De la misma manera, si ya existe una librería, escrita en C/C++, que provee de una determinada funcionalidad, y nos interesa usarla en Node.js, podemos realizarlo mediante la creación de un complemento. Los “Addons”, complementos, están escritos en C o en C++, son objetos compartidos que vinculamos dinámicamente, cargándolos en Node.js utilizando la función require(), de tal manera que podemos utilizarlos como un módulo ordinario de Node.js.
    

> Podemos observar los módulos o “bindings”, (API o Binding), que se han cargado en la plataforma en un momento determinado, usando el “array” “**_process.moduleLoadList_**_”_. En esta lista se puede identificar cada uno por la etiqueta que precede al nombre:

- **_NativeModule_** (API core)
    
- **_Binding_**.
    

Si por ejemplo, importamos el modulo http a través de un “require(‘http’)”, podemos observar cómo se ha cargado la cadena de dependencias de los diferentes módulos nativos y su binding.


![[Pasted image 20250106173933.png]]

**Dependencias de Node.js:** En el nivel más bajo podemos encontrar las librerías nativas escritas en C/C ++ que son el corazón de node.js y las que proporcionan las diferentes funcionalidades, principalmente la máquina virtual de JavaScript, el **motor V8**, que permite **ejecutar el código JavaScript** a una gran **velocidad** y la librería **libuv** que es la que proporciona las características más notorias de la plataforma Node.js, el **bucle de eventos y la E/S asíncrona sin bloqueos**. A continuación se exponen las principales dependencias:

- **V8**: Es el motor de JavaScript que usa Google Chrome. Está escrito en C++ y puede ejecutarse de forma independiente o integrado en cualquier aplicación C++. V8 fue diseñado para aumentar el rendimiento de la ejecución de JavaScript en el interior de los navegadores web. Con el fin de obtener la velocidad, V8 compila JavaScript en código de máquina nativo, mediante la implementación de un compilador JIT (Just-In-Time) en lugar de interpretarlo o ejecutarlo como bytecode, básicamente es una combinación de un intérprete con un compilador que realiza optimizaciones, a medida que se interpreta y se ejecuta el código, éste es observado por un monitor o generador de perfiles, en base a esa monitorización del código se decide enviarlo al compilador que realiza optimizaciones y almacena la compilación para usarla más adelante.
    
- **c-ares**: Es una librería de C para la petición asíncrona de DNS. Está destinado a aplicaciones que necesitan realizar consultas DNS sin bloquear, o la necesidad de realizar múltiples consultas DNS en paralelo.
    
- **http_parser**: Una librería escrita en C que se usa para el análisis de mensajes HTTP, pudiendo analizar tanto las peticiones como las respuestas. Está diseñada para no hacer ninguna llamada al sistema o asignaciones, por lo que tiene una huella muy pequeña de memoria por solicitud. El analizador sintáctico extrae información de los mensajes HTTP como: campos y valores de las cabeceras, Content-Length, el método usado en la petición, código de estado de la respuesta, Transfer-Encoding, versión HTTP, URL de la solicitud y el cuerpo del mensaje.
    
- **OpenSSL**: Es una implementación de código abierto de Secure Sockets Layer (SSL v2/v3) y Transport Layer Security (TLS), así como una biblioteca criptográfica de propósito general. Esta librería se usa extensamente en los módulos “tls” y “crypto” de la API de Node.
    
- **Zlib**: Es una librería de compresión y descompresión de datos de propósito general escrita en C, es compatible con la lectura y escritura de archivos en “gzip” que es el formato que se emplea, entre otros usos, para comprimir las páginas web en el servidor antes de servirlas a los navegadores, con el objetivo de que ocupen mucho menos espacio y por tanto se transfieran por la red de una manera más rápida.
    
- **ICU**: Conjunto de librerías C++ que proporciona soporte Unicode y la capacidad de internacionalización. Se utiliza principalmente para resolver los problemas de codificación multiplataforma. (formatos de números, fechas y horas, conversión de página de códigos a Unicode y viceversa, comparación de cadenas, expresiones regulares etc.)
    
- **Libuv**: Es una librería escrita C++ que permite a Node.js relacionarse con el entorno. Independientemente de la plataforma permite abstraer las funcionalidades de E/S tanto de red como del sistema de archivo, además de aportar otros servicios, como los temporizadores. Libuv se encarga de recopilar los eventos que provienen del sistema operativo o de otras fuentes de eventos y de proporcionar un bucle de eventos, en definitiva es la pieza fundamental que permite implementar un modelo orientado a eventos.