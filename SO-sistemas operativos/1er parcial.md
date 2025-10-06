A continuación, se presenta un resumen estructurado de la transcripción, incluyendo detalles clave y posibles preguntas/respuestas relevantes para exámenes de Sistemas Operativos y Arquitectura de Computadoras:

### **1. Modos de Ejecución y Protección del Hardware**

- **Forma Correcta de Operar sobre Hardware:**
    
    - **Método:** Realizar una _syscall_ (llamada al sistema).
    - **Justificación:** Los programas de usuario no pueden acceder directamente al hardware para garantizar la protección del sistema. Una _syscall_ permite que el sistema operativo (que opera en modo privilegiado) realice la operación en nombre del programa de usuario.
    
- **Forma Incorrecta de Operar sobre Hardware:**
    
    - **Método:** Usar instrucciones privilegiadas directamente desde un proceso de usuario.
    - **Justificación:**
        
        - **Riesgo de Ruptura:** Ejecutar instrucciones privilegiadas desde el modo usuario puede romper el sistema operativo o causar un "segmentation fault" (fallo de segmento).
        - **Riesgo de Software Malicioso:** Otorgar demasiado poder al programador sobre el hardware en modo usuario podría facilitar la creación de software malicioso.
        - **Restricción del Modo Usuario:** Las operaciones sobre hardware no están permitidas en modo usuario por diseño para mantener la estabilidad y seguridad del sistema.
        
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Explique la diferencia entre el modo usuario y el modo privilegiado en un sistema operativo y por qué es crucial para la protección del hardware.
    - **Respuesta:** El modo privilegiado (o modo kernel) permite el acceso completo a todos los recursos del sistema, incluido el hardware, mientras que el modo usuario tiene acceso restringido. Esta distinción es crucial para la protección, ya que evita que programas maliciosos o erróneos en modo usuario dañen el sistema o accedan a datos sensibles. Las operaciones de hardware solo pueden ser realizadas por el kernel a través de _syscalls_.
    - **Pregunta:** ¿Qué sucede si un programa en modo usuario intenta ejecutar una instrucción privilegiada?
    - **Respuesta:** El sistema operativo detectará un intento de instrucción privilegiada y generará una excepción o fallo de protección, lo que generalmente resulta en la terminación del programa (por ejemplo, un "segmentation fault").
    

### **2. Procesos vs. Hilos en Navegadores Web**

- **Ventajas de Usar Procesos sobre Hilos en un Navegador Web:**
    
    - **Estabilidad:** Los procesos son más estables que los hilos. Si una pestaña (proceso) falla, no afecta a las demás pestañas (procesos), a diferencia de los hilos donde el fallo de uno puede colapsar todo el proceso (ejemplo clásico de Flash en Firefox antiguo).
    - **Seguridad:** Los procesos no comparten memoria por defecto (a menos que se configure explícitamente), lo que los hace más seguros. Un proceso malicioso en una pestaña no podría leer o modificar la memoria de otro proceso/pestaña (ejemplo de Home Banking y sitio de origen dudoso). Los hilos, en cambio, comparten el _heap_ y podrían potencialmente acceder o sobrescribir el _stack_ de otros hilos.
    
- **Proceso por Pestaña vs. Proceso por Dominio:**
    
    - **Proceso por Pestaña (o por Dominio):**
        
        - **Ventaja:** Mayor aislamiento y estabilidad. Si una pestaña o un dominio específico falla, solo afecta a ese proceso.
        - **Desventaja:** Mayor consumo de recursos (RAM, CPU) debido a la duplicación de segmentos de código y datos para cada proceso.
        
    - **Hilo por Pestaña (mismo dominio):**
        
        - **Ventaja:** Menor consumo de memoria RAM al compartir el segmento de código y otros recursos dentro del mismo proceso.
        - **Desventaja:** Menor estabilidad (un fallo en un hilo puede afectar a todos los hilos del mismo proceso) y menor seguridad (los hilos comparten memoria, lo que podría permitir el acceso no autorizado entre pestañas del mismo dominio si no se maneja con cuidado).
        - **Consideración:** Podría ser aceptable si las pestañas son del mismo dominio y se confía en ellas (ej. varias pestañas de un mismo sitio web interno), ya que la seguridad entre ellas no es una preocupación primordial.
        
    - **Dependencia del Dominio y Funcionalidad:** La elección depende del dominio y la funcionalidad.
        
        - Si un dominio aloja aplicaciones muy diferentes o de diferentes desarrolladores (ej. hosting compartido), es preferible usar procesos separados para cada una.
        - Si el dominio es controlado y las aplicaciones son de confianza, los hilos podrían ser una opción para optimizar recursos.
        
    - **Cookies:** Las cookies son un factor a considerar, ya que son compartidas dentro del mismo dominio, lo que podría influir en la decisión de agrupar pestañas del mismo dominio en un solo proceso.
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Compare y contraste el uso de procesos e hilos en el contexto de un navegador web, destacando las ventajas y desventajas de cada enfoque en términos de estabilidad y seguridad.
    - **Respuesta:** (Ver puntos anteriores).
    - **Pregunta:** ¿En qué escenarios sería más apropiado usar un proceso por cada pestaña en un navegador, y cuándo podría ser aceptable usar hilos para múltiples pestañas?
    - **Respuesta:** (Ver puntos anteriores, enfatizando la justificación).
    

