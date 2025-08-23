- **Saludos y Asistencia:** La clase comienza con saludos y una observación sobre la baja asistencia, posiblemente debido a parciales de otras materias.
- **Parciales y Receso:**
    
    - Los estudiantes están con parciales de "análisis matemático y discreto".
    - La materia actual no tendrá parcial antes del receso de invierno.
    - El parcial de esta materia se tomará "al regreso del receso", lo que da "un poco más de margen de tiempo".
    
- **Planificación de la Clase:**
    
    - Se planeaba cubrir "bastantes temas", pero es probable que no se llegue a ver todo.
    - Se contempla una "clase especial más después para ver bien por ahí lo que quede de los prácticos".
    - La clase especial sería "el lunes que viene no el otro".
    - Si se realiza la clase especial, sería bueno hacer "medio tipo un repaso para la segunda parte del parcial así tipo algunas preguntas tipo parcial".
    
- **Contenido de la Clase Actual:**
    
    - Terminar la parte teórica: "segunda parte del modelo de ejecución esta computadora ficticia que estábamos viendo la computadora x".
    - Ver los prácticos: "aclarar por ahí algunas cosas que habían quedado pendientes del práctico 5 y bueno el seis y el siete que sería lo que interesaría más ver que son los prácticos nuevos y por ahí qué s yo más eh complicados".
    
- **Importancia de Preguntar:** Se enfatiza la necesidad de que los estudiantes hagan preguntas, ya sea en clase, en el foro del aula virtual o por correo electrónico, dado que las clases regulares están por terminar.

### **Revisión del Modelo de Ejecución de la Computadora X**

- **Contexto:** Se retoma la Unidad 7, segunda parte, enfocándose en una visión más global del programa básico visto en la clase anterior (suma y promedio de dos números).
- **Concepto Clave: Fetch y Execute:**
    
    - "Nunca se olviden que todas las instrucciones siempre tienen una parte fetch que es fija".
    - El fetch implica: "buscar la instrucción a la memoria, leerla y dejarla dentro de la unidad de control en el registro y donde después se la procesa".
    - La parte de ejecución ("execute") es la que varía.
    - En este modelo simplificado, hay solo dos etapas: fetch y execute, sin solapamiento.
    
- **Ejemplo Detallado de Fetch y Execute (LDA A0A):**
    
    - **Estado Inicial:** Se muestra una tabla con registros (IP, IR, MAR, MDR, AC, SR, Flag F, Flag H) y direcciones de memoria con datos e instrucciones.
        
        - **IP (Instruction Pointer):** Puntero de instrucción, contiene la dirección de la próxima instrucción a ejecutar.
        - **IR (Instruction Register):** Registro dentro de la unidad de control donde se ubica la instrucción para decodificarla.
        - **MAR (Memory Address Register):** Para ubicarse en una posición de memoria (leer/escribir).
        - **MDR (Memory Data Register):** Para leer/escribir datos de/a la memoria.
        - **AC (Accumulator):** Registro acumulador, usado para operaciones aritméticas/lógicas.
        - **SR (Status Register):** Registro de estado (flags).
        - **Flag F:** Habilita el fetch.
        - **Flag H:** No se recuerda su función en el momento.
        - **Memoria:** Lógicamente dividida en datos (A0A, A0B, A0C) e instrucciones (000, 001, 002, 003, 004).
        - **Formato de Instrucción:** Código de operación (4 bits) y parte Data.
        
    - **Fetch de LDA A0A (1 A0A):**
        
        1. `IP -> MAR`: Copia el contenido del IP (000) al MAR.
        2. `Memoria[MAR] -> MDR`: Lee la instrucción (1 A0A) de la memoria y la copia al MDR.
        3. `MDR -> IR`: Copia la instrucción del MDR al IR.
        4. `IP + 1 -> IP`: Actualiza el IP (000 -> 001).
        5. `0 -> Flag F`: Habilita el execute.
        
    - **Execute de LDA A0A:**
        
        1. `Parte Data (IR) -> MAR`: Copia la parte Data (A0A) de la instrucción al MAR.
        2. `Memoria[MAR] -> MDR`: Lee el dato (004) de la memoria y lo copia al MDR.
        3. `MDR -> AC`: Copia el dato del MDR al acumulador (AC = 004).
        4. `1 -> Flag F`: Habilita el fetch siguiente.
        
    
