Aquí tienes un resumen detallado de la tercera y última parte de la presentación sobre modelos de Deep Learning, cubriendo la evolución desde redes recurrentes (LSTM y GRU) hacia los Large Language Models (LLM) y, finalmente, los Modelos de Difusión (Diffusion Models):

### **1. Introducción y Repaso: Redes Recurrentes (RNNs), LSTM y GRU**

La presentación comienza retomando el tema de la traducción automática, que fue un punto de partida para la evolución hacia modelos más complejos.

- **Aplicación Inicial: Traducción Automática:** Se retoma el ejemplo de la traducción automática, donde un texto en un idioma se convierte en un texto equivalente en otro idioma (ej., "machine learning is fun" a "aprendizaje automático es divertido"). Para esto, se usaban modelos **Sec-to-Sec (Sequence-to-Sequence)**
    - **Estructura Sec-to-Sec:** Consiste en un _encoder_ (codificador) que procesa la secuencia de entrada y la comprime en un vector de valores numéricos (la "sentencia codificada" o "vector de contexto"), y un _decoder_ (decodificador) que toma este vector para generar la secuencia de salida.
    - **Similitud con Deep Auto Encoders (DAE):** Se destaca que esta arquitectura es muy similar a la de los DAEs, donde el encoder comprime la información en una capa de "features" y el decoder la reconstruye. Se compara con la generación de _deepfakes_ donde un encoder codifica la imagen de una persona y un decoder reconstruye la imagen de otra.
    - **Limitaciones de los Sec-to-Sec Puros:**
        - **Pérdida de Información:** El principal problema era que el vector de contexto (sentencia codificada) tenía que comprimir _toda_ la información de la secuencia de entrada. Para textos largos, esto llevaba a una pérdida significativa de información, haciendo que la decodificación fuera más complicada y propensa a errores.
        - **Ineficiencia en Paralelo:** No se podía aprovechar el procesamiento en paralelo con múltiples GPUs, ya que la decodificación se hacía palabra por palabra y dependía de un único vector. Intentar aumentar el tamaño del vector para capturar más información resultaba contraproducente, empeorando los resultados.
- **El Mecanismo de Atención (Attention Mechanism) como Solución:**
    - **Idea Central:** Para superar las limitaciones de los Sec-to-Sec, se propuso un mecanismo que permitiera al decoder "prestar atención" solo a las partes más relevantes de la entrada al generar cada parte de la salida.
    - **Implementación:** Se introduce una red neuronal auxiliar entre el encoder y el decoder. Esta red de atención determina qué datos del encoder son más útiles para la decodificación en un momento dado.
    - **Metáfora de Búsqueda:** Se explica con la analogía de una búsqueda de base de datos: un "query" (término de búsqueda) busca entre "keys" (claves) para obtener los "values" (valores) más relevantes, ponderados por "pesos de atención".
    - **Funcionamiento con Tokens:** El mecanismo de atención trabaja con representaciones vectoriales (embeddings) de los tokens (palabras o subpalabras), no directamente con las palabras.
    - **Importancia Semántica:** Permite que el modelo asigne mayor peso a los tokens semánticamente más importantes para la tarea actual (ej., para traducir "divertido", considera "fan" y también el sujeto para el género).
    - **Ventaja Clave:** Permite manejar frases y sentencias más largas de manera efectiva, regulando la comunicación entre las capas de codificación y decodificación.
    

### **2. Modelos LLM (Large Language Models) y la Arquitectura Transformer**

La introducción del mecanismo de atención llevó a una revolución en el procesamiento del lenguaje natural.

- **El Paper "Attention Is All You Need":** Google publicó este influyente paper, argumentando que las capas recurrentes (LSTM y GRU) ya no eran necesarias si se utilizaba el mecanismo de atención.
- **Nacimiento del Transformer:** Propusieron una nuevo modelo llamado Transformer, diseñada para "transformar" una entrada en una salida.
    
    - **Componentes Principales:** Consiste en un módulo de _codificación_ y un módulo de _decodificación_, ambos basados exclusivamente en mecanismos de atención y redes neuronales lineales (feed-forward).
    - **Multi-Head Attention:** Una extensión del mecanismo de atención que permite múltiples "cabezas" de atención funcionando en paralelo. Cada cabeza puede aprender a enfocarse en diferentes aspectos o relaciones dentro de los datos, lo que aumenta la flexibilidad y capacidad del modelo para manejar sinónimos y contextos complejos. ==Acá se maneja mejor los sinonimos.==
    - **Add & Norm (Add and Layer Normalization):** Capas que suman la información la entrada original a la salida procesada por una subcapa y luego normalizan el resultado. Esto ayuda a preservar la información original y a estabilizar el entrenamiento.
    - **Positional Encoding:** Dado que los Transformers no tienen recurrencia (no procesan la secuencia en orden), se añade un vector de "codificación posicional" al embedding de cada token para informar al modelo sobre la posición relativa de los tokens en la secuencia.
    - **Masked Multi-Head Attention (en el Decoder):** Una variante de atención en el decoder que "enmascara" las palabras futuras, asegurando que el modelo solo use el contexto de las palabras ya generadas para predecir la siguiente.
    
- **Ventajas del Transformer:**
    
    - **Paralelización Masiva:** Su arquitectura permite un procesamiento altamente paralelo, lo que acelera drásticamente el entrenamiento y la inferencia, especialmente con múltiples GPUs.
    - **Base de LLM Modernos:** El modelo Transformer es el "antecesor común" de todos los LLM actuales como ChatGPT, Gemini, LLaMA, etc.
    
