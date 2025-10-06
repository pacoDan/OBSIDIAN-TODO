### **2. Deadlock (Interbloqueo)**

La segunda parte de la transcripción se centra en el concepto de deadlock, sus condiciones y estrategias para manejarlo.

**Definición de Deadlock:**

- Un deadlock es una situación en la que dos o más procesos o hilos están bloqueados indefinidamente, esperando un recurso que está siendo retenido por otro proceso bloqueado en el mismo ciclo.

**Condiciones Necesarias para Deadlock (Condiciones de Coffman):**

1. **Exclusión Mutua:** Los recursos deben ser no compartibles; solo un proceso puede usar el recurso a la vez. (Ej. un pedazo de calle solo puede ser ocupado por un auto).
2. **Retención y Espera (Hold and Wait):** Un proceso debe estar reteniendo al menos un recurso mientras espera adquirir recursos adicionales que están siendo retenidos por otros procesos. (Ej. un auto ocupa una intersección mientras espera que se libere la siguiente).
3. **NO OCURRE DESALOJO/ No Apropiación (No Preemption):** Los recursos no pueden ser arrebatados a un proceso; deben ser liberados voluntariamente por el proceso que los retiene. (Ej. un auto no puede ser "desalojado" de la calle).
4. **Espera Circular (Circular Wait):** ...

**Representación Gráfica (Grafo de Asignación de Recursos):**

- **Nodos:** Procesos (burbujas) y Recursos (cajas).
- **Instancias de Recursos:** Puntos dentro de las cajas de recursos.
- **Flechas:**
    
    - **Recurso -> Proceso:** Asignación (el recurso está siendo usado por el proceso).
    - **Proceso -> Recurso:** Petición (el proceso está esperando ese recurso).
    
- **Detección de Deadlock:** Un ciclo en el grafo de asignación de recursos indica un posible deadlock. Si cada recurso tiene una sola instancia, un ciclo es una condición suficiente para deadlock. Si los recursos tienen múltiples instancias, un ciclo indica un posible deadlock, pero no necesariamente uno.

**Estrategias para Manejar Deadlock:**

1. **Ignorar el Problema (Ostrich Algorithm):**
    
    - **Descripción:** No hacer nada. Asumir que los deadlocks son raros y que el costo de prevenirlos o detectarlos es mayor que el costo de reiniciar el sistema ocasionalmente.
    - **Ventajas:** Simplicidad, bajo costo de implementación.
    - **Desventajas:** Puede llevar a fallos del sistema y pérdida de datos en entornos críticos.
    - **Aplicación:** Común en sistemas de escritorio donde un reinicio es aceptable.
    
2. **==Prevención== de Deadlock:**
    
    - **Descripción:** Diseñar el sistema para que al menos ==una de las cuatro condiciones== de deadlock nunca se cumpla.
    - **Prevención de Exclusión Mutua:** Generalmente no es viable, ya que muchos recursos son inherentemente no compartibles.
    - **Prevención de Retención y Espera:**
        
        - **Opción 1:** Exigir que un proceso solicite y se le ==asignen todos sus recursos== necesarios antes de comenzar la ejecución. (Ineficiente, ya que los recursos pueden estar ociosos por mucho tiempo).
        - **Opción 2:** Exigir que un proceso libere todos sus recursos actuales antes de solicitar nuevos. (Puede ser ineficiente si el proceso necesita usar recursos en conjunto).
        
    - **Prevención de No Apropiación:**
        
        - **Opción 1:** Si un proceso que retiene recursos solicita uno nuevo y no puede obtenerlo, debe liberar todos los recursos que actualmente retiene.
        - **Opción 2:** Si un proceso solicita un recurso que está siendo retenido por otro proceso que está esperando recursos adicionales, el sistema puede expropiar el recurso al segundo proceso.
        - **Problema:** No siempre es posible (ej. imprimir a mitad de un archivo).
        
    - **Prevención de Espera Circular:**
        
        - **Descripción:** Imponer un orden total a todos los tipos de recursos y exigir que cada proceso solicite los recursos en orden ascendente.
        - **Ejemplo:** ...
        - **Ventajas:** Rompe el ciclo de espera.
        - **Desventajas:** Puede ser ineficiente, ya que los procesos pueden tener que solicitar recursos antes de necesitarlos, o liberar recursos antes de tiempo.
        
    
