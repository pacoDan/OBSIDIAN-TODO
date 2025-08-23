A continuación, se presenta la estructura de la transcripción, recopilando preguntas y respuestas relevantes para exámenes, con un enfoque en los detalles proporcionados:

### **I. Circuitos Secuenciales vs. Circuitos Combinacionales**

- **Pregunta de Examen:** ¿Cuál es la principal diferencia entre los circuitos secuenciales y los circuitos combinacionales?
    
    - **Respuesta:**
        
        - **Circuitos Combinacionales:**
            
            - El bloque básico para su construcción son las compuertas lógicas.
            - La salida depende únicamente de la combinación actual de las entradas.
            
        - **Circuitos Secuenciales:**
            
            - La característica principal es que hay una retroalimentación de la salida a la entrada.
            - El bloque básico son los "flip-flops" (FF).
            - La salida depende de la combinación actual de las entradas y de los estados anteriores (tienen memoria).
            
        
    

### **II. Flip-Flops (FF)**

- **Pregunta de Examen:** ¿Qué son los flip-flops y cuál es su función principal?
    
    - **Respuesta:**
        
        - **Definición:** Son el bloque básico de los circuitos secuenciales. Internamente se hacen con compuertas, pero se representan como "cajas negras".
        - **Función Principal:** Tienen características de memoria, lo que les permite almacenar un bit de información.
        - **Otros Nombres:** También se les conoce como "cerrojos", "multivibradores biestables" o "binarios".
        - **Construcción:** Se pueden construir a partir de compuertas (ej. NAND) o comprar como circuitos integrados.
        - **Interconexión:** Se interconectan para formar circuitos lógicos secuenciales que almacenan datos, generan tiempos, cuentan y siguen secuencias.
        
    
- **Pregunta de Examen:** Mencione los cuatro tipos principales de flip-flops.
    
    - **Respuesta:**
        
        - RS
        - JK
        - D
        - T
        
    

#### **A. Flip-Flop RS (Set-Reset)**

- **Pregunta de Examen:** Describa el funcionamiento del flip-flop RS asincrónico, incluyendo sus entradas, salidas y modos de operación.
    
    - **Respuesta:**
        
        - **Entradas:** Set (S) y Reset (R).
        - **Salidas:** Q (salida normal) y Q negado (complemento de Q).
        - **Representación:** Diagrama de bloque (caja negra).
        - **Construcción:** Se puede implementar con compuertas NOR (o NAND).
        - **Retroalimentación:** Se toma una muestra de la salida Q y se reinserta en la entrada de la otra compuerta, y lo mismo con Q negado.
        - **Análisis:** Más complejo que los combinacionales debido a la retroalimentación; requiere diagramas de tiempo para considerar el tiempo y los estados anteriores/presentes.
        - **Tabla de Verdad (Asincrónico):**
            
            - **S=1, R=0 (SET):** Q se pone en 1.
            - **S=0, R=1 (RESET):** Q se pone en 0.
            - **S=0, R=0 (MANTENIMIENTO):** Mantiene el valor anterior de Q.
            - **S=1, R=1 (PROHIBIDA):** Produce una salida indeterminada, el circuito se comporta de manera inestable.
            
        
    
- **Pregunta de Examen:** Explique cómo se analiza un flip-flop RS asincrónico utilizando un diagrama de tiempo.
    
    - **Respuesta:**
        
        - Se divide el tiempo en pulsos o instantes.
        - Se analizan las entradas R y S a través del tiempo.
        - Se determina el estado de Q y Q negado en cada instante, considerando el modo de operación (SET, RESET, MANTENIMIENTO).
        - **Ejemplo de Análisis:**
            
            - Si R=0, S=0 y Q venía en 0, Q sigue en 0.
            - Si R=0, S=1 (SET), Q se pone en 1.
            - Si R=0, S=0 (MANTENIMIENTO) y Q estaba en 1, Q sigue en 1.
            - Si R=1, S=0 (RESET), Q se pone en 0.
            
        
    
