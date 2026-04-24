según este contexto, cual seria los ejercicios si inferimos segun  documentos anteriores a resolver según Dominio, Persistencia y Arquitectura, según textos anteriores: 
Contexto

Una organización social destinada a impulsar la lectura en la población ha decidido iniciar un proyecto de circulación de libros. En este marco, se propone el diseño y desarrollo de un sistema para facilitar el proceso de préstamos de libros, devoluciones y cesiones.

Se promueve el préstamo de libros a otras personas, incluso sin necesidad de volver a su dueño original y sin que ese dueño original pierda la propiedad. Esto significa que si una persona A presta un libro a B, B lo puede prestar a C, C a D, sin embargo, la propiedad continúa siendo de A hasta que él decida otorgársela a otro. En realidad, el objeto de operaciones es un ejemplar de una edición de una obra.

Las operaciones permitidas son el préstamo, devolución, la cesión de la propiedad y la baja del ejemplar.


---


**Patrones de Diseño:** Justifique el uso de patrones.

- _Sugerencia:_ ¿Cómo usaría el patrón **State** para manejar los estados del `Ejemplar` (Disponible, Prestado, Cedido, Dado de Baja)?
    
- _Sugerencia:_ ¿Cómo aplicaría el patrón **Observer** para notificar al dueño original cada vez que su ejemplar es prestado a una nueva persona en la cadena?

- **Estados sugeridos:** `Disponible`, `Prestado`, `EnProcesoDeCesion`, `Baja`.

**Diagrama de Secuencia o Pseudocódigo:** Explicar el flujo de una operación compleja, como la **cesión de propiedad** mientras el libro está en poder de un tercero, o el proceso de **préstamo en cadena** (A -> B -> C)



### 2. Persistencia / Datos (25 - 30 puntos)

Este punto se enfoca en cómo guardar la información de forma permanente.

- **A. Modelo de Datos Relacional (DER):** Diseñar un diagrama físico de base de datos. Debe incluir:
    
    - Tablas, campos y tipos de datos.
        
    - Claves Primarias (PK) y Foráneas (FK).
        
    - Cardinalidad (1:1, 1:n, n:n) y modalidad.
        
- **B. Justificación de Decisiones:**
    
    - Identificar qué elementos deben persistirse (ej. historial de préstamos) y cuáles no.
        
    - **Impedance Mismatch:** Explicar cómo mapeas la herencia o las relaciones complejas del objeto a la tabla.

	- **Impedance Mismatch:** Explicar cómo se resolvieron las diferencias entre objetos y tablas, especialmente en la jerarquía `Obra` -> `Edicion` -> `Ejemplar` (ej. usando estrategias de herencia como _Table per Class_).
        
    - **Desnormalización:** Justificar si decides duplicar datos por performance (ej. guardar el nombre del dueño actual directamente en el ejemplar para evitar JOINS).
    - **Desnormalización:** Evaluar si es necesario desnormalizar algún dato (como el `nombre de la obra` dentro de la tabla `Ejemplar`) para mejorar la performance de las búsquedas.

- `tenedor_actual_id` en EJEMPLAR es una **desnormalización controlada** para evitar recorrer toda la cadena de préstamos para saber quién tiene el libro actualmente

**🔷 Qué persistir:**

- Todo se persiste ya que el sistema requiere **trazabilidad completa** de operaciones
- El historial de préstamos, cesiones y bajas es crítico para auditoría

**🔷 Impedance Mismatches resueltos:**

|Problema OO|Solución Relacional|
|---|---|
|Herencia de Operacion|Single Table Inheritance** con campo `tipo` + tablas hijas por operación|
|Cadena de préstamos (lista enlazada)|Campo autorreferencial `prestamo_padre_id`|
|Propiedad vs Tenencia|Dos FK en EJEMPLAR: `propietario_id` y `tenedor_actual_id`|


**Justificación de Persistencia:**

- **Impedance Mismatch:** Explique cómo resolvió la diferencia entre su modelo de objetos (jerarquía Obra-Edicion-Ejemplar) y las tablas relacionales.
    
