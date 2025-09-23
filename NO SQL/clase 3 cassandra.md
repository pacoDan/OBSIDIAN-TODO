### **1. Introducción a Column Family y Cassandra**

- **Definición de Column Family:** Agrupación lógica de columnas bajo un mismo prefijo. Cada fila puede tener una cantidad distinta de columnas con valores y prefijos diferentes.
- **White Column / White Row:** Filas que crecen a lo ancho con una cantidad de columnas casi ilimitada.
- **Row Key / Partition Key:** Clave principal que agrupa las columnas. En Cassandra, es la clave de acceso obligatoria.
- **Estructura de Column Family:** `Row Key` -> `(Column Key, Value)` -> `(Column Key, Value)`...
- **Clustering Column:** Segunda clave para ordenar y buscar datos dentro de una `Partition Key`. Permite búsquedas jerárquicas.
- **Valores Opacos:** No se puede buscar directamente por el valor de una columna; el valor debería ser una clave para ello.
- **Uso Incorrecto de Cassandra:** Empresas que usan Cassandra como una base de datos relacional, resultando en consultas de bajo rendimiento.
- **Metodología de Chebotko:** Metodología de diseño de Cassandra guiada por las consultas (`query-driven methodology`).

### **2. Ejemplo de Modelado en Cassandra (Alumno-Materia)**

- **Escenario:** Qué materias cursó un alumno específico.
- **Row Key:** Legajo del alumno (porque la consulta es por alumno).
- **Columnas:** Nombre de la materia (como clave de acceso) y número de curso (como valor).
- **Filas Distintas:** Dos filas de la misma `column family` pueden tener columnas diferentes y en distinta cantidad.
- **Diferencia con SQL:** La columna "materia" se almacena como clave de acceso y el número de curso como valor, diferente a cómo se maneja en SQL.
- **Vista Lógica:** `n` `row keys`, cada una con un conjunto de `(columna, valor)`.

### **3. Arquitectura y Características de Cassandra**

- **Tipo de Base de Datos:** Column Family, Peer-to-Peer.
- **Modelo Peer-to-Peer:** Cualquier nodo puede leer o escribir datos, a diferencia de Master-Slave.
- **Base de Datos Distribuida:** No tiene Single Point of Failure (SPOF).
    
    - **SPOF:** Único punto de falla (puede ser software o hardware). Cassandra está diseñada para evitarlo.
    
- **Teorema CAP:** Cassandra prioriza **A**vailability (disponibilidad) y **P**artition Tolerance (tolerancia a particiones de red), pero no la **C**onsistency (consistencia fuerte). Tiene consistencia eventual.
    
    - **Consistencia Eventual:** Los datos pueden ser inconsistentes temporalmente durante una partición de red, pero eventualmente se sincronizarán.
    - **Comparación con HBase:** HBase está en el segmento CP (Consistencia y Tolerancia a Particiones), inhabilitando parte del clúster para asegurar consistencia.
    
- **Escalabilidad:** Lineal y masivamente escalable (hasta miles de nodos).
- **Organización Lógica:** Tablas, filas y columnas (pero no es un modelo relacional).
- **Lenguaje de Consulta:** Cassandra Query Language (CQL), similar a SQL pero con diferencias fundamentales.
- **Origen:** Desarrollado por Facebook, basado en especificaciones de Google BigTable.
- **Versiones:** Evolución constante, la versión actual es 5.0.4 (febrero 2025).
- **Estructura Lógica:**
    
    - **Cluster:** Conjunto de servidores.
    - **Keyspace:** Equivalente a una base de datos.
    - **Column Family (Table):** Equivalente a una tabla.
    - **Filas:** Contienen `Partition Key` y el resto de la estructura.
    
