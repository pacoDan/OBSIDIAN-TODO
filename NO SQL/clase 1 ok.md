## Estructura de la Transcripción y Detalles sobre Bases de Datos NoSQL

### I. Presentación de la Materia y Docentes

- **Docentes:**
    
    - Juan Safaroni (Ingeniero en Sistemas de UTN, dando clases desde 1991, socio y dueño de una empresa de Big Data Analytics).
    - Santiago Villarreal (Ingeniero en Sistemas, recibido en 2013, con experiencia en desarrollo Java, liderazgo de proyectos y AWS Cloud Engineer, con implementaciones de NoSQL como Redis, MongoDB, DynamoDB).
    
- **Creación y Evolución de la Materia:**
    
    - Creada en 2014.
    - Ajustes y mejoras anuales en bases de datos trabajadas, versiones y cambio de bases de datos (ej. de Rayak a Redis).
    
- **Objetivo de la Materia:** Que los estudiantes vean las bases de datos NoSQL, que se clasifican en cuatro tipos:
    
    - Documentales
    - Column Family
    - Key-Value
    - Grafos
    

### II. Metodología de Clases y Evaluación

- **Estructura de Clases por Tipo de Base de Datos:**
    
    - Inicialmente, dos clases por cada tipo de base de datos:
        
        - Una clase de CRUD (Create, Read, Update, Delete/Insert, Select).
        - Una clase de Arquitectura.
        
    - **Importante:** Los lenguajes de consulta en NoSQL no usan SQL (Not SQL), aunque algunos como Cassandra pueden usarlo. Generalmente, cada base de datos tiene su propio lenguaje.
    
- **Base de Datos Principal:**
    
    - MongoDB es la base de datos más fuerte, completa y la que se verá para las bases de datos documentales.
    - Muchos temas "cross" a todas las bases de datos (consistencia, replicación, sharding, persistencia políglota, agregaciones, modelado) se verán con ejemplos en MongoDB.
    
- **Bases de Datos a Estudiar:**
    
    - MongoDB (rojo, para documentales)
    - Redis (celeste, para Key-Value)
    - Cassandra (para Column Family)
    - Neo4j (para Grafos)
    
- **Actividades en Clase:**
    
    - **8x8:** Cuestionario de 8 preguntas en 8 minutos, contestado en Google Form en grupos. Puede ser sobre la clase anterior o la actual.
    - **Trabajos Prácticos (TPs):**
        
        - Nueve TPs en total, cubriendo todos los temas.
        - Requiere instalar Docker, Redis, Cassandra, etc.
        - **TP8 (Investigación):**
            
            - Doble nota: trabajo hecho y presentación en clase (30-40 minutos por grupo con demo del producto).
            - Investigar tres productos (generalmente bases de datos NoSQL no vistas) y compararlas con las vistas.
            
        
    
- **Evaluación:**
    
    - **Parcial:**
        
        - Estilo certificación.
        - 30 preguntas (multiple choice, verdadero/falso con justificación, algunas para escribir).
        - 60% de preguntas: repaso de lo visto en clase.
        - 20% de preguntas: más prácticas (ej. identificar queries correctas, ordenar comandos).
        - 20% de preguntas: para "florearse" y promocionar con excelencia (todo visto en clase).
        
    - **Promoción:** Parcial (8 o más) O Primer Recuperatorio (8 o más) + Promedio de TPs + 8x8. La nota final debe ser 8 o más.
    - **Examen Final (si no se promociona):** Cuatro preguntas a desarrollar sobre temas de la cursada (teórico, sin práctica).
    

### III. Cronograma y Temas Clave (Ejemplo del Cuatrimestre Pasado)

- **Clase 1 (Hoy):** Presentación de la materia, docentes, estudiantes, Unidad 1 (Surgimiento y Conceptualización de Bases NoSQL).
- **Clase Siguiente:** Modelado en bases NoSQL y clase de Redis.
- **Posteriores Clases:**
    
    - Column Family (Cassandra).
    - Datos de MongoDB.
    - Neo4j.
    - Estas primeras cinco clases se centran en el CRUD de cada base de datos.
    
