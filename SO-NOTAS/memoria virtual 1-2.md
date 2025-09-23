### **Memoria Virtual: Conceptos Fundamentales y Funcionamiento**

La memoria virtual es una evolución del concepto de memoria que permite a los sistemas operativos ejecutar procesos más grandes que la memoria física disponible. Su desarrollo fue impulsado por la mejora en la velocidad de los dispositivos de almacenamiento físico (discos).

#### **1. Concepto de Memoria Virtual**

- **Definición:** Permite que un proceso utilice un espacio de direcciones lógicas mucho mayor que la memoria física real disponible.
- **Transparencia:** Para el proceso, la gestión de la memoria virtual es completamente transparente. El proceso solo solicita páginas y el sistema operativo se encarga de su ubicación física (RAM o swap).
- **Ventajas:**
    
    - Permite ejecutar procesos cuyo tamaño excede la memoria física.
    - Aumenta el grado de multiprogramación al permitir que más procesos residan parcialmente en memoria.
    - Facilita la programación al abstraer la gestión de memoria física del programador (a diferencia de los "overlays" manuales).
    

#### **2. Paginación por Demanda**

- **Idea Principal:** Las páginas se cargan en memoria física solo cuando son necesarias. Esto ahorra memoria y permite descargar páginas que ya no se usan.
- **Bits Adicionales en la Tabla de Páginas:**
    
    - **Bit de Presencia/Validez (P/V):** Indica si la página está actualmente en memoria principal (1) o en swap (0).
    - **Bit Modificado (M/D - Dirty Bit):** Indica si la copia de la página en memoria principal ha sido modificada con respecto a su copia en swap.
        
        - **M=0:** Las copias son iguales. La página puede ser descartada de RAM sin escribirla en disco.
        - **M=1:** La copia en RAM ha sido modificada. Debe escribirse en swap antes de ser descartada para mantener la consistencia.
        
    

#### **3. Ciclo de Acceso a Memoria con Paginación por Demanda**

Este es un proceso crucial y complejo:

- **Paso 1: Traducción de Dirección Lógica:**
    
    - La CPU genera una dirección lógica.
    - Se busca la traducción en la TLB (Translation Lookaside Buffer).
    - **TLB Hit:** Si la traducción está en la TLB, se obtiene la dirección física directamente (caso más rápido).
    - **TLB Miss:** Si no está en la TLB, se busca en la tabla de páginas.
    
- **Paso 2: Verificación en la Tabla de Páginas:**
    
    - Se verifica el bit de presencia/validez (P/V) de la página.
    - **P/V = 1 (Página Presente):** La página está en memoria física. Se obtiene el marco, se actualiza la TLB y se accede a la dirección física.
    - **P/V = 0 (Página Ausente - Page Fault):** Se produce una interrupción/excepción de "acceso inválido" (Page Fault).
    
- **Paso 3: Manejo del Page Fault (Sistema Operativo):**
    
    - El sistema operativo toma el control.
    - **Verificación de Validez Real:** Determina si la página es realmente inválida (termina el proceso) o si es un fallo de página (la página es válida pero no está en RAM).
    - **Búsqueda de Marco Libre:**
        
        - **Hay Marcos Libres:** Se reserva un marco libre en memoria física.
        - **No Hay Marcos Libres:** Se debe elegir una "víctima" (página a reemplazar) usando un algoritmo de sustitución de páginas.
            
            - **Bit Modificado de la Víctima (M=0):** La página no ha sido modificada. Se descarta directamente de RAM.
            - **Bit Modificado de la Víctima (M=1):** La página ha sido modificada. Se debe escribir primero en swap (operación de E/S) antes de liberarla.
            
        
    - **Carga de la Página:** Se busca la página en disco (swap) y se carga en el marco asignado (operación de E/S). Esto bloquea el proceso.
    - **Actualización de Tabla de Páginas y TLB:** Una vez cargada, se actualiza la tabla de páginas (P/V=1, se asigna el marco) y la TLB.
    - **Reinicio de la Instrucción:** La instrucción que causó el page fault se reinicia.
    

#### **4. Asignación de Marcos y Sustitución de Páginas**

- **Asignación de Marcos:**
    
    - **Fija:** Un proceso recibe una cantidad predefinida y constante de marcos.
    - **Dinámica:** La cantidad de marcos asignados a un proceso puede variar con el tiempo.
    
- **Sustitución de Páginas (Elección de Víctima):**
    
    - **Local:** El algoritmo elige una víctima solo entre los marcos asignados al propio proceso que causó el page fault.
    - **Global:** El algoritmo puede elegir una víctima entre todos los marcos de memoria física, incluso los de otros procesos.
    
