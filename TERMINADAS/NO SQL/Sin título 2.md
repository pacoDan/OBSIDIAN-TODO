La implementación de la replicación y el _sharding_ en MongoDB requiere configurar varios componentes que trabajan juntos para lograr la distribución de datos y la alta disponibilidad. MongoDB es una base de datos de tipo CP (Consistencia y Tolerancia a Particiones), priorizando la consistencia por encima de la disponibilidad absoluta.

A continuación, se detalla el proceso de implementación de un _Replica Set_ (Conjunto de Réplicas) y posteriormente la configuración del _Sharding_ para la colección `HistoriaSocio` en la base de datos `GestionClub`, siguiendo los pasos solicitados.

---

## FASE 1: Implementación de Replicación (Replica Set R1)

La replicación en MongoDB se realiza mediante un _Replica Set_ (RS), un conjunto de servidores (nodos) donde uno es el `Primary` (Maestro) y los demás son `Secondaries` (Esclavos). El nodo Primary es el único que acepta operaciones de escritura.

Para este ejemplo, utilizaremos el **Replica Set R1** con tres nodos, simulando que están en los puertos `27058`, `27059` y `27060`.

### 1. Iniciar los Servidores Mongod

Se utiliza el comando `mongod` agregando el parámetro `--replSet` para indicar a qué conjunto de réplicas pertenecerá cada instancia.

|Nodo|Puerto|Comando de inicio (Ejemplo)|
|:--|:--|:--|
|**N1**|`27058`|`mongod --replSet R1 --port 27058 --dbpath /data/A1`|
|**N2**|`27059`|`mongod --replSet R1 --port 27059 --dbpath /data/A2`|
|**N3**|`27060`|`mongod --replSet R1 --port 27060 --dbpath /data/A3`|

### 2. Iniciar el Replica Set

Conectándose al puerto del primer nodo (`27058`), se inicializa el conjunto de réplicas.

```
mongosh --port 27058
rs.initiate({
  _id: "R1",
  members: [
    { _id: 0, host: "127.0.0.1:27058" }
  ]
})
```

Una vez ejecutado, el nodo en `27058` se convierte en el `Primary`.

### 3. Agregar los Nodos Secundarios

Se agregan los nodos restantes al Replica Set R1, utilizando el comando `rs.add()`.

```
rs.add("127.0.0.1:27059")
rs.add("127.0.0.1:27060")
```

Tras la adición, los nodos secundarios replican los datos del `Primary` de manera asincrónica.

### 4. Verificar el Estatus

El comando `rs.status()` muestra que el conjunto de réplicas está activo, indicando cuál es el `Primary` y cuáles son los `Secondaries`.

---

## FASE 2: Implementación de Sharding en BD MongoDB

El _sharding_ (particionamiento) se implementa dividiendo la base de datos en partes más pequeñas (colecciones específicas) y distribuyéndolas en múltiples _Replica Sets_ (Shards), coordinados por un servidor de configuración y un enrutador (Mongo S).

### 1. Componentes del Clúster Shardeado

Se necesitan levantar al menos tres componentes clave para el _Sharding_ en un entorno de prueba:

1. **Shards (R1 y R2):** Los Replica Sets que almacenarán los datos.
2. **Config Servers (RS_CON):** Un Replica Set que contiene la _metadata_ del clúster.
3. **Mongo S (Proxy/Router):** La interfaz a la que se conectan las aplicaciones.

#### a. Configurar Replica Set R1 como Shard Server

Los nodos de R1 deben reiniciarse (o levantarse inicialmente) con el parámetro `--shardsvr`:

```
mongod --replSet R1 --port 27058 --dbpath /data/A1 --shardsvr
# Repetir para 27059 y 27060
```

#### b. Levantar y Configurar el Config Server (RS_CON)

Se levanta un nodo y se inicia como un Replica Set de Configuración.

```
# 1. Iniciar el nodo de Configuración (ej. puerto 27500)
mongod --configsvr --replSet RS_CON --port 27500 --dbpath /data/config

# 2. Conectarse e iniciar el Replica Set RS_CON
mongosh --port 27500
rs.initiate({ _id: "RS_CON", members: [{ _id: 0, host: "127.0.0.1:27500" }] })
```

#### c. Levantar el Enrutador Mongo S

El enrutador Mongo S (un binario diferente) se levanta apuntando al Replica Set de Configuración (RS_CON):

```
# Se levanta en el puerto 27000 (ejemplo, o 27017 por defecto)
mongos --configdb RS_CON/127.0.0.1:27500 --port 27000
```

#### d. Conectar el Replica Set R1 al Sharding

Conectándose a través del Mongo S (proxy), se agrega R1 como la primera partición (_shard_) del clúster.

```
mongosh --port 27000
sh.addShard("R1/127.0.0.1:27058")
```

### 2. Definir Clave e Implementar Sharding en HistoriaSocio

El _sharding_ se realiza sobre colecciones específicas. En este caso, sobre `GestionClub.HistoriaSocio`.

#### a. Definir Clave de Sharding

