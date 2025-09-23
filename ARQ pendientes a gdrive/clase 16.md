- **Inicio de la Clase: Definición de Memoria:**
    
    - La profesora comienza a grabar la clase y pide a los alumnos que anoten la definición de memoria.
    - **Definición de Memoria:**
        
        - Desde el punto de vista circuital, una memoria es una matriz de M por N.
        - **M:** Cantidad de posiciones direccionables (filas).
        - **N:** Cantidad de bits por posición (columnas).
        - **Posición/Locación:** Un renglón completo de la matriz.
        - **Celda Binaria:** Un cuadradito individual dentro de la matriz (un bit).
        
    
- **Tipos de Memoria (Estática vs. Dinámica):**
    
    - **Memoria Estática (SRAM):**
        
        - Cada celda binaria es un biestable (flip-flop).
        - Típica de las memorias caché.
        - Requiere transistores (mínimo 4 por compuerta NOR, o 6 si es sincrónica).
        - No pierde la información mientras tenga energía.
        
    - **Memoria Dinámica (DRAM):**
        
        - Cada celda binaria es un capacitor.
        - El capacitor representa el 1 lógico con un nivel de voltaje y el 0 lógico con otro.
        - El capacitor degrada y pierde la información con el tiempo (se comporta como un filtro).
        - Requiere un proceso de "refresco" o "restauración" constante para evitar la pérdida de datos.
        - Mientras se refresca, la memoria no es accesible.
        - Ejemplos: DDR, DDR4, DDR5.
        - La "S" en SDR significa "sincrónico", no "estático".
        
    
- **Capacidad de Memoria:**
    
    - Se puede dar en bits o en bytes.
    - **En bits:** M * N (producto de filas por columnas).
    - **En bytes:** (M * N) / 8.
    - Ejemplo: Una memoria de 4x8 tiene una capacidad de 32 bits o 4 bytes.
    - **Unidades de Capacidad:**
        
        - K (Kilo): 2^10 (1024)
        - Mega: 2^20 (K * K)
        - Giga: 2^30 (K * Mega)
        - Tera: 2^40 (Mega * Mega)
        - Peta: 2^50 (K * Tera)
        
    
- **Ejercicio de Rangos de Direcciones y Capacidades:**
    
    - La profesora pide a los alumnos que calculen el rango de direcciones (en decimal, binario y hexadecimal) y la capacidad (en bits y bytes) para varias matrices de memoria:
        
        - 4x8
        - 4x16
        - 2x16
        - 8x8
        - 16x8
        - 1024x8
        - Kx8
        - 2Kx8
        - 4Kx8
        - 4Kx16
        - 4Kx32
        
    - Se enfatiza que el rango de direcciones se refiere a M (cantidad de posiciones), no a N (bits por posición).
    - Se concluye que trabajar con binario es tedioso y que se usará hexadecimal para las direcciones.
    
- **Importancia de la Memoria en la Computadora:**
    
    - Se discute por qué la memoria es esencial: para guardar información y datos (procesados y no procesados).
    - **Firmware:** Software implementado físicamente (ej. BIOS), con funciones básicas para encender la PC.
    - **Memoria RAM:** Almacena programas, datos (no procesados) y resultados (datos procesados/información).
    - **CPU y RAM:** La CPU (procesador) ejecuta el software y necesita acceder constantemente a la RAM para buscar instrucciones, leer datos, procesarlos y volcar resultados. La RAM no accede a la CPU, es la CPU la que accede a la RAM.
    - **Memoria Principal:** La memoria RAM es la memoria principal, a la que la CPU accede directamente sin intermediarios. Se diferencia de las memorias secundarias (ej. MicroSD).
    - **Buses:** La CPU se conecta con la memoria principal a través de buses (caminos de comunicación).
    
- **Direccionamiento de Memoria:**
    
    - **Dirección de Memoria (Memory Address):** Número asociado a cada fila/locación de memoria.
    - La CPU accede a la memoria por renglón (posición).
    
