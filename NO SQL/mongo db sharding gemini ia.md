# Estructura del Contenido: Bases de Datos NoSQL, Replicación y Sharding en MongoDB

A continuación, he reorganizado y estructurado el contenido proporcionado de la transcripción de la clase impartida por Juan Zaffaroni. He dividido el material en secciones lógicas para mayor claridad, eliminando repeticiones, corrigiendo errores menores de transcripción y resumiendo conceptos clave sin alterar el significado original. El enfoque está en bases de datos NoSQL, escalabilidad, replicación, particionamiento y su implementación práctica en MongoDB (incluyendo replica sets y sharding). He utilizado un formato markdown para facilitar la lectura, con subsecciones, listas y resúmenes.

## 1. Introducción a Bases de Datos NoSQL y Escalabilidad

### Contexto General

- **Problemas con Bases de Datos Relacionales**: Cuando se manejan grandes volúmenes de datos y usuarios concurrentes, las bases de datos relacionales enfrentan limitaciones en un solo servidor (e.g., capacidad de CPU, memoria, almacenamiento). Esto llevó al surgimiento de bases de datos NoSQL, diseñadas para clústeres distribuidos.
- **Concepto de Clúster**: Un grupo de servidores interconectados que actúan como un único recurso de procesamiento. Mejora la escalabilidad, distribución de carga (consultas y escrituras) y disponibilidad 24/7.
- **Diferencias con Bases Antiguas**: A diferencia de bases jerárquicas como Apollo, las NoSQL están optimizadas para clústeres, permitiendo mayor tolerancia a fallos (si un servidor falla, otro toma el relevo).

### Escalamiento Vertical vs. Horizontal

- **Escalamiento Vertical**:
    
    - Añadir más recursos (CPU, RAM, disco) a un solo servidor.
    - Sencillo para bases relacionales y bases de grafos como Neo4j (e.g., en una red social, cada funcionalidad crece individualmente).
    - Limitaciones: Costoso, tiene un techo físico (no se puede escalar indefinidamente).
    
- **Escalamiento Horizontal**:
    
    - Añadir más servidores al clúster (usando servidores más pequeños y rentables).
    - Ideal para NoSQL: Incluye **replicación** (copiar datos en múltiples servidores sin distribuirlos) y **particionamiento** (distribuir datos diferentes en servidores).
    - Arquitecturas comunes:
        
        - **Master-Slave**: Usado por MongoDB y Redis (un maestro coordina esclavos).
        - **Peer-to-Peer**: Usado por Cassandra (todos los nodos son pares, sin jerarquía estricta).
        
    - Beneficios: Maneja grandes datos, alta disponibilidad y distribución geográfica.
    

## 2. Replicación y Particionamiento

### Replicación

- **Definición**: Copia de los mismos datos en múltiples servidores para alta disponibilidad y tolerancia a fallos.
    
    - No distribuye datos (la BD es completa en todos los servidores).
    - Mejora consultas simultáneas (esclavos manejan lecturas), pero solo un nodo (maestro) maneja escrituras.
    
- **Esquema Master-Slave (MongoDB, Redis)**:
    
    - **Nodo Primario (Maestro)**: Único que recibe actualizaciones y consultas de escritura. Garantiza consistencia 100% en escrituras; replica asincrónicamente a secundarios.
    - **Nodos Secundarios (Esclavos)**: Solo lecturas; replican el "oplog" (registro de operaciones del primario).
    - **Conmutación por Error**: Si el primario falla, un secundario se elige automáticamente como nuevo primario (vía quorum). El primario caído se reconecta como secundario.
    - **Problemas Potenciales**:
        
        - No escala escrituras (solo un nodo escribe, puede causar bloqueos).
        - Inconsistencia temporal en lecturas (latencia en replicación).
        - Aplicación a Relacionales: Posible, pero no implica particionamiento real (datos no se distribuyen).
        
    