- **Pregunta de Examen:** ¿Cuál es la diferencia entre un flip-flop asincrónico y uno sincrónico? ¿Por qué se prefieren los sincrónicos?
    
    - **Respuesta:**
        
        - **Asincrónico:** Responde inmediatamente a los cambios en las entradas.
            
            - **Desventaja:** Comportamiento muy inestable, no hay control sobre el momento de los cambios de estado. No se utilizan en la práctica.
            
        - **Sincrónico:** Los cambios de estado (valores de Q) solo se pueden dar en un período de tiempo determinado.
            
            - **Ventaja:** Mayor estabilidad y control.
            - **Mecanismo:** Incluyen una tercera señal llamada "reloj" o "clock" que indica los intervalos de tiempo en los que se pueden realizar los cambios. Fuera del pulso de clock, el circuito permanece inactivo.
            - **Implementación (RS Sincrónico):** Se añade una compuerta AND en cada rama de entrada (R y S) que recibe la señal de clock.
                
                - Si Clock=0, las salidas de las AND son 0, y el flip-flop mantiene su estado anterior.
                - Si Clock=1, las entradas R y S pasan directamente a las compuertas NOR (o NAND) internas, y el flip-flop opera según su tabla de verdad asincrónica.
                
            
        
    
- **Pregunta de Examen:** Explique el concepto de "flanco" en las señales de clock y su importancia en los flip-flops.
    
    - **Respuesta:**
        
        - **Definición:** Son las transiciones de la señal de clock.
            
            - **Flanco de Bajada (Negativo):** Transición de nivel alto a nivel bajo.
            - **Flanco de Subida (Positivo):** Transición de nivel bajo a nivel alto.
            
        - **Importancia:** Para minimizar problemas de ruido y asegurar cambios de estado precisos, se utilizan flip-flops habilitados por flanco. El cambio se produce solo en el momento del flanco (positivo o negativo), ignorando ruidos o pulsos intermedios.
        - **Simbología:**
            
            - Flanco Positivo: Triángulo en la entrada de clock.
            - Flanco Negativo: Círculo y triángulo en la entrada de clock.
            
        
    
- **Pregunta de Examen:** ¿Para qué se utilizan las entradas asincrónicas Clear y Preset en los flip-flops?
    
    - **Respuesta:**
        
        - **Función:** Se utilizan para inicializar el flip-flop en un estado determinado, independientemente de las entradas sincrónicas.
        - **Clear:** Pone la salida Q en 0.
        - **Preset:** Pone la salida Q en 1.
        - **Uso:** Normalmente se usan solo para la inicialización; después, el circuito funciona de manera sincrónica.
        
    

#### **B. Flip-Flop JK**

- **Pregunta de Examen:** ¿Cuál es la principal ventaja del flip-flop JK sobre el RS? Describa su tabla de verdad.
    
    - **Respuesta:**
        
        - **Ventaja Principal:** Elimina el problema de la entrada prohibida (1,1) del RS. Se considera un flip-flop universal, ya que se pueden construir otros flip-flops a partir de él.
        - **Comportamiento:** J equivale a Set, K equivale a Reset.
        - **Tabla de Verdad (Sincrónico, Clock=1):**
            
            - **J=0, K=0 (MANTENIMIENTO):** Mantiene el estado anterior de Q.
            - **J=0, K=1 (RESET):** Q se pone en 0.
            - **J=1, K=0 (SET):** Q se pone en 1.
            - **J=1, K=1 (CONMUTACIÓN):** Q toma el valor complementado del Q anterior (si Q era 0, ahora es 1; si Q era 1, ahora es 0).
            
        - **Implementación:** Se puede construir a partir de un RS añadiendo compuertas AND en las entradas J y K, conectadas a Q y Q negado del RS.
        
    

#### **C. Flip-Flop D (Delay)**

- **Pregunta de Examen:** Describa el funcionamiento del flip-flop D y su aplicación principal.
    
    - **Respuesta:**
        
        - **Entradas:** Una única entrada de datos (D) y la entrada de clock.
        - **Salidas:** Q y Q negado.
        - **Función:** Actúa como un "retardo". La entrada D se reescribe en la salida Q en el próximo pulso de clock.
        - **Tabla de Verdad (Sincrónico, Clock=1):**
            
            - **D=0:** Q se pone en 0.
            - **D=1:** Q se pone en 1.
            
        - **Implementación:** Se puede construir a partir de un RS o un JK.
            
            - **Con RS:** D se conecta a S, y D negado se conecta a R.
            - **Con JK:** D se conecta a J, y D negado se conecta a K.
            
        
    

#### **D. Flip-Flop T (Toggle)**

- **Pregunta de Examen:** Explique el funcionamiento del flip-flop T y su modo de operación principal.
    
    - **Respuesta:**
        
        - **Entradas:** Una única entrada de datos (T) y la entrada de clock.
        - **Salidas:** Q y Q negado.
        - **Función:** Es un flip-flop de conmutación.
        - **Tabla de Verdad (Sincrónico, Clock=1):**
            
            - **T=0:** Mantiene el valor anterior de Q.
            - **T=1 (CONMUTACIÓN):** Q toma el valor complementado del Q anterior.
            
        - **Implementación:** Se construye a partir de un JK uniendo sus dos entradas (J y K) y conectándolas a la entrada T.
        
    

