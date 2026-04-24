I. Fundamentos de Consistencia y Distribución

La consistencia en bases de datos distribuidas es un desafío crucial, refiriéndose a que la información obtenida en una consulta sea la más actualizada, sin importar el nodo consultado.

A. Consistencia vs. Integridad

Es esencial distinguir entre estos dos conceptos:

• **Consistencia:** Se refiere a la **corrección de los datos** según la lógica de negocio que se defina.

• **Integridad:** Garantiza el **cumplimiento automático** de las reglas de integridad referencial y de entidad (como las claves primarias/foráneas).

B. Consistencia en Bases de Datos Relacionales (RDBMs)

• Las bases de datos relacionales son sistemas con **consistencia muy fuerte**.

• Las transacciones se rigen por las propiedades **ACID** (Atomicidad, Consistencia, Aislamiento y Durabilidad), que son fundamentales para la integridad de los datos.

C. Consistencia en Bases de Datos NoSQL

• En el mundo NoSQL, las propiedades ACID no siempre son fundamentales.

• La consistencia ya no es absoluta; depende de la aplicación y de la **necesidad del negocio**.

• Aparecen conceptos como el **Teorema CAP** y la **Consistencia Eventual**.

--------------------------------------------------------------------------------

II. El Teorema CAP (Consistencia, Disponibilidad y Tolerancia a Particiones)

El Teorema CAP establece que un sistema distribuido no puede garantizar simultáneamente las tres propiedades de manera absoluta. Este teorema fue propuesto por la gente de Berkeley y probado formalmente por el MIT en 2002.

A. Propiedades CAP

1. **Consistencia (C):** Asegura que todos los nodos del clúster tienen la misma versión del dato al momento de consultarlo.

2. **Disponibilidad (A):** Garantiza que los datos estén accesibles y que el sistema pueda seguir funcionando incluso si algunos nodos fallan (evitando el **SPOF**, o _Single Point of Failure_).

3. **Tolerancia a Particiones de Red (P):** Asegura que el sistema puede continuar operando si la red se divide o se corta, quedando nodos separados físicamente o aislados.

B. Segmentos del Teorema CAP

No existe un motor de base de datos distribuido que cumpla absolutamente las tres propiedades. Las bases de datos se sitúan en uno de estos espacios:

• **Espacio CA (Consistencia y Disponibilidad):** Incluye bases de datos que no están distribuidas horizontalmente. Ejemplos: Bases de datos relacionales y Neo4j.

• **Espacio CP (Consistencia y Tolerancia a Particiones):** Priorizan la **consistencia** y resuelven bien las particiones de red, sacrificando la disponibilidad. Ejemplos: **MongoDB** y HBase.

• **Espacio AP (Disponibilidad y Tolerancia a Particiones):** Priorizan la disponibilidad, sacrificando la consistencia. Ejemplos: Cassandra (que ofrece consistencia eventual).

C. Consistencia Eventual

La Consistencia Eventual significa que los datos pueden ser inconsistentes al momento de la escritura (_momento cero_), pero **eventualmente se estabilizarán y se volverán consistentes**. Un ejemplo común fuera de bases de datos son los DNS.

--------------------------------------------------------------------------------

III. Gestión de la Consistencia en MongoDB

MongoDB utiliza la configuración de Réplica Sets (conjunto de réplicas) y parámetros específicos para controlar el nivel de consistencia deseado en las operaciones.

A. El Concepto de Quórum

Para asegurar la consistencia y disponibilidad, se utiliza el concepto de **quórum**, donde la consistencia se verifica en una **mayoría de nodos**, típicamente la mitad más uno (N/2+1).

• Si un Replica Set (ej. de 3 nodos) pierde quórum (solo queda 1 nodo vivo), el nodo restante se pondrá en modo **solo lectura (****readonly****)** porque no puede asegurar la consistencia, priorizando C sobre A.