- **Esquema Peer-to-Peer (Cassandra)**:
    
    - Todos los nodos son iguales; cualquier nodo acepta escrituras y replica a otros.
    - Mejora escalabilidad y disponibilidad, pero requiere manejo cuidadoso de consistencia (e.g., problemas en particiones de red).
    
- **Combinación con Particionamiento**: La más segura para producción (alta disponibilidad + distribución de carga), aunque añade complejidad administrativa.

### Particionamiento (Sharding)

- **Definición**: Distribución de datos diferentes en servidores (cada partición es una BD independiente físicamente, pero lógicamente una sola).
    
    - Permite manejar volúmenes masivos (e.g., datos de sensores que crecen constantemente).
    - No garantiza alta disponibilidad por sí solo (sin redundancia); se combina con replicación.
    
- **Estrategias**:
    
    - **Por Tags Geográficos**: Dirigir datos a servidores específicos (e.g., tag "USA" → servidor USA).
    - **Por Rangos o Hash**: En MongoDB, usa claves de shard.
    - **Consideraciones**:
        
        - Agrupar datos relacionados en la misma partición para consultas eficientes.
        - Evitar particionamiento si los datos caben en un servidor (mayoría de casos usan solo replicación).
        - Costos: Movimiento de datos, latencia geográfica.
        
    
- **Problemas**: Particiones de red pueden causar inconsistencias (inserciones en un lado no se replican al otro).

## 3. Implementación en MongoDB: Replica Sets

### Conceptos Básicos

- **Replica Set**: Conjunto de servidores MongoDB interconectados que actúan como una unidad con redundancia (esquema master-slave).
    
    - **Configuración Mínima**: 1 primario + 1 secundario + 1 árbitro (nodo sin datos que vota en quorum).
    - **Primario**: Solo escrituras; secundarios solo lecturas.
    - **Replicación**: Secundarios copian el oplog del primario. Si primario falla, secundarios eligen nuevo (prioridad por parámetro "priority").
    - **Consistencia vs. Disponibilidad**: Mongo prioriza consistencia; si >50% de nodos fallan (e.g., 2 de 3), se vuelve solo lectura.
    - **Límites**: Hasta 50 réplicas; útil para consultas geográficamente distribuidas.
    
- **Tipos de Nodos**:
    
    - **Árbitro (Arbiter)**: No almacena datos, solo vota para quorum. No requiere licencia Enterprise. Evita problemas en sets de 2 nodos.
    - **Secundario con Delay (Slave Delay)**: Retraso intencional en replicación (útil para recuperación de errores o backups fuera de pico). Nunca primario (priority=0).
    - **Hidden**: Nodos ocultos para backups (priority=0, no visible para clientes).
    - **Build Indexes=False**: No crea índices (ahorra espacio); no puede ser primario.
    
- **Árbol de Replicación**: Secundarios replican de otros secundarios para reducir carga en primario.
- **Latencia**: Problema en transacciones sensibles al tiempo si primario está lejos; aceptable para datos no críticos (e.g., imágenes).

### Configuración Práctica

- **Pasos para Crear un Replica Set**:
    
    1. Levantar instancias MongoDB (e.g., puertos 27058, 27059, 27060; carpetas separadas para datos).
    2. Usar `mongo --replSet R1` para conectar.
    3. En primario: `rs.initiate()` (crea set con un solo nodo primario).
    4. Agregar nodos: `rs.add("host:puerto")` (datos se copian automáticamente).
    5. Verificar: `rs.status()` (muestra primario, uptime, optime como secuenciador).
    
- **Comportamiento en Fallos**:
    
    - Apagar primario → Secundario se elige nuevo (vía votos).
    - Reconexión: Nodo caído entra en resincronización vía oplog.
    - Partición de Red: Nodo sin quorum se vuelve secundario (solo lecturas); en emergencias, convertir a standalone y recrear set.
    
- **Conexión de Clientes**: No a IP individual, sino al replica set (balanceador implícito).
- **Recomendaciones**: PSS (Primary-Secondary-Secondary) como mínimo; PSA (con árbitro) viable si costos son un issue, pese a advertencias de docs.

### Caso Práctico