### **3. Algoritmo de Colas Multinivel en Smartphones**

- **Contexto:** Sistema operativo de smartphone con diferentes prioridades (llamadas, notificaciones, mensajes, aplicaciones). Solo una aplicación se muestra en pantalla, pero varias pueden ejecutarse simultáneamente.
    
- **Diseño del Algoritmo (Ejemplo Propuesto):**
    
    - **Colas y Prioridades:**
        
        - **Cola 1 (Máxima Prioridad): Llamadas.**
            
            - **Algoritmo:** Prioridades (la llamada en atención tiene la máxima prioridad). Las llamadas en espera tienen igual prioridad y se desempatan por FIFO.
            - **Transición:** Si llega una llamada, se le asigna la CPU inmediatamente, interrumpiendo cualquier otra tarea.
            
        - **Cola 2 (Prioridad Intermedia): Aplicaciones.**
            
            - **Algoritmo:** Round Robin con _quantum_ variable o sistema de envejecimiento.
            - **Sub-colas (opcional):**
                
                - Aplicación en pantalla: Mayor prioridad (ej. _quantum_ grande).
                - Aplicaciones en segundo plano: Menor prioridad (ej. _quantum_ pequeño, o envejecimiento para que eventualmente obtengan CPU).
                
            - **Transición:** Una aplicación que pasa a estar en pantalla sube de prioridad.
            
        - **Cola 3 (Baja Prioridad): Notificaciones y Mensajes.**
            
            - **Algoritmo:** FIFO o Round Robin con _quantum_ muy pequeño.
            - **Transición:** Podría implementarse un envejecimiento: si una notificación/mensaje espera más de un tiempo determinado (ej. 5 segundos), su prioridad sube para ser mostrada.
            
        
    - **Transiciones entre Colas:**
        
        - **Fin de Quantum:** Un proceso que agota su _quantum_ en una cola de mayor prioridad pasa a una cola de menor prioridad.
        - **Fin de E/S:** Un proceso que completa una operación de E/S (entrada/salida) vuelve a la cola de mayor prioridad.
        - **Llegada de Proceso:** Los nuevos procesos (ej. llamadas entrantes) ingresan a la cola de mayor prioridad.
        
    - **Justificación:** Es crucial justificar cada decisión: por qué se elige un algoritmo, por qué se asignan prioridades, cómo se manejan las transiciones, y cómo esto optimiza el funcionamiento del planificador (ej. asegurar que las llamadas no se interrumpan, que las notificaciones se muestren a tiempo, y que las aplicaciones en pantalla sean fluidas).
    - **Consideraciones Adicionales:**
        
        - **Entrada/Salida:** Las operaciones de E/S (ej. leer un mensaje de texto de la memoria) pueden implicar cambios de modo y la intervención del planificador.
        - **Paralelismo vs. Concurrencia:** La frase "varias pueden ejecutar al mismo tiempo" puede interpretarse como paralelismo (múltiples núcleos) o concurrencia (multitarea en un solo núcleo). La justificación debe aclarar la interpretación.
        - **Servicios en Segundo Plano:** Se puede optar por incluir o excluir servicios en segundo plano (ej. WhatsApp consultando mensajes) en el diseño, justificando la decisión.
        
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Diseñe un algoritmo de colas multinivel para un smartphone, justificando la asignación de prioridades, los algoritmos de planificación en cada cola y las transiciones entre ellas.
    - **Respuesta:** (Describir el diseño propuesto con justificaciones claras para cada componente).
    - **Pregunta:** ¿Cómo manejaría la situación en la que una llamada telefónica llega mientras el usuario está jugando un juego de alta demanda gráfica?
    - **Respuesta:** La llamada, al ser de máxima prioridad, interrumpiría el juego. El juego pasaría a un estado de espera o de menor prioridad. Se podría argumentar que el juego se pausa completamente o que se le asigna un _quantum_ mínimo si el dispositivo tiene múltiples núcleos para permitir cierta concurrencia.
    