- **Desafíos de los LLM:**
    
    - **Altos Requisitos:** Demandan enormes cantidades de hardware, tiempo y dinero para su entrenamiento (ej., GPT-4: 191 millones).
    - **Datos Masivos:** Necesitan volúmenes gigantescos de datos (ej., GPT-3: 45 TB de texto).
    - **Investigación Activa:** Hay un campo de investigación muy activo para reducir estos requisitos (ej., el trabajo de Karpathy, el caso controversial de DeepSeek).
    https://youtu.be/MT4Pmzutrns?list=PLfQtPEPnkUVnm3CNtV6f02__b5-SrQOaZ&t=3509
    https://youtu.be/MT4Pmzutrns?list=PLfQtPEPnkUVnm3CNtV6f02__b5-SrQOaZ&t=3549
- **Estrategias de Implementación y Uso:**
    
    - **Modelos Pequeños (Mini-GPT):** Es posible implementar versiones más pequeñas de Transformers para tareas específicas, aunque pueden no aprender todo.
    - **IA como Servicio (APIs):** Empresas como OpenAI ofrecen acceso a sus modelos entrenados a través de APIs, eliminando la necesidad de hardware propio.
    - **Fine-tuning (Ajuste Fino):** Utilizar modelos pre-entrenados ("Foundation Models") y ajustarlos con datos específicos para una tarea o dominio particular (ej., un chatbot especializado en productos de una empresa). Esto puede implicar entrenar solo las últimas capas o todo el modelo con tasas de aprendizaje diferenciadas.
    - **Hugging Face:** Un repositorio popular que ofrece una vasta colección de modelos pre-entrenados para diversas tareas de PNL (clasificación, traducción, resumen, generación de código, etc.), facilitando su uso y ajuste.
    

**Ejemplos de Aplicaciones de LLM (mostrados en la transcripción):**

- **Procesamiento de Texto:** Respuesta a preguntas, traducción multilingüe, resumen, generación de código (SQL, Python), clasificación de texto (incluyendo _zero-shot classification_), generación de audio a partir de texto.
- **Aplicaciones Innovadoras:**
    
    - **Undermine:** Un LLM para búsqueda y procesamiento de información académica.
    - **Illuminate:** Una aplicación de Google que genera podcasts de discusión sobre papers científicos.
    - **LLM como Font:** Un tipo de letra que ejecuta un LLM para autocompletar texto.
    - **LLM como Backend:** Usar un LLM para gestionar la lógica de negocio de una aplicación sin código tradicional.
    - **Descompilación de Código:** Transformar código de bajo nivel (Assembler) a lenguajes de alto nivel (C).
    - **Vision Transformer:** Uso de Transformers para tareas de visión por computadora como detección de objetos, ofreciendo una alternativa a las CNNs.
    - **Modelos Multimodales:** Modelos que combinan texto e imagen (ej., dar una imagen y hacer preguntas sobre ella).
    

### **3. Modelos de Difusión (Diffusion Models)**

Estos modelos son la base de la generación de imágenes y otros datos complejos.

- **Concepto Central:** A diferencia de "dibujar", los modelos de difusión aprenden a _eliminar ruido_ de una imagen.
- **Dos Procesos Fundamentales:**
    
    - **1. Proceso de Difusión Hacia Adelante (Forward Diffusion Process):**
        
        - **Propósito:** Preparar los datos de entrenamiento.
        - **Mecanismo:** Se añade ruido gaussiano de forma progresiva y controlada a una imagen original (X0) a lo largo de múltiples pasos de tiempo (T), hasta que la imagen se convierte en puro ruido aleatorio (XT).
        - **Control Matemático:** El ruido se añade siguiendo una función matemática específica, lo que permite calcular la imagen con ruido en cualquier paso 't' directamente, sin necesidad de iterar desde el principio.
        
    - **2. Proceso Inverso (Reverse Noise Mode Process):**
        
        - **Propósito:** Generar una imagen limpia a partir del ruido.
        - **Mecanismo:** Una red neuronal (generalmente una **U-Net**) se entrena para _predecir el ruido_ presente en una imagen ruidosa.
        - **Reconstrucción:** Una vez que el modelo predice el ruido, este ruido se _resta_ de la imagen de entrada. Este proceso de predicción y resta se itera muchas veces, comenzando desde una imagen de ruido puro, hasta que se obtiene una imagen limpia y coherente.
        - **Entrenamiento:** La U-Net se entrena de forma supervisada, conociendo el ruido real que se añadió en el proceso forward.
        
    
- **Modelos de Difusión Latentes (Latent Diffusion Models):**
    
    - **Optimización:** Para manejar imágenes de alta resolución de manera eficiente.
    - **Mecanismo:** Se utiliza un **Deep Auto Encoder** para comprimir la imagen original en una representación de "datos latentes" (features). El modelo de difusión opera _únicamente_ sobre estos datos latentes de menor dimensión.
    - **Ventajas:** Reducción significativa del tiempo de entrenamiento y generación, mayor expresividad para trabajar con diversos tipos de datos (no solo píxeles). Al final, el decoder del DAE convierte los datos latentes generados de nuevo en una imagen.
    
- **Adición de Condiciones (Conditional Diffusion Models):**
    
    - **Control Creativo:** Permite guiar la generación de imágenes con entradas adicionales.
    - **Mecanismo:** Se añade una entrada adicional a la U-Net, que es una codificación (embedding) de la condición deseada (ej., un texto descriptivo, una imagen de referencia, un mapa semántico).
    - **Combinación de Condiciones:** Múltiples condiciones (ej., texto e imagen) pueden combinarse (ej., mediante multiplicación de sus vectores de embedding) para influir en la generación.
    - **Entrenamiento:** Requiere datos de entrenamiento que emparejen imágenes con sus condiciones correspondientes.
    