- **Temas "Cross" (Práctica en MongoDB):**
    
    - Modelos de distribución de datos (en varios servers).
    - Replicación de datos (asincrónica).
    - Sharding (distribución de datos).
    - Persistencia políglota (aplicación que interactúa con diferentes tipos de bases de datos).
    - Presentación de casos de negocio (experiencias reales con diferentes bases de datos).
    - Consistencia de datos (trabajando sobre MongoDB).
    
- **Clases Avanzadas por Base de Datos:**
    
    - Clase 2 de Cassandra.
    - Clase 2 de Neo4j y Redis (más cortas, en una misma clase).
    
- **Conceptos Adicionales:**
    
    - Procesos distribuidos (Hadoop, MapReduce).
    - Plataformas analíticas complejas (Hadoop y sus implementaciones en la nube).
    
- **Después del Parcial:**
    
    - Exposición del TP8.
    - Clase de bases de datos en la nube, ETLs y ELTs (si el tiempo lo permite, sino grabación).
    
- **Recuperatorios:** Primer y segundo recuperatorio.
- **TPs por Clase (Ejemplos):**
    
    - TP de modelo en Redis.
    - TP de Cassandra.
    - TP de MongoDB.
    - TP de Neo4j.
    - TP de replicación en MongoDB.
    - TP de persistencia políglota (en clase).
    - TP de Sharding en MongoDB.
    - TP de investigación de producto.
    - TP de Aggregation Framework.
    
- **Importancia de MongoDB:** Es la base de datos NoSQL número uno del mercado, por lo que tiene más práctica.

### IV. Experiencias de los Estudiantes con Bases de Datos NoSQL

- **Agustín:** Desarrollador en Eudimonia, usa MongoDB y Redis a través de librerías, busca entender el modelado correcto y queries específicas.
- **Alan Risncker:** Ciberseguridad en un banco (ACC), poca experiencia con bases de datos, pero le interesó la materia.
- **Carlos Deiderio:** Trabaja en MercadoLibre (Backend), usa bases de datos relacionales con abstracción, busca profundizar en NoSQL. Trabaja con Java, Kotlin, Go.
- **Ezequiel Alfonso:** Administrador de bases de datos en PCR (Postgres, MySQL), implementó Redis para manejar sesiones (Docker). Busca entender la analogía y administración de clústeres, sharding, memoria, etc.
- **Gonzalo Pardo Rodríguez:** Analista e ingeniero de datos en una empresa pequeña, no ha trabajado con NoSQL más allá de object storage. Interesado en el mundo NoSQL.
- **Juan Manuel:** Programador Backend en un banco, usa una base de datos NoSQL propietaria tipo objeto (posiblemente Hydra).
- **Julián Pandulo:** Desarrollador Frontend (accesibilidad web), experiencia previa con relacionales. Interesado en NoSQL porque su empresa (seguridad de hogar) está migrando a estas tecnologías.
- **Genti:** En búsqueda de trabajo como desarrollador Java, solo ha usado bases de datos no relacionales. Usó MongoDB en un TP de diseño de sistemas. Busca un marco de referencia para el mercado laboral.
- **León Reinosa:** Desarrollador Backend en PedidosYa (Kotlin), usa bases de datos NoSQL (Key-Value y documentales): Redis y DynamoDB (en AWS). Busca entender mejor el mundo NoSQL para aplicarlo en el trabajo.
- **Luca Cuenca:** DevOps en una startup. Busca tener más referencia para elegir entre SQL y NoSQL en proyectos, y entender conceptos de clúster, escalabilidad horizontal/vertical.
- **Martín:** Desarrollador en la secretaría de la facultad (Postgres, JavaScript, Next.js). Interesado en profundizar en bases de datos no relacionales.
- **Matías Buch:** Desarrollador Backend (Java, .NET, Delphi, JavaScript en Frontend). Siempre usó bases de datos relacionales (SQL Server, MySQL, Postgres). Poca experiencia con NoSQL (solo para trabajos de la facultad).
- **Maximiliano Fiandrino:** Desarrollador Backend en Despegar (Java). Tuvo que usar Cassandra y Redis con ayuda de ChatGPT y documentación, busca entender más a fondo.
- **Nelson Molineri:** Desarrollador en UNREF (Laravel PHP). Usó Rayak y MongoDB en otros TPs, busca profundizar.
- **Nicolás Ledesma:** Desarrollador Full Stack (View, React, Angular, Java en Backend), migrando a líder de desarrollo. Su empresa usa solo SQL (Hibernate, procedimientos), busca implementar NoSQL.
- **Nico Rosa:** Analista de datos y desarrollador Backend, siempre en bases de datos relacionales. Poca relación con NoSQL, le generó curiosidad.