### **4. Seguridad en Ambientes Multithreading (variable++)**

- **`variable++` en Multithreading:**
    
    - **Problema:** No es una operación atómica. Se descompone en múltiples instrucciones a nivel de máquina (leer, incrementar, escribir).
    - **Riesgo:** Puede causar una condición de carrera, donde múltiples hilos intentan modificar la variable simultáneamente, llevando a resultados inconsistentes o incorrectos.
    - **Ejemplo:** Si `variable` es 5, Hilo A lee 5, Hilo B lee 5. Hilo A incrementa a 6 y escribe 6. Hilo B incrementa a 6 y escribe 6. El resultado final es 6, cuando debería ser 7.
    - **Consideración:** Aunque la variable sea local, si se asigna a una variable global o compartida, o si otro hilo la lee/escribe, sigue siendo insegura.
    
- **Desventajas de Compilador que Agrega Mutex Automáticamente:**
    
    - **Overhead Innecesario:**
        
        - **Hilos Únicos:** Si el código se ejecuta en un solo hilo, el _mutex_ es innecesario y añade sobrecarga de rendimiento.
        - **Variables No Compartidas:** Si la variable no es global o no es accedida por múltiples hilos, el _mutex_ es redundante.
        - **Tolerancia a Inexactitud:** En algunos casos, la exactitud del valor de la variable no es crítica, y el _overhead_ de un _mutex_ no se justifica.
        
    - **Rendimiento:** La adición automática de _mutexes_ a cada operación `variable++` podría ralentizar significativamente el programa debido a la sobrecarga de las operaciones de sincronización (adquisición y liberación de _locks_).
    - **Control del Programador:** El programador es quien mejor conoce las regiones críticas y las necesidades de sincronización. La automatización excesiva podría llevar a un diseño ineficiente o incorrecto.
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Explique por qué la sentencia `variable++` no es segura en un ambiente _multithreading_ y qué problema puede ocasionar.
    - **Respuesta:** (Ver puntos anteriores, explicando la condición de carrera).
    - **Pregunta:** ¿Qué desventajas traería que un compilador agregara automáticamente _mutexes_ a cada aparición de una sentencia similar a `variable++`?
    - **Respuesta:** (Ver puntos anteriores, enfocándose en el _overhead_ y la pérdida de control del programador).
    - **Pregunta:** Si `variable2 = variable` (donde `variable` es compartida), ¿se necesitaría un _mutex_?
    - **Respuesta:** Sí, si otro hilo está escribiendo en `variable` mientras se lee, se necesita un _mutex_ para garantizar la consistencia del valor leído y evitar una condición de carrera de lectura/escritura.
    

### **5. Deadlock con Semáforos Mutex Distintos**

- **Posibilidad de Deadlock:** Sí, es posible que ocurra un _deadlock_ con dos semáforos _mutex_ distintos entre dos procesos.
    
- **Justificación (Pseudo-código):**
    
    - **Proceso 1:**
          
        `wait(mutex1) wait(mutex2) // Sección crítica signal(mutex2) signal(mutex1)`
        
    - **Proceso 2:**
        
        `wait(mutex2) wait(mutex1) // Sección crítica signal(mutex1) signal(mutex2)`
        
    - **Escenario de Deadlock:**
        
        1. Proceso 1 ejecuta `wait(mutex1)` y adquiere `mutex1`.
        2. Proceso 2 ejecuta `wait(mutex2)` y adquiere `mutex2`.
        3. Proceso 1 intenta ejecutar `wait(mutex2)` pero `mutex2` está retenido por Proceso 2, por lo que Proceso 1 se bloquea.
        4. Proceso 2 intenta ejecutar `wait(mutex1)` pero `mutex1` está retenido por Proceso 1, por lo que Proceso 2 se bloquea.
        
        - Ambos procesos están bloqueados indefinidamente, esperando un recurso que el otro proceso retiene.
        
    