**Ejemplos de Aplicaciones de Modelos de Difusión (mostrados en la transcripción):**

- **Text-to-Image:** Generación de imágenes a partir de descripciones textuales (ej., DALL-E).
- **Image-to-Image:**
    
    - Generación de variaciones de una imagen.
    - Transformación de estilos o elementos dentro de una imagen (ej., añadir tentáculos a un pato, cambiar cuernos de un ciervo, transformar una manzana en un kiwi).
    - Edición y mejora de imágenes (ej., panorámicas, mejora de calidad).
    
- **Generación de Video:** Crear videos a partir de texto o transformar videos existentes.

**Consideraciones Finales:**

- La combinación de modelos (ej., LLM para codificar texto y Modelos de Difusión para generar imágenes) es una tendencia clave en la IA multimodal.
- La calidad de los resultados de los modelos de difusión puede degradarse si se encadenan múltiples modelos o si las entradas son de baja calidad.
- El funcionamiento de los modelos de difusión, aunque contraintuitivo, ha demostrado ser extremadamente efectivo.


---

Aquí tienes un resumen detallado de la tercera y última parte de la presentación sobre modelos de Deep Learning, centrándose en los **Large Language Models (LLM)** y los **Modelos de Difusión (Diffusion Models)**:

### **1. Modelos LLM (Large Language Models)**

**Características Generales:**

- **Requisitos de Hardware:** Son modelos que demandan mucho hardware, memoria y poder de procesamiento tanto para su entrenamiento como para su funcionamiento.
- **Resultados:** Generan resultados muy buenos a pesar de sus altos requisitos.
- **Aprendizaje Híbrido:** Combinan entrenamiento supervisado con pre-entrenamiento y, a menudo, aprendizaje por refuerzo (Reinforcement Learning) para que el modelo aprenda por sí mismo a partir de la evaluación de resultados.

**Evolución desde Modelos Sec-to-Sec (Sequence-to-Sequence):** Seq2Seq

- **Aplicación Inicial:** La traducción automática (ej., "machine learning is fun" a "aprendizaje automático es divertido").
- **Modelos Sec-to-Sec (Encoder-Decoder):**
    
    - **Funcionamiento:** Un _encoder_ procesa la secuencia de entrada y la comprime en un vector numérico (sentencia codificada o "features"). Un _decoder_ toma este vector y genera la secuencia de salida.
    - **Limitaciones:** Fallaban con textos muy largos porque el vector intermedio no podía comprimir toda la información sin perderla. Además, no permitían el procesamiento paralelo con múltiples GPUs.
    
- **Introducción del Mecanismo de Atención (Attention Mechanism):**
    
    - **Problema Resuelto:** Supera la limitación del vector único en los modelos Sec-to-Sec.
    - **Funcionamiento:** En lugar de un único vector, una red neuronal auxiliar (capa de atención) conecta el encoder y el decoder. Esta red determina qué partes de la entrada son más relevantes para cada parte de la salida, suministrando solo la información más útil al decoder.
    - **Metáfora:** Se asemeja a una búsqueda de "claves" (keys) y "valores" (values) para un "término de búsqueda" (query), donde los "pesos de atención" indican la importancia.
    - **Ejemplo:** Para traducir "fun" (divertido), el modelo no solo considera "fun" sino también "machine learning" para determinar el género ("divertido" vs. "divertida").
    - **Representación:** Trabaja con representaciones vectoriales de tokens (embeddings), no directamente con las palabras.
    - **Ventaja:** Permite que el modelo se enfoque en las partes más relevantes de la entrada, mejorando la traducción de frases largas y la comprensión semántica.
    

**Modelos Transformer:**

- **Origen:** Google publicó el paper "Attention Is All You Need" (2017), proponiendo que solo el mecanismo de atención era necesario, eliminando las capas recurrentes (LSTM/GRU).
- **Arquitectura:**
    
    - **Encoder y Decoder:** Módulos que utilizan exclusivamente mecanismos de atención y redes neuronales lineales (feed-forward).
    - **Multi-Head Attention:** Extiende el mecanismo de atención, permitiendo múltiples "cabezas" de atención que procesan la información en paralelo, capturando diferentes aspectos de la relación entre tokens (ej., sinónimos).
    - **Add & Norm (Add and Layer Normalization):** Capas que suman la entrada original a la salida procesada y normalizan el resultado, mejorando el rendimiento y la estabilidad del entrenamiento.
    - **Positional Encoding:** Un vector que se añade al embedding de cada token para indicar su posición en la secuencia, ya que los Transformers no tienen recurrencia y no procesan la secuencia de forma ordenada.
    - **Masked Multi-Head Attention (en el Decoder):** Una versión especial de atención que "enmascara" las salidas futuras para que el modelo solo aprenda a predecir el siguiente token basándose en los tokens ya generados.
    
- **Ventajas:**
    
    - **Paralelización:** Mucho más fáciles de entrenar con múltiples GPUs, acelerando enormemente el proceso.
    - **Rendimiento:** Superan a los modelos recurrentes en muchas tareas de procesamiento de lenguaje.
    
