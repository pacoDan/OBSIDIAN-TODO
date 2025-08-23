Juan Zaffaroni

20:00

[https://drive.google.com/drive/folders/0B27PgUCCYOICUmVsa2dzdElpeTA?resourcekey=0-yJtxU6GI8hXc_KEXKd7VLg&usp=drive_link](https://drive.google.com/drive/folders/0B27PgUCCYOICUmVsa2dzdElpeTA?resourcekey=0-yJtxU6GI8hXc_KEXKd7VLg&usp=drive_link&authuser=1)

[https://drive.google.com/drive/folders/1_U-1jBUtxLyLmMSYLGEMTwBId2EwHS7m?usp=drive_link](https://drive.google.com/drive/folders/1_U-1jBUtxLyLmMSYLGEMTwBId2EwHS7m?usp=drive_link&authuser=1)

[https://drive.google.com/drive/folders/1BXEp4HCdpRnikNmj4N_6sHGhSf9jnwgx?usp=drive_link](https://drive.google.com/drive/folders/1BXEp4HCdpRnikNmj4N_6sHGhSf9jnwgx?usp=drive_link&authuser=1)

[https://redis.io/docs/latest/commands/](https://redis.io/docs/latest/commands/)

---
## Estructura de la Transcripción: NOSQL Clase 2

### **1. Introducción y Contexto de Modelado de Datos**

- **Modelado de Datos:**
    
    - **Aspecto Físico:** Estructura y forma de almacenamiento.
    - **Aspecto Lógico:** Cómo se modelan las estructuras lógicas de datos.
    
- **Historia de Bases de Datos:**
    
    - Lo más común es el modelado relacional.
    - Las bases de datos relacionales tienen un área de memoria compartida, estructuras de disco y procesos.
    
- **Interacción con el Motor de Base de Datos:** Se envían sentencias y el motor devuelve datos o un estatus (OK, Not Found, etc.).

### **2. Modelo Relacional**

- **Origen:** Creado y formulado por Edgar Codd en los años 70.
- **Concepto de Relación (según Codd):**
    
    - Estructura bidimensional.
    - **Cabecera:** Atributos relacionados con sus dominios (ej. año, fecha de nacimiento con lógica de validación).
    - **Cuerpo:** Conjunto de tuplas (filas) con pares atributo-valor (ej. número de legajo, nombre de alumno).
    
- **Reglas de Codd:** Características que debe cumplir una base de datos para ser considerada relacional.
- **Claves en el Modelo Relacional:**
    
    - **Claves Primarias:** Atributos o conjunto de atributos que definen unívocamente un elemento de una relación/tabla.
    - **Claves Foráneas:** Atributos que referencian la clave primaria de otra tabla.
    
- **Reglas de Integridad:**
    
    - **Integridad de la Entidad:** La clave primaria no puede ser nula.
    - **Integridad Referencial:** Si una clave foránea no es nula, su valor debe existir en la clave primaria referenciada.
    - **Integridad Semántica:** Constraints adicionales (NOT NULL, CHECK, DEFAULT, tipo de dato).
    
- **Modelado Relacional Tradicional:**
    
    - Mucha experiencia y notaciones (Chen, Martin, DDFX, etc.).
    - **Costo Espacial:** Más bajo (menos repetición de datos).
    - **Costo Computacional:** Más alto (más joins, que son operaciones costosas).
    

### **3. Modelado NoSQL**

- **Diferencias con el Modelado Relacional:**
    
    - No hay estándares definidos para el modelado NoSQL.
    - Pocas herramientas estandarizadas para DERs en NoSQL.
    - Metodologías específicas para bases de datos puntuales (ej. Cassandra).
    - No hay un modelado de datos estándar en el mercado NoSQL debido a la disimilitud de arquitecturas.
    
- **Principios Básicos del Modelado NoSQL:**
    
    - **Desnormalización:**
        
        - Replicación de datos en múltiples registros/documentos.
        - **Objetivo:** Simplificar y optimizar el procesamiento de consultas.
        - **Ejemplo:** Agregar campos del cliente a la tabla de órdenes de compra para evitar joins.
        - **Relaciones Uno a Muchos:** Se resuelven dentro de un agregado (ej. array de renglones de una orden de compra).
        - **Costo Espacial:** Más alto (más datos repetidos).
        - **Costo Computacional:** Más bajo (consultas más rápidas en una sola estructura).
        
    - **Agregados:**
        
        - Unidad de registro compleja que puede contener subregistros, estructuras anidadas, arrays, listas.
        - **Formato:** XML, JSON.
        - **Origen:** Domain Driven Design (colección de objetos relacionados tratados como una unidad).
        - **Unidad Mínima:** De manipulación y administración de consistencia.
        - **Atomicidad:** El agregado es atómico (se graba/modifica completo o no se graba/modifica).
        - **Replicación y Distribución:** Se replican y distribuyen agregados completos.
        - **Minimiza Relaciones Uno a Muchos:** Se resuelven dentro del agregado (ej. orden de compra con array de detalles).
        - **Incorpora Reglas de Negocio:** Colecciones de datos de otras tablas se incluyen en el agregado (ej. datos principales del cliente en la orden de compra).
        - **Ejemplo de Agregado:** Un documento JSON con clave-valor, subdocumentos, arrays de subdocumentos.
        - **Ejemplo de Modelado:** Producto con atributos comunes y atributos específicos por tipo (libro, álbum, jean) dentro de un mismo agregado.
        - **Transacciones en NoSQL:** Muchas bases de datos NoSQL actuales tienen transacciones, pero el agregado sigue siendo atómico.
        
    
- **Joins en NoSQL:**
    
    - En general, se trata de no hacer joins.
    - Muchas bases de datos NoSQL no soportan joins (o los soportan de forma limitada).
    - **Resolución de Joins:** A menudo se resuelven desde la aplicación (ej. buscar un dato, luego usarlo para buscar otro en otra colección).
    - **Casos Inevitables:** Relaciones muchos a muchos, o relaciones uno a muchos con gran volumen de datos (ej. historial de emails).
    - **Ejemplo de Mensajes:** No guardar millones de emails en un array dentro del agregado de usuario (demasiado grande para replicación/distribución). Mejor tener los últimos X mensajes en el agregado y el resto en otra colección referenciada.
    

### **4. Tipos de Bases de Datos NoSQL (y sus características)**

- **Key-Value (Kivalue):**
    
    - **Concepto:** Clave-valor. A partir de una clave, se consulta su valor. No se puede consultar a través del valor.
    - **Estructura:** Muy genérica, el valor puede ser cualquier cosa (foto, video, JSON).
    - **Flexibilidad:** Alta, pero la aplicación debe saber qué se guardó.
    - **Integridad del Dato:** No asegurada (el valor es opaco para la base de datos). No hay constraints.
    - **Uso Principal:** Caché (sesiones, queries), alta velocidad de acceso.
    - **Ejemplo:** Redis.
    
- **Column Family:**
    
    - **Concepto:** Capa superior a Key-Value. Incluye Key-Value.
    - **Estructura:** Familias de columnas, donde el nombre del atributo puede ser variable.
    - **Unidad Básica de Almacenamiento:** Columna (o fila completa con columnas).
    - **Acceso:** Dos niveles de acceso (row key/partition key y clave a nivel columna).
    - **Flexibilidad:** Para crear columnas en diferentes filas (no todas las filas tienen las mismas columnas).
    - **Integridad:** Relativa (no hay joins, no hay shins).
    - **Ejemplo:** Cassandra.
    
- **Document Based:**
    
    - **Concepto:** Basadas en documentos (ej. JSON, XML).
    - **Modelado:** Mucho más rico.
    - **Estructura:** Documentos JSON con pares clave-valor, arrays de pares, subdocumentos, arrays de subdocumentos.
    - **Flexibilidad:** Muy amplia.
    - **Esquema:** Schemaless (no tienen un esquema predefinido rígido). Los documentos pueden diferir en formato.
    - **Atributos:** Pueden ser nulos o vacíos. Se pueden crear nuevos atributos sin definición previa.
    - **Ejemplo:** MongoDB.
    
- **Graph Databases:**
    
    - **Concepto:** Modelado muy diferente. Se trabaja con nodos y relaciones.
    - **Estructura:** Nodos y relaciones, ambos con atributos.
    - **Modelado:** Requiere considerar muchas cosas nuevas (definir si algo es un nodo, una relación o ambos).
    - **Ejemplo:** Neo4j.
    

### **5. Redis: Implementación de Key-Value**

- **Definición:** Base de datos Key-Value en memoria.
- **Características Generales:**
    
    - Open source (con versión Enterprise).
    - Escrita en C (para performance).
    - Dataset en memoria (lectura muy rápida).
    - El "value" no es tan opaco: almacena distintas estructuras de datos.
    
- **Casos de Uso Típicos:**
    
    - **Caché:** Mejorar tiempos de respuesta de sistemas lentos (ej. datos de sesión, perfiles de usuario, carritos de compra).
    - **Contadores:** Incrementos/decrementos atómicos.
    - **Colas/Pilas:** Listas para comunicación entre procesos (productor-consumidor).
    - **Ranking/Leaderboards:** Conjuntos ordenados.
    - **Geoespacial:** Consultas de proximidad.
    - **Analíticas en Tiempo Real:** Conteo de ocurrencias únicas (Hyperloglog).
    - **IoT:** Streams para datos de sensores.
    
- **Qué se puede hacer en Redis:**
    
    - **Operaciones Básicas (Strings):** `SET`, `GET`, `DEL`.
    - **Modificadores de SET:** `NX` (si no existe), `XX` (si existe).
    - **Expiración (TTL):** `EXPIRE` (en segundos), `PEXPIRE` (en milisegundos).
    - **Contadores Atómicos:** `INCR`, `DECR`, `INCRBY`, `DECRBY`.
    - **Hashes:** `HSET`, `HGET`, `HGETALL`, `HMGET`, `HINCRBY` (para representar objetos con subclaves).
    - **Listas:** `LPUSH`, `RPUSH`, `LPOP`, `RPOP`, `LLEN`, `LRANGE`, `LTRIM`, `BLPOP`, `BRPOP` (para colas/pilas).
    - **Conjuntos (Sets):** `SADD`, `SREM`, `SISMEMBER`, `SMEMBERS`, `SCARD`, `SRANDMEMBER` (para elementos únicos sin orden).
    - **Operaciones entre Conjuntos:** `SINTER` (intersección), `SUNION` (unión), `SDIFF` (diferencia).
    - **Conjuntos Ordenados (Sorted Sets):** `ZADD` (con score), `ZRANGE`, `ZREVRANGE`, `ZRANGEBYSCORE` (para rankings).
    - **Bitmaps:** `SETBIT`, `GETBIT` (para flags booleanos, ahorro de espacio).
    - **Geoespacial:** `GEOADD`, `GEODIST`, `GEORADIUS` (para consultas de proximidad).
    - **Hyperloglog:** `PFADD`, `PFCOUNT` (para conteo probabilístico de ocurrencias únicas con bajo consumo de memoria).
    - **Streams:** `XADD`, `XRANGE` (para series de tiempo, IoT, eventos).
    - **Operaciones sobre Claves en General:** `EXISTS`, `TYPE`, `TTL`, `SCAN` (para iterar claves).
    - **Transacciones (Simuladas):** `MULTI`, `EXEC`, `DISCARD` (garantizan atomicidad y aislamiento, pero no rollback completo en caso de error lógico).
    - **Bloqueo Optimista:** `WATCH` (para asegurar que una clave no fue modificada por otro cliente antes de una transacción).
    - **Scripts LUA:** Para funcionalidades no cubiertas por comandos nativos (ejecución atómica, pero pueden bloquear si son largos).
    - **Módulos (Redis Modules):** Extienden la funcionalidad (ej. RedisJSON, RediSearch, RedisGraph).
    
- **Qué NO se puede hacer en Redis (o no es su función principal):**
    
    - **Transacciones Completas:** No ofrece el mismo nivel de transaccionalidad y rollback que una base de datos relacional.
    - **Consultas por Valores:** No se puede consultar directamente el contenido del valor si es opaco (ej. buscar un campo dentro de un string JSON sin parsearlo).
    - **Consistencia y Durabilidad como Base de Datos Principal:** Aunque tiene mecanismos de persistencia, no es su función principal garantizar la durabilidad total del dato como una base de datos relacional.
    - **Joins:** No soporta joins entre claves o estructuras.
    - **Esquema Rígido:** No impone un esquema, lo que puede llevar a inconsistencias si no se maneja bien desde la aplicación.
    - **Grandes Volúmenes de Datos en una Sola Estructura:** Aunque las estructuras no tienen límite de tamaño, guardar datasets muy grandes en una sola lista o hash puede ser ineficiente para replicación/distribución.
    - **Búsquedas Full-Text Complejas:** Aunque RediSearch existe, no es su fortaleza principal comparado con ElasticSearch.
    

### **6. Comparación con Bases de Datos Relacionales**

|**Característica**|**Bases de Datos Relacionales**|**Bases de Datos NoSQL (General)**|**Redis (Específico)**|
|---|---|---|---|
|**Modelado**|Rígido, estructurado (tablas, filas, columnas).|Flexible, _schemaless_ (documentos, clave-valor, grafos).|Modelo clave-valor con estructuras avanzadas (strings, hashes, listas, sets, sorted sets, streams).|
|**Normalización**|Alta (evita repetición de datos).|Desnormalización (replica datos para optimizar consultas).|Desnormalización (datos agregados en valores).|
|**Joins**|Fundamentales, pero costosos.|Generalmente no soportados (resueltos por la aplicación).|No soporta joins.|
|**Escalabilidad**|Escalabilidad vertical (más CPU, RAM, disco a un nodo).|Escalabilidad horizontal (añadir nodos al clúster).|Escalabilidad horizontal (clúster con partición de datos/sharding).|
|**Consistencia**|Consistencia fuerte (ACID).|Varía según modelo (eventual, fuerte, etc.).|Atomicidad en operaciones simples y transacciones simuladas, pero sin rollback completo.|
|**Durabilidad**|Alta (persistencia en disco con logs).|Varía (algunas priorizan velocidad sobre durabilidad).|Principalmente en memoria, con mecanismos de persistencia secundarios (RDB, AOF).|
|**Costo Espacial**|Bajo (menos repetición por normalización).|Alto (más repetición por desnormalización).|Alto (datos en memoria, estructuras ocupan espacio adicional).|
|**Costo Computacional**|Alto (joins y consultas complejas).|Bajo (consultas directas a estructuras agregadas).|Muy bajo (operaciones en memoria con O(1) o cercano).|
|**Casos de Uso**|Transacciones complejas, datos estructurados, integridad de datos.|Big Data, datos no estructurados, escalabilidad y disponibilidad.|Caché, contadores, colas, rankings, pub/sub, sesiones, analítica en tiempo real.|

---

👉 Con esta versión ya queda clara la comparación:

- Relacional = consistencia e integridad.
    
- NoSQL = flexibilidad y escalabilidad.
    
- Redis = ultra rápido, especializado en memoria.

### **7. Preguntas y Respuestas del Examen (Recopilación)**

- **Pregunta 1:** El modelo relacional fue diseñado para trabajar con grandes volúmenes de datos no estructurados. (Verdadero/Falso)
    
    - **Respuesta:** Falso. El modelo relacional está diseñado para datos estructurados y no se adapta eficientemente a grandes volúmenes de datos no estructurados.
    
- **Pregunta 2:** ¿Qué entendemos por escalabilidad horizontal y por qué es importante en entornos de Big Data?
    
    - **Respuesta:** La escalabilidad horizontal se refiere a aumentar la capacidad de un clúster agregando más nodos. Es crucial en Big Data porque permite manejar el crecimiento masivo de datos y usuarios distribuyendo la carga entre múltiples máquinas, a diferencia de la escalabilidad vertical que solo aumenta los recursos de un único servidor. Los datos modernos (sensores, logs, apps móviles) son inherentemente distribuidos, haciendo la escalabilidad horizontal necesaria.
    
- **Pregunta 3:** ¿Cuál de los siguientes factores fue fundamental para el surgimiento del movimiento de Big Data? (Múltiple Choice)
    
    - a) La disminución del uso de dispositivos móviles.
    - b) El incremento de la capacidad de procesamiento de los mainframes.
    - c) La explosión de datos generados por usuarios, sensores, redes sociales y dispositivos.
    - d) La consolidación del modelo relacional como estándar para todos los tipos de datos.
    - **Respuesta:** c) La explosión de datos generados por usuarios, sensores, redes sociales y dispositivos. (Relacionado con las 4 V: Volumen, Velocidad, Variedad, Veracidad).
    
