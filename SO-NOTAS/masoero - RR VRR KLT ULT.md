La transcripción aborda conceptos fundamentales de sistemas operativos, centrándose en la planificación de procesos y la introducción de hilos (threads). A continuación, se presenta un resumen estructurado con detalles clave y posibles preguntas de examen.

### **1. Planificación de Procesos**

La planificación de procesos es la forma en que el sistema operativo decide qué proceso se ejecutará en la CPU y cuándo.

#### **1.1. Interacción del Sistema Operativo con Dispositivos de Entrada/Salida (I/O)**

- **Mecanismo:** Cuando un proceso necesita realizar una operación de I/O (ej. leer/escribir en disco, pantalla, teclado), no interactúa directamente con el dispositivo. En su lugar, realiza una **System Call (Syscall)** al sistema operativo.
- **Proceso:**
    
    - El sistema operativo ejecuta código para preparar la operación de I/O.
    - Una vez que la operación de I/O finaliza, el dispositivo envía una **interrupción** a la CPU.
    - La CPU, al finalizar la instrucción actual, atiende la interrupción y cede el control al sistema operativo.
    - El manejador de interrupciones del sistema operativo finaliza la tarea solicitada por el proceso (ej. entrega los datos solicitados o notifica la finalización del envío).
    
- **Importancia:** Las Syscalls y las interrupciones son mecanismos cruciales para la interacción entre procesos de usuario y recursos del sistema, ya que ningún proceso de usuario habla directamente con los dispositivos de I/O.

#### **1.2. Algoritmos de Planificación**

##### **1.2.1. FIFO (First-In, First-Out)**

- **Criterio:** Los procesos se ejecutan en el orden en que llegan a la cola de "ready".
- **Características:**
    
    - **No expropiativo (non-preemptive):** Una vez que un proceso comienza a ejecutarse, no es interrumpido hasta que finaliza su ráfaga de CPU o realiza una Syscall de I/O.
    - **Simplicidad:** Es el algoritmo más sencillo de implementar.
    
- **Desventajas:**
    
    - **Monopolización de la CPU:** Un proceso con una ráfaga de CPU muy larga puede acaparar la CPU, impidiendo que otros procesos se ejecuten o respondan. Esto puede llevar a tiempos de respuesta muy altos para otros procesos.
    - **No evita inanición (starvation):** Aunque no se menciona explícitamente que FIFO cause inanición, la monopolización puede simularla para procesos que esperan mucho tiempo.
    
- **Syscalls e Interrupciones en FIFO:**
    
    - **Syscalls:**
        
        - **Creación de procesos:** Ocurre cuando un proceso llega al sistema (ej. en instantes 0, 1, 2 para procesos B, C, A respectivamente).
        - **Petición de I/O:** Cuando un proceso solicita una operación de entrada/salida (ej. instantes 4, 7, 9 para B, C, A).
        - **Finalización de proceso (exit):** Cuando un proceso termina su ejecución (ej. instantes 14, 16, 19).
        
    - **Interrupciones:**
        
        - **Fin de I/O:** Cuando un dispositivo de I/O termina una operación y notifica al sistema operativo (ej. instantes 9, 11, 12). Siempre hay una correspondencia entre Syscalls de I/O y interrupciones de fin de I/O.
##### **1.2.2. SJF (Shortest Job First)**

- **Criterio:** Prioriza el proceso con la ráfaga de CPU más corta entre los procesos en estado "ready".
- **Variantes:**
    
    - **Sin desalojo (non-preemptive):** Una vez que un proceso comienza a ejecutarse, no es interrumpido hasta que finaliza su ráfaga de CPU o realiza una Syscall de I/O.
    - **Con desalojo (preemptive):** Si llega un nuevo proceso con una ráfaga de CPU más corta que el tiempo restante del proceso actualmente en ejecución, el proceso actual es desalojado y el nuevo proceso toma la CPU.
    
