https://youtu.be/ANOW6sd1xjU
El siguiente es un análisis estructurado de la transcripción, recopilando los puntos clave, las lecciones aprendidas y las preguntas/respuestas del examen (8x8), con especial énfasis en el material de "Persistencia Políglota".

--------------------------------------------------------------------------------

I. Conceptos y Lecciones Aprendidas de Persistencia Políglota

La clase se centró en el concepto de Persistencia Políglota, que surge de la necesidad de utilizar diferentes motores de bases de datos para resolver las distintas necesidades de una plataforma, en lugar de forzar todos los casos de uso a un único motor.

A. Fundamentos y Definición

• **Persistencia Políglota:** Se refiere a la práctica de emplear múltiples motores de persistencia o "idiomas" de bases de datos para gestionar las diversas necesidades de almacenamiento de una plataforma.

• **Origen Conceptual:** La idea se basa en el concepto de **Programación Políglota**, propuesto por Neal Ford en 2006, que sugiere escribir aplicaciones en un _mix_ de lenguajes para aprovechar las fortalezas de cada uno en diferentes problemas.

• **Referentes:** Martin Fowler es destacado como uno de los fundadores o impulsores de esta idea en el ámbito de la persistencia.

• **Justificación:** Un solo motor relacional (aunque es un buen caballo de batalla) puede volverse subóptimo o penalizado, especialmente en el nodo principal (_writer_ o _primary_), cuando se le cargan operaciones diversas (ej. gestión de sesión, reportes, órdenes).

B. Aplicación en Casos de Uso (E-commerce Ejemplo)

El enfoque políglota sugiere **separar los casos de uso por funcionalidad**.

|   |   |   |
|---|---|---|
|Funcionalidad o Dato|Tipo de Persistencia Recomendada|Justificación/Ejemplo|
|**Datos de Sesión y Caché**|Key Value Store (In-memory, ej. Redis)|Necesitan alta disponibilidad y la simpleza de recuperar valores por clave. Evita estresar al motor relacional principal con escrituras de sesión menos críticas.|
|**Órdenes Completadas**|Document Store (ej. MongoDB)|Adecuado para escalar masivamente y manejar estructuras de datos variables.|
|**Inventario y Precios (Legacy)**|Relacional|Los productos e inventario difícilmente escalan de manera masiva, siendo apropiado para el legado si no requiere un rendimiento extremo.|
|**Grafo Social de Clientes/Recomendaciones**|Base de Datos de Grafos (Graph, ej. Neo4j)|Optimiza las operaciones de relaciones, _joins_ autorreferenciados y la búsqueda del camino más óptimo (ej. ruteo).|
|**Indexación y Búsqueda**|Motores de Búsqueda (ej. Solr, Elastic Search)|Funcionan como caché o motor de búsquedas eficientes.|
|**Financiero / Facturación / Banca**|Relacional|Priorizan la **consistencia** (propiedades ACID).|
|**Telemetría / Time Series / Logs**|Column Family (ej. Cassandra) o Documental|Capaces de manejar escrituras masivas a escalas gigantes; el modelo documental se adapta a estructuras de _logs_ variantes.|

C. Lecciones Aprendidas y Consideraciones Profesionales

Al implementar la persistencia políglota, es crucial evaluar múltiples aristas (como un _checklist_):

1. **Criterio Uténiano (Inteligencia sobre Fanatismo):** La implementación debe ser justificada por necesidades intensivas de procesamiento y no solo por moda. Se debe medir y considerar la naturaleza de cada proyecto.

2. **Pruebas de Concepto (POC):** Instalar el motor, cargarlo con datos realistas, replicar consultas, medirlas y hacer _tests_ de carga para comparar con la solución existente.

3. **Monitoreo y Operaciones (Ops):** Pensar en quién se hará cargo del monitoreo en producción (performance, _queries_ colgadas, caídas). Se pueden usar servicios de nube como Cloudwatch (AWS), SNS y _hooks_ de Slack o Pager Duty para alertas.

4. **Costos y Complejidad:** La persistencia políglota multiplica la complejidad y los costos. Es fundamental hacer un análisis de costo-beneficio antes de proponer cambios.

5. **Backup y Restauración:** Analizar las estrategias específicas de backup y restauración de cada motor.

