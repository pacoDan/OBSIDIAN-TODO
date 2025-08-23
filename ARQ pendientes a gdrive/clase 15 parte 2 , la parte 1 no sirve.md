#### **II. Conceptos Fundamentales de Arquitectura de Computadoras**

- **Unidades de Procesamiento de Datos:**
    
    - **Unidad de Punto Fijo (Fixed-Point Unit):** Opera enteros.
    - **Unidad de Punto Flotante (Floating-Point Unit):** Opera reales.
    - **Importancia:** Son lo mínimo que tiene una CPU comercial.
    - **Conjunto:** Forman la parte que opera con datos.
    
- **Procesador en Dispositivos Cotidianos (Celulares):**
    
    - **Pregunta:** ¿Cómo se llama en un celular genéricamente lo que ejecuta programas, aplicaciones y opera datos?
    - **Respuesta:** Procesador o microprocesador.
    - **Aclaración:** El sistema operativo es software, no hardware.
    - **Ejemplos de Procesadores:** Intel (i7, i5, i3), ARM (arm7, m2, arm4a).
    - **Núcleos e Hilos:** Se menciona la existencia de múltiples núcleos (ej. Xeon con 50, Ryzen con 4 u 8) e hilos.
    
- **Definición de CPU:**
    
    - **CPU (Central Processing Unit):** Se define como el **núcleo**.
    - **Procesador:** Un conjunto de CPUs.
    - **Función de la Materia:** Contar cómo una CPU se interconecta con la memoria.
    - **Nivel de Estudio:** No se aborda el nivel multinúcleo, ya que lo maneja el sistema operativo.
    - **Definición Clave:** La CPU es la unidad mínima de procesamiento de instrucciones.
    
- **Unidad de Control:**
    
    - **Pregunta:** Si la unidad de coma fija opera enteros y la unidad de coma flotante opera reales, ¿quién opera las instrucciones?
    - **Respuesta:** Una unidad de control.
    - **Definición:** Es quien interpreta, busca en la memoria, y ejecuta instrucciones.
    - **Relación con Calculadoras:** Para ejecutar, usa las "calculadoras" (unidades de coma fija y flotante).
    - **Unidad de Ejecución:** El conjunto de unidad de coma fija y coma flotante es la unidad de ejecución o unidad de proceso de datos.
    - **Entidades Clave:** Unidad de Control (interpreta y ejecuta instrucciones) y Unidad de Ejecución (procesa datos).
    

#### **III. Algoritmos y Lenguajes de Programación**

- **Algoritmos:**
    
    - **Pregunta:** ¿Por qué se llama así la materia "Algoritmos y Estructura de Datos"?
    - **Respuesta:** Porque se desarrollan algoritmos y se ven diferentes estructuras de datos para usar en ellos.
    - **Definición de Algoritmo:** Pasos definidos con una finalidad, con principio y fin. Una secuencia de pasos ordenados lógicamente, finita, que sirven para resolver un problema.
    - **Ejemplo:** Una receta de cocina es un algoritmo.
    - **Representación de Algoritmos:**
        
        - Diagramas (dibujos).
        - Lenguaje de programación (codificación).
        
    
- **Lenguajes de Programación:**
    
    - **Necesidad:** Para que una CPU ejecute un programa o algoritmo, debe recibirlo escrito en un lenguaje de programación.
    - **Lenguaje Aprendido:** C++.
    - **Sentencia:** Una línea de código/programa en un lenguaje de programación.
    - **Características de un Lenguaje:** Sentencioso, tiene semántica y sintaxis que deben respetarse.
    
- **Código de Máquina vs. Código Fuente:**
    
    - **Problema:** Un programa en C++ no es ejecutable directamente por la computadora.
    - **Razón:** La computadora no "habla inglés", solo binario (código de máquina).
    - **Confusión con "Código":**
        
        - **Código C++:** Cómo se escribe la sentencia (ej. `C = A + B;`).
        - **Código de Máquina (Machine Code):** El lenguaje que entiende una máquina/procesador en particular.
        
    - **Proceso de Conversión:**
        
        - **Compilación:** Convierte un programa en C++ a lenguaje de máquina.
        - **Librerías:** Actúan como traductor entre el código fuente y el lenguaje de máquina binario.
        
    - **ASCII:**
        
        - **Función:** Códigos de representación de caracteres alfanuméricos.
        - **Almacenamiento:** Cuando se ingresa código C++ por teclado, se almacena en memoria en binario, pero como representación de caracteres (ASCII), no ejecutable.
        - **Importante:** Todo lo que entra a la computadora es binario, no solo el código de máquina. Cualquier carácter (alfabético, numérico, especial, de control) tiene una codificación binaria predeterminada.
        
    - **Compilador:**
        
        - **Función:** Interpreta la cadena ASCII (código fuente) y genera un conjunto de pasos (instrucciones en código de máquina).
        - **Relación Sentencia-Instrucción:** Por cada sentencia de C++, puede haber una o más instrucciones de máquina.
        - **Producto:** Genera un archivo `.exe` (ejecutable).
        
    - **Ejecución:**
        
        - La CPU (unidad de control) interpreta, decodifica y ejecuta **instrucciones de máquina**, no instrucciones de C++.
        - Para ejecutar, solo interesa el código de máquina (`.exe`). El código fuente (`.cpp`) es para leer, editar, modificar y recompilar.
        
    