3. **EVASIÓN/ Evitación de Deadlock (Algoritmo del Banquero):** es pesimista, por que evalua en el peor(máximo uso de recursos) de los casos habria deadlock
    
    - **Descripción:** El sistema operativo evalúa cada solicitud de recursos para determinar si la asignación llevaría al sistema a un estado inseguro (donde un deadlock es posible). Solo se concede la solicitud si el sistema permanece en un estado seguro.
    - **Conceptos Clave:**
        
        - **Estado Seguro:** Un estado en el que existe una secuencia de procesos que pueden completar su ejecución sin entrar en deadlock, incluso si todos solicitan sus recursos máximos.
        - **Estado Inseguro:** Un estado en el que no se puede garantizar que todos los procesos terminen, lo que significa que un deadlock es posible.
        - **Pesimismo:** El algoritmo asume el peor escenario (todos los procesos pedirán sus recursos máximos).
        
    - **Información Necesaria:**
        
        - **`Max` (Máximo):** La cantidad máxima de cada tipo de recurso que cada proceso puede solicitar.
        - **`Allocation` (Asignación):** La cantidad de cada tipo de recurso que cada proceso tiene actualmente asignada.
        - **`Available` (Disponible):** La cantidad de cada tipo de recurso disponible en el sistema.
        - **`Need` (Necesidad):** La cantidad restante de cada tipo de recurso que cada proceso aún necesita (`Need = Max - Allocation`).
        
    - **Algoritmo de Seguridad (Sub-paso del Banquero):**
        
        1. Inicializar `Work = Available` y `Finish[i] = false` para todos los procesos.
        2. Encontrar un proceso `i` tal que `Finish[i] == false` y `Need[i] <= Work`.
        3. Si se encuentra tal proceso:
            
            - `Work = Work + Allocation[i]` (simular que el proceso termina y libera sus recursos).
            - `Finish[i] = true`.
            - Volver al paso 2.
            
        4. Si no se encuentra tal proceso:
            
            - Si `Finish[i] == true` para todos los procesos, el sistema está en un estado seguro.
            - De lo contrario, el sistema está en un estado inseguro.
            
        
    - **Funcionamiento del Algoritmo del Banquero:** funciona de forma pesimista con los recursos máximos

    - **Ventajas:** Evita deadlocks.
    - **Desventajas:** Requiere que los procesos declaren sus necesidades máximas de antemano, puede ser computacionalmente costoso, y los recursos pueden estar subutilizados.
    
4. **Detección y Recuperación de Deadlock:**
    
    - **Descripción:** Permitir que los deadlocks ocurran, detectarlos y luego recuperarse de ellos.
    - **Algoritmo de Detección:**
        
        1. Similar al algoritmo de seguridad, pero utiliza las solicitudes actuales (`Request`) en lugar de las necesidades máximas (`Need`).
        2. **`Available`:** Recursos disponibles.
        3. **`Allocation`:** Recursos asignados.
        4. **`Request`:** Recursos que los procesos están pidiendo actualmente.
        5. **Funcionamiento:**
            
            - Inicializar `Work = Available` y `Finish[i] = false` para procesos que no están pidiendo nada (`Request[i] == 0`).
            - Encontrar un proceso `i` tal que `Finish[i] == false` y `Request[i] <= Work`.
            - Si se encuentra tal proceso:
                
                - `Work = Work + Allocation[i]` (simular que el proceso termina y libera sus recursos).
                - `Finish[i] = true`.
                - Volver al paso anterior.
                
            - Si no se encuentra tal proceso:
                
                - Si `Finish[i] == true` para todos los procesos, no hay deadlock.
                - De lo contrario, los procesos para los cuales `Finish[i] == false` están en deadlock.
                
            
        
    - **Recuperación de Deadlock:**
        
        - **Terminación de Procesos:**
            
            - Terminar todos los procesos involucrados en el deadlock. (Drástico, pérdida de trabajo).
            - Terminar un proceso a la vez hasta que el deadlock se rompa. (Menos drástico, pero puede requerir múltiples terminaciones).
            
        - **Apropiación de Recursos:**
            
            - Seleccionar un proceso víctima y expropiar sus recursos. Estos recursos se asignan a otros procesos para romper el ciclo.
            - **Consideraciones:** Elegir la víctima (ej. proceso con menos recursos, proceso que ha usado menos CPU, proceso con menor prioridad), reversión (el proceso víctima puede necesitar ser revertido a un estado seguro).
            
        
    - **Ventajas:** No impone restricciones en el uso de recursos, lo que puede llevar a una mayor utilización de recursos.
    - **Desventajas:** Puede ser costoso en términos de tiempo de CPU para la detección y de recursos para la recuperación.
    