- **Ejemplo Detallado de Fetch y Execute (ADA A0B):**
    
    - **Fetch de ADA A0B (2 A0B):** (Proceso similar al fetch anterior, IP = 001)
        
        1. `IP -> MAR` (001 -> MAR)
        2. `Memoria[MAR] -> MDR` (2 A0B -> MDR)
        3. `MDR -> IR`
        4. `IP + 1 -> IP` (001 -> 002)
        5. `0 -> Flag F`
        
    - **Execute de ADA A0B:**
        
        1. `Parte Data (IR) -> MAR` (A0B -> MAR)
        2. `Memoria[MAR] -> MDR` (002 -> MDR)
        3. `AC + MDR -> AC` (004 + 002 = 006, AC = 006).
        4. **Actualización de Flags:** Se revisan los flags (acarreo, overflow, cero, signo). En este caso, todos en cero.
        5. `1 -> Flag F`
        
    
- **Ejemplo Detallado de Fetch y Execute (SHR):**
    
    - **Fetch de SHR (A XX):** (Proceso similar al fetch anterior, IP = 002)
        
        1. `IP -> MAR` (002 -> MAR)
        2. `Memoria[MAR] -> MDR` (A XX -> MDR)
        3. `MDR -> IR`
        4. `IP + 1 -> IP` (002 -> 003)
        5. `0 -> Flag F`
        
    - **Execute de SHR:**
        
        1. `AC >> 1 -> AC` (006 >> 1 = 003, AC = 003). (División por 2, corrimiento a la derecha).
        2. `1 -> Flag F`
        
    
- **Ejemplo Detallado de Fetch y Execute (STA A0C):**
    
    - **Fetch de STA A0C (3 A0C):** (Proceso similar al fetch anterior, IP = 003)
        
        1. `IP -> MAR` (003 -> MAR)
        2. `Memoria[MAR] -> MDR` (3 A0C -> MDR)
        3. `MDR -> IR`
        4. `IP + 1 -> IP` (003 -> 004)
        5. `0 -> Flag F`
        
    - **Execute de STA A0C:**
        
        1. `Parte Data (IR) -> MAR` (A0C -> MAR)
        2. `AC -> MDR` (003 -> MDR). (Preparación para escribir en memoria).
        3. `MDR -> Memoria[MAR]` (003 -> Memoria[A0C]).
        4. `1 -> Flag F`
        
    
- **Ejemplo Detallado de Fetch y Execute (HTL):**
    
    - **Fetch de HTL (0 XX):** (Proceso similar al fetch anterior, IP = 004)
        
        1. `IP -> MAR` (004 -> MAR)
        2. `Memoria[MAR] -> MDR` (0 XX -> MDR)
        3. `MDR -> IR`
        4. `IP + 1 -> IP` (004 -> 005)
        5. `0 -> Flag F`
        
    - **Execute de HTL:**
        
        1. Inhibe la generación de pulsos de clock (pone todos los T en cero).
        2. Fin de la ejecución del programa.
        
    

### **Tipos de Instrucciones de la Computadora X**

