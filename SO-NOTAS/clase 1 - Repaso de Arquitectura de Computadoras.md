https://www.youtube.com/watch?v=BKv8rM6WXzQ&list=PL6oA23OrxDZDQEFo7aKBceotX48vLmQYA&index=3&pp=iAQB
A continuación, se presenta un resumen estructurado de la transcripción sobre arquitectura de computadoras, incluyendo detalles clave y posibles preguntas de examen:
### **Repaso de Arquitectura de Computadoras**
- **Registros:**
    - **Definición:** Pequeñas porciones de memoria ubicadas dentro del procesador (CPU).
    - **Tipos:**
        - **Uso General:** Destinados a ser utilizados por programadores de bajo nivel.
        - **Uso Específico:** Tienen funciones predefinidas por el fabricante y son cruciales para el funcionamiento del procesador (ej. puntero de pila, puntero de instrucción, _Program Status Word_ (PSW) que contiene _flags_ de estado).
    - **Función:** Almacenan datos y direcciones que la CPU necesita para sus operaciones.
- **Ciclo de Instrucción Básico:**
    - **Fases:**
        1. **Fetch (Búsqueda):** Ir a buscar la instrucción de la memoria.
        2. **Decode (Decodificación):** Entender qué debe hacer la instrucción.
        3. **Fetch Operands (Búsqueda de Operandos):** Si la instrucción requiere datos, ir a buscarlos.
        4. **Execute (Ejecución):** Realizar la operación indicada por la instrucción.
        5. **Write Back (Escritura de Resultado):** Escribir el resultado de la operación (si aplica).
    - **Verificación de Interrupciones:** Después de cada ciclo de instrucción, la CPU verifica si hay interrupciones pendientes y si están habilitadas.
- **Interrupciones y Excepciones:**
    - **Definición General:** Mecanismos para notificar a la CPU sobre un evento.
    - **Interrupciones (Hardware):**        
        - **Origen:** Dispositivos de hardware externos a la CPU (ej. disco duro termina de leer, impresora sin papel, conexión de un dispositivo).
        - **Naturaleza:** Asíncronas (la CPU no sabe cuándo ocurrirán).
        - **Manejo:** Se verifican _después_ de cada ciclo de instrucción completo.
    - **Excepciones (Software):**
        - **Origen:** Eventos que ocurren _durante_ el ciclo de instrucción, generalmente asociados a errores o condiciones especiales (ej. división por cero, acceso a memoria no permitida, instrucción inválida).
        - **Naturaleza:** Síncronas (ocurren en un punto predecible del flujo de ejecución).
        - **Manejo:** Interrumpen el ciclo de instrucción en curso.
    - **Tipos de Interrupciones (por capacidad de ignorar):**
        - **Enmascarables:** Pueden ser ignoradas o deshabilitadas temporalmente por software (ej. para ejecutar un bloque de código crítico sin interrupciones).
        - **No Enmascarables:** No pueden ser ignoradas y suelen estar asociadas a errores de hardware severos (ej. fallos de voltaje) que requieren atención inmediata.
        
    - **Manejo de Múltiples Interrupciones:**
        
        - **Por Prioridad:** Cada interrupción tiene una prioridad asignada (gestionada por un controlador de interrupciones programable, PIC).
        - **Anidamiento:** Una interrupción de mayor prioridad puede interrumpir el manejo de una interrupción de menor prioridad.
        
    - **Procesamiento de Interrupciones (Pasos):**
        
        1. El dispositivo genera la interrupción.
        2. El procesador termina la instrucción actual.
        3. Se guarda el estado del proceso actual (registros, PSW, puntero de instrucción) en la pila del sistema.
        4. Se carga la rutina de atención a la interrupción (ISR) desde el vector de interrupciones.
        5. La ISR procesa la interrupción.
        6. Se restaura el estado del proceso original desde la pila.
        7. El proceso original reanuda su ejecución.
        
    
