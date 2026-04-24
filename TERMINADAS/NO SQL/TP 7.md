
los Shards (conjuntos de réplicas que contienen los datos), los Servidores de Configuración (que almacenan la metadata del clúster) y el Mongo S (el _proxy_ o enrutador de consultas).

A continuación, se detalla la implementación y el análisis de consistencia, según lo solicitado.

--------------------------------------------------------------------------------

1. Implementación de Sharding en BD MongoDB

Para esta implementación, se asume que el Replica Set inicial (R1) ya está levantado y que los componentes de _sharding_ (Config Server y Mongo S) deben ser configurados.

1.1. Base: ReplicaSet (R1) y Configuración Inicial

Se requiere que el Replica Set base (`R1` en el ejemplo práctico de los fuentes) esté levantado (e.g., puertos 27058, 27059, 27060).

**Acción Requerida:** Iniciar cada nodo del Replica Set R1 con el parámetro `--shardsvr` para que puedan actuar como particiones.

_Ejemplo de comando (para el Primary):_

```
mongod --replSet R1 --port 27058 --dbpath /ruta/data/a1 --shardsvr
```

**Configuración del Clúster Shardeado (Config Server y Mongo S):**

1. **Levantar el Servidor de Configuración (Config Server):** Se debe crear un Replica Set para los servidores de configuración (ej. `RC` - Replica Config). En un entorno de producción, se necesitan 3 nodos, pero para la configuración mínima de desarrollo puede usarse uno solo.

    ◦ Se utiliza el parámetro `--configsvr` y se inicia como un Replica Set (ej. puerto 27500).

    ◦ Se debe inicializar el Replica Set: `rs.initiate()`.

2. **Levantar el Roteador de Consulta (Mongo S):** Se levanta el proceso `mongos` apuntando al Replica Set de configuración.

    ◦ _Ejemplo de comando:_ `mongos --configdb RC/localhost:27500 --port 27000` (usando el puerto 27000 como _proxy_).

3. **Conexión del Shard R1:** Conectarse al Mongo S (puerto 27000) y agregar el Replica Set R1 como el primer _shard_.

    ◦ `sh.addShard("R1/localhost:27058")`.

1.2. Definir una Clave para Implementar Sharding

La clave de _sharding_ debe elegirse basándose en los patrones de consulta esperados. Para la colección `HistoriaSocio` en la base de datos `GestionClub`, una clave adecuada para la distribución y el rendimiento de las búsquedas podría ser el identificador del socio.

**Clave de Sharding definida:** `idSocio: 1` (Particionamiento basado en rangos, o se podría aplicar _hash_ para una distribución uniforme si los IDs son secuenciales).

1.3. Implementar Sharding en

1. **Habilitar Sharding para la Base de Datos:**

    ◦ Conectarse al Mongo S y ejecutar: `sh.enableSharding("GestionClub")`.

2. **Crear Índice de Sharding:** Se debe crear un índice en la colección con la clave de _sharding_ deseada antes de particionar.

    ◦ `use GestionClub`

    ◦ `db.HistoriaSocio.createIndex({ idSocio: 1 })`.

3. **Particionar la Colección:**

    ◦ `sh.shardCollection("GestionClub.HistoriaSocio", { idSocio: 1 })`.

1.4. Configurar un Segundo ReplicaSet (R2) y Agregarlo al Sharding

1. **Levantar el Replica Set R2:** Se levantan 3 servidores para R2 (ej. 27158, 27159, 27160), utilizando el parámetro `--shardsvr` y `--replSet R2`.

2. **Inicializar R2:** Conectarse a uno de los nodos de R2 e inicializar el Replica Set: `rs.initiate()`.

3. **Agregar R2 al Clúster Shardeado:** Conectarse al Mongo S y agregar R2 como un nuevo _shard_.

    ◦ `sh.addShard("R2/localhost:27158")`.

**Nota:** Al agregar R2, el **Balanceador** comenzará a actuar automáticamente para migrar los _chunks_ de R1 a R2, distribuyendo físicamente los documentos para equilibrar la carga.

1.5 y 1.6. Creación e Inserción de Documentos

1. **Crear Archivo JSON:** Generar un archivo (ej. `historia_socios.json`) con 10,000 documentos que sigan la estructura de `HistoriaSocio` (basado en copias de _inserts_ del TP 5).

2. **Insertar Documentos:** Utilizar `mongoimport` o un _bulk insert_ para cargar los datos a través del Mongo S, lo cual es más eficiente para cargas masivas.

_Ejemplo usando mongoimport (conectándose al puerto 27000 del Mongo S):_

```
mongoimport --host localhost:27000 --db GestionClub --collection HistoriaSocio --file historia_socios.json
```

1.7. Consultar los Chunks Creados y en qué Shard están

Una vez que el Balanceador haya actuado, se puede consultar la metadata en la base de datos `config` a través del Mongo S para ver la distribución de los rangos de datos (_chunks_) entre los _shards_ (R1 y R2).

**Acción Requerida:** Conectarse al Mongo S y consultar la colección `config.chunks`:

```
use config;
db.chunks.find({ ns: "GestionClub.HistoriaSocio" });
```