- **Protocolo Gossip:** Los nodos se comunican para conocer su estado.
- **Replicación:** Los datos se replican en múltiples nodos (definido por `replication factor` en el `keyspace`) para alta disponibilidad y distribución de carga.
- **Unidad Básica de Replicación y Particionamiento:** La partición (`Partition Key`).
- **Mentira de Cassandra:** A partir de la versión 2, `Column Family` se llama `Table`, lo que puede confundir con bases de datos relacionales.
- **Ausencia de Joins:** No se pueden unir tablas en Cassandra. La única forma es obtener un valor de una tabla y usarlo para buscar en otra (programáticamente).
- **Ausencia de Foreign Keys:** No hay integridad referencial.
- **Ausencia de Transacciones ACID:** No cumple con atomicidad, consistencia, aislamiento y durabilidad como en bases de datos relacionales.
- **Modelado Query-Driven:** El modelado se basa en las consultas de negocio.

### **4. CQL (Cassandra Query Language)**

- **CREATE KEYSPACE:** Define una base de datos con propiedades de replicación.
- **CREATE TABLE:** Define la tabla, columnas, tipos de datos y la `PRIMARY KEY`.
    
    - **PRIMARY KEY:** Compuesta por `Partition Key` (entre paréntesis) y `Clustering Columns`.
    - **Partition Key:** Clave de acceso fundamental.
    - **Clustering Columns:** Ordenan los datos dentro de la partición y permiten búsquedas jerárquicas.
    
- **INSERT:** Similar a SQL.
- **TRUNCATE:** Elimina todos los datos de una tabla, pero la tabla sigue existiendo.
- **SELECT:**
    
    - `SELECT * FROM table`: Realiza un `table scan` en todos los nodos, lo cual es muy costoso en grandes volúmenes.
    - **Búsqueda por Partition Key:** Eficiente.
    - **Búsqueda por Clustering Column:** Eficiente si se usa junto con la `Partition Key` y en el orden correcto.
    - **`ALLOW FILTERING`:** Permite consultas que no usan la `Partition Key` o `Clustering Columns` en el orden esperado. **¡Es una mala práctica en producción!** Fuerza una búsqueda secuencial en todos los nodos, lo que es extremadamente lento para grandes volúmenes.
    
- **UPDATE:**
    
    - Requiere geoposicionamiento exacto (usando `Partition Key` y `Clustering Columns`).
    - Funciona como `UPSERT`: si el registro no existe, lo crea; si existe, lo actualiza.
    
- **DELETE:**
    
    - Puede borrar una columna específica o una fila completa (si se especifica solo la `Partition Key`).
    
- **Base de Datos Sparsa:** Los valores nulos o vacíos no ocupan espacio.

### **5. Tipos de Datos Especiales en Cassandra**

- **Text:** String.
- **Integer, BigInteger:** Números enteros.
- **Timestamp, Date:** Fechas y horas.
- **UUID (Universal Unique ID):** ID universal basado en un hash que combina fecha, servidor, timestamp, etc., asegurando unicidad global.
- **Counter:**
    
    - **Propósito:** Contadores numéricos.
    - **Restricciones:** No pueden ser parte de la `PRIMARY KEY` (ni `Partition Key` ni `Clustering Column`) porque mutan constantemente.
    - **Operaciones:** Solo se pueden actualizar (`UPDATE`), no insertar (`INSERT`). El `UPDATE` actúa como `UPSERT`.
    - **Manejo de Concurrencia:** Atómico.
    
- **Collections:**
    
    - **SET:** Lista de valores únicos (sin duplicados).
        
        - **Sintaxis:** `{valor1, valor2}`.
        - **Comportamiento:** Si se intenta agregar un valor existente, no se añade.
        
    - **LIST:** Lista de valores que permite duplicados.
        
        - **Sintaxis:** `[valor1, valor2]`.
        - **Operaciones:** Se pueden agregar elementos al principio o al final, y actualizar elementos por índice.
        
    - **MAP:** Lista de pares clave-valor.
        
        - **Sintaxis:** `{clave1: valor1, clave2: valor2}`.
        - **Comportamiento:** La clave dentro del `MAP` es única; si se intenta agregar una clave existente, se actualiza su valor.
        
    

### **6. Metodología de Chebotko para Modelado**