### V. Preguntas y Respuestas Clave para Exámenes (Enfocado en NoSQL)

- **¿Cuáles son los cuatro tipos principales de bases de datos NoSQL que se verán en la materia?**
    
    - Documentales, Column Family, Key-Value, y de Grafos.
    
- **¿Qué base de datos NoSQL es considerada la más fuerte y completa en la materia, y por qué?**
    
    - MongoDB, porque es la base de datos NoSQL número uno del mercado y se utilizará para la mayoría de las prácticas y para ver temas "cross" como consistencia, replicación y sharding.
    
- **¿Cuál es la principal diferencia en el lenguaje de consulta entre las bases de datos SQL y NoSQL?**
    
    - Las bases de datos NoSQL (Not SQL) generalmente no usan SQL como lenguaje de consulta, sino que tienen su propio lenguaje. Aunque algunas, como Cassandra, pueden tener cierta compatibilidad.
    
- **Mencione al menos tres temas "cross" a todas las bases de datos NoSQL que se abordarán en la materia.**
    
    - Consistencia, replicación, sharding (particionamiento), persistencia políglota, agregaciones, modelado.
    
- **¿Qué es la "persistencia políglota" en el contexto de bases de datos NoSQL?**
    
    - Es la capacidad de una aplicación para interactuar con diferentes tipos de bases de datos (relacionales y NoSQL de distintos tipos) simultáneamente.
    
- **Describa el propósito del "8x8" en la metodología de la materia.**
    
    - Es un cuestionario de ocho preguntas que los estudiantes deben contestar en ocho minutos en un Google Form, en grupos. Sirve para evaluar la comprensión de la clase anterior o la actual.
    
- **¿Qué se espera de los estudiantes en el TP8 de investigación?**
    
    - Investigar y comparar tres productos (generalmente bases de datos NoSQL no vistas en clase) con las bases de datos estudiadas. El trabajo tiene una doble nota: el informe y una presentación en clase con una demo del producto.
    
- **¿Cómo se estructura el parcial de la materia en términos de tipos de preguntas y porcentajes?**
    
    - 30 preguntas tipo certificación (multiple choice, verdadero/falso con justificación, algunas de escritura).
    - 60% de preguntas: repaso de lo visto en clase.
    - 20% de preguntas: más prácticas (ej. identificar queries correctas, ordenar comandos).
    - 20% de preguntas: para excelencia, pero basadas en material visto.
    
- **Mencione al menos dos bases de datos NoSQL específicas que los estudiantes mencionaron haber usado o estar interesados en usar en sus trabajos o proyectos.**
    
    - MongoDB, Redis, Cassandra, DynamoDB, Hydra (propietaria).
    
- **¿Qué concepto importante, además de NoSQL y Big Data, se destaca como "cross" a las aplicaciones escalables y se verá en la materia?**
    
    - Conceptos de clúster, escalabilidad horizontal y vertical, que son comunes a cualquier elemento de una aplicación (servidores web, de aplicaciones, etc.).
    
- **¿Por qué es importante para los estudiantes aprender a elegir la base de datos adecuada (SQL vs. NoSQL) para un proyecto?**
    
    - Para evitar "aberraciones de errores de arquitectura" y "errores de definición de qué base usar", asegurando que la herramienta se use de manera eficiente y correcta para el problema específico.
---
## Transcripción Estructurada: Bases de Datos NoSQL

### **1. Introducción y Evolución de la Tecnología**

- **Cambios en la Tecnología (Últimos 30 años):**
    
    - Arquitecturas de aplicación.
    - Manejo de programación distribuida.
    - Paradigmas de programación.
    - Cambios en lenguajes y su cruce con paradigmas.
    - Herramientas de desarrollo low-code o sin código.
    - Desarrollos a través de internet y distribuidos geográficamente.
    - Componentes que escalan según necesidades de usuarios o volúmenes de datos.
    