• El **Árbitro (****Arbiter****)** es un nodo sin datos de usuario, que sirve únicamente para votar y dar quórum en caso de _failover_, lo cual es útil para configuraciones de dos nodos con datos (PSA).

B. Parámetros de Escritura y Lectura (N, W, R)

|   |   |   |
|---|---|---|
|Parámetro|Definición|Impacto en Consistencia|
|**N** (Réplicas)|Cantidad de réplicas definidas para un conjunto o _keyspace_. **No es la cantidad total de nodos** en el clúster.|Se usa para calcular la mayoría (quórum).|
|**W** (Write Concern)|Define cuántas copias deben grabarse sincrónicamente para que la operación de escritura se considere exitosa.|**W alto** (ej. igual a N o `majority`) asegura **mayor consistencia** de escritura, pero afecta la velocidad y puede fallar si un nodo cae.|
|**R** (Read Concern)|Define cuántos nodos deben ser consultados sincrónicamente en una lectura.|**R alto** asegura una **consistencia de lectura más fuerte**, pero afecta el rendimiento.|

Consistencia Fuerte por Escritura

Una política de **consistencia fuerte en escrituras** asegura que el dato se graba sincrónicamente en múltiples nodos (ej. **W=N**), lo que permite que las lecturas sean rápidas (R bajo) sin problemas de consistencia, aunque esta configuración no se recomienda por su alto costo y riesgo de indisponibilidad.

Valores Clave en MongoDB

• **W por Defecto:** Es `1` (el _primary_ confirma la inserción).

• **majority** **(W y R):** Es una palabra reservada que garantiza que la operación se realice en la mayoría de los miembros del Replica Set, adaptándose automáticamente si el número de réplicas cambia.

• **Journaling (****J: true****):** Asegura que los datos se graben en un **registro transaccional en disco** (_journal_) antes de la confirmación a la aplicación (en menos de 50ms), fundamental para la recuperación (_recovery_).

C. Configuración de Lectura (Read Preference y Read Concern)

Los **niveles de Read Concern** permiten definir la fuerza de consistencia de la lectura:

• **majority****:** Garantiza que los datos más recientes estén escritos en la mayoría de los nodos réplica.

• **Nearest****:** Permite leer del nodo con **menor latencia** de red, útil en clústeres distribuidos geográficamente.

• **Read Preference:** Define _de dónde_ se debe leer: `primary` (default, garantiza consistencia plena), `secondary only`, o `primary preferred` (lee de un _secondary_ si el _primary_ no está disponible).

D. Transacciones y Validación de Esquemas

• **Transacciones (Mongo 4.x):** MongoDB implementó transacciones con comandos como `start transaction`, `commit transaction` y `abort transaction`, que permiten manejar operaciones de `insert` y `update` de manera atómica.

• **Validación de Esquemas (Mongo 3.2+):** Permite controlar el modelo de datos _schemaless_.

    ◦ **validationAction****:** Define la acción ante una violación de la regla: `warn` (registra la violación sin fallar) o `error` (impide la operación).

    ◦ **validationLevel****:** Define la aplicación de las reglas: `strict` (aplica a inserciones y modificaciones) o `moderate` (aplica a inserciones y solo a _updates_ de documentos que ya cumplen la regla).

--------------------------------------------------------------------------------

IV. Preguntas y Respuestas Clave para Exámenes

Se recopilan las preguntas y respuestas directamente relacionadas con los conceptos de consistencia y el Teorema CAP extraídas de las transcripciones.

