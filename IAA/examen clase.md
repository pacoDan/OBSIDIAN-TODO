**Preguntas y Respuestas de la Transcripción sobre Inteligencia Artificial Avanzada y Redes Neuronales**


1. **¿Por qué una red neuronal convolucional (CNN) es eficiente para el análisis de imágenes?**
    - **Respuesta:** Las CNN son eficientes porque utilizan filtros (kernels) que permiten detectar características locales en las imágenes, comparten pesos para reducir la cantidad de parámetros y son capaces de capturar patrones jerárquicos, facilitando el reconocimiento de objetos.
2. **¿Cuáles son las diferencias y similitudes entre redes neuronales artificiales y redes bayesianas?**
    
    - **Respuesta:**
        
        - **Diferencias:** Las redes neuronales se definen en función de unidades de procesamiento, mientras que las redes bayesianas se definen según la información del problema. Además, las redes bayesianas permiten cambiar la topología más fácilmente que las redes neuronales.
        - **Similitudes:** Ambas aprenden a partir de datos y se pueden usar en problemas similares como clasificación y predicción.
        
3. **¿Cuáles son las tres alternativas para diseñar la estructura de una red bayesiana?**
    
    - **Respuesta:**
        
        - A partir de datos.
        - Con la ayuda de un experto en el problema.
        - Combinando ambas, lo cual es generalmente la mejor opción, ya que permite integrar conocimiento objetivo y subjetivo.
        
    
4. **¿Qué es el algoritmo de abejas y cuáles son sus características principales?**
    
    - **Respuesta:** El algoritmo de abejas genera zonas asociadas a abejas exploradoras y ubica abejas obreras dentro de esas áreas. Si una abeja obrera encuentra una mejor solución, se convierte en exploradora. Sus características incluyen la explotación de áreas del espacio de búsqueda y la capacidad de encontrar buenas soluciones, aunque no siempre óptimas.
    
5. **¿Qué aplicaciones tiene AlphaZero?**
    
    - **Respuesta:** AlphaZero se utiliza principalmente en juegos de estrategia como ajedrez, Go y shogi, donde aprende y mejora a través de la auto-jugabilidad, desarrollando estrategias avanzadas.
    
6. **¿Qué factores pueden causar fallas en la implementación de un sistema inteligente?**
    
    - **Respuesta:** Las fallas pueden deberse a datos de entrenamiento insuficientes o sesgados, modelos mal diseñados, falta de validación y pruebas exhaustivas, y cambios en el entorno que no se reflejan en los datos de entrenamiento.
    
7. **¿Cómo se define la función heurística para un algoritmo de enjambre y qué características debe tener?**
    
    - **Respuesta:** La función heurística debe evaluar la calidad de las soluciones en el espacio de búsqueda, ser eficiente en tiempo de cálculo, guiar al algoritmo hacia soluciones óptimas y ser adaptativa.
    
8. **¿Qué tipo de problemas se pueden resolver con algoritmos de inteligencia de enjambre?**
    
    - **Respuesta:** Se pueden resolver problemas de optimización, búsqueda y clasificación, así como problemas relacionados con la logística y la planificación.
    
9. **¿Qué se espera de los estudiantes en el examen respecto a la comprensión de las tecnologías de inteligencia artificial?**
    
    - **Respuesta:** Se espera que los estudiantes comprendan las características, aplicaciones, ventajas y desventajas de las diferentes tecnologías de inteligencia artificial, así como su capacidad para resolver problemas específicos.

---
clase ok
Aquí están las respuestas a las preguntas, basadas en la transcripción proporcionada:

1. **¿Por qué una Convolutional Neural Networks (ConvNets) no necesita una gran cantidad de parámetros (pesos de conexiones) para aprender a procesar imágenes?** **RTA.:** Una ConvNet no necesita una gran cantidad de parámetros debido al concepto del **kernel de filtro**. Este filtro se mueve dentro de la matriz de los datos de entrada (píxeles de la imagen), generando un procesamiento de todos los valores de entrada de la imagen. Los pesos de las conexiones se comparten porque siempre se usan los mismos valores del filtro o kernel de filtro. Durante el entrenamiento, se definen los valores de este filtro los parámetros de filtro, que generalmente son de tamaños pequeños (e.g., 3x3, 5x5 1x1 o 2x2  para procesar la imagen). Esto reduce drásticamente la cantidad de parámetros a definir en comparación con una red multiperceptrón que necesitaría un peso por cada conexión.
    