6. **RPO y RTO (Recuperación):** Definir el RPO (_Restore Point Objective_, la pérdida de datos aceptable) y el RTO (_Restore Time Objective_, el tiempo máximo para recuperarse y estar online).

7. **Seguridad y Auditoría:** En NoSQL, la seguridad tradicionalmente yace en la aplicación. Sin embargo, soluciones _Enterprise_ o servicios gestionados (ej. Elastic Cache de AWS) ofrecen características como **Encryption at Rest** (cifrado en disco) y **Encryption in Flight** (TLS/SSL para el tráfico de ida y vuelta).

8. **Drivers y Lenguajes:** Verificar que existan _drivers_ de calidad, bien mantenidos y seguros para todos los lenguajes de programación utilizados por el equipo (en el contexto de programación políglota).

9. **Despliegue y Mantenimiento:** El despliegue se multiplica (podrías tener cinco _clusters_ en producción en lugar de uno). También se debe considerar el ritmo de actualizaciones del motor y la posibilidad de _Breaking Changes_.

10. **Capacidad del Equipo:** La elección del motor también depende de cuán capaz esté el equipo de adoptar y mantener la nueva tecnología.

--------------------------------------------------------------------------------

II. Preguntas y Respuestas del Examen (8x8)

Durante la clase, se realizó un ejercicio "8x8" para consolidar ideas.

|   |   |   |   |
|---|---|---|---|
|Nro|Pregunta|Tipo|Respuesta y Justificación|
|**1**|¿Por qué utilizar un único motor de base de datos para la totalidad de una aplicación puede dar soluciones de bajo rendimiento?|Desarrollo|**Respuesta:** Porque cada motor está diseñado para un tipo de caso de uso especial. Forzar todos los casos de uso a un mismo esquema genera consultas ineficientes que utilizan más recursos de hardware y resultan en problemas de escalabilidad.|
|**2**|Persistencia políglota se llama al uso de diferentes motores de base de datos NoSQL para resolver diferentes problemas de una aplicación. Las RDBMs no son consideradas.|Verdadero/Falso|**Falso**. Cualquier motor de persistencia, incluidas las bases de datos relacionales (RDBMs), es bienvenido si agrega valor a la plataforma y resuelve el caso de uso.|
|**3**|Por lo general, en los sistemas con persistencia políglota, la seguridad yace en la aplicación.|Verdadero/Falso|**Verdadero**. Históricamente, en los comienzos de NoSQL, la seguridad se delegaba a la capa de aplicación, ya que los motores se enfocaban en la resolución del caso de uso principal. Aunque las bases de datos modernas están incorporando más seguridad, la afirmación se sostiene como regla general.|
|**4**|Antes de realizar un desarrollo en una nueva tecnología de bases de datos, hay que evaluar si es que existen:|Múltiple Opción|**Todos**: necesidades intensivas de procesamiento que justifiquen la nueva tecnología, la forma de acceso a los datos, y verificar que la tecnología esté probada y tenga buen soporte.|
|**5**|Siempre que se pueda hay que utilizar persistencia políglota.|Verdadero/Falso|**Falso**. La implementación depende siempre del contexto, la complejidad, el costo y la justificación real del proyecto.|
|**6**|¿Qué motor utilizaría para implementar un sistema CDN (Content Delivery Network)?|Opción Múltiple|**Key Value Store**. Es la mejor opción dada la simpleza de recuperar un valor (contenido estático) por una clave (URL).|
|**7**|¿Qué motor utilizaría para implementar un sistema que permita consultar qué medio de transporte tomar para viajar de un punto a otro de la ciudad?|Opción Múltiple|**Graph** (Base de Grafos). Este motor facilita el recorrido del gráfico y la búsqueda del camino más óptimo (ruteo).|
|**8**|¿Qué motor utilizaría para implementar un sistema de votación electrónica, donde los resultados se publican al día siguiente de la elección?|Opción Múltiple|**Relacional**. La clave está en que es un caso de uso sensible donde la **consistencia** es la prioridad.|

--------------------------------------------------------------------------------

III. Conceptos Adicionales de Consistencia y Sharding (MongoDB)