- **Modelos LLM Actuales:** Todos los modelos modernos (ChatGPT, Gemini, LLaMA) se basan en la arquitectura Transformer, aunque con variaciones y mejoras.
- **Costo y Datos:**
    
    - **Entrenamiento:** Requieren enormes cantidades de tiempo, hardware y dinero (ej., GPT-4: 191M).
    - **Datos:** Necesitan volúmenes masivos de datos (ej., GPT-3: 45 TB de texto).
    - **Optimización:** Hay mucha investigación para reducir los requisitos de procesamiento y tiempo de entrenamiento (ej., el trabajo de Karpathy, el controversial DeepSeek).
    
- **Estrategias de Uso:**
    
    - **APIs:** Utilizar modelos pre-entrenados a través de APIs (IA como servicio).
    - **Fine-tuning (Ajuste Fino):** Tomar un modelo pre-entrenado (Foundation Model) y entrenarlo con un conjunto de datos más pequeño y específico para una tarea particular (ej., chatbot de atención al cliente). Esto puede implicar entrenar solo las últimas capas o todo el modelo con un algoritmo de actualización de pesos modificado.
    - **Repositorios:** Plataformas como Hugging Face ofrecen una gran variedad de modelos pre-entrenados para diversas tareas (clasificación de texto, traducción, resumen, generación de código, etc.).
    

**Ejemplos de Aplicaciones de LLM (mostrados en la transcripción):**

- **Text-to-Text:**
    
    - Respuesta a preguntas (ej., "Whisper" de OpenAI para transcripción de audio a texto en múltiples idiomas).
    - Traducción (multilingüe).
    - Resumen de texto.
    - Generación de código (ej., SQL, Python).
    - Clasificación de texto (incluyendo "zero-shot classification" donde las etiquetas se definen en tiempo de ejecución).
    - Generación de audio a partir de texto.
    
- **Aplicaciones Innovadoras:**
    
    - **Undermine:** LLM para información académica.
    - **Illuminate:** Genera podcasts de discusión sobre papers científicos.
    - **LLM como Font:** Un tipo de letra que ejecuta un LLM para autocompletar texto.
    - **LLM como Backend:** Usar un LLM para gestionar la lógica de negocio de una aplicación (ej., gestión de stock).
    - **Descompilación de Código:** Transformar código Assembler a C.
    

### **2. Modelos de Difusión (Diffusion Models)**

**Concepto Fundamental:**

- **Generación de Imágenes:** Crean imágenes realistas a partir de ruido aleatorio.
- **Funcionamiento (Contraintuitivo):** No "dibujan" píxel por píxel, sino que aprenden a _eliminar ruido_ de una imagen.

**Dos Procesos Clave:**

- **1. Proceso de Difusión Hacia Adelante (Forward Diffusion Process):**
    
    - **Objetivo:** Preparar los datos de entrenamiento.
    - **Funcionamiento:** A una imagen original (X0) se le añade ruido progresivamente en múltiples pasos (T) hasta que la imagen se convierte en puro ruido aleatorio (XT).
    - **Ruido Controlado:** El ruido se añade de forma matemática (distribución gaussiana) para que sea predecible.
    - **Fórmula Simplificada:** Existen fórmulas que permiten calcular directamente la imagen con ruido en cualquier paso 't' sin tener que pasar por todos los pasos intermedios.
    
- **2. Proceso Inverso (Reverse Noise Mode Process):**
    
    - **Objetivo:** Aprender a reconstruir la imagen original a partir del ruido.
    - **Funcionamiento:** El modelo (una red neuronal) toma una imagen con ruido y predice _dónde está el ruido_ en esa imagen.
    - **Red Predictora de Ruido (U-Net):** La red neuronal utilizada para esta predicción suele ser una U-Net (una arquitectura basada en convoluciones y atención).
    - **Reconstrucción:** Una vez que el modelo predice el ruido, ese ruido se _resta_ de la imagen de entrada para obtener una versión con menos ruido. Este proceso se itera muchas veces hasta obtener la imagen limpia.
    
- **Entrenamiento:**
    
    - **Supervisado:** Se entrena la U-Net dándole imágenes con ruido conocido (generado por el proceso forward) y el ruido real como objetivo.
    - **Objetivo:** La red aprende a predecir el ruido con bajo error.
    
- **Producción (Generación):**
    
    - Se inicia con una imagen de ruido total (totalmente aleatoria).
    - Se itera el proceso inverso: la U-Net predice el ruido, se resta de la imagen, y la nueva imagen (con menos ruido) se usa para la siguiente iteración.
    - Se repite hasta que se alcanza un número predefinido de ciclos o la imagen es lo suficientemente clara.
    

**Modelos de Difusión Latentes (Latent Diffusion Models):**

- **Optimización:** Para reducir el tiempo de entrenamiento y operación en imágenes de alta resolución.
- **Funcionamiento:**
    
    - Se entrena un **Deep Auto Encoder** para comprimir las imágenes originales en una representación de "datos latentes" (features).
    - El **Modelo de Difusión** trabaja _únicamente_ con estos datos latentes comprimidos, no con los píxeles originales. Esto reduce drásticamente la cantidad de información a procesar.
    - Al final, los datos latentes generados por el modelo de difusión se pasan por el _decoder_ del Deep Auto Encoder para reconstruir la imagen de alta resolución.
    
- **Ventajas:** Eliminación de ruido más sencilla, generación más rápida, y mayor expresividad para manejar diversos tipos de datos (no solo imágenes).

**Adición de Condiciones (Conditional Diffusion Models):**