- **Combinaciones Posibles:**
    
    - **Fija y Local:** Común y sencilla. El proceso siempre tiene su cuota de marcos y reemplaza solo dentro de ellos.
    - **Dinámica y Global:** Permite que los procesos crezcan y tomen marcos de otros, pero puede llevar a que un proceso pierda marcos si no está activo.
    - **Dinámica y Local:** Un proceso puede ajustar su número de marcos, pero solo reemplaza dentro de su propia asignación. Esto podría darse si el sistema operativo decide aumentar o disminuir la cuota de marcos de un proceso basándose en su comportamiento, pero el reemplazo interno sigue siendo local.
    - **Fija y Global:** No tiene sentido, ya que si la asignación es fija, no se puede "robar" marcos de otros procesos de forma global.
    

#### **5. Thrashing (Hiperpaginación / Sobrepaginación)**

- **Concepto:** Ocurre cuando un proceso (o el sistema en general) no tiene suficientes marcos de memoria para contener su "localidad" (conjunto de páginas que usa activamente).
- **Síntomas:**
    
    - Alta tasa de fallos de página.
    - El sistema pasa la mayor parte del tiempo realizando operaciones de E/S (cargando/descargando páginas) en lugar de ejecutar instrucciones.
    - Baja utilización de la CPU (la CPU está ociosa esperando las operaciones de E/S).
    - Rendimiento general del sistema muy lento.
    
- **Causas:**
    
    - Demasiados procesos compitiendo por poca memoria física.
    - Procesos con localidades muy grandes que requieren muchos marcos.
    
- **Soluciones:**
    
    - **Añadir más memoria RAM:** La solución más directa, pero no siempre posible.
    - **Reducir el grado de multiprogramación:** Matar o suspender procesos para liberar marcos y permitir que los procesos restantes tengan suficiente memoria para su localidad.
    - **Ajustar la asignación de marcos:** Asegurarse de que cada proceso tenga suficientes marcos para su working set.
    

#### **6. Principio de Localidad**

- **Definición:** La tendencia de un programa a acceder a un conjunto limitado de páginas de memoria en un período de tiempo dado. Es fundamental para el buen funcionamiento de la memoria virtual.
- **Tipos:**
    
    - **Localidad Temporal:** Si se accede a una posición de memoria, es probable que se acceda a la misma posición en un futuro cercano (ej: bucles, variables).
    - **Localidad Espacial:** Si se accede a una posición de memoria, es probable que se acceda a posiciones cercanas en un futuro cercano (ej: arrays, código secuencial).
    
- **Working Set:** Una aproximación a la localidad de un proceso, representando el conjunto de páginas que ha sido referenciado recientemente.

#### **7. Archivos Mapeados en Memoria (Memory-Mapped Files)**

- **Concepto:** Permite tratar un archivo en disco como si fuera una porción de memoria virtual.
- **Funcionamiento:** El sistema operativo utiliza los mismos mecanismos de paginación por demanda para cargar partes del archivo en memoria física cuando son accedidas y escribirlas de vuelta al disco cuando son modificadas o liberadas.
- **Ventajas:**
    
    - Simplifica la E/S de archivos: Se accede al archivo usando punteros de memoria, eliminando la necesidad de llamadas `read()`/`write()` explícitas.
    - Eficiencia: El sistema operativo gestiona automáticamente la carga y descarga de datos, optimizando las operaciones de E/S.
    - Uso en Código de Procesos: El segmento de código de un proceso a menudo se trata como un archivo mapeado en memoria, ya que no necesita ser copiado al swap y se carga por demanda directamente desde el ejecutable en disco.
    

#### **8. Buddy System (Sistema de Compañeros)**

- **Concepto:** Un algoritmo de asignación de memoria contigua que divide la memoria en bloques de tamaño potencia de 2.
- **Funcionamiento:**
    
    - Cuando se solicita memoria, el bloque más pequeño que es una potencia de 2 y es lo suficientemente grande se divide recursivamente en dos "buddies" hasta que se encuentra un bloque adecuado.
    - **Fragmentación Interna:** Puede ocurrir si el tamaño solicitado es menor que el bloque asignado (ej: pedir 30KB y recibir 32KB).
    - **Consolidación:** Cuando dos bloques "buddy" contiguos (que provienen de la misma división) se liberan, se fusionan para formar un bloque más grande. Esto ayuda a reducir la fragmentación externa.
    
- **Ventajas:**
    
    - Rápido para asignar y liberar memoria.
    - Eficiente para la consolidación de bloques libres.
    