- **Mecanismos de Traducción:**
    
    - **Compiladores:** Traducen el código fuente a código de máquina.
    - **Intérpretes:** Funcionamiento análogo, pero de manera diferente. El producto final es la instrucción de máquina.
    
- **Lenguaje Ensamblador (Assembler):**
    
    - **Manual del Procesador:** El fabricante (ej. AMD) entrega un manual con las instrucciones que el procesador puede ejecutar.
    - **Lectura del Manual:** Las instrucciones no se leen en unos y ceros, sino en código ensamblador.
    - **Definición de Assembler:** Una versión del código de máquina escrita en símbolos que el programador puede entender más fácilmente.
    - **Importancia de Estudiar Assembler:** No es un lenguaje "viejo", cada nuevo procesador tiene su propio assembler. Se estudia para entender cómo ejecuta la CPU, ya que el código de máquina es imposible de estudiar directamente.
    - **Definición Clave:** El assembler es el lenguaje simbólico del código de máquina.
    - **Programación en Alto Nivel vs. Bajo Nivel:**
        
        - **Alto Nivel (C++, Python, Java):** Creados para que los programadores se desentiendan de la intimidad de la CPU. No requieren conocer el hardware interno.
        - **Bajo Nivel (Assembler):** Necesario cuando se quiere trabajar a nivel CPU (ej. hacer una interfaz, un driver, conectar una impresora). Permite acceder a registros internos, memorias, puertos.
        
    - **Niveles de Lenguaje:**
        
        1. **Lenguaje de Alto Nivel:** Genera archivos en ASCII (código fuente).
        2. **Lenguaje Ensamblador:** Genera archivos en ASCII, pero representan código de máquina simbólico.
        3. **Código de Máquina:** Conjunto de ceros y unos que la CPU puede entender y ejecutar.
        
    - **Ejecutable:** Solo el archivo `.exe` (código de máquina) es ejecutable.
    - **Ensamblador (Software):**
        
        - **Función:** Traduce una instrucción en lenguaje ensamblador a una instrucción en código de máquina, una a una.
        - **Diferencia con Compilador:** Aunque hace algo similar, no se llama compilador.
        
    - **Proceso de Compilación (Dudas):**
        
        - **Pregunta:** ¿Cuando compilo C++, pasa a assembler y luego a lenguaje de máquina, o directamente a lenguaje de máquina?
        - **Respuesta:** Un compilador puede generar el ejecutable directamente. Algunos compiladores permiten generar un archivo assembler intermedio.
        - **¿Cuándo usar Assembler?** Cuando se necesita programar una comunicación, acceder a puertos de entrada/salida, controlar registros de estado de dispositivos (ej. impresora). Es decir, cuando se trabaja con lo físico.
        
    

#### **IV. Memoria**

- **Tipos de Memoria Vistos:**
    
    - **RAM (Random Access Memory):** Memoria de semiconductores, de lectura y escritura.
        
        - **Estructura:** Matricial (filas por columnas).
        - **Acceso:** La CPU accede a ella de forma directa.
        - **Nomenclatura:** Memoria principal o memoria interna.
        - **Razón de "Principal":** Las otras son auxiliares (pueden o no estar).
        - **Razón de "Interna":** Debe estar presente para que el procesador funcione.
        
    - **Registros:** Mencionados como tipo de memoria.
    - **Memoria de Semiconductores:**
        
        - **Base:** Biestables (flip-flops) formados por compuertas lógicas (componentes electrónicos).
        
    - **Otras Memorias (No de Compuertas):**
        
        - **Disco Duro:** Tecnología magnética/electromagnética.
        - **ROM (Read-Only Memory):** Mencionada pero dejada de lado.
        - **Estado Sólido (SSD, Pendrive, Tarjetas Externas):**
            
            - **Nomenclatura:** Memorias externas, masivas, secundarias.
            - **Características:** Mucha capacidad (muchos bytes).
            - **Acceso:** La CPU no accede a ellas de forma directa.
            - **Presencia:** Pueden o no estar presentes en un sistema.
            
        
    
