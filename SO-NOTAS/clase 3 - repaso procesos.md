A continuación, se presenta un resumen estructurado de la transcripción sobre el repaso de procesos en sistemas operativos, incluyendo detalles clave y posibles preguntas y respuestas para exámenes.

---
### **Repaso de Procesos en Sistemas Operativos**

### **1. Definición de Proceso**
- **Proceso:** Un proceso es un programa en ejecución. Es una instancia de un programa que se está ejecutando en la computadora y tiene su propio espacio de memoria y recursos.
### **2. Componentes de un Proceso**
- **Código/Texto:** Parte estática que contiene las instrucciones del programa.
- **Datos:** Variables globales y estáticas que son conocidas de antemano.
- **Stack (Pila):** Memoria dinámica para variables locales, parámetros de funciones y direcciones de retorno. Crece y decrece con las llamadas y retornos de funciones.
- **Heap (Montículo):** Memoria dinámica para datos asignados en tiempo de ejecución. Crece a medida que el programa solicita más memoria.
### **3. Estados de un Proceso**

- **New (Nuevo):** El proceso está siendo creado. El sistema operativo está asignando recursos y estructuras necesarias.
- **Ready (Listo):** El proceso está esperando que se le asigne la CPU para ejecutarse.
- **Running (Ejecución):** El proceso está utilizando la CPU y ejecutando sus instrucciones.
- **Waiting/Blocked (Esperando/Bloqueado):** El proceso está esperando que ocurra un evento (ej. finalización de una operación de E/S).
- **Terminated (Terminado):** El proceso ha finalizado su ejecución y libera sus recursos.
### **4. Transiciones entre Estados**

- **New -> Ready:** Cuando el proceso es admitido por el sistema operativo.
- **Ready -> Running:** Cuando el planificador de corto plazo le asigna la CPU.
- **Running -> Ready:** Por interrupción (ej. fin de su quantum de tiempo, llegada de un proceso de mayor prioridad).
- **Running -> Waiting:** Por un evento (ej. solicitud de E/S).
- **Waiting -> Ready:** Cuando el evento esperado ocurre.
- **Running -> Terminated:** Cuando el proceso finaliza su ejecución (exit).
- **Ready/Waiting -> Suspended (Suspendido):** Proceso movido a disco para liberar memoria principal.

### **5. Bloque de Control de Proceso (PCB)**

- **Definición:** Estructura de datos que el sistema operativo utiliza para almacenar toda la información relevante sobre un proceso.
- **Contenido:** ID del proceso (PID), estado actual, puntero de programa (Program Counter), valores de los registros de la CPU, información de planificación, información de gestión de memoria, información de contabilidad, información de E/S.

### **6. Cambio de Contexto**

- **Definición:** Proceso de guardar el estado de un proceso en ejecución y cargar el estado de otro proceso para que pueda ejecutarse.
- **Pasos:**
    1. Guardar el contexto del proceso actual (registros de CPU, Program Counter, Stack Pointer, etc.) en su PCB.
    2. Cargar el contexto del nuevo proceso desde su PCB en los registros de la CPU.
- **Costo:** Es una operación costosa en términos de tiempo de CPU, ya que no realiza trabajo útil.
### **7. Planificadores de Procesos**

- **Planificador de Largo Plazo:** Controla el grado de multiprogramación, decidiendo qué procesos son admitidos en el sistema.
- **Planificador de Mediano Plazo:** Gestiona la suspensión y reanudación de procesos.
- **Planificador de Corto Plazo (Dispatcher):** Decide qué proceso en estado "Ready" se ejecutará a continuación en la CPU.
---
### **Posibles Preguntas y Respuestas para Exámenes**

1. **P:** ¿Qué es un proceso en el contexto de los sistemas operativos? ¿Cuál es la diferencia entre un programa y un proceso? **R:** Un proceso es un programa en ejecución. Un programa es el código estático, mientras que un proceso es una instancia dinámica de ese código con sus propios recursos (memoria, registros, etc.).
    
2. **P:** Describa los componentes principales de la imagen de un proceso. ¿Cuál es la función del stack y el heap? **R:** Los componentes son: **Código/Texto** (instrucciones), **Datos** (variables globales), **Stack** (pila para variables locales, parámetros y retornos de función) y **Heap** (memoria dinámica asignada en tiempo de ejecución). El stack gestiona llamadas a funciones y variables locales; el heap gestiona memoria asignada dinámicamente.
    
