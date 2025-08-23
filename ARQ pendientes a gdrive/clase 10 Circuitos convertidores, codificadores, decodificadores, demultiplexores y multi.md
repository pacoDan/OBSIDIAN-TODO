https://youtu.be/7VZJJ8zZN54?list=PLfQtPEPnkUVmO5uPGUUm0_vS9TDKjqYAp
### **III. Circuitos Convertidores, Codificadores, Decodificadores, Multiplexores y Demultiplexores**

#### **A. Circuitos Convertidores (Ej. BCD 8421 a 2421)**

- **Concepto:** Circuitos cuya función es obtener combinaciones binarias en las salidas que pertenecen a una convención de representación de caracteres (numéricos o alfanuméricos). Las entradas pueden ser señales de dispositivos o combinaciones binarias de otro código.
- **Procedimiento de Diseño:**
    
    1. **Diagrama en Bloques:** Representación de caja negra con entradas (ej. 4 bits BCD puro) y salidas (ej. 4 bits BCD Aiken).
    2. **Tabla de Verdad:**
        
        - Incluir las entradas (ej. BCD 8421) y las salidas esperadas (ej. BCD Aiken).
        - **Entradas Válidas:** Los 10 primeros valores (0 al 9) son válidos para BCD.
        - **Entradas Inválidas:** Las combinaciones del 10 al 15 no son válidas en BCD. Sus salidas son indeterminadas (marcadas con 'X').
        - **Minimización (Opcional):** Las 'X' en las salidas indeterminadas pueden usarse como "comodines" (unos) en mapas de Karnaugh para simplificar el circuito, aunque no es obligatorio.
        
    3. **Formas Canónicas:** Para cada función de salida (ej. f0, f1, f2, f3), encontrar la forma normal disyuntiva (o conjuntiva). Se recomienda usar la disyuntiva para simplificar.
    4. **Dibujar el Circuito:** Graficar el diagrama lógico correspondiente a cada función.
        
        - Se usan compuertas AND para cada minitérmino y una compuerta OR final para unirlos.
        - Es práctico dibujar las variables de entrada y sus negaciones en paralelo para facilitar la conexión.
        
    
- **Importancia de la Simplificación:** Aunque no es obligatoria, simplificar el circuito (ej. con mapas de Karnaugh) resulta en un diagrama más compacto y fácil de graficar.

#### **B. Circuitos Codificadores (Ej. Teclado Numérico a BCD)**

- **Concepto:** Circuitos que toman señales de entrada (ej. teclas de un teclado numérico) y las codifican en un formato binario (ej. BCD puro).
- **Análisis Especial (Simplificación):**
    
    - Normalmente, 10 entradas (teclas) darían 2^10 (1024) combinaciones.
    - **Supuesto Simplificador:** Se asume que solo se presiona una tecla a la vez. Esto reduce drásticamente la tabla de verdad.
    - **Tabla de Verdad Simplificada:** Solo se muestran las filas donde una única tecla está activa (ej. T0 activa, resto en 0; T1 activa, resto en 0, etc.).
    
- **Implementación del Circuito:**
    
    - No se aplican formas canónicas tradicionales debido a la tabla simplificada.
    - **Compuertas OR:** Las funciones de salida (ej. f0, f1, f2, f3) se implementan directamente con compuertas OR.
    - **Ejemplo:** Para f3 (bit más significativo), si se activa con T8 o T9, se usa una compuerta OR que une T8 y T9.
    - **Razón para OR:** Como solo una tecla puede estar activa a la vez, no hay ambigüedad con la OR.
    
- **Entrada Habilitadora:**
    
    - **Propósito:** Diferenciar entre un circuito inactivo (todas las entradas en cero) y la presión de la tecla '0' (que también produce una salida de ceros).
    - **Funcionamiento:**
        
        - Cuando la entrada habilitadora (E) está en 1, el circuito codifica normalmente.
        - Cuando la entrada habilitadora (E) está en 0, el circuito permanece inactivo y todas las salidas son cero, independientemente de las entradas.
        
    - **Implementación:** Se agrega la entrada habilitadora a cada compuerta AND de los minitérminos (si se usaran) o a las compuertas OR (si se implementa directamente).
    

#### **C. Circuitos Decodificadores (Ej. BCD 8421 a Display de 7 Segmentos)**

- **Concepto:** Operan de forma inversa a los codificadores. La información entra como combinaciones binarias y la salida es una representación visual (ej. display de 7 segmentos).
- **Funcionamiento:** La combinación BCD de entrada debe encender o apagar los segmentos del display para formar el número decimal correspondiente.
- **Procedimiento de Diseño:**
    
    1. **Diagrama en Bloques:** Entradas (ej. 4 bits BCD) y salidas (ej. 7 segmentos del display: a, b, c, d, e, f, g).
    2. **Tabla de Verdad:**
        
        - **Entradas:** Las combinaciones BCD válidas (0-9).
        - **Salidas:** Para cada combinación de entrada, se indica qué segmentos del display deben estar encendidos (1) o apagados (0) para formar el número.
        - **Entradas Inválidas:** Las combinaciones no válidas (10-15) pueden usarse para simplificación (con 'X').
        
    3. **Formas Canónicas:** Para cada función de salida (cada segmento: a, b, c, d, e, f, g), se aplica el método de las formas normales (disyuntiva).
    4. **Dibujar el Circuito:** Graficar el diagrama lógico para cada función de segmento.
    

#### **D. Circuitos Decodificadores N por 2 a la N**

- **Concepto:** Circuitos que toman 'N' entradas y activan una única salida de '2 a la N' posibles, según la combinación de entrada.
- **Ejemplo (2x4):**
    
    - **Entradas:** A, B (2 entradas).
    - **Salidas:** f0, f1, f2, f3 (4 salidas).
    - **Funcionamiento:**
        
        - 00 activa f0.
        - 01 activa f1.
        - 10 activa f2.
        - 11 activa f3.
        
    
- **Implementación:**
    
    - Cada salida es un minitérmino de las entradas.
    - f0 = A'B'
    - f1 = A'B
    - f2 = AB'
    - f3 = AB
    - Se usan compuertas AND para cada salida.
    
- **Con Entrada Habilitadora:**
    
    - **Propósito:** Diferenciar entre la combinación 00 y un circuito inactivo.
    - **Funcionamiento:**
        
        - Si la entrada habilitadora (E) es 1, el circuito decodifica normalmente.
        - Si la entrada habilitadora (E) es 0, todas las salidas son 0, independientemente de las entradas A y B.
        
    - **Implementación:** La entrada habilitadora se conecta a cada compuerta AND de las salidas.
        
        - f0 = A'B'E
        - f1 = A'BE
        - f2 = AB'E
        - f3 = ABE
        
    
- **Ejercicio Práctico (3x8):** Se pide un decodificador 3x8. Tendrá 3 entradas (ej. A, B, C) y 8 salidas. El procedimiento es el mismo.

#### **E. Circuitos Multiplexores y Demultiplexores**

- **Demultiplexor (1 a 2^N):**
    
    - **Concepto:** Encaminar información de una única línea de entrada a una de 2^N salidas.
    - **Componentes:**
        
        - **Entrada de Datos (D):** La única línea por donde viene el dato.
        - **Entradas de Selección (C0, C1...):** Determinan a qué salida se transmite el dato.
        - **Salidas (D0, D1...):** Las posibles líneas de salida.
        
    - **Funcionamiento:** Las entradas de selección eligen una única salida para transmitir el dato de entrada. Las demás salidas permanecen en cero.
    - **Ejemplo (1x4):**
        
        - Entradas de Selección: C0, C1.
        - Salidas: D0, D1, D2, D3.
        - Si C1C0 = 00, D0 = D (el dato de entrada). D1, D2, D3 = 0.
        - Si C1C0 = 01, D1 = D. D0, D2, D3 = 0.
        
    - **Implementación:** Cada salida es el AND de las entradas de selección (negadas o sin negar según la combinación) y la entrada de datos (D).
        
        - D0 = C1'C0'D
        - D1 = C1'C0D
        - D2 = C1C0'D
        - D3 = C1C0D
        
    
- **Multiplexor (2^N a 1):**
    
    - **Concepto:** Encaminar el dato de una de 2^N entradas a una única línea de salida.
    - **Componentes:**
        
        - **Entradas de Datos (D0, D1...):** Las múltiples líneas de entrada.
        - **Entradas de Selección (C0, C1...):** Determinan qué entrada se transmite a la salida.
        - **Salida (S):** La única línea de salida.
        
    - **Funcionamiento:** Las entradas de selección eligen una única entrada de datos para que su valor se copie a la salida.
    - **Ejemplo (4x1):**
        
        - Entradas de Datos: D0, D1, D2, D3.
        - Entradas de Selección: C0, C1.
        - Salida: S.
        - Si C1C0 = 00, S = D0.
        - Si C1C0 = 01, S = D1.
        
    - **Implementación:** La salida es una compuerta OR de los AND de cada entrada de datos con la combinación de selección correspondiente.
        
        - S = (C1'C0' AND D0) OR (C1'C0 AND D1) OR (C1C0' AND D2) OR (C1C0 AND D3)
        - Se usan compuertas AND para cada combinación de selección con su respectiva entrada de datos, y una compuerta OR final para unir todas las salidas de las AND.
        
    
- **Ejercicios Prácticos:** Se piden multiplexores y demultiplexores con 3 entradas de selección y 8 entradas/salidas de datos. El procedimiento es el mismo.