- **Flujo de Operaciones:**
    
    1. **Modelo Conceptual:** Entender el modelo de negocio (DER tradicional).
    2. **Workflow de la Aplicación:** Definir las consultas y sus interacciones.
    3. **Mapeo Conceptual a Lógico:** Traducir el modelo conceptual y las consultas a un modelo lógico de Cassandra.
    4. **Modelo Físico:** Implementar el modelo en Cassandra.
    
- **Principios para Modelar en Cassandra:**
    
    - **Conocer tus Datos:** Entender el modelo conceptual de negocio.
    - **Conocer tus Consultas:** Definir las consultas y el flujo de interacción.
    - **Anidar tus Datos:** Usar colecciones dentro de las tablas.
    - **Tener en Cuenta las Particiones:** Entender cómo se distribuyen los datos.
    - **Duplicar tus Datos:** Crear múltiples `Column Families` con los mismos datos organizados de forma diferente para optimizar distintas consultas.
    
- **Premisas para el Mapeo Conceptual:**
    
    - **Entidades y Relaciones:** Se mapean a tablas (`Column Families`).
    - **Atributos de Búsqueda por Igualdad:** Se convierten en `Partition Key`.
    - **Atributos de Búsqueda por Inecuación (rangos):** Se convierten en `Clustering Columns`.
    - **Atributos de Ordenamiento:** Se convierten en `Clustering Columns` (el orden importa).
    - **Atributos para Unicidad:** Se convierten en `Clustering Columns` para garantizar geoposicionamiento exacto.
    

## Preguntas y Respuestas para Exámenes

### **1. Preguntas sobre Column Family y Cassandra Básicos**

- **Pregunta:** ¿Qué es una base de datos Column Family y cómo se diferencia de una base de datos relacional en términos de estructura de fila?
    
    - **Respuesta:** Una Column Family agrupa lógicamente columnas. A diferencia de una base de datos relacional donde todas las filas de una tabla tienen la misma estructura de columnas, en una Column Family, cada fila puede tener una cantidad distinta de columnas con valores y prefijos diferentes. Son "white rows" que crecen a lo ancho.
    
- **Pregunta:** Explique el concepto de "Row Key" o "Partition Key" en Cassandra. ¿Por qué es fundamental?
    
    - **Respuesta:** La Row Key (o Partition Key) es la clave principal que agrupa un conjunto de columnas en una Column Family. Es fundamental porque es la clave de acceso obligatoria para buscar cualquier dato en una tabla de Cassandra. Sin ella, las búsquedas son ineficientes o imposibles.
    
- **Pregunta:** ¿Qué es una "Clustering Column" y cuál es su propósito en Cassandra?
    
    - **Respuesta:** Una Clustering Column es una segunda clave que se utiliza para ordenar los datos dentro de una Partition Key. Permite realizar búsquedas jerárquicas y eficientes dentro de una partición, y también puede usarse para garantizar la unicidad de los registros dentro de esa partición.
    
- **Pregunta:** ¿Por qué se dice que los valores en Cassandra son "opacos" para la búsqueda directa?
    
    - **Respuesta:** Los valores de las columnas en Cassandra son opacos para la búsqueda directa porque no se puede buscar directamente por el contenido de un valor. Para que un valor sea buscable, debe ser parte de una clave (Partition Key o Clustering Column). Intentar buscar por un valor sin que sea clave resultaría en un `table scan` ineficiente.
    

### **2. Preguntas sobre Arquitectura y Características**

- **Pregunta:** Describa el modelo "Peer-to-Peer" de Cassandra y cómo contribuye a su alta disponibilidad.
    
    - **Respuesta:** En un modelo Peer-to-Peer, todos los nodos son iguales y pueden leer o escribir datos. A diferencia de un modelo Master-Slave, no hay un único punto de falla. Si un nodo falla, otros nodos pueden seguir sirviendo las solicitudes, lo que garantiza una alta disponibilidad del sistema.
    