3. **P:** Explique los cinco estados principales de un proceso y las transiciones entre ellos. **R:**
    
    - **New:** Proceso siendo creado.
    - **Ready:** Proceso esperando CPU.
    - **Running:** Proceso usando CPU.
    - **Waiting/Blocked:** Proceso esperando un evento (ej. E/S).
    - **Terminated:** Proceso finalizado.
    - **Transiciones:** New -> Ready (admisión); Ready <-> Running (planificación); Running -> Waiting (bloqueo por E/S); Waiting -> Ready (evento completado); Running -> Terminated (exit).
    
4. **P:** ¿Qué es el PCB y por qué es fundamental para el sistema operativo? **R:** El **PCB** es una estructura de datos que contiene toda la información necesaria para gestionar un proceso (PID, estado, registros, memoria, etc.). Es fundamental porque es la "identidad" del proceso para el SO; sin su PCB en memoria, el sistema operativo no sabe que el proceso existe ni cómo gestionarlo.
    
5. **P:** ¿Qué es un cambio de contexto? ¿Por qué es una operación costosa? **R:** Un **cambio de contexto** es el acto de guardar el estado de un proceso que está dejando la CPU y cargar el estado de otro proceso que va a empezar a usarla. Es costoso porque implica guardar y restaurar muchos registros de la CPU y, a menudo, un cambio de modo (usuario/kernel), lo que consume tiempo de CPU sin realizar trabajo útil.
    
6. **P:** Describa los roles de los planificadores de largo, mediano y corto plazo. ¿Cuál es el más crítico para el rendimiento y por qué? **R:**
    - **Largo Plazo:** Controla el grado de multiprogramación y decide qué procesos son admitidos en el sistema.
    - **Mediano Plazo:** Gestiona la suspensión y reanudación de procesos.
    - **Corto Plazo:** Decide qué proceso en estado "Ready" se ejecutará a continuación en la CPU. El **planificador de corto plazo** es el más crítico para el rendimiento porque se ejecuta con mucha frecuencia (cada pocos milisegundos), por lo que cualquier ineficiencia en él afecta directamente la capacidad de respuesta del sistema.
    
7. **P:** ¿Qué es un registro y cuál es su importancia en la arquitectura de la CPU? **R:** Un **registro** es una pequeña porción de memoria de muy alta velocidad ubicada directamente dentro de la CPU. Son cruciales porque almacenan datos e instrucciones que la CPU necesita para sus operaciones inmediatas, permitiendo un acceso extremadamente rápido y optimizando el rendimiento del procesador.
    
8. **P:** Describa las fases del ciclo de instrucción básico de una CPU. ¿En qué momento se verifican las interrupciones? **R:** Las fases son:
    1. **Fetch (Búsqueda):** La CPU busca la siguiente instrucción en memoria.
    2. **Decode (Decodificación):** La CPU interpreta la instrucción.
    3. **Fetch Operands (Búsqueda de Operandos):** La CPU busca los datos necesarios para la instrucción.
    4. **Execute (Ejecución):** La CPU realiza la operación.
    5. **Write Back (Escritura de Resultado):** La CPU escribe el resultado de la operación. Las interrupciones se verifican **después de cada ciclo de instrucción completo**.
    
9. **P:** Explique la diferencia fundamental entre una interrupción y una excepción, incluyendo su origen y naturaleza (síncrona/asíncrona). Proporcione un ejemplo de cada una. **R:**
    - **Interrupción:** Evento **asíncrono** generado por un dispositivo de **hardware externo** a la CPU (ej. disco duro termina una operación, teclado presionado).
    - **Excepción:** Evento **síncrono** generado por la propia **CPU** debido a una condición que ocurre _durante_ la ejecución de una instrucción (ej. división por cero, acceso a memoria no permitido).
    
10. **P:** ¿Qué significa que una interrupción sea "enmascarable" o "no enmascarable"? ¿Por qué existen interrupciones no enmascarables? **R:**
    
    - **Enmascarable:** Puede ser ignorada o deshabilitada temporalmente por software.
    - **No Enmascarable:** No puede ser ignorada y debe ser atendida inmediatamente. Existen para manejar errores de hardware críticos (ej. fallo de voltaje) que requieren una respuesta inmediata para evitar daños mayores al sistema.
---
Esta recopilación de preguntas y respuestas puede ser útil para estudiar y prepararse para exámenes sobre procesos en sistemas operativos y arquitectura de computadoras. Si necesitas más información o detalles sobre algún tema específico, no dudes en preguntar.