|   |   |   |   |
|---|---|---|---|
|Nro.|Pregunta|Respuesta y Justificación|Fuente(s)|
|**1**|¿Un sistema distribuido puede garantizar simultáneamente Consistencia, Disponibilidad y Tolerancia a Particiones?|**Falso**. El Teorema CAP establece que solo puede garantizar dos de estas tres propiedades.||
|**2**|¿Qué motor utilizaría para implementar un sistema de votación electrónica, donde la consistencia es la prioridad?|**Relacional**. Es un caso de uso sensible donde la **consistencia** (propiedades ACID) es la prioridad.||
|**3**|Neo4j (Base de Grafos) se encuentra en el espacio **CP** del Teorema CAP.|**Falso**. Neo4j y las bases relacionales se encuentran en el espacio **CA** (Consistencia y Disponibilidad) porque no están distribuidas horizontalmente.||
|**4**|¿Cómo se relaciona Cassandra con el Teorema CAP?|Cassandra se posiciona en el segmento **AP** (Disponibilidad y Tolerancia a Particiones), sacrificando la **Consistencia**.||
|**5**|¿Por qué utilizar un único motor de base de datos para la totalidad de una aplicación puede dar soluciones de bajo rendimiento?|**Respuesta:** Porque cada motor está diseñado para un tipo de caso de uso especial. Forzar todos los casos de uso a un mismo esquema puede generar consultas ineficientes, estresar el nodo principal y causar problemas de escalabilidad.||
|**6**|¿Cuál es la función del Balancer en un esquema de _sharding_?|**Función:** Redistribuir los _chunks_ (rangos de datos) entre las particiones (_shards_) para equilibrar la carga.||
|**7**|¿Qué sucede si un Replica Set de 3 nodos pierde 2 nodos?|El nodo Primary restante se pondrá en modo **solo lectura (****readonly****)** porque no cumple con el quórum (N/2+1) y no puede garantizar la consistencia.||
|**8**|¿Es una buena política poner un W (Write Concern) igual a N (número de réplicas)?|**Falso**. Aunque garantiza consistencia fuerte en la escritura, es costoso, afecta la velocidad de inserción y tiene un alto riesgo de fallar la operación si un servidor cae, lo que no es recomendado en servidores _commodity_.||

--------------------------------------------------------------------------------

V. Lecciones Aprendidas y Consideraciones Profesionales

A. Implicaciones de Consistencia y Latencia

1. **Quórum y Seguridad:** La mínima configuración segura de un Replica Set es de 3 nodos (idealmente PSS: Primary, Secondary, Secondary, o PSA: Primary, Secondary, Arbiter) para garantizar el quórum.

2. **Partición de Red:** Una partición de red es un corte de conectividad que puede aislar nodos. MongoDB prioriza la consistencia; si un nodo pierde el quórum debido a una partición, se pone en _readonly_ para evitar inconsistencias con otros segmentos del clúster.

3. **Slave Delay** **(Retraso de Esclavo):** Un nodo secundario puede configurarse con un retraso intencional en la replicación (ej. 1 hora) para servir como un **punto de restauración de emergencia** en caso de que un error catastrófico (como una eliminación accidental) se replique demasiado rápido a los otros nodos.

B. Consistencia y Operaciones en MongoDB/Sharding

1. **Inserciones sin Consistencia Fuerte:** Un **W bajo** (ej. W=1) aumenta la velocidad de inserción, lo cual es útil para sistemas de ingesta de datos o APIs con alta concurrencia, incluso a riesgo de una consistencia eventual a corto plazo.

2. **Riesgo de Lectura Inconsistente (R bajo):** Si el valor de R es bajo y la lectura ocurre inmediatamente después de una inserción, el dato podría estar desactualizado si aún no se ha replicado al _secondary_ consultado.

3. **Acceso al Cluster Shardeado:** En un cluster con _sharding_ (particionamiento), es crucial que las aplicaciones se conecten a través del **Mongo S** (el _proxy_ de consultas) para garantizar que los datos se busquen en la partición correcta. Conectarse directamente a los Replica Sets (_shards_) es una **mala práctica (****macana****)** porque solo se verían los datos de ese _shard_ y no la colección completa.

4. **Eficiencia de Consultas Particionadas:** Las consultas son **muy rápidas** si se utiliza la clave de partición (_sharding key_), ya que Mongo S puede dirigir la consulta a un solo _shard_ (_single shard_). Las consultas que no usan la clave de partición son **mucho más lentas** porque requieren buscar en todas las particiones (_shard merge_ y _colscan_).