- **Control de Generación:** Permite guiar la generación de imágenes con entradas adicionales (ej., texto, otra imagen).
- **Funcionamiento:** Se añade una entrada adicional a la U-Net (la red predictora de ruido). Esta entrada es una codificación (embedding) de la condición (ej., el texto "un gato sentado en una mesa").
- **Codificación de Condiciones:**
    
    - **Texto:** Un LLM (o un encoder de texto) procesa el texto de la condición y lo convierte en un vector.
    - **Imágenes:** Un encoder de imagen procesa la imagen de referencia y la convierte en un vector.
    - **Combinación:** Múltiples condiciones (texto e imagen) pueden combinarse (ej., multiplicando sus vectores de embedding) para influir en la generación.
    
- **Entrenamiento:** Requiere ejemplos de imágenes emparejadas con sus condiciones (ej., imagen de gato + texto "gato").

**Ejemplos de Aplicaciones de Modelos de Difusión (mostrados en la transcripción):**

- **Text-to-Image:** Generar imágenes a partir de descripciones de texto (ej., DALL-E, Stable Diffusion).
- **Image-to-Image:**
    
    - Generar variaciones de una imagen existente.
    - Transformar objetos o estilos (ej., pato con tentáculos, casa victoriana a moderna).
    - Edición de imágenes (ej., cambiar elementos, mejorar calidad, añadir efectos).
    
- **Image Inpainting/Outpainting:** Rellenar partes faltantes de una imagen o extenderla más allá de sus límites originales, creando contenido nuevo que se integra con el contexto.
- **Generación de Video:** Crear videos a partir de texto o transformar videos existentes.

**Consideraciones Finales:**

- Los modelos de difusión son computacionalmente intensivos, especialmente en la fase de generación (iteraciones).
- La calidad de los resultados puede variar mucho entre modelos y con la complejidad de las indicaciones.
- La combinación de LLMs y modelos de difusión (como en los modelos condicionales) es una tendencia clave para la generación multimodal.

---
### **Preguntas y Respuestas para el Examen**

#### **Tema 1: Modelos Sec-to-Sec y Mecanismo de Atención**

**Pregunta 1:** **Contexto:** "Estos traductores solían funcionar bien con estos modelos, sobre todo para frases cortas. Pero cuando se quería hacer una traducción de un texto muy largo, eh estos modelos solían fallar. El problema, ah, bueno, me olvidé de aclarar acá, estos modelos se lo suelen llamar sec to sec porque se decía que trabajaban con secuencias de entrada y con esa entrada procesada generaban una secuencia de de salida." **Pregunta:** Explica las limitaciones principales de los modelos "Sec-to-Sec" puros (Encoder-Decoder) para la traducción de textos largos y cómo el mecanismo de atención aborda estas limitaciones.

**Respuesta:**

- **Limitaciones de los Modelos Sec-to-Sec Puros:**
    
    - **Pérdida de Información:** El problema principal radicaba en la "sentencia codificada" (el vector de valores numéricos) que conectaba el _encoder_ con el _decoder_. Este vector debía comprimir _toda_ la información del texto de entrada. Para textos largos, esto resultaba en una pérdida significativa de información, haciendo que la decodificación fuera más complicada y propensa a errores. Intentar ampliar el tamaño de este vector para representar sentencias más largas no solo impactaba negativamente el rendimiento, sino que también empeoraba los resultados, ya que el modelo se volvía "perezoso" y la codificación no era tan buena.
    - **Falta de Paralelización:** Técnicamente, al tener la información codificada en un solo vector y requerir la decodificación palabra por palabra, no se podía aprovechar el procesamiento en paralelo con múltiples GPUs, lo que ralentizaba el proceso.
    
- **Cómo el Mecanismo de Atención Aborda estas Limitaciones:**
    
    - **Suministro de Información Relevante:** En lugar de depender de un único vector comprimido, el mecanismo de atención (implementado a través de una red neuronal auxiliar) suministra a la capa de decodificación _solo la información más útil_ de la capa de codificación para realizar la traducción de cada término.
    - **Enfoque Dinámico:** El modelo de decodificación recibe indicaciones, a través de una representación en vectores, sobre a qué datos debe prestar más atención para cada término a traducir. Esto permite que la red neuronal auxiliar se adapte a la posición que el decodificador necesita traducir, facilitando su trabajo.
    - **Mejora en Textos Largos:** Al no tener que comprimir toda la información en un solo vector, se evita la pérdida de información, permitiendo un manejo más efectivo de frases y sentencias largas.
    - **Paralelización (en Transformers):** Aunque no se detalla explícitamente en este punto, la introducción del mecanismo de atención en los Transformers (que se explica más adelante) es clave para permitir el procesamiento paralelo.
    

---

**Pregunta 2:** **Contexto:** "Eh, esto eh lo que yo leí de de atención es que no sé si es correcto, eh si me podés corregir, pero por ejemplo eh esta capita es eh la red neuronal entre el encoder y el decoder, el mecanismo de atención lo que hace que, por ejemplo, en una frase no todas las palabras tienen el mismo peso. semánticamente hay palabras que le le dan el significado semántico a una frase y eso es el lo que el valor que le agrega la capa de atención. Eso es lo que yo había leído. Claro. Sí. Es eso que yo le decía que determina a cuál le tiene que dar más importancia." **Pregunta:** Explica la función principal del mecanismo de atención en el contexto de la traducción de texto, utilizando el ejemplo de la traducción de "fun" (divertido) y cómo maneja las dependencias semánticas.

**Respuesta:**