- **Pregunta:** ¿Cómo se relaciona Cassandra con el Teorema CAP? ¿Qué implicaciones tiene esto para su uso?
    
    - **Respuesta:** Cassandra se posiciona en el segmento "AP" del Teorema CAP, priorizando la **A**vailability (disponibilidad) y la **P**artition Tolerance (tolerancia a particiones de red) sobre la **C**onsistency (consistencia fuerte). Esto significa que, en caso de una partición de red, Cassandra seguirá operando y aceptando escrituras, aunque los datos puedan ser temporalmente inconsistentes entre nodos (consistencia eventual). Esto la hace ideal para aplicaciones que requieren alta disponibilidad y escalabilidad, incluso a costa de una consistencia inmediata.
    
- **Pregunta:** ¿Por qué Cassandra no tiene "Single Point of Failure" (SPOF)?
    
    - **Respuesta:** Cassandra no tiene SPOF porque su arquitectura distribuida y peer-to-peer replica los datos en múltiples nodos. Si un nodo falla, otros nodos tienen copias de los datos y pueden continuar operando, asegurando que el sistema permanezca disponible. El SPOF puede ser tanto de software como de hardware.
    
- **Pregunta:** ¿Es posible realizar `JOIN`s entre tablas en Cassandra? Justifique su respuesta.
    
    - **Respuesta:** No, no es posible realizar `JOIN`s directamente entre tablas en Cassandra. Cassandra no es una base de datos relacional y no soporta operaciones de `JOIN`. Para simular una unión, se debe obtener un valor de una tabla y luego usar ese valor para realizar una segunda consulta en otra tabla, lo cual debe ser manejado a nivel de aplicación.
    
- **Pregunta:** ¿Cassandra soporta transacciones ACID como las bases de datos relacionales?
    
    - **Respuesta:** No, Cassandra no soporta transacciones ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad) en el sentido estricto de las bases de datos relacionales. Ofrece consistencia eventual y mecanismos para garantizar la durabilidad, pero no las garantías transaccionales completas de un sistema relacional.
    

### **3. Preguntas sobre CQL y Operaciones**

- **Pregunta:** ¿Cuál es la diferencia fundamental entre `INSERT` y `UPDATE` en Cassandra, especialmente en el contexto de los "Counters" y el concepto de "UPSERT"?
    
    - **Respuesta:** En Cassandra, el `UPDATE` funciona como un `UPSERT`: si el registro no existe, lo crea; si existe, lo actualiza. Para los "Counters", solo se permite `UPDATE` (que actúa como `UPSERT`), no `INSERT`, porque los contadores mutan y no pueden ser insertados con un valor inicial de la misma manera que otros tipos de datos.
    
- **Pregunta:** Explique por qué el uso de `ALLOW FILTERING` en una consulta CQL es una mala práctica en entornos de producción con grandes volúmenes de datos.
    
    - **Respuesta:** `ALLOW FILTERING` fuerza a Cassandra a realizar un `table scan` (búsqueda secuencial) sobre todos los nodos del clúster para encontrar los datos que cumplen la condición. Esto es extremadamente ineficiente y lento para grandes volúmenes de datos, ya que no aprovecha la distribución de datos por `Partition Key`. Su uso indica un modelado de datos incorrecto para las consultas deseadas.
    
- **Pregunta:** ¿Qué restricciones existen para el uso de "Counters" en Cassandra?
    
    - **Respuesta:** Los "Counters" no pueden ser parte de la `PRIMARY KEY` (ni `Partition Key` ni `Clustering Column`) porque su valor muta constantemente, lo que afectaría la distribución de datos. Además, no se pueden `INSERTAR` directamente; solo se pueden `ACTUALIZAR` (`UPDATE`), y el `UPDATE` actúa como un `UPSERT` para ellos.
    
- **Pregunta:** Describa la diferencia entre los tipos de colección `SET` y `LIST` en Cassandra.
    
    - **Respuesta:** Un `SET` es una colección de valores únicos, lo que significa que no permite duplicados. Si se intenta agregar un valor que ya existe, la operación no tendrá efecto. Un `LIST`, por otro lado, es una colección ordenada de valores que sí permite duplicados. Se pueden agregar elementos al principio o al final, y se pueden actualizar elementos por su índice.
    

### **4. Preguntas sobre Modelado de Datos**