- **Uso:** Comúnmente utilizado por el kernel para sus propias asignaciones de memoria debido a su velocidad.

#### **9. Optimizaciones Adicionales**

- **Prepaginación:** Cargar páginas en memoria de forma anticipada (antes de que sean solicitadas) si se predice que serán necesarias. Esto reduce los fallos de página iniciales.
- **Copy-on-Write (COW):** Una técnica de optimización utilizada en operaciones como `fork()`. En lugar de copiar inmediatamente toda la memoria del proceso padre al hijo, ambos procesos comparten las mismas páginas. La copia real de una página solo se realiza cuando uno de los procesos intenta modificarla. Esto ahorra memoria y tiempo si el proceso hijo no modifica muchas páginas.

---

### **Posibles Preguntas de Examen**

- **¿Qué es la memoria virtual y cuáles son sus principales ventajas?**
    
    - **Definición:** La memoria virtual es una evolución del concepto de memoria que permite a los sistemas operativos ejecutar procesos más grandes de lo que la memoria RAM física permite. Surge de la necesidad de manejar programas que requieren más memoria de la disponible físicamente.
    - **Ventajas Principales:**
        
        - **Ejecución de Procesos Grandes:** Permite correr procesos cuyo tamaño excede la capacidad de la RAM física.
        - **Mayor Multiprogramación:** Al no necesitar que todo el proceso esté en memoria principal, se pueden tener más procesos en memoria simultáneamente.
        - **Transparencia para el Programador:** El programador no necesita preocuparse por la gestión de la memoria física, ya que el sistema operativo se encarga de mover las partes del proceso entre la RAM y el disco de forma transparente.
        
    
- **¿Cómo la memoria virtual permite ejecutar procesos más grandes que la RAM física?**
    
    - La memoria virtual logra esto al dividir los procesos en partes (páginas) y solo cargar en la memoria principal (RAM) las partes que son necesarias en un momento dado. Las partes no utilizadas se almacenan en el disco (swap). Cuando una parte necesaria no está en RAM, se produce un "fallo de página" y el sistema operativo la trae del disco a la memoria principal, liberando espacio si es necesario.
    
- **Explique la transparencia de la memoria virtual para el programador.**
    
    - La transparencia significa que el programador trabaja con direcciones lógicas (virtuales) sin tener que preocuparse por dónde se encuentran físicamente los datos en la memoria RAM o en el disco. El sistema operativo se encarga de toda la traducción de direcciones lógicas a físicas y de la gestión del movimiento de páginas entre la RAM y el disco. Para el proceso, simplemente pide una página de memoria y esta se le devuelve, sin saber si estaba en RAM o si tuvo que ser traída del disco.
    

### 2. Paginación por Demanda:

- **Describa el concepto de paginación por demanda.**
    
    - La paginación por demanda es una técnica de memoria virtual donde las páginas de un proceso se cargan en la memoria principal solo cuando son realmente necesarias (es decir, cuando se produce un acceso a una página que no está en RAM). Esto optimiza el uso de la memoria, ya que no se cargan páginas que quizás nunca se utilicen.
    
- **Explique la función de los bits de Presencia/Validez y Modificado en la tabla de páginas. Proporcione ejemplos de cuándo cada bit tomaría un valor específico y qué implicaría.**
    
    - **Bit de Presencia/Validez (P/V):** Indica si la página está presente en la memoria principal (RAM) o no.
        
        - **P/V = 1:** La página está en memoria principal.
        - **P/V = 0:** La página no está en memoria principal (está en swap o nunca ha sido cargada).
        
    - **Bit Modificado (M):** Indica si la página en memoria principal ha sido modificada desde que fue cargada del disco.
        
        - **M = 1:** La página en memoria principal ha sido modificada y es diferente de la copia en disco. Si esta página necesita ser reemplazada, su contenido debe ser escrito de vuelta al disco para mantener la consistencia.
        - **M = 0:** La página en memoria principal no ha sido modificada y es idéntica a la copia en disco. Si esta página necesita ser reemplazada, puede ser descartada sin necesidad de escribirla de vuelta al disco, ya que una copia idéntica ya existe en el disco.
        
    - **Ejemplos de Combinaciones:**
        
        - **P/V = 0, Frame = Guion/Basura:** La página 0 en el ejemplo. Implica que la página no está en memoria principal y quizás nunca ha sido traída.
        - **P/V = 0, Frame = Valor (ej. 2):** La página 1 en el ejemplo. Implica que la página estuvo en memoria principal (usando el frame 2) pero ya no está más; el frame 2 fue asignado a otra página.
        - **P/V = 1, Frame = Valor (ej. 7), M = 1:** La página 2 en el ejemplo. Implica que la página está en memoria principal (en el frame 7) y ha sido modificada. Su contenido en RAM es diferente al de su copia en swap.
        - **P/V = 1, Frame = Valor (ej. 2), M = 0:** La página 3 en el ejemplo. Implica que la página está en memoria principal (en el frame 2) y no ha sido modificada. Su contenido en RAM es idéntico al de su copia en swap.
        
    

