### **Flip-Flops, Registros y Contadores**

Este documento explora los circuitos secuenciales, centrándose en los flip-flops como bloques básicos de construcción, y su aplicación en registros y contadores.

#### **1. Circuitos Secuenciales vs. Combinacionales**

- **Circuitos Combinacionales:**
    
    - La salida depende únicamente de la combinación actual de las entradas.
    - Bloque básico: Compuertas lógicas (AND, OR, NOT, NAND, NOR, etc.).
    - Ejemplos: Sumadores, multiplexores, decodificadores.
    
- **Circuitos Secuenciales:**
    
    - La salida depende de la combinación actual de las entradas Y del estado anterior del circuito (memoria).
    - Característica principal: Retroalimentación de la salida a la entrada.
    - Bloque básico: Flip-flops.
    

#### **2. Flip-Flops (FF)**

Los flip-flops son elementos de memoria fundamentales en la electrónica digital, capaces de almacenar un bit de información.

- **Nombres Alternativos:**
    
    - FF
    - Cerrojos
    - Multivibradores biestables
    - Binarios
    
- **Características Generales:**
    
    - Pueden almacenar un bit de información.
    - Se construyen a partir de compuertas lógicas (ej. NAND, NOR) o se adquieren como circuitos integrados.
    - Se interconectan para formar circuitos lógicos secuenciales que almacenan datos, generan tiempos, cuentan y siguen secuencias.
    - Representación: Diagrama de bloque (caja negra) con entradas y salidas, sin mostrar la implementación interna.
    - Salidas: Generalmente tienen dos salidas, Q (normal) y Q negado (complemento de Q).
    
- **Tipos de Flip-Flops:**
    
    - RS (Set-Reset)
    - JK
    - D (Delay)
    - T (Toggle)
    

##### **2.1. Flip-Flop RS (Set-Reset)**

Es el flip-flop más básico.

- **Entradas:**
    
    - S (Set): Pone la salida Q en 1.
    - R (Reset): Pone la salida Q en 0.
    
- **Implementación:**
    
    - Se puede construir con compuertas NOR o NAND.
    - Muestra retroalimentación de las salidas a las entradas.
    
- **Análisis (Tabla de Verdad y Diagrama de Tiempo):**
    
    - Requiere considerar el tiempo debido a la retroalimentación.
    - Se analiza el estado presente (Q(t)) y el estado futuro (Q(t+1)).
    
- **Modos de Operación (Asincrónico):**
    

|S|R|Q(t+1)|Modo de Operación|
|---|---|---|---|
|0|0|Q(t)|Mantenimiento|
|0|1|0|Reset|
|1|0|1|Set|
|1|1|Prohibido|Indeterminado/Inestable|

- **Diagrama de Tiempo:** Permite visualizar el comportamiento del flip-flop a lo largo del tiempo, mostrando cómo las entradas S y R afectan las salidas Q y Q negado en diferentes instantes.

##### **2.2. Flip-Flop RS Sincrónico**

Para un comportamiento más estable y controlable, se añade una señal de reloj (clock).

- **Señal de Clock (CLK):**
    
    - Pulsos periódicos que indican los intervalos de tiempo en los que se pueden producir cambios de estado.
    - Funciona como una entrada habilitadora.
    - Los cambios en las salidas solo ocurren cuando el clock está activo (generalmente en 1).
    
- **Implementación:**
    
    - Se añade una compuerta AND en cada entrada (S y R) del flip-flop RS asincrónico, con la otra entrada conectada al clock.
    - Si CLK = 0, las entradas efectivas al flip-flop son 0, manteniendo el estado anterior.
    - Si CLK = 1, las entradas S y R pasan directamente al flip-flop, y este opera según su tabla de verdad.
    
- **Tabla de Verdad (Sincrónico):**
    

|CLK|S|R|Q(t+1)|Modo de Operación|
|---|---|---|---|---|
|0|X|X|Q(t)|Mantenimiento|
|1|0|0|Q(t)|Mantenimiento|
|1|0|1|0|Reset|
|1|1|0|1|Set|
|1|1|1|Prohibido|Indeterminado/Inestable|

- **Activación por Flanco:**
    
    - Para minimizar problemas de ruido y asegurar cambios precisos, los flip-flops se activan por flanco (transición de la señal de clock).
    - **Flanco Positivo:** Cambio de 0 a 1 en el clock (simbolizado con un triángulo en la entrada CLK).
    - **Flanco Negativo:** Cambio de 1 a 0 en el clock (simbolizado con un círculo y un triángulo en la entrada CLK).
    - Los cambios en la salida Q solo ocurren en el instante del flanco.
    