- **Pregunta:** ¿Cuál es el principio fundamental del modelado de datos en Cassandra según la metodología de Chebotko?
    
    - **Respuesta:** El principio fundamental es el "modelado basado en consultas" (`query-driven data modeling`). Esto significa que el diseño de las tablas (Column Families) se define en función de las consultas de negocio que se esperan realizar, en lugar de un modelo relacional normalizado.
    
- **Pregunta:** ¿Por qué es común y aceptable "duplicar datos" en Cassandra?
    
    - **Respuesta:** Es común y aceptable duplicar datos en Cassandra creando múltiples `Column Families` con los mismos datos organizados de forma diferente. Esto se hace para optimizar distintas consultas. Por ejemplo, si se necesita buscar datos por "alumno" y también por "materia", se pueden crear dos tablas separadas, cada una optimizada para una de esas consultas, lo que mejora significativamente el rendimiento de acceso. El costo de almacenamiento es menor que el costo de procesamiento.
    
- **Pregunta:** Si una consulta de negocio requiere buscar datos por un rango de fechas, ¿qué tipo de clave debería ser el campo de fecha en el modelo de Cassandra?
    
    - **Respuesta:** Si una consulta requiere buscar datos por un rango (inecuación), el campo de fecha debería ser una `Clustering Column`. Esto permite que Cassandra ordene los datos dentro de la partición por fecha y realice búsquedas de rango eficientemente.
    

## Lecciones Aprendidas

- **Cassandra no es SQL:** Aunque CQL se parezca a SQL, Cassandra es fundamentalmente diferente de una base de datos relacional. Intentar usarla como una relacional llevará a problemas de rendimiento y frustración.
- **El Modelado es Clave:** El éxito con Cassandra depende casi por completo de un buen modelado de datos, que debe ser `query-driven`. Es crucial entender las consultas de negocio antes de diseñar las tablas.
- **Prioridad AP:** Cassandra prioriza la disponibilidad y la tolerancia a particiones, lo que la hace excelente para sistemas distribuidos a gran escala, pero implica una consistencia eventual.
- **Evitar `ALLOW FILTERING`:** Esta cláusula es un "anti-patrón" en producción. Si una consulta la requiere, es una señal de que el modelo de datos es incorrecto para esa consulta.
- **Duplicación de Datos:** Es una práctica aceptada y necesaria para optimizar el rendimiento de diferentes consultas. El almacenamiento es barato, el procesamiento es caro.
- **Restricciones de Claves:** Entender qué tipos de datos pueden ser `Partition Keys` o `Clustering Columns` (ej. los `Counters` no pueden ser claves).
- **Geoposicionamiento en Updates:** Los `UPDATE`s requieren una especificación exacta de la `Partition Key` y `Clustering Columns` para localizar el dato.
- **Tipos de Datos Especiales:** Cassandra ofrece tipos de datos como `Counters`, `Sets`, `Lists` y `Maps` que permiten modelar datos complejos de manera eficiente, pero con sus propias reglas y restricciones.
- **Comunicación con el Negocio:** Es fundamental que los desarrolladores y arquitectos de datos trabajen de cerca con los dueños de producto para entender las necesidades de consulta del negocio.

## Diferencias Clave: Relacional/SQL vs. Cassandra

### **Base de Datos Relacional/SQL**

- **Modelo de Datos:** Relacional, basado en tablas con esquemas fijos y predefinidos.
- **Estructura de Filas:** Todas las filas en una tabla tienen la misma estructura de columnas.
- **Normalización:** Se busca la normalización para reducir la redundancia y mantener la integridad de los datos (formas normales).
- **Consultas:** Lenguaje SQL estándar. Permite `JOIN`s complejos entre tablas, `FOREIGN KEYS` para integridad referencial.
- **Transacciones:** Soporte completo de transacciones ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad).
- **Escalabilidad:** Principalmente escalabilidad vertical (aumentar recursos de un solo servidor). La escalabilidad horizontal es más compleja.
- **Consistencia:** Consistencia fuerte (todos los nodos tienen la misma vista de los datos en todo momento).
- **Modelado:** Orientado a la estructura de los datos y las relaciones entre ellos.
- **Uso Típico:** Aplicaciones transaccionales (OLTP) que requieren alta integridad de datos y consultas complejas sobre datos relacionados.