**Salida esperada (ejemplo):** El resultado mostrará una lista de _chunks_ (rangos lógicos de valores) de la colección, indicando qué _shard_ (`R1` o `R2`) es responsable de cada rango.

• `{ "_id" : "GestionClub.HistoriaSocio-idSocio_MinKey", "ns" : "GestionClub.HistoriaSocio", "min" : { "idSocio" : MinKey }, "max" : { "idSocio" : X }, "shard" : "R1" }`

• `{ "_id" : "GestionClub.HistoriaSocio-idSocio_Y", "ns" : "GestionClub.HistoriaSocio", "min" : { "idSocio" : Y }, "max" : { "idSocio" : MaxKey }, "shard" : "R2" }`

• Si el Balanceador actuó, se vería una distribución que busca ser equitativa en número de _chunks_ entre R1 y R2.

1.8. Definir una Consulta con Explain

Se define una consulta que utiliza la clave de partición (`idSocio`) para asegurar una búsqueda eficiente.

**Consulta de ejemplo (utilizando la clave de sharding):**

```
db.HistoriaSocio.find({ idSocio: 1000 }).explain("executionStats");
```

**Salida esperada del Explain:**

La salida debería indicar que la consulta es eficiente porque el Mongo S pudo dirigir la búsqueda a una **única partición** (_Single Shard_) y realizar un **escaneo de índice** (_Index Scan_).

• **Shard Filtering:** Se esperaría ver `Single Shard` o una indicación de que solo se consultó a `R1` o `R2`.

• **Execution Strategy:** El `winning plan` debería ser `Index Scan`.

• **Contraste:** Si la consulta se realizara sobre una clave que **no** fuera la clave de _sharding_, el _explain_ mostraría un **Shard Merge** y un **Col Scan** (escaneo de colección completo en todos los _shards_), resultando en un proceso mucho más lento.

--------------------------------------------------------------------------------

2. Consistencia

El análisis de consistencia se basa en la arquitectura del clúster _shardeado_ que consta de dos Shards (R1 y R2), cada uno configurado como un Replica Set de 3 servidores.

a) Cuántos nodos tiene el cluster

El cluster _shardeado_ de MongoDB se compone de múltiples servidores (nodos) para diferentes funciones.

• **Nodos de Datos (Shards):** 6 nodos (3 en R1 + 3 en R2).

• **Nodos de Configuración (Config Servers):** Aunque para un laboratorio se puede usar un solo nodo, para una arquitectura robusta y con quórum (como se espera para un sistema distribuido), se recomienda un Replica Set de 3 nodos (ej. PSA o PSS).

• **Nodos de Enrutamiento (Mongo S):** Al menos 1 nodo, pero para evitar un _Single Point of Failure_ (SPOF), se recomienda tener varios.

Considerando una arquitectura mínima funcional para la metadata y los datos:

El clúster tiene **al menos 10 componentes** (Config Servers: 3, Mongo S: 1, Shard R1: 3, Shard R2: 3). Si nos referimos solo a los **nodos que contienen datos de la colección particionada**, el cluster tiene **6 nodos** (los 3 nodos de R1 y los 3 nodos de R2).

b) Cuál es el valor de N

El parámetro **N** se refiere a la cantidad de réplicas definidas para una operación exitosa en un clúster. **N no es la cantidad total de nodos del clúster**.

Dado que R1 y R2 son Replica Sets de 3 servidores cada uno, el factor de replicación (`N`) para las operaciones de lectura o escritura en cualquier _shard_ es .

c) Cuál sería una configuración adecuada de R y W para favorecer la consistencia de escritura y garantizando lecturas más rápidas

Para favorecer la **consistencia de escritura** y garantizar **lecturas más rápidas**, se debe priorizar una W alta y una R baja.

• **W (Write Concern):** Debe ser la mayoría de los nodos del Replica Set para garantizar la consistencia fuerte en la escritura. Dado que N=3, el quórum es N/2+1=2.

    ◦ Configuración recomendada: o, preferiblemente, .

• **R (Read Concern):** Puede ser baja, ya que la alta consistencia de escritura asegura que el dato replicado es consistente.

    ◦ Configuración recomendada: (lectura del primario o el nodo local).

**Justificación:** Al usar W≥majority, nos aseguramos de que el dato esté grabado de forma sincrónica en la mayoría de los nodos antes de confirmar la operación. Esto garantiza que cualquier lectura posterior (R=1) encontrará la versión más reciente, haciendo que las lecturas sean rápidas y, a la vez, consistentes (consistencia fuerte en escrituras).

d) ¿Debería variar esta configuración para reforzar la consistencia de lectura? Si la respuesta es afirmativa, indicar cómo.

**Sí**, la configuración debería variar para reforzar la consistencia de lectura.

• **Variación Requerida:** Aumentar el parámetro de lectura (R).

• **Configuración Recomendada:** o .

**Justificación:** Un valor alto de R obliga al sistema a consultar más nodos de forma sincrónica (dos en este caso). Al utilizar , se asegura que la aplicación lee la versión del dato que ha sido confirmada por la mayoría de los nodos réplica. Esto ofrece un nivel de consistencia de lectura más fuerte, aunque **afecta negativamente el rendimiento** de la lectura debido al costo de consultar múltiples servidores simultáneamente.