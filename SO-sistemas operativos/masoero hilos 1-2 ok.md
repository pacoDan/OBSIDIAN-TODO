### **Clase 4: Hilos y Microkernels - Resumen Estructurado**
**1. Introducción y Contexto de la Multiprogramación**
- **Recapitulando Clases Anteriores:**
    - **Sistemas Multiprogramados:** Permiten tener muchos programas activos en memoria (muchos procesos) que se alternan en el uso de recursos (principalmente la CPU) para maximizar el aprovechamiento del sistema.
    - **Concepto de Proceso:** Una instancia de un programa en ejecución, con su propio espacio de memoria, recursos y estado.
    - **Planificación (Scheduling):** Mecanismos para orquestar la competencia de múltiples procesos por las CPU limitadas. Incluye algoritmos (largo, mediano, corto plazo) y métricas de evaluación (equidad, eficiencia, prioridad).
    - **CPU como Recurso Finito:** La planificación es crucial para distribuir el tiempo de CPU de manera equitativa, justa y eficiente entre los procesos.
- **Evolución hacia la Eficiencia:**
    - La multiprogramación mejoró el aprovechamiento del sistema, pero la búsqueda de mayor eficiencia lleva al concepto de **hilos**.
    - **Hilos:** Una forma de lograr multiprogramación de manera más eficiente para ciertos tipos de problemas, permitiendo exprimir "cada centavo" del sistema.

**2. Caso de Estudio: Desarrollo de un Servidor FTP**

- **Requisitos del Servidor FTP:**
    
    - Soportar múltiples clientes conectados simultáneamente, enviando comandos distintos.
    - Guardar estadísticas de operaciones (ej. bytes transferidos).
    - Acceder a un archivo de configuración (puerto, ruta de archivos, etc.).
    - Servir a múltiples clientes de manera concurrente, no serial.
    
- **Solución 1: Monoproceso (Servidor Serial)**
    
    - **Implementación:** Un único proceso `ftp_server` con un bucle `while true` que recibe una solicitud, la procesa y luego espera la siguiente.
    - **Problema:**
        
        - **Serialidad:** Solo puede atender a un cliente a la vez. Si un cliente solicita una operación larga (ej. transferencia de archivo grande), los demás clientes deben esperar.
        - **Ineficiencia:** No aprovecha la concurrencia. Mientras se envía un archivo (I/O), la CPU podría estar procesando otro comando de otro cliente.
        
    - **Conclusión:** Funciona, pero no es concurrente ni eficiente para múltiples clientes.
    
- **Solución 2: Multiproceso (Servidor Concurrente con Procesos)**
    
    - **Implementación:**
        
        - Un proceso `ftp_coordinator` principal que acepta conexiones de clientes.
        - Por cada cliente, el coordinador **crea un nuevo proceso hijo** (`handler`) para manejar la comunicación con ese cliente.
        - El cliente se comunica directamente con su proceso `handler` asignado.
        
    - **Ventajas:**
        
        - **Concurrencia Real:** Múltiples clientes pueden ser atendidos simultáneamente por procesos distintos.
        - **Modularización:** Diseño más limpio, con responsabilidades separadas (coordinador vs. handlers).
        - **Aprovechamiento de Múltiples CPUs:** Si hay varias CPUs, los procesos `handler` pueden ejecutarse en paralelo.
        - **Independencia:** Los procesos hijos son entidades independientes; si uno falla, no afecta a los demás.
        
    - **Desventajas (Observaciones que llevan a Hilos):**
        
        - **Comunicación entre Procesos (IPC):** Los procesos son independientes y no comparten memoria por defecto. Para compartir información (ej. estadísticas), requieren mecanismos IPC (sockets, memoria compartida, semáforos, colas de mensajes), que implican `syscalls` y **overhead** (cambio de modo usuario/kernel, cambio de contexto).
        - **Archivos de Configuración:** Cada proceso `handler` debe abrir y leer el archivo de configuración, generando estructuras administrativas duplicadas.
        - **Creación de Procesos Costosa:** Crear un proceso implica reservar memoria para código, datos, pila, heap y el PCB, inicializarlo y copiar valores. Esto es un **overhead significativo**.
        - **Reutilización de Código (Memoria):** Si múltiples procesos ejecutan el mismo programa (`handler`), el código se carga múltiples veces en memoria RAM, lo que es un **desaprovechamiento de memoria**. Aunque se puede mitigar con librerías compartidas, esto añade complejidad.
        
    

**3. Hilos (Threads): La Solución Eficiente**

- **Concepto Central:** Procesos "ligeros" que comparten recursos.
    
