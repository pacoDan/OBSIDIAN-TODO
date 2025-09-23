https://www.youtube.com/watch?v=3uuELl4l0Ts&list=PL6oA23OrxDZDQEFo7aKBceotX48vLmQYA&index=4&pp=iAQB
A continuación, se presenta un resumen estructurado de la transcripción sobre sistemas operativos y arquitectura de computadoras, incluyendo detalles clave y posibles preguntas de examen:
### **Introducción a los Sistemas Operativos**

- **Propósito Principal:** Un sistema operativo (SO) permite a los usuarios interactuar con la computadora de manera intuitiva y ejecutar programas sin necesidad de conocimientos técnicos profundos sobre el hardware.
- **Funciones Clave para el Usuario Final:**
    
    - **Interfaz de Usuario:** Facilita la interacción con la máquina (ej. interfaz gráfica vs. línea de comandos).
    - **Interfaz con Dispositivos:** Permite el uso de periféricos sin necesidad de programarlos a bajo nivel.
    - **Ejecución de Programas:** Fundamental para el usuario común, ya que determina qué aplicaciones pueden correr en el SO.
    
- **Funciones Técnicas (Más allá del Usuario Final):**
    - Administración de memoria.
    - Administración de dispositivos de entrada/salida.
    - Administración de archivos.
    - Comunicación entre programas.

### **Estructura de un Sistema Informático (Pirámide)**

- **Hardware (Base):** Componentes físicos de la computadora.
- **Sistema Operativo:** Capa de software que gestiona el hardware.
- **Utilidades:** Herramientas como compiladores, interfaces gráficas (ej. en Linux se pueden elegir varias).
- **Programas (Cima):** Aplicaciones que el usuario final utiliza.
- **Roles de Usuario:**    
    - **Usuario Final:** Interactúa principalmente con los programas.
    - **Programador:** Utiliza utilidades y servicios del SO.
    - **Diseñador de SO:** Trabaja directamente con el hardware y el kernel.
### **Componentes del Sistema Operativo**

- **Kernel:**
    
    - **Definición:** La parte del SO más cercana al hardware, siempre residente en memoria.
    - **Residencia en Memoria:** Si el kernel es grande, consume mucha memoria constantemente. La recompilación del kernel en Linux busca reducir su tamaño.
    - **Funcionalidad:** Gestiona recursos críticos como la memoria y el acceso a dispositivos.
    
- **System Calls (Llamadas al Sistema):**
    
    - **Definición:** Interfaz que permite a los programas de usuario solicitar servicios al kernel.
    - **Acceso a Hardware/Memoria:** Permiten operaciones como leer archivos (requiere que el disco gire y asigne memoria).
    - **Rendimiento:** Son rápidas y eficientes a nivel de rendimiento.
    - **Complejidad:** Son "rústicas" para la programación diaria; a menudo se necesitan varias system calls para una operación simple (ej. `malloc` usa varias system calls).
    - **Portabilidad:** Generalmente asociadas a un SO específico, aunque algunas son estándar.
    
- **Bibliotecas del Sistema:**
    
    - **Definición:** Conjuntos de funciones que agrupan system calls para usos comunes (ej. pedir memoria, abrir/leer archivos).
    - **Ventajas:**
        
        - **Comodidad:** Más fáciles de usar para los programadores.
        - **Portabilidad:** Permiten que el código funcione en diferentes SO sin preocuparse por las implementaciones subyacentes (ej. `printf` funciona igual en Linux y Windows).
        - **Estabilidad:** Menos propensas a errores que el uso directo de system calls.
        
    - **Desventajas:** Pueden ser menos flexibles o performantes que el uso directo de system calls para casos muy específicos.
    

### **Modos de Ejecución (Privilegios)**

- **Concepto:** Mecanismo de seguridad que controla las instrucciones que un programa puede ejecutar. Se puede pensar como un _flag_ (prendido/apagado).
- **Modo Usuario:**
    
    - **Restricciones:** Solo puede ejecutar un subconjunto de instrucciones. No puede, por ejemplo, deshabilitar interrupciones o acceder directamente a ciertas áreas de hardware.
    - **Solicitud de Servicios:** Para operaciones privilegiadas, debe solicitar al kernel a través de system calls.
    
- **Modo Kernel (Privilegiado):**
    
    - **Acceso Total:** Puede ejecutar todas las instrucciones y acceder directamente al hardware.
    - **Inicio del SO:** El SO arranca en modo kernel y luego pasa a modo usuario para las aplicaciones.
    
- **Cambio de Modo:**
    
    - **Kernel a Usuario:** Sencillo, ya que el kernel tiene control total.
    - **Usuario a Kernel:** Más complejo y controlado para evitar que programas de usuario maliciosos tomen el control.
        
        - **`syscall` Instruction:** Una instrucción específica que cambia a modo kernel y transfiere el control a una rutina del SO para atender la llamada.
        - **Interrupciones/Excepciones:** En algunas arquitecturas, se usa una interrupción forzada para pasar a modo kernel. Esto es más lento que una instrucción `syscall` directa.
        
    
