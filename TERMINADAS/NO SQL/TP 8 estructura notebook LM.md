Este informe detallado consolida los conceptos adquiridos sobre bases de datos NoSQL, la infraestructura de Big Data y el análisis específico de los principales motores (MongoDB, Redis, Cassandra, Neo4j), junto con recomendaciones de modelado para bases de datos de Series de Tiempo.

---

## INFORME DE CONCEPTOS AVANZADOS NO SQL Y ESTRATEGIAS DE PERSISTENCIA POLÍGLOTA

## I. Tecnologías Relacionadas con Data & Analytics y Big Data

El movimiento Big Data surgió por la necesidad de manejar el **Volumen** (cantidad masiva de datos), la **Velocidad** (rapidez de generación y procesamiento) y la **Variedad** (diversidad de formatos como logs, JSON, imágenes, etc.) de los datos.

Las tecnologías de Big Data y Data & Analytics se centran en el **Escalamiento Horizontal** (agregar más servidores) para distribuir el procesamiento y el almacenamiento, ya que el escalamiento vertical (aumentar recursos en un solo servidor) resulta insuficiente y costoso para estos volúmenes.

### A. Ecosistema Tecnológico

Las bases de datos NoSQL son parte del mundo operacional/transaccional. Las plataformas analíticas complejas o _Data Warehouses_ orientadas a Big Data incluyen:

1. **Sistemas de Procesamiento Distribuido:** Plataformas como **Hadoop** y **MapReduce** (procesamiento en paralelo).
2. **Plataformas de _Streaming_ y Análisis:** Tecnologías como **Spark**.
3. **Almacenamiento de Objetos (_Object Storage_):** Utilizado para guardar datos semi-estructurados y no estructurados a bajo costo.
4. **_Data Warehouses_ en la Nube:** Productos modernos como **Snowflake** y **Google BigQuery** han mostrado un crecimiento significativo, compitiendo con soluciones tradicionales.

### B. Couchbase y Bases de Datos Tipo Time Series (TD)

Las bases de datos documentales, como Couchbase, almacenan documentos (generalmente JSON) y son conocidas por su esquema flexible (_schemaless_).

**Utilidad de Couchbase para Time Series:** Los documentos proporcionados **no detallan la utilidad específica de Couchbase** como una base de datos de series de tiempo.

Sin embargo, para manejar datos de **Telemetría, Time Series o Logs**, que requieren **escrituras masivas a escalas gigantes**, la persistencia políglota recomienda:

- **Column Family (ej. Cassandra):** Este modelo es capaz de manejar escrituras masivas, lo que lo hace una **gran elección** para datos de sensores.
- **Documental:** El modelo documental también puede adaptarse a este tipo de datos, especialmente si las estructuras de los _logs_ son muy variantes.

---

## II. Análisis Detallado de Motores de Persistencia

A continuación, se presenta un análisis comparativo de los principales motores NoSQL y el modelo relacional (RDBMs).