### 3. Manejo de Page Faults:

- **Dibuje y explique el ciclo completo de acceso a memoria en un sistema con paginación por demanda, incluyendo el manejo de un page fault.**
    
    - **Ciclo de Acceso a Memoria (Simplificado):**
        
        1. **Dirección Lógica:** La CPU genera una dirección lógica.
        2. **TLB Lookup:** Se busca la traducción en la Translation Lookaside Buffer (TLB).
            
            - **TLB Hit:** Si la traducción está en la TLB, se obtiene la dirección física directamente (caso más rápido).
            - **TLB Miss:** Si no está en la TLB, se busca en la tabla de páginas.
            
        3. **Tabla de Páginas:** Se accede a la tabla de páginas para obtener la dirección física.
            
            - **Página Presente (P/V = 1):** Si la página está en memoria, se obtiene el número de marco y se forma la dirección física. La entrada se añade a la TLB para futuras referencias.
            - **Page Fault (P/V = 0):** Si la página no está en memoria, se produce una interrupción (excepción de page fault).
            
        
    - **Manejo de Page Fault:**
        
        1. **Interrupción:** El hardware genera una interrupción de page fault.
        2. **Sistema Operativo:** El SO toma el control.
        3. **Validación:** El SO verifica si la dirección es válida (si la página existe en el espacio de direcciones del proceso, aunque no esté en RAM). Si es inválida, el proceso se termina.
        4. **Buscar Marco Libre:** El SO busca un marco de página libre en la memoria principal.
        5. **Sustitución (si no hay marcos libres):** Si no hay marcos libres, el SO selecciona una página "víctima" para reemplazar utilizando un algoritmo de sustitución de páginas.
            
            - Si el bit Modificado de la víctima es 1, la página víctima se escribe de vuelta al disco.
            - Si el bit Modificado de la víctima es 0, la página víctima se descarta.
            - Se actualiza la tabla de páginas de la víctima para marcarla como no presente.
            
        6. **Cargar Página:** La página requerida se carga del disco al marco libre (o al marco de la víctima). Esto implica una operación de E/S, que bloquea el proceso.
        7. **Actualizar Tabla de Páginas:** Una vez cargada, la tabla de páginas del proceso se actualiza: el bit P/V se pone a 1, se registra el número de marco, y el bit Modificado se pone a 0.
        8. **Actualizar TLB:** La entrada correspondiente se añade o actualiza en la TLB.
        9. **Reiniciar Instrucción:** La instrucción que causó el page fault se reinicia.
        
    
- **¿Qué sucede si no hay marcos libres cuando se produce un page fault? Describa los pasos involucrados, considerando el bit modificado de la página víctima.**
    
    - Si no hay marcos libres, el sistema operativo debe elegir una página "víctima" para desalojar de la memoria principal.
    - **Selección de Víctima:** Se utiliza un algoritmo de sustitución de páginas (ej., FIFO, LRU, etc.) para seleccionar la página a reemplazar.
    - **Verificación del Bit Modificado:**
        
        - **Bit Modificado = 1:** Si la página víctima ha sido modificada, su contenido debe ser escrito de vuelta al disco (swap) antes de ser desalojada. Esto implica una operación de E/S adicional, lo que añade latencia.
        - **Bit Modificado = 0:** Si la página víctima no ha sido modificada, su contenido es idéntico a la copia en disco, por lo que puede ser descartada directamente sin necesidad de escribirla de vuelta al disco.
        
    - **Actualización de Tablas:** La entrada de la página víctima en la tabla de páginas se marca como no presente (P/V = 0), y el marco se marca como libre.
    - **Carga de Nueva Página:** Una vez liberado el marco, la página que causó el page fault se carga del disco a ese marco.
    
- **¿Por qué la instrucción que causó el page fault se reinicia después de que la página es cargada?**
    
    - La instrucción se reinicia porque el page fault es una interrupción que ocurre _durante_ la ejecución de una instrucción. Para que la instrucción se complete correctamente, la página que necesitaba debe estar disponible en memoria. Una vez que la página ha sido cargada y la tabla de páginas actualizada, el sistema operativo devuelve el control a la CPU para que re-ejecute la misma instrucción. Esta vez, la página estará en memoria, y la instrucción podrá completarse sin problemas.
    