- **Estimación de la Próxima Ráfaga:**
    
    - El sistema operativo no conoce de antemano la duración exacta de la próxima ráfaga de CPU.
    - Se utiliza una fórmula de estimación basada en el comportamiento pasado del proceso: `Estimación(n+1) = α * TiempoEjecutado(n) + (1 - α) * Estimación(n)`.
        
        - `α` (alfa) es una constante entre 0 y 1.
        - Si `α = 1`, la estimación se basa solo en la última ráfaga ejecutada (reacción rápida a cambios).
        - Si `α = 0`, la estimación se basa solo en la estimación anterior (reacción lenta, considera el historial).
        - Comúnmente se usa `α = 0.5` para dar igual peso a la última ráfaga y la estimación anterior.
        
    - **Importancia del `α`:** Un `α` cercano a 1 reacciona rápidamente a los cambios, mientras que un `α` cercano a 0 mantiene la estimación más estable. La elección depende de la naturaleza de los procesos (estables vs. erráticos).
    
- **Desventajas (SJF sin desalojo):**
    
    - **Inanición (Starvation):** Procesos con ráfagas de CPU largas pueden nunca ejecutarse si continuamente llegan procesos con ráfagas más cortas. Esto se conoce como "morir de hambre".
    
- **Ventajas (SJF con desalojo):**
    
    - Mejora el tiempo de respuesta para procesos cortos.
    - Evita la inanición en algunos escenarios, pero no completamente si los procesos largos nunca tienen la ráfaga más corta.
    
- **Overhead:** SJF (especialmente con desalojo) puede tener más overhead que FIFO debido a la necesidad de recalcular prioridades y realizar desalojos.

##### **1.2.3. Round Robin (RR)**

- **Criterio:** Los procesos se ejecutan en un orden FIFO, pero cada proceso solo puede usar la CPU por un tiempo máximo predefinido llamado **quantum**.
- **Características:**
    
    - **Expropiativo (preemptive):** Un proceso es desalojado de la CPU si su quantum expira, incluso si no ha terminado su ráfaga de CPU.
    - **Equidad:** Busca dar a todos los procesos un uso equitativo de la CPU.
    
- **Mecanismo de Desalojo:** Se utiliza una **interrupción de reloj (clock interrupt)** para notificar al sistema operativo que el quantum ha expirado.
- **Ventajas:**
    
    - **Evita la monopolización de la CPU:** Ningún proceso puede acaparar la CPU indefinidamente.
    - **Mejora el tiempo de respuesta:** Los procesos obtienen una porción de CPU rápidamente, lo que es beneficioso para aplicaciones interactivas.
    - **No sufre inanición:** Todos los procesos eventualmente obtendrán tiempo de CPU.
    
- **Desventajas:**
    
    - **Overhead:** El cambio de contexto frecuente (debido a la expiración del quantum) introduce overhead. Un quantum muy pequeño aumenta el overhead.
    - **Elección del Quantum:**
        
        - **Quantum muy pequeño:** Mayor overhead, pero mejor tiempo de respuesta.
        - **Quantum muy grande (infinito):** Se comporta como FIFO.
        
    
- **Syscalls e Interrupciones en Round Robin:**
    
    - Además de las Syscalls de creación, I/O y exit, y las interrupciones de fin de I/O, se añaden:
        
        - **Interrupciones de Clock:** Ocurren cada vez que un quantum finaliza (ej. instantes 3, 6, 9, 18).
        
    

##### **1.2.4. Virtual Round Robin (VRR)**

- **Criterio:** Una mejora de Round Robin que busca beneficiar a los procesos "ligados a I/O" (I/O bound).
- **Mecanismo:**
    
    - Introduce una cola de "ready" prioritaria (Ready Plus o auxiliar).
    - Si un proceso es desalojado de la CPU porque su quantum expiró, va a la cola de "ready" normal.
    - Si un proceso deja la CPU voluntariamente (ej. por una Syscall de I/O) antes de que su quantum expire, se le guarda el quantum restante y se le coloca en la cola Ready Plus.
    - Los procesos en Ready Plus tienen prioridad sobre los procesos en la cola de "ready" normal. Cuando un proceso de Ready Plus vuelve a la CPU, utiliza su quantum restante. Una vez que agota su quantum restante, se le renueva el quantum completo y se envía a la cola de "ready" normal.
    