- Importar datos (e.g., 30k facturas con `mongoimport`).
- Demostración: Inserciones en primario se replican automáticamente; fallos simulan conmutación.

## 4. Sharding en MongoDB

### Conceptos Básicos

- **Sharding**: Particionamiento de colecciones específicas (no toda la BD). Replica BDs completas, pero shards colecciones.
- **Componentes Esenciales**:
    
    - **Shards (Particiones)**: Conjuntos de réplicas que almacenan datos (mínimo 2-3 por shard en producción).
    - **Mongos (Enrutadores)**: Proxies que leen metadatos de config servers y enrutan consultas.
    - **Config Servers**: Replica set especial para metadatos del clúster (mínimo 3 en producción).
    
- **Clúster Productivo**: Mínimo ~10 servidores (shards + config + mongos). Siempre con réplicas para evitar pérdida de datos.
- **Clave de Shard**:
    
    - **Por Rango**: Basado en valores (e.g., fecha); eficiente para consultas de rango, pero desigual distribución.
    - **Por Hash**: Distribución uniforme (aleatoria); bueno para IDs, pero ineficiente para rangos (busca en todo clúster).
    
- **Chunks**: Unidades lógicas de datos (rangos de valores). Tamaño máximo ~64MB (anteriormente 1024MB? – nota: docs actuales recomiendan ~64MB).
    
    - **Splitting**: Divide chunk si excede tamaño (automático).
    - **Balancer**: Reubica chunks entre shards para equilibrio (corre en mongos; desactivar en horarios pico para ahorrar costos).
    

### Configuración Práctica

- **Pasos**:
    
    1. Agregar `--shardsvr` a shards existentes.
    2. Crear config server (e.g., replica set de 1 miembro para demo).
    3. Levantar mongos: `--configdb configReplSet/configHost1:port,...`.
    4. Conectar mongos y agregar shards: `sh.addShard("replSet/host:port")`.
    5. Habilitar sharding: Crear índice en clave de shard; `sh.enableSharding("db")`; `sh.shardCollection("db.collection", {clave:1})`.
    
- **Comportamiento**: Datos se distribuyen en chunks; balancer mueve automáticamente al agregar shards.
- **Ventajas**: Escala horizontal para grandes volúmenes; soporta geodistribución.
- **Consideraciones**: Elegir clave carefully (agrupar datos relacionados); ventana de balanceo para colecciones.

## Preguntas y Respuestas para Exámenes

Basado en el contenido estructurado, he generado 15 preguntas típicas de exámenes (mezcla de conceptuales, comparativas y prácticas). Incluyo respuestas concisas con referencias a secciones. Estas cubren temas clave para preparación (e.g., exámenes universitarios o certificaciones MongoDB). Las preguntas están en español, como la consulta del usuario.

### Preguntas Conceptuales

1. **¿Cuál es la diferencia principal entre escalamiento vertical y horizontal en bases de datos NoSQL?**  
    **Respuesta**: Vertical: Mejora recursos en un solo servidor (sencillo, pero limitado; ideal para relacionales como Neo4j). Horizontal: Añade servidores (usa replicación/particionamiento; escalable para NoSQL como MongoDB). (Sección 1).
    
2. **Explica el esquema Master-Slave en replicación y sus limitaciones.**  
    **Respuesta**: Un primario maneja escrituras (consistente); secundarios replican asincrónicamente para lecturas. Limitaciones: No escala escrituras (bloqueos); inconsistencia temporal. Usado en MongoDB/Redis. (Sección 2).
    
3. **¿Qué es un Replica Set en MongoDB y cuál es su configuración mínima recomendada?**  
    **Respuesta**: Conjunto de servidores interconectados (master-slave) para redundancia. Mínimo: PSS (Primary-Secondary-Secondary) o PSA (con árbitro para quorum). Prioriza consistencia. (Sección 3).
    
4. **Diferencia entre replicación y particionamiento en bases distribuidas.**  
    **Respuesta**: Replicación: Copia datos idénticos (alta disponibilidad, no distribución). Particionamiento: Datos diferentes por servidor (distribución de carga, pero sin redundancia sola). Combinar para producción. (Sección 2).
    
