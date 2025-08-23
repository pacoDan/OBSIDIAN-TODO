### **II. Circuitos Contadores (Sincrónicos y Asincrónicos)**

- **Contador Sincrónico:**
    
    - **Mecanismo:** Similar a otros contadores, pero más complejo de analizar debido a la compuerta AND.
    - **Activación:** Todos los flip-flops se activan al mismo tiempo.
    - **Ventaja:** No presenta problemas de acumulación de retardos de tiempo (es más rápido).
    - **Desventaja:** Más difícil de implementar.
    - **Análisis de Funcionamiento (Ejemplo):**
        
        - **Estado Inicial:** Todas las salidas Q en cero.
        - **Primer Pulso de Clock (Flanco Negativo):**
            
            - **Flip-flop JK (entradas en 1):** Conmuta el estado (de 0 a 1).
            - **Compuerta AND:** Toma el Q anterior y la entrada del flip-flop anterior.
            - **Flip-flop JK (entradas en 00):** Mantiene el estado.
            
        - **Proceso Iterativo:** Se repite el análisis para cada pulso de clock, registrando los estados de las salidas Q y las entradas de la compuerta AND.
        - **Finalización de la Cuenta:** Se llega al estado inicial (000).
        
    - **Representación:**
        
        - **Diagrama de Tiempo:** Muestra los cambios de estado en los flancos negativos del clock.
        - **Tabla de Código de Cuenta:** En este caso, cuenta en binario puro del 0 al 7.
        
    
- **Contador Asincrónico:**
    
    - **Características:** También cuenta en binario puro y es activado por flanco negativo.
    - **Diferencia con Sincrónico:** El clock solo afecta al primer flip-flop; el resto de los flip-flops se conectan a la salida Q del flip-flop anterior.
    - **Problema:** Acumulación de retardos de tiempo (más lento).
    

### **III. Modelo de Ejecución (Unidad 7)**

- **Importancia:** Permite entender los componentes internos de una computadora y cómo se procesa una instrucción.
- **Diseño de una Computadora Digital:**
    
    - **Definición:** Organización de módulos de hardware interconectados por rutas de control y datos.
    - **Función:** Permitir el flujo de señales binarias para transformar datos de entrada en información útil.
    - **Representación:** Módulos como "cajas negras".
    - **Transmisión de Datos:** A través de buses (bus de datos, bus de control, bus de direcciones).
    
- **Microoperaciones:**
    
    - **Definición:** Operación aplicada a un registro (abreviatura: μop).
    - **Activación:** Sincronizadas por los pulsos de clock.
    
- **Ejemplo de Módulo Sumador:**
    
    - **Registros:** A y B (operandos), C (resultado).
    - **Señal de Control (S):** Habilita el módulo de suma y genera microoperaciones.
    
- **Programación en Lenguaje de Máquina:**
    
    - **Concepto:** Implica conocer el tipo de instrucciones en código de máquina (binario) que obedece la computadora.
    - **Assembler:** Lenguaje simbólico de bajo nivel para simplificar la tarea de recordar secuencias binarias.
        
        - **Nemónico:** Abreviatura de tres letras para la instrucción.
        - **Relación con Hardware:** Cada computadora tiene su propio assembler, íntimamente relacionado con su hardware.
        
    - **Lenguajes de Bajo Nivel:** Permiten programar rutinas muy básicas (ej. interacción con teclado/monitor) que no se podrían implementar en alto nivel.
    
- **Traducción de Lenguajes:**
    
    - **Alto Nivel a Código de Máquina:** Más compleja, realizada por un compilador (traduce a otro lenguaje intermedio).
    - **Assembler a Código de Máquina:** Más sencilla, realizada por un ensamblador (traducción uno a uno).
    
- **Almacenamiento de Programas en Memoria:**
    
    - **Instrucciones y Datos:** Se guardan en binario en direcciones de memoria.
    - **Ejemplo:** Instrucciones `LDA`, `ADA`, `STA` con sus códigos binarios y direcciones de memoria.
    
- **Código de Instrucción (Opcode):**
    
    - **Definición:** Combinación de bits que la unidad de control de la CPU interpreta para generar microoperaciones.
    - **Formato de Instrucción (Computadora X):**
        
        - **Código de Operación (COP):** 4 bits.
        - **Parte Data:** 12 bits (generalmente una dirección de memoria).
        - **Total:** 16 bits.
        
    