### **3. Livelock (Bloqueo por Actividad)** mas difíciles de detectar que deadlock

- **Descripción:** Una situación en la que dos o más procesos cambian continuamente de estado en respuesta a los cambios de los otros procesos, sin realizar ==ningún progreso útil==. A diferencia del deadlock, los procesos no están bloqueados, sino que están activos y consumiendo recursos, pero sin avanzar.
- **Ejemplo:** Dos personas que intentan pasar por un pasillo estrecho, cada una cediendo el paso a la otra, pero terminan moviéndose de un lado a otro sin que ninguna logre pasar.
- **Detección:** Mucho más difícil de detectar que el deadlock, ya que los procesos parecen estar ejecutándose normalmente. Se puede inferir por la falta de progreso en las tareas o el consumo constante de recursos sin resultados.
- **Relación con Inanición (Starvation):** El livelock puede llevar a la inanición, donde un proceso nunca logra completar su tarea debido a la actividad constante e inútil.

**Posibles Preguntas de Examen:**

- **Pregunta:** Enumere y explique las cuatro condiciones necesarias para que ocurra un deadlock.
    
    - **Respuesta:** Exclusión Mutua, Retención y Espera, No Apropiación, Espera Circular. (Explicar cada una con un ejemplo).
    
- **Pregunta:** ¿Cuál es la diferencia fundamental entre la prevención y la evitación de deadlock?
    
    - **Respuesta:** La **prevención** asegura que al menos una de las condiciones de deadlock nunca se cumpla. La **evitación** (ej. Algoritmo del Banquero) permite que las condiciones existan, pero evalúa cada solicitud de recursos para asegurar que el sistema siempre permanezca en un estado seguro.
    
- **Pregunta:** Explique el concepto de "estado seguro" en el Algoritmo del Banquero. ¿Por qué el algoritmo es considerado "pesimista"?
    
    - **Respuesta:** Un estado seguro es aquel en el que el sistema puede encontrar una secuencia de ejecución para todos los procesos que les permita completar sus tareas, incluso si todos solicitan sus recursos máximos. Es pesimista porque siempre asume el peor escenario posible (que todos los procesos pedirán sus máximos recursos) para garantizar la seguridad.
    
- **Pregunta:** ¿Cuándo se utiliza el algoritmo de detección de deadlock y qué información necesita?
    
    - **Respuesta:** Se utiliza periódicamente para verificar si existe un deadlock en el sistema. Necesita información sobre los recursos disponibles, los recursos asignados a cada proceso y los recursos que cada proceso está solicitando actualmente.
    
- **Pregunta:** Describa el concepto de livelock y cómo se diferencia del deadlock.
    
    - **Respuesta:** Livelock es una situación donde los procesos cambian de estado continuamente sin hacer progreso, mientras que en deadlock los procesos están bloqueados esperando recursos. En livelock, los procesos están activos y consumiendo CPU, lo que lo hace más difícil de detectar.
    
- **Pregunta:** ¿Qué estrategias de recuperación de deadlock existen y cuáles son sus desventajas?
    
    - **Respuesta:** Terminación de procesos (drástica, pérdida de trabajo) y apropiación de recursos (compleja, requiere reversión de procesos).
    

Este resumen proporciona una base sólida para comprender los semáforos y el deadlock en sistemas operativos, cubriendo los aspectos teóricos y prácticos presentados en la transcripción.