2. **Indique por lo menos dos diferencias y dos similitudes entre las Redes Neuronales Artificiales y las Redes Bayesianas.** **RTA.:**
    
    - **Diferencias:**
        
        - **Definición de Topología:** En una Red Neuronal Artificial, la topología se define en función de las unidades de procesamiento necesarias y, si el problema cambia, a menudo se requiere un reentrenamiento completo. En una Red Bayesiana, la topología se define en función de la información disponible del problema y es más fácil agregar nodos o cambiar puntos de entrada/salida sin un reentrenamiento completo.
        - **Interpretación (Caja Negra vs. Caja Blanca):** Las Redes Neuronales Artificiales son a menudo consideradas "caja negra" porque es difícil justificar sus resultados. Las Redes Bayesianas son más "caja blanca" ya que pueden justificar sus resultados y son más interpretables.

en RNA defino una topologia, si hay mas problemas, meto mas neuronas y entreno desde cero, cada problea debo reentrenar (implica reentrenamiento)
la bayesaiana le puedo agregar mas estados que puedo considerar y agregar mas variables, las conexiones que existen no hace falta cambiar, entbces es mas facil agregar nodos en una red bayesiada
las bayesianas son supervizadas (el atrubuto clase que lo ahce supervizado), la RNA puede ser ambas (supervizado y no supervizado)
las redes bayesianas se puede definir con un experto del problema, las rna se puede definir con un experto de rna

las bayesianas no pueden tener ciclos
pero las RNA pueden tener ciclos, como las redes recurrentes tiene ciclos


RNA ajusta los pesos de las condiciones
la bayesiada ajusta los valores de las  probabilidades condicionales y de las realidades a priori

    - **Similitudes:**
        
        - **Aprendizaje a partir de Datos:** Ambas tecnologías aprenden a partir de datos, aunque lo hacen bajo diferentes paradigmas.
        - **Aplicación a Problemas Similares:** Se pueden usar en problemas similares como clasificación, predicción y diagnóstico.

podemos usar concepto de redes conectados



pueden haber convolucionas vs perceptron, similitudes, el tipo de problema que se puede aplicar, la especificacion de la estimacion, aprende a partir de datos, definir la topologia, que son de caja negra, que son algoritmos de  back propagation

diferencias como nodo de filtro que la tiene las conv net que tiene auqmneta la cantidad de parametros que se tine que definir en el entrenamiento
la multiperceptron tarda mas aen aprender que una convolucional
la multiperceptron maneja datos en forma de matriz
una usa el concepto de pooling
ambas se recomienda usar  redbool
la multiperceptron tarda mas en aprender, usa e forma de vector
la vonc red en forma de matriz

**Similitudes:**

- **Aprendizaje a partir de Datos:** Ambas aprenden a partir de datos, aunque con diferentes paradigmas.
- **Aplicación a Problemas Similares:** Se pueden usar en problemas similares como clasificación, predicción y diagnóstico.
- **Estructura de Red:** Ambas utilizan el concepto de redes con nodos conectados (grafos). Sin embargo, en las Redes Bayesianas, los grafos son acíclicos dirigidos, mientras que en las Redes Neuronales, algunas (como las recurrentes) pueden tener ciclos y otras no.
- **Parámetros Numéricos Ajustables:** Ambas tienen parámetros numéricos que se definen durante el entrenamiento a partir de datos. En las RNA, se ajustan los pesos de las conexiones; en las Redes Bayesianas, se ajustan los valores de las probabilidades condicionales y a priori.