- **Constante en el Tiempo:** Los motores de bases de datos relacionales, creados por Edgar Codd en los años 70, siguen vigentes y presentes en todas las empresas.
- **Propósito de NoSQL:** Complementar el mundo de las bases de datos relacionales, no reemplazarlas, cubriendo espacios vacíos y problemas no pensados en los años 70.

### **2. Bases de Datos Relacionales y sus Características**

- **Historia:**
    
    - Edgar Codd definió el modelo relacional y el álgebra relacional en los años 70.
    - IBM lanzó System R (1974).
    - Surgieron Oracle, Progress (competidor de Oracle, luego adquirido por IBM y destruido), DB2, SQL Server (Microsoft, basado en CBASE, luego reescrito).
    - MySQL (adquirido por Oracle), con su escisión MariaDB.
    - PostgreSQL.
    - SQLite (base de datos autocontenida).
    - Sybase (adquirido por SAP).
    
- **Concepto Clave:** Manejo de transacciones con propiedades ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad), una genialidad que no ofrecían bases de datos anteriores (modelo de red, jerárquicas).
- **Compatibilidad:** El modelo de tablas relacionales era asimilable a archivos, facilitando la transición para programadores de lenguajes históricos (Cobol, RPG, C, Pascal) al inyectar SQL.
- **Limitaciones:** No escalan bien en entornos distribuidos y no son eficientes para datos no estructurados.

### **3. Surgimiento de NoSQL y Big Data**

- **Contexto:** Últimos 20 años, revolución que desafía los motores relacionales.
- **Nuevos Paradigmas de Almacenamiento:** Motivados por la cantidad, velocidad y variabilidad de los datos.
- **Concepto de Big Data:**
    
    - **Volumen:** Cantidad masiva de datos (ej. redes sociales, sensores, geoposición, búsquedas).
    - **Velocidad:** Rapidez con la que se generan y procesan los datos.
    - **Variedad:** Diversidad de formatos de datos (video, audio, imágenes, texto, JSON, XML, logs).
    - **Veracidad (opcional):** Fiabilidad de la fuente de los datos.
    - **Valor (opcional):** Utilidad de los datos.
    
- **Ejemplos de Volumen de Datos (2012-2016):**
    
    - **YouTube:** 48 horas de video/minuto (2012) -> 300 horas de video/minuto (2015).
    - **Google:** >2 millones de búsquedas/minuto (2012) -> duplicado en 2013.
    - **Facebook:** ~700,000 piezas compartidas/minuto (2012) -> ~2.5 millones (2013).
    - **Twitter:** >100,000 tweets/minuto (2012) -> 277,000 (2013).
    - **The Weather Channel:** ~14 millones de pronósticos/minuto (2016) -> 18 millones (2017).
    - **Spam Mails:** 103 millones de mails spam/minuto (2017).
    
- **Necesidad de Distribución Horizontal:** Para manejar el volumen y la velocidad de los datos, se requiere un procesamiento distribuido en múltiples computadoras, no un crecimiento vertical (más RAM, más disco en un solo servidor).
- **Aplicaciones Modernas:**
    
    - Tiempos de respuesta menores a un segundo.
    - Disponibilidad 24/7 (ej. redes sociales, home banking).
    - Alta disponibilidad.
    - Generación masiva de datos (sensores).
    
- **Sacrificio de Propiedades ACID:** Se sacrifican propiedades como la consistencia fuerte por:
    
    - **Latencia:** Tiempo de respuesta rápido.
    - **Particionamiento:** Datos distribuidos globalmente y replicados.
    - **Alta Disponibilidad:** Sistema siempre activo.
    - **Ejemplo LinkedIn:** No importa la consistencia exacta de las visualizaciones, sino que la publicación sea visible globalmente y el sistema esté disponible y rápido.
    
- **Costos de Almacenamiento:** La drástica reducción del costo por GB (de 0.10 hoy) permitió cambiar los paradigmas de modelado:
    
    - **Relacionales:** Normalización, poca redundancia de datos.
    - **NoSQL/Big Data:** Desnormalización, repetición de datos para menor costo de procesamiento y mayor velocidad.
    