- **Pregunta 4:** NoSQL significa "No Structured Query Language" y excluye toda posibilidad de realizar consultas complejas sobre los datos. (Verdadero/Falso)
    
    - **Respuesta:** Falso. NoSQL significa "Not Only SQL". No excluye consultas complejas, sino que ofrece alternativas y complementa a las bases de datos relacionales.
    
- **Pregunta 5:** ¿Qué características comunes tienen las bases de datos NoSQL? (Múltiple Choice, varias correctas)
    
    - a) Escalamiento horizontal.
    - b) Rígida estructura de tablas.
    - c) Alta disponibilidad.
    - d) Capacidad para trabajar con datos no estructurados.
    - **Respuesta:** a), c), d). Las bases de datos NoSQL no imponen una estructura rígida y están diseñadas para escalar horizontalmente y ser altamente disponibles.
    
- **Pregunta 6:** Uno de los motivos por los cuales surgen nuevas bases de datos es que las bases relacionales presentan limitaciones para escalar eficientemente en arquitecturas distribuidas. (Verdadero/Falso)
    
    - **Respuesta:** Verdadero. Esta es una de las principales razones, llevando a empresas como Google o Netflix a desarrollar sus propios motores NoSQL.
    
- **Pregunta 7:** Menciona al menos dos diferencias claves entre bases de datos relacionales y bases de datos NoSQL.
    
    - **Respuesta:**
        
        - **Estructura de Datos:** Relacionales usan tablas rígidas; NoSQL usan modelos flexibles (documentos, clave-valor, grafos).
        - **Normalización:** Relacionales buscan normalización; NoSQL priorizan la desnormalización.
        - **Escalabilidad:** Relacionales escalan verticalmente; NoSQL escalan horizontalmente.
        - **Joins:** Relacionales los usan extensivamente; NoSQL los evitan o los resuelven en la aplicación.
        - **Consistencia:** Relacionales ofrecen fuerte consistencia (ACID); NoSQL varían (consistencia eventual).
        
    