- **Rings de Protección:** Algunas arquitecturas usan múltiples niveles de privilegio (más de un bit) para mayor granularidad (ej. drivers en un nivel intermedio entre usuario y kernel).
- **Ejemplos de Operaciones Privilegiadas:**
    
    - Escribir en un disco.
    - Modificar estructuras internas del SO (ej. identificadores de procesos).
    - Asignar memoria (aunque se solicita vía system call, la asignación real es privilegiada).
    
- **Principio de Responsabilidad:** "Gran poder conlleva gran responsabilidad." Cuanto más cerca del kernel, más poder y más riesgo de romper el sistema si se cometen errores.

### **Arquitecturas de Sistemas Operativos**

- **Monolítico:**
    
    - **Concepto:** Todo el SO (kernel, drivers, servicios) está en un único bloque de código. Cualquier módulo puede llamar a cualquier otro.
    - **Ventajas:**
        
        - **Rendimiento:** Generalmente más rápido debido a la ausencia de "pasamanos" entre componentes.
        - **Actualización:** Más fácil de actualizar para el usuario final (ej. "se actualizó Windows").
        - **Gestión de Dependencias:** Todas las partes usan la última versión de las funciones, evitando problemas de dependencia entre módulos.
        
    - **Desventajas:**
        
        - **Estabilidad:** Más propenso a errores; un fallo en una parte puede colgar todo el sistema.
        - **Desarrollo:** Más desordenado y difícil de mantener para los programadores (ej. el kernel de Linux o proyectos Java monolíticos). Requiere mucha organización y procesos de revisión rigurosos.
        
    
- **Multicapa:**
    
    - **Concepto:** El SO se divide en capas, cada una con responsabilidades específicas e interfaces bien definidas. Los pedidos fluyen de capas superiores a inferiores y las respuestas de inferiores a superiores.
    - **Ventajas:** Mejor organización y modularidad.
    - **Desventajas:** Puede introducir "pasamanos" que afectan el rendimiento y problemas de comunicación entre equipos que mantienen diferentes capas. Menos común en SO reales.
    
- **Microkernel:**
    
    - **Concepto:** Solo las funciones esenciales (gestión de procesos, memoria básica, comunicación interprocesos) residen en el kernel (modo kernel). La mayoría de los servicios (drivers, sistemas de archivos) se ejecutan como procesos de usuario.
    - **Ventajas:**
        
        - **Estabilidad:** Mucho más estable, ya que un fallo en un servicio de usuario no colapsa todo el kernel (ej. si falla el gestor de archivos, se reinicia solo).
        - **Modularidad:** Facilita el desarrollo y la depuración de servicios.
        
    - **Desventajas:**
        
        - **Rendimiento:** Significativamente más lento debido a la constante necesidad de cambiar entre modo usuario y modo kernel para cada solicitud de servicio. Cada system call implica un cambio de contexto.
        
    - **Ejemplo:** MINIX (diseñado para enseñanza, no para uso comercial).
    
- **Máquinas Virtuales (VMs):**
    
    - **Concepto:** Software que emula hardware, permitiendo ejecutar múltiples sistemas operativos o instancias de un SO en una única máquina física.
    - **Tipo 2 (Hosted Hypervisor):**
        
        - **Funcionamiento:** Se instala un software (ej. VirtualBox) sobre un SO anfitrión, y este software emula el hardware para el SO invitado.
        - **Uso:** Común para desarrollo, pruebas (ej. probar aplicaciones en diferentes SO o versiones), y entornos de laboratorio (como en el curso).
        - **Ejemplo:** VirtualBox, emuladores de consolas (aunque más sofisticados por la traducción de instrucciones y acceso directo a memoria).
        
    - **Tipo 1 (Bare-Metal Hypervisor):**
        
        - **Funcionamiento:** El hipervisor se instala directamente sobre el hardware, y los SO invitados se ejecutan sobre él. El kernel ya tiene el hipervisor integrado.
        - **Uso:** Entornos de servidor, computación en la nube (ej. Amazon EC2), donde se particiona un hardware potente en múltiples máquinas virtuales.
        - **Ventajas:** Mayor eficiencia y rendimiento que el Tipo 2, ya que no hay un SO anfitrión intermedio.
        
    

### **Posibles Preguntas de Examen**

1. **Funciones del SO:**
    
    - ¿Cuáles son las funciones principales de un sistema operativo desde la perspectiva de un usuario final?
    - Mencione y explique al menos tres funciones técnicas de un sistema operativo que van más allá de la interacción directa del usuario.
    