### **4. Teorema CAP (Consistencia, Disponibilidad, Tolerancia a Particiones)**

- **Definición:** Un sistema distribuido (bases de datos NoSQL distribuidas) puede cumplir al 100% dos de estas tres propiedades:
    
    - **Consistencia (C):** Todos los nodos tienen la misma versión del dato actualizado.
    - **Disponibilidad (A):** El sistema sigue funcionando y accesible a los datos, incluso si algunos nodos fallan.
    - **Tolerancia a Particiones (P):** El sistema continúa funcionando ante un corte en la red que divide el clúster.
    
- **Tipos de Bases de Datos según CAP:**
    
    - **CA (Consistencia y Disponibilidad):** Bases de datos relacionales (no se distribuyen en n nodos).
    - **AP (Disponibilidad y Tolerancia a Particiones):** Priorizan estas dos propiedades sobre la consistencia. Ej: Cassandra.
    - **CP (Consistencia y Tolerancia a Particiones):** Priorizan estas dos propiedades sobre la disponibilidad. Ej: MongoDB, Redis.
    
- **Comportamiento ante Partición de Red:**
    
    - Algunos motores permiten solo lectura en la parte minoritaria del clúster.
    - Otros permiten actualizaciones en ambas partes y resuelven conflictos al reunirse la red.
    
- **Importancia:** La elección de la base de datos NoSQL depende de la necesidad del negocio y qué propiedades se priorizan.

### **5. Crecimiento de Datos Estructurados vs. No Estructurados**

- **Datos Estructurados (azul oscuro):** Producto del negocio (sistemas comerciales, RRHH). Crecimiento acotado (5-10% anual), atado al negocio.
- **Datos No Estructurados (celeste):** Vienen de sensores, internet, logs, mails. Crecimiento exponencial y logarítmico (ej. sensores que generan miles de millones de medidas).

### **6. Popularidad de Bases de Datos (DB-Engines Ranking)**

- **Metodología:** Menciones en motores de búsqueda, Google Trends, discusiones técnicas (Stack Overflow), ofertas de empleo (Indeed), perfiles profesionales (LinkedIn), redes sociales (Twitter/X).
- **Ranking (Agosto 2025 vs. Agosto 2021):**
    
    - **Relacionales:** Oracle (1ra), MySQL (2da), SQL Server (3ra), PostgreSQL (4ta). Han bajado en puntaje, pero siguen dominando.
    - **NoSQL:**
        
        - MongoDB: 5ta (se mantiene).
        - Redis: 7ma (se mantiene).
        - Apache Cassandra: 11va (se mantiene).
        - Neo4j: 21va (se mantiene).
        
    - **Nuevos Jugadores:** Snowflake (creciendo, 6ta), Google BigQuery (subiendo).
    
- **Estabilización del Auge NoSQL:** El crecimiento de las bases de datos NoSQL se ha estabilizado, en parte debido a la competencia de las bases de datos NoSQL ofrecidas por los proveedores de la nube (ej. AWS DocumentDB, Azure Cosmos DB compiten con MongoDB).

### **7. Historia de Bases de Datos NoSQL**

- **Pre-Relacionales:**
    
    - **1966:** IBM IMS (jerárquica), usada en el programa espacial Apolo.
    - **Lotus Notes:** Primera base de datos documental (no existía el concepto NoSQL, pero sentó las bases).
    
- **Iniciadores del Movimiento NoSQL:** Empresas de internet (Amazon, Google, redes sociales) que necesitaban soluciones para el volumen de datos que generaban, ya que las empresas tradicionales no las ofrecían.
- **Hitos NoSQL:**
    
    - **2000:** Neo4j (primeras NoSQL, modelo de grafos, no distribuida horizontalmente).
    - **2005:** CouchDB (documental, inspirada en Lotus Notes).
    - **2006:** Google BigTable (base para Column Family, como HBase).
    - **2007:** Amazon DynamoDB (clave-valor), MongoDB (documental, líder en su segmento).
    - **2008:** Cassandra (liberada por Facebook, desarrollada por autor de Amazon Dynamo).
    - **2009:** HBase (surge de especificación BigTable, proyecto Apache, Column Family).
    - **2010:** Redis (proyecto interno, luego apoyado por VMWare, clave-valor en memoria).
    