- **Pregunta 8:** ¿Qué enunciado refleja mejor el objetivo del movimiento de NoSQL? (Múltiple Choice)
    
    - a) Eliminar por completo el modelo relacional.
    - b) Ofrecer una solución alternativa para casos en que el modelo relacional no es eficiente.
    - c) Sustituir SQL como lenguaje estándar.
    - d) Crear bases de datos centralizadas para entornos de Big Data.
    - **Respuesta:** b) Ofrecer una solución alternativa para casos en que el modelo relacional no es eficiente. El objetivo es complementar, no reemplazar.
    

### **8. Lecciones Aprendidas y Consejos Prácticos**

- **Importancia del Modelado:** El modelado de datos es crucial, especialmente en NoSQL, donde la estructura de los datos y las claves debe alinearse con los patrones de acceso y las consultas esperadas.
- **Desnormalización vs. Normalización:** Entender cuándo aplicar cada una es clave. La desnormalización en NoSQL optimiza la lectura a costa de la repetición de datos.
- **Atomicidad del Agregado:** En NoSQL, el agregado es la unidad atómica de operación, replicación y distribución. Mantener los agregados compactos es vital para la performance.
- **NoSQL no es "No SQL":** Significa "Not Only SQL", complementando las bases de datos relacionales, no reemplazándolas.
- **Elegir la Herramienta Correcta:** Cada tipo de base de datos (relacional, Key-Value, Column Family, Document, Graph) tiene sus fortalezas y debilidades. La elección depende del caso de uso específico (persistencia políglota).
- **Redis como Caché:** Su principal fortaleza es la velocidad y el bajo tiempo de respuesta, ideal para datos temporales o de alta frecuencia de acceso.
- **Limitaciones de Redis:** No es una base de datos transaccional completa ni está diseñada para la durabilidad principal de datos. Las "transacciones" son simulaciones.
- **Funcionalidades de Redis:** Redis va más allá de un simple Key-Value, ofreciendo diversas estructuras de datos (hashes, listas, sets, sorted sets, streams, etc.) que permiten implementar funcionalidades complejas de manera eficiente.
- **Diseño de Claves en Redis:** Un esquema consistente en las claves (ej. `user:ID:tweets`) es fundamental para organizar y acceder a los datos de manera lógica, emulando consultas.
- **Cuidado con Operaciones Bloqueantes:** En Redis, al ser single-threaded, operaciones largas (como `KEYS` o scripts LUA complejos) pueden bloquear el servidor.
- **Módulos de Redis:** Permiten extender la funcionalidad de Redis para casos de uso más específicos (JSON, búsqueda, grafos), pero siempre considerando si es la herramienta óptima para esa necesidad principal.
- **Preparación para TPs:** Entregar scripts de carga, comandos ejecutados y documentación detallada con capturas de pantalla es crucial para la evaluación.