---

sharding:

Aquí tienes un resumen detallado y estructurado de toda la información sobre **Sharding (Particionamiento)** en MongoDB, extrayendo los conceptos clave, la justificación, los componentes y la operativa, según las transcripciones proporcionadas.

---

## I. Fundamentos y Justificación del Sharding

El _sharding_ o particionamiento es una estrategia de escalamiento horizontal que permite a las bases de datos NoSQL manejar grandes volúmenes de datos distribuyéndolos en múltiples servidores.

### A. Diferencia entre Sharding y Replicación

Es crucial distinguir el _sharding_ de la replicación, aunque en producción deben combinarse.

|Concepto|Propósito|Aplicación|
|:--|:--|:--|
|**Replicación**|Copiar los **mismos datos** en distintos servidores (nodos) para asegurar la **Alta Disponibilidad (HA)**.|Si un servidor cae, otro nodo idéntico toma el control.|
|**Sharding (Particionamiento)**|Distribuye **datos diferentes** entre múltiples servidores, donde la suma de todas las partes conforma el 100% de la base de datos.|Permite distribuir la carga de escrituras, lecturas y gestionar el volumen de almacenamiento.|

### B. Necesidad y Consideraciones de Uso

El _sharding_ es una técnica que debe aplicarse **estrictamente si es necesario**, debido a la complejidad y costos que añade.

- **Necesidad Principal:** Se aplica cuando la cantidad de datos que se maneja estresa la capacidad de almacenamiento y procesamiento de un solo servidor.
- **Producción:** Para entornos productivos, es la **única opción** combinar la replicación y el particionamiento. El _sharding_ sin replicación resulta en una arquitectura sin Alta Disponibilidad (HA) y un riesgo de pérdida total de datos.
- **Colecciones Específicas:** MongoDB no particiona la base de datos completa, sino **colecciones específicas** (generalmente aquellas con un volumen masivo de transacciones, no colecciones pequeñas como clientes).
- **Costo y Complejidad:** El _sharding_ no es una práctica recomendada por gusto, ya que implica un **costo administrativo y de manejo** significativo que complica la infraestructura.

---

## II. Componentes de un Clúster Shardeado en MongoDB

Un clúster distribuido en MongoDB requiere de tres componentes clave que trabajan juntos para gestionar los datos y la metadata.

|Componente|Función y Rol|Configuración Clave|
|:--|:--|:--|
|**Particiones (_Shards_)**|Los contenedores físicos de los datos distribuidos. Cada partición debe ser un **Replica Set** (conjunto de réplicas) para garantizar la HA.|Los nodos del Replica Set deben iniciarse con el parámetro `--shardsvr`.|
|**Servidores de Configuración (_Config Servers_)**|**Almacenan la metadata** del clúster: qué colecciones existen, cuáles están particionadas y dónde se encuentra mapeado cada rango de datos (_chunk_).|Deben ser obligatoriamente un **Replica Set** (aunque en entornos de desarrollo pueden simularse con un solo nodo).|
|**Roteadores de Consulta (_Mongo S_)**|Actúan como **proxy** o interfaz entre la aplicación y el clúster. Leen la metadata para dirigir las consultas y escrituras a la partición correcta.|Se levanta con el binario `mongos` y debe apuntar al Replica Set de configuración mediante el comando `--configdb`.|

- **Acceso (Proxy):** Las aplicaciones deben conectarse **siempre** a través del Mongo S (el proxy) para acceder a los datos. Conectarse directamente a los Replica Sets (_shards_) es una mala práctica, ya que solo se verían los datos contenidos en esa partición y no la colección completa.
- **Mínimo de Servidores:** Simular un entorno de producción con dos particiones (shards) requeriría un mínimo de 10 servidores (un Mongo S, 3 Config Servers y 3 nodos en cada uno de los dos Replica Sets).