3. **Describa las tres alternativas para diseñar la estructura de una Red Bayesiana. ¿Cuál es la mejor? ¿Por qué?**  
**RTA.:** Las tres alternativas para diseñar la estructura de una Red Bayesiana son:

    - **A partir de datos:** La estructura se genera automáticamente utilizando algoritmos que analizan los datos disponibles.
    - **Con ayuda de un experto:** Un experto en el dominio del problema define la estructura de la red basándose en su conocimiento.
    - **Combinada (híbrida):** Se genera la estructura a partir de los datos y luego un experto la revisa y realiza los cambios necesarios. La **mejor** alternativa es la **combinada**. Esto se debe a que combina el conocimiento objetivo derivado de los datos con la información y experiencia del experto, lo que permite mejorar la topología de la red y los valores de las probabilidades, aprovechando tanto el conocimiento público como el privado.

		    **RTA.:** Las tres alternativas para diseñar la estructura de una Red Bayesiana son:

**A partir de datos:** La estructura de la red se infiere y aprende directamente de los datos disponibles.  No siempre esta disponible el experto
	**Con ayuda de un experto:** La estructura es definida por un experto en el dominio del problema, basándose en su conocimiento y experiencia.
	 **Combinada (Híbrida):** Se genera la estructura inicialmente a partir de los datos, y luego un experto la revisa y realiza los ajustes o cambios necesarios para mejorar los resultados.
	 
3. **¿En qué tipo de problema aplicaría un algoritmo de Inteligencia de Enjambre? ¿Por qué?** **RTA.:** Un algoritmo de Inteligencia de Enjambre se aplicaría principalmente en problemas de **optimización** y **búsqueda**.
    
    - **Optimización:** Permite encontrar la mejor combinación de valores que maximiza o minimiza una función. Por ejemplo, optimizar los tiempos de los semáforos en una ciudad para maximizar el movimiento de vehículos y reducir la congestión.
    - **Búsqueda:** Algoritmos como el de hormigas pueden barrer un mapa de búsqueda, probando caminos y dejando rastros (feromonas) para encontrar el mejor camino, incluso alternativos si el óptimo no es viable (e.g., rutas de GPS para evitar cortes). La justificación radica en que estos algoritmos están diseñados para explorar eficientemente grandes espacios de soluciones, imitando comportamientos colectivos de la naturaleza para converger hacia soluciones óptimas o casi óptimas.
    
4. **Indique por lo menos dos diferencias y dos similitudes entre los algoritmos de Computación Evolutiva y los de Inteligencia de Enjambre.** **RTA.:**
    
    - **Diferencias:**
        
        - **Mecanismo de Trabajo:** La Computación Evolutiva aplica el concepto de evolución con operadores como selección, cruzamiento y mutación, donde los individuos compiten entre sí. La Inteligencia de Enjambre aplica otros operadores que emulan cómo los seres vivos buscan comida, siendo más cooperativos y usando la inteligencia colectiva.
        - **Naturaleza de los Individuos:** En Computación Evolutiva, la "supervivencia del más apto" es clave, con un enfoque más individualista en la mejora de soluciones. En Inteligencia de Enjambre, hay una mayor cooperación entre los agentes para encontrar la mejor solución.
        
    - **Similitudes:**
        
        - **Resolución de Problemas de Optimización:** Ambos tipos de algoritmos se pueden usar para resolver problemas de optimización.
        - **Necesidad de Función de Evaluación:** Ambos necesitan una función definida para evaluar las posibles soluciones (función de aptitud en Computación Evolutiva o función heurística en Inteligencia de Enjambre), que indica qué tan buena es una solución.
        
    
5. **¿Qué es el Algoritmo de Abejas? Descríbalo e indique sus principales características.** **RTA.:** El Algoritmo de Abejas es un algoritmo de optimización inspirado en el comportamiento de búsqueda de alimento de las abejas.
    
    - **Descripción:** El algoritmo genera zonas o áreas asociadas a abejas exploradoras. Dentro de estas áreas, ubica abejas obreras. Si una abeja obrera encuentra una solución mejor que la actual en su área, se convierte en una nueva abeja exploradora y define una nueva área. De esta manera, el algoritmo explota regiones prometedoras del espacio de búsqueda y luego explora otras si no se pueden mejorar los resultados.
    - **Principales Características:**
        
        - Trabaja por áreas, lo que le permite explotar partes específicas del espacio de búsqueda.
        - Busca encontrar la mejor solución, aunque no siempre garantiza encontrar el óptimo global.
        - Generalmente encuentra buenas soluciones.
        
    