- **Modelo Single-Threaded (Proceso Tradicional):** Un proceso con un único flujo de ejecución, su propio espacio de direcciones (código, datos, heap) y una pila.
    
- **Modelo Multi-Threaded:**
    
    - El **proceso** sigue siendo la entidad grande que posee los recursos (espacio de direcciones, archivos abiertos, semáforos).
    - Dentro del proceso, existen **múltiples hilos de ejecución**.
    - **Recursos Compartidos:** Todos los hilos dentro del mismo proceso comparten:
        
        - **Código:** Las instrucciones del programa.
        - **Datos Globales/Estáticos:** Variables globales.
        - **Heap:** Memoria dinámica asignada.
        - **Recursos Abiertos:** Archivos, sockets, semáforos.
        
    - **Recursos Propios de Cada Hilo:** Cada hilo tiene su propio:
        
        - **Pila (Stack):** Para llamadas a funciones, direcciones de retorno y variables locales.
        - **Bloque de Control de Hilo (TCB - Thread Control Block):** Contiene información administrativa del hilo (ID del hilo, estado, contexto de ejecución - copia de registros y flags).
        
    
- **Definición de Hilo:** Una unidad de trabajo que puede ser planificada (por el SO o una biblioteca), que involucra un estado de ejecución, un contexto de ejecución y una pila propia.
    
- **Relación Hilo-Proceso:**
    
    - Un proceso se inicia con un primer hilo (hilo principal).
    - Los hilos pertenecen al proceso y usan sus recursos.
    - **Dependencia:** Si el proceso muere, todos sus hilos mueren automáticamente.
    
- **Solución 3: Multihilo (Servidor Concurrente con Hilos)**
    
    - **Implementación:**
        
        - Un único proceso `ftp_server` gigante.
        - Dentro de este proceso, un **hilo coordinador** acepta conexiones.
        - Por cada cliente, el hilo coordinador **crea un nuevo hilo hermano** (handler) dentro del mismo proceso `ftp_server` para manejar la comunicación.
        
    - **Ventajas (respecto a la solución multiproceso):**
        
        - **Creación/Destrucción de Hilos más Rápida:** Menos estructuras que crear (solo TCB y stack), no se duplica el espacio de direcciones.
        - **Cambio de Contexto (Switch) entre Hilos más Rápido:** No es necesario cambiar el espacio de direcciones ni los punteros a segmentos de memoria, ya que los hilos comparten el mismo espacio. Menos overhead.
        - **Comunicación entre Hilos más Rápida:** Los hilos comparten memoria por defecto. No se requieren `syscalls` para IPC; pueden acceder directamente a variables globales o estructuras compartidas.
        - **Aprovechamiento de Memoria:** El código se carga una sola vez.
        - **Diseño Modular:** Se mantiene la separación de responsabilidades.
        
    - **Desventajas (Problemas a Considerar):**
        
        - **Corrupción de Recursos Compartidos:** El acceso concurrente a la memoria compartida (ej. variables globales, estadísticas) puede llevar a problemas de consistencia de datos si no se sincroniza adecuadamente (tema de clases futuras).
        
    

**4. Tipos de Hilos y Planificación**

- **Hilos a Nivel de Kernel (KLT - Kernel-Level Threads):**
    
    - **Visibilidad:** Son vistos y administrados directamente por el kernel del sistema operativo.
    - **Planificación:** El kernel planifica hilos en lugar de procesos. Si hay múltiples CPUs, hilos de diferentes procesos (o del mismo proceso) pueden ejecutarse en paralelo en distintas CPUs.
    - **Bloqueo:** Si un KLT se bloquea (ej. por I/O), el resto de los KLTs del mismo proceso (si están listos) pueden seguir ejecutándose.
    - **Overhead:** Mayor overhead en creación, destrucción y cambio de contexto que los ULTs, ya que implican `syscalls` y cambios de modo.
    - **Ejemplo:** `pthread_create` en Linux crea KLTs.
    