### **III. Aplicaciones de los Flip-Flops: Registros**

- **Pregunta de Examen:** ¿Cuál es la función digital de los registros y cómo se relacionan con los flip-flops?
    
    - **Respuesta:**
        
        - **Función:** Almacenar información (funcionan como una especie de memoria temporal).
        - **Relación con FF:** Cada registro está formado por uno o más flip-flops.
        - **Uso en CPU:** La CPU tiene una pequeña memoria de acceso rápido formada por varios registros que almacenan información intermedia.
        
    

#### **A. Registros Paralelo (Latch)**

- **Pregunta de Examen:** Describa el funcionamiento de un registro paralelo (latch) de 4 bits.
    
    - **Respuesta:**
        
        - **Diagrama:** Utiliza flip-flops D (o de otro tipo) en paralelo, uno por cada bit.
        - **Funcionamiento:** En un solo pulso de clock, todos los datos se cargan simultáneamente al registro.
        - **Velocidad:** Son mucho más rápidos que los registros en serie, ya que cargan múltiples bits a la vez.
        - **Ejemplo:** Si un registro de 4 bits tiene "0000" y se quiere guardar "1010", con un pulso de clock, el registro cambia a "1010".
        
    

#### **B. Registros de Desplazamiento (Shift Register)**

- **Pregunta de Examen:** Explique el funcionamiento de un registro de desplazamiento y compare su velocidad con la de un registro paralelo.
    
    - **Respuesta:**
        
        - **Diagrama:** Los flip-flops están conectados en serie, donde la salida Q de un flip-flop se conecta a la entrada D del siguiente. Hay una única entrada de datos en serie.
        - **Funcionamiento:** La información se maneja en serie, bit a bit, por cada pulso de clock. En cada pulso, el bit de entrada se carga en el primer flip-flop, y los bits existentes se "desplazan" al siguiente flip-flop.
        - **Velocidad:** Son más lentos que los registros paralelos. Para almacenar N bits, se necesitan N pulsos de clock.
        - **Ejemplo (Registro de 4 bits):** Para cargar "0000" en un registro que inicialmente tiene "1111":
            
            - **Pulso 1:** Se carga el primer '0', los bits existentes se desplazan.
            - **Pulso 2:** Se carga el segundo '0', los bits se desplazan.
            - **Pulso 3:** Se carga el tercer '0', los bits se desplazan.
            - **Pulso 4:** Se carga el cuarto '0', los bits se desplazan.
            
        
    

### **IV. Aplicaciones de los Flip-Flops: Contadores**

- **Pregunta de Examen:** ¿Qué son los contadores y qué tipos existen según su dirección de conteo y su sincronización?
    
    - **Respuesta:**
        
        - **Función:** Permiten contar eventos con un código de cuenta particular.
        - **Dirección de Conteo:**
            
            - **Progresivos:** Cuentan en forma ascendente.
            - **Regresivos:** Cuentan en forma descendente (a menudo usando la salida Q negado).
            
        - **Sincronización:**
            
            - **Asincrónicos:** La entrada de clock afecta solo al primer flip-flop; los demás toman la salida del anterior como clock.
            - **Sincrónicos:** La entrada de clock afecta a todos los flip-flops al mismo tiempo. (Más complejos de analizar).
            
        - **Nota:** Los flip-flops individuales siempre funcionan de forma sincrónica.
        
    
- **Pregunta de Examen:** Defina "módulo" y "código de cuenta" en el contexto de los contadores. ¿Cuál es el módulo máximo para N flip-flops?
    
    - **Respuesta:**
        
        - **Módulo:** Número de pulsos que puede contar el contador (o número de estados distintos).
        - **Código de Cuenta:** El código en el que el contador va a contar (ej. binario puro, código de Johnson, código Gray).
        - **Módulo Máximo:** Para N flip-flops, el módulo máximo es 2^N.
        
    

#### **A. Contador Asincrónico Básico (Progresivo)**