- **Función Principal:** El mecanismo de atención permite que el modelo de decodificación determine a qué partes de la secuencia de entrada debe "prestar más atención" (dar más importancia o peso) al generar cada parte de la secuencia de salida. Esto significa que no todas las palabras de la frase de entrada tienen el mismo peso semántico para la traducción de una palabra específica.
- **Manejo de Dependencias Semánticas (Ejemplo "divertido"):**
    
    - Para traducir el término "fun" (divertido), el modelo no solo considera la palabra "fun" en sí misma.
    - También toma en cuenta el contexto proporcionado por otras palabras de la frase, como "machine learning".
    - Esto es crucial para determinar la conjugación o el género adecuado del adjetivo en español ("divertido" si el sujeto es masculino como "aprendizaje automático", o "divertida" si fuera femenino).
    - Los "pesos de atención" reflejan esta importancia: la palabra "fun" tendrá el mayor peso (ej., 0.8), pero "machine" y "learning" también tendrán un peso menor pero significativo (ej., 0.1 cada una), influyendo en la elección final de la palabra traducida.
    - De manera similar, para traducir "is" (es/está), el modelo necesita considerar el sujeto y el predicado para elegir la conjugación correcta del verbo "ser" o "estar".
    
- **Control Automático:** El modelo aprende a controlar estas dependencias de forma automática, basándose en ejemplos de frases de entrada y salida, sin necesidad de información explícita sobre reglas gramaticales.

---

**Pregunta 3:** **Contexto:** "Profe, eh, y esto, por ejemplo, se me ocurre decirme si capaz no es por acá, pero se podría tener de salida no una traducción con la misma cantidad de token, sino eh, no sé, le mando un texto de entrada y el mecanismo de atención eh lo que quiero es que me determine si este texto fue escrito por una persona, no sé, con esquizofrenia, por ejemplo, con lo que sea, se puede extrapolar más información a partir de un texto y a la salida me da un sí o un No, por ejemplo, o que me diagnostica cosas o Sí, sí. Lo que en ese caso por este lado en ese caso la en vez de tener un decoder, lo que vas a tener es otra capa lineal para para ir lo que estarías haciendo es como una una especie de clasificación eh para decir sí o no si la persona tiene tal enfermedad o cuál es la enfermedad que tiene la persona. Se podría hacer." **Pregunta:** ¿Es posible utilizar la arquitectura de un modelo con mecanismo de atención para tareas diferentes a la traducción, como la clasificación o la respuesta a preguntas? Explica cómo se adaptaría la arquitectura para estas tareas.

**Respuesta:**

- **Sí, es posible.** La arquitectura de un modelo con mecanismo de atención (como la base de los Transformers) es muy versátil y puede adaptarse para diversas tareas más allá de la traducción.
- **Adaptación para Clasificación:**
    
    - En lugar de tener un _decoder_ que genera texto, se reemplazaría la capa de decodificación por una o más **capas lineales (densas)** al final del modelo.
    - Estas capas lineales se encargarían de realizar una **clasificación**. Por ejemplo, si se quiere determinar si un texto fue escrito por una persona con una condición específica, la salida sería un ID de clase (un número o un "sí/no") en lugar de una secuencia de texto.
    - Esto es más sencillo que generar texto, ya que el objetivo es producir una etiqueta o un valor numérico.
    
- **Adaptación para Chatbots/Respuesta a Preguntas:**
    
    - La misma arquitectura (encoder + attention + decoder) puede usarse para desarrollar un chatbot o un sistema de respuesta a preguntas.
    - El modelo recibiría un texto de entrada que contiene un contexto y una pregunta.
    - El _decoder_ generaría la respuesta a esa pregunta.
    - El modelo aprendería que, para un texto de entrada con una pregunta, la salida esperada es una respuesta coherente. El modelo no "sabe" que está traduciendo o respondiendo, solo aprende a generar una secuencia de palabras que se corresponde con la entrada dada.
    

---

#### **Tema 2: Modelos Transformer**

**Pregunta 4:** **Contexto:** "La gente de Google se dio cuenta que al agregarle esta capa de atención, donde lo que hacemos es le damos la posibilidad al modelo de prestar atención a ciertos términos al momento de hacer la traducción, eh se dieron cuenta que no valía la pena tener las capas LCTM ni las capas GRU en este modelo y con el modelo de atención alcanzable. Entonces ellos publicaron este paper que le pusieron el nombre, el attention is all you need. Atención es todo lo que necesitas." **Pregunta:** ¿Cuál fue la principal innovación de los modelos Transformer propuesta en el paper "Attention Is All You Need" y qué ventaja clave ofrecieron respecto a las arquitecturas recurrentes (LSTM/GRU) anteriores?

**Respuesta:**

- **Principal Innovación:** La principal innovación de los modelos Transformer fue la propuesta de que **solo el mecanismo de atención era necesario** para el procesamiento de secuencias, eliminando la necesidad de las capas recurrentes (LSTM y GRU) que eran la base de los modelos Sec-to-Sec anteriores. De ahí el título del paper: "Attention Is All You Need".
- **Ventaja Clave:** La ventaja más significativa que ofrecieron los Transformers fue su capacidad para **procesar la información de forma altamente paralela**. A diferencia de las redes recurrentes que procesan las secuencias de forma secuencial (palabra por palabra), la arquitectura basada en atención de los Transformers permite que diferentes partes de la secuencia se procesen simultáneamente. Esto se traduce en una **aceleración drástica del entrenamiento**, especialmente con múltiples GPUs, lo que era una limitación importante en los modelos recurrentes.

---