- **División Lógica de la Memoria:**
    
    - **Memoria de Instrucciones:** Para guardar las instrucciones del programa.
    - **Memoria de Datos:** Para guardar los datos involucrados en las instrucciones.
    - **Modelos Reales:** Incluyen un segmento de pila (para subrutinas, estados internos de CPU).
    
- **Procesamiento de Instrucciones:**
    
    - **Unidad de Control:** Lee una instrucción de memoria, la guarda en el Registro de Instrucción (IR).
    - **Interpretación:** Se interpreta el COP para ver si afecta un dato, buscarlo si es necesario, y generar microoperaciones.
    - **Estado de Ejecución:** La instrucción está en estado de ejecución cuando está en el IR.
    
- **Modelo de Von Neumann (Computadora X):**
    
    - **Características:**
        
        - **Memoria:** RAM, 4 KB (4096 palabras) de 16 bits cada una.
        - **Direcciones:** 12 bits (000h a FFFh).
        - **División Lógica:** Memoria de datos y memoria de programa.
        - **Procesamiento:** Monoprogramación (un programa a la vez).
        
    - **Esquema Interno (Componentes):**
        
        - **CPU:** Unidad de Control (UC) y Unidad Aritmético Lógica (ALU).
        - **Clock:** Sincroniza operaciones.
        - **Registros de la UC:**
            
            - **IP (Instruction Pointer):** Contiene la dirección de la próxima instrucción a ejecutar.
            - **IR (Instruction Register):** Almacena la instrucción leída de memoria.
            
        - **Memoria Principal:**
            
            - **MAR (Memory Address Register):** Almacena la dirección de memoria a acceder.
            - **MDR (Memory Data Register):** Almacena los datos leídos o a escribir en memoria.
            
        - **Registros de la ALU:**
            
            - **Acumulador:** Registro principal para operaciones y resultados.
            - **Status Register:** Actualiza flags (signo, acarreo, cero, overflow).
            
        - **Buses:** Control, Datos, Direcciones.
        
    
- **Fases del Ciclo de Instrucción:**
    
    - **Fetch (Búsqueda):** Buscar la instrucción en memoria, leerla y dejarla lista en la UC.
    - **Execute (Ejecución):** Interpretar el COP, buscar datos si es necesario, y generar microoperaciones.
    - **Alternancia:** La UC alterna entre Fetch y Execute (Ciclo de Instrucción).
    
- **Fase Fetch (Detalle):**
    
    - **Microoperaciones (Orden y Función):**
        
        1. **IP → MAR:** Copiar el contenido del IP al MAR (apuntar a la dirección de la instrucción).
        2. **Memoria[MAR] → MDR:** Leer la instrucción de memoria y copiarla al MDR.
        3. **MDR → IR:** Copiar la instrucción del MDR al IR (para interpretación).
        4. **IP + 1 → IP:** Actualizar el IP para apuntar a la siguiente instrucción.
        5. **0 → F (Flag):** Poner el flag F en cero para habilitar la fase Execute.
        
    - **Características:** Es idéntica para todas las instrucciones.
    - **Suposiciones de Tiempo:**
        
        - Lectura/escritura de memoria: 4 pulsos de clock.
        - Ejecución de instrucción: No más de 8 pulsos de clock.
        
    - **Implementación (Hardware):** Compuertas AND que combinan el flag F (en 1 para Fetch) con los instantes de tiempo (T0, T1, T5, T7).
    
- **Fase Execute (Detalle):**
    
    - **Variabilidad:** Las microoperaciones varían según la instrucción.
    - **Implementación (Hardware):** Compuertas AND que combinan el flag F (en 0 para Execute, por lo que se usa negado), los instantes de tiempo, y el código de operación (COP).
    