- **Entradas Asincrónicas (Clear y Preset):**
    
    - Permiten inicializar el flip-flop a un estado determinado, independientemente de las entradas S, R o CLK.
    - **Clear:** Pone la salida Q en 0.
    - **Preset:** Pone la salida Q en 1.
    - Se usan principalmente para inicialización.
    

##### **2.3. Flip-Flop JK**

Considerado un flip-flop universal, ya que puede emular el comportamiento de otros tipos.

- **Entradas:**
    
    - J (equivalente a Set)
    - K (equivalente a Reset)
    
- **Ventaja:** Elimina el estado prohibido (1,1) del flip-flop RS.
    
- **Tabla de Verdad (Sincrónico):**
    

|CLK|J|K|Q(t+1)|Modo de Operación|
|---|---|---|---|---|
|0|X|X|Q(t)|Mantenimiento|
|1|0|0|Q(t)|Mantenimiento|
|1|0|1|0|Reset|
|1|1|0|1|Set|
|1|1|1|Q(t) negado|Conmutación (Toggle)|

- **Implementación:** Se puede construir a partir de un flip-flop RS añadiendo compuertas AND en las entradas J y K, conectadas a las salidas Q y Q negado del propio flip-flop.

##### **2.4. Flip-Flop D (Delay)**

También conocido como flip-flop de retardo.

- **Entradas:**
    
    - D (Data): Única entrada de datos.
    - CLK (Clock)
    
- **Funcionamiento:** La salida Q toma el valor de la entrada D en el instante del pulso de clock. Retrasa la señal de entrada un ciclo de clock.
    
- **Tabla de Verdad (Sincrónico):**
    

|CLK|D|Q(t+1)|Modo de Operación|
|---|---|---|---|
|0|X|Q(t)|Mantenimiento|
|1|0|0|Reset|
|1|1|1|Set|

- **Implementación:** Se puede construir a partir de un flip-flop RS o JK.
    
    - **Con RS:** La entrada D se conecta a S, y D negado se conecta a R.
    - **Con JK:** La entrada D se conecta a J, y D negado se conecta a K.
    

##### **2.5. Flip-Flop T (Toggle)**

Flip-flop de conmutación.

- **Entradas:**
    
    - T (Toggle): Única entrada de datos.
    - CLK (Clock)
    
- **Funcionamiento:** La salida Q conmuta (cambia de estado) cada vez que la entrada T está en 1 y se produce un pulso de clock.
    
- **Tabla de Verdad (Sincrónico):**
    

|CLK|T|Q(t+1)|Modo de Operación|
|---|---|---|---|
|0|X|Q(t)|Mantenimiento|
|1|0|Q(t)|Mantenimiento|
|1|1|Q(t) negado|Conmutación (Toggle)|

- **Implementación:** Se construye a partir de un flip-flop JK uniendo sus entradas J y K a la entrada T.

#### **3. Registros**

Los registros son circuitos digitales que almacenan información, funcionando como una forma de memoria temporal.

- **Función:** Almacenar información (bits).
- **Composición:** Uno o más flip-flops.
- **Aplicación:** La CPU utiliza registros para almacenar información intermedia de acceso rápido.

##### **3.1. Registros Paralelo (Latch)**

- **Funcionamiento:** Carga todos los bits de datos simultáneamente en un solo pulso de clock.
- **Velocidad:** Muy rápidos, ya que la carga es paralela.
- **Ejemplo:** Un registro de 4 bits con flip-flops D. Todas las entradas D se conectan a las líneas de datos, y todas las entradas CLK se conectan a la misma señal de clock.

##### **3.2. Registros de Desplazamiento (Shift Register)**

- **Funcionamiento:** La información se maneja en serie, un bit a la vez por pulso de clock. Los bits se "desplazan" de un flip-flop al siguiente.
- **Velocidad:** Más lentos que los registros paralelos para cargar la misma cantidad de bits (requieren N pulsos de clock para N bits).
- **Ejemplo:** Un registro de 4 bits donde la salida Q de un flip-flop se conecta a la entrada D del siguiente.

#### **4. Contadores**

Los contadores son circuitos secuenciales que permiten contar eventos, generando una secuencia de estados predefinida.

- **Tipos de Conteo:**
    
    - **Progresivos:** Cuentan en forma ascendente.
    - **Regresivos:** Cuentan en forma descendente (a menudo usando la salida Q negado).
    
