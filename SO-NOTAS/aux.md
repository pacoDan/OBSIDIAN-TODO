memoria
### **Segmentación Pura en Gestión de Memoria**

**Escenario:** Sistema con 64KB de memoria, segmentación pura, y un proceso con 3 segmentos (código, pila, datos).

- **Concepto de Segmentación Pura:**
    
    - No hay memoria virtual, las direcciones lógicas se traducen directamente a direcciones físicas sin paginación.
    - La dirección física se calcula como: `Base del Segmento + Offset`.
    - La fragmentación externa es un problema inherente a la segmentación dinámica.
    
- **Reconstrucción de la Tabla de Segmentos:**
    
    - **Identificación de Segmentos:**
        
        - Los segmentos 0 y 1 son adyacentes.
        - El segmento 2 está al final de la memoria.
        
    - **Determinación del Formato de Dirección Lógica:**
        
        - La dirección lógica se divide en `Número de Segmento` y `Desplazamiento (Offset)`.
        - Analizando las direcciones dadas, se deduce que se usan 3 bits para el número de segmento y 13 bits para el desplazamiento. Esto permite identificar hasta 8 segmentos ().
        
    - **Cálculo de Bases y Límites:**
        
        - **Segmento 0:**
            
            - Dirección lógica `0000` se mapea a física `0000`.
            - Offset de `0000` es `0000`.
            - Base del segmento 0: `0000` (física) - `0000` (offset) = `0000`.
            - Límite del segmento 0: Se calcula restando la base del segmento 0 a la base del segmento 1.
            
        - **Segmento 1:**
            
            - Dirección lógica `201` se mapea a física `0FFF`.
            - Offset de `201` es `001`.
            - Base del segmento 1: `0FFF` (física) - `001` (offset) = `0FFE`.
            - Límite del segmento 1: La dirección lógica `201F` genera un "segmentation fault", lo que indica que `201` es la última dirección válida del segmento. Por lo tanto, el límite es el offset de `201` (que es `001`).
            
        - **Segmento 2:**
            
            - Dirección lógica `4077` se mapea a física `FFF7`.
            - Offset de `4077` es `077`.
            - Base del segmento 2: `FFF7` (física) - `077` (offset) = `FFF0`.
            - Límite del segmento 2: Como está al final de la memoria (64KB = `FFFF`), y la base es `FFF0`, el límite es `FFFF` - `FFF0` = `000F`.
            
        
    
- **Identificación de Segmentos (Código, Pila, Datos):**
    
    - Si una escritura en la dirección `200` (segmento 2) genera una interrupción por modo inválido, el segmento 2 es probablemente el segmento de código (ya que el código no debería ser modificable).
    - Los otros segmentos (0 y 1) serían pila y datos, que permiten escritura.
    
- **Tipo de Fragmentación:**
    
    - **Fragmentación Externa:** Es el tipo de fragmentación presente en la segmentación pura, ya que las particiones de memoria son dinámicas y pueden dejar huecos no contiguos entre los segmentos.
    

**Pregunta de Examen:** Dada una dirección lógica en un sistema de segmentación pura, ¿cómo se determina el número de segmento y el desplazamiento? **Respuesta:** Se debe analizar el formato de la dirección lógica (generalmente en hexadecimal o binario) y determinar cuántos bits se utilizan para el número de segmento y cuántos para el desplazamiento. Esto se deduce a menudo de la cantidad de segmentos que el sistema puede manejar y de las direcciones lógicas de ejemplo proporcionadas. Una vez identificados los bits, se separan para obtener el número de segmento y el offset.

### **7. Ejercicios de Parcial (Recomendaciones)**

- **Paginación bajo Demanda (Ejercicio 2):**
    
    - Implica calcular el número de página y el desplazamiento a partir de una dirección lógica, aplicar algoritmos de sustitución de páginas (FIFO, LRU, Clock Modificado) y determinar qué algoritmo se utilizó basándose en el estado final de la tabla de páginas.
    - **Clave:** Entender cómo los bits de la dirección lógica se dividen para la página y el offset, y cómo cada algoritmo de sustitución maneja los reemplazos.
    
- **File System (Lectura/Escritura entre Volúmenes - Ejercicio 95):**
    
    - Mover un archivo entre volúmenes con diferentes tamaños de bloque.
    - **Clave:** Calcular cuántos bloques se leen del volumen de origen y cuántos bloques se escriben en el volumen de destino, considerando los diferentes tamaños de bloque. Esto implica entender que la cantidad de bloques puede cambiar incluso si el tamaño del archivo es el mismo.
    

**Consejo General para Exámenes:**

- **Convertir a Binario:** Para cálculos de direcciones y offsets, convertir a binario facilita las operaciones y reduce errores.
- **Explicar el Razonamiento:** No solo dar la respuesta, sino explicar el "por qué" de cada paso y decisión.
- **Asumir Memoria Infinita:** A menos que se especifique lo contrario, para ejercicios de File System, asumir que hay suficiente memoria para cargar estructuras de datos (como bloques de punteros o inodos) una vez.