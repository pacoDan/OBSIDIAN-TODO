https://youtu.be/CRW16WWRpUk?list=PL6oA23OrxDZDQEFo7aKBceotX48vLmQYA
A continuación, se presenta un resumen estructurado de la transcripción sobre procesos e hilos en sistemas operativos y arquitectura de computadoras, incluyendo detalles clave, posibles preguntas y respuestas para exámenes:

### **Procesos e Hilos**

### **1. Procesos**

- **Definición:** Un proceso es un programa en ejecución. Es una instancia de un programa que se está ejecutando en la computadora.
    
- **Relación Programa vs. Proceso:** Un programa es el "molde" o el código estático, mientras que un proceso es una instancia dinámica de ese molde en ejecución. Un mismo programa puede tener múltiples procesos ejecutándose concurrentemente.
    
- **Componentes de un Proceso (Imagen del Proceso):**
    
    - **Código/Texto:** La parte estática del programa, las instrucciones ejecutables.
    - **Datos:** Variables globales y estáticas, conocidas de antemano.
    - **Stack (Pila):** Memoria dinámica para variables locales, parámetros de funciones y direcciones de retorno de llamadas a funciones. Crece y decrece con las llamadas y retornos de funciones. Un crecimiento excesivo (ej. recursión infinita) causa un "stack overflow".
    - **Heap (Montículo):** Memoria dinámica para datos asignados en tiempo de ejecución (ej. con `malloc`). Crece a medida que el programa solicita más memoria.
    - **Otros:** Puntero de instrucción (Program Counter), registros de CPU, información de planificación, información de gestión de memoria, información de contabilidad, información de E/S.
    
- **Estados de un Proceso:**
    
    - **New (Nuevo):** El proceso está siendo creado. El sistema operativo está asignando recursos y estructuras (ej. PCB, stack, heap).
    - **Ready (Listo):** El proceso está esperando que se le asigne la CPU para ejecutarse. Está listo para correr.
    - **Running (Ejecución):** El proceso está utilizando la CPU y ejecutando sus instrucciones.
    - **Waiting/Blocked (Esperando/Bloqueado):** El proceso está esperando que ocurra algún evento (ej. finalización de una operación de E/S, un recurso esté disponible). No puede ejecutarse hasta que el evento ocurra.
    - **Terminated (Terminado):** El proceso ha finalizado su ejecución (voluntariamente o por ser matado). Libera sus recursos.
    
- **Transiciones entre Estados:**
    
    - **New -> Ready:** Cuando el proceso es admitido por el sistema operativo.
    - **Ready -> Running:** Cuando el planificador de corto plazo le asigna la CPU.
    - **Running -> Ready:** Por interrupción (ej. fin de su quantum de tiempo, llegada de un proceso de mayor prioridad).
    - **Running -> Waiting:** Por un evento (ej. solicitud de E/S).
    - **Waiting -> Ready:** Cuando el evento esperado ocurre.
    - **Running -> Terminated:** Cuando el proceso finaliza su ejecución (exit).
    - **Ready/Waiting -> Suspended (Suspendido):**
        
        - **Ready Suspended:** Proceso en disco, listo para ser cargado en memoria y ejecutarse.
        - **Blocked Suspended:** Proceso en disco, esperando un evento.
        - **Propósito:** Liberar memoria principal cuando el sistema está sobrecargado o para procesos de baja prioridad. El proceso se mueve del disco a la memoria principal cuando se "desuspende".
        
    
- **Grado de Multiprogramación:**
    
    - **Definición:** El número máximo de procesos que el sistema operativo permite tener en memoria principal (en estados Ready, Running, Waiting) en un momento dado.
    - **Control:** Gestionado por el planificador de largo plazo.
    - **Ejemplo:** Windows Vista Starter limitaba el número de programas concurrentes.
    
- **Grado de Multiprocesamiento:**
    
    - **Definición:** El número de procesos que pueden estar en estado Running simultáneamente.
    - **Control:** Determinado por el hardware (número de CPUs/núcleos).
    - **Relación con Concurrencia y Paralelismo:**
        
        - **Concurrencia:** Múltiples procesos progresan en un intervalo de tiempo (pueden o no ejecutarse al mismo tiempo).
        - **Paralelismo:** Múltiples procesos se ejecutan _simultáneamente_ (requiere múltiples CPUs). El paralelismo implica concurrencia, pero la concurrencia no implica paralelismo.
        