- **Hilos a Nivel de Usuario (ULT - User-Level Threads):**
    
    - **Visibilidad:** Son administrados por una biblioteca de hilos en el espacio de usuario. El kernel **no tiene idea** de su existencia; solo ve el proceso completo.
    - **Planificación:**
        
        - El kernel planifica el **proceso** que contiene los ULTs.
        - La biblioteca de hilos (en espacio de usuario) tiene su propio algoritmo de planificación interno para decidir qué ULT ejecutar dentro del proceso.
        - Hay una **doble planificación** (kernel planifica procesos, biblioteca planifica ULTs).
        
    - **Ventajas:**
        
        - **Mínimo Overhead:** Creación, destrucción y cambio de contexto son muy rápidos, ya que todo ocurre en espacio de usuario (no hay `syscalls` ni cambios de modo).
        - **Planificación Personalizable:** La biblioteca puede implementar cualquier algoritmo de planificación deseado.
        - **Portabilidad:** Un programa con ULTs bien programados puede ser más portable entre sistemas operativos, ya que no depende de las llamadas a kernel específicas de cada SO.
        
    - **Desventajas:**
        
        - **Bloqueo del Proceso Completo:** Si un ULT realiza una operación bloqueante (ej. I/O), el kernel bloquea el **proceso completo**, deteniendo a todos los demás ULTs dentro de ese proceso, incluso si están listos para ejecutar.
        - **No Paralelismo Real en Múltiples CPUs:** El kernel solo ve un proceso. No puede asignar múltiples ULTs del mismo proceso a diferentes CPUs simultáneamente, ya que no los conoce individualmente.
        
    - **Manejo de I/O en ULTs (Importante para Exámenes):**
        
        - **Problema:** Si un ULT llama directamente a una `syscall` bloqueante (ej. `read()`), el kernel bloquea el proceso.
        - **Solución (Jacketing/Wrappers):** Las bibliotecas de ULTs deben proporcionar funciones "wrapper" (envoltorios) para las `syscalls` de I/O. Cuando un ULT llama a la función wrapper:
            
            1. La biblioteca intercepta la llamada.
            2. Puede realizar la I/O de forma no bloqueante (si es posible) o ceder el control a otro ULT mientras espera.
            3. El control siempre regresa a la biblioteca de hilos, que puede entonces replanificar y ejecutar otro ULT.
            4. El concepto de `yield()` permite a un ULT ceder voluntariamente la CPU a la biblioteca para que esta replanifique.
    
- **Modelos de Mapeo (KLTs y ULTs):**
    - **Uno a Uno (1:1):** Cada ULT se mapea a un KLT. (Común en Linux, Windows).
    - **Muchos a Uno (N:1):** Muchos ULTs se mapean a un solo KLT. (Típico de ULTs puros).
    - **Muchos a Muchos (N:M):** Muchos ULTs se mapean a un número menor o igual de KLTs. (Combina ventajas de ambos, ej. Solaris en el pasado, algunas bases de datos como Redis).
    

**5. Ejemplo de Código (Linux - `pthread_create`)**
- **`pthread_create`:** Función para crear un hilo en Linux. Es una `syscall`, lo que indica que crea KLTs.
- **Parámetros:** Recibe una función (ej. `print_data_and_wait`) que el nuevo hilo ejecutará como su código principal.
- **`fork()` y Hilos:**
    
    - Cuando un proceso padre llama a `fork()`, se crea un proceso hijo que es una copia del padre.
    - **Importante:** Las variables globales se **copian** al proceso hijo, no se comparten. Cada proceso tiene su propia copia de las variables globales.
    - **Hilos dentro de un Proceso:** Los hilos creados dentro del mismo proceso **comparten** las variables globales de ese proceso.
    - **Ejemplo de la Clase:** La variable `global_var` se incrementa por el proceso padre, y luego por los hilos del proceso hijo. El valor final de `global_var` en el padre y en el hijo será diferente porque cada uno tiene su propia copia de la variable global inicial.

---
### **Posibles Preguntas y Respuestas para Exámenes**

**1. Preguntas de Definición y Conceptos Básicos:**

- **Pregunta:** ¿Qué es un hilo (thread) en el contexto de los sistemas operativos y cuáles son sus componentes principales que lo diferencian de un proceso?
    
    - **Respuesta:** Un hilo es una unidad de ejecución dentro de un proceso. A diferencia de un proceso, los hilos comparten el espacio de direcciones (código, datos globales, heap) y los recursos abiertos del proceso. Cada hilo tiene su propia pila (stack) y su propio bloque de control de hilo (TCB) que contiene su contexto de ejecución (registros, ID, estado).
    
- **Pregunta:** Explique la diferencia fundamental entre un hilo de kernel (KLT) y un hilo de usuario (ULT) en términos de su visibilidad y gestión por parte del sistema operativo.
    
    - **Respuesta:** Los KLTs son directamente conocidos y planificados por el kernel del SO. Los ULTs son gestionados por una biblioteca en el espacio de usuario y son invisibles para el kernel; el kernel solo ve el proceso completo al que pertenecen.
    
- **Pregunta:** ¿Por qué la creación y el cambio de contexto entre hilos son generalmente más rápidos que entre procesos?
    
    - **Respuesta:** La creación de hilos es más rápida porque no se duplica el espacio de direcciones completo del proceso, solo se crea una pila y un TCB. El cambio de contexto es más rápido porque no es necesario cambiar los punteros a los segmentos de memoria (código, datos, heap) ya que los hilos comparten el mismo espacio de direcciones.
    

