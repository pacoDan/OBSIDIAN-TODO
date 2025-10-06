https://youtu.be/nECCu1Am9kY?list=PLAjdG1oI3oIq7wupG2mUKQw9-1cFMmLyo
Aquí tienes un resumen estructurado sobre el concepto de operaciones bloqueantes y no bloqueantes en sistemas operativos y arquitectura de computadoras, incluyendo detalles importantes y posibles preguntas de examen:

### **Operaciones Bloqueantes y No Bloqueantes en Sistemas Operativos**

**1. Introducción a las Operaciones Bloqueantes y No Bloqueantes**

- **Definición:**
     
    - **Operaciones Bloqueantes:** Son aquellas que hacen que el hilo o proceso que las ejecuta se detenga hasta que la operación se complete. Por ejemplo, una llamada a una función de entrada/salida (I/O) que espera a que se complete la lectura o escritura de datos.
    - **Operaciones No Bloqueantes:** Permiten que el hilo o proceso continúe su ejecución sin esperar a que la operación se complete. En lugar de detenerse, el hilo puede realizar otras tareas mientras espera que la operación finalice.
    

**2. Ejemplos de Operaciones Bloqueantes y No Bloqueantes**

- **Operaciones Bloqueantes:**
    
    - Ejemplo: Una llamada a `read()` en un archivo que no tiene datos disponibles. El hilo se bloquea hasta que hay datos que leer.
    - Consecuencia: Puede llevar a un uso ineficiente de los recursos, especialmente en sistemas multihilo, ya que otros hilos pueden estar listos para ejecutarse pero no pueden hacerlo porque el hilo bloqueado monopoliza el CPU.
    
- **Operaciones No Bloqueantes:**
    
    - Ejemplo: Una llamada a `poll()` o `select()` que verifica si hay datos disponibles para leer sin bloquear el hilo.
    - Consecuencia: Permite que el hilo realice otras tareas o verifique el estado de otras operaciones, mejorando la eficiencia y la utilización de recursos.
    

**3. Mecanismos de Implementación**

- **Bloqueo:**
    
    - Cuando un hilo realiza una operación bloqueante, el sistema operativo cambia el estado del hilo a "bloqueado" y lo coloca en una cola de espera. Esto libera el CPU para que otros hilos o procesos puedan ejecutarse.
    - Ejemplo: En un sistema operativo, si un hilo realiza una operación de I/O bloqueante, el sistema operativo puede cambiar el contexto a otro hilo que esté listo para ejecutarse.
    
- **No Bloqueo:**
    
    - Las operaciones no bloqueantes suelen utilizar técnicas como polling, callbacks o promesas para manejar la finalización de la operación sin detener el hilo.
    - Ejemplo: Un hilo puede usar un bucle para verificar periódicamente si una operación de I/O ha finalizado, permitiendo que el hilo realice otras tareas en el ínterin.
    

**4. Ventajas y Desventajas**

- **Ventajas de las Operaciones Bloqueantes:**
    
    - Simplicidad en la programación, ya que el flujo de control es lineal y fácil de seguir.
    - Ideal para operaciones donde la espera es inevitable y no se requiere realizar otras tareas.
    
- **Desventajas de las Operaciones Bloqueantes:**
    
    - Puede llevar a un uso ineficiente de los recursos, especialmente en sistemas multihilo.
    - Puede causar que el sistema se vuelva menos responsivo si muchos hilos están bloqueados.
    
- **Ventajas de las Operaciones No Bloqueantes:**
    
    - Mejora la eficiencia y la utilización de recursos, ya que permite que otros hilos se ejecuten mientras se espera la finalización de una operación.
    - Aumenta la responsividad del sistema, especialmente en aplicaciones interactivas.
    
- **Desventajas de las Operaciones No Bloqueantes:**
    
    - Mayor complejidad en la programación, ya que se requiere manejar el estado de las operaciones y la sincronización entre hilos.
    - Puede llevar a un uso excesivo de CPU si no se implementa correctamente, ya que el polling puede consumir ciclos de CPU innecesariamente.
    

---

### **Posibles Preguntas y Respuestas para Exámenes**

**1. Preguntas de Definición:**

- **Pregunta:** ¿Qué es una operación bloqueante y cómo afecta a un hilo en un sistema operativo?
    
    - **Respuesta:** Una operación bloqueante es aquella que detiene la ejecución del hilo que la invoca hasta que la operación se completa. Esto puede llevar a que el hilo monopolice el CPU, impidiendo que otros hilos se ejecuten.
    
- **Pregunta:** Define una operación no bloqueante y proporciona un ejemplo.
    
    - **Respuesta:** Una operación no bloqueante permite que el hilo continúe su ejecución sin esperar a que la operación se complete. Un ejemplo es el uso de `poll()` para verificar si hay datos disponibles para leer en un socket.
    

**2. Preguntas de Comparación:**

- **Pregunta:** Compara las ventajas y desventajas de las operaciones bloqueantes y no bloqueantes.
    
    - **Respuesta:**
        
        - **Ventajas de Bloqueantes:** Simplicidad en la programación y adecuado para operaciones inevitables.
        - **Desventajas de Bloqueantes:** Uso ineficiente de recursos y posible falta de responsividad.
        - **Ventajas de No Bloqueantes:** Mejora la eficiencia y responsividad del sistema.
        - **Desventajas de No Bloqueantes:** Mayor complejidad en la programación y posible uso excesivo de CPU.
        
    

**3. Preguntas de Escenario:**

- **Pregunta:** Un desarrollador está creando una aplicación que realiza múltiples operaciones de I/O. ¿Qué tipo de operación debería preferir para mejorar la eficiencia y por qué?
    
    - **Respuesta:** Debería preferir operaciones no bloqueantes, ya que permiten que el hilo continúe ejecutándose mientras espera que las operaciones de I/O se completen, mejorando la eficiencia y la utilización de recursos.
    
- **Pregunta:** Si un hilo está realizando una operación bloqueante y se encuentra en un sistema multihilo, ¿qué impacto puede tener en el rendimiento general del sistema?
    
    - **Respuesta:** Puede causar que otros hilos no se ejecuten, lo que lleva a un uso ineficiente de los recursos y puede hacer que el sistema se vuelva menos responsivo, especialmente si muchos hilos están bloqueados.
    

**4. Preguntas de Concepto Avanzado:**

- **Pregunta:** ¿Cómo puede un programador implementar un mecanismo de polling para manejar operaciones no bloqueantes?
    
    - **Respuesta:** Un programador puede implementar un bucle que verifique periódicamente el estado de la operación de I/O. Si la operación no ha finalizado, el hilo puede realizar otras tareas o simplemente esperar un breve período antes de volver a verificar.
    
- **Pregunta:** ¿Qué técnicas se pueden utilizar para evitar el uso excesivo de CPU en operaciones no bloqueantes?
    
    - **Respuesta:** Se pueden utilizar técnicas como el uso de temporizadores para espaciar las verificaciones de estado, o implementar callbacks que se ejecuten cuando la operación de I/O se complete, en lugar de usar un bucle de polling constante.