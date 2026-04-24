### Arquitectura General y Patrones

- **API / API REST:** Es una interfaz de programación de aplicaciones que permite la comunicación entre productos y servicios sin conocer su implementación interna. La **API REST** se apoya en el protocolo **HTTP** y utiliza generalmente **JSON** como formato de intercambio.
    - **Ventajas:** Desacoplamiento, tecnología agnóstica y facilidad de entendimiento para los desarrolladores.
    - **Desventajas:** Es predominantemente **sincrónica**, lo que puede generar bloqueos si el servidor no responde rápido.
- **Patrón Broker:** Es un patrón arquitectónico donde un intermediario inteligente gestiona la comunicación entre publicadores y suscriptores mediante **topics**.
    - **Ventajas:** Desacoplamiento total entre emisor y receptor, alta **escalabilidad** y persistencia de mensajes si el suscriptor está offline.
    - **Desventajas:** Añade complejidad a la infraestructura y, si el broker cae, se puede perder la comunicación del sistema.
- **Modelo en Capas / MVC:** El **MVC** es un patrón de interacción que separa la lógica. El modelo en capas busca que cada nivel tenga una responsabilidad única.
    - **Ventajas:** Facilita el mantenimiento y la organización del código.
    - **Desventajas:** Puede generar una cadena de llamadas larga que aumente la latencia.
- **Arquitectura Limpia y Hexagonal:** Filosofías de diseño que organizan el código en niveles concéntricos donde las dependencias solo fluyen hacia **adentro** (hacia la lógica de negocio).
    - **Ventajas:** Muy bajo acoplamiento, alta cohesión y permite cambiar tecnologías externas (como la DB) sin afectar el núcleo del negocio.
    - **Desventajas:** Puede introducir una **complejidad artificial** si el problema es pequeño.

### Arquitectura Web

- **Concepto de Sesión:** Permite al servidor recordar interacciones previas del cliente en una arquitectura que de otro modo sería _stateless_.
    - **Ventajas:** Facilita el manejo de estados de usuario.
    - **Desventajas:** Dificulta la **escalabilidad horizontal** (problema de _sticky sessions_).
- **Cliente Pesado vs. Cliente Liviano:** El **cliente pesado** (ej. React) gestiona la UI en el navegador. El **cliente liviano** delega el renderizado al servidor.
    - **Ventajas Cliente Pesado:** Interfaz fluida sin recargar páginas y mejor experiencia de usuario.
    - **Desventajas Cliente Pesado:** Mayor consumo de recursos en el cliente y lógica de seguridad más compleja.
- **Apps Mobile Nativas vs. Híbridas:** Las nativas se desarrollan para un OS específico, mientras que las híbridas pueden usar un motor web.

### Atributos de Calidad

- **Escalabilidad:** La **Vertical** aumenta el hardware de un solo nodo; la **Horizontal** suma más servidores.
    - **Horizontal Ventajas:** Sin límites físicos y alta disponibilidad.
    - **Horizontal Desventajas:** Mayor complejidad técnica y de sincronización.
- **Load Balancer (Balanceador de Cargas):** Distribuye solicitudes entre múltiples instancias.
    - **Ventajas:** Optimiza el rendimiento, evita sobrecargas y mejora la disponibilidad al redirigir si un nodo falla.
- **Disponibilidad y Mantenibilidad:** La disponibilidad busca que el sistema siga operando ante fallos. La mantenibilidad se logra con bajo acoplamiento y evitando lógica duplicada (_DRY_).

### Estilos Arquitectónicos

- **Monolítica vs. No Monolítica (SOA / Microservicios):**
    - **Monolítica:** Todo el código en un único proyecto.
        - **Ventajas:** Fácil de desarrollar inicialmente y de desplegar.
        - **Desventajas:** Difícil de escalar partes específicas y cualquier cambio requiere desplegar todo el sistema.
    - **Microservicios:** Conjunto de servicios pequeños e independientes.
        - **Ventajas:** Escalado independiente, despliegues parciales y tolerancia a fallas.
        - **Desventajas:** Alta complejidad de red, latencia y dificultad para mantener la integridad de datos entre servicios.
- **Componentes de Soporte:** En microservicios son esenciales el **API Gateway** (punto de entrada), el **Service Registry** (inventario de servicios) y el **Circuit Breaker** (corta llamadas a servicios caídos).

### Integración de Sistemas

- **SOAP:** Protocolo basado en **XML** con un contrato estricto (**WSDL**).
    - **Ventajas:** Formalidad y validación automática de contratos. **Desventajas:** Muy pesado, alto acoplamiento y difícil de procesar comparado con REST.
- **GraphQL:** Permite al cliente pedir exactamente los campos que necesita.
    - **Ventajas:** Gran eficiencia de red y evita múltiples llamadas encadenadas.
    - **Desventajas:** Requiere implementar un motor adicional (como Hasura).
- **gRPC:** Usa **Protocol Buffers** (binario) sobre **HTTP/2**.
    - **Ventajas:** Altísimo rendimiento y soporte de streaming bidireccional.
- **Cola de Mensajes:** Comunicación **asincrónica** donde el mensaje se almacena hasta ser procesado.
    - **Ventajas:** Desacopla procesos pesados y garantiza que no se pierdan datos si el receptor está caído.
- **Base de Datos Compartida:** Múltiples sistemas leen y escriben en la misma DB.
    - **Ventajas:** Simple de implementar inicialmente.
    - **Desventajas:** Alto acoplamiento a nivel de esquema y cuellos de botella en performance.

### Infraestructura

- **CDN:** Red de servidores distribuidos para entregar contenido estático rápido según la ubicación del usuario.
- **Caché:** Almacena datos frecuentes para reducir tiempos de acceso.
    - **Ventajas:** Mejora performance y reduce carga en la base de datos.
- **SSO (Single Sign-On):** Permite al usuario autenticarse una vez para acceder a múltiples aplicaciones (ej. Auth0).

### Documentación de la Arquitectura

- **Modelo 4+1:** Describe el sistema desde las vistas: Lógica (clases), Procesos (flujos), Despliegue (componentes), Física (nodos) y Escenarios (+1, casos de uso).
- **Modelo C4:** Niveles de detalle: Contexto (relaciones externas), Contenedores (aplicaciones/DBs), Componentes (módulos internos) y Código (clases).
- **Nodo vs. Componente:** Un **Nodo** es un contenedor físico o virtual (ej. un servidor o contenedor Docker); un **Componente** es la pieza de software que ejecuta código (ej. un JAR o una Web App).
- **Protocolos:** **HTTP/HTTPS** para web, **AMQP** para colas de mensajes y **MQTT** para brokers ligeros de IoT.
- **Interfaz:** El componente que ofrece el servicio (servidor) expone la **Interfaz**, mientras que el cliente la consume para iniciar la comunicación.