6. **Describa brevemente algún Problema de Optimización (inventado o real) e indique qué tecnología sería la más adecuada para resolverlo. Justifique su respuesta teniendo en cuenta sus características.** **RTA.:**
    
    - **Problema:** Optimización de la agenda diaria de una persona. Dada una serie de actividades con duraciones y posibles dependencias, determinar el orden óptimo para realizarlas de manera que se minimice el tiempo muerto o se maximice la productividad.
    - **Tecnología más adecuada:** Un algoritmo de **Inteligencia de Enjambre** (como el Algoritmo de Abejas o el de Partículas) o un algoritmo de **Computación Evolutiva** (como un Algoritmo Genético).
    - **Justificación:** Estos algoritmos son adecuados porque el problema implica encontrar la mejor combinación de un conjunto de elementos (las actividades) en un espacio de búsqueda potencialmente grande. Los algoritmos de enjambre y evolutivos son robustos para explorar y explotar soluciones en este tipo de espacios, permitiendo encontrar una secuencia de actividades que optimice el objetivo deseado (minimizar tiempo, maximizar productividad), incluso si el óptimo global es difícil de alcanzar.
    
7. **Describa brevemente algún Problema (inventado o real) donde sería adecuado aplicar un modelo Large Language Model (LLM) justificando su respuesta.** **RTA.:**
    
    - **Problema:** Generación de diagnósticos médicos simulados para estudiantes de medicina. Un LLM podría generar radiografías simuladas con diversas características y condiciones (e.g., una manchita, una variación) y proporcionar un diagnóstico correspondiente. El estudiante podría entonces practicar la identificación de enfermedades y corroborar sus propios diagnósticos.
    - **Justificación:** Los LLM son ideales para este problema porque están orientados al procesamiento de texto y series temporales, y pueden generar contenido coherente y contextualizado. Aunque el ejemplo es de imágenes, el LLM podría generar las descripciones textuales de las radiografías y los diagnósticos. Su capacidad para aprender de grandes volúmenes de datos y generar texto complejo y relevante los hace aptos para crear escenarios de práctica variados y realistas, incluyendo la descripción de hallazgos y la justificación de diagnósticos.
    
8. **En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con mejores características para ser aplicado en la resolución de problemas? ¿Por qué?** **RTA.:** Esta es una pregunta de opinión, y la justificación es clave.
    
    - **Ejemplo de Respuesta:** En mi opinión, las **Redes Neuronales Convolucionales (CNNs)** tienen las mejores características para la resolución de problemas que involucran el procesamiento de imágenes.
    - **Justificación:** Su capacidad para aprender jerarquías de características directamente de los datos de imagen, junto con el uso de filtros compartidos que reducen la cantidad de parámetros, las hace extremadamente eficientes y potentes para tareas como clasificación de imágenes, detección de objetos y reconocimiento facial. Su rendimiento superior en estos dominios las convierte en una herramienta indispensable.
    
9. **En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con peores características para ser aplicado en la resolución de problemas? ¿Por qué?** **RTA.:** Esta es una pregunta de opinión, y la justificación es clave.
    
    - **Ejemplo de Respuesta:** En mi opinión, las **Redes Neuronales Recurrentes (RNNs) básicas** tienen las peores características para problemas de secuencias a largo plazo.
    - **Justificación:** Aunque fueron pioneras en el procesamiento de secuencias, las RNNs básicas sufren del problema del "gradiente desvanecido" o "gradiente explosivo", lo que les dificulta aprender dependencias a largo plazo en los datos. Esto las hace menos efectivas para tareas donde la información relevante puede estar muy separada en la secuencia, en comparación con sus evoluciones como LSTM o GRU, o los más recientes LLM basados en atención.