- **Clasificación:**
    
    1. **Instrucciones que afectan datos en memoria:**
        
        - LDA (Load Accumulator): Cargar el acumulador con un dato de memoria. Código: 1.
        - ADA (Add Accumulator): Sumar al acumulador un dato de memoria. Código: 2.
        - STA (Store Accumulator): Guardar el acumulador en memoria. Código: 3.
        - ANA (Logical AND): AND lógico entre acumulador y dato de memoria. Código: 5.
        - XOA (Logical XOR): XOR lógico entre acumulador y dato de memoria. Código: 6.
        
    2. **Instrucciones que afectan datos en registros (no de memoria):**
        
        - HLT (Halt): Inhibir pulsos de clock. Código: 0.
        - CLA (Clear Accumulator): Poner el acumulador en cero. Código: 7.
        - CMA (Complement Accumulator): Complemento restringido del acumulador (invertir bits). Código: 8.
        - INC (Increment Accumulator): Sumar uno al acumulador. Código: 9.
        - SHR (Shift Right): Desplazar a la derecha el acumulador. Código: A.
        - SNA (Jump if Negative): Salto condicional si el signo es negativo (flag S en 1). Código: B.
        - SZA (Jump if Zero): Salto condicional si el resultado es cero (flag Z en 1). Código: C.
        - SCA (Jump if Carry): Salto condicional si hubo acarreo (flag C en 1). Código: D.
        
    3. **Instrucciones de entrada/salida:**
        
        - INP (Input): Capturar dato del exterior al acumulador. Código: E.
        - OUT (Output): Mostrar dato del acumulador al exterior. Código: F.
        
    

### **Fundamentos del Hardware de la Computadora X**

- **Computadora Sincrónica:** Controlada por un sistema de reloj.
- **Ciclo de Reloj / Ciclo Menor:** Intervalo entre dos pulsos consecutivos de reloj.
- **Frecuencia:** Medida en Hertz (Hz), ciclos de reloj por segundo.
- **Ejemplo de Cálculo de Nanosegundos:** Para una CPU de 25 MHz, un ciclo de reloj tarda 40 nanosegundos.
- **Ciclo de Computadora / Ciclo Mayor / Ciclo de Máquina:** Secuencia repetitiva de señales de tiempo (ej. 0 a 15).
- **Ciclo de Memoria:** Tiempo de acceso a la memoria (4 ciclos de reloj en la Computadora X).
- **Clock de la Computadora X:** Genera 8 señales de tiempo, asociado a un registro de desplazamiento circular.

### **Operaciones Aritméticas y Lógicas**

- **ALU (Unidad Aritmético Lógica):** Realiza todas las operaciones.
- **Operaciones sobre un solo dato (en AC):** CLA, CMA, INC, SHR, SHL (no implementada).
- **Operaciones sobre dos datos:**
    
    - Primer dato: Siempre en el acumulador.
    - Segundo dato: En el MDR (leído de memoria).
    - Resultado: Guardado en el acumulador.
    - Ejemplos: ADA, ANA, XOA.
    
- **Actualización del Registro de Estado (Flags):**
    
    - **Flag C (Carry):** Actualizado por el acarreo 15 (el bit más significativo).
    - **Flag S (Sign):** Actualizado por el bit 15 del acumulador (el bit más significativo).
    - **Flag Z (Zero):** Se pone en 1 solo si todos los bits del acumulador son cero.
    - **Flag V (Overflow):** Se activa si los dos últimos acarreos (15 y 14) son diferentes, y los operandos tienen el mismo signo.
    

### **Ejemplos de Códigos en Assembler de la Computadora X**

- **Comparación de Dos Números (mediante resta):**
    
    - **Objetivo:** Comparar dos números (ej. en direcciones A0A y A0B) y saltar a diferentes secciones de código según si son iguales, el primero es menor o el primero es mayor.
    - **Estrategia:** Realizar una resta utilizando el complemento a la base.
    - **Pasos:**
        
        1. `LDA A0B`: Cargar el sustraendo (segundo número) en el acumulador.
        2. `CMA`: Complemento restringido del acumulador.
        3. `INC`: Incrementar el acumulador en 1 (para obtener el complemento a la base).
        4. `ADA A0A`: Sumar el primer número al acumulador (realizando la resta).
        5. `SZA 100`: Salta a la dirección 100 si el resultado es cero (números iguales).
        6. `SNA 200`: Salta a la dirección 200 si el resultado es negativo (primer número menor).
        7. `JMP 300`: Salto incondicional a la dirección 300 (primer número mayor).
        
    
