https://youtu.be/NaFY0ic19P8
La siguiente es una **Estructura Detallada de la Transcripción** enfocada en los conceptos de Consistencia y Sharding en MongoDB, incluyendo la recopilación de preguntas/respuestas de exámenes y lecciones aprendidas, según lo solicitado.

--------------------------------------------------------------------------------

I. Estructura y Componentes del Sharding en MongoDB

El _sharding_ (particionamiento) es un concepto clave de la distribución de datos que busca dividir la base de datos en varias partes y distribuirlas entre múltiples servidores, permitiendo el escalamiento horizontal.

A. Justificación y Objetivos del Sharding

El escalamiento horizontal (agregar más servidores) es la estrategia principal de las bases de datos NoSQL para manejar el volumen, la velocidad y la variedad de los datos.

1. **Escalamiento vs. Replicación:**

    ◦ **Replicación:** Copia los **mismos datos** en distintos servidores para alta disponibilidad (HA).

    ◦ **Particionamiento (****Sharding****):** Distribuye **datos diferentes** en cada servidor, donde la suma de todas las partes conforma el total de la base de datos.

2. **Necesidad:** El _sharding_ es necesario cuando el volumen de datos estresa la capacidad de almacenamiento y procesamiento de un solo servidor.

3. **Producción:** La única opción viable para producción es la **combinación de replicación y particionamiento**. Particionar sin replicar resulta en una arquitectura sin Alta Disponibilidad (HA), un riesgo de pérdida de datos.

4. **Beneficios:** Distribución de carga de escrituras y lecturas, y optimización de accesos.

B. Componentes Arquitectónicos del Cluster Shardeado

Un cluster de _sharding_ en MongoDB requiere tres componentes principales:

|   |   |   |
|---|---|---|
|Componente|Definición y Función|Configuración|
|**Particiones (****Shards****)**|Los contenedores reales de los datos. Cada partición es un **conjunto de réplicas** (_Replica Set_), no un servidor _standalone_.|Los nodos de un Replica Set deben incluir el parámetro `--shardsvr`.|
|**Servidores de Configuración (****Config Servers****)**|Almacenan la **metadata** del clúster: qué bases de datos y colecciones existen, y dónde se encuentran los datos (el mapeo de _chunks_).|Obligatoriamente deben ser un **Replica Set** (típicamente de tipo PSS o PSA en entornos de desarrollo).|
|**Roteadores de Consulta (****Mongo S****)**|Actúan como _proxy_ o interfaz entre la aplicación y el cluster. Consultan la metadata para determinar a qué partición (_shard_) enviar la consulta.|Es un binario diferente que se conecta al Replica Set de configuración mediante el comando `mongos --configdb`.|

C. Proceso y Claves de Particionamiento

1. **Colecciones Particionadas:** MongoDB no particiona la base de datos completa, sino **colecciones específicas** (ej. colecciones de transacciones masivas, no colecciones de clientes pequeños).

2. **Clave de Sharding:** Se debe definir una clave de partición. Puede ser:

    ◦ **Basada en Rangos:** Utiliza un valor de negocio (ej. fechas, IDs de cliente). Permite consultas eficientes basadas en rangos.

    ◦ **Basada en Hash:** Aplica una función de hash a un campo (ej. ID) para asegurar una **distribución uniforme** de los datos. Es menos eficiente para búsquedas por rango.

3. **Proceso:** Se requiere primero **crear un índice** en la colección con la clave de sharding. Luego se usa el comando `shardCollection`.

4. **Rendimiento de Consultas:** Una búsqueda que utiliza la clave de partición es muy rápida (_index scan_), ya que solo busca en una partición. Una búsqueda sin la clave de partición es mucho más lenta (_shard merge_ y _colscan_) porque debe buscar en todas las particiones.

D. Distribución y Balanceo de Datos

La distribución de datos se gestiona mediante conceptos lógicos y procesos de movimiento:

1. **Chunks** **(Rangos Lógicos):** Son rangos de valores que mapean los datos. Su tamaño por defecto es de 1024 megas.

2. **Splitting:** Cuando un _chunk_ crece más allá del tamaño especificado (por peso o cantidad de documentos), el proceso lo divide en dos nuevos _chunks_ lógicos, pero **no mueve los datos físicamente**.