- **Tipos de Procesos:**
    
    - **I/O Bound:** Procesos con ráfagas de CPU cortas y mucha actividad de I/O (ej. proceso 2 en el ejemplo). Son beneficiados por VRR.
    - **CPU Bound:** Procesos con ráfagas de CPU largas y poca actividad de I/O (ej. procesos 1 y 3 en el ejemplo). Son beneficiados por Round Robin común.
    
- **Ventajas:** Mejora el rendimiento de los procesos I/O bound al darles prioridad para usar la CPU cuando vuelven de una operación de I/O.

##### **1.2.5. HRRN (Highest Response Ratio Next)**

- **Criterio:** Prioriza procesos que han estado esperando mucho tiempo en la cola de "ready", buscando evitar la inanición.
- **Fórmula:** `Ratio de Respuesta = (Tiempo en Ready + Próxima Ráfaga) / Próxima Ráfaga` o `1 + (Tiempo en Ready / Próxima Ráfaga)`.
    
    - El proceso con el mayor ratio de respuesta es el siguiente en ejecutarse.
    
- **Características:**
    
    - **No expropiativo (non-preemptive):** Una vez que un proceso comienza, no es desalojado.
    - **Evita inanición (Starvation):** A medida que un proceso espera más tiempo, su "Tiempo en Ready" aumenta, lo que incrementa su ratio de respuesta y, eventualmente, le dará la prioridad más alta.
    
- **Overhead:** Requiere calcular el ratio de respuesta para los procesos en "ready" antes de cada asignación de CPU.

##### **1.2.6. Algoritmos Multinivel (Multilevel Queue Scheduling)**

- **Concepto:** Divide la cola de "ready" en múltiples colas, cada una con una prioridad diferente y, opcionalmente, su propio algoritmo de planificación.
- **Funcionamiento:** El sistema operativo siempre atiende primero la cola de mayor prioridad. Solo cuando una cola de mayor prioridad está vacía, se atienden los procesos de la siguiente cola de prioridad.
- **Variantes:**
    
    - **Sin retroalimentación (without feedback):** Un proceso se asigna a una cola de prioridad al inicio y permanece en esa cola durante toda su ejecución.
    - **Con retroalimentación (with feedback):** Los procesos pueden cambiar de cola de prioridad durante su ejecución. Por ejemplo, un proceso que usa mucha CPU puede ser degradado a una cola de menor prioridad, o un proceso que espera mucho tiempo puede ser ascendido a una cola de mayor prioridad (para evitar inanición).
    
- **Ventajas:** Permite priorizar ciertos tipos de procesos (ej. procesos interactivos de alta prioridad, procesos batch de baja prioridad).
- **Desventajas:** Puede llevar a inanición para procesos en colas de baja prioridad si las colas de alta prioridad siempre tienen procesos.

#### **1.3. Clasificación de Algoritmos de Planificación**

- **No Expropiativos (Non-Preemptive):** El sistema operativo interviene solo cuando un proceso realiza una Syscall bloqueante o finaliza.
    
    - FIFO
    - SJF (sin desalojo)
    - HRRN
    - Multinivel (sin desalojo entre colas)
    
- **Expropiativos (Preemptive):** El sistema operativo interviene cuando un proceso realiza una Syscall bloqueante, finaliza, o cuando llega un proceso de mayor prioridad (SJF con desalojo, multinivel con desalojo) o cuando expira un quantum (Round Robin, Virtual Round Robin).
    
    - SJF (con desalojo)
    - Round Robin
    - Virtual Round Robin
    - Multinivel (con desalojo entre colas)
    

#### **1.4. Desempate en Eventos Simultáneos (Solo para Ejercicios)**

En la vida real, los eventos no ocurren exactamente al mismo tiempo. Sin embargo, en ejercicios, si múltiples eventos ocurren simultáneamente, la convención de desempate es:

1. Proceso que viene de ser desalojado de la CPU.
2. Proceso que viene de finalizar una operación de I/O (estaba bloqueado).
3. Proceso recién creado.

### **2. Hilos (Threads)**

Los hilos son una forma más eficiente de multiprogramación, a veces llamados "procesos livianos". Permiten que una aplicación realice múltiples tareas concurrentemente dentro de un mismo proceso.

#### **2.1. Problema de la Concurrencia en Aplicaciones Secuenciales (Ejemplo FTP Server)**