2. **Kernel y System Calls:**
    
    - Defina qué es el kernel de un sistema operativo y por qué se dice que es "residente en memoria".
    - Explique el propósito de las system calls. ¿Por qué son necesarias y qué ventajas ofrecen a nivel de rendimiento?
    - ¿Cuál es la diferencia fundamental entre usar system calls directamente y usar bibliotecas del sistema? Proporcione ejemplos de cuándo se preferiría una sobre la otra.
    
3. **Modos de Ejecución:**
    
    - Describa los modos de ejecución "modo usuario" y "modo kernel". ¿Qué restricciones tiene el modo usuario y por qué existen?
    - Explique cómo se realiza el cambio de modo de usuario a modo kernel. ¿Cuáles son las dos formas principales mencionadas y cuál es más eficiente?
    - ¿Qué significa que una instrucción sea "privilegiada"? Dé un ejemplo de una operación que requiera modo kernel.
    
4. **Arquitecturas de SO:**
    
    - Compare las arquitecturas de SO monolíticas y microkernel. Mencione al menos dos ventajas y dos desventajas de cada una.
    - ¿Por qué los microkernels, a pesar de su estabilidad, no son ampliamente utilizados en sistemas operativos comerciales?
    - Explique el concepto de máquinas virtuales. Describa la diferencia entre un hipervisor Tipo 1 y Tipo 2, y dé un ejemplo de uso para cada uno.
    
5. **Conceptos Generales:**
    
    - ¿Cómo se relaciona la "pirámide" de un sistema informático (hardware, SO, utilidades, programas) con los diferentes roles de los usuarios y desarrolladores?
    - Explique el principio de "gran poder conlleva gran responsabilidad" en el contexto de la programación a bajo nivel en sistemas operativos.
    

### **Detalles Adicionales y Curiosidades**

- **Recompilación del Kernel en Linux:** Permite optimizar el kernel para un hardware específico, reduciendo el consumo de memoria al eliminar componentes innecesarios.
- **Proceso de Pull Request en Proyectos Monolíticos Grandes:** Se mencionó el ejemplo de un proyecto Java monolítico donde los cambios requieren extensas pruebas y revisiones por múltiples equipos debido a la interconexión de todo el código.
- **Botón "Turbo" en PCs Antiguas:** Curiosidad histórica donde el botón en realidad ralentizaba la CPU para que los juegos antiguos funcionaran correctamente, ya que estaban diseñados para procesadores más lentos.
- **Emuladores de Consolas:** Son un tipo de máquina virtual más sofisticado, ya que no solo emulan hardware, sino que también traducen conjuntos de instrucciones y manejan accesos directos a memoria que eran comunes en consolas antiguas.
- **Recursos Adicionales:** Se mencionaron enlaces a tutoriales para implementar `malloc` propio, comandos útiles de Linux y wikis para construir un SO simple. También se hizo referencia al famoso debate entre Linus Torvalds y Andrew Tanenbaum sobre la arquitectura del kernel.
---
### **Tema 2: Arquitecturas de Sistemas Operativos**

**Preguntas de Definición y Concepto:**

1. **P:** Compare las arquitecturas de SO monolíticas y microkernel. Mencione al menos dos ventajas y dos desventajas de cada una. **R:**
    
    - **Monolítico:**
        
        - **Ventajas:** Más rápido (menos overhead de comunicación), más fácil de actualizar para el usuario.
        - **Desventajas:** Menos estable (un fallo puede colgar todo el sistema), más difícil de desarrollar y mantener (código muy acoplado).
        
    - **Microkernel:**
        
        - **Ventajas:** Más estable (fallos en servicios de usuario no afectan al kernel), más modular y fácil de extender.
        - **Desventajas:** Más lento (mayor overhead por comunicación entre procesos de usuario y kernel), más complejo de diseñar.
        
    
2. **P:** ¿Por qué los microkernels, a pesar de su estabilidad, no son ampliamente utilizados en sistemas operativos comerciales? **R:** Principalmente por su **rendimiento inferior**. El constante cambio de contexto entre modo usuario y modo kernel para cada servicio solicitado introduce una latencia significativa que los hace menos adecuados para sistemas de propósito general donde la velocidad es crucial.
    
3. **P:** Explique el concepto de máquinas virtuales. Describa la diferencia entre un hipervisor Tipo 1 y Tipo 2, y dé un ejemplo de uso para cada uno. **R:** Las **máquinas virtuales (VMs)** son software que emula hardware, permitiendo ejecutar múltiples sistemas operativos en una única máquina física.
    
    - **Hipervisor Tipo 1 (Bare-Metal):** Se instala directamente sobre el hardware físico.
        
        - **Ejemplo de uso:** Servidores en la nube (ej. Amazon EC2), centros de datos empresariales.
        
    - **Hipervisor Tipo 2 (Hosted):** Se instala como una aplicación sobre un sistema operativo anfitrión.
        
        - **Ejemplo de uso:** VirtualBox, VMware Workstation, emuladores de consolas (para desarrollo y pruebas en una PC de escritorio).