### 4. Asignación y Sustitución:

- **Compare y contraste la asignación fija y dinámica de marcos.**
    
    - **Asignación Fija:**
        
        - **Concepto:** A cada proceso se le asigna una cantidad predeterminada y constante de marcos de memoria. Esta cantidad puede ser la misma para todos los procesos o variar según el tipo de proceso, pero una vez asignada, no cambia durante la ejecución del proceso.
        - **Ventajas:** Simplicidad en la gestión, predecibilidad.
        - **Desventajas:** Puede llevar a un uso ineficiente de la memoria si un proceso necesita más o menos marcos de los asignados en diferentes momentos. Puede causar thrashing si la asignación es muy baja para la localidad del proceso.
        
    - **Asignación Dinámica:**
        
        - **Concepto:** La cantidad de marcos asignados a un proceso puede variar durante su ejecución, adaptándose a sus necesidades cambiantes. El sistema operativo puede aumentar o disminuir los marcos de un proceso según su comportamiento (ej., su localidad).
        - **Ventajas:** Uso más eficiente de la memoria, mayor flexibilidad, puede adaptarse mejor a las necesidades de localidad de los procesos.
        - **Desventajas:** Mayor complejidad en la gestión, puede llevar a problemas como el thrashing si no se gestiona adecuadamente.
        
    
- **Compare y contraste la sustitución local y global de páginas.**
    
    - **Sustitución Local:**
        
        - **Concepto:** Cuando un proceso necesita reemplazar una página, el algoritmo de sustitución elige una página víctima _solo de los marcos asignados a ese mismo proceso_.
        - **Ventajas:** El rendimiento de un proceso no se ve directamente afectado por el comportamiento de otros procesos. Cada proceso gestiona su propio conjunto de marcos.
        - **Desventajas:** Puede ser menos eficiente en el uso global de la memoria, ya que un proceso podría tener marcos infrautilizados mientras otro proceso sufre de falta de marcos.
        
    - **Sustitución Global:**
        
        - **Concepto:** Cuando un proceso necesita reemplazar una página, el algoritmo de sustitución elige una página víctima _de todos los marcos disponibles en el sistema_ (es decir, de cualquier proceso).
        - **Ventajas:** Mayor eficiencia global en el uso de la memoria, ya que los marcos pueden ser asignados dinámicamente a los procesos que más los necesitan.
        - **Desventajas:** El rendimiento de un proceso puede verse afectado por el comportamiento de otros procesos (ej., un proceso "codicioso" podría robar marcos a otros). Puede ser más difícil de depurar y predecir el rendimiento individual de los procesos.
        
    
- **Analice las combinaciones posibles de asignación y sustitución (fija/local, dinámica/global, dinámica/local) y explique por qué algunas combinaciones no tienen sentido.**
    
    - **Fija/Local:**
        
        - **Sentido:** Sí, tiene sentido. Un proceso tiene un número fijo de marcos y solo puede reemplazar páginas dentro de ese conjunto. Es una combinación común y relativamente sencilla de implementar.
        
    - **Dinámica/Global:**
        
        - **Sentido:** Sí, tiene sentido. Los procesos pueden crecer o encoger su asignación de marcos, y el sistema puede robar marcos de cualquier proceso para satisfacer las necesidades de otro. Es la combinación más flexible y potencialmente más eficiente en el uso global de la memoria, pero también la más compleja de gestionar.
        
    - **Dinámica/Local:**
        
        - **Sentido:** Sí, tiene sentido, aunque es menos intuitiva. Un proceso puede tener una asignación dinámica de marcos (el sistema operativo le da o le quita marcos), pero cuando necesita reemplazar una página, solo puede elegir una víctima de su propio conjunto de marcos actual. Esto podría darse si el sistema operativo ajusta periódicamente la asignación de marcos a cada proceso basándose en su comportamiento, pero la política de sustitución interna de cada proceso es local.
        
    - **Fija/Global:**
        
        - **Sentido:** No tiene sentido. Si la asignación es fija, un proceso siempre tiene el mismo número de marcos. Si la sustitución fuera global, significaría que un proceso podría robar marcos de otros, lo que contradice la idea de una asignación fija para ese proceso. Si un proceso tiene una asignación fija, no puede "robar" marcos de otros procesos para aumentar su propia asignación, ni otros procesos pueden "robarle" marcos para disminuir su asignación, ya que la asignación es fija.
        
    

### 5. Thrashing:

-