- **Condiciones de Deadlock (se cumplen):**
    
    - **Exclusión Mutua:** Los _mutexes_ garantizan que solo un proceso pueda acceder al recurso a la vez.
    - **Retención y Espera:** Cada proceso retiene un recurso (un _mutex_) mientras espera por otro.
    - **No Apropiación:** Los recursos no pueden ser quitados a la fuerza una vez adquiridos.
    - **Espera Circular:** Existe una cadena circular de procesos, donde cada proceso espera por un recurso retenido por el siguiente proceso en la cadena.
    
- **Inicialización de Mutexes:** Los _mutexes_ deben inicializarse a 1 (o a un valor que indique que están disponibles).
    
- **Semáforos Nombrados:** Para que los semáforos funcionen entre procesos diferentes, se utilizan semáforos nombrados (ej. `mutex1`, `mutex2`), donde el sistema operativo se encarga de su gestión.
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** ¿Puede ocurrir un _deadlock_ entre dos procesos utilizando dos semáforos _mutex_ distintos? Justifique su respuesta con un ejemplo de pseudo-código y explique las condiciones de _deadlock_ que se cumplen.
    - **Respuesta:** (Ver puntos anteriores).
    - **Pregunta:** ¿Cómo se aseguran los semáforos de que funcionen entre procesos diferentes en lugar de solo entre hilos del mismo proceso?
    - **Respuesta:** Utilizando semáforos nombrados, donde el sistema operativo gestiona el acceso a estos semáforos compartidos por su nombre.
    

### **6. Planificación de Procesos y Hilos (Análisis de Traza)**

- **Análisis de la Traza de Ejecución:**
    
    - **Identificación de Algoritmos:**
        
        - **Cola de Mayor Prioridad:** Round Robin con _quantum_ = 2.
        - **Cola de Menor Prioridad:** Round Robin con _quantum_ = 3.
        
    - **Transiciones entre Colas:**
        
        - **Fin de Quantum:** Un proceso que agota su _quantum_ en la cola de RR(2) pasa a la cola de RR(3).
        - **Llegada de Nuevo Proceso:** Los nuevos procesos (ej. KLT3 en t=4, KLT4 en t=6) ingresan a la cola de mayor prioridad (RR(2)).
        - **Fin de E/S:** Un proceso que completa una operación de E/S (ej. KLT3 en t=5) vuelve a la cola de mayor prioridad (RR(2)).
        
    - **Prioridad de Eventos:** La interrupción por fin de E/S tiene mayor prioridad que la llegada de un nuevo proceso (ej. KLT3 vuelve de E/S en t=5 y se ejecuta antes que KLT4 que llegó en t=6).
    - **Planificación de Hilos de Usuario (ULTs):**
        
        - **Algoritmo:** Prioridades (ULT B tiene mayor prioridad que ULT A, ya que B se ejecuta primero y luego A). No es FIFO (A no se ejecuta antes que B) ni Round Robin (no hay alternancia clara).
        - **No Preemptivo:** La planificación de ULTs es realizada por la biblioteca de hilos de usuario, no por el kernel. Generalmente, los ULTs no son desalojados por el kernel a menos que el KLT al que pertenecen sea desalojado.
        - **No Jacketing:** No hay _jacketing_ (ejecución de otro hilo mientras uno realiza E/S). Cuando un ULT realiza E/S, el KLT se bloquea y no se ejecuta ningún otro ULT de ese KLT.
        
    
- **Cambios de Modo:**
    
    - **Instante 0:** Creación de KLT1 y KLT2 (implica _syscalls_ y cambio a modo privilegiado).
    - **Instante 2:** Fin de _quantum_ de KLT1 (interrupción, cambio a modo privilegiado para que el planificador elija el siguiente proceso).
    - **Instante 5:** Fin de E/S de KLT3 (interrupción, cambio a modo privilegiado).
    - **Inicio de E/S:** Cualquier inicio de E/S (ej. KLT1 en t=1, KLT3 en t=4, KLT4 en t=7) implica una _syscall_ y un cambio a modo privilegiado.
    
- **Involucramiento del Planificador:**
    
    - **Fin de Quantum:** El planificador se activa para elegir el siguiente proceso.
    - **Fin de E/S:** El planificador se activa para reinsertar el proceso en la cola de _ready_ y elegir el siguiente.
    - **Llegada de Nuevo Proceso:** El planificador se activa para insertar el nuevo proceso en la cola de _ready_ y potencialmente reevaluar la planificación.
    
