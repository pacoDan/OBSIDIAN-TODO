### Pub/Sub

Es un protocolo de transporte de mensajes Cliente/Servidor donde el servidor emite un mensaje basado en ciertos filtros y el cliente recibe los mensajes a los que está suscrito. . Existen 2 tipos de suscripción: **Topic-based** y **Content-based** . Cada vez que un mensaje es publicado será recibido por el resto de dispositivos adheridos a un tópico del protocolo. . Me recuerda mucho al patrón de diseño [Observer](https://es.wikipedia.org/wiki/Observer_(patr%C3%B3n_de_dise%C3%B1o)), sólo con la diferencia de que en Pub/Sub el cliente no conoce al servidor y el servidor no conoce al cliente y esta comunicación la maneja el event bus, mientras que en Observer el cliente y servidor tienen comunicación directa.

### [MQTT (Message Queue Telemetry Transport)](http://www.tst-sistemas.es/mqtt/)

Es un protocolo de transporte de mensajes Cliente/Servidor basado en el patrón Pub/Sub, donde existen publicaciones y subscripciones a los denominados “tópicos”. Cada vez que un mensaje es publicado será recibido por el resto de dispositivos adheridos a un tópico del protocolo.

### [Web sockets](https://developer.mozilla.org/es/docs/Web/API/WebSockets_API)

Es una tecnología avanzada que hace posible abrir una sesión de comunicación interactiva entre el navegador del usuario y un servidor. Con esta API, puede enviar mensajes a un servidor y recibir respuestas controladas por eventos sin tener que consultar al servidor para una respuesta.

Es una tecnología que proporciona un canal de comunicación bidireccional y [full-duplex](https://es.wikipedia.org/wiki/Duplex_(telecomunicaciones)#Full-duplex) sobre un único [socket](https://es.wikipedia.org/wiki/Socket_de_Internet) [TCP](https://es.wikipedia.org/wiki/Protocolo_de_control_de_transmisi%C3%B3n). Está diseñada para ser implementada en [navegadores](https://es.wikipedia.org/wiki/Navegador_web) y [servidores web](https://es.wikipedia.org/wiki/Servidor_web), pero puede utilizarse por cualquier aplicación cliente/servidor.