- **Ejemplo de Programa (Suma y Promedio):**
    
    - **Objetivo:** Sumar dos datos y calcular su promedio.
    - **Instrucciones Utilizadas (Computadora X):**
        
        - **LDA (Load Accumulator):** Carga el acumulador con el dato de una dirección de memoria (COP: 1h).
        - **ADA (Add Accumulator):** Suma al acumulador el dato de una dirección de memoria (COP: 2h).
        - **SHR (Shift Right):** Desplaza el acumulador un bit a la derecha (divide por 2) (COP: Ah). No involucra datos.
        - **STA (Store Accumulator):** Guarda el contenido del acumulador en una dirección de memoria (COP: 3h).
        - **HTL (Halt):** Fin de programa (inhibe pulsos de clock).
        
    - **Ejecución de Instrucciones (Fase Execute):**
        
        - **LDA:**
            
            1. **Data (IR) → MAR:** Copia la dirección del dato al MAR.
            2. **Memoria[MAR] → MDR:** Lee el dato de memoria al MDR.
            3. **MDR → Acumulador:** Carga el dato en el acumulador.
            4. **1 → F (Flag):** Habilita el Fetch.
            
        - **ADA:**
            
            1. **Data (IR) → MAR:** Copia la dirección del dato al MAR.
            2. **Memoria[MAR] → MDR:** Lee el dato de memoria al MDR.
            3. **Acumulador + MDR → Acumulador:** Suma y guarda el resultado en el acumulador.
            4. **1 → F (Flag):** Habilita el Fetch.
            
        - **SHR:**
            
            1. **Acumulador (desplazado) → Acumulador:** Desplaza el contenido del acumulador.
            2. **1 → F (Flag):** Habilita el Fetch.
            
        - **STA:**
            
            1. **Data (IR) → MAR:** Copia la dirección de destino al MAR.
            2. **Acumulador → MDR:** Copia el contenido del acumulador al MDR.
            3. **MDR → Memoria[MAR]:** Escribe el dato del MDR en memoria.
            4. **1 → F (Flag):** Habilita el Fetch.
            
        - **HTL:** Inhibe la generación de pulsos de clock.
        
    

---

## Preguntas y Respuestas para Exámenes

### **Circuitos Contadores**

- **Pregunta:** ¿Cuál es la principal diferencia entre un contador sincrónico y uno asincrónico en términos de activación de flip-flops y problemas de retardo?
    
    - **Respuesta:**
        
        - **Contador Sincrónico:** Todos los flip-flops se activan simultáneamente con el mismo pulso de clock. Su principal ventaja es que **no presenta problemas de acumulación de retardos de tiempo**, lo que lo hace más rápido.
        - **Contador Asincrónico:** El clock solo afecta al primer flip-flop, y los siguientes flip-flops se activan con la salida del flip-flop anterior. Su principal desventaja es que **sí presenta acumulación de retardos de tiempo**, lo que lo hace más lento.
        
    
- **Pregunta:** Describa el proceso de análisis de un contador sincrónico, incluyendo cómo se determina el estado de los flip-flops JK y el papel de las compuertas AND.
    
    - **Respuesta:** El análisis de un contador sincrónico comienza con un estado inicial dado (generalmente todas las salidas Q en cero). Para cada pulso de clock (generalmente flanco negativo):
        
        - **Flip-flop JK:** Se evalúan sus entradas J y K. Si ambas están en 1, el flip-flop conmuta (cambia al estado opuesto). Si ambas están en 0, mantiene el estado anterior.
        - **Compuerta AND:** Sus entradas suelen ser las salidas Q anteriores de otros flip-flops. La salida de la compuerta AND influye en las entradas J y K de los siguientes flip-flops, determinando su comportamiento.
        - **Proceso:** Se registra el nuevo estado de cada salida Q y se utiliza para determinar las entradas de las compuertas AND y los siguientes flip-flops en el siguiente pulso de clock, hasta que el contador regresa a su estado inicial.
        
    
- **Pregunta:** ¿Qué significa que un contador cuente en "binario puro"?
    
    - **Respuesta:** Que el contador representa los números en su forma binaria estándar, donde cada estado consecutivo del contador corresponde a la siguiente secuencia binaria natural (ej. 000, 001, 010, 011, etc.).
    

### **Modelo de Ejecución**

- **Pregunta:** Defina "microoperación" y explique cómo se activan en el contexto del diseño de una computadora digital.
    
    - **Respuesta:** Una **microoperación** es una operación elemental aplicada a un registro dentro de la CPU. Se activan en un instante de tiempo específico, **sincronizadas por los pulsos de clock** generados por el reloj de la computadora.
    
- **Pregunta:** Explique la diferencia entre un compilador y un ensamblador en el proceso de traducción de programas a código de máquina.
    
    - **Respuesta:**
        
        - **Compilador:** Traduce programas escritos en **lenguajes de alto nivel** (más cercanos al lenguaje humano) a código de máquina. Este proceso es más complejo, ya que una instrucción de alto nivel puede traducirse en múltiples instrucciones de código de máquina.
        - **Ensamblador:** Traduce programas escritos en **lenguaje ensamblador** (lenguaje de bajo nivel, con nemónicos) a código de máquina. Este proceso es más sencillo y directo, con una traducción uno a uno entre las instrucciones ensamblador y las instrucciones de máquina.
        
    
- **Pregunta:** Describa la división lógica de la memoria en el modelo de la Computadora X y mencione una división adicional presente en modelos reales.
    
    - **Respuesta:** En el modelo de la Computadora X, la memoria se divide lógicamente en dos partes:
        
        - **Memoria de Instrucciones:** Donde se almacenan las instrucciones del programa.
        - **Memoria de Datos:** Donde se almacenan los datos que serán procesados por las instrucciones. En modelos reales, existe una **tercera división adicional llamada segmento de pila**, que se utiliza para almacenar direcciones de retorno de subrutinas, estados internos de la CPU, y otros datos temporales.
        
    
- **Pregunta:** Identifique los componentes principales de la CPU en el esquema interno de la Computadora X y describa brevemente la función de cada uno.
    
    - **Respuesta:** Los componentes principales de la CPU en la Computadora X son:
        
        - **Unidad de Control (UC):** Encargada de gestionar el procesamiento de la información. Lee las instrucciones de memoria, las interpreta y genera las microoperaciones necesarias para su ejecución.
        - **Unidad Aritmético Lógica (ALU):** Realiza las operaciones aritméticas (suma, resta, etc.) y lógicas (AND, OR, NOT, etc.) sobre los datos.
        
    
- **Pregunta:** Explique las dos fases principales del ciclo de instrucción (Fetch y Execute) y cómo se alternan.
    
    - **Respuesta:** El ciclo de instrucción se divide en dos fases principales:
        
        - **Fetch (Búsqueda):** La unidad de control busca la instrucción en la memoria, la lee y la prepara para su interpretación.
        - **Execute (Ejecución):** La unidad de control interpreta el código de operación de la instrucción, busca los datos si es necesario y genera las microoperaciones para llevar a cabo la acción especificada por la instrucción. Estas fases se **alternan continuamente** en el procesamiento de un programa: se busca una instrucción, se ejecuta; se busca la siguiente, se ejecuta, y así sucesivamente hasta el final del programa.
        
    
- **Pregunta:** Enumere y describa las microoperaciones que componen la fase Fetch en la Computadora X. ¿Por qué esta fase es idéntica para todas las instrucciones?
    
    - **Respuesta:** Las microoperaciones de la fase Fetch son:
        
        1. **IP → MAR:** El contenido del Instruction Pointer (dirección de la próxima instrucción) se copia al Memory Address Register, apuntando a la ubicación de la instrucción en memoria.
        2. **Memoria[MAR] → MDR:** La instrucción ubicada en la dirección apuntada por el MAR se lee de la memoria y se copia al Memory Data Register.
        3. **MDR → IR:** La instrucción del MDR se copia al Instruction Register, donde será interpretada.
        4. **IP + 1 → IP:** El Instruction Pointer se incrementa en 1 para apuntar a la siguiente instrucción en secuencia.
        5. **0 → F (Flag):** El flag F (de fase) se pone en cero para habilitar la fase Execute. Esta fase es idéntica para todas las instrucciones porque su propósito es siempre el mismo: **buscar la instrucción en memoria, leerla y prepararla para su posterior interpretación y ejecución**, independientemente de la acción específica que realice la instrucción.
        
    
- **Pregunta:** En el contexto de la fase Execute, ¿cómo se implementa el control de las microoperaciones en hardware, considerando las variables de tiempo, estado y código de operación?
    
    - **Respuesta:** El control de las microoperaciones en la fase Execute se implementa utilizando compuertas lógicas (generalmente AND) que combinan tres tipos de variables:
        
        - **Control de la Fase (Flag F):** Como en Execute el flag F está en 0, se utiliza su negado (F') como entrada a las compuertas AND.
        - **Instantes de Tiempo (T0, T1, T5, T7, etc.):** Cada microoperación se activa en un instante de tiempo específico.
        - **Código de Operación (COP):** A diferencia de la fase Fetch, el COP es crucial aquí. La salida del decodificador del COP (que identifica la instrucción) se utiliza como entrada a las compuertas AND, asegurando que solo las microoperaciones relevantes para la instrucción actual se activen en el momento correcto.
        
    
- **Pregunta:** Describa el propósito de la instrucción `HTL` (Halt) en la Computadora X y cómo logra su efecto.
    
    - **Respuesta:** La instrucción `HTL` (Halt) tiene como propósito **finalizar la ejecución del programa**. Logra su efecto al **inhibir la generación de los pulsos de clock**. Al detener los pulsos de clock, la computadora deja de generar microoperaciones, deteniendo así todo procesamiento y la ejecución del programa.