**Pregunta 5:** **Contexto:** "Fíjense arrancando ya con mirando las cajitas que hay unas cajitas marrones que se llaman multiad attention. Multiad attention lo que hace es extender la idea del mecanismo de self attention o mecanismo de de atención que nosotros veníamos hablando, donde yo voy a tener muchos eh muchos de esos mecanismos funcionando en paralelos." **Pregunta:** Describe el concepto de "Multi-Head Attention" en la arquitectura Transformer y explica cómo contribuye a la flexibilidad y capacidad del modelo.

**Respuesta:**

- **Concepto de Multi-Head Attention:** El "Multi-Head Attention" (Atención Multi-Cabeza) es una extensión del mecanismo de auto-atención (self-attention). Consiste en tener **múltiples mecanismos de atención funcionando en paralelo** dentro de la misma capa. Cada uno de estos mecanismos paralelos se denomina una "cabeza de atención".
- **Contribución a la Flexibilidad y Capacidad:**
    
    - **Captura de Diversas Relaciones:** Al tener varias cabezas de atención, el modelo puede aprender a enfocarse en diferentes tipos de relaciones o aspectos de la información de entrada simultáneamente. Por ejemplo, una cabeza podría enfocarse en relaciones sintácticas, mientras que otra se enfoca en relaciones semánticas o en sinónimos.
    - **Mayor Flexibilidad:** Permite que el modelo represente la información de distintas maneras. Como se mencionó en el ejemplo de los sinónimos, una cabeza podría dar mayor peso a una palabra para generar un sinónimo específico ("divertido"), mientras que otra cabeza podría enfocarse en otro sinónimo ("bullicioso").
    - **Resultados Consolidados:** Los resultados de todas estas cabezas de atención se concatenan y se procesan mediante una capa densa para generar un resultado más consolidado y rico en información.
    - **Parámetro de Diseño:** La cantidad de cabezas es un parámetro que se define al construir el modelo, permitiendo ajustar su capacidad de atención y, consecuentemente, sus requisitos de procesamiento.
    

---

**Pregunta 6:** **Contexto:** "Estos todos estos modelos están basados en el modelo Transformer con alguna diferencia, con alguna mejora. En los modelos más viejos aparecía la letra T de Transformer. En GTP la T también es de Transformer, pero los modelos los últimos ya ya no le ponen la T. De hecho, Google ahora la arquitectura la llama Lambda porque cambió un poco la forma de trabajo y sobre Lambda hizo después Géminis, eh Meta hizo Meta que también es distinto." **Pregunta:** ¿Cuál es la relación entre los modelos LLM actuales (como ChatGPT, Gemini, LLaMA) y la arquitectura Transformer? ¿Han evolucionado o se mantienen idénticos al Transformer original?

**Respuesta:**

- **Relación con Transformer:** Todos los modelos LLM actuales (como ChatGPT, Gemini, LLaMA) tienen una **relación directa y están basados de alguna manera en la arquitectura Transformer**. El Transformer es el "antecesor común" o la base fundamental sobre la cual se construyen estos modelos.
- **Evolución y Mejoras:** No se mantienen idénticos al Transformer original. Han **evolucionado** significativamente. Aunque todos siguen utilizando la idea central del mecanismo de atención, las implementaciones han incorporado:
    
    - **Diferencias y Mejoras:** Se han introducido variaciones y mejoras en la forma en que se conectan las capas, en los algoritmos de entrenamiento, y en la optimización de la arquitectura.
    - **Nuevos Nombres:** Las compañías a menudo les dan nombres propios a sus arquitecturas evolucionadas (ej., Google con Lambda y Gemini, Meta con LLaMA), incluso si la "T" de Transformer ya no está explícitamente en el acrónimo.
    - **Tamaño y Rendimiento:** Los modelos actuales son mucho más grandes en términos de billones de parámetros, lo que requiere más procesamiento pero también genera mejores resultados.
    

---

#### **Tema 3: Modelos de Difusión**

**Pregunta 7:** **Contexto:** "Yo voy a ser sincero, cuando me enteré de estos modelos, pensé que era un modelo que aprendía dibujar. Dije, bueno, le enseñaron a pintar al modelo como si fuera un pintor. Y de esa manera el modelo iba pintando píxel por píxel para generar eh la imagen que que correspondía. En la realidad no hace eso. La eh el modelo diffusion va a estar basado más en tratar de corregir el error que va a tener en una imagen de entrada y eso lo va a realizar tantas veces hasta que genere una imagen con buena calidad." **Pregunta:** Contrario a la intuición, ¿cómo funciona un modelo de difusión para generar una imagen a partir de ruido? Describe los dos procesos principales involucrados.

**Respuesta:**

- **Funcionamiento Contraintuitivo:** Un modelo de difusión no "aprende a dibujar" o a pintar píxel por píxel como un pintor. En cambio, su funcionamiento se basa en **aprender a eliminar o predecir el ruido** de una imagen.
- **Dos Procesos Principales:**
    
    1. **Proceso de Difusión Hacia Adelante (Forward Diffusion Process):**
        
        - **Propósito:** Preparar los datos de entrenamiento.
        - **Mecanismo:** A una imagen original (X0) se le añade ruido progresivamente en múltiples pasos de tiempo (T). Este ruido se añade de forma controlada y matemática (usando una distribución gaussiana) hasta que la imagen se convierte en puro ruido aleatorio (XT), donde ya no se distingue el objeto original.
        - **Control:** Existen fórmulas que permiten calcular directamente la imagen con ruido en cualquier paso 't' sin tener que pasar por todos los pasos intermedios, lo que simplifica el proceso de preparación de datos.
        
    2. **Proceso Inverso (Reverse Noise Mode Process):**
        
        - **Propósito:** Generar una imagen limpia a partir del ruido.
        - **Mecanismo:** Una red neuronal (comúnmente una U-Net) se entrena para **predecir dónde está el ruido** en una imagen ruidosa que se le da como entrada.
        - **Reconstrucción:** Una vez que el modelo predice el ruido, este ruido se _resta_ de la imagen de entrada. Este proceso de predicción y resta se itera muchas veces, comenzando desde una imagen de ruido total (aleatoria), hasta que se obtiene una imagen sin ruido y con buena calidad, que representa el objeto deseado.
        - **Entrenamiento:** La red predictora de ruido se entrena de forma supervisada, ya que durante el entrenamiento se conoce el ruido real que se añadió en el proceso forward.
        
    