- **Bloque de Control de Proceso (PCB - Process Control Block):**
    
    - **Definición:** Estructura de datos que el sistema operativo utiliza para almacenar toda la información relevante sobre un proceso. Es la "tarjeta de identidad" del proceso.
    - **Contenido:** ID del proceso (PID), estado actual, puntero de programa (Program Counter), valores de los registros de la CPU, información de planificación (prioridad, quantum), información de gestión de memoria (punteros a tablas de páginas), información de contabilidad (tiempo de CPU usado), información de E/S (archivos abiertos, dispositivos asignados).
    - **Ubicación:** Reside en la memoria del sistema operativo. Si el PCB no está en memoria, el SO no sabe que el proceso existe.
    
- **Cambio de Contexto (Context Switch):**
    
    - **Definición:** Proceso de guardar el estado de un proceso en ejecución y cargar el estado de otro proceso para que pueda ejecutarse.
    - **Pasos:**
        
        1. Guardar el contexto del proceso actual (registros de CPU, Program Counter, Stack Pointer, etc.) en su PCB.
        2. Cargar el contexto del nuevo proceso desde su PCB en los registros de la CPU.
        
    - **Costo:** Es una operación costosa en tiempo de CPU, ya que no realiza trabajo útil. El objetivo es minimizar su frecuencia.
    - **Cambio de Modo:** Un cambio de contexto a menudo implica un cambio de modo (de usuario a kernel para acceder al PCB y luego de kernel a usuario para el nuevo proceso).
    
- **Planificadores (Schedulers):**
    
    - **Planificador de Largo Plazo (Long-Term Scheduler):**
        
        - **Función:** Controla el grado de multiprogramación, decidiendo qué procesos pasan del estado "New" a "Ready".
        - **Frecuencia:** Se ejecuta con poca frecuencia (cada mucho tiempo).
        
    - **Planificador de Mediano Plazo (Medium-Term Scheduler):**
        
        - **Función:** Gestiona la suspensión y reanudación de procesos (moviendo procesos entre memoria y disco - swap).
        - **Frecuencia:** Se ejecuta con una frecuencia intermedia.
        
    - **Planificador de Corto Plazo (Short-Term Scheduler / Dispatcher):**
        
        - **Función:** Decide qué proceso en estado "Ready" se ejecutará a continuación en la CPU.
        - **Frecuencia:** Se ejecuta muy frecuentemente (cada pocos milisegundos). Es el más crítico para el rendimiento del sistema.
### **2. Hilos (Threads)**

- **Definición:** Un hilo es una unidad de ejecución dentro de un proceso. Un proceso puede tener uno o varios hilos.
    
- **Compartición de Recursos:**
    
    - **Comparten:** Código, datos (variables globales), heap, archivos abiertos, recursos del proceso.
    - **No Comparten:** Stack (cada hilo tiene su propia pila), registros de CPU (cada hilo tiene su propio conjunto de registros, incluyendo el Program Counter).
    
- **Ventajas de los Hilos:**
    
    - **Paralelismo/Concurrencia:** Permiten que diferentes partes de un mismo programa se ejecuten concurrentemente o en paralelo (si hay múltiples CPUs).
    - **Comunicación Rápida:** Se comunican de forma eficiente a través de memoria compartida (variables globales, heap) sin necesidad de intervención del sistema operativo (no requieren system calls ni cambios de contexto entre hilos para comunicación).
    - **Menor Overhead:** La creación y el cambio de contexto entre hilos son más rápidos y eficientes que entre procesos, ya que se comparte gran parte del contexto.
    - **Estructuración:** Permiten estructurar programas complejos en tareas más pequeñas y manejables.
    
- **Desventajas de los Hilos:**
    
    - **Falta de Protección:** No hay protección de memoria entre hilos del mismo proceso. Un error en un hilo (ej. escribir fuera de su stack) puede corromper la memoria de otro hilo o del proceso completo.
    - **Sincronización:** Requieren mecanismos de sincronización para evitar condiciones de carrera y asegurar la consistencia de los datos compartidos.
    
- **Bloque de Control de Hilo (TCB - Thread Control Block):**
    
    - **Definición:** Estructura de datos que almacena la información específica de un hilo (stack pointer, registros, Program Counter).
    - **Relación con PCB:** El PCB contiene información del proceso, y apunta a los TCBs de sus hilos.
    
- **Tipos de Hilos (Implementación):**
    
    - **Hilos a Nivel de Kernel (KLT - Kernel-Level Threads):**
        
        - **Conocimiento del SO:** El sistema operativo es consciente de la existencia de cada hilo y los gestiona directamente.
        - **Planificación:** El SO puede planificar cada KLT de forma independiente en diferentes CPUs, permitiendo paralelismo real.
        - **Bloqueo:** Si un KLT se bloquea (ej. por E/S), solo ese hilo se bloquea; otros hilos del mismo proceso pueden seguir ejecutándose.
        - **Overhead:** Mayor overhead en creación y cambio de contexto que los ULTs, ya que implican system calls.
        
    - **Hilos a Nivel de Usuario (ULT - User-Level Threads / Green Threads):**
        
        - **Conocimiento del SO:** El sistema operativo _no_ es consciente de la existencia de estos hilos. Son gestionados por una biblioteca de hilos en el espacio de usuario.
        - **Planificación:** La biblioteca de hilos planifica los ULTs. El SO solo ve un único proceso.
        - **Bloqueo:** Si un ULT se bloquea (ej. por E/S), todo el proceso se bloquea, ya que el SO solo ve un proceso y lo suspende.
        - **Overhead:** Menor overhead en creación y cambio de contexto que los KLTs, ya que no implican system calls.
        - **Uso:** Pueden ser útiles si se necesita una planificación personalizada o si el SO no soporta hilos a nivel de kernel.
        
    
- **Ejemplos de Uso de Procesos e Hilos:**
    
    - **Google Chrome (Procesos):** Cada pestaña y plugin se ejecuta como un proceso separado.
        
        - **Ventajas:** Mayor estabilidad (si una pestaña falla, solo se cierra ese proceso, no todo el navegador), mayor seguridad (aislamiento de memoria entre pestañas).
        - **Desventajas:** Mayor consumo de memoria (cada proceso tiene su propia copia de código y datos).
        
    - **Servidores Web (Procesos vs. Hilos):**
        
        - **Apache (Procesos):** Crea procesos hijos para manejar cada solicitud. Más estable (un fallo en un proceso hijo no afecta a otros) y libera memoria al morir.
        - **Tomcat (Hilos):** Utiliza hilos para manejar solicitudes. Más eficiente en memoria y creación/cambio de contexto.
            
            - **Problemas:** Susceptible a "memory leaks" (fugas de memoria) y "thread leaks" (fugas de hilos) si no se gestionan correctamente, lo que puede llevar a un consumo excesivo de recursos y colapsos.
### **3. Creación y Terminación de Procesos/Hilos**

- **Creación de Procesos (Fork/Exec):**
    
    - **`fork()`:** Crea un nuevo proceso (hijo) que es una copia casi idéntica del proceso padre. El hijo recibe un PID de 0 (convención) y el padre recibe el PID del hijo.
    - **`exec()`:** Reemplaza la imagen del proceso actual (código, datos, stack, heap) con la de un nuevo programa. Se usa comúnmente después de un `fork()` para que el proceso hijo ejecute un programa diferente.
    - **`wait()`:** El proceso padre puede usar `wait()` para esperar a que uno o todos sus procesos hijos terminen.
    
- **Creación de Hilos (Pthreads):**
    
    - **`pthread_create()`:** Crea un nuevo hilo dentro del proceso actual. Se le pasa una función que el hilo ejecutará y sus parámetros.
    - **`pthread_join()`:** El hilo principal (o cualquier otro hilo) puede usar `pthread_join()` para esperar a que un hilo específico termine.
    
- **Terminación de Procesos:**
    
    - **`exit()`:** El proceso termina voluntariamente. Puede pasar un código de estado al padre. Libera todos los recursos.
    - **`abort()`:** Terminación anormal del proceso.
    - **Terminación por el Padre:** Un proceso padre puede terminar a sus hijos.
    - **Señales (ej. `kill -9`):** Terminación forzada e inmediata de un proceso. No permite que el proceso libere sus recursos de forma ordenada, dejando "procesos llorando" (recursos no liberados).
### **Posibles Preguntas y Respuestas para Exámenes:**
**Preguntas de Definición y Concepto:**
1. **P:** ¿Qué es un proceso en el contexto de los sistemas operativos? ¿Cuál es la diferencia entre un programa y un proceso? **R:** Un proceso es un programa en ejecución. Un programa es el código estático, mientras que un proceso es una instancia dinámica de ese código con sus propios recursos (memoria, registros, etc.).
2. **P:** Describa los componentes principales de la imagen de un proceso. ¿Cuál es la función del stack y el heap? **R:** Código, datos, stack y heap. El stack gestiona llamadas a funciones y variables locales; el heap gestiona memoria asignada dinámicamente.
3. **P:** Describa los componentes principales de la imagen de un proceso. ¿Cuál es la función del stack y el heap? **R:** Los componentes son: **Código/Texto** (instrucciones), **Datos** (variables globales), **Stack** (pila para variables locales, parámetros y retornos de función) y **Heap** (memoria dinámica asignada en tiempo de ejecución). El stack crece y decrece automáticamente con las llamadas a funciones, mientras que el heap es gestionado explícitamente por el programador.
4. **P:** Explique los cinco estados principales de un proceso (New, Ready, Running, Waiting/Blocked, Terminated) y las transiciones entre ellos. **R:**
    - **New:** Proceso siendo creado.
    - **Ready:** Proceso esperando CPU.
    - **Running:** Proceso usando CPU.
    - **Waiting/Blocked:** Proceso esperando un evento (ej. E/S).
    - **Terminated:** Proceso finalizado.
    - **Transiciones:** New -> Ready (admisión); Ready <-> Running (planificación); Running -> Waiting (bloqueo por E/S); Waiting -> Ready (evento completado); Running -> Terminated (exit).
5. **P:** ¿Qué es el PCB y por qué es fundamental para el sistema operativo? **R:** El Bloque de Control de Proceso es una estructura de datos que contiene toda la información de un proceso. Es fundamental porque sin él, el SO no puede gestionar ni conocer la existencia del proceso.
6. **P:** ¿Qué es un cambio de contexto? ¿Por qué es una operación costosa? **R:** Es el proceso de guardar el estado de un proceso en ejecución y cargar el estado de otro. Es costoso porque implica guardar y restaurar muchos registros y a menudo un cambio de modo (kernel/usuario), lo que no realiza trabajo útil.
7. **P:** Describa los roles de los planificadores de largo, mediano y corto plazo. ¿Cuál es el más crítico para el rendimiento y por qué? **R:** Largo plazo (admisión de procesos), mediano plazo (suspensión/reanudación), corto plazo (asignación de CPU). El de corto plazo es el más crítico porque se ejecuta muy frecuentemente.
8. **P:** ¿Qué es un hilo? ¿Qué recursos comparte un hilo con su proceso y qué recursos son propios de cada hilo? **R:** Un hilo es una unidad de ejecución dentro de un proceso. Comparten código, datos, heap, archivos abiertos. No comparten stack ni registros de CPU.
9. **P:** Compare los hilos a nivel de kernel (KLT) y los hilos a nivel de usuario (ULT). ¿Cuáles son las ventajas y desventajas de cada uno? **R:** KLTs son conocidos y gestionados por el SO (paralelismo real, bloqueo individual), pero con mayor overhead. ULTs son gestionados por una biblioteca de usuario (menor overhead, pero bloqueo de todo el proceso si un hilo se bloquea, no hay paralelismo real).
10. **P:** Explique la diferencia entre `fork()` y `exec()` en la creación de procesos. **R:** `fork()` crea una copia del proceso padre. `exec()` reemplaza el código del proceso actual con un nuevo programa.
11. **P:** ¿Cuál es la diferencia entre terminar un proceso con `exit()` y con `kill -9`? **R:** `exit()` es una terminación ordenada y voluntaria que permite al proceso liberar sus recursos. `kill -9` es una terminación forzada e inmediata que no permite la liberación ordenada de recursos.

**Preguntas de Análisis y Aplicación:**

1. **P:** Si un programa tiene un "memory leak" (fuga de memoria), ¿cómo afectaría esto a un servidor web que utiliza hilos (como Tomcat) en comparación con uno que utiliza procesos (como Apache)? **R:** En un servidor basado en hilos, el "memory leak" afectaría a todo el proceso del servidor, ya que todos los hilos comparten el mismo espacio de memoria. Con el tiempo, el proceso consumiría toda la memoria disponible y podría colapsar el servidor. En un servidor basado en procesos, la fuga de memoria se limitaría a un proceso hijo específico. Al terminar y reiniciar ese proceso hijo, la memoria se liberaría, lo que lo hace más robusto.
2. **P:** ¿Por qué Google Chrome utiliza múltiples procesos para sus pestañas en lugar de múltiples hilos, a pesar del mayor consumo de memoria? **R:** Por razones de estabilidad y seguridad. Si una pestaña falla, solo se cierra ese proceso, no todo el navegador. Además, el aislamiento de procesos proporciona una barrera de seguridad, impidiendo que código malicioso en una pestaña acceda a datos de otras pestañas o del sistema.
3. **P:** Un programador está desarrollando una aplicación que realiza cálculos intensivos y también operaciones de E/S. ¿Recomendaría el uso de hilos o procesos para estructurar esta aplicación? Justifique su respuesta considerando las ventajas y desventajas de cada uno. **R:** Para cálculos intensivos que pueden ejecutarse en paralelo, los hilos son eficientes debido a su menor overhead y fácil comunicación. Para operaciones de E/S que pueden bloquear, los hilos a nivel de kernel serían preferibles para evitar que todo el proceso se bloquee. Si la aplicación necesita aislamiento de fallos o seguridad entre componentes, los procesos serían una mejor opción. La elección depende del equilibrio entre rendimiento, complejidad de comunicación, estabilidad y seguridad.
4. **P:** Si un proceso está en estado "Ready Suspended", ¿qué significa esto y qué transiciones puede experimentar? **R:** Significa que el proceso está en el disco (swapped out), pero está listo para ejecutarse si se le asigna la CPU y se carga de nuevo en memoria. Puede pasar a "Ready" (si se carga en memoria) o a "Blocked Suspended" (si se bloquea mientras está suspendido).
5. **P:** ¿Cómo se relaciona el concepto de "stack overflow" con la gestión de memoria de un proceso? **R:** Un "stack overflow" ocurre cuando el stack de un proceso excede su límite de tamaño asignado. Esto suele deberse a recursión infinita o asignaciones excesivas de variables locales, lo que indica un error en el programa.

---
**Preguntas de Definición y Concepto:**

    
3. **P:** ¿Qué es el PCB (Bloque de Control de Proceso) y por qué es fundamental para el sistema operativo? **R:** El **PCB** es una estructura de datos que contiene toda la información necesaria para gestionar un proceso (PID, estado, registros, memoria, etc.). Es fundamental porque es la "identidad" del proceso para el SO; sin su PCB en memoria, el sistema operativo no sabe que el proceso existe ni cómo gestionarlo.
    
4. **P:** ¿Qué es un cambio de contexto? ¿Por qué es una operación costosa? **R:** Un **cambio de contexto** es el acto de guardar el estado (contexto) del proceso que está dejando la CPU y cargar el estado del proceso que va a empezar a usarla. Es costoso porque implica guardar y restaurar muchos registros de la CPU y, a menudo, un cambio de modo (usuario/kernel), lo que consume tiempo de CPU sin realizar trabajo útil para la aplicación.
    
5. **P:** Describa los roles de los planificadores de largo, mediano y corto plazo. ¿Cuál es el más crítico para el rendimiento y por qué? **R:**
    
    - **Largo Plazo:** Decide qué procesos son admitidos en el sistema (controla el grado de multiprogramación).
    - **Mediano Plazo:** Gestiona la suspensión y reanudación de procesos (swapping entre memoria y disco).
    - **Corto Plazo (Dispatcher):** Decide qué proceso en estado "Ready" se ejecutará a continuación en la CPU. El **planificador de corto plazo** es el más crítico para el rendimiento porque se ejecuta con mucha frecuencia (cada pocos milisegundos), por lo que cualquier ineficiencia en él afecta directamente la capacidad de respuesta del sistema.
    
6. **P:** ¿Qué es un hilo? ¿Qué recursos comparte un hilo con su proceso y qué recursos son propios de cada hilo? **R:** Un **hilo** es una unidad de ejecución dentro de un proceso.
    
    - **Comparten:** Código, datos (variables globales), heap, archivos abiertos, recursos del proceso.
    - **Propios de cada hilo:** Stack (pila de ejecución), registros de CPU (incluyendo el Program Counter).
    
7. **P:** Compare los hilos a nivel de kernel (KLT) y los hilos a nivel de usuario (ULT). ¿Cuáles son las ventajas y desventajas de cada uno? **R:**
    
    - **KLT (Kernel-Level Threads):**
        
        - **Ventajas:** El SO los conoce y puede planificarlos en múltiples CPUs (paralelismo real). Si un KLT se bloquea, otros hilos del mismo proceso pueden seguir ejecutándose.
        - **Desventajas:** Mayor overhead en creación y cambio de contexto (implican _system calls_).
        
    - **ULT (User-Level Threads):**
        
        - **Ventajas:** Menor overhead en creación y cambio de contexto (gestionados por una biblioteca de usuario, no _system calls_).
        - **Desventajas:** El SO no los conoce (solo ve un proceso), por lo que si un ULT se bloquea, todo el proceso se bloquea. No pueden aprovechar múltiples CPUs para paralelismo real.
        
    
8. **P:** Explique la diferencia entre `fork()` y `exec()` en la creación de procesos. **R:**
    
    - `fork()`: Crea un **nuevo proceso (hijo)** que es una copia casi idéntica del proceso padre, incluyendo su espacio de memoria.
    - `exec()`: **Reemplaza la imagen del proceso actual** (código, datos, etc.) con la de un nuevo programa. Se usa comúnmente después de un `fork()` para que el proceso hijo ejecute un programa diferente al padre.
    
9. **P:** ¿Cuál es la diferencia entre terminar un proceso con `exit()` y con `kill -9`? **R:**
    
    - `exit()`: Es una terminación **ordenada y voluntaria**. El proceso tiene la oportunidad de liberar sus recursos de forma limpia y pasar un código de estado al padre.
    - `kill -9`: Es una terminación **forzada e inmediata**. El proceso es terminado abruptamente por el sistema operativo sin darle la oportunidad de liberar recursos o realizar tareas de limpieza. Esto puede dejar recursos sin liberar ("procesos llorando").
    

**Preguntas de Análisis y Aplicación:**

1. **P:** Si un programa tiene un "memory leak" (fuga de memoria), ¿cómo afectaría esto a un servidor web que utiliza hilos (como Tomcat) en comparación con uno que utiliza procesos (como Apache)? **R:** En un servidor basado en **hilos** (ej. Tomcat), todos los hilos comparten el mismo espacio de memoria. Una fuga de memoria en un hilo afectaría a todo el proceso, que crecería indefinidamente hasta consumir toda la RAM y colapsar el servidor. En un servidor basado en **procesos** (ej. Apache), cada solicitud es manejada por un proceso separado. Si un proceso hijo tiene una fuga de memoria, solo afectaría a ese proceso. Al terminar y reiniciar el proceso hijo, la memoria se liberaría, haciendo el sistema más robusto.
    
2. **P:** ¿Por qué Google Chrome utiliza múltiples procesos para sus pestañas en lugar de múltiples hilos, a pesar del mayor consumo de memoria? **R:** Chrome prioriza la **estabilidad y la seguridad**. Al usar procesos separados para cada pestaña, si una pestaña falla, solo se cierra ese proceso sin afectar al resto del navegador. Además, los procesos proporcionan un aislamiento de memoria más fuerte, lo que mejora la seguridad al dificultar que código malicioso en una pestaña acceda a datos de otras.
    
3. **P:** Un programador está desarrollando una aplicación que realiza cálculos intensivos y también operaciones de E/S. ¿Recomendaría el uso de hilos o procesos para estructurar esta aplicación? Justifique su respuesta considerando las ventajas y desventajas de cada uno. **R:** Para **cálculos intensivos**, los **hilos** son generalmente preferibles por su menor overhead en creación y cambio de contexto, y su fácil comunicación a través de memoria compartida. Para **operaciones de E/S**, si se usan hilos a nivel de kernel, el bloqueo de un hilo por E/S no bloqueará a todo el proceso. Si la aplicación requiere **aislamiento de fallos** o **seguridad** entre sus componentes (ej. si diferentes partes manejan datos sensibles o provienen de fuentes no confiables), los **procesos** serían una mejor opción, aunque con mayor consumo de recursos y complejidad de comunicación. La elección final dependería del equilibrio deseado entre rendimiento, robustez y seguridad.
    
4. **P:** Si un proceso está en estado "Ready Suspended", ¿qué significa esto y qué transiciones puede experimentar? **R:** Significa que el proceso ha sido **movido del disco a la memoria secundaria (swap)**, pero está listo para ejecutarse si se le asigna la CPU y se carga de nuevo en la memoria principal. Puede transicionar a "Ready" (cuando es cargado de nuevo en memoria principal) o a "Blocked Suspended" (si se bloquea por un evento mientras está suspendido).
    
5. **P:** ¿Cómo se relaciona el concepto de "stack overflow" con la gestión de memoria de un proceso? **R:** Un "stack overflow" ocurre cuando el **stack (pila)** de un proceso excede el límite de memoria asignado para él. Esto generalmente sucede debido a una recursión infinita o muy profunda, o a la asignación excesiva de variables locales. Es un error de programación que indica que el programa ha agotado el espacio de su pila.