- **Desnormalización:** ¿Consideraría desnormalizar el campo `Poseedor_Actual` en la tabla `Ejemplar` para evitar consultar siempre la tabla de préstamos? Justifique por performance.

**Lógica de Propiedad vs. Posesión:** El diagrama debe reflejar que un `Ejemplar` tiene un `Dueño` (quien posee la propiedad legal) y un `Poseedor Actual` (quien tiene el libro físicamente tras una cadena de préstamos) [Contexto].


### **B. Atributos de Calidad Sugeridos**

**🔷 Trazabilidad / Auditabilidad**

- Toda operación queda registrada con fecha, usuario y ejemplar
- Se puede reconstruir la cadena completa de préstamos
- **Decisión:** Nunca se eliminan registros, solo se marca `activo = false`

**🔷 Disponibilidad**

- Sistema crítico para la organización social
- Se recomienda base de datos con réplica de lectura
- Caché para consultas frecuentes (estado actual del ejemplar)




### 3. Arquitectura (40 puntos)

Este punto define la infraestructura y comunicación del sistema.

- **A. Diagrama de Despliegue y Componentes:** Dibujar la arquitectura física (Servidores, Clientes, Base de Datos, APIs externas).
    
- **B. Atributos de Calidad:** Identificar y resolver desafíos específicos. Por ejemplo:
    
    - **Disponibilidad/Escalabilidad:** ¿Cómo manejarías un pico de tráfico si la organización lanza una campaña masiva de lectura?
        
    - **Integridad de Datos:** ¿Cómo aseguras que un libro no sea "prestado" por dos personas al mismo tiempo?
        
- **C. Estrategia de Integración:** Si el sistema necesitara validar datos de libros con una API externa (como Google Books), explicar si la comunicación sería sincrónica o asincrónica y dar un ejemplo del mensaje (ej. un JSON con el ISBN).


Este punto evalúa la infraestructura, los atributos de calidad y la integración.

1. **Diagrama de Arquitectura (Despliegue + Componentes):** Realice un diagrama UML que muestre la solución. Considere que el sistema tendrá una App Mobile para que los usuarios escaneen un código QR en el ejemplar para realizar préstamos rápidos.
    
    - Incluya: Balanceador de Carga, Servidores de Aplicaciones, Base de Datos y un Servicio de Notificaciones.
        
2. **Atributos de Calidad y Escenarios:** * **Disponibilidad:** Si la organización lanza una campaña nacional y el tráfico aumenta súbitamente, ¿cómo asegura que el sistema no se caiga? Explique el uso de **Escalabilidad Horizontal** y un **Load Balancer**.
    
    - **Integración:** El sistema debe integrarse con una API externa (ej. Google Books) para obtener los datos de la `Obra` automáticamente mediante el ISBN. ¿Esta comunicación debe ser sincrónica o asincrónica? Justifique y dé un ejemplo del mensaje JSON.
        
3. **Seguridad y Sesión:** Dado que es un sistema con usuarios registrados, ¿qué componente propone para el Inicio de Sesión (SSO)? Si usa múltiples servidores, ¿cómo manejaría la sesión para que el usuario no tenga que re-loguearse si el balanceador lo envía a otro nodo (Sticky Sessions vs. Redis)?


**Stateless vs Stateful:** Se podría preguntar si el servicio de préstamos es _stateless_ y cómo esto facilita la escalabilidad.

**SOLID:** Asegúrese de que la clase `Ejemplar` no tenga demasiadas responsabilidades (Single Responsibility Principle), delegando la lógica de préstamos a un servicio o gestor.

**Estrategia de Integración:** Dado que el sistema maneja "ejemplares de ediciones de una obra", se podría plantear la integración con una **API externa de catálogos** (como Google Books). El ejercicio pediría definir si la integración es sincrónica o asincrónica, y cómo minimizar costos si la API cobra por solicitud (ej. implementando un **Cache**)