3. **Balancer (Balanceador):** Es el proceso que **mueve físicamente** los documentos de un _chunk_ de una partición a otra para equilibrar la carga.

    ◦ **Configuración:** El balanceador puede ser inhabilitado o configurarse para funcionar solo en una ventana de tiempo específica (ej. de madrugada), ya que mover datos en producción genera _overhead_.

    ◦ **Prioridad:** Durante la migración de datos, MongoDB prioriza las consultas sobre el balanceo.

--------------------------------------------------------------------------------

II. Teoría y Práctica de Replicación en MongoDB

La replicación en MongoDB se gestiona mediante el concepto de **Replica Set** (conjunto de réplicas), que opera bajo un esquema Maestro/Esclavo.

A. Estructura de un Replica Set

• **Nodos:** Un Replica Set tiene un único **Primary** y uno o más **Secondaries**.

    ◦ El **Primary** es el único que acepta operaciones de escritura (_updates_), aunque también permite consultas.

    ◦ Los **Secondaries** solo permiten consultas.

• **Arbiters:** Un nodo _arbiter_ es un servidor que **no contiene datos de usuario** pero participa en la votación para garantizar el cuórum (la mitad más uno). Si un Primary cae, el Arbiter vota al Secondary con los datos más actualizados para convertirlo en el nuevo Primary.

• **Votación y Quórum:** Si un Replica Set pierde el cuórum (ej. dos de tres nodos caen), el nodo restante se pone en modo **solo lectura (****readonly****)**. MongoDB prioriza la consistencia sobre la disponibilidad en este escenario.

B. Parámetros de Configuración del Nodo

Los nodos en un Replica Set pueden configurarse para roles específicos:

|   |   |   |
|---|---|---|
|Parámetro|Función|Detalle Clave|
|`arbiterOnly: true`|Define el nodo como un _Arbiter_ (solo para votar).|No almacena datos y no paga licencia en versiones _Enterprise_.|
|`priority`|Prioridad para ser elegido como Primary.|`Priority: 0` significa que el nodo **nunca** puede ser Primary.|
|`slaveDelay`|Introduce un retraso intencional en la replicación.|Utilizado como estrategia de recuperación ante desastres (ej. revertir una eliminación accidental), ya que mantiene una copia atrasada.|
|`votes`|Define si el nodo puede votar. Máximo de 7 nodos pueden votar en un Replica Set grande.|Por defecto, votan todos. Se usa en clústeres de 50 nodos para limitar el coste de la votación.|

C. Proceso de Failover y Recuperación

1. **Caída del Primary:** Si el Primary se cae, los Secondaries votan (junto con los Arbiters) y eligen al nodo con el `uptime` más alto (el más actualizado) como el nuevo Primary.

2. **Reconexión:** Cuando el Primary original se recupera, se conecta al clúster como un **Secondary**.

3. **OpLog:** Los Secondaries replican el **OpLog** (log de operaciones) del Primary de manera asincrónica. Este log almacena todas las operaciones realizadas, y las Secondaries lo consumen para sincronizarse.

4. **Operación Extrema (Standalone):** En un caso extremo de emergencia (pérdida de casi todos los nodos), se puede sacar el servidor restante del Replica Set y levantarlo como _standalone_ (sin replicación) para que pueda aceptar escrituras y seguir operando, aunque con cero HA.

--------------------------------------------------------------------------------

III. Conceptos de Consistencia y Propiedades ACID/CAP

La consistencia en NoSQL no es absoluta, sino que se gestiona mediante configuraciones de lectura y escritura.

A. Consistencia y Teorema CAP

• **Definición:** La **Consistencia** se refiere a la corrección de los datos según la lógica de negocio, mientras que la **Integridad** garantiza el cumplimiento automático de reglas referenciales/de entidad.

• **Teorema CAP:** Los sistemas distribuidos solo pueden garantizar dos de tres propiedades simultáneamente: **C**onsistencia, **A**lta Disponibilidad y **P**artición de Red.

• **MongoDB en CAP:** MongoDB pertenece al espacio **CP** (Consistencia y Tolerancia a Particiones), sacrificando la disponibilidad.

• **Consistencia Eventual:** Bases de datos como Cassandra se ubican en el espacio **AP** (Disponibilidad y Tolerancia a Particiones), donde los datos pueden ser inconsistentes al momento de la escritura, pero eventualmente se sincronizarán.

B. Gestión de Consistencia (W, R)

MongoDB utiliza los parámetros **Write Concern (W)** y **Read Concern (R)** para definir el nivel de consistencia requerido para cada operación:

1. **W (Write Concern):** Define cuántas copias deben grabarse sincrónicamente para que la operación de escritura sea considerada exitosa.

    ◦ Una W alta asegura mayor consistencia, pero puede afectar la velocidad de inserción y la disponibilidad si un nodo falla.

    ◦ El valor `majority` se utiliza en lugar de un número específico para que el sistema se adapte automáticamente al número de nodos, garantizando la escritura en la mayoría (N/2+1).

2. **R (Read Concern):** Define cuántos nodos deben ser consultados sincrónicamente durante una operación de lectura.

    ◦ Una R alta ofrece una consistencia de lectura más fuerte pero afecta el rendimiento.

    ◦ `Nearest` permite leer del nodo con menor latencia de red, útil en clústeres geográficamente distribuidos.

3. **Journaling (****J: true****):** Garantiza que los datos se graben primero en un registro transaccional en disco (_journal_) antes de la confirmación a la aplicación, asegurando la recuperación.

--------------------------------------------------------------------------------

IV. Preguntas y Respuestas para Exámenes (QA y 8x8)

A. Preguntas y Respuestas de la Clase de Sharding y Consistencia (QA)

|   |   |   |   |
|---|---|---|---|
|Nro.|Pregunta|Respuesta y Justificación|Fuente(s)|
|**1**|¿Qué es el escalamiento vertical?|Aumentar la capacidad del mismo servidor (memoria, almacenamiento, CPU). Es más simple, pero es la única opción en las bases de datos relacionales tradicionales.||
|**2**|¿Qué es el escalamiento horizontal?|Agregar más servidores (nodos) al clúster para distribuir la carga. Permite usar servidores más pequeños y la HA la proporciona la plataforma.||
|**3**|¿Cuál es la diferencia entre replicación y particionamiento?|La **replicación** es copiar los mismos datos; el **particionamiento** (_sharding_) es tener datos diferentes en cada servidor.||
|**4**|¿Cuál es el principal problema del método de replicación _Peer-to-Peer_ (ej. Cassandra)?|El principal riesgo es la **consistencia** si ocurre una partición de red, ya que los datos podrían ser inconsistentes temporalmente.||
|**5**|¿Qué motor de base de datos se encuentra en el espacio **CA** (Consistencia y Disponibilidad) del Teorema CAP?|Bases de datos relacionales y Neo4j.||
|**6**|¿Qué motor de base de datos se encuentra en el espacio **CP** (Consistencia y Tolerancia a Particiones) del Teorema CAP?|MongoDB y HBase.||
|**7**|¿Qué motor de base de datos se encuentra en el espacio **AP** (Disponibilidad y Tolerancia a Particiones) del Teorema CAP?|Cassandra (que ofrece consistencia eventual).||
|**8**|¿Cuál es la función del **Balancer** en un esquema de _sharding_?|Redistribuir los _chunks_ (rangos de datos) entre las particiones para **equilibrar la carga** de almacenamiento y procesamiento.||
|**9**|¿Se puede usar el **Balancer** en un Replica Set sin _sharding_?|No. El _sharding_ implica particionamiento de datos, y los Replica Sets sin particionamiento solo replican el 100% de los datos.||
|**10**|¿Cuál es la diferencia entre **Arbiter** y **Secondary** en un Replica Set de MongoDB?|El **Secondary** es una copia viva de los datos del Primary. El **Arbiter** no contiene datos de usuario, solo existe para votar y dar cuórum en caso de _failover_.||
|**11**|¿Qué sucede si un Replica Set de 3 nodos pierde 2 nodos?|El nodo Primary restante se pondrá en modo **solo lectura (****readonly****)** porque no cumple con el quórum (mitad más uno) y no puede garantizar la consistencia.||
|**12**|¿Qué función cumple el parámetro `slaveDelay`?|Introduce un retraso intencional en la replicación, permitiendo que ese nodo actúe como punto de restauración ante un error catastrófico (ej. eliminación masiva).||

B. Preguntas y Respuestas de Persistencia Políglota (8x8)

