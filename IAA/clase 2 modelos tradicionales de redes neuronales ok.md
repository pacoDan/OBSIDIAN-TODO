https://youtu.be/j18B7BKfiRc?list=PLfQtPEPnkUVnm3CNtV6f02__b5-SrQOaZ&t=3248

### **Introducción a Redes Neuronales Tradicionales y Machine Learning**

- **Contexto General:** La sesión aborda la aplicación de Machine Learning y redes neuronales artificiales tradicionales, diferenciándolas de las redes profundas (Deep Learning) que se verán en futuras clases. Aunque las redes profundas son más modernas, ambas comparten principios fundamentales.
- **Jerarquía de Tecnologías:**
    
    - Inteligencia Artificial (IA)
    - Machine Learning (ML) es un subtipo de IA.
    - Redes Neuronales Artificiales (RNA) son un subtipo de ML.
    
- **Objetivo de la Clase:** Repasar y aplicar conceptos de redes neuronales artificiales a través de ejemplos prácticos en Google Colab.
### **Modelos de Redes Neuronales Multicapa (MLP) y su Aplicación**

- **Clasificación vs. Estimación:**
    
    - **Clasificación:** La salida es discreta (ej., categorías de flores).
    - **Estimación:** La salida es un atributo continuo (ej., un número).
    
- **Ejemplo con Datos de Flores Iris:**
    
    - **Carga de Datos:** Se utilizan datos de flores Iris (largo y ancho de pétalo y sépalo) para clasificar la especie.
    - **Preparación de Datos:**
        
        - **Vectores X e Y:** Los datos de entrada se organizan en un vector X y las clases de salida en un vector Y. Es crucial que ambos tengan la misma cantidad de ejemplos.
        - **Normalización (Opcional):** Se puede normalizar los datos para llevarlos a la misma escala (ej., entre 0 y 1) usando métodos como `MinMaxScaler`. Esto puede mejorar el aprendizaje, especialmente con valores dispares.
        - **División de Datos:** Los datos se dividen en conjuntos de entrenamiento (75%) y prueba (25%). Para clasificación, se usa muestreo estratificado para asegurar una distribución equitativa de clases en ambos conjuntos.
        
    
- **Definición del Modelo MLP:**
    
    - **Capas Ocultas:** Se define la cantidad de capas ocultas y neuronas por capa (ej., una capa de 8 neuronas, o dos capas de 10 y 4 neuronas). La capa de entrada y salida son automáticas.
    - **Funciones de Activación:** Las más comunes son ReLU, sigmoidal y tangente hiperbólica. ReLU es la más usada.
    - **Capa de Salida:**
        - **Softmax:** Para clasificación multiclase, devuelve una puntuación para cada clase, eligiendo la de mayor puntuación.
        - **Lineal:** Para estimación o cuando se desea que la red devuelva un número que represente la clase.
        
    - **Parámetros Entrenables:** El modelo muestra la cantidad total de pesos de las conexiones que se ajustarán durante el entrenamiento.
    - **Optimizador:** El algoritmo para ajustar los pesos. Adam es el más recomendado por su eficiencia, aunque se menciona el gradiente decreciente. El _learning rate_ (tasa de aprendizaje) puede ser dinámico con optimizadores como Adam.
    
- **Entrenamiento del Modelo:**
    
    - **Épocas:** Número de veces que la red cicla sobre los datos de entrenamiento.
    - **Métricas:** Durante el entrenamiento, se monitorean el _accuracy_ (exactitud) y el _loss_ (error) para los datos de entrenamiento y validación.
    - **Sobreentrenamiento:** Se explica que un modelo está sobreentrenado si funciona bien con los datos de entrenamiento pero mal con los datos de prueba. Los gráficos de _loss_ y _accuracy_ para entrenamiento y validación ayudan a identificar esto.
    - **Dropout:** Una técnica para prevenir el sobreentrenamiento, donde un porcentaje de conexiones se excluye aleatoriamente del ajuste de pesos en cada época.
    
- **Evaluación del Modelo:**
    
    - **Métricas de Clasificación:** Exactitud general, precisión, recuperación (recall) y F1-score por clase.
    - **Matriz de Confusión:** Representación visual de los aciertos y errores de clasificación por clase.
    - **Métricas de Estimación:** Error absoluto, error relativo, Root Mean Squared Error (RMSE).
    - **Ajuste del Modelo:** Si los resultados no son aceptables, se puede ajustar la topología de la red, el optimizador, el _learning rate_ o la cantidad de épocas. Se sugiere un "ajuste fino" (épocas, optimizador) antes de un "ajuste grueso" (topología de capas).
    
- **Guardado del Modelo:** Se guarda el modelo entrenado (configuración y pesos) para su posterior uso sin necesidad de reentrenar.

### **AutoKeras: Automatización del Diseño de Redes**
- **Función:** AutoKeras es una librería que automatiza la búsqueda de la mejor arquitectura de red neuronal y sus hiperparámetros.
- **Instalación:** No viene preinstalado en Colab y requiere `pip install autokeras`.
- **Funcionamiento:** Se le indica a AutoKeras cuántos intentos debe realizar y cuántas épocas de entrenamiento debe usar por cada intento. AutoKeras prueba diferentes arquitecturas y optimizadores, mostrando un resumen de los resultados.
- **Ventajas:** Puede encontrar arquitecturas complejas y eficientes que serían difíciles de diseñar manualmente.
- **Limitaciones:** No siempre es perfecto y puede generar modelos muy grandes que consumen mucha memoria, especialmente en la versión gratuita de Colab.
### **Redes Neuronales No Supervisadas: Kohonen SOM (Self-Organizing Map)**

- **Propósito:** Realizar _clustering_ (para segmentar datos de grupos similares, agrupación automática de datos) ==sin supervisión==, esta red la hace de manera automática.
- **Arquitectura:** Consta de una capa de entrada y una capa de salida. La capa de salida organiza las neuronas en un mapa topológico (generalmente cuadrado o rectangular), que se puede aplicar para armar clustering de datos.
https://youtu.be/j18B7BKfiRc?list=PLfQtPEPnkUVnm3CNtV6f02__b5-SrQOaZ&t=6494
- **Funcionamiento:** hay una capa de entrada y una capa de salida
    
    - **Neurona Ganadora:** Para cada ejemplo de entrada, se activa la neurona de salida cuyos pesos son más similares (menor distancia euclidiana) a los valores de entrada. ==en la capa de salida hay solo una neurona que devuelve el valor de 1, solo se activa una unica salida==
    - **Zona de Vecindad:**  principio de zona de vecindad,  esto es Durante el entrenamiento, no solo se ajustan los pesos de la neurona ganadora, sino también los de las neuronas cercanas en el mapa topológico. La influencia de la vecindad disminuye con el tiempo y la distancia.
    - **Ajuste de Pesos:** Se utiliza una fórmula que incorpora un _learning rate_ dinámico (que disminuye con las épocas) y una función de vecindad.
    - **Fases de Entrenamiento:** Primero, una ==ordenación global== (ajuste amplio de neuronas) y luego un ==ajuste fino== (especialización de neuronas).
    - **Resultados:** Cada neurona de salida representa un _cluster_. Los pesos finales de las conexiones de cada neurona de salida corresponden a los "centroides" o valores descriptivos de cada _cluster_. 
    
- **Ejemplo con Vinos y Flores Iris:**
    
    - **Vinos:** Se muestra cómo SOM puede agrupar vinos por características químicas, revelando que los vinos tintos forman un _cluster_ y los blancos se dividen en varios subtipos.
    - **Flores Iris:** Se demuestra cómo SOM puede generar _clusters_ que se alinean con las clases originales de las flores, incluso si se le pide un número diferente de _clusters_ (ej., 4 _clusters_ para 3 clases de flores).
    
- **Ventajas:** Útil para descubrir patrones ocultos y segmentar datos automáticamente.

### **Redes Neuronales Supervisadas: LVQ (Learning Vector Quantization)**
==Con aprendizaje supervisado==
==ídem al anterior de dos capas, le agrego una tercer capa, que se conecta con  alguna de esa capa oculta, por lo que hay conectividad parcial entre esas capas, hay una cantidad de neuronas igual a la cantidad de clases que yo quiero conocer==
- **Propósito:** Realizar ==clasificación supervisada==, pero con la capacidad de identificar subclases dentro de cada clase conocida.
- **Arquitectura:**
    - **Capa de Entrada:** Recibe los datos.
    - **Capa Competitiva (Oculta):** Similar a la capa de salida de SOM, pero ahora es una capa oculta. Cada neurona competitiva se conecta a una única neurona de la capa de salida.
    - **Capa de Salida:** Una neurona por cada clase conocida.
    
- **Funcionamiento:**
    
    - **Conectividad:** Conectividad total entre la capa de entrada y la capa competitiva, y parcial entre la capa competitiva y la capa de salida.
    - **Subclases:** La cantidad de neuronas en la capa competitiva define el número de subclases que se generarán por cada clase conocida.
    - **Ajuste de Pesos:** Si la red clasifica correctamente, los pesos del vector ganador se acercan a la entrada. Si se equivoca, los pesos se alejan.
    
- **Ejemplo con Flores Iris:**
    
    - Se configura LVQ para generar dos subclases por cada tipo de flor (setosa, versicolor, virginica).
    - **Métricas:** Se evalúa el rendimiento del modelo con métricas de clasificación (exactitud, errores).
    - **Ventajas:** Entrenamiento rápido y la capacidad de obtener descripciones de subclases dentro de las clases principales.
    

### **Consideraciones Adicionales**

- **Prueba y Error:** El diseño y ajuste de redes neuronales es un proceso iterativo de prueba y error.
- **Calidad de Datos:** La calidad y representatividad de los datos son fundamentales para el éxito del modelo.
- **Aplicaciones Reales:** Se mencionan ejemplos de aplicación de _clustering_ en el análisis de terremotos y la identificación de talentos en deportes (ej., rugby).

En resumen, la transcripción ofrece una visión detallada de las redes neuronales tradicionales, desde su implementación práctica en Google Colab hasta la explicación de modelos específicos como MLP, SOM y LVQ, destacando sus diferencias, aplicaciones y el proceso de entrenamiento y evaluación.