- **Proceso de Lectura de la RAM por la CPU (3 Pasos):**
    
    - **Paso 1: Transferir la Dirección:**
        
        - La CPU envía la dirección deseada a través del **bus de direcciones** al **Registro de Direcciones de Memoria (MAR - Memory Address Register)**.
        - Un **decodificador de memoria** (N a 2^N) usa los bits del MAR para seleccionar la fila correcta.
        
    - **Paso 2: Dar Orden de Lectura:**
        
        - La CPU envía una señal de "lectura" (un 1 lógico) a través de una línea de control (ej. Rd/Wr).
        
    - **Paso 3: Transferir Contenido Leído:**
        
        - El contenido binario de la posición seleccionada se carga en el **Registro de Datos de Memoria (MDR - Memory Data Register)**, que actúa como un buffer.
        - El MDR tiene tantos bits como N (cantidad de bits por posición).
        - El contenido se transfiere desde el MDR al destino (ej. un registro interno de la CPU) a través del **bus de datos**.
        
    - **Microoperaciones:** Cada uno de estos pasos es una microoperación y ocurre acompañada de un evento de clock.
    
- **Relación con el Modelo de Estudio Anterior (Unidad 7):**
    
    - Se repasa el modelo de estudio anterior (antes de vacaciones) donde la memoria RAM era de 4096 posiciones (0 a 4095), requiriendo 12 bits para direccionar (2^12 = 4096).
    - La memoria era de 4Kx16 (cada posición almacenaba 16 bits).
    - **Código de Operación (Opcode):** Los primeros bits de una instrucción que indican qué acción debe realizar la CPU. En el modelo anterior, eran 4 bits (16 verbos/instrucciones).
    - **Instrucción Completa:** Opcode (4 bits) + Dirección (12 bits) = 16 bits.
    - **Ejemplo de Programa en Memoria (Suma A+B en C):**
        
        - Se muestra cómo un programa simple (C = A + B) se almacena en memoria RAM en formato binario y hexadecimal.
        - **Instrucción 1 (10F0):** Cargar el valor de la dirección 0F0 (variable A) en el acumulador de la CPU.
        - **Instrucción 2 (20F1):** Sumar al acumulador el valor de la dirección 0F1 (variable B).
        - **Instrucción 3 (30FF):** Almacenar el resultado del acumulador en la dirección 0FF (variable C).
        
    - **Assembler:** Se compara el código de máquina con su representación en assembler (LDA, ADA, Store Accumulator).
    
- **Próxima Clase y Trabajo Práctico:**
    
    - Se retoma el ejercicio de las matrices de memoria para calcular:
        
        - Rangos de direcciones en potencias de dos (0 a 2^N - 1).
        - Capacidad de memoria en bits y bytes (en la unidad más adecuada: KB, MB, GB).
        - Cantidad de líneas del bus de direcciones y del bus de datos.
        - Cantidad de bits que almacenan el MAR y el MDR.
        
    - Se explica cómo calcular la capacidad en bits y bytes usando potencias de dos (ej. 2Kx32 = 2^1 * 2^10 * 2^5 = 2^16 bits = 64K bits; 2^16 / 8 = 2^13 bytes = 8K bytes).
    - Se anuncia que el trabajo práctico de la Unidad 7 (que ya habían visto) tiene fecha de entrega en 15 días y es obligatorio.
    - Se aclara que los trabajos prácticos son obligatorios (70% de entrega) y se entregan por el buzón en la fecha indicada.
    
- **Ciclo de Instrucción (Repaso):**
    
    - **Fetch (Búsqueda):** Buscar la instrucción en memoria RAM y cargarla en el **Registro de Instrucciones (IR)**.
    - **Decode (Decodificación):** La **Unidad de Control** decodifica el código de operación.
    - **Operand Fetch (Búsqueda de Operando):** No siempre es necesario. Si la instrucción requiere un operando, la dirección del operando se saca del campo de datos de la instrucción, se transfiere al MAR, se da la orden de lectura, y el contenido se almacena en el MDR.
    - **Execute (Ejecución):** Se realiza la operación (suma, AND, etc.) con el operando.
    