- **Entrada/Salida (I/O):**
    
    - **Definición:** Mecanismos para transferir datos entre la CPU y los dispositivos externos.
    - **Tipos de I/O:**
        
        1. **I/O Programada (Polling):**
            
            - **Funcionamiento:** La CPU inicia la operación de I/O y luego entra en un bucle de "espera activa" (polling), preguntando repetidamente al dispositivo si la operación ha terminado.
            - **Ventajas:** Simple de implementar.
            - **Desventajas:** Desperdicia muchos ciclos de CPU, ya que la CPU está constantemente ocupada preguntando en lugar de hacer otro trabajo. Ineficiente para operaciones de I/O lentas.
            - **Uso:** Podría ser útil para operaciones de I/O extremadamente cortas donde el costo de cambiar de contexto es mayor que el polling.
            
        2. **I/O por Interrupciones:**
            
            - **Funcionamiento:** La CPU inicia la operación de I/O y luego puede realizar otras tareas. Cuando la operación de I/O termina (o una parte de ella), el dispositivo genera una interrupción para notificar a la CPU.
            - **Ventajas:** Permite a la CPU ser más eficiente al realizar otras tareas mientras espera la I/O.
            - **Desventajas:** La CPU aún debe manejar múltiples interrupciones si la operación de I/O es grande y se realiza en partes (ej. llenar un buffer, generar una interrupción, vaciar el buffer, repetir).
            
        3. **I/O por DMA (Direct Memory Access):**
            
            - **Funcionamiento:** Un controlador DMA (un pequeño procesador dedicado) se encarga de la transferencia de datos entre el dispositivo de I/O y la memoria principal, sin involucrar a la CPU en cada paso. La CPU solo inicia la operación y recibe una única interrupción cuando la transferencia completa ha finalizado.
            - **Ventajas:** La forma más eficiente de I/O a nivel de CPU, ya que libera completamente a la CPU para otras tareas durante la transferencia de datos.
            - **Uso:** Fundamental para dispositivos de alta velocidad (discos duros, tarjetas de red).
            
        
    

### **Analogía de la Biblioteca (para I/O):**

- **I/O Programada:** Vas a la biblioteca, pides un libro y te quedas esperando en el mostrador hasta que lo traen.
- **I/O por Interrupciones:** Vas a la biblioteca, pides un libro, te vas a hacer otras cosas y la biblioteca te avisa (interrupción) cuando el libro está listo para que lo recojas.
- **I/O por DMA:** Vas a la biblioteca, pides un libro, y la biblioteca se encarga de que alguien te lo lleve directamente a tu casa sin que tengas que volver a la biblioteca.

### **Posibles Preguntas de Examen:**

1. **Registros y Ciclo de Instrucción:**
    
    - ¿Qué es un registro y cuál es su importancia en la arquitectura de la CPU?
    - Describa las fases del ciclo de instrucción básico de una CPU. ¿En qué momento se verifican las interrupciones?
    
2. **Interrupciones y Excepciones:**
    
    - Explique la diferencia fundamental entre una interrupción y una excepción, incluyendo su origen y naturaleza (síncrona/asíncrona). Proporcione un ejemplo de cada una.
    - ¿Qué significa que una interrupción sea "enmascarable" o "no enmascarable"? ¿Por qué existen interrupciones no enmascarables?
    - Describa el proceso general que sigue la CPU cuando se produce una interrupción, desde su generación hasta la reanudación del proceso original. ¿Qué papel juega la pila del sistema en este proceso?
    - ¿Cómo se manejan múltiples interrupciones que ocurren simultáneamente o en un corto intervalo de tiempo?
    
3. **Mecanismos de Entrada/Salida:**
    
    - Compare los tres mecanismos de entrada/salida (programada, por interrupciones, por DMA) en términos de eficiencia de la CPU y complejidad.
    - ¿En qué escenarios específicos podría ser preferible la I/O programada sobre la I/O por interrupciones o DMA, a pesar de su aparente ineficiencia?
    - Explique el papel del controlador DMA en las operaciones de I/O. ¿Cómo contribuye a la eficiencia de la CPU?
    - Utilice la analogía de la biblioteca para explicar los tres tipos de I/O.
    

### **Detalles Adicionales y Curiosidades:**