**Manejo de picos de tráfico:** Proponer cómo resolver un alto tráfico cuando muchos usuarios consultan la disponibilidad de libros simultáneamente (ej. escalamiento horizontal y balanceo de carga)

Integración con Catálogos Externos y Resiliencia

• **El Requerimiento:** Para evitar que los usuarios carguen manualmente todos los datos de un libro, el sistema debería integrarse con **APIs externas** (como Google Books o registros nacionales) mediante el **Patrón Adapter**.

• **El Problema:** Las APIs externas pueden ser costosas o fallar (timeouts). Basándose en las fuentes, se debe implementar una **Cache** para minimizar solicitudes pagas y un **Circuit Breaker** (como Resilience4j) para que el sistema no se caiga si el servicio externo no responde.



Arquitectura Escalable y Desacoplada

• **El Requerimiento:** El sistema debe manejar picos de tráfico (por ejemplo, durante campañas de fomento a la lectura) y permitir búsquedas rápidas de libros disponibles.

• **El Problema:** Un sistema monolítico podría saturarse. La recomendación es usar una **API Gateway** como punto de entrada único y un **Service Registry (Eureka)** para localizar dinámicamente los servicios de préstamos y catálogos. Para procesos pesados, como la carga masiva de catálogos desde archivos CSV, se debe usar **procesamiento asincrónico** con una cola de mensajes para no bloquear al usuario



---

temas completos que pueden entrar:
# ***Temas de Repaso***

##     **Arquitectura:** 

* Repasar los contenidos vistos en clase para el Primer Parcial (concepto de API/API REST, Integración entre Sistemas, Patrón Broker, MVC, modelo en capas, entre otros)  
* Nociones de Arquitectura Limpia y Arquitectura Hexagonal  
* **Arquitectura Web:**   
  * Concepto de Sesión, Recursos Web  
  * Arquitectura Cliente Pesado versus Cliente Liviano  
  * Aplicaciones mobile nativas e híbridas  
* **Atributos de Calidad enfocados en la Arquitectura:**   
  * Concepto de **escalabilidad Horizontal y Vertical**  
    * Load Balancer  
  * Disponibilidad  
  * Mantenibilidad  
  * Enfoque en trade-offs.   
* **Estilos Arquitectónicos:**  
  * Arquitectura Monolítica versus Arquitecturas No Monolíticas: SOA \- Microservicios  
    * Componentes arquitectónicos involucrados producto de la implementación de una Arquitectura No Monolítica.  
* **Integración de Sistemas:**   
  * Web Services: API REST, GraphQL, gRPC, SOAP  
  * Cola de mensajes  
  * Base de Datos Compartida  
* **Infraestructura**  
* **Componentes Arquitectónicos**  
  * CDN   
  * Caché  
  * SSO  
* **Documentación de una Arquitectura**  
  * Modelo 4+1  
  * Modelo C4  
  * Diagrama de despliegue  
    * Reconocer e identificar un nodo versus un componente de software. Reconocer a un Nodo como un contenedor de un componente y determinar en qué nodos están ubicados los componentes de la Arquitectura.  
    * Protocolos involucrados (HTTP, HTTPS, TCP/IP, AMQP, MQTT) en la conexión entre componentes.  
    * Identificar qué componente expone una Interfaz en una conexión. 

## **Seguridad:** 

* ## Tríada de la Seguridad

* ## Mecanismos de Seguridad

* ## Autenticación vs. Autorización

* ## OWASP

* ## Componentes Arquitectónicos

## **Persistencia y Modelo de Datos:** 

* Concepto de Persistencia, tipos de persistencia.   
* Modelo Relacional.   
* Modelo de Datos.   
* Persistencia en Java utilizando las anotaciones del ORM Hibernate.  
* Desnormalización por consistencia de datos y por performance. 

# ***Bonus \- Posible Estrategia de Abordaje para decisiones a realizar sobre Arquitectura***

