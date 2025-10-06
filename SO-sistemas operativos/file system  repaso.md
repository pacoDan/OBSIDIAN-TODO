El contenido proporcionado es una transcripción de una clase o repaso sobre **Sistemas de Archivos (File Systems)** en el contexto de Sistemas Operativos y Arquitectura de Computadoras. A continuación, se presenta un resumen estructurado, incluyendo detalles clave y posibles preguntas de examen, basado en la transcripción.

### **1. Introducción al Administrador de Archivos**

- **Definición:** El administrador de archivos es un módulo del sistema operativo encargado de gestionar el almacenamiento secundario (discos rígidos, SSDs, etc.) y terciario (dispositivos extraíbles).
- **Objetivos al Evaluar un File System:**
    
    - **Asignación de Espacio:** Cómo se asigna espacio a los archivos.
    - **Administración de Espacio Libre:** Cómo se gestiona el espacio no utilizado.
    - **Fragmentación:** Cómo se maneja la fragmentación de archivos.
    - **Seguridad:** Garantizar la protección de los datos.
    - **Coherencia:** Mantener la integridad del sistema de archivos, especialmente después de fallos (ej. apagones).
    

### **2. Conceptos Fundamentales del File System**

- **Partición:** Una división lógica o agrupación de espacio en disco. Puede ser una unión de varios discos.
- **Volumen:** Una partición con formato. Contiene la metadata necesaria para administrar el file system, además de los datos del usuario.
- **Archivo:** Una colección de información con algún tipo de relación para su creador.
    
    - **Atributos Principales:** Nombre, identificador, tipo, fecha de creación, fecha de último acceso, fecha de última actualización, protección, etc.
    
- **FCB (File Control Block):** Un bloque que guarda la metadata de un archivo dentro del file system.
    
    - **Persistencia:** El FCB está en el disco. Cuando se abre un archivo, su FCB se lee y se lleva a memoria.
    - **Diferencia con PCB:** A diferencia del PCB (Process Control Block) que reside en memoria, el FCB está en disco.
    - **Implementación en EXTended (Linux):** Utiliza "inodos" como FCBs, que contienen información y punteros a los bloques de datos.
    

### **3. Operaciones sobre Archivos y Directorios**

- **Operaciones Básicas:** Crear, escribir, leer, posicionar, etc.
- **Operaciones Combinadas:**
    
    - **Mover un Archivo:** Dentro del mismo file system, a menudo implica solo actualizar una entrada de directorio, no una copia completa.
    - **Crear un Directorio:** Implica una operación de escritura.
    - **Leer un Directorio:** Implica una operación de lectura.
    - **Crear un Archivo en un Directorio:** Abrir el directorio, escribir en él y luego cerrarlo.
    

### **4. Bloqueos (Locks) y Coherencia**

- **Propósito:** Evitar que múltiples procesos escriban simultáneamente en un archivo y asegurar la integridad de los datos (evitar leer datos desactualizados).
- **Tipos de Locks:**
    
    - **Compartidos (Shared Locks):** Permiten acceso de lectura a múltiples procesos.
    - **Exclusivos (Exclusive Locks):** Permiten acceso de escritura a un único proceso.
    
- **Mecanismos de Implementación:**
    
    - **Obligatorio:** El sistema operativo garantiza la integridad (ej. Windows). Si un archivo tiene un lock de escritura, nadie más puede acceder.
    - **Sugerido:** La integridad es responsabilidad del usuario/programador (ej. Linux). El sistema operativo provee mecanismos para consultar el estado del lock, pero no lo impone estrictamente.
    
- **Diferencia con Semáforos:** Los locks están orientados a archivos y son gestionados por el sistema operativo para garantizar la integridad a nivel global, mientras que los semáforos son para la sincronización de procesos programados por el usuario.

### **5. Apertura de Archivos y Descriptores**

- **Tablas de Archivos Abiertos:**
    
    - **Tabla Global:** Contiene entradas para todos los archivos abiertos en el sistema. Incluye un contador de aperturas.
    - **Tabla por Proceso:** Contiene descriptores de archivo específicos para cada proceso.
    