- **PSW (Program Status Word):** Contiene flags importantes, incluyendo el flag de interrupciones habilitadas y el flag de modo (usuario/kernel).
- **Vector de Interrupciones:** Una tabla en memoria que contiene las direcciones de las rutinas de atención a interrupciones (ISRs).
- **PIC (Programmable Interrupt Controller):** Dispositivo de hardware que gestiona las interrupciones de múltiples dispositivos y las prioriza antes de enviarlas a la CPU.
- **Costo del Cambio de Contexto:** El proceso de guardar y restaurar el estado de un proceso (cambio de contexto) es costoso en términos de tiempo de CPU. Evitar interrupciones innecesarias o frecuentes es crucial para el rendimiento.
- **Recursos Adicionales:** Se mencionaron enlaces a recursos sobre el funcionamiento de una CPU simple, cómo funcionan los procesadores modernos y cómo se gestiona la memoria a bajo nivel.

---
**Preguntas de Definición y Concepto:**

1. **P:** ¿Cuáles son las funciones principales de un sistema operativo desde la perspectiva de un usuario final? **R:** Las funciones principales son la **interfaz de usuario** (facilita la interacción), la **interfaz con dispositivos** (permite usar periféricos sin programarlos a bajo nivel) y la **ejecución de programas** (fundamental para correr aplicaciones).
    
2. **P:** Mencione y explique al menos tres funciones técnicas de un sistema operativo que van más allá de la interacción directa del usuario. **R:**
    
    - **Administración de memoria:** Gestiona cómo se asigna y libera la memoria para los programas.
    - **Administración de dispositivos de entrada/salida:** Controla el acceso y la comunicación con periféricos.
    - **Administración de archivos:** Organiza y gestiona el almacenamiento de datos en el disco.
    - **Comunicación entre programas:** Permite que diferentes programas intercambien información.
    
3. **P:** Defina qué es el kernel de un sistema operativo y por qué se dice que es "residente en memoria". **R:** El **kernel** es la parte central del sistema operativo, la más cercana al hardware. Se dice que es "residente en memoria" porque permanece cargado en la memoria principal de forma constante mientras el sistema está en funcionamiento, ya que gestiona los recursos más críticos.
    
4. **P:** Explique el propósito de las _system calls_ (llamadas al sistema). ¿Por qué son necesarias y qué ventajas ofrecen a nivel de rendimiento? **R:** Las _system calls_ son la interfaz que permite a los programas de usuario solicitar servicios privilegiados al kernel (ej. acceder a hardware, gestionar memoria). Son necesarias porque los programas de usuario no tienen acceso directo a estos recursos por seguridad. Ofrecen buen rendimiento porque son el método más directo y rápido para interactuar con el kernel.
    
5. **P:** ¿Cuál es la diferencia fundamental entre usar _system calls_ directamente y usar bibliotecas del sistema? Proporcione ejemplos de cuándo se preferiría una sobre la otra. **R:** Las _system calls_ son las funciones de bajo nivel que interactúan directamente con el kernel, son muy potentes pero "rústicas" y específicas de cada SO. Las **bibliotecas del sistema** son colecciones de funciones que agrupan y abstraen múltiples _system calls_ para tareas comunes, ofreciendo mayor comodidad y portabilidad.
    
    - Se preferirían **bibliotecas** para la programación diaria (ej. `printf`, `malloc`) por su facilidad de uso y portabilidad.
    - Se preferirían _system calls_ directas para casos muy específicos donde se requiere máxima optimización o control a bajo nivel, aunque es más complejo y menos portable.
    
6. **P:** Describa los modos de ejecución "modo usuario" y "modo kernel". ¿Qué restricciones tiene el modo usuario y por qué existen? **R:**
    
    - **Modo Usuario:** Es el modo en el que se ejecutan las aplicaciones normales. Tiene restricciones en las instrucciones que puede ejecutar y en el acceso directo al hardware.
    - **Modo Kernel (o Privilegiado):** Es el modo en el que se ejecuta el kernel del SO. Tiene acceso total a todas las instrucciones y al hardware.
    - Las restricciones en modo usuario existen por **seguridad y estabilidad**. Impiden que un programa de usuario malicioso o con errores pueda dañar el sistema operativo o interferir con otros programas.
    