---

**Pregunta 8:** **Contexto:** "Una cosa que se dieron cuenta cuando empezaron a implementar estos modelos de fusion para imágenes eh más grandes, es que el tiempo de entrenamiento y el tiempo de operación demoraba mucho por eh por la cantidad de píxeles que tenía que generar el modelo de difusón. Entonces, eh los investigadores dijeron, 'Bueno, ¿cómo podemos hacer para reducir la cantidad de de de información que tiene que procesar el modelo Difusion?'" **Pregunta:** Explica el concepto de "Modelos de Difusión Latentes" y cómo resuelven el problema del alto costo computacional al generar imágenes de alta resolución.

**Respuesta:**

- **Problema a Resolver:** Los modelos de difusión puros eran muy costosos computacionalmente (en tiempo de entrenamiento y operación) al trabajar directamente con imágenes de alta resolución debido a la gran cantidad de píxeles a procesar.
- **Concepto de Modelos de Difusión Latentes:** Para abordar esto, se introdujo el uso de un **Deep Auto Encoder (DAE)** en la arquitectura.
    
    - **Compresión de Datos:** Primero, se entrena un DAE para comprimir las imágenes originales en una representación de menor dimensión llamada "datos latentes" (o "latent data"). Esta capa de features del DAE captura la información principal de la imagen de forma compacta.
    - **Operación en Espacio Latente:** El modelo de difusión (la red U-Net que predice el ruido) ya no trabaja con los píxeles de la imagen original, sino que opera _directamente sobre estos datos latentes_. Esto significa que, en lugar de procesar una matriz de 1000x1000 píxeles, el modelo de difusión podría trabajar con una matriz mucho más pequeña, como 10x10.
    - **Reconstrucción Final:** Una vez que el modelo de difusión ha generado los datos latentes "limpios" (sin ruido), estos se pasan a través del _decoder_ del DAE para reconstruir la imagen final de alta resolución.
    
- **Ventajas:**
    
    - **Reducción Computacional:** Al trabajar en un espacio latente de menor dimensión, se reduce drásticamente la cantidad de información que el modelo de difusión tiene que procesar, lo que acelera significativamente el tiempo de entrenamiento y la generación de imágenes.
    - **Mayor Expresividad:** Permite que el modelo de difusión sea más versátil y pueda trabajar con cualquier tipo de datos (texto, 3D, etc.) siempre que puedan ser codificados en un espacio latente por un DAE.
    

---

**Pregunta 9:** **Contexto:** "Ustedes saben que yo con estos modelos de difusión puedo ponerle un texto diciéndole, por ejemplo, quiero una foto de un gato o quiero la foto de un gato sentado arriba de la mesa. Bueno, ¿cómo hago para entrenar un modelo que haga eso? Porque los modelos que vimos hasta ahora eh no le pusimos ninguna condición." **Pregunta:** Explica cómo se añaden "condiciones" (como texto o imágenes de referencia) a un modelo de difusión para guiar la generación de imágenes, y cómo se combinan múltiples tipos de condiciones.

**Respuesta:**

- **Mecanismo de Adición de Condiciones:** Para añadir condiciones a un modelo de difusión, se incorpora una **entrada adicional** a la red predictora de ruido (la U-Net). Esta entrada es una **codificación (embedding)** de la condición deseada.
- **Tipos de Condiciones y su Procesamiento:**
    
    - **Texto:** Si la condición es un texto (ej., "un gato sentado arriba de la mesa"), este texto es preprocesado por otro modelo (ej., un LLM o un encoder de texto) que lo convierte en un vector numérico (embedding). Este vector se alimenta a la U-Net.
    - **Imágenes de Referencia:** Si la condición es una imagen, se utiliza un encoder de imagen para convertirla en un vector numérico (embedding). Este vector también se alimenta a la U-Net.
    - **Otros Datos:** Se podría usar cualquier tipo de información (mapas semánticos, datos 3D) siempre que puedan ser codificados en un vector.
    
- **Combinación de Múltiples Condiciones:** Cuando se quieren combinar varias condiciones (ej., una imagen de referencia y un texto), los embeddings de cada condición se combinan (ej., mediante una **multiplicación de vectores**). El resultado de esta combinación (una matriz) es lo que se le pasa a la U-Net para que tenga en cuenta todas las condiciones al predecir el ruido.
- **Entrenamiento:** Para que el modelo aprenda a usar estas condiciones, durante el entrenamiento se le deben proporcionar ejemplos de imágenes junto con las condiciones correspondientes (ej., una imagen de un gato con el texto "gato"). Es importante que las condiciones textuales tengan variaciones para que el modelo aprenda a interpretarlas correctamente.