- **Cambio de Planificación si ULTs fueran KLTs:**
    
    - **Instante 0:** Si los ULTs fueran KLTs, el planificador del kernel los manejaría directamente. La planificación podría cambiar desde el instante 0, ya que el kernel podría elegir el KLT B antes que el KLT A si tuviera mayor prioridad o si fuera un SJF.
    - **Instante 6 (o 7):** El _jacketing_ (si existiera) cambiaría la planificación en el instante en que un KLT se va a E/S, permitiendo que otro KLT se ejecute inmediatamente.
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Analice la traza de ejecución proporcionada, identificando los algoritmos de planificación utilizados en cada cola, las transiciones entre ellas y la prioridad de los eventos.
    - **Respuesta:** (Describir el análisis detallado de la traza, justificando cada deducción).
    - **Pregunta:** ¿En qué instantes ocurren cambios de modo en la traza y por qué?
    - **Respuesta:** (Identificar los instantes y explicar la razón: _syscalls_, interrupciones).
    - **Pregunta:** ¿Cómo cambiaría la planificación si los hilos de usuario (ULTs) fueran hilos a nivel de kernel (KLTs)? ¿En qué instante se vería el primer cambio significativo?
    - **Respuesta:** (Explicar las implicaciones de KLTs, como la planificación preemptiva por el kernel y la posibilidad de _jacketing_, y el instante en que se vería el cambio).
    

### **7. Sincronización (Maratón Star Wars)**

- **Problema:** Gestión de un sistema de registro para una maratón con múltiples máquinas de ingreso de datos, colas de atención y restricciones de tickets.
    
- **Regiones Críticas y Sincronización:**
    
    - **Encolar Tickets:** La cola de tickets es una región crítica.
        
        - **Restricción:** No más de 30 tickets pendientes. Esto implica un problema productor-consumidor.
        - **Solución:** Semáforos para controlar el número de tickets disponibles (productor) y tickets pendientes (consumidor).
        
    - **Atención por Carrera:** Hay 5 colas de atención, una por cada carrera.
        
        - **Solución:** Un _mutex_ por cada carrera para asegurar la exclusión mutua al acceder a la cola de esa carrera.
        
    - **Orden de Operaciones:**
        
        - **Generar Ticket:** Solo si hay lugar en la cola de la carrera correspondiente.
        - **Entregar Planilla/Probar Remera:** Solo cuando el empleado lo solicite.
        
    
- **Componentes de Sincronización:**
    
    - **Mutexes por Carrera:** Para proteger el acceso a las colas de tickets de cada carrera.
    - **Semáforos de Productor-Consumidor:** Para gestionar el límite de 30 tickets pendientes.
        
        - `empty_slots`: Semáforo inicializado a 30 (para el productor, las máquinas de ingreso).
        - `filled_slots`: Semáforo inicializado a 0 (para el consumidor, los empleados).
        - `queue_mutex`: Mutex para proteger el acceso a la cola de tickets en sí.
        
    
- **Flujo Lógico (Simplificado):**
    
    1. **Corredor en Máquina:**
        
        - `wait(empty_slots)`: Espera si no hay espacio para tickets.
        - `wait(queue_mutex)`: Adquiere el _lock_ de la cola.
        - Genera ticket y lo encola.
        - `signal(queue_mutex)`: Libera el _lock_.
        - `signal(filled_slots)`: Indica que hay un ticket disponible.
        
    2. **Empleado en Atención:**
        
        - `wait(filled_slots)`: Espera si no hay tickets.
        - `wait(queue_mutex)`: Adquiere el _lock_ de la cola.
        - Desencola ticket y atiende al corredor.
        - `signal(queue_mutex)`: Libera el _lock_.
        - `signal(empty_slots)`: Indica que hay un espacio libre.
        
    
