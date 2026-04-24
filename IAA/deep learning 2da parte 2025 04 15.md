Aquí tienes un resumen detallado de la segunda parte de la presentación sobre Deep Learning, cubriendo los Deep Auto Encoders y las Redes Recurrentes (LSTM y GRU), así como el procesamiento de texto:

### **1. Deep Auto Encoders (DAE o AE)** : pueden generar imágenes a partir de la información aprendida, también corregir imágenes y datos
![[Pasted image 20250710200534.png]]
![[Pasted image 20250710201629.png]]
**Concepto y Funcionamiento:**

- **Aprendizaje No Supervisado:** Los DAEs realizan un aprendizaje no supervisado, similar a las redes de Kohonen, para hacer _clustering_.
- **Objetivo:** Asignar un grupo (llamado "features" o "clusters") a los datos de entrada y luego reconstruir la entrada original a partir de esos features.
- **Aplicación Principal:** Corrección de ruido en imágenes o datos, y completado de datos faltantes.
- **Estructura Básica (Auto Encoder Pequeño):**
    
    - **Capas de Entrada y Salida:** Tienen la misma cantidad de neuronas (ej., 3 de entrada, 3 de salida).
    - **Capa Oculta (Capa de Features):** Es la única capa oculta y debe tener **menos neuronas** que las capas de entrada/salida. Esto fuerza a la red a aprender una representación comprimida (codificación) de los datos y luego a reconstruirlos (descompresión).
    - **Entrenamiento:** Se entrena dando la misma imagen como entrada y como salida deseada.
    

**Deep Auto Encoders (DAE) con Múltiples Capas:**
![[Pasted image 20250710202307.png]]
topología de la red:
![[Pasted image 20250710202852.png]]
- **Arquitectura:** Incorporan múltiples capas ocultas entre la entrada y la capa de features, y entre la capa de features y la salida.
- **Capas de Codificación:** Las capas antes de la capa de features, ==a la izquierda de la capa de features==, donde el número de neuronas disminuye progresivamente (ej., 300 -> 150 -> 50 -> 30 features). es la uuncia que noe sta espejada, siempre menor cantifad de neuronas, si la red noe sta espejada, la red no aprende bien
- **Capas de Reconstrucción:** Las capas después de la capa de features, que son un **espejo inverso** de las capas de codificación (ej., 30 features -> 50 -> 150 -> 300 de salida). Esto asegura que la red pueda reconstruir la información de manera efectiva.
- **Capa de Features:** Siempre es una sola capa y tiene la menor cantidad de neuronas, representando la información principal comprimida.
- **Entrenamiento:** Sigue siendo no supervisado, con la entrada igual a la salida deseada.

**Aplicaciones de los DAEs:** Deep Auto Encoder genera imágenes 
- **Corrección de Ruido en Imágenes:** Se entrena la red con imágenes ruidosas como entrada y las imágenes limpias como salida deseada. Ejemplo: Limpiar dígitos numéricos con ruido.
- **Completado de Datos Faltantes:** Se introducen valores especiales (ej., -99) para representar datos desconocidos en una tabla, y la red aprende a inferir los valores correctos. Ejemplo: Completar atributos de flores Iris.
- **Clustering y Reducción de Dimensionalidad:** La capa de features puede usarse para agrupar datos o reducir su dimensionalidad (similar a PCA).
- **Búsqueda de Imágenes Similares:** Se codifican imágenes en sus features, y luego se buscan imágenes con features similares para encontrar coincidencias.
- **Transcipción de Susurros:** Un DAE puede procesar espectrogramas de susurros, extrayendo features que luego se combinan con otros métodos (ej., Modelos Ocultos de Markov) para transcribir el habla.
- **Generación de Imágenes Falsas (Deepfakes):** Aunque ahora se usan más los modelos de difusión, los DAEs fueron pioneros. Se entrenan dos DAEs con pesos compartidos en la capa de codificación para transferir gestos de una persona a la cara de otra.
### **2. Redes Recurrentes (RNNs), LSTM y GRU**
ideales ==para series temporales y texto, generar texto y procesar texto, análisis de sentimientos==.
**Concepto General de Redes Recurrentes:**

- **Memoria:** Tienen conexiones recursivas que les permiten "recordar" información pasada, haciéndolas ideales ==para series temporales y texto, generar texto y procesar texto, análisis de sentimientos==.
- **Limitación:** Las RNNs básicas tienen dificultades para aprender dependencias a largo plazo.

**Variantes Avanzadas:**

- **LSTM (Long Short-Term Memory):** Introducen "puertas" (input, forget, output gates) que controlan el flujo de información, permitiendo una memoria a corto y largo plazo más efectiva. Esto aumenta la cantidad de pesos a entrenar. ==arquitectura bidireccional, y por ejemplo sirve para entrenar los valores de fibonacci==
- **GRU (Gated Recurrent Unit):** Una versión simplificada de LSTM con solo dos puertas (reset y update), que a menudo ofrece un rendimiento similar con menos complejidad computacional.

**Topologías de Redes Recurrentes:**

- **Simple:** Una capa de entrada, una capa LSTM/GRU, una capa lineal (Dense) y una capa de salida.
- **Stacked (Apiladas):** Múltiples capas LSTM/GRU secuenciales. La salida de una capa LSTM/GRU alimenta la entrada de la siguiente. Útil para información más compleja.
- **Bidireccional:** Dos capas LSTM/GRU que procesan la secuencia en direcciones opuestas (una hacia adelante, otra hacia atrás). Sus resultados se concatenan y alimentan una capa lineal. Ideal cuando el contexto futuro es tan importante como el pasado (ej., traducción, análisis de texto).

**Aplicaciones de Redes Recurrentes:**

- **Predicción de Series Temporales:** Ej., valores de acciones, criptomonedas. Se mostró un ejemplo prediciendo la serie de Fibonacci, donde la arquitectura bidireccional GRU obtuvo los mejores resultados relativos.
- **Procesamiento de Texto:**
    
    - **Clasificación de Texto:** Determinar la categoría de un texto (ej., género de película, tema de noticia, sentimiento).
    - **Estimación de Valores a partir de Texto:** Asignar un puntaje numérico a un texto (ej., puntaje promedio de una película, polaridad de sentimiento).
    - **Generación de Texto:** Crear texto nuevo palabra por palabra o carácter por carácter (ej., citas bíblicas, poesía, nombres de películas).
### **3. Procesamiento de Texto para Redes Neuronales**

Las redes neuronales requieren datos numéricos. El texto debe pasar por varias etapas de preprocesamiento:

**Paso 1: Integración, Limpieza y Formateo:**

- **Integración:** Consolidar todo el texto en un único lugar, manteniendo el orden si es relevante.
- **Limpieza:**
    
    - **Formato:** Eliminar o codificar elementos de formato (negritas, cursivas).
    - **Caracteres Especiales y Puntuación:** Decidir si eliminar o mantener, considerando la semántica.
    - **Corrección de Errores:** Identificar y corregir palabras mal escritas o abreviaturas para mantener la intención.
    
- **Formateo:**
    
    - **Títulos/Subtítulos:** Eliminar o marcar con tags.
    - **Normalización:** Convertir todo a minúsculas/mayúsculas.
    - **Acentos:** Eliminar o mantener.
    - **Palabras Especiales:** Normalizar acrónimos y abreviaturas.
    

**Paso 2: Encoding (Codificación):**

- **Transformar Texto a Números:** Asignar un valor numérico a cada unidad de texto.
- **Nivel de Granularidad:**
    
    - **Carácter:** Cada letra/símbolo es un número.
    - **Palabra:** Cada palabra es un número.
    - **N-grams (Tokens):** Secuencias de N caracteres/palabras.
    - **Sentencia:** Toda una oración.
    
- **Métodos de Codificación:**
    
    - **Vocabulario/Diccionario:** Asignar un número único a cada carácter/palabra según su aparición o un orden predefinido.
    - **One-Hot Vectors:** Representar cada unidad con un vector donde solo una posición es 1 y el resto 0.
    - **Vectores de Distribución:** Codificación basada en el contexto (elementos antes y después).
    

**Paso 3: Embedding:**

- **Representación Vectorial:** Transformar los números codificados en vectores densos de tamaño parametrizable.
- **Aprendizaje:** La capa de embedding es entrenable y aprende la mejor representación vectorial de las palabras/caracteres para la tarea específica.
- **Propósito:** Facilita el aprendizaje de las capas LSTM/GRU al capturar relaciones semánticas entre las palabras.

**Arquitectura de Red para Procesamiento de Texto:**

- **Capas:** Entrada -> Encoding -> Embedding -> LSTM/GRU -> Lineal -> Salida.
- **Generación de Texto (Ejemplo):**
    
    - **Entrenamiento:** Se entrena la red para predecir la siguiente palabra/carácter en una secuencia (ej., "Machine" -> "learning", "learning" -> "is").
    - **Inferencia:** Se le da una palabra inicial, la red predice la siguiente, y esa predicción se realimenta como entrada para generar la siguiente, hasta que se predice un símbolo de fin de texto.
    - **Diversity:** Un parámetro que controla el grado de aleatoriedad en la generación de texto (mayor diversity = más creativo/azaroso).
    

**Otros Usos de Redes Recurrentes (Combinadas con CNNs):**

- **Descripción de Imágenes:** Una CNN procesa la imagen, y una LSTM genera una descripción textual de lo que aparece en ella.
- **Análisis de Eventos en Video:** Una CNN procesa cada frame del video, y una LSTM analiza la secuencia de frames para detectar eventos (ej., peleas, cumplimiento de normas de seguridad).

**Consideraciones Finales:**

- La elección de la arquitectura (simple, stacked, bidireccional) depende de la complejidad de la información y la tarea.
- La calidad de los datos de entrenamiento es crucial, especialmente para el procesamiento de texto, donde las particularidades lingüísticas (acentos, abreviaturas, regionalismos) pueden afectar el rendimiento.
- La tecnología avanza rápidamente; modelos más recientes como los Transformers (LLMs) y los modelos de difusión han superado a las LSTM/GRU en muchas tareas de texto y generación de imágenes, respectivamente.