### **Cassandra (Column Family)**

- **Modelo de Datos:** NoSQL, Column Family. Esquema flexible (cada fila puede tener columnas diferentes).
- **Estructura de Filas:** "White rows" – las filas pueden tener una cantidad variable de columnas.
- **Normalización:** No se busca la normalización. Se acepta y fomenta la **duplicación de datos** para optimizar el rendimiento de las consultas.
- **Consultas:** Cassandra Query Language (CQL), similar a SQL pero con **restricciones significativas**.
    
    - **No hay `JOIN`s:** Las uniones deben ser manejadas a nivel de aplicación.
    - **No hay `FOREIGN KEYS`:** No hay integridad referencial automática.
    - **Búsquedas:** Altamente optimizadas por `Partition Key` y `Clustering Columns`. Las búsquedas que no usan estas claves son ineficientes (`ALLOW FILTERING` es una mala práctica).
    
- **Transacciones:** No soporta transacciones ACID completas. Ofrece consistencia eventual.
- **Escalabilidad:** Lineal y masivamente escalable horizontalmente (añadir más nodos).
- **Consistencia:** Consistencia eventual (prioriza disponibilidad y tolerancia a particiones).
- **Modelado:** **`Query-driven`** (orientado a las consultas). El diseño de la tabla se basa en cómo se accederán los datos.
- **Uso Típico:** Aplicaciones con grandes volúmenes de datos, alta disponibilidad, baja latencia y patrones de acceso predecibles (ej. redes sociales, IoT, personalización de sitios web).

### **Qué NO se puede hacer en Cassandra (y sí en SQL)**

- **`JOIN`s entre tablas:** No hay soporte nativo.
- **`FOREIGN KEYS`:** No hay integridad referencial automática.
- **Transacciones ACID completas:** No hay garantías de atomicidad, consistencia fuerte, aislamiento y durabilidad en el mismo sentido que SQL.
- **Consultas ad-hoc complejas:** No está diseñada para consultas exploratorias o complejas que no se ajusten a los patrones de acceso definidos por las `Partition Keys` y `Clustering Columns`.
- **Búsquedas eficientes por cualquier columna:** Solo es eficiente si la columna es parte de la `PRIMARY KEY` (Partition o Clustering).
- **`INSERT`s en `COUNTER`s:** Solo `UPDATE`s.
- **Cambiar la `Partition Key` de un registro:** Implicaría mover el registro a otro nodo, lo cual es ineficiente.
- **Modelar sin conocer las consultas:** Un modelo relacional genérico no funcionará bien en Cassandra.

### **Qué SÍ se puede hacer en Cassandra (y es su fortaleza)**

- **Escalar horizontalmente a grandes volúmenes de datos:** Maneja petabytes de datos y miles de nodos.
- **Alta disponibilidad:** Diseñada para no tener SPOF y seguir operando incluso con fallos de nodos o particiones de red.
- **Baja latencia en escrituras y lecturas:** Muy rápida para patrones de acceso predecibles.
- **Modelado `query-driven`:** Optimizar el rendimiento para consultas específicas.
- **Duplicar datos:** Crear múltiples vistas de los mismos datos para diferentes patrones de consulta.
- **Usar `Partition Keys` y `Clustering Columns`:** Para definir patrones de acceso eficientes y ordenar datos.
- **Manejar datos semi-estructurados:** Gracias a su esquema flexible y tipos de colección (Set, List, Map).
- **Contadores atómicos:** `COUNTER`s para manejar incrementos/decrementos concurrentes.
- **`UPSERT`s:** `UPDATE`s que insertan si el registro no existe.

En resumen, Cassandra es una herramienta poderosa para escenarios específicos que requieren escalabilidad masiva, alta disponibilidad y baja latencia para patrones de acceso de datos bien definidos. No es un reemplazo universal para las bases de datos relacionales, y su uso efectivo requiere un cambio fundamental en la mentalidad de modelado de datos.