- **Consideraciones Adicionales:**
    
    - **Máquinas Disponibles:** Si hay 4 máquinas, no se necesita un semáforo adicional para ellas a menos que haya una restricción de uso simultáneo (ej. solo 1 a la vez). Las máquinas simplemente compiten por los _mutexes_ de las colas.
    - **Complejidad:** Este ejercicio es complejo debido a la combinación de múltiples restricciones y la necesidad de matrices de semáforos/mutexes.
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Identifique las regiones críticas en el sistema de registro de la maratón y proponga una solución de sincronización utilizando semáforos y _mutexes_.
    - **Respuesta:** (Describir las regiones críticas y la implementación de productor-consumidor y _mutexes_ por carrera).
    - **Pregunta:** ¿Cómo se asegura que el sistema no permita más de 30 tickets pendientes?
    - **Respuesta:** Utilizando un semáforo de conteo (`empty_slots`) inicializado a 30, sobre el cual las máquinas de ingreso realizan una operación `wait()`.
    

### **8. Detección y Recuperación de Deadlock**

- **Contexto:** Un sistema con recursos R1, R2, R3, R4 y varios procesos (P1-P5).
    
- **Recursos Disponibles:**
    
    - R1: 0
    - R2: 0
    - R3: 2
    - R4: 0
    - (Inicialmente, solo 2 unidades de R3 están disponibles).
    
- **Algoritmo de Detección (Simplificado):**
    
    1. **Paso 0:** Identificar procesos que no tienen recursos asignados (ej. P4). Estos no participan en el _deadlock_ actual.
    2. **Paso 1:** Identificar procesos que pueden ser atendidos con los recursos disponibles.
        
        - P2 puede ser atendido (necesita 0 de R1, 0 de R2, 1 de R3, 0 de R4; tenemos 0,0,2,0).
        
    3. **Paso 2:** Ejecutar los procesos que pueden ser atendidos y liberar sus recursos.
        
        - P2 ejecuta y libera sus recursos (1 de R1, 0 de R2, 1 de R3, 0 de R4).
        - Recursos disponibles ahora: (1 de R1, 0 de R2, 3 de R3, 0 de R4).
        
    4. **Paso 3:** Reevaluar qué procesos pueden ser atendidos con los nuevos recursos.
        
        - P1, P3, P5 aún no pueden ser atendidos (necesitan más recursos de los disponibles).
        
    
- **Problema Identificado:** _Deadlock_ entre P1, P3 y P5.
    
- **Criterio de Recuperación (según enunciado):** Matar al proceso que esté usando más recursos.
    
    - **Análisis:**
        
        - Si se mata a P3 (usa más recursos): P3 libera sus recursos (1 de R1, 1 de R2, 0 de R3, 0 de R4).
        - Nuevos recursos disponibles: (2 de R1, 1 de R2, 3 de R3, 0 de R4).
        - Con estos recursos, P1 y P5 aún no pueden ser atendidos. Esto significa que matar a P3 no resuelve el _deadlock_ por sí solo y obliga a matar a más procesos.
        
    
- **Problema de la Estrategia de Recuperación:** La estrategia de matar al proceso con más recursos puede no ser óptima, ya que podría no romper el ciclo de _deadlock_ y requerir la terminación de múltiples procesos, lo que es costoso.
    
- **Criterio de Recuperación Óptimo (Alternativo):** Matar al proceso que, al ser terminado, rompa el ciclo de _deadlock_ con el menor costo (ej. liberar los recursos necesarios para que otros procesos puedan continuar).
    
    - **Ejemplo:** Si se mata a P1 (libera 1 de R1, 0 de R2, 1 de R3, 0 de R4).
        
        - Recursos disponibles: (2 de R1, 0 de R2, 3 de R3, 0 de R4).
        - Con estos recursos, P3 y P5 podrían ser atendidos. Matar a P1 podría ser una mejor solución.
        
    
- **Posibles Preguntas de Examen:**
    
    - **Pregunta:** Dado un estado del sistema (recursos disponibles, asignados, solicitados), identifique si existe un _deadlock_ y qué procesos están involucrados.
    - **Respuesta:** (Aplicar el algoritmo de detección de _deadlock_ y listar los procesos en _deadlock_).
    - **Pregunta:** Si la estrategia de recuperación es terminar el proceso que usa más recursos, ¿qué problemas podría presentar esta estrategia en el escenario dado? Proponga un criterio de recuperación más efectivo.
    - **Respuesta:** (Explicar que la estrategia dada puede no romper el _deadlock_ y obligar a matar más procesos. Proponer un criterio que rompa el ciclo con el menor costo, como matar al proceso que libere los recursos clave para desbloquear a otros).
    

Este resumen abarca los puntos principales de la transcripción, proporcionando una estructura clara y destacando la información relevante para el estudio y la preparación de exámenes.