### **8. Tipos de Bases de Datos y su Orientación**

- **Bases de Datos Orientadas a Analítica:** Data Warehouses (en Big Data: plataformas en la nube, Hadoop, Object Storage, Spark).
- **Bases de Datos Orientadas a Operacional/Transaccional:**
    
    - **Relacionales:** Para transacciones económicas, consistencia fuerte.
    - **NoSQL:** Para operaciones, transacciones, mundo operacional.
    

### **9. Conceptos Clave en Big Data y NoSQL**

- **Escalamiento Horizontal:** Agregar más servidores (nodos) para aumentar la capacidad de procesamiento y almacenamiento.
- **Alta Disponibilidad:** Replicar datos (generalmente 3 veces) en múltiples servidores para asegurar el acceso continuo incluso si un servidor falla.
- **Particionamiento de Datos:** Dividir la base de datos en partes más pequeñas y distribuirlas entre múltiples servidores, donde la suma de todas las partes conforma el 100% de los datos.
- **Procesamiento en Paralelo:** Utilizar múltiples computadoras para procesar datos simultáneamente, esencial para grandes volúmenes.
- **Persistencia Políglota:** Una aplicación utiliza la mejor base de datos para cada caso de uso específico (ej. Redis para sesiones, Elasticsearch para búsquedas, MongoDB para documentación, relacional para transacciones económicas).

### **10. Tipos de Bases de Datos NoSQL (Detalle)**

- **Key-Value (Clave-Valor):**
    
    - **Modelo:** Almacena datos como pares clave-valor. El valor es opaco para la base de datos.
    - **Búsqueda:** Solo permite buscar por la clave. Muy rápidas.
    - **Uso:** Sesiones de usuario, cachés distribuidos, bloqueos distribuidos.
    - **Ejemplos:** Redis (líder, todo en memoria), Riak, Oracle NoSQL Database.
    
- **Column Family (Columnar):**
    
    - **Modelo:** Dos niveles de búsqueda (row key y clustering column).
    - **Búsqueda:** Restrictiva, atada al modelo.
    - **Uso:** Series de tiempo, datos de sensores.
    - **Ejemplos:** Apache Cassandra (líder), HBase.
    
- **Documentales:**
    
    - **Modelo:** Almacena documentos (generalmente en formato JSON), que pueden contener subdocumentos.
    - **Uso:** Catálogos de productos, información de documentación.
    - **Ejemplos:** MongoDB (líder, usa BSON internamente), CouchDB, Couchbase.
    - **Relación con otros tipos:** Una base de datos documental puede emular el comportamiento de una Key-Value o Column Family, pero con menor rendimiento.
    
- **Grafos:**
    
    - **Modelo:** Nodos conectados por relaciones (arcos). Modelado muy diferente.
    - **Uso:** Análisis de fraudes, redes sociales, relaciones complejas.
    - **Ejemplos:** Neo4j (líder).
    - **Nicho:** Son bases de datos muy particulares y de nicho.
    

### **11. Preguntas y Respuestas del Examen (8x8)**

**Pregunta 1: Verdadero/Falso**

- **Enunciado:** El modelo relacional fue diseñado para trabajar con grandes volúmenes de datos no estructurados.
- **Respuesta:** Falso.
- **Justificación:** Fue diseñado para datos estructurados (filas, columnas) y no es eficiente para datos no estructurados como videos, imágenes, JSON, logs.

**Pregunta 2: Desarrollo**

- **Enunciado:** ¿Qué entendemos por escalabilidad horizontal y por qué es importante en entornos de Big Data?
- **Respuesta:**
    
    - **Escalabilidad Horizontal:** Capacidad de agregar nuevos servidores (nodos) a un sistema para aumentar su capacidad de procesamiento y almacenamiento, en lugar de concentrar todo en un único nodo con hardware más potente.
    - **Importancia en Big Data:** Es clave porque permite manejar los gigantes volúmenes de datos crecientes y la alta concurrencia de forma distribuida y más económica, utilizando nodos de bajo costo.
    