- **Conexión CPU-Memoria RAM:**
    
    - **Medio:** Buses.
    - **Tipos de Buses:**
        
        1. **Bus de Direcciones:**
            
            - **Función:** Transmite la dirección a buscar en memoria.
            - **Característica Clave:** Unidireccional (siempre la CPU le dice a la memoria a qué acceder).
            - **Direccionabilidad:** La memoria RAM es direccionable (cada elemento tiene un número/dirección).
            - **Dirección Física de Memoria:** El número de orden del lugar.
            - **Potencial de Direccionamiento:**
                
                - **Pregunta:** Si tengo una memoria de 4 bytes, ¿cuántas direcciones tiene?
                - **Respuesta:** 4 (0, 1, 2, 3).
                - **Representación Binaria:** 00, 01, 10, 11.
                - **Líneas del Bus:** Necesita 2 líneas (2^2 = 4).
                - **Expansión:** No es expandible con 2 líneas a 5 bytes.
                - **Relación Líneas-Capacidad:** Por cada línea agregada al bus de direcciones, se duplica el potencial de direccionamiento (2^n).
                - **Ejemplo:** 3 líneas = 8 bytes; 4 líneas = 16 bytes.
                
            
        2. **Bus de Datos:**
            
            - **Función:** Transfiere los contenidos del lugar direccionado.
            - **Característica Clave:** Bidireccional (se lee y se escribe).
            - **Ancho de Palabra:** La cantidad de líneas del bus de datos tiene que ver con el ancho de la palabra (cantidad de bits a acceder por vez).
            - **Ejemplo:** Si se accede por byte, necesita 8 líneas.
            
        3. **Bus de Control:**
            
            - **Función:** Da órdenes de lectura o escritura a la memoria.
            - **Líneas:** Una o dos líneas.
            
        
    
- **Proceso de Acceso a Memoria (CPU):**
    
    - **Lectura:**
        
        1. Mandar la dirección (por bus de direcciones).
        2. Dar orden de lectura (por bus de control).
        3. Esperar transferencia del contenido (por bus de datos).
        
    - **Escritura:**
        
        1. Direccionar (por bus de direcciones).
        2. Transferir el contenido (por bus de datos).
        3. Dar la orden de escritura (por bus de control).
        
    
- **Registros Particulares de Memoria (Unidad 7):**
    
    - **MAR (Memory Address Register):** Recibe la dirección a la que se va a acceder.
    - **MDR (Memory Data Register):** Recibe el contenido de lo que se va a escribir o lo que fue leído. Son como "puertas de acceso" a la memoria.
    

#### **V. Ejecución de Programas y Ciclo de Instrucción**

- **Programa vs. Algoritmo:** Se usará "programa" en lugar de "algoritmo" porque la representación es a través de lenguajes de programación.
- **Ejecución de Programas:**
    
    - **Requisito:** Para ejecutar, el programa debe estar previamente almacenado en la **memoria principal (RAM)**. No se puede ejecutar directamente desde un disco.
    - **Sistema Operativo:** Permite ejecutar múltiples programas simultáneamente, coordinándolos y administrándolos en memoria principal.
    
- **Niveles de Pasos (Granularidad):**
    
    - **Programa No Ejecutable (Fuente):** Pasos "gigantes".
    - **Compilador:** Genera pasos más pequeños (instrucciones).
    - **Microoperaciones:** Pasos aún más pequeños y cortitos (ej. direccionar, dar orden de lectura, transferir).
    
- **Sincronización de Microoperaciones:**
    
    - **Necesidad:** Las microoperaciones deben estar sincronizadas (ej. no se puede dar orden de lectura sin direccionar primero).
    - **Sistema de Relojería:** Asegura que las microoperaciones ocurran en un momento determinado (T0, T1, etc.).
    