7. **P:** Explique cómo se realiza el cambio de modo de usuario a modo kernel. ¿Cuáles son las dos formas principales mencionadas y cuál es más eficiente? **R:** El cambio de modo usuario a kernel se realiza cuando un programa de usuario necesita un servicio privilegiado.
    
    - **Instrucción `syscall`:** Es una instrucción específica que cambia el modo y transfiere el control a una rutina del kernel. Es la forma más **eficiente**.
    - **Interrupción/Excepción:** En algunas arquitecturas, se puede forzar una interrupción para pasar a modo kernel. Es menos eficiente que `syscall` porque el manejo de interrupciones es más costoso.
    
8. **P:** ¿Qué significa que una instrucción sea "privilegiada"? Dé un ejemplo de una operación que requiera modo kernel. **R:** Una instrucción "privilegiada" es aquella que solo puede ser ejecutada cuando la CPU está en modo kernel.
    
    - **Ejemplo:** Escribir directamente en un sector específico del disco duro, deshabilitar interrupciones, o modificar estructuras internas del sistema operativo.
    
9. **P:** ¿Qué es un registro y cuál es su importancia en la arquitectura de la CPU? **R:** Un **registro** es una pequeña porción de memoria de muy alta velocidad ubicada directamente dentro de la CPU. Son cruciales porque almacenan datos e instrucciones que la CPU necesita para sus operaciones inmediatas, permitiendo un acceso extremadamente rápido y optimizando el rendimiento del procesador.
    
10. **P:** Describa las fases del ciclo de instrucción básico de una CPU. ¿En qué momento se verifican las interrupciones? **R:** Las fases son:
    
    1. **Fetch (Búsqueda):** La CPU busca la siguiente instrucción en memoria.
    2. **Decode (Decodificación):** La CPU interpreta la instrucción.
    3. **Fetch Operands (Búsqueda de Operandos):** La CPU busca los datos necesarios para la instrucción.
    4. **Execute (Ejecución):** La CPU realiza la operación.
    5. **Write Back (Escritura de Resultado):** La CPU escribe el resultado de la operación. Las interrupciones se verifican **después de cada ciclo de instrucción completo**.
    
11. **P:** Explique la diferencia fundamental entre una interrupción y una excepción, incluyendo su origen y naturaleza (síncrona/asíncrona). Proporcione un ejemplo de cada una. **R:**
    
    - **Interrupción:** Evento **asíncrono** generado por un dispositivo de **hardware externo** a la CPU (ej. disco duro termina una operación, teclado presionado).
    - **Excepción:** Evento **síncrono** generado por la propia **CPU** debido a una condición que ocurre _durante_ la ejecución de una instrucción (ej. división por cero, acceso a memoria no permitido).
    
12. **P:** ¿Qué significa que una interrupción sea "enmascarable" o "no enmascarable"? ¿Por qué existen interrupciones no enmascarables? **R:**
    
    - **Enmascarable:** Puede ser ignorada o deshabilitada temporalmente por software.
    - **No Enmascarable:** No puede ser ignorada y debe ser atendida inmediatamente. Existen para manejar errores de hardware críticos (ej. fallo de voltaje) que requieren una respuesta inmediata para evitar daños mayores al sistema.
    
13. **P:** Describa el proceso general que sigue la CPU cuando se produce una interrupción, desde su generación hasta la reanudación del proceso original. ¿Qué papel juega la pila del sistema en este proceso? **R:**
    
    1. El dispositivo genera la interrupción.
    2. La CPU termina la instrucción actual.
    3. Se guarda el estado del proceso actual (registros, PC, PSW) en la **pila del sistema**.
    4. Se carga la rutina de atención a la interrupción (ISR).
    5. La ISR procesa la interrupción.
    6. Se restaura el estado del proceso original desde la pila del sistema.
    7. El proceso original reanuda su ejecución. La pila del sistema es crucial para **guardar el contexto** del proceso interrumpido, permitiendo que se reanude correctamente después de que la interrupción sea atendida.
    