---

## III. Operativa del Sharding y Distribución de Datos

### A. Clave de Sharding (Partition Key)

Para particionar una colección, es necesario definir una clave de partición.

1. **Creación de Índice:** Primero se debe **crear un índice** en la colección utilizando la clave deseada.
2. **Particionamiento de la Colección:** Se usa el comando `shardCollection`, especificando la base de datos, la colección y la clave (índice).
3. **Tipos de Clave:**
    - **Basado en Rangos:** Utiliza un valor de negocio (ej. fechas, IDs de cliente). Permite consultas eficientes basadas en rangos.
    - **Basado en Hash:** Aplica una función de _hash_ a un campo (ej. ID) para asegurar una **distribución uniforme y aleatoria** de los datos. Esto dificulta las búsquedas por rango.

### B. Chunks y Distribución Lógica

El Mongo S utiliza el concepto de _Chunks_ para mapear los datos dentro del clúster.

- **Definición:** Un _chunk_ es un **concepto lógico** (un rango de valores) que mapea un conjunto de documentos de una colección en una partición específica.
- **Tamaño por Defecto:** El tamaño por defecto de un _chunk_ es de **1024 megas** y se puede modificar creando un documento `_id: "chunksize"` en la colección `config.settings`.
- **Splitting:** Cuando los documentos que referencian a un _chunk_ superan el tamaño máximo, el proceso de _splitting_ divide ese rango en dos _chunks_ lógicos, pero **no mueve los documentos físicamente**. El _splitting_ solo actualiza la metadata.

### C. Balanceador (_Balancer_)

El _balancer_ es el proceso encargado de mover físicamente los datos entre particiones.

- **Función:** Mueve los documentos de los _chunks_ de una partición a otra para **mantener un equilibrio** en la carga de almacenamiento y procesamiento.
- **Activación:** El _balancer_ entra en acción automáticamente cuando se agrega una nueva partición a un clúster _shardeado_ que ya contiene _chunks_.
- **Overhead y Horarios:** Mover datos genera un **overhead** significativo en la red y el rendimiento. Se recomienda no realizar esta configuración durante las horas de producción y se puede configurar el _balancer_ para funcionar en una **ventana de tiempo específica** (ej. de madrugada) o inhabilitarlo hasta que sea necesario.
- **Prioridad de Consultas:** Durante la migración de datos, las consultas impactarán el dato en su ubicación **original** (_shard original_). Se asume que MongoDB prioriza las consultas sobre el balanceo.
- **Escrituras durante Balanceo:** Si el _balancer_ está corriendo, las nuevas inserciones de datos se mandan al _shard_ original donde se creó el _chunk_, incluso si este _chunk_ está en proceso de moverse a otro _shard_.

### D. Impacto en el Rendimiento de Consultas

La eficiencia de una consulta depende directamente de si utiliza o no la clave de partición.

- **Consulta Rápida (con clave de partición):** Si la búsqueda utiliza la clave de partición (ej. `cliente_region`), el Mongo S puede determinar que el dato está en un **Single Shard** (una sola partición) y realiza un **Index Scan**, lo cual es muy rápido.
- **Consulta Lenta (sin clave de partición):** Si la búsqueda se realiza sin la clave de partición, el sistema tiene que buscar en **todas las particiones**. Esto resulta en un **Shard Merge** y un **Col Scan** (escaneo de colección completo en cada _shard_), siendo un proceso mucho más lento.

---

## IV. Simulación Práctica de Sharding (Resumen de la Práctica)

La transcripción describe el proceso paso a paso para configurar un clúster shardeado de prueba:

1. **Creación del Replica Set R1:** Se levantan 3 servidores (`27058`, `27059`, `27060`) como miembros de un Replica Set llamado `R1` y se les inserta una colección grande (ej. 73,000 facturas).
2. **Configuración Shard Server:** Se reinician los nodos del Replica Set `R1` con el parámetro `--shardsvr` para que puedan actuar como particiones.
3. **Creación del Config Server y Mongo S:**
    - Se levanta el servidor de configuración (Config Server) en un puerto separado (ej. `27500`) y se inicializa como su propio Replica Set.
    - Se levanta el Mongo S (el proxy) apuntando al Config Server.
4. **Conexión del Shard R1:** Se conecta el Replica Set `R1` al clúster usando el comando `sh.addShard` (o `db.runCommand({ addShard: "R1/..." })`) a través del Mongo S.
5. **Habilitación y Particionamiento:**
    - Se habilita el particionamiento para la base de datos (ej. `finanzas`).
    - Se crea un índice con la clave de _sharding_ y se aplica el `shardCollection`.
    - **Creación de Chunks Lógicos:** Este paso crea la metadata de los _chunks_ (rangos), pero los datos permanecen en `R1`.
6. **Adición del Shard R2:** Se crea un segundo Replica Set (`R2`) con sus propios nodos (`27158`, etc.) y se agrega al clúster.
7. **Balanceo y Migración:** Al agregar `R2`, el _balancer_ comienza a actuar, moviendo físicamente los documentos de algunos _chunks_ de `R1` a `R2` para equilibrar la carga.

---

## V. Preguntas y Respuestas Clave para Exámenes (Sharding)

|Nro.|Pregunta|Tipo|Respuesta y Justificación|Fuente(s)|
|:--|:--|:--|:--|:--|
|**1**|¿Cuál es la diferencia entre replicación y particionamiento (_sharding_)?|Desarrollo|La **replicación** copia los mismos datos para alta disponibilidad; el **particionamiento** distribuye datos diferentes en cada servidor para escalamiento horizontal.|
|**2**|¿Por qué no se recomienda usar _sharding_ solo (sin replicación) en producción?|Desarrollo|Porque una partición sin réplicas es un **Single Point of Failure (SPOF)**. Si ese servidor cae, se pierde la porción de datos que contenía, comprometiendo la HA.|
|**3**|¿Cuáles son los tres componentes clave de un clúster _shardeado_ en MongoDB?|Desarrollo|**1. Particiones (_Shards_)** (Replica Sets que almacenan los datos); **2. Servidores de Configuración** (Replica Sets que almacenan la metadata); **3. Roteadores de Consulta (Mongo S)** (el proxy que dirige el tráfico).|
|**4**|¿Cuál es la función del Balancer en un esquema de _sharding_?|Desarrollo|**Mover físicamente los datos** (los _chunks_) entre las distintas particiones (_shards_) para mantener una distribución equilibrada de la carga.|
|**5**|¿Por qué una búsqueda sin la clave de partición (_sharding key_) es mucho más lenta en un clúster _shardeado_?|Desarrollo|Porque obliga al sistema a realizar un **Shard Merge** y un **Col Scan** (escaneo de colección) en **todas las particiones** del clúster, en lugar de dirigirse a un _Single Shard_.|
|**6**|¿Cuál es el riesgo de ejecutar el Balancer durante las horas de producción?|Desarrollo|Genera un **overhead** significativo debido al movimiento de datos a través de la red, lo que puede afectar la performance de otros procesos y causar lentitud.|
|**7**|¿Qué es un _chunk_ en el contexto de _sharding_ de MongoDB?|Desarrollo|Un **rango lógico de valores** que mapea un conjunto de documentos a una partición. Es metadata y no un archivo físico.|
|**8**|¿Qué hace el proceso de _splitting_?|Desarrollo|Divide un _chunk_ lógico en dos nuevos _chunks_ cuando este supera el tamaño configurado (ej. 1024 megas), pero **no mueve los datos físicamente**.|
|**9**|¿Qué tipo de colecciones son las más adecuadas para ser particionadas?|Múltiple Opción|Colecciones con **volúmenes masivos de datos** o transacciones, ya que estas son las que estresan la capacidad de un servidor.|