- **Introducción al Modelo Intel (Unidad 8):**
    
    - Se introduce la arquitectura de CPU Intel (x86, 32/64 bits).
    - **Registros de CPU:**
        
        - En el modelo Intel, en lugar de un solo acumulador, hay **cuatro registros de cálculo** de 32 bits (ajustables a 16 u 8 bits).
        - **EAX (Extended Accumulator):** Acumulador por excelencia.
        - **EBX (Extended Base):** Registro base.
        - **ECX (Extended Counter):** Contador (para iteraciones, cuenta regresivamente).
        - **EDX (Extended Data):** Registro de datos.
        - Versiones de 16 bits: AX, BX, CX, DX.
        - Versiones de 64 bits: RAX, RBX, RCX, RDX (R de "re-extended").
        - Estos registros son afectados por instrucciones aritméticas y lógicas.
        - Intel tiene instrucciones complejas (ej. multiplicación directa).
        
    - **Direccionamiento en Intel:**
        
        - Intel identifica cada byte de memoria con una dirección.
        - Las direcciones son de 32 bits (ej. 4GB de memoria = 2^32 direcciones).
        - Las direcciones en las instrucciones (entre corchetes) no son direcciones absolutas, sino **desplazamientos (offsets)**.
        - El sistema operativo asigna una base, y el compilador el desplazamiento, para manejar la reubicación de programas en memoria.
        
    - **Acceso a Partes de Registros:**
        
        - Los registros de 32 bits (EAX, EBX, ECX, EDX) se pueden dividir en partes de 16 bits (AX, BX, CX, DX).
        - Las partes de 16 bits se pueden dividir en partes de 8 bits:
            
            - AH (Accumulator High), AL (Accumulator Low)
            - BH (Base High), BL (Base Low)
            - CH (Counter High), CL (Counter Low)
            - DH (Data High), DL (Data Low)
            
        - Esto permite manipular datos de diferentes tamaños.
        - Ejemplo: `move ax, [0200]` carga 2 bytes (direcciones 200 y 201) en AX.
        - Ejemplo: `move al, [0200]` carga solo 1 byte (dirección 200) en AL.
        
    - La CPU tiene una pequeña memoria local: su banco de registros de cálculo.
    
- **Cierre de la Clase:**
    
    - La profesora finaliza la clase, indicando que la próxima clase continuarán con la Unidad 8 (modelo Intel).
    - Se recuerda la importancia de la presencialidad para la promoción (cuestionarios sencillos durante la clase).
    

**2. Preguntas y Respuestas para Exámenes:**

- **Definición de Memoria:**
    
    - **Pregunta:** Desde el punto de vista circuital, ¿cómo se define una memoria?
    - **Respuesta:** Una memoria es una matriz de M por N, donde M es la cantidad de posiciones direccionables (filas) y N es la cantidad de bits por posición (columnas).
    
- **Tipos de Memoria:**
    
    - **Pregunta:** ¿Cuál es la diferencia principal entre una memoria estática (SRAM) y una memoria dinámica (DRAM) en cuanto a su celda binaria y su comportamiento?
    - **Respuesta:**
        
        - **SRAM:** Cada celda binaria es un biestable (flip-flop). No pierde la información mientras tenga energía.
        - **DRAM:** Cada celda binaria es un capacitor. Pierde la información con el tiempo y requiere un proceso constante de "refresco" o "restauración" para mantener los datos.
        
    
- **Capacidad de Memoria:**
    
    - **Pregunta:** ¿Cómo se calcula la capacidad de una memoria en bits y en bytes, dada una matriz de M por N?
    - **Respuesta:**
        
        - Capacidad en bits = M * N
        - Capacidad en bytes = (M * N) / 8
        
    
- **Proceso de Lectura de la RAM por la CPU:**
    
    - **Pregunta:** Describa los tres pasos principales que sigue la CPU para leer datos de la memoria RAM. Mencione los buses y registros involucrados.
    - **Respuesta:**
        
        1. **Transferir la Dirección:** La CPU envía la dirección deseada a través del **bus de direcciones** al **Memory Address Register (MAR)**.
        2. **Dar Orden de Lectura:** La CPU envía una señal de lectura (un 1 lógico) a la memoria.
        3. **Transferir Contenido Leído:** El contenido de la posición seleccionada se carga en el **Memory Data Register (MDR)** y luego se transfiere al destino a través del **bus de datos**.
        
    