- **Sincronización:**
    
    - **Asincrónicos:** La entrada de clock del primer flip-flop es la señal principal, y las salidas de los flip-flops anteriores actúan como clock para los siguientes (encadenados).
    - **Sincrónicos:** Todos los flip-flops reciben la misma señal de clock simultáneamente. Son más complejos de analizar pero más rápidos y estables.
    
- **Conceptos Clave:**
    
    - **Módulo (M):** Número de estados distintos que puede contar el contador.
    - **Código de Cuenta:** La secuencia de estados que genera el contador (ej. binario puro, código Johnson, código Gray).
    - **Módulo Máximo:** Para N flip-flops, el módulo máximo es 2 ^ N
##### **4.1. Contador Asincrónico Básico (Progresivo)**

- **Implementación:** Generalmente con flip-flops JK configurados en modo conmutación (J=K=1).
- **Funcionamiento:** La salida Q del flip-flop anterior actúa como la entrada de clock del siguiente.
- **Análisis:** Se realiza con diagramas de tiempo, analizando cada flip-flop secuencialmente.
- **Ventajas:** Fácil de implementar y analizar.
- **Desventajas:**
    
    - Retardos de propagación acumulativos, limitando la frecuencia de operación (circuitos lentos).
    - No apto para cadenas largas de flip-flops.
    - El período de la señal de salida de cada flip-flop es el doble del período de su señal de clock de entrada.
    

##### **4.2. Contadores en Anillo**

Son contadores que no cuentan en binario puro y tienen una estructura donde las salidas se retroalimentan a las entradas del primer flip-flop.

- **Contador en Anillo Básico:**
    
    - La salida Q del último flip-flop se conecta a la entrada J del primer flip-flop, y Q negado del último se conecta a la entrada K del primer flip-flop.
    - Requiere un estado inicial específico (ej. un solo 1 y el resto 0s).
    - **Módulo:**  M=N (donde N es el número de flip-flops). Cuenta N palabras distintas.
    - **Código de Cuenta:** El "1" se desplaza a través de los flip-flops.
    
- **Contador en Anillo Modificado (Johnson Counter):**
    
    - La salida Q negado del último flip-flop se conecta a la entrada J del primer flip-flop, y Q del último se conecta a la entrada K del primer flip-flop.
    - **Módulo:**  M=2N (donde N es el número de flip-flops).
    - **Código de Cuenta (Código Johnson):** Se caracteriza por una secuencia donde los bits se "llenan" con 1s y luego con 0s.
    
- **Variantes de Contadores en Anillo:**
    
    - Conexiones de retroalimentación diferentes pueden generar códigos de cuenta distintos o saltarse combinaciones.
    

---

### **Preguntas y Respuestas**

#### **Preguntas sobre Flip-Flops**

1. **¿Cuál es la diferencia fundamental entre un circuito combinacional y un circuito secuencial?**
    
    - **Respuesta:** La diferencia fundamental radica en la memoria. Un circuito combinacional produce una salida basada únicamente en sus entradas actuales, mientras que un circuito secuencial considera tanto las entradas actuales como el estado anterior (almacenado en elementos de memoria como los flip-flops) para determinar su salida.
    
2. **¿Qué es un flip-flop y cuál es su función principal?**
    
    - **Respuesta:** Un flip-flop es el bloque básico de construcción de los circuitos secuenciales. Su función principal es almacenar un bit de información, actuando como una unidad de memoria elemental.
    
3. **Mencione los cuatro tipos principales de flip-flops y una característica distintiva de cada uno.**
    
    - **Respuesta:**
        
        - **Flip-Flop RS:** Es el más básico, pero tiene un estado prohibido (cuando S y R son 1 simultáneamente).
        - **Flip-Flop JK:** Elimina el estado prohibido del RS, introduciendo un modo de conmutación (toggle) cuando J y K son 1.
        - **Flip-Flop D:** Actúa como un retardo, transfiriendo el valor de su entrada D a la salida Q en el siguiente pulso de clock.
        - **Flip-Flop T:** Conmuta su salida (cambia de estado) cada vez que su entrada T es 1 y se produce un pulso de clock.
        
    
4. **¿Por qué se utiliza una señal de clock en los flip-flops sincrónicos?**
    
    - **Respuesta:** La señal de clock se utiliza para sincronizar los cambios de estado en el flip-flop. Permite que los cambios en la salida Q ocurran solo en momentos específicos (generalmente en los flancos del pulso de clock), lo que mejora la estabilidad y el control del circuito, evitando comportamientos inestables causados por cambios asincrónicos en las entradas.
    
5. **Explique la diferencia entre activación por flanco positivo y por flanco negativo en un flip-flop.**
    
    - **Respuesta:** La activación por flanco se refiere al momento exacto en que el flip-flop "lee" sus entradas y actualiza su salida.
        
        - **Flanco Positivo:** El cambio de estado ocurre cuando la señal de clock pasa de un nivel bajo (0) a un nivel alto (1).
        - **Flanco Negativo:** El cambio de estado ocurre cuando la señal de clock pasa de un nivel alto (1) a un nivel bajo (0).
        
    - Esto asegura que el flip-flop sea sensible a un instante preciso de la señal de clock, ignorando los cambios en las entradas durante el resto del ciclo.
    
6. **¿Para qué se utilizan las entradas Clear y Preset en un flip-flop?**
    
    - **Respuesta:** Las entradas Clear y Preset son entradas asincrónicas que se utilizan para inicializar el flip-flop a un estado conocido, independientemente de las entradas de datos o del clock.
        
        - **Clear:** Pone la salida Q en 0.
        - **Preset:** Pone la salida Q en 1.
        
    

#### **Preguntas sobre Registros**

1. **¿Cuál es la función principal de un registro en un sistema digital?**
    
    - **Respuesta:** La función principal de un registro es almacenar temporalmente información digital (bits). Actúan como una pequeña memoria de acceso rápido, esencial para el procesamiento de datos en componentes como la CPU.
    
2. **Compare los registros paralelo y de desplazamiento en términos de cómo cargan los datos y su velocidad.**
    
    - **Respuesta:**
        
        - **Registro Paralelo (Latch):** Carga todos los bits de datos simultáneamente en un solo pulso de clock. Son muy rápidos para la carga de datos.
        - **Registro de Desplazamiento (Shift Register):** Carga los datos en serie, un bit a la vez por cada pulso de clock. Los bits se desplazan secuencialmente a través de los flip-flops. Son más lentos para cargar la misma cantidad de bits que un registro paralelo, ya que requieren N pulsos de clock para N bits.
        
    
3. **Si tengo un registro de 8 bits, ¿cuántos flip-flops necesitaría para construirlo?**
    
    - **Respuesta:** Se necesitarían 8 flip-flops, ya que cada flip-flop almacena un bit de información.
    

#### **Preguntas sobre Contadores**

1. **¿Qué es un contador en electrónica digital?**
    
    - **Respuesta:** Un contador es un circuito secuencial diseñado para contar eventos o pulsos, generando una secuencia predefinida de estados binarios.
    
2. **Explique la diferencia entre un contador asincrónico y un contador sincrónico.**
    
    - **Respuesta:**
        
        - **Contador Asincrónico (Ripple Counter):** La señal de clock se aplica solo al primer flip-flop. La salida de cada flip-flop actúa como la señal de clock para el siguiente. Esto crea un efecto de "onda" o "propagación" del clock. Son más simples de diseñar pero sufren de retardos de propagación acumulativos.
        - **Contador Sincrónico:** La misma señal de clock se aplica simultáneamente a todos los flip-flops del contador. Esto elimina los retardos de propagación acumulativos, haciéndolos más rápidos y estables, aunque su diseño es más complejo.
        
    
3. **¿Qué significa el "módulo" de un contador? Si tengo un contador con 3 flip-flops, ¿cuál es su módulo máximo?**
    
    - **Respuesta:** El "módulo" de un contador se refiere al número total de estados distintos por los que pasa el contador antes de repetir su secuencia. Para un contador con N flip-flops, el módulo máximo es 2^N. Por lo tanto, para un contador con 3 flip-flops, su módulo máximo es 8=2^3.
    
4. **Describa brevemente el funcionamiento de un contador en anillo básico y un contador Johnson.**
    
    - **Respuesta:**
        
        - **Contador en Anillo Básico:** Es un registro de desplazamiento donde la salida del último flip-flop se retroalimenta a la entrada del primero. Requiere una inicialización específica (ej. un solo '1' y el resto '0's). Su módulo es igual al número de flip-flops (N).
        - **Contador Johnson (Twisted Ring Counter):** Es una variante del contador en anillo donde la salida _negada_ del último flip-flop se retroalimenta a la entrada del primero. Su módulo es el doble del número de flip-flops (2N). Genera un código de cuenta único donde los bits se "llenan" con unos y luego con ceros.
        
    
5. **¿Cuál es la principal desventaja de los contadores asincrónicos?**
    
    - **Respuesta:** La principal desventaja es la acumulación de retardos de propagación. Dado que la señal de clock se propaga de un flip-flop al siguiente, cada flip-flop introduce un pequeño retardo. En contadores con muchos flip-flops, estos retardos se suman, lo que puede limitar la velocidad máxima de operación del contador y causar problemas de sincronización.