1. Plantear o Comprender el Escenario de Aplicación   
2. Plantear el Problema a Resolver.  
3. Enumerar el Atributo de Calidad que está en juego, y definirlo, de esa manera entendemos que nos referimos a lo mismo.  
4. Justificar con aspectos técnicos la solución/abordaje propuesto. 

   ## **Ejemplo para aplicar:**

*Suponiendo y considerando que el Sistema cuenta con una arquitectura web Stateful, con varios servidores atendiendo solicitudes de forma simultánea, ¿cómo resolvería el siguiente problema reportado por los usuarios?*  
*“Varios usuarios han reportado que, mientras utilizan la plataforma (previamente logueados), el Sistema los vuelve a llevar a la pantalla de Inicio de Sesión, teniendo que volver a ingresar sus credenciales para continuar con su labor.”*

1. **Escenario de Aplicación:** Se cuenta con una arquitectura de varios servidores que guardan (de alguna manera) la sesión del usuario. Delante de estos Servidores tengo un Balanceador de Carga.   
2. **Problema a Resolver:** Que el Usuario no tenga que loguearse nuevamente o que no se pierda su sesión.  
3. **Atributo de calidad en juego:** En este caso podemos analizarlo desde la Disponibilidad o Usabilidad (si consideramos que el sistema sigue funcionando pero se pierde calidad en la experiencia del usuario)  
   * **Disponibilidad**: Se trata de la capacidad de un sistema, a ser accesible y utilizable por los usuarios/procesos cuando ellos lo requieran.  
4. Para resolver esta situación se pueden proponer diferentes abordajes:  
   * **Balanceador con Sticky-Session:** El balanceador de carga enviará al Usuario siempre al mismo Servidor que lo envió por primera vez. En caso de que el Servidor no se encuentre disponible, seguirá perdiendo la sesión.  
   * **Espacio de Almacenamiento de Sesión Compartida**: Sumar un Componente a la Arquitectura que guarde las sesiones y sea compartido por todas las instancias de Servidor. Por ejemplo una Base de Datos Clave-Valor como Redis.

 ## **Temas de repaso**

* Diagrama de Clases \- Relaciones entre clases  
  * Clases sin métodos  
  * Herencia vs composición  
  * ¿Herencias sin comportamiento?  
* Patrones vistos en clase:  
  * State  
  * Template Method  
  * Strategy  
  * Adapter  
  * Observer  
  * Command  
  * Factories, Singleton & Builder  
* Atributos de Calidad (ISO 25000\) y Cualidades de diseño   
* Principios SOLID \- Code Smells  
* Componentes Stateless y Stateful  
* Inyección de dependencias  
* Arquitectura  
  * Modelo en capas y niveles de arquitectura   
  * MVC  
  * Cliente- servidor  
  * Protocolo HTTP  
  * Integración de Sistemas: Interfaces entrantes y salientes  
    * Publish \- Subscribe  
    * Patron Broker  
    * Mecanismos pull y push- based  
    * Web Hook \- dirección de callback  
  * Ejecuciones asincrónicas mediante Cron task (jobs)  
  * Repositorios y servicios  
* Modelado de roles, usuarios y permisos.

  ## **Tips a tener en cuenta**

* Tipos de datos de los atributos (int, float, double)  
* Consistencia de datos (clase, string, enum)  
* Métodos vacíos (sin parámetros y que no devuelven nada)  
* Considerar si conviene resolver todo en una clase, hacer una herencia o usar composición  
* Tipos de datos de los atributos y retorno de las funciones.  
* Preguntas que deberían hacerse mientras diseñan (arquitectura):  
  * Alcance del sistema  
  * Configuración de entorno de objetos (¿Cómo se instancian?)  
  * Deploy (instalación del sistema)  
  * Uso  
* Análisis que se puede realizar:   
  * ¿Cómo es el procesamiento de un requerimiento? ¿Es preferible pensar que se ejecuta de forma asincrónica o sincrónica?  
  * ¿Cómo se podría implementar este requerimiento?  
  * ¿En qué capa se resolvería utilizando el patrón MVC?

  