|   |   |   |   |   |
|---|---|---|---|---|
|Nro|Pregunta|Tipo|Respuesta y Justificación|Fuente(s)|
|**1**|¿Por qué utilizar un único motor de base de datos para la totalidad de una aplicación puede dar soluciones de bajo rendimiento?|Desarrollo|Porque cada motor está diseñado para un caso de uso especial. Forzar todos los casos a un mismo esquema genera consultas ineficientes que estresan el _primary_ y causan problemas de escalabilidad.||
|**2**|Persistencia políglota se llama al uso de diferentes motores de base de datos NoSQL. Las RDBMs no son consideradas.|Verdadero/Falso|**Falso**. Cualquier motor de persistencia, incluidas las bases de datos relacionales (RDBMs), es bienvenido si agrega valor y resuelve el caso de uso.||
|**3**|Por lo general, en los sistemas con persistencia políglota, la seguridad yace en la aplicación.|Verdadero/Falso|**Verdadero**. Históricamente, los motores NoSQL se enfocaban en el caso de uso principal, delegando la seguridad (perfiles, roles) a la capa de aplicación.||
|**4**|Antes de realizar un desarrollo en una nueva tecnología de bases de datos, hay que evaluar si existen:|Múltiple Opción|**Todos**: Necesidades intensivas de procesamiento que justifiquen la nueva tecnología, la forma de acceso a los datos, y verificar que la tecnología esté probada y tenga buen soporte.||
|**5**|Siempre que se pueda hay que utilizar persistencia políglota.|Verdadero/Falso|**Falso**. La implementación debe ser justificada por el contexto, la complejidad, el costo y la naturaleza del proyecto (Criterio Uténiano, no fanatismo).||
|**6**|¿Qué motor utilizaría para implementar un sistema CDN (Content Delivery Network)?|Opción Múltiple|**Key Value Store**. Es la mejor opción dada la simpleza de recuperar un valor (contenido estático) por una clave (URL) con alta velocidad.||
|**7**|¿Qué motor utilizaría para implementar un sistema que permita consultar qué medio de transporte tomar para viajar de un punto a otro de la ciudad?|Opción Múltiple|**Graph** (Base de Grafos). Facilita el recorrido del gráfico y la búsqueda del camino más óptimo (ruteo, logística).||
|**8**|¿Qué motor utilizaría para implementar un sistema de votación electrónica, donde los resultados se publican al día siguiente de la elección?|Opción Múltiple|**Relacional**. Es un caso de uso sensible donde la **consistencia** (propiedades ACID) es la prioridad.||

--------------------------------------------------------------------------------

V. Lecciones Aprendidas Clave

A. Lecciones de Persistencia Políglota

1. **Criterio Uténiano:** La persistencia políglota (usar múltiples motores, incluyendo RDBMs, Key-Value, Documentales, Grafos) debe ser justificada por necesidades intensivas de procesamiento y no por moda.

2. **Riesgos de Implementación:** Multiplica la complejidad y los costos de _deployment_, monitoreo (_ops_) y mantenimiento. Es crucial hacer Pruebas de Concepto (POC) y analizar el costo-beneficio antes de proponer el cambio.

3. **Checklist de Implementación:** Antes de elegir un nuevo motor, se debe revisar: costos, _backup_ y restauración, RPO (_Restore Point Objective_) y RTO (_Restore Time Objective_), seguridad (Encryption at Rest/in Flight), disponibilidad de _drivers_ de calidad, y la capacidad del equipo para adoptar la nueva tecnología.

B. Lecciones de MongoDB Sharding y Replicación

1. **Prioridad de Consistencia:** MongoDB (CP) prioriza la consistencia; por ello, requiere quórum para aceptar escrituras.

2. **Particionamiento vs. Colección:** El _sharding_ se aplica a **colecciones específicas** (generalmente las más grandes), no a la base de datos completa.

3. **Rol del Arbiter:** El _Arbiter_ es clave para asegurar el cuórum en configuraciones de dos nodos con datos (PSA), sin aumentar los costos de almacenamiento.

4. **Anti-Patrón de Sharding:** Implementar _sharding_ sin replicación (particiones _standalone_) es un riesgo de pérdida total de datos en producción.

5. **Overhead del Sharding:** Configurar un cluster shardeado para producción es complejo y requiere levantar un mínimo de 10 servidores (ej. 3 Config Servers, 1 Mongo S, 2 Replica Sets con 3 nodos c/u).

6. **Operaciones en el Cluster:** Las búsquedas son óptimas si se usan la clave de partición, de lo contrario, se requiere un lento proceso de _shard merge_ (búsqueda en todas las particiones). El **Balancer** debe usarse fuera de las horas pico debido al _overhead_ que genera el movimiento físico de datos.