- **Proceso de Apertura:**
    
    1. Buscar en la tabla global.
    2. Si no está, agregar una entrada en la tabla global y en la tabla del proceso.
    3. Si ya está abierto por otro proceso, solo agregar una entrada en la tabla del proceso.
    
- **Contador de Aperturas:** En la tabla global, indica cuántos procesos tienen un archivo abierto. Cuando llega a cero, la entrada puede eliminarse.
- **File Descriptors:** Números enteros que identifican un archivo abierto dentro de un proceso.
    
    - **Reservados:** 0 (stdin), 1 (stdout), 2 (stderr).
    - **Uso:** A partir del 3. Son locales a cada proceso y pueden repetirse entre procesos.
    - **Compartidos entre Hilos:** Los file descriptors son compartidos entre los hilos de un mismo proceso.
    

### **6. Estructuras de Directorios**

- **Representación Lógica:** Tablas con identificadores de archivo (ej. número de FCB/inodo) y nombres. Pueden incluir metadata redundante para optimización.
- **Tipos de Estructuras:**
    
    - **Lista Lineal:** Simple, pero ineficiente para búsquedas.
    - **Árboles/Grafos:** Más complejos y eficientes.
        
        - **Grafos Acíclicos:** Comunes en sistemas modernos (ej. Linux con hard links a archivos), evitan ciclos para simplificar búsquedas y recursión.
        
    
- **Entrada de Directorio:** Un archivo de tipo directorio contiene entradas que apuntan a otros archivos o directorios. Cada entrada tiene un tamaño fijo, limitando el número de entradas por bloque.

### **7. Protección y Permisos**

- **Niveles de Protección:**
    
    - **Completa:** Acceso restringido.
    - **Libre:** Sin restricciones.
    - **Controlado:** Basado en permisos definidos.
    
- **ACL (Access Control List):** Lista granular de usuarios y sus permisos para cada archivo. Problema: gestión compleja al añadir nuevos usuarios.
- **Propietario/Grupo/Universo (Owner/Group/Others):** Esquema más sencillo (ej. Unix/Linux) que define permisos (lectura, escritura, ejecución) para el propietario, el grupo al que pertenece el propietario y el resto de usuarios. Utiliza 9 bits.
- **Granularidad:** Posibilidad de aplicar permisos a archivos individuales, carpetas, o subcarpetas.

### **8. Asignación de Espacio en Disco**

- **Asignación Contigua:**
    
    - **Concepto:** Asigna bloques contiguos en disco a un archivo.
    - **Ventajas:** Menos reposicionamiento del cabezal del disco, lectura/escritura rápida para acceso secuencial y directo. Ideal para dispositivos de solo lectura o archivos que no crecen.
    - **Desventajas:** Fragmentación externa, dificultad para hacer crecer archivos.
    - **Soluciones:**
        
        - **Compactación:** Mover bloques para consolidar espacio libre.
        - **Pre-asignación:** Asignar más bloques de los necesarios al crear el archivo.
        - **Punteros al final:** Si un archivo no puede crecer contiguamente, se puede apuntar a otro bloque en otro lugar.
        
    
- **Asignación Enlazada (Linked Allocation):**
    
    - **Concepto:** Cada bloque de un archivo contiene un puntero al siguiente bloque. El directorio solo almacena el primer bloque.
    - **Ventajas:** No hay fragmentación externa, fácil crecimiento de archivos.
    - **Desventajas:** Acceso directo lento (requiere recorrer todos los punteros), dispersión de bloques (más movimiento del cabezal).
    - **Herramientas:** Desfragmentadores de disco para mejorar el rendimiento.
    
- **Asignación Indexada (Indexed Allocation):**
    
    - **Concepto:** Cada archivo tiene un bloque índice (inodo en EXT) que contiene punteros a todos sus bloques de datos.
    - **Ventajas:** Acceso directo rápido (se accede al bloque índice y luego al bloque deseado), no hay fragmentación externa.
    - **Desventajas:** El bloque índice puede ser un cuello de botella si el archivo es muy grande.
    - **Soluciones (en EXT):**
        
        - **Punteros Directos:** Apuntan directamente a bloques de datos.
        - **Punteros Indirectos Simples:** Apuntan a un bloque que contiene punteros a bloques de datos.
        - **Punteros Indirectos Dobles:** Apuntan a un bloque que contiene punteros a bloques que contienen punteros a bloques de datos.
        - **Punteros Indirectos Triples:** Apuntan a un bloque que contiene punteros a bloques que contienen punteros a bloques que contienen punteros a bloques de datos.
        - Esto permite manejar archivos de tamaños extremadamente grandes de forma exponencial.
        
    