- **Ciclo de Instrucción:**
    
    - **Pregunta:** ¿Cuáles son las cuatro etapas en las que se divide un ciclo de instrucción? Describa brevemente cada una.
    - **Respuesta:**
        
        1. **Fetch (Búsqueda):** La instrucción se busca en memoria RAM y se carga en el Registro de Instrucciones (IR).
        2. **Decode (Decodificación):** La Unidad de Control interpreta el código de operación de la instrucción.
        3. **Operand Fetch (Búsqueda de Operando):** Si la instrucción lo requiere, se busca la dirección del operando y se carga su contenido.
        4. **Execute (Ejecución):** Se realiza la operación especificada por la instrucción.
        
    
- **Registros de CPU Intel:**
    
    - **Pregunta:** Mencione los cuatro registros de cálculo principales en la arquitectura Intel (32 bits) y su función general.
    - **Respuesta:**
        
        1. **EAX (Extended Accumulator):** Acumulador principal para operaciones aritméticas y lógicas.
        2. **EBX (Extended Base):** Registro base, a menudo usado para direccionamiento.
        3. **ECX (Extended Counter):** Contador, usado para bucles e iteraciones.
        4. **EDX (Extended Data):** Registro de datos, a menudo usado para operaciones de E/S o como extensión de EAX en multiplicaciones/divisiones.
        
    
- **Direccionamiento en Intel:**
    
    - **Pregunta:** En la arquitectura Intel, ¿por qué las direcciones en las instrucciones (entre corchetes) no son direcciones absolutas, y qué representan?
    - **Respuesta:** No son direcciones absolutas porque los programas pueden cargarse en diferentes ubicaciones de memoria. Representan **desplazamientos (offsets)** relativos a una dirección base asignada por el sistema operativo, lo que permite la reubicación de programas.
    

**3. Lecciones Aprendidas:**

- **Importancia de la Memoria:** La memoria es fundamental para el funcionamiento de una computadora, ya que almacena tanto los programas como los datos (procesados y no procesados) que la CPU necesita para operar.
- **Estructura Matricial de la Memoria:** Comprender que la memoria se organiza como una matriz de M filas por N columnas es clave para entender cómo se accede a los datos y cómo se calcula su capacidad.
- **Diferencia entre SRAM y DRAM:** La distinción entre memoria estática (biestables, más rápida, más cara, usada en caché) y dinámica (capacitores, más lenta, más barata, usada en RAM principal) es crucial para entender el rendimiento y el costo de los sistemas.
- **Proceso de Acceso a Memoria:** El algoritmo de tres pasos (transferir dirección, dar orden, transferir contenido) y los componentes involucrados (buses de direcciones y datos, MAR, MDR, decodificador) son la base de cómo la CPU interactúa con la memoria.
- **Ciclo de Instrucción:** Las cuatro fases (Fetch, Decode, Operand Fetch, Execute) son el corazón del funcionamiento de la CPU y cómo procesa las instrucciones.
- **Evolución de la Arquitectura de CPU:** La transición de modelos básicos con un solo acumulador a arquitecturas más complejas como Intel, con múltiples registros de cálculo y direccionamiento segmentado/relativo, muestra el avance en el diseño de procesadores.
- **Relevancia de las Matemáticas en Informática:** Aunque algunas materias puedan parecer ajenas, las matemáticas (álgebra, funciones) son herramientas esenciales para el desarrollo de software de base y la comprensión de algoritmos complejos.
- **Importancia de la Presencialidad y Participación:** La interacción en clase y la resolución de ejercicios prácticos son fundamentales para afianzar los conocimientos, más allá de la disponibilidad de grabaciones.
- **Rol del Analista Funcional:** Es una figura clave en el desarrollo de sistemas, actuando como puente entre las necesidades del negocio y la implementación técnica, asegurando que el software cumpla con los requisitos y sea útil para la organización.
- **Uso de Hexadecimal:** Para manejar grandes rangos de direcciones de memoria, el hexadecimal es una notación más eficiente y práctica que el binario.