- **Escenario:** Un servidor FTP programado secuencialmente solo puede atender a un cliente a la vez. Si un cliente solicita una operación larga (ej. transferir un archivo grande), el servidor queda bloqueado y no puede atender a otros clientes hasta que la operación finalice.
- **Limitación:** Un código secuencial no puede manejar múltiples solicitudes concurrentes de manera eficiente.

#### **2.2. Solución Basada en Procesos (Multiprocesamiento)**

- **Idea:** Un proceso coordinador acepta las conexiones y, por cada nueva conexión, lanza un nuevo proceso hijo para manejar la solicitud del cliente.
- **Ventajas:**
    
    - **Mejor diseño y modularización:** Cada proceso hijo se encarga de una tarea específica.
    - **Multiprocesador-friendly:** Si hay múltiples CPUs, los procesos hijos pueden ejecutarse en paralelo en diferentes CPUs.
    
- **Desventajas:**
    
    - **Comunicación entre procesos (IPC):** Requiere Syscalls y mecanismos de IPC (ej. pipes, memoria compartida) para que los procesos se comuniquen, lo que introduce overhead.
    - **Duplicación de recursos:** Cada proceso hijo tiene su propio espacio de direcciones, lo que significa que el código y los datos pueden duplicarse en memoria RAM.
    - **Overhead de creación/destrucción de procesos:** Crear y destruir procesos es una operación costosa en términos de recursos del sistema.
    - **Reutilización de código:** Si múltiples procesos usan el mismo código, este se carga varias veces en memoria, a menos que se use una biblioteca compartida, lo que añade complejidad.
    

#### **2.3. Solución Basada en Hilos (Multithreading)**

- **Concepto:** Múltiples hilos de ejecución dentro de un mismo proceso.
- **Componentes de un Proceso (repaso):**
    
    - **PCB (Process Control Block):** Contiene información del proceso.
    - **Espacio de Direcciones de Usuario:** Incluye código, datos, heap (memoria dinámica).
    - **Stack (Pila):** Almacena variables locales y el contexto de llamadas a funciones.
    
- **Compartición de Recursos en Hilos:**
    
    - **Compartido por todos los hilos del proceso:**
        
        - **Código:** El código del programa se carga una sola vez en memoria.
        - **Datos:** Variables globales y datos en el heap.
        - **Recursos abiertos:** Archivos, sockets, etc.
        
    - **Propio de cada hilo:**
        
        - **Stack (Pila):** Cada hilo tiene su propia pila para almacenar variables locales y el contexto de sus llamadas a funciones. **(Pregunta de examen: ¿Por qué cada hilo necesita su propia pila?** Respuesta: Para evitar conflictos y asegurar que cada hilo pueda mantener su propio flujo de ejecución y contexto de llamadas a funciones de forma independiente. Si compartieran la pila, las llamadas a funciones de un hilo podrían sobrescribir o interferir con el contexto de otro hilo, llevando a un comportamiento impredecible y errores.)
        - **TCB (Thread Control Block):** Bloque de control del hilo. Contiene información específica del hilo, como su Program Counter (PC), registros de CPU y estado del hilo. **(Pregunta de examen: ¿Qué información se guarda en el TCB?** Respuesta: Program Counter, registros de CPU, estado del hilo, puntero a la pila del hilo, etc. Es análogo al PCB pero para hilos.)
        
    
- **Ventajas de los Hilos sobre los Procesos (para concurrencia dentro de una aplicación):**
    
    - **Creación/Destrucción más rápida:** Menos overhead que crear/destruir procesos, ya que no se duplica el espacio de direcciones completo.
    - **Cambio de contexto más rápido (Thread Switch):** Menos overhead que un cambio de proceso (Process Switch), ya que no se necesita cambiar el espacio de direcciones.
    - **Comunicación más eficiente:** Los hilos comparten memoria directamente (variables globales, heap), lo que facilita la comunicación sin necesidad de Syscalls adicionales.
    - **Reutilización de código:** El código se carga una sola vez y es compartido por todos los hilos.
    
