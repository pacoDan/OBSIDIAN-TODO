### **Reestructuración del Contenido: Circuitos Lógicos Fundamentales**

**1. Introducción a los Circuitos Lógicos Combinacionales**

- **Definición:** Circuitos digitales cuyas salidas dependen únicamente de las entradas actuales.
- **Aplicaciones:** Conversión de códigos, codificación, decodificación, selección y distribución de datos.
- **Herramientas de Diseño:** Tablas de verdad, formas canónicas (disyuntiva y conjuntiva), mapas de Karnaugh (para simplificación, aunque no obligatorio en este curso).

**2. Convertidores de Código**

- **Función:** Transforman una combinación binaria de entrada de un código a su equivalente en otro código.
- **Ejemplo Práctico:** Conversor de BCD 8421 a BCD Aiken.
    
    - **Proceso de Diseño:**
        
        - **Diagrama en Bloques:** Representación de caja negra con entradas (BCD 8421) y salidas (BCD Aiken).
        - **Tabla de Verdad:** Definición de las entradas válidas (0-9 para BCD) y sus correspondientes salidas. Se pueden incluir combinaciones inválidas (10-15) con salidas indeterminadas ('X') para simplificación (mapas de Karnaugh).
        - **Formas Canónicas:** Obtención de la función lógica para cada salida (F0, F1, F2, F3) utilizando la forma normal disyuntiva (minitérminos).
        - **Implementación del Circuito:** Dibujo del diagrama lógico utilizando compuertas AND para los minitérminos y compuertas OR para unirlos.
        
    

**3. Codificadores**

- **Función:** Convierten una entrada activa (por ejemplo, la pulsación de una tecla) en una combinación binaria codificada.
- **Ejemplo Práctico:** Codificador de teclado numérico a BCD puro.
    
    - **Consideraciones Especiales:**
        
        - Se asume que solo se presiona una tecla a la vez para simplificar la tabla de verdad.
        - La tabla de verdad muestra la tecla activa y su correspondiente salida BCD.
        
    - **Implementación del Circuito:** Uso de compuertas OR para cada salida, donde cada entrada de la OR corresponde a una tecla que activa esa salida.
    - **Concepto de Entrada Habilitadora:** Permite diferenciar entre un circuito inactivo (todas las salidas en cero) y una entrada válida de cero. Cuando la entrada habilitadora está en 1, el circuito funciona; cuando está en 0, todas las salidas son 0.
    

**4. Decodificadores**

- **Función:** Convierten una combinación binaria de entrada en una salida activa específica.
- **Ejemplo Práctico 1:** Decodificador BCD 8421 a display LED de siete segmentos.
    
    - **Función:** La entrada BCD activa los segmentos LED necesarios para mostrar el dígito decimal correspondiente.
    - **Proceso de Diseño:**
        
        - **Diagrama en Bloques:** Entradas BCD y salidas para cada segmento (a, b, c, d, e, f, g).
        - **Tabla de Verdad:** Para cada combinación BCD (0-9), se especifica qué segmentos deben estar encendidos (1) o apagados (0).
        - **Formas Canónicas:** Obtención de la función lógica para cada segmento (a, b, c, d, e, f, g) utilizando la forma normal disyuntiva.
        - **Implementación del Circuito:** Dibujo del diagrama lógico para cada segmento.
        
    
- **Ejemplo Práctico 2:** Decodificador N por .
    
    - **Función:** Para N entradas, activa una de  salidas posibles.
    - **Implementación:** Cada salida es el resultado de una compuerta AND que combina las entradas (negadas o sin negar) para la combinación específica.
    - **Entrada Habilitadora:** Similar al codificador, permite activar o desactivar el funcionamiento del decodificador.
    

**5. Multiplexores y Demultiplexores**

- **Demultiplexor (DeMux):**
    
    - **Función:** Encaminar información de una única línea de entrada a una de  salidas posibles.
    - **Entradas de Selección:** N entradas que determinan a qué salida se dirige el dato.
    - **Implementación:** Similar al decodificador N por , donde la entrada de habilitación es el dato a transmitir.
    
- **Multiplexor (Mux):**
    
    - **Función:** Seleccionar una de  entradas y encaminar su dato a una única línea de salida.
    - **Entradas de Selección:** N entradas que determinan cuál de las entradas de datos se selecciona.
    - **Implementación:** Cada entrada de datos se combina con las entradas de selección (negadas o sin negar) mediante compuertas AND, y todas las salidas de estas AND se unen en una compuerta OR final.
    

---

### **Preguntas y Respuestas (Basadas en el Contenido y Conceptos Relacionados)**

Dado que el texto no profundiza en flip-flops, registros y contadores, las preguntas se centrarán en los circuitos lógicos combinacionales explicados, con una mención general a su papel en sistemas secuenciales.

**1. Circuitos Lógicos Combinacionales**

- **Pregunta:** ¿Cuál es la característica principal de un circuito lógico combinacional?
    
    - **Respuesta:** La característica principal es que sus **salidas dependen únicamente de los valores actuales de sus entradas**. No tienen memoria ni dependen de estados anteriores.
    