Se define una clave compuesta basada en el ID del socio y la fecha del evento (`id_socio` y `fecha_evento`), lo que permite el _sharding_ basado en rangos:

```
use GestionClub
// 1. Crear el índice en la colección HistoriaSocio
db.HistoriaSocio.createIndex({ id_socio: 1, fecha_evento: 1 })
```

#### b. Habilitar Sharding en la Base de Datos y Colección

```
// 2. Habilitar el sharding para la base de datos GestionClub
sh.enableSharding("GestionClub")

// 3. Implementar el sharding en la colección HistoriaSocio
sh.shardCollection("GestionClub.HistoriaSocio", { id_socio: 1, fecha_evento: 1 })
```

Este paso crea la _metadata_ de los **Chunks** (rangos lógicos de valores) en el Config Server, aunque los datos permanecen en R1.

> **Nota sobre el tamaño de Chunk:** El tamaño por defecto del _chunk_ es de 1024 MB. Para generar más _chunks_ lógicos para la distribución en un entorno de prueba, se puede reducir este tamaño a 5 MB, insertando un documento en la colección `config.settings`: `use config` `db.settings.insertOne({ _id: "chunksize", value: 5 })`

### 3. Configurar y Agregar el Segundo Replica Set (R2)

Se configura un segundo Replica Set (R2) con 3 servidores, el cual se agregará como un _shard_ adicional.

#### a. Iniciar los Servidores de R2

Se levantan los nodos de R2 (ej. puertos 27158, 27159, 27160), configurados como _shard servers_:

```
mongod --replSet R2 --port 27158 --dbpath /data/B1 --shardsvr
# Repetir para 27159 y 27160
```

#### b. Iniciar e Integrar R2 al Clúster

```
# 1. Conectarse a 27158 e inicializar R2
mongosh --port 27158
rs.initiate({ _id: "R2", members: [...] })

# 2. Conectarse al Mongo S (proxy en 27000)
mongosh --port 27000

# 3. Agregar R2 como un nuevo shard
sh.addShard("R2/127.0.0.1:27158")
```

Al agregar R2, el **Balancer** (Balanceador) se activa automáticamente y comienza a mover físicamente los documentos de los _chunks_ del R1 hacia el R2 para equilibrar la carga.

### 4. Crear Archivo JSON e Insertar Documentos

Se simula la creación y la inserción de 10,000 documentos. Es importante realizar la inserción a través del **Mongo S** (proxy) para que el enrutador distribuya las escrituras según la clave de _sharding_.

#### a. Creación y Carga (Ejemplo)

```
# Suponiendo que 'historia_socio_10000.json' contiene 10,000 documentos
mongoimport --port 27000 --db GestionClub --collection HistoriaSocio --file /ruta/a/historia_socio_10000.json
```

### 5. Consultar los Chunks Creados y su Ubicación

Para ver cómo se distribuyeron los rangos lógicos (_chunks_), se consulta la colección `chunks` en la base de datos `config`.

```
mongosh --port 27000
use config

// Consultar los chunks para la colección particionada
db.chunks.find({ ns: "GestionClub.HistoriaSocio" })
```

La salida mostrará el rango de la clave de _sharding_ para cada _chunk_ y el _shard_ (`R1` o `R2`) al que está asignado, demostrando que la colección ahora está distribuida.

### 6. Definir Consulta e Informar la Salida del Explain

La eficiencia de la consulta depende de si se utiliza la **clave de partición** (`id_socio` y `fecha_evento`).

#### a. Consulta Rápida (Utilizando la Clave de Partición)

Se busca un historial específico utilizando la clave de _sharding_. El Mongo S puede dirigir la consulta a un solo _shard_.

```
db.HistoriaSocio.find({
    id_socio: 500,
    fecha_evento: { $gte: ISODate("2023-01-01T00:00:00Z") }
}).explain("executionStats")
```

**Salida del Explain (Ejemplo esperado):** La salida indicará un `winningPlan` con **`SINGLE_SHARD`** y **`INDEX_SCAN`**.

- **`Sharding Filter`**: Aplicado.
- **`Query Plan`**: Muestra que la búsqueda se realizó en un **`Single Shard`** (un solo _shard_) y utilizó el índice de la clave de _sharding_ (Index Scan), resultando en una operación muy rápida.

#### b. Consulta Lenta (Sin Utilizar la Clave de Partición)

Se busca por un campo que no forma parte de la clave de _sharding_ (ej. `monto_compra`). El sistema debe buscar en todas las particiones.

```
db.HistoriaSocio.find({ monto_compra: { $gt: 5000 } }).explain("executionStats")
```

**Salida del Explain (Ejemplo esperado):** La salida indicará **`SHARD_MERGE`** y **`COLLSCAN`**.

- **`Sharding Filter`**: No pudo optimizar el filtro.
- **`Query Plan`**: Muestra un **`Shard Merge`**, lo que significa que tuvo que buscar en todos los _shards_ (`R1` y `R2`). Dentro de cada _shard_, realizó un **`COLLSCAN`** (escaneo completo de la colección), lo cual es ineficiente y mucho más lento.