- **Desventajas:**
    
    - **Complejidad en la programación:** La compartición de recursos introduce problemas de concurrencia (ej. condiciones de carrera, deadlocks) que deben ser manejados cuidadosamente. **(Pregunta de examen: ¿Cuál es la principal desventaja de usar hilos y qué problemas introduce?** Respuesta: La complejidad en la programación debido a la compartición de recursos, lo que puede llevar a problemas de concurrencia como condiciones de carrera, interbloqueos (deadlocks) y errores difíciles de depurar.)
    

#### **2.4. Implementación de Hilos**

##### **2.4.1. Hilos a Nivel de Usuario (ULTs - User-Level Threads)**

- **Administración:** Administrados por una biblioteca de hilos en el espacio de usuario (no por el kernel). El kernel no tiene conocimiento de la existencia de estos hilos.
- **Ventajas:**
    
    - **Menor overhead:** Los cambios de contexto entre ULTs no requieren Syscalls ni cambios de modo (kernel/usuario), lo que los hace muy rápidos.
    - **Planificación personalizada:** La biblioteca de hilos puede implementar su propio algoritmo de planificación, permitiendo una gran flexibilidad.
    - **Portabilidad:** El mismo código con ULTs puede ejecutarse en diferentes sistemas operativos si la biblioteca de hilos es compatible.
    
- **Desventajas:**
    
    - **No aprovechan el multiprocesamiento real:** El kernel solo ve un proceso. Si un proceso tiene múltiples ULTs, solo uno de ellos puede ejecutarse en la CPU a la vez, incluso si hay múltiples CPUs disponibles. Los otros CPUs quedan ociosos para ese proceso.
    - **Bloqueo de todo el proceso:** Si un ULT realiza una Syscall bloqueante (ej. I/O), el kernel bloquea todo el proceso, impidiendo que otros ULTs del mismo proceso se ejecuten.
    - **Manejo de Syscalls:**
        
        - **Llamada directa:** Si un ULT llama directamente a una Syscall bloqueante, todo el proceso se bloquea.
        - **Jacketing:** La biblioteca de hilos intercepta las Syscalls y las convierte en llamadas no bloqueantes (si es posible). Esto permite que otros ULTs se ejecuten mientras uno espera por I/O. **(Pregunta de examen: ¿Qué es Jacketing y por qué es importante para los ULTs?** Respuesta: Jacketing es una técnica donde la biblioteca de hilos intercepta las Syscalls realizadas por los ULTs y las convierte en llamadas no bloqueantes. Es importante porque evita que una Syscall bloqueante de un solo ULT bloquee todo el proceso, permitiendo que otros ULTs del mismo proceso continúen ejecutándose.)
        
    

##### **2.4.2. Hilos a Nivel de Kernel (KLTs - Kernel-Level Threads)**

- **Administración:** Administrados directamente por el kernel del sistema operativo. El kernel tiene conocimiento de cada KLT.
- **Ventajas:**
    
    - **Aprovechan el multiprocesamiento real:** El kernel puede planificar diferentes KLTs del mismo proceso para que se ejecuten en paralelo en diferentes CPUs.
    - **Bloqueo individual:** Si un KLT realiza una Syscall bloqueante, solo ese KLT se bloquea. Otros KLTs del mismo proceso pueden seguir ejecutándose.
    
- **Desventajas:**
    
    - **Mayor overhead:** Los cambios de contexto entre KLTs requieren Syscalls y cambios de modo, lo que los hace más lentos que los ULTs.
    - **Menos flexibilidad en la planificación:** La planificación de los KLTs está determinada por el algoritmo de planificación del kernel, sin posibilidad de personalización a nivel de aplicación.
    

##### **2.4.3. Modelos Híbridos (Combinación de ULTs y KLTs)**

- **Concepto:** Un proceso puede tener múltiples KLTs, y cada KLT puede tener a su vez múltiples ULTs.
- **Ventajas:** Busca combinar las ventajas de ambos enfoques:
    
    - Los KLTs permiten el paralelismo real en múltiples CPUs.
    - Los ULTs dentro de cada KLT ofrecen un cambio de contexto rápido y planificación personalizada a nivel de usuario.
    
- **Funcionamiento:** El kernel planifica los KLTs, y la biblioteca de hilos en el espacio de usuario planifica los ULTs dentro de cada KLT.

### **Posibles Preguntas de Examen**