- **Pregunta:** ¿Qué método se utiliza comúnmente para obtener la función lógica de un circuito a partir de su tabla de verdad en este curso?
    
    - **Respuesta:** Se utiliza la **forma normal disyuntiva (suma de minitérminos)**. Aunque la forma normal conjuntiva (producto de maxitérminos) también es válida, la disyuntiva es la preferida para simplificar el proceso en este contexto.
    

**2. Convertidores de Código**

- **Pregunta:** En el diseño de un convertidor de código BCD 8421 a BCD Aiken, ¿por qué se incluyen combinaciones de entrada inválidas (10-15) en la tabla de verdad, marcadas con 'X'?
    
    - **Respuesta:** Estas combinaciones se incluyen para **facilitar la simplificación del circuito utilizando mapas de Karnaugh**. Las 'X' (don't care conditions) actúan como comodines que pueden ser considerados como 0 o 1 para agrupar términos y reducir la complejidad de la función lógica, aunque no son entradas válidas en BCD.
    
- **Pregunta:** Si un convertidor de código BCD 8421 a BCD Aiken recibe la entrada binaria , ¿qué salida se esperaría en BCD Aiken?
    
    - **Respuesta:** La entrada  en BCD 8421 representa el dígito decimal 5. En BCD Aiken (2421), el dígito 5 se representa como . Por lo tanto, la salida esperada sería .
    

**3. Codificadores**

- **Pregunta:** En el ejemplo del codificador de teclado numérico a BCD, ¿por qué se asume que solo se presiona una tecla a la vez?
    
    - **Respuesta:** Esta suposición simplifica enormemente la tabla de verdad y el diseño del circuito. En un teclado numérico real, la pulsación simultánea de dos teclas no produce una suma de sus valores, sino que generalmente se ignora o se procesa una a la vez. Al asumir una única pulsación, se evita la necesidad de manejar  combinaciones de entrada, reduciendo el problema a un conjunto manejable de 10 filas.
    
- **Pregunta:** ¿Cuál es el propósito de una "entrada habilitadora" en un codificador?
    
    - **Respuesta:** La entrada habilitadora permite **distinguir entre un circuito inactivo (todas las salidas en cero) y una entrada válida de cero**. Si la entrada habilitadora está en 0, el circuito está inactivo y todas las salidas son 0, independientemente de las entradas. Si está en 1, el circuito funciona normalmente y codifica las entradas.
    

**4. Decodificadores**

- **Pregunta:** Describa brevemente cómo un decodificador BCD a display LED de siete segmentos forma el número "2".
    
    - **Respuesta:** Para formar el número "2", el decodificador recibe la entrada BCD correspondiente a 2 (que es  en BCD 8421). Basándose en su lógica interna, activa los segmentos LED 'a', 'b', 'g', 'e' y 'd' (poniéndolos en 1), mientras que los segmentos 'c' y 'f' permanecen apagados (en 0). Visualmente, esto crea la forma del número 2 en el display.
    
- **Pregunta:** Si un decodificador N por  tiene 3 entradas, ¿cuántas salidas tendrá y cómo se activará una de ellas?
    
    - **Respuesta:** Si tiene 3 entradas (N=3), tendrá  salidas. Una de las salidas se activará cuando la combinación binaria específica de las 3 entradas coincida con el índice de esa salida. Por ejemplo, si las entradas son , la salida F2 se activará (asumiendo que las salidas están numeradas de F0 a F7).
    

**5. Multiplexores y Demultiplexores**

- **Pregunta:** Explique la diferencia fundamental entre un multiplexor y un demultiplexor.
    
    - **Respuesta:**
        
        - Un **multiplexor (Mux)** selecciona una de varias entradas de datos y la dirige a una única línea de salida. Actúa como un "selector de datos" o "muchos a uno".
        - Un **demultiplexor (DeMux)** toma un único dato de entrada y lo dirige a una de varias líneas de salida posibles. Actúa como un "distribuidor de datos" o "uno a muchos". Ambos utilizan entradas de selección para determinar la ruta del dato.
        
    
- **Pregunta:** En un demultiplexor con dos entradas de selección (C0, C1) y una entrada de datos (D), si las entradas de selección son , ¿a qué salida se transmitirá el dato D?
    
    - **Respuesta:** Si las entradas de selección son  (que representa el decimal 2), el dato D se transmitirá a la salida D2. Las demás salidas permanecerán en 0.
    

---

**Nota sobre Flip-Flops, Registros y Contadores:**

Aunque el contenido proporcionado no los cubre directamente, es importante destacar que los **flip-flops** son los bloques de construcción fundamentales de los circuitos lógicos secuenciales, ya que tienen la capacidad de almacenar un bit de información (memoria).

- Un **registro** es un conjunto de flip-flops que se utilizan para almacenar múltiples bits de datos (una palabra binaria).
- Un **contador** es un tipo especial de registro que sigue una secuencia predefinida de estados (números binarios) en respuesta a pulsos de reloj.

Estos elementos son cruciales para la construcción de sistemas de memoria, unidades de control y otras partes esenciales de la arquitectura de computadoras, y su funcionamiento se basa en la lógica combinacional para sus transiciones de estado.