**Pregunta 3: Múltiple Choice**

- **Enunciado:** ¿Cuál de los siguientes factores fue fundamental para el surgimiento del movimiento de Big Data?
- **Opciones:**
    
    - A) La disminución del costo de los servidores.
    - B) La necesidad de almacenar datos en la nube.
    - C) La explosión de datos generados por usuarios, sensores, redes sociales y dispositivos conectados.
    - D) El desarrollo de nuevos lenguajes de programación.
    
- **Respuesta:** C) La explosión de datos generados por usuarios, sensores, redes sociales y dispositivos conectados.
- **Justificación:** Este crecimiento masivo demandó nuevas tecnologías y arquitecturas, llevando a los gigantes tecnológicos a desarrollar sus propios motores al no encontrar soluciones adecuadas en el mercado.

**Pregunta 4: Verdadero/Falso**

- **Enunciado:** NoSQL significa "No Structured Query Language" y excluye toda posibilidad de realizar consultas complejas sobre los datos.
- **Respuesta:** Falso.
- **Justificación:** NoSQL significa "Not Only SQL". La idea es complementar las bases de datos relacionales, no reemplazarlas, ofreciendo un "sabor" adicional de motores que permiten otro tipo de consultas y manejo de datos.

**Pregunta 5: Múltiple Choice**

- **Enunciado:** ¿Qué características comunes tienen las bases de datos NoSQL? (Seleccionar todas las correctas)
- **Opciones:**
    
    - A) Escalabilidad horizontal.
    - B) Rigidez en estructuras de tablas.
    - C) Alta disponibilidad.
    - D) Capacidad de trabajar con datos no estructurados.
    
- **Respuesta:** A, C, D.
- **Justificación:** La rigidez en estructuras de tablas es una prioridad del mundo relacional, no de NoSQL.

**Pregunta 6: Verdadero/Falso**

- **Enunciado:** Uno de los motivos por los cuales surgen nuevas bases de datos es que las bases relacionales presentan limitaciones para escalar eficientemente en arquitecturas distribuidas.
- **Respuesta:** Verdadero.
- **Justificación:** El modelo relacional, orientado a la consistencia fuerte (ACID), no escala bien en entornos distribuidos. Esto llevó al surgimiento de la idea de "consistencia eventual" como una estrategia diferente.

**Pregunta 7: Desarrollo**

- **Enunciado:** Mencionar al menos dos diferencias clave entre bases de datos relacionales y bases de datos NoSQL.
- **Respuesta (Ejemplos):**
    
    - **Consistencia:** Relacionales priorizan consistencia fuerte (ACID); NoSQL pueden optar por consistencia eventual.
    - **Esquema:** Relacionales tienen esquemas fijos y rígidos; NoSQL ofrecen flexibilidad de esquema (sin esquema o esquema dinámico).
    - **Escalabilidad:** Relacionales escalan verticalmente; NoSQL escalan horizontalmente.
    - **Tipo de Datos:** Relacionales para datos estructurados; NoSQL para datos estructurados, semi-estructurados y no estructurados.
    - **Modelo de Datos:** Relacionales usan tablas; NoSQL usan clave-valor, documentos, columnas, grafos.
    

**Pregunta 8: Múltiple Choice**

- **Enunciado:** ¿Qué enunciado refleja mejor el objetivo del movimiento NoSQL?
- **Opciones:**
    
    - A) Reemplazar completamente las bases de datos relacionales.
    - B) Ofrecer una solución alternativa para casos en que el modelo relacional no es eficiente.
    - C) Simplificar el lenguaje de consulta de bases de datos.
    - D) Eliminar la necesidad de esquemas de bases de datos.
    
- **Respuesta:** B) Ofrecer una solución alternativa para casos en que el modelo relacional no es eficiente.
- **Justificación:** Las bases de datos NoSQL complementan, no reemplazan, y atacan otro tipo de escenarios, especialmente aquellos que requieren alta velocidad de escritura/lectura, flexibilidad de esquema y manejo de grandes volúmenes de datos (las "cuatro V" de Big Data).