**2. Preguntas de Escenario y Análisis:**

- **Pregunta:** Un servidor FTP implementado con un modelo multiproceso (Solución 2) experimenta un alto overhead debido a la comunicación entre el proceso coordinador y los procesos `handler` para actualizar estadísticas. ¿Cómo podría la migración a un modelo multihilo (Solución 3) resolver este problema y por qué?
    
    - **Respuesta:** En un modelo multihilo, todos los hilos (coordinador y handlers) residen dentro del mismo proceso y, por lo tanto, comparten el mismo espacio de memoria. Las estadísticas podrían ser una variable global o una estructura en el heap. Los hilos podrían acceder y modificar esta variable directamente sin necesidad de mecanismos IPC costosos (como sockets o memoria compartida gestionada por el kernel), reduciendo significativamente el overhead de comunicación.
    
- **Pregunta:** Considere un sistema con un único CPU. Si un proceso tiene múltiples hilos de usuario (ULTs) y uno de ellos realiza una operación de I/O bloqueante, ¿qué sucede con los demás ULTs de ese mismo proceso? ¿Cómo se compara esto con un escenario donde el proceso usa hilos de kernel (KLTs)?
    
    - **Respuesta:** Si un ULT realiza una operación de I/O bloqueante, el kernel, al no ser consciente de los ULTs individuales, bloqueará el **proceso completo**. Esto significa que todos los demás ULTs de ese proceso también se detendrán, incluso si están listos para ejecutarse. En contraste, si el proceso usara KLTs, y uno de ellos se bloquea por I/O, el kernel podría planificar y ejecutar otros KLTs del mismo proceso (o de otros procesos) que estén listos, ya que el kernel los administra individualmente.
    
- **Pregunta:** En el ejemplo de código de la clase, la variable `global_var` tiene un valor diferente en el proceso padre y en el proceso hijo después de la llamada a `fork()`. Explique por qué ocurre esto y cómo se relaciona con el concepto de compartir recursos entre procesos e hilos.
    
    - **Respuesta:** Cuando `fork()` es llamado, el proceso hijo recibe una **copia** del espacio de direcciones del padre, incluyendo las variables globales. Por lo tanto, `global_var` en el padre y en el hijo son dos variables distintas, aunque inicialmente tengan el mismo valor. Las modificaciones en una no afectan a la otra. Sin embargo, dentro del proceso hijo, los hilos creados **comparten** la misma `global_var` (la copia del hijo), por lo que las modificaciones de los hilos sí se reflejan entre ellos.
    

**3. Preguntas de Implementación y Buenas Prácticas:**

- **Pregunta:** Un programador está utilizando una biblioteca de hilos de usuario (ULTs) y nota que las operaciones de I/O bloquean todo su programa. ¿Qué técnica debería emplear la biblioteca de hilos para evitar este comportamiento y permitir la concurrencia?
    
    - **Respuesta:** La biblioteca de hilos debería implementar funciones "wrapper" (envoltorios) para las `syscalls` de I/O. Estas funciones interceptarían la llamada, realizarían la I/O de forma no bloqueante (si es posible) o cederían el control a otro ULT mientras esperan la finalización de la I/O. De esta manera, el control siempre regresa a la biblioteca, permitiéndole replanificar y mantener la concurrencia.
    
- **Pregunta:** ¿Qué es el concepto de "jacketing" en el contexto de los hilos de usuario y cómo contribuye a la eficiencia?
    
    - **Respuesta:** "Jacketing" es una técnica donde las llamadas a funciones bloqueantes del sistema se "envuelven" para que se comporten de manera no bloqueante para el hilo de usuario. Esto permite que, cuando un ULT inicia una operación de I/O, el KLT subyacente no se bloquee, y la biblioteca de hilos pueda continuar ejecutando otros ULTs, mejorando la concurrencia y el aprovechamiento de la CPU.
    
- **Pregunta:** ¿Por qué es importante que los programadores utilicen las funciones específicas de la biblioteca de hilos (ej. `pthread_create`, `pthread_mutex_lock`) en lugar de llamadas directas al sistema operativo cuando trabajan con hilos?
    
    - **Respuesta:** Es crucial porque las funciones de la biblioteca de hilos están diseñadas para gestionar correctamente el estado y la planificación de los hilos. Si se usan llamadas directas al SO, la biblioteca de hilos puede perder el control sobre la planificación, lo que puede llevar a bloqueos inesperados, ineficiencias o problemas de concurrencia que son difíciles de depurar.