5. **¿Qué rol juega el "árbitro" en un Replica Set de MongoDB?**  
    **Respuesta**: Nodo sin datos que vota en quorum para elegir primario. Asegura decisión en sets impares; no almacena datos, ahorra costos. (Sección 3).
    

### Preguntas Comparativas

6. **Compara los esquemas Master-Slave y Peer-to-Peer en NoSQL.**  
    **Respuesta**: Master-Slave (MongoDB): Jerárquico, solo primario escribe; bueno para consistencia, malo para escalar escrituras. Peer-to-Peer (Cassandra): Todos escriben/replican; mejor escalabilidad, pero riesgos de inconsistencia en redes particionadas. (Sección 2).
    
7. **¿Por qué las bases de datos relacionales no escalan horizontalmente como las NoSQL?**  
    **Respuesta**: Relacionales requieren distribución de datos (particionamiento), pero su ACID estricto complica esto; usan solo replicación master-slave sin partición real. NoSQL diseñadas para clústeres distribuidos. (Sección 1-2).
    
8. **Diferencia entre particionamiento por rango y por hash en sharding de MongoDB.**  
    **Respuesta**: Rango: Eficiente para consultas de rango (e.g., fechas), pero distribución desigual. Hash: Uniforme (aleatoria), bueno para IDs, pero ineficiente para rangos (busca todo clúster). (Sección 4).
    

### Preguntas Prácticas

9. **Describe los pasos para crear un Replica Set en MongoDB con 3 nodos.**  
    **Respuesta**: 1. Levantar mongod con `--replSet R1` en puertos separados. 2. En uno: `rs.initiate()`. 3. Agregar otros: `rs.add("host:puerto")`. 4. Verificar: `rs.status()`. Datos se replican automáticamente. (Sección 3).
    
10. **¿Qué sucede si el primario de un Replica Set falla?**  
    **Respuesta**: Secundarios votan (quorum) para elegir nuevo primario. Nodo caído se resincroniza vía oplog al reconectar. Si >50% fallan, solo lecturas. (Sección 3).
    
11. **Explica el rol de "chunks", "splitting" y "balancer" en sharding de MongoDB.**  
    **Respuesta**: Chunks: Unidades lógicas de datos. Splitting: Divide chunk >64MB. Balancer: Reubica chunks para equilibrio (corre en mongos; desactivar en picos). (Sección 4).
    
12. **¿Cómo se configura un clúster sharded en MongoDB? Menciona componentes clave.**  
    **Respuesta**: 1. Config servers (replica set para metadatos). 2. Mongos (enrutadores). 3. Shards (réplicas). Pasos: `sh.addShard()`, `sh.enableSharding("db")`, `sh.shardCollection()`. (Sección 4).
    
13. **¿Qué es "slave delay" en MongoDB y para qué sirve?**  
    **Respuesta**: Retraso intencional en replicación de un secundario (e.g., horas). Útil para recuperación de errores/eliminaciones accidentales o backups fuera de pico. Nodo nunca primario. (Sección 3).
    
14. **En un escenario de partición de red, ¿qué pasa con un nodo primario en MongoDB?**  
    **Respuesta**: Si pierde quorum, se vuelve secundario (solo lecturas). En emergencias (e.g., centro caído), convertir a standalone y recrear set. (Sección 3).
    
15. **¿Por qué se recomienda desactivar el balancer en horarios pico en sharding?**  
    **Respuesta**: Mueve datos entre shards (costoso en I/O y latencia). Configurar ventana de balanceo para noches/fines de semana. (Sección 4).
    

Estas preguntas cubren ~80% del contenido y pueden usarse para autoevaluación. Si necesitas más detalles, variaciones o foco en un sub-tema (e.g., solo sharding), ¡házmelo saber! El código "yha-fttz-sqo" no parece relevante al contenido; si es un ID de examen, avísame para buscar recursos específicos.