### **9. Administración de Espacio Libre**

- **Bitmap (Mapa de Bits):** Un bit por cada bloque en disco, indicando si está libre (0) u ocupado (1).
    
    - **Ventajas:** Rápido para encontrar espacio libre.
    - **Desventajas:** El bitmap puede ser muy grande y debe estar en RAM para un acceso rápido, lo que requiere sincronización con el disco.
    

### **10. Coherencia y Recuperación de Fallos**

- **ScanDisk/CheckDisk:** Herramientas que revisan bloque por bloque la consistencia del file system.
- **Journaling (Registro por Diario):**
    
    - **Concepto:** Se guarda un historial de transacciones (operaciones) antes de ejecutarlas.
    - **Proceso:** Antes de una operación (ej. crear archivo), se registran todos los pasos necesarios. Una vez completados, se marca la transacción como finalizada ("commit").
    - **Recuperación:** Si hay un fallo, el sistema solo necesita revisar las últimas transacciones incompletas en el journal, lo que es mucho más rápido que escanear todo el disco.
    

### **11. Ejemplos de File Systems**

- **FAT (File Allocation Table):**
    
    - **Variantes:** FAT12, FAT16, FAT32 (el número indica la cantidad de bits por entrada en la tabla FAT).
    - **Funcionamiento:** Utiliza una tabla FAT al inicio del sistema para gestionar la asignación de bloques. Cada entrada en la tabla apunta al siguiente bloque del archivo.
    - **Características:**
        
        - **Fragmentación:** Tiende a fragmentarse porque asigna el primer bloque libre que encuentra.
        - **Tamaño de Bloque:** El tamaño del bloque afecta la fragmentación interna y el tamaño máximo del disco soportado. Bloques más grandes reducen el tamaño de la tabla FAT pero aumentan la fragmentación interna.
        - **Entradas Especiales en FAT:** 0x000 (libre), 0xFFF/0xFFF8 (fin de archivo), 0xFFF7 (bloque dañado).
        - **FCB:** La información del FCB se guarda en los directorios.
        
    
- **EXT (Extended File System):**
    
    - **Concepto de Grupos:** Divide el disco en grupos de cilindros para optimizar la localización de archivos y minimizar el movimiento del cabezal. Cada grupo es como un "mini file system".
    - **Superbloque:** Contiene información general del file system y metadata de cada grupo (ej. número de inodos libres, bloques libres).
    - **Inodos:** Son los FCBs de EXT. Se pre-crean en cada grupo y se asignan a los archivos. Contienen metadata y punteros a bloques de datos (directos, indirectos simples, dobles, triples).
    

### **12. Enlaces (Links)**

- **Hard Link (Enlace Duro):**
    
    - **Concepto:** Múltiples entradas de directorio apuntan al mismo inodo (o FCB).
    - **Características:**
        
        - Son el mismo archivo, comparten permisos y metadata.
        - El sistema mantiene un contador de enlaces. El archivo solo se borra cuando el contador llega a cero.
        - No se permiten a directorios (para evitar ciclos en el grafo).
        
    
- **Soft Link / Symbolic Link (Enlace Blando / Simbólico):**
    
    - **Concepto:** Es un archivo diferente cuyo contenido es una ruta a otro archivo o directorio.
    - **Características:**
        
        - Es un tipo de archivo distinto (regular, directorio, simbólico).
        - Puede apuntar a archivos o directorios que no existen o que están fuera del file system actual.
        - Si el archivo original se borra, el symbolic link queda "roto".
        - Implica más accesos a disco (leer el link, luego seguir la ruta), por lo que es más lento que un hard link.
        