14. **P:** ¿Cómo se manejan múltiples interrupciones que ocurren simultáneamente o en un corto intervalo de tiempo? **R:** Se manejan principalmente por **prioridad**. Cada interrupción tiene una prioridad asignada. Las interrupciones de mayor prioridad pueden incluso interrumpir el manejo de una interrupción de menor prioridad (anidamiento).
    
15. **P:** Compare los tres mecanismos de entrada/salida (programada, por interrupciones, por DMA) en términos de eficiencia de la CPU y complejidad. **R:**
    
    - **Programada (Polling):** CPU inicia I/O y espera activamente. **Menos eficiente** (CPU desperdicia ciclos), **simple**.
    - **Por Interrupciones:** CPU inicia I/O y hace otras tareas; dispositivo interrumpe al finalizar. **Más eficiente** que polling (CPU hace trabajo útil), **más compleja**.
    - **DMA (Direct Memory Access):** Un controlador DMA maneja la transferencia de datos directamente entre dispositivo y memoria; CPU solo inicia y recibe una interrupción final. **Más eficiente** (CPU liberada casi por completo), **más compleja**.
    
16. **P:** ¿En qué escenarios específicos podría ser preferible la I/O programada sobre la I/O por interrupciones o DMA, a pesar de su aparente ineficiencia? **R:** Podría ser preferible para operaciones de I/O **extremadamente cortas** donde el overhead (costo) de un cambio de contexto o el manejo de una interrupción sería mayor que el tiempo de espera activa. Por ejemplo, si se espera que el dato esté disponible casi instantáneamente (ej. una caché muy rápida).
    
17. **P:** Explique el papel del controlador DMA en las operaciones de I/O. ¿Cómo contribuye a la eficiencia de la CPU? **R:** El **controlador DMA** es un componente de hardware que se encarga de transferir datos directamente entre un dispositivo de I/O y la memoria principal, sin la intervención constante de la CPU. Contribuye a la eficiencia de la CPU al **liberarla** de la tarea de gestionar cada byte de la transferencia, permitiéndole realizar otras operaciones mientras la DMA se encarga de la I/O.
    

**Preguntas de Análisis y Aplicación:**

1. **P:** ¿Cómo se relaciona la "pirámide" de un sistema informático (hardware, SO, utilidades, programas) con los diferentes roles de los usuarios y desarrolladores? **R:** La pirámide muestra las capas de abstracción. El **usuario final** interactúa con la capa superior (programas). El **programador** utiliza las utilidades y servicios del SO. El **diseñador de SO** trabaja en las capas inferiores, interactuando directamente con el hardware y el kernel. Cada rol se enfoca en una capa diferente de la abstracción.
    
2. **P:** Explique el principio de "gran poder conlleva gran responsabilidad" en el contexto de la programación a bajo nivel en sistemas operativos. **R:** Este principio significa que cuanto más cerca se programa del hardware y del kernel (mayor poder y control), mayor es la responsabilidad de asegurar que el código sea correcto y seguro. Un error a bajo nivel puede tener consecuencias catastróficas, como colgar todo el sistema o comprometer la seguridad, a diferencia de un error en una aplicación de usuario.
    
3. **P:** Utilice la analogía de la biblioteca para explicar los tres tipos de I/O (programada, por interrupciones, por DMA). **R:**
    
    - **I/O Programada:** Vas a la biblioteca, pides un libro y te quedas **esperando en el mostrador** hasta que te lo traen. (CPU ocupada esperando).
    - **I/O por Interrupciones:** Vas a la biblioteca, pides un libro, te vas a **hacer otras cosas** y la biblioteca te **avisa** (interrupción) cuando el libro está listo para que lo recojas. (CPU liberada, pero debe atender avisos).
    - **I/O por DMA:** Vas a la biblioteca, pides un libro, y la biblioteca se encarga de que **alguien te lo lleve directamente a tu casa** sin que tengas que volver a la biblioteca. (CPU casi completamente liberada).