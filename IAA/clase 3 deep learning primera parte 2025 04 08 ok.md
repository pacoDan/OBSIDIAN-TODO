### **Introducción a Redes Neuronales Profundas y Convolucionales**

- **Fecha y Tema:** La clase, tercera de Inteligencia Artificial Avanzada, se centró en redes de _deep learning_, específicamente redes convolucionales (CNNs) para procesamiento de imágenes.
- **Deep Learning:** Se define como una extensión de las redes neuronales artificiales para procesar datos más complejos.
- **Pioneros:** Se mencionan a Hinton (padre de la Red Multipceptron Back Propagation) y otros dos autores conocidos que en 2006 propusieron la red DBN.
- **Redes DBN:** Aunque fueron importantes por su pre-entrenamiento no supervisado y ajuste fino, actualmente no son muy utilizadas. Se menciona que aún hay ejemplos en Google Colab para quienes deseen explorarlas.
- **Comparativa de Redes:** Se establece una comparación entre redes tradicionales (shallow/vainilla) y redes profundas, introduciendo el concepto de _representation learning_ a través de múltiples capas y la hipótesis del _manifold_ para reconocer variaciones en los datos.
- **Hardware para Procesamiento:** Se discute el uso de GPUs y TPUs para acelerar el procesamiento, señalando que los GPUs suelen ser más rápidos que los TPUs en la experiencia del orador, aunque ambos son superiores a las CPUs.

### **Redes Convolucionales (CNNs)**:  clasificacion de imagenes  es una CNN comun

- **Enfoque Principal:** La clase se enfoca en CNNs y sus variaciones, orientadas al procesamiento de imágenes.
- **Etapas de una CNN:**
    
    - **Convolucional:** ==Aplica filtros (kernels)== para extraer características de la imagen. Estos filtros representan los pesos de las conexiones y permiten compartir valores entre neuronas, reduciendo la cantidad de parámetros y acelerando el entrenamiento sin perder rendimiento. El desplazamiento del kernel es configurable.
    - **Detector (ReLU):** Aplica una función de activación no lineal (comúnmente ReLU) para introducir no linealidad en los datos, facilitando el aprendizaje de patrones complejos.
    - **Pooling:** Comprime el resultado de las etapas anteriores, reduciendo las dimensiones de los datos de salida ( se puede aplicar Max Pooling o Average Pooling).
    
- **Capas en una CNN:**
     
    - **Capas Convolucionales:** Múltiples capas convolucionales procesan la imagen, extrayendo información de diferentes maneras.
    - **Capa Lineal (Densa):** Se recomienda al menos una capa lineal al final para organizar los datos procesados por las capas convolucionales y permitir que la capa de salida identifique la clase correcta. Requiere una capa `reshape` para transformar la matriz de salida de las capas convolucionales en un vector.
    - **Capa Dropout:** ==Ayuda a prevenir el sobreentrenamiento== de la red al seleccionar aleatoriamente qué conexiones se ajustarán durante el entrenamiento.
    - **Capa de Salida:** Puede devolver directamente el ID de la clase o una probabilidad (Softmax) para clasificación.
    
- **Ejemplos de Aplicación:**
    
    - Reconocimiento de personas en Excel (demostrando la implementación de una red entrenada en cualquier tecnología).
    - Reconocimiento de números dibujados a mano.
    - **AlexNet (2012):** Red pionera que ganó la competencia ImageNet, demostrando la eficacia de las CNNs con un error del 16.4%.
    - **GoogleNet (2014):** Red de Google que redujo el error al 6.6% y fue utilizada para mejorar el buscador de imágenes de Google.
    

### **Organización de Datos para Imágenes**

- **Estructura de Directorios:** Se recomienda organizar las imágenes en un árbol de directorios, donde cada directorio lleva el nombre de la clase a la que pertenecen las imágenes (ej. `/train/gato`, `/test/perro`).
- **Archivos de Imagen:** Guardar cada imagen como un archivo PNG o JPEG.
- **Separación de Datos:** Se pueden separar las imágenes de entrenamiento y prueba de forma fija o aleatoria usando scripts.
- **Image Augmentation (Data Augmentation):** Técnica para generar ==mayor diversidad de imágenes== aplicando transformaciones simples (flip, traslación, rotación, zoom, contraste, brillo) de forma aleatoria durante el entrenamiento. Útil cuando se tienen pocas imágenes, aunque puede requerir más ciclos de entrenamiento.
https://youtu.be/0LokQEG5Bcw?list=PLfQtPEPnkUVnm3CNtV6f02__b5-SrQOaZ&t=4535
### **Variaciones de Redes Convolucionales**
![[Pasted image 20250710181607.png]]
los Depp Convolutiuonal Inverse Graphics Netwoks (DCIGN) son para colorear y restarurar imagenes
- **Red Deconvolucional (Inversa):** Intento temprano de redes generativas, donde se indica un ID de clase y la red genera una imagen correspondiente. No fue muy exitosa en sus inicios debido a la baja calidad de las imágenes generadas.
- **Redes DCGAN (Deep Convolutional Generative Adversarial Networks):**  ==DGAN, genera fotos de dormitorios, generar lugares con otros climas, generar edad de una persona==
    - **Concepto:** Redes generativas compuestas por dos subredes: un **generador** (de convolucional) que crea imágenes y un **discriminador** (convolucional) que intenta distinguir imágenes reales de las generadas.
    - **Funcionamiento:** El generador intenta engañar al discriminador, y el discriminador intenta mejorar su capacidad de detección. Esta competencia mutua mejora la calidad de las imágenes generadas con el tiempo.
    - **Aplicaciones:** Generación de imágenes realistas (ej. dormitorios que no existen), transformación de imágenes (ojos cerrados a abiertos, verano a invierno, cebra a caballo). Aunque populares en el pasado, han sido superadas por los modelos de difusión.
- **Modelos de Detección de Objetos (Object Detection):** es subtipo de las convolucionales  ==procesar imagen con múltiples objetos==
    
    - **Propósito:** Reconocer múltiples objetos en una imagen y delimitar su ubicación con un recuadro y un puntaje de confianza.
    - **Etiquetado de Datos:** Requiere etiquetar manualmente las regiones de los objetos en las imágenes de entrenamiento (ej. usando archivos XML con coordenadas).
    - **Métrica:** Se utiliza la métrica mAP (mean Average Precision) para evaluar la precisión de la detección y la delimitación de las regiones.
    - **Arquitecturas:**
        
        - **R-CNN (Region-based CNN):** demora mucho, Primer intento, lento (orden promiedio tarda 50 segundos por imagen) y con precisión del 66% de mAP.
        - **Fast R-CNN:** Mejora la velocidad a 2 segundos por imagen, 66.9% de mAP
        - **Faster R-CNN:** Aún más rápida (0.2 segundos por imagen) con métricas similares, eliminando el método de búsqueda de regiones.
        - **YOLO (You Only Look Once) y SSD (Single Shot Detector):** son Arquitecturas de un solo paso, más rápidas pero con menor exactitud (YOLO) o problemas con objetos pequeños (SSD).
        - **RetinaNet:** Ofrece un buen equilibrio entre precisión y velocidad.
        
    - **Consideraciones:** La resolución de la imagen afecta la precisión y el tiempo de inferencia.
    - **Transfer Learning:** Posibilidad de usar modelos pre-entrenados (Inception, MobileNet, ResNet) y re-entrenarlos para tareas específicas.
    
- **Modelos de Segmentación de Imágenes (Image Segmentation):**
    
    - **Propósito:** Delimitar el área específica de un objeto con una máscara, ofreciendo un nivel de detalle mayor que la detección de objetos.
    - **Aplicaciones:** Medicina (identificación de órganos), análisis detallado de objetos.
    - **Complejidad:** Requiere etiquetar máscaras en las imágenes de entrenamiento, lo que es más complejo que delimitar regiones.
    
- **Modelos de Detección de Puntos Clave (Keypoint Detection):**
    
    - **Propósito:** ==Marcar puntos== específicos en un objeto (ej. articulaciones de una persona, partes de un avión).
    - **Ventaja:** Más sencillo de entrenar que la segmentación de imágenes, ya que solo requiere etiquetar puntos.
    - **Aplicaciones:** Seguimiento de peatones, análisis de posturas (ej. OpenPose para identificar puntos en el cuerpo humano para evaluar ejercicios o bailes).
### **Próximas Clases**

- **Martes Siguiente:** Modelos Deep Auto Encoder, redes recurrentes (LSTM y GRU).
- **Dos Semanas Después:** Modelos LLM (Large Language Models) y modelos de difusión, que son los más actuales y de moda.

### **Conclusiones y Recomendaciones**

- **Elección del Modelo:** La elección del modelo más adecuado depende de la tarea específica y los requisitos de precisión y velocidad.
- **Etiquetado de Datos:** El etiquetado de datos es un trabajo tedioso pero crucial para el entrenamiento de modelos de visión por computadora. Se puede tercerizar o buscar datasets públicos.
- **Experimentación:** Es fundamental experimentar con diferentes arquitecturas y parámetros para encontrar la configuración óptima.