1. **Explique la diferencia fundamental entre un proceso y un hilo, y cuándo sería más apropiado usar uno u otro.**
    
    - **Respuesta esperada:** Un proceso es una instancia de un programa en ejecución con su propio espacio de direcciones y recursos. Un hilo es una unidad de ejecución dentro de un proceso que comparte el espacio de direcciones y recursos del proceso. Se usarían procesos para tareas independientes que requieren aislamiento y protección, mientras que los hilos son ideales para tareas concurrentes dentro de la misma aplicación que necesitan compartir datos y recursos de manera eficiente.
    
2. **Describa las ventajas y desventajas de los hilos a nivel de usuario (ULTs) y los hilos a nivel de kernel (KLTs).**
    
    - **Respuesta esperada:** Ver secciones 2.4.1 y 2.4.2. Enfatizar overhead, paralelismo real y bloqueo.
    
3. **¿Por qué cada hilo necesita su propia pila (stack) y su propio Program Counter (PC)?**
    
    - **Respuesta esperada:** Ver sección 2.3, "Compartición de Recursos en Hilos". La pila es necesaria para mantener el contexto de ejecución de cada hilo (variables locales, llamadas a funciones) de forma independiente. El PC es necesario para que cada hilo sepa dónde continuar su ejecución dentro del código compartido.
    
4. **¿Qué es la inanición (starvation) en el contexto de la planificación de procesos? Mencione un algoritmo que pueda sufrirla y uno que la evite.**
    
    - **Respuesta esperada:** La inanición ocurre cuando un proceso nunca obtiene tiempo de CPU debido a la priorización constante de otros procesos. SJF (sin desalojo) puede sufrirla. Round Robin y HRRN están diseñados para evitarla.
    
5. **Explique el concepto de "quantum" en Round Robin y cómo su tamaño afecta el rendimiento del sistema.**
    
    - **Respuesta esperada:** El quantum es el tiempo máximo que un proceso puede ejecutar en la CPU antes de ser desalojado. Un quantum pequeño aumenta el overhead pero mejora el tiempo de respuesta. Un quantum grande reduce el overhead pero puede llevar a monopolización (comportándose como FIFO).
    
6. **Compare Round Robin y Virtual Round Robin. ¿Qué tipo de procesos se benefician más de cada uno y por qué?**
    
    - **Respuesta esperada:** Ver sección 1.2.4. Round Robin beneficia a procesos CPU-bound. Virtual Round Robin beneficia a procesos I/O-bound al darles prioridad cuando vuelven de operaciones de I/O.
    
7. **¿Qué es una System Call y una interrupción? Proporcione ejemplos de cuándo ocurren en la ejecución de un proceso.**
    
    - **Respuesta esperada:** Ver sección 1.1. Syscall es una solicitud de un proceso al kernel para acceder a recursos o servicios. Interrupción es una señal de hardware o software que notifica un evento al CPU. Ejemplos: Syscall para I/O, creación/finalización de proceso; Interrupción por fin de I/O, interrupción de reloj.
    
8. **Describa el concepto de "overhead" en los sistemas operativos y cómo se relaciona con los algoritmos de planificación y el uso de hilos.**
    
    - **Respuesta esperada:** Overhead se refiere al tiempo y recursos que el sistema operativo gasta en tareas administrativas (ej. cambio de contexto, planificación) en lugar de ejecutar código de usuario. Algoritmos preemptivos y hilos (especialmente KLTs) pueden introducir más overhead que sus contrapartes no preemptivas o procesos, respectivamente.
    
9. **¿Cómo se estima la próxima ráfaga de CPU en algoritmos como SJF? Explique el papel del parámetro alfa (α).**
    
    - **Respuesta esperada:** Ver sección 1.2.2, "Estimación de la Próxima Ráfaga". Explicar la fórmula y cómo alfa pondera la importancia de la última ráfaga vs. el historial.
    
10. **¿Qué es la monopolización de la CPU y qué algoritmo de planificación es más propenso a sufrirla? ¿Cómo se mitiga este problema?**
    
    - **Respuesta esperada:** Monopolización es cuando un proceso acapara la CPU. FIFO es propenso a sufrirla. Se mitiga con algoritmos preemptivos como Round Robin.