- **Pregunta de Examen:** Describa el contador asincrónico básico progresivo, su implementación y cómo se analiza su funcionamiento.
    
    - **Respuesta:**
        
        - **Implementación:** Utiliza flip-flops JK (con J y K unidos y puestos a 1, es decir, en modo conmutación). El clock principal se conecta solo al primer flip-flop; la salida Q del primer FF es el clock del segundo, y así sucesivamente.
        - **Activación:** Generalmente activados por flanco negativo.
        - **Módulo:** 2^N (ej. para 3 FF, 2^3 = 8 palabras distintas).
        - **Código de Cuenta:** Cuenta en binario puro.
        - **Análisis (Diagrama de Tiempo):**
            
            1. **Dibujar la señal de Clock:** Marcar los flancos negativos.
            2. **Establecer Estado Inicial:** (ej. 000 para Q2Q1Q0).
            3. **Analizar Q0:** Como está en modo conmutación y su clock es el principal, Q0 cambia de estado en cada flanco negativo del clock.
            4. **Analizar Q1:** Su clock es Q0. Q1 cambia de estado en cada flanco negativo de Q0.
            5. **Analizar Q2:** Su clock es Q1. Q2 cambia de estado en cada flanco negativo de Q1.
            6. **Continuar:** El análisis se detiene cuando se vuelve al estado inicial.
            7. **Tabla de Código de Cuenta:** Transcribir los estados de Q2Q1Q0 en orden cronológico para ver el código de cuenta (ej. 000, 001, 010, ...).
            
        - **Desventajas:**
            
            - Se producen retardos de tiempo acumulados, lo que limita la frecuencia de operación (son lentos).
            - No se pueden hacer cadenas largas de flip-flops.
            - El período de la señal de salida de cada FF es el doble del período de su señal de clock (ej. Q0 tiene período 2T, Q1 tiene 4T, Q2 tiene 8T).
            
        
    

#### **B. Contador Sincrónico (Binario Puro)**

- **Pregunta de Examen:** ¿Cuál es la principal diferencia en el análisis de un contador sincrónico en comparación con uno asincrónico?
    
    - **Respuesta:**
        
        - **Diferencia:** En un contador sincrónico, todos los flip-flops tienen la misma entrada de clock. Esto significa que, al analizarlo, se deben considerar los cambios en los tres flip-flops (o N flip-flops) _simultáneamente_ en cada pulso de clock, lo que lo hace más complejo.
        
    

#### **C. Contadores en Anillo**

- **Pregunta de Examen:** Describa el funcionamiento de un contador en anillo básico y su módulo de conteo.
    
    - **Respuesta:**
        
        - **Característica:** Las entradas del primer flip-flop están conectadas directamente a las salidas del último flip-flop. Cada salida Q está conectada a la entrada del flip-flop siguiente.
        - **Implementación (Básico):** J del primer FF conectado a Q del último FF, y K del primer FF conectado a Q negado del último FF.
        - **Estado Inicial:** Es crucial para el funcionamiento (ej. 100 para Q2Q1Q0).
        - **Funcionamiento:** El "1" inicial se va desplazando de un flip-flop a otro con cada pulso de clock.
        - **Módulo:** M = N (donde N es el número de flip-flops). Para 3 FF, cuenta 3 palabras distintas.
        - **Código de Cuenta:** Genera un código donde un solo '1' se desplaza (ej. 100, 010, 001). Requiere un '1' inicial para funcionar.
        - **Análisis:** Se puede analizar paso a paso, determinando el estado de cada FF en cada pulso de clock, y luego volcando los resultados al diagrama de tiempo y la tabla de código de cuenta.
        
    
- **Pregunta de Examen:** Explique la variante del contador en anillo que genera el "código de Johnson".
    
    - **Respuesta:**
        
        - **Variante:** La entrada J del primer FF se conecta a Q negado del último FF, y la entrada K del primer FF se conecta a Q del último FF.
        - **Estado Inicial:** Generalmente 000.
        - **Módulo:** 2 * N (para 3 FF, cuenta 6 palabras distintas).
        - **Código de Cuenta (Código de Johnson):**
            
            - Empieza con todos ceros (000).
            - Se van añadiendo unos desde la derecha (001, 011, 111).
            - Una vez que todos son unos, se empiezan a añadir ceros desde la derecha (110, 100, 000).
            
        - **Análisis:** Similar al contador en anillo básico, pero con la lógica de conexión modificada.
        
    
- **Pregunta de Examen:** Describa otra variante del contador en anillo y cómo afecta al código de cuenta.
    
    - **Respuesta:**
        
        - **Variante:** La entrada K del primer FF se conecta a Q del flip-flop anterior (no el último), y J se conecta a Q negado del último FF. (La descripción en el texto es un poco confusa, pero se refiere a una conexión diferente que altera el patrón).
        - **Estado Inicial:** 000.
        - **Efecto en el Código:** Genera un código similar al de Johnson pero salteándose el estado de "todos unos" (ej. para 3 FF, cuenta 5 palabras distintas: 000, 001, 011, 110, 100).
        