- **Frecuencia y Velocidad:**
    
    - **Frecuencia:** Cantidad de ciclos por segundo (inversa del período).
    - **Unidad de Medida:** Hertz (Hz).
    - **Relación Frecuencia-Tiempo:** A mayor frecuencia, disminuye la distancia de tiempo entre pulsos (inversamente proporcional).
    - **Unidades de Tiempo:**
        
        - 1000 Hz = 1 milisegundo (ms) por ciclo.
        - 1 millón de Hz = 1 microsegundo (µs) por ciclo.
        - 1 billón de Hz (10^9 Hz) = 1 nanosegundo (ns) por ciclo.
        
    - **Impacto en Ejecución:** Cuanto más veloz sea el reloj y más rápido se relacionen CPU y memoria, más rápido se ejecutarán los pasos y el programa.
    - **Tiempo de Respuesta de Memoria:**
        
        - **Ejemplo:** Memoria que responde en 20 ns (desde que la CPU da la orden de lectura hasta que el contenido está en el MDR).
        - **Comparación:** 40 ns es más lento que 20 ns.
        - **Importancia:** La velocidad de la memoria incide en la ejecución global de instrucciones. Una memoria lenta hace que la CPU espere más (cuello de botella).
        
    - **Estrategias para Mitigar Lentitud de Memoria:**
        
        - Unidad de pre-búsqueda.
        - Memoria caché (alberga instrucciones anticipadamente).
        - Uso de memorias dinámicas (DDR4) que son más lentas pero almacenan más bits, compensando con artilugios como la caché.
        
    
- **Ciclo de Instrucción:**
    
    - **Inicio de Ejecución:** Toda ejecución arranca con una lectura de memoria (la CPU debe "traerse" la instrucción).
    - **Fases del Ciclo de Instrucción:**
        
        1. **Fase Fetch (Fetch Instruction - FI):** Búsqueda de la instrucción.
            
            - **Proceso:**
                
                - Contenido del **Instruction Pointer (IP)** se transfiere al **MAR** (vía bus de direcciones).
                - Se da la orden de lectura a la memoria.
                - El contenido (instrucción) se vuelca en el **MDR**.
                - El contenido del MDR se transfiere al **Instruction Register (IR)** (registro de la unidad de control que interpreta la instrucción).
                
            - **Tiempo:** Ejemplo: 1 ns (IP a MAR) + 20 ns (espera memoria) + 1 ns (MDR a IR) = 22 ns.
            
        2. **Decode (Decode Opcode):** Decodificación del código de operación.
            
            - **Opcode (Operational Code):** Número que identifica el "verbo" (lo que la CPU debe hacer).
            - **Función:** La unidad de control decodifica el número para saber qué acción realizar (ej. sumar, desplazar, saltar).
            - **Ejemplo:** La unidad 8 plantea una computadora con 16 verbos (16 opcodes diferentes), identificados por 4 bits (0 a 15).
            - **Estructura de la Instrucción:**
                
                - Mínimamente: Código de Operación.
                - Eventualmente: Campo Data o campo de referencia a dato (para instrucciones que operan con datos).
                
            
        3. **Fetch Operand (FO):** Búsqueda del operando (si la instrucción lo requiere).
        4. **Execute (EX):** Ejecución propiamente dicha.
            
            - Realiza la acción indicada por el opcode (ej. suma, resta).
            
        
    - **Actualización del Puntero de Instrucción (IP):**
        
        - **Función del IP:** Sigue la traza del programa, indicando la próxima instrucción a ejecutarse.
        - **Contador Progresivo:** Crece para apuntar a la siguiente instrucción.
        - **Saltos:** Un salto altera el puntero para ir a otra parte del programa.
        - **Tamaño del IP:** Limita la cantidad de direcciones a las que puede acceder (potencial de direccionamiento).
            
            - **Ejemplos:**
                
                - IP de 2 bits: 2^2 = 4 direcciones (0-3).
                - IP de 12 bits: 2^12 = 4096 direcciones (0-4095), si la palabra es de 1 byte, son 4 KB.
                - IP de 16 bits: 2^16 = 65536 direcciones (0-65535), 64 KB.
                - IP de 32 bits: 2^32 = 4 GB.
                - IP de 64 bits: 2^64 = 16 Exabytes (un montón).
                
            
        - **Momento de Actualización:** Varía según el procesador. En Intel, se hace al final de la ejecución.
        - **Instrucciones de Distinto Tamaño (Intel):** El IP crece en función del tamaño de la instrucción (no todas las instrucciones son iguales). La instrucción tiene una "etiqueta" (un número) que indica su tipo/formato y cantidad de bytes.
        - **Instrucciones de Tamaño Uniforme (ej. ARM):** El IP crece de a una palabra, ya que todas las instrucciones tienen el mismo tamaño (ej. 32 bits).
        
    
- **Fin del Programa:**
    
    - El ciclo de instrucción se repite hasta que se encuentra la instrucción de "fin de programa".
    - **Consecuencia de No Poner Fin:** El programa no termina y puede intentar ejecutar cualquier cosa en memoria, llevando a errores (ej. "código de operación inválido", programa abortado).
    - **Compiladores y Errores:** Algunos compiladores detectan la falta de fin de programa; otros, en lenguajes con múltiples ramas de ejecución, pueden no detectarlo y generar un ejecutable que fallará en tiempo de ejecución.