- **Multiplicación por Números No Potencia de 2:**
    
    - **Ejemplo:** Multiplicar por 5 (ej. 6 * 5).
    - **Estrategia:** Desplazamientos (multiplicación por potencias de 2) y sumas.
    - `6 * 5 = 6 * (2 * 2 + 1) = 6 * 4 + 6`.
    - Se realizan dos desplazamientos a la izquierda (multiplicar por 4) y luego se suma el número original.
    
- **Operaciones Lógicas (AND):**
    
    - **Ejemplo:** `Z = A AND B`.
    - `LDA A`: Cargar A en el acumulador.
    - `ANA B`: Realizar AND con B (leído de memoria al MDR).
    - `STA Z`: Guardar el resultado en Z.
    

### **Conceptos de Programación**

- **Programa:** Conjunto ordenado de instrucciones para resolver una tarea.
- **Compiladores:** Traducen código de alto nivel a código binario (ejecutable) antes de la ejecución.
- **Intérpretes:** Traducen código de alto nivel a bajo nivel durante la ejecución (ej. navegador HTML).
- **Ciclo de Desarrollo de Software:** Algoritmo -> Código Fuente -> Programa Objeto -> Programa Ejecutable.
- **Lenguaje de Máquina:** Codificación binaria de instrucciones (unos y ceros). Es específico para cada computadora.
- **Ensamblador:** Set de instrucciones expresado en nemónicos (ej. LDA, ADA). Equivalencia uno a uno con lenguaje de máquina.
- **Lenguaje de Alto Nivel vs. Bajo Nivel:**
    
    - Alto nivel: Una instrucción (ej. `A + B = C`) se traduce a N instrucciones de bajo nivel.
    - Bajo nivel: Nemónicos tienen equivalencia uno a uno con lenguaje de máquina.
    - Todo se traduce a unos y ceros para la computadora.
    

### **Práctico 5 (Circuitos Lógicos)**

- **Ejercicio 1:** Tablas de verdad para compuertas AND, NOR, XOR con tres variables.
- **Ejercicio 2 (Tren de Pulsos):**
    
    - Interpretar gráficos de trenes de pulsos como entradas (0 o 1).
    - Determinar la salida de compuertas lógicas (AND, OR, etc.) en cada instante de tiempo.
    - **Ejemplo:** Para una compuerta AND con entrada A (0, 0, 1, 0, 1, 0, 1, 0) y entrada B (1, 0, 0, 1, 1, 0, 1, 0), la salida sería (0, 0, 0, 0, 1, 0, 1, 0).
    
- **Ejercicio 3 (Conversor BCD 8421 a 2421):**
    
    - Determinar tabla de verdad y funciones de salida (usando formas canónicas, minitérminos).
    - Se vio en clase.
    
- **Ejercicio 4 (Decodificador 8421 a Display 7 Segmentos):**
    
    - Determinar tabla de verdad y funciones de salida.
    - Se vio en clase.
    
