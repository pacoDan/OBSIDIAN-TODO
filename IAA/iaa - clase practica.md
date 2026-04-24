Aquí tienes la estructura del contenido de la transcripción, junto con las preguntas y respuestas relevantes para un examen:

**Estructura del Contenido de la Transcripción**

- **Desafío 1: Clasificación de Vinos**
    
    - **Problema:** Clasificar vinos (tinto o blanco) utilizando datos de calidad de vino.
    - **Datos:** Numéricos, disponibles en el repositorio `demo ML`, `calidad de vinos`.
    - **Tarea del Estudiante:** Elegir la tecnología de clasificación más adecuada.
    - **Tiempo:** 10 minutos iniciales, extendido a 15 minutos.
    - **Resultados y Discusión:**
        
        - **Franco:** Usó EBQ (posiblemente un error de transcripción, podría ser LVQ o un modelo similar para clustering/clasificación). Precisión: 0.95 (blanco), 0.84 (tinto) en datos de prueba.
        - **Nicolás:** Usó RNA (Red Neuronal Artificial) Multiperceptrón con una capa oculta de 12 neuronas. Precisión: 0.98 (blanco), 0.99 (tinto) en datos de prueba. Considerado el mejor resultado inicial.
        - **Otro estudiante:** Usó red convolucional (CNN) 1D. Precisión: 0.98-0.99. Mencionó sobreentrenamiento con muchas épocas.
        - **Profesor:** Confirmó que los datos están desbalanceados (más ejemplos de blanco).
        
    
- **Interrupción: Consulta sobre el Trabajo Práctico (TP)**
    
    - **Grupo F (Clustering de jugadores de fútbol):**
        
        - **Modelo:** Cojonan (Kohonen Self-Organizing Map).
        - **Estado:** Adaptaron un template, faltan métricas.
        - **Pregunta:** ¿Qué significa "prueba de concepto" o "prototipo funcional" para la segunda entrega?
        - **Respuesta del Profesor:** Entregar algo que funcione y tenga resultados (no necesita automatización ni aplicación). Incluir análisis de resultados y propuestas de mejora para la tercera entrega.
        - **Métricas en Clustering:** No hay métricas supervisadas, pero se evalúa si los clusters tienen sentido y si agrupan jugadores correctamente según sus características.
        - **Evaluación del TP:** No se esperan resultados óptimos en la segunda entrega. Se valora el proceso, el análisis de errores y la propuesta de mejoras para la tercera entrega.
        
- **Desafío 2: Estimación de Sumas**
    
    - **Problema:** Estimar el campo "suma" en el archivo `sumas.ccb`.
    - **Datos:** Pequeños, con dos números de entrada y su suma como salida.
    - **Tarea del Estudiante:** Adaptar modelos para estimación (salida continua).
    - **Tiempo:** 15 minutos.
    - **Resultados y Discusión:**
        
        - **Estudiante 1:** Usó red convolucional. Error absoluto mínimo: 0.01, relativo mínimo: 0.05. Error absoluto máximo: 19.46, relativo máximo: 38.53.
        - **Estudiante 2:** Usó red convolucional, no encontró combinación para error relativo bajo (siempre por encima de 30).
        - **Profesor:** Usó Multiperceptrón. Error máximo: 3, relativo: 5%. Red pequeña (1 capa oculta, 10 neuronas), entrenó por más de 300 épocas sin sobreentrenamiento.
        - **Sugerencia:** Usar algoritmos de regresión para problemas simples puede dar resultados perfectos.
        
    
- **Desafío 3: Estimación de la Serie de Fibonacci**
    
    - **Problema:** Estimar el atributo `F` de la serie de Fibonacci.
    - **Datos:** Serie temporal, donde `F` depende de valores anteriores. La columna `N` (posición) no es útil.
    - **Recomendación del Profesor:** Usar redes recurrentes (RNN) o Transformers.
        
        - **RNN:** Arquitecturas simple, stacked, bidireccional, bidireccional stacked. Capas LCTM o GRU.
        - **Transformer:** Definir número de capas Transformer (multihead) y capas lineales.
        
    - **Tiempo:** 20 minutos.
    - **Resultados y Discusión:**
        
        - **Estudiante 1:** Usó Transfer Learning (no recomendado para este problema). Error relativo mínimo: 0.57, máximo: 290.
        - **Estudiante 2:** Usó red recurrente (GRU). Error relativo promedio: 2.36. Mínimo: 0.11, máximo: 16.57. Error absoluto promedio muy alto (621,000).
        - **Profesor:** Mencionó que la serie de Fibonacci crece exponencialmente, lo que complica el aprendizaje.
        
    
- **Desafío 4: Clasificación de Imágenes de Animales**
    
    - **Problema:** Clasificar imágenes de animales (gato, león, lobo, perro, tigre, zorro).
    - **Datos:** Imágenes divididas en conjuntos de prueba y entrenamiento. Caras de animales.
    - **Tecnologías Sugeridas:**
        
        - `imagional` (convolucional)
        - `IMAC MLP`
        - `AutoKeras` para imagen
        - `Imagas Neuroevolution`
        - `Transfer Learning` (cargando modelo preentrenado y agregando capas, congelando las preentrenadas).
        
    - **Recomendaciones:** Usar imágenes a color para aprovechar la información cromática.
    - **Tiempo:** 20 minutos.
    - **Resultados y Discusión:**
        
        - **Estudiante 1:** Usó Transfer Learning. Exactitud: 60% en datos de prueba.
        - **Estudiante 2:** Usó Transfer Learning. Exactitud: 66% en entrenamiento.
        - **Estudiante 3:** Intentó con convolucional, pero el entrenamiento era muy lento.
        - **Profesor:** Probó con Neuroevolución. Exactitud general: 75%. Problemas con gato/perro (50-60% precisión) y lobo/tigre/gato (clasificaciones raras). Mencionó que los datos son "especiales" y cuesta que el modelo aprenda.
        
    
- **Preguntas Generales y Consejos para el TP**
    
    - **Capa de Salida para Predicción Numérica:** Debe ser lineal (función identidad, `activation=None` en Keras) para valores continuos. Softmax es solo para clasificación.
    - **Optimizador:** Adam es genérico y bueno. Se puede probar NAdam o Adagrad para datos desbalanceados.
    - **Evaluación del TP (Entregas 2 y 3):**
        
        - No es necesario usar todas las tecnologías en la entrega 2.
        - La entrega 2 es una prueba sencilla con análisis y propuestas de mejora.
        - La entrega 3 aplica las mejoras.
        - No se esperan resultados perfectos en la entrega 2. Se valora el proceso, el análisis de errores y las conclusiones.
        - El informe debe demostrar comprensión de la tecnología y cómo se usó.
        
    

**Preguntas y Respuestas para el Examen**

**1. Conceptos Fundamentales de Redes Neuronales**

- **Pregunta:** ¿Cuál es la diferencia fundamental entre un problema de clasificación y uno de estimación (regresión) en el contexto de redes neuronales?
    
    - **Respuesta:**
        
        - **Clasificación:** La red predice una categoría o clase discreta (ej., tinto/blanco, gato/perro). La capa de salida suele usar una función de activación como Softmax para obtener probabilidades sobre las clases.
        - **Estimación (Regresión):** La red predice un valor numérico continuo (ej., la suma de dos números, el siguiente valor de Fibonacci). La capa de salida debe ser lineal (función de activación identidad o `None` en Keras) para permitir la salida de cualquier valor real.
        
    
- **Pregunta:** ¿Por qué es importante la elección de la función de activación en la capa de salida de una red neuronal, especialmente para problemas de estimación numérica?
    
    - **Respuesta:** La función de activación en la capa de salida determina el rango y la naturaleza de los valores que la red puede predecir. Para estimación numérica, se necesita una función lineal (identidad) para permitir que la red genere cualquier valor real. Funciones como Softmax (para clasificación) o Sigmoide (para valores entre 0 y 1) restringirían la salida y no serían adecuadas para predecir valores continuos arbitrarios.
    
- **Pregunta:** ¿Qué es el sobreentrenamiento y cómo se puede identificar en el proceso de entrenamiento de una red neuronal?
    
    - **Respuesta:** El sobreentrenamiento ocurre cuando una red neuronal aprende demasiado bien los datos de entrenamiento, memorizando el ruido y los detalles específicos en lugar de las patrones generales. Esto lleva a un buen rendimiento en los datos de entrenamiento, pero un rendimiento pobre en datos nuevos o no vistos (datos de prueba). Se identifica cuando el error en el conjunto de entrenamiento sigue disminuyendo, pero el error en el conjunto de validación o prueba comienza a aumentar.
    

**2. Tipos de Redes Neuronales y sus Aplicaciones**

- **Pregunta:** Mencione y describa brevemente dos tipos de arquitecturas de redes neuronales mencionadas en la transcripción, indicando un tipo de problema para el que son adecuadas.
    
    - **Respuesta:**
        
        - **Multiperceptrón (MLP) / Red Neuronal Artificial (RNA):** Son redes neuronales feedforward con una o más capas ocultas. Son adecuadas para problemas de clasificación y regresión en datos tabulares o cuando la relación entre entradas y salidas no tiene una estructura temporal o espacial compleja. (Ej. Clasificación de vinos, estimación de sumas).
        - **Redes Convolucionales (CNN):** Son redes especializadas en el procesamiento de datos con una estructura de cuadrícula, como imágenes. Utilizan capas convolucionales para extraer características jerárquicas. Son excelentes para clasificación de imágenes, detección de objetos, etc. (Ej. Clasificación de animales, también se probó para sumas y vinos).
        - **Redes Recurrentes (RNN) / LSTMs / GRUs:** Son redes diseñadas para procesar secuencias de datos, donde el orden de los elementos es importante. Tienen conexiones que forman ciclos, permitiendo que la información persista. Son ideales para series temporales, procesamiento de lenguaje natural. (Ej. Estimación de la serie de Fibonacci).
        - **Transformers:** Son arquitecturas más recientes que utilizan mecanismos de auto-atención (self-attention) para procesar secuencias. Son muy potentes para tareas de series temporales y procesamiento de lenguaje natural, a menudo superando a las RNN tradicionales en ciertos contextos. (Ej. Estimación de la serie de Fibonacci).
        
    
- **Pregunta:** ¿Para qué tipo de problema se recomendaría el uso de una red recurrente (RNN) o un Transformer, y por qué?
    
    - **Respuesta:** Se recomendaría para problemas que involucran **series temporales** o **secuencias de datos**, como la estimación de la serie de Fibonacci. Esto se debe a que estas arquitecturas están diseñadas para capturar dependencias y patrones a lo largo del tiempo o en el orden de los elementos de una secuencia, a diferencia de las redes feedforward que tratan cada entrada de forma independiente.
    

**3. Métricas y Evaluación de Modelos**

- **Pregunta:** En el contexto de un problema de clasificación, ¿qué métricas de evaluación se mencionaron y qué indican?
    
    - **Respuesta:** Se mencionó la **precisión (accuracy)**, que indica el porcentaje de predicciones correctas del modelo. También se habló de la **matriz de confusión**, que muestra el número de aciertos y errores para cada clase, permitiendo ver qué clases se confunden entre sí.
    
- **Pregunta:** Para un problema de estimación (regresión), ¿qué métricas de error se mencionaron y qué representa cada una?
    
    - **Respuesta:** Se mencionaron el **error absoluto** y el **error relativo**.
        
        - **Error Absoluto:** La diferencia en valor absoluto entre la predicción del modelo y el valor real. Indica la magnitud del error en las mismas unidades que la variable objetivo.
        - **Error Relativo:** El error absoluto dividido por el valor real (o el valor absoluto del valor real). Se expresa a menudo como un porcentaje y es útil para entender la magnitud del error en relación con el tamaño del valor que se está prediciendo. Un error absoluto grande puede ser aceptable si el valor real es muy grande, y el error relativo ayuda a contextualizar esto.
        
    

**4. Consideraciones Prácticas en el Entrenamiento**

- **Pregunta:** ¿Por qué el profesor sugirió usar imágenes a color para la clasificación de animales, a pesar de que a veces se usan imágenes en escala de grises?
    
    - **Respuesta:** El profesor sugirió usar imágenes a color porque el color puede ser una característica muy útil para el reconocimiento de animales. Por ejemplo, el patrón de colores de un tigre (negro, blanco, amarillo) o el color rojizo de un zorro son distintivos y pueden ayudar al modelo a identificar el animal de manera más efectiva.
    
- **Pregunta:** ¿Qué es un "prototipo funcional" en el contexto de una entrega de trabajo práctico, y qué se espera de él en la segunda entrega?
    
    - **Respuesta:** Un "prototipo funcional" es una versión inicial del sistema que demuestra que la idea o el modelo funciona y produce resultados, aunque no esté optimizado ni automatizado. Para la segunda entrega, se espera que los estudiantes presenten un modelo que funcione, muestre resultados, y que incluyan un análisis de esos resultados junto con propuestas de mejora para la siguiente entrega. No se requiere que sea óptimo ni que tenga una aplicación detrás.
    
- **Pregunta:** ¿Por qué el profesor enfatizó que no se esperan los "mejores resultados" en la segunda entrega del trabajo práctico?
    
    - **Respuesta:** El profesor enfatizó esto para aliviar la presión sobre los estudiantes. La segunda entrega es una etapa de prueba y aprendizaje. Se valora que los estudiantes hayan experimentado con las tecnologías, entendido cómo funcionan, y puedan analizar los resultados obtenidos (incluso si son subóptimos) para proponer una "futura línea de trabajo" y mejoras para la tercera entrega. El objetivo es evaluar el proceso de aprendizaje y análisis, no solo el rendimiento final del modelo en esa etapa.
    

**5. Variables en Simulación (Contexto del Banco de Sangre)**

- **Pregunta:** En el problema del banco de sangre, identifique la variable de control y la variable de estado.
    
    - **Respuesta:**
        
        - **Variable de Control:** La cantidad de litros de sangre que el hospital provincial solicita semanalmente al gobierno nacional. Es la variable que se puede ajustar para influir en el sistema.
        - **Variable de Estado:** La cantidad de sangre disponible (litros guardados/almacenados) en el banco de sangre del hospital en un momento dado. Representa el estado actual del sistema.
        
    
- **Pregunta:** En el problema del banco de sangre, ¿cuáles son los tres eventos principales que alteran la variable de estado?
    
    - **Respuesta:**
        
        - **Llegada de sangre solicitada:** La sangre que llega semanalmente del gobierno nacional.
        - **Llegada de sangre por donaciones:** Las donaciones de sangre que recibe el hospital.
        - **Entrega/Distribución de sangre:** La sangre que el hospital entrega a los centros de salud municipales.