|Motor|1. Características Generales|2. Operaciones Básicas|3. Consistencia y CAP|4. Funcionalidad de Replicación|5. Características Especiales|6. Caso de Uso Recomendado|
|:--|:--|:--|:--|:--|:--|:--|
|**RDBMs**|Basado en tablas con esquema rígido. Escalamiento principalmente **Vertical**.|**CRUD** (Create, Read, Update, Delete) mediante SQL. Uso intensivo de **JOINs** y Claves Foráneas.|**ACID** (Atomicidad, Consistencia, Aislamiento, Durabilidad). Consistencia muy **fuerte**. Espacio **CA** (Consistencia y Disponibilidad).|Esquema **Master/Slave** (Maestro/Esclavo).|Integridad de la Entidad y Referencial. Adecuado para **Legacy**.|Sistemas Financieros, Facturación, Banca, o votación electrónica (donde la **Consistencia** es prioridad).|
|**MongoDB** (Documental)|Líder del segmento documental. Almacena documentos en **BSON** (JSON binario). Modelo _schemaless_ o con validación de esquemas.|**CRUD** (Insert, Find, Update, Remove). Lenguaje de consulta basado en JSON. Soporte para **Transacciones** (a partir de v4.x).|Espacio **CP** (Consistencia y Tolerancia a Particiones). Prioriza la consistencia sobre la disponibilidad.|**Replica Set** (Maestro/Esclavo/Árbitro). Replicación asincrónica (OpLog).|**Sharding** (Particionamiento) con componentes clave: **Mongo S**, **Config Servers**, **Shards**. **Journaling** (J: true) para recovery.|Catálogos de productos, Órdenes completadas, Documentación.|
|**Cassandra** (Column Family)|Modelo **Peer-to-Peer** (todos los nodos iguales). Masivamente escalable y lineal. El modelado es _Query-Driven_.|**CQL** (similar a SQL). **INSERT** y **UPDATE** funcionan como **UPSERT**. No soporta **JOINs** ni Claves Foráneas.|Espacio **AP** (Disponibilidad y Tolerancia a Particiones). Ofrece **Consistencia Eventual**.|Modelo Peer-to-Peer. La replicación se define por **Replication Factor** en el _Keyspace_. Particionamiento y Replicación combinadas.|**No SPOF** (Single Point of Failure). Tipos de colección especiales (Set, List, Map). Contadores (_Counter_) atómicos.|Datos de Sensores, Telemetría, Logs. Aplicaciones que requieren alta **Disponibilidad** y escalabilidad.|
|**Redis** (Key-Value)|Base de datos **In-Memory** (en memoria). Escrita en C (para performance).|**SET, GET, DEL** (strings). Estructuras avanzadas (Hashes, Lists, Sorted Sets, Streams). Transacciones simuladas (**MULTI/EXEC**).|Espacio **CP**. Atomicidad garantizada en comandos simples. Durabilidad secundaria (RDB/AOF).|Esquema **Master/Slave**. Cluster para escalamiento (Sharding).|**Ultra-rápido** (latencia muy baja). Uso principal para Caché, sesiones, contadores atómicos y rankings.|Caché Distribuido, Datos de Sesión, CDN (Content Delivery Network).|
|**Neo4j** (Grafos)|Basado en **Nodos**, **Relaciones** (arcos) y **Propiedades**. No distribuye los datos horizontalmente (no tiene _sharding_).|Lenguaje **Cypher**. Cláusulas **MATCH** (patrones) y **MERGE** (upsert). Función `shortestPath` para ruteo.|Cumple con propiedades **ACID**. Consistencia **fuerte**. Ubicado en el espacio **CA** o **CP**.|Replicación posible (Causal Cluster), pero no particionamiento de datos geográfico.|Las **Relaciones son físicas y directas** (punteros), no enlaces lógicos como las Claves Foráneas. **Visualización** intuitiva.|Motores de Recomendación, Detección de Fraude, Servicios de Ruteo/Logística.|

---

## III. Analogía NoSQL para Developers y Expertos

Los sistemas NoSQL se eligen por la **flexibilidad y escalabilidad** que ofrecen, complementando las RDBMs.

Si consideramos una plataforma como un equipo de especialistas en persistencia, los puntos fuertes de NoSQL se manifiestan en la elección del experto adecuado para la tarea:

|Motor|Analogía para Developers/Expertos|Puntos Fuertes de NoSQL|
|:--|:--|:--|
|**Redis**|**El Corredor de 100 Metros:** Es el especialista en velocidad pura (O(1)). Guarda la información en memoria para acceso inmediato. No le pidas que te haga un _join_ complejo, solo que te dé el dato ahora.|**Velocidad y Latencia Mínima:** Ideal para sistemas que requieren tiempos de respuesta ultrarrápidos para la experiencia del usuario (ej. caché de sesiones, _leaderboards_).|
|**MongoDB**|**El Archivista Flexible:** Es el experto en guardar documentos, capaz de manejar estructuras cambiantes (_schemaless_). Puede guardar documentos completos (agregados) de forma atómica. Es el motor documental más completo del mercado.|**Flexibilidad de Esquema y Atomicidad:** Permite la evolución rápida de la aplicación sin migraciones de esquema costosas, manteniendo la **atomicidad del agregado** (la unidad de registro compleja).|
|**Cassandra**|**El Maestro de la Distribución Global:** Es el experto en escalamiento masivo. Diseñado para recibir escrituras concurrentes desde miles de nodos sin caerse (Peer-to-Peer). Sacrifica la consistencia inmediata por **Disponibilidad** total.|**Escalabilidad Lineal y Alta Disponibilidad (AP):** Excelente para ingesta de datos de IoT o redes sociales donde el volumen es la mayor preocupación, y la **Consistencia Eventual** es aceptable.|
|**Neo4j**|**El Sociólogo o Cartógrafo:** Es el experto en relaciones. Maneja nodos y arcos de forma física y directa, lo que hace que buscar el "amigo de mi amigo de mi amigo" sea trivial. No distribuye los datos en múltiples regiones, pero es ACID en su operación.|**Consultas Relacionales Complejas y Ruteo:** Su fortaleza es la gestión de relaciones complejas, con rendimiento superior a las RDBMs para búsquedas recursivas o patrones (ej. fraudes o recomendaciones).|

---

## IV. Estructuración y Recomendaciones para Bases de Datos Time Series

Para manejar millones y millones de datos de series de tiempo (como datos de sensores o telemetría), se requieren estrategias de modelado orientadas a la **ingesta masiva** y el **rango de tiempo**. Las fuentes sugieren que las bases **Column Family (Cassandra)** son altamente capaces para este fin.

### A. Estructuración y Modelado (Basado en Column Family)

El modelado debe ser _query-driven_, priorizando las consultas basadas en la clave de partición y el tiempo.

1. **Clave de Partición (Partition Key):** Es la clave fundamental de acceso en sistemas distribuidos.
    - Para datos Time Series, la clave de partición debe agrupar los datos por la **entidad consultada** (ej. `ID_Sensor` o `ID_Máquina`) y, si el volumen de una sola entidad es demasiado alto en un corto periodo, combinarse con una **unidad de tiempo superior** (ej. `ID_Sensor + Mes`) para distribuir la carga de escrituras en múltiples nodos.
2. **Clustering Columns:** Definen el ordenamiento y las búsquedas eficientes dentro de una partición.
    - La **marca de tiempo (Timestamp)** debe ser la principal _Clustering Column_. Esto asegura que los datos se ordenen cronológicamente dentro de cada partición (sensor) y permite búsquedas eficientes por rango de tiempo (ej. "dame todos los datos del Sensor X entre las 14:00 y las 15:00").
3. **Desnormalización:** Es aceptable y necesario **duplicar** los metadatos del sensor (ej. ubicación, tipo de sensor) en la tabla principal de series de tiempo para evitar _JOINs_ programáticos.

### B. Interacción y Recomendaciones

|Componente|Recomendación y Uso|Interacción/Justificación|
|:--|:--|:--|
|**Backend (Servicio de Ingesta)**|Usar un **W** (Write Concern) **bajo** (ej. W=1 o W=majority). Priorizar la **velocidad de inserción**.|El _Backend_ maneja la **Velocidad**. Un W bajo (o consistencia eventual en Cassandra) asegura la máxima ingesta sin estresar el _primary_.|
|**Backend (Configuración)**|Implementar **sharding/particionamiento**.|La ingesta masiva (millones de datos) requiere distribuir los datos en **múltiples nodos** para manejar el **Volumen**.|
|**Frontend/Reporting**|Usar consultas que aprovechen la **Clave de Partición y el Tiempo** (Clustering Column).|El _Frontend_ debe pedir datos de forma **eficiente**. Consultar sin la clave de partición resulta en un **Col Scan masivo** (_shard merge_) y es una mala práctica.|
|**Administración (Ops)**|Utilizar el **Balancer** solo en horas de bajo tráfico.|El movimiento de datos (balanceo) genera un **overhead** significativo y afecta el rendimiento del sistema.|
|**Recomendación General**|Aplicar **Persistencia Políglota**.|Usar un Key-Value Store (Redis) para el **caché** de los _queries_ de series de tiempo más comunes y un motor de **Column Family** (Cassandra) para el almacenamiento masivo y permanente.|