Aunque el enfoque principal del examen es la persistencia políglota, la transcripción también cubre en detalle la consistencia y el _sharding_ en NoSQL, especialmente en MongoDB.

A. Consistencia en Sistemas Distribuidos y Teorema CAP

• **Consistencia vs. Integridad:** La consistencia es la corrección de los datos según la lógica de negocio, mientras que la integridad garantiza reglas referenciales y de entidad automáticas.

• **Teorema CAP:** Un sistema distribuido solo puede garantizar dos de estas tres propiedades simultáneamente: Consistencia, Disponibilidad, y Tolerancia a Particiones de red. No existe un motor de base de datos que cumpla absolutamente las tres.

• **Modelos de Consistencia:**

    ◦ **CA (Consistencia y Disponibilidad):** Bases relacionales, Neo4j.

    ◦ **CP (Consistencia y Tolerancia a Particiones):** MongoDB, HBase.

    ◦ **AP (Disponibilidad y Tolerancia a Particiones):** Cassandra (consistencia eventual).

• **Consistencia Eventual:** Los datos pueden ser inconsistentes al momento de la escritura (_momento cero_), pero eventualmente alcanzarán la consistencia.

B. Configuración de Réplicas (N, W, R)

• **N (Réplicas):** Cantidad de réplicas necesarias para una operación exitosa, que no es la cantidad total de nodos.

• **W (Write Concern):** Define cuántas copias deben grabarse sincrónicamente para que la operación de escritura se considere exitosa. Una W alta garantiza mayor consistencia, pero puede afectar la velocidad y disponibilidad. Se puede usar el valor **majority** en lugar de un número específico.

• **R (Read Concern):** Define cuántos nodos deben ser consultados sincrónicamente en una lectura. Una R alta ofrece una consistencia de lectura más fuerte pero afecta el rendimiento.

• **Consistencia por Quórum:** Se busca un nivel de consistencia verificando la escritura en una mayoría de nodos, típicamente la mitad más uno (n/2+1).

C. Características de MongoDB

• **Write Concern y Journaling:** Por defecto, el `write concern` (W) es 1 (solo el _primary_ confirma). El parámetro `J: true` (journal en true) asegura que los datos se graben primero en un registro transaccional en disco (journal) antes de la confirmación a la aplicación.

• **Validación de Esquemas:** A partir de Mongo 3.2, permite controlar el modelo de datos (_schemaless_). Se usan dos propiedades:

    ◦ `validationAction`: Puede deshabilitar la validación, emitir una advertencia (_warn_), o causar un error (_error_).

    ◦ `validationLevel`: Puede ser _strict_ (aplica reglas a todas las inserciones y modificaciones) o _moderate_ (aplica restricciones solo a inserciones y documentos que ya cumplen).

• **Transacciones:** Implementadas a partir de Mongo 4.x, incluyendo `start transaction`, `commit transaction` y `abort transaction`.

• **Read Concern:** Niveles como _majority_ (garantiza datos recientes escritos en la mayoría de nodos) y _Nearest_ (lee del nodo con menor latencia, útil en clústeres distribuidos geográficamente).

D. Sharding y Distribución de Datos

• **Configuración:** Requiere levantar un _config server_ (que es un réplica set) y un proceso **Mongo S** (un binario diferente) que apunta al servidor de configuración para mapear los metadatos. Los nodos de réplica set deben incluir el parámetro `--shardsvr`.

• **Proceso de Sharding:** Primero se crea un índice con la clave de _sharding_, y luego se usa el comando `shardCollection`.

• **Chunks:** Son rangos de valores que mapean los datos. Su tamaño por defecto es de 1024 megas y se puede modificar en la colección `config.settings`.

• **Consultas Particionadas:** Una búsqueda con la clave de partición es muy rápida (_index scan_), ya que detecta que los datos están en una sola partición. Una búsqueda sin la clave de partición es mucho más lenta, ya que requiere buscar en todas las particiones (_shard merge_ y _colscan_).

• **Balanceador (Balancer):** Mueve los datos entre particiones (_shards_) para mantener un equilibrio. El _balancer_ puede configurarse para funcionar en una ventana de tiempo específica por base de datos o colección, o inhabilitarse. Durante la migración de datos, las consultas impactan el dato original, priorizando Mongo las consultas sobre el balanceo.