- **Ejercicio 5 (Decodificador N por 2 a la N con Habilitación):**
    
    - **Concepto de Habilitación:**
        
        - Si la entrada de habilitación está en 0: El circuito está inactivo, no importa la combinación de entrada, la salida es 0.
        - Si la entrada de habilitación está en 1: El circuito trabaja, decodifica la entrada.
        
    - Para 3 entradas (A, B, C), habrá 2^3 = 8 salidas (F0 a F7).
    - La tabla de verdad mostrará las 8 combinaciones de entrada y la salida correspondiente (solo una salida activa a la vez).
    - Las funciones de salida (ej. F0 = E * A' * B' * C') se usan para construir el circuito.
    
- **Ejercicio 10 (Multiplexor 3 Entradas de Selección, 8 Entradas de Datos):**
    
    - **Función:** Selecciona una de las 8 entradas de datos para transmitirla a una única línea de salida.
    - **Tabla de Verdad:** Las combinaciones de las 3 entradas de selección (C0, C1, C2) determinan qué entrada de datos (D0 a D7) se conecta a la salida (D).
    - **Circuito:** Compuesto por compuertas AND (para seleccionar la entrada) y una compuerta OR final (para combinar las salidas).
    
- **Ejercicio 11 (Demultiplexor 3 Entradas de Selección, 8 Salidas):**
    
    - **Función:** Dirige una única entrada de datos a una de las 8 salidas.
    - **Tabla de Verdad:** Las combinaciones de las 3 entradas de selección (C0, C1, C2) determinan a qué salida (D0 a D7) se dirige la entrada de datos (D).
    - **Circuito:** Compuesto por compuertas AND.
    
- **Ejercicios 7, 8, 9 (Sumadores para Complementos y Conversión):**
    
    - **Objetivo:** Usar semisumadores y sumadores completos para operaciones no convencionales.
    - **Complemento a la Base -1 (Ejercicio 8):**
        
        - **Concepto:** Invertir todos los bits de un número binario.
        - **Implementación:** Usar semisumadores. Una entrada del semisumador se pone en 0, y la otra entrada se conecta al bit del número a complementar a través de un negador.
        
    - **Complemento a la Base (Ejercicio 7):**
        
        - **Concepto:** Complemento a la base -1 + 1.
        - **Implementación:** El mismo circuito del complemento a la base -1, pero sumándole 1 al resultado final (ej. usando un semisumador adicional).
        
    - **Conversor BCD 8421 a BCD Exceso 3 (Ejercicio 9):**
        
        - **Concepto:** BCD Exceso 3 = BCD Puro + 3.
        - **Implementación:** Sumar 3 al número BCD puro utilizando sumadores. Se puede usar un semisumador para el primer bit (sumando 1), y sumadores completos para los siguientes bits (sumando 1 y considerando acarreos).
        
    

### **Práctico 6 (Circuitos Secuenciales)**

- **Ejercicio 1 (Contador en Anillo):**
    
    - Similar a los vistos en clase, pero con un flip-flop más.
    - Se debe analizar el comportamiento del circuito (cambios de estado de los flip-flops) y generar el diagrama de tiempo y el código de cuenta.
    - **Conexión:** La salida Q de un flip-flop se conecta a la entrada J del siguiente, y la salida no-Q a la entrada K del siguiente.
    - **Análisis:** Los estados se arrastran de un flip-flop al siguiente.
    
- **Ejercicio 2 (Contador con Negador):**
    
    - Similar a uno visto en clase, pero con un negador adicional.
    - Analizar el comportamiento y el código de cuenta resultante.
    
- **Ejercicio 3 (Flip-Flops con Estados Iniciales):**
    
    - Analizar los cambios de estado de dos flip-flops con estados iniciales dados.
    - Considerar las entradas asincrónicas (Clear y Preset) y cómo afectan el estado.
    
- **Ejercicio 4 (Contador con Diferentes Tipos de Flip-Flops):**
    
    - Implica el uso de flip-flops tipo T, JK y D.
    - Aunque son diferentes tipos, se espera que se comporten de manera similar en la configuración dada.
    
- **Ejercicio 5 (Contador Sincrónico):**
    
    - El más complejo, similar al contador sincrónico visto en clase.
    - Implica el uso de compuertas lógicas entre los flip-flops.
    
- **Ejercicio 6 (Componentes de Tres Estados):**
    
    - **Concepto:** Permiten o bloquean el paso de un dato.
    - **Funcionamiento:** Si la señal de control (B) está en 1, el dato pasa de A a C. Si B está en 0, el circuito está en "alta impedancia" (Z), bloqueando el paso del dato.
    
- **Ejercicio 7 (Registro Paralelo de 8 bits):**
    
    - **Base:** Similar al registro paralelo de 4 bits visto en clase.
    - **Características:**
        
        - Entradas de datos (D0 a D7).
        - Salidas (Q0 a Q7).
        - **Inicialización:** Usar la entrada asincrónica "Clear" para poner todos los flip-flops en cero.
        - **Habilitar Escritura:** Se habilita a través del pulso de clock.
        
    
- **Ejercicio 8 (Registro Paralelo con Componentes de Tres Estados):**
    
    - Modificar el registro paralelo del ejercicio 7 para incluir componentes de tres estados.
    - Una señal de control ("Mostrar") habilitará la visualización del dato almacenado.
    
- **Ejercicio 9 (Registro en Serie con Componentes de Tres Estados):**
    
    - **Base:** Registro en serie (una única entrada de datos, las salidas Q se conectan a las entradas D del siguiente flip-flop).
    - Incluir componentes de tres estados para controlar la transmisión del dato.
    

### **Preguntas y Respuestas para Exámenes**

#### **Conceptos Fundamentales de la Computadora X**

- **¿Cuáles son las dos etapas principales del ciclo de instrucción en la Computadora X y qué implica cada una?**
    
    - **Respuesta:** Las dos etapas son **Fetch** y **Execute**.
        
        - **Fetch:** Es la etapa fija para todas las instrucciones. Implica buscar la instrucción en la memoria, leerla y dejarla en el registro IR de la unidad de control para su procesamiento.
        - **Execute:** Es la etapa variable, donde se realizan las microoperaciones específicas de la instrucción.
        
    
- **Mencione y describa brevemente los registros principales de la Computadora X.**
    
    - **Respuesta:**
        
        - **IP (Instruction Pointer):** Contiene la dirección de la próxima instrucción a ejecutar.
        - **IR (Instruction Register):** Almacena la instrucción actual para su decodificación y ejecución.
        - **MAR (Memory Address Register):** Contiene la dirección de memoria a la que se va a acceder (leer o escribir).
        - **MDR (Memory Data Register):** Almacena temporalmente los datos leídos o a escribir en la memoria.
        - **AC (Accumulator):** Registro principal para operaciones aritméticas y lógicas.
        - **SR (Status Register):** Contiene los flags de estado (C, S, Z, V) que reflejan el resultado de las operaciones.
        
    
- **¿Cómo se actualizan los flags C, S, Z y V en el Registro de Estado (SR) después de una operación aritmética o lógica en la Computadora X?**
    
    - **Respuesta:**
        
        - **Flag C (Carry):** Se actualiza con el acarreo del bit más significativo (acarreo 15).
        - **Flag S (Sign):** Se actualiza con el valor del bit más significativo (bit 15) del acumulador.
        - **Flag Z (Zero):** Se pone en 1 solo si el resultado de la operación es cero (todos los bits del acumulador son cero).
        - **Flag V (Overflow):** Se activa si los dos últimos acarreos (15 y 14) son diferentes Y los operandos tienen el mismo signo.
        
    
- **Explique la diferencia entre un compilador y un intérprete.**
    
    - **Respuesta:**
        
        - **Compilador:** Traduce el código fuente de alto nivel a código binario (ejecutable) _antes_ de la ejecución del programa. Genera un archivo ejecutable independiente.
        - **Intérprete:** Traduce y ejecuta el código fuente de alto nivel línea por línea _durante_ la ejecución del programa. No genera un archivo ejecutable independiente.
        
    
- **¿Qué es el lenguaje de máquina y cuál es su relación con el ensamblador?**
    
    - **Respuesta:** El **lenguaje de máquina** son las instrucciones expresadas en codificación binaria (unos y ceros) que la computadora entiende directamente. El **ensamblador** es una representación simbólica (nemónicos) de estas instrucciones de máquina, con una equivalencia uno a uno. El ensamblador es más legible para los humanos, pero debe ser traducido a lenguaje de máquina para su ejecución.
    

#### **Instrucciones de la Computadora X**

- **Identifique el código de operación de las siguientes instrucciones de la Computadora X: LDA, ADA, STA, HLT, SHR, INP.**
    
    - **Respuesta:**
        
        - LDA: 1
        - ADA: 2
        - STA: 3
        - HLT: 0
        - SHR: A
        - INP: E
        
    
- **¿Qué instrucción de la Computadora X se utiliza para invertir todos los bits del acumulador? ¿Cuál es su código de operación?**
    
    - **Respuesta:** La instrucción es **CMA** (Complement Accumulator). Su código de operación es **8**.
    
- **Describa la función de las instrucciones de salto condicional SZA, SNA y SCA.**
    
    - **Respuesta:**
        
        - **SZA (Jump if Zero):** Salta a una dirección de memoria específica si el flag Z (Zero) del registro de estado está en 1 (es decir, si el resultado de la última operación fue cero).
        - **SNA (Jump if Negative):** Salta a una dirección de memoria específica si el flag S (Sign) del registro de estado está en 1 (es decir, si el resultado de la última operación fue negativo).
        - **SCA (Jump if Carry):** Salta a una dirección de memoria específica si el flag C (Carry) del registro de estado está en 1 (es decir, si hubo un acarreo en la última operación).
        
    
- **¿Cómo se implementa una resta en la Computadora X, dado que no tiene una instrucción de resta directa? Proporcione un ejemplo con las instrucciones.**
    
    - **Respuesta:** Una resta (X - Y) se implementa utilizando el complemento a la base de Y y sumándolo a X.
        
        - **Pasos:**
            
            1. Cargar el sustraendo (Y) en el acumulador: `LDA Y`
            2. Calcular el complemento restringido de Y: `CMA`
            3. Incrementar el acumulador en 1 para obtener el complemento a la base: `INC`
            4. Sumar el minuendo (X) al acumulador: `ADA X`
            
        - **Ejemplo:** Para calcular `A - B`:
	    ```sh
	    LDA B   ; Carga B en el acumulador
		CMA     ; Complemento restringido de B
		INC     ; Complemento a la base de B
		ADA A   ; Suma A al complemento a la base de B (realiza A - B)
	    ```
- **Explique cómo se puede realizar una multiplicación por un número que no es potencia de 2 (ej. por 5) en la Computadora X, utilizando las instrucciones disponibles.**
    
    - **Respuesta:** Se descompone la multiplicación en una combinación de desplazamientos (multiplicaciones por potencias de 2) y sumas.
    - **Ejemplo (Multiplicar por 5):** `Número * 5 = Número * (2 * 2 + 1) = Número * 4 + Número`.
        
        - Se realizarían dos desplazamientos a la izquierda (SHL, si estuviera disponible, o dos SHR si se invierte la lógica) para multiplicar por 4.
        - Luego, se sumaría el número original al resultado.
        - **Instrucciones (ejemplo conceptual, asumiendo SHL):**
	    ```sh
	    LDA B   ; Carga B en el acumulador
		CMA     ; Complemento restringido de B
		INC     ; Complemento a la base de B
		ADA A   ; Suma A al complemento a la base de B (realiza A - B)
	    ```
#### **Circuitos Lógicos y Secuenciales**

- **¿Qué función cumple la entrada de habilitación en un decodificador N por 2 a la N? ¿Qué sucede si está en 0 y si está en 1?**
    
    - **Respuesta:** La entrada de habilitación (Enable) controla si el decodificador está activo o inactivo.
        
        - **Si está en 0:** El decodificador está inactivo. Todas sus salidas permanecen en 0, independientemente de las entradas.
        - **Si está en 1:** El decodificador está activo y funciona normalmente, decodificando la combinación de entrada y activando la salida correspondiente.
        
    
- **Describa la diferencia fundamental entre un multiplexor y un demultiplexor.**
    
    - **Respuesta:**
        
        - **Multiplexor:** Tiene múltiples entradas de datos y una única salida. Utiliza entradas de selección para elegir cuál de las entradas de datos se transmite a la salida. Es un "selector de datos".
        - **Demultiplexor:** Tiene una única entrada de datos y múltiples salidas. Utiliza entradas de selección para dirigir el dato de la entrada a una de las salidas específicas. Es un "distribuidor de datos".
        
    
- **¿Cómo se implementaría un circuito para calcular el complemento a la base -1 de un número binario de 4 bits utilizando semisumadores?**
    
    - **Respuesta:** Para cada bit del número, se utiliza un semisumador. Una de las entradas del semisumador se conecta a 0, y la otra entrada se conecta al bit del número a través de un negador. Esto invierte cada bit, logrando el complemento a la base -1.
    
- **Explique cómo se puede convertir un número BCD 8421 a BCD Exceso 3 utilizando sumadores.**
    
    - **Respuesta:** La conversión de BCD 8421 a BCD Exceso 3 implica sumar 3 al número BCD 8421. Esto se puede lograr utilizando una combinación de semisumadores y sumadores completos, donde se "suman" los bits correspondientes al valor binario de 3 (0011).
    
- **¿Cuál es la función de las entradas Clear y Preset en un flip-flop?**
    
    - **Respuesta:** Son entradas asincrónicas que permiten establecer el estado inicial del flip-flop independientemente de la señal de clock.
        
        - **Clear:** Pone la salida Q del flip-flop en 0.
        - **Preset:** Pone la salida Q del flip-flop en 1.
        
    
- **Describa el concepto de un componente de tres estados (Tri-state buffer) y su utilidad en circuitos digitales.**
    
    - **Respuesta:** Un componente de tres estados es un tipo de buffer que tiene una entrada de datos, una salida y una entrada de control (habilitación). A diferencia de un buffer normal, su salida puede estar en uno de tres estados: alto (1), bajo (0) o alta impedancia (Z).
        
        - **Utilidad:** Permite conectar múltiples dispositivos a una misma línea de bus sin que interfieran entre sí. Cuando la entrada de control está activa, el dato pasa. Cuando está inactiva, la salida entra en alta impedancia, desconectando efectivamente el dispositivo del bus.
        
    

#### **Preguntas de Aplicación y Análisis (Tipo Práctico)**

- **Dado un contador en anillo con 4 flip-flops JK y un estado inicial de Q3Q2Q1Q0 = 0000, dibuje el diagrama de tiempo y determine el código de cuenta para los primeros 5 pulsos de reloj.**
    
    - **Respuesta:** (Requiere dibujar el diagrama y la tabla de estados, siguiendo la lógica de conexión del contador en anillo).
    
- **Se le proporciona un código en assembler de la Computadora X. Analice el código y determine el valor final del acumulador y el contenido de una dirección de memoria específica después de su ejecución.**
    
    - **Respuesta:** (Requiere seguir el flujo de ejecución de las instrucciones, actualizando los valores de los registros y la memoria).
    
- **Diseñe un circuito que implemente un registro en serie de 4 bits con una entrada de habilitación para la escritura, utilizando flip-flops D y componentes de tres estados.**
    
    - **Respuesta:** (Requiere dibujar el circuito, mostrando las conexiones de los flip-flops D en serie, la entrada de clock, la entrada Clear/Preset y el componente de tres estados controlando la entrada de datos).
    

---

**Nota:** La transcripción original contenía algunas imprecisiones en la numeración de los ejercicios del práctico 5 y 6, así como en la descripción de algunos conceptos. Se ha intentado corregir y clarificar estos puntos en la estructura y las respuestas para examen. Se recomienda a los estudiantes revisar el material de clase (PowerPoints, etc.) para una comprensión completa y precisa.