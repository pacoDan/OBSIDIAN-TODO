#### **1) ¿Por qué una Convolutional Neural Networks (ConvNets) no necesita una gran cantidad de parámetros (pesos de conexiones) para aprender a procesar imágenes?**

- **Respuesta:** Las ConvNets no necesitan una gran cantidad de parámetros debido al **concepto del kernel o filtro**. o kernel de filtro que aplican esta red para intentar reducir el peso d elas conexiones
    
    - Este filtro se mueve dentro de la matriz de los datos de entrada (píxeles de la imagen), generando un procesamiento de todos  los valores de entrada. simulando como si fuera la entradas de muchas neuronas.
    - Los pesos de las conexiones están **compartidos** porque siempre se usan los mismos valores del filtro o filtro de kernel, y se va aplicando o desplazando  a distintos valores de entrada.
    - Durante el entrenamiento, se definen los parámetros del filtro, que suelen ser de tamaños pequeños (ej., 3x3, 5x5 o 2x2 etc).
    - Esto reduce drásticamente la cantidad de parámetros a definir en comparación con una red multiperceptrón, que necesitaría un peso por cada conexión. Por ejemplo, 10 filtros de 3x3 solo requieren 90 parámetros, una cantidad mínima comparada con lo que necesitaría una red multiperceptrón para una imagen grande.
    

#### **2) Indique por lo menos dos diferencias y dos similitudes entre las Redes Neuronales Artificiales y las Redes Bayesianas.**

- **Diferencias:**
    
    - **Definición de Topología:** Las Redes Neuronales Artificiales (RNA) se definen en función de las unidades de procesamiento necesarias y tienen topologías más definidas. Si el problema cambia, a menudo se requiere un reentrenamiento completo o un cambio de red. Las Redes Bayesianas (RB) se definen en función de la información disponible del problema y permiten cambiar la topología o agregar nodos más fácilmente sin un reentrenamiento completo de las conexiones existentes.
    - **Flexibilidad de Nodos de Entrada/Salida:** En una RB, se puede poner evidencia en cualquier nodo (entrada o salida), lo que permite cambiar los puntos de entrada y salida. En una RNA, los nodos de entrada y salida son fijos.
    - **Interpretabilidad (Caja Negra vs. Caja Blanca):** Las RNA son a menudo consideradas "caja negra" porque es difícil interpretar cómo llegan a sus resultados. Las RB son más "caja blanca" porque pueden justificar sus resultados a través de las probabilidades y la estructura de las relaciones.
    - **Uso de Expertos:** Las RB pueden definirse con la ayuda de un experto del problema, además de datos. Las RNA se definen con la ayuda de un experto en redes neuronales, pero no necesariamente un experto en el dominio del problema.
    - **Parámetros de Ajuste:** Las RNA ajustan los pesos de las conexiones durante el entrenamiento. Las RB ajustan los valores de las probabilidades condicionales y a priori.
    
- **Similitudes:**
    
    - **Aprendizaje a partir de Datos:** Ambas tecnologías aprenden a partir de datos, aunque con diferentes paradigmas.
    - **Aplicación a Problemas Similares:** Ambas pueden usarse para resolver problemas de clasificación, predicción y diagnóstico.
    - **Estructura de Red:** Ambas utilizan el concepto de redes con nodos conectados. (Aunque las RB son grafos acíclicos dirigidos, y algunas RNA, como las recurrentes, pueden tener ciclos).
    - **Parámetros Numéricos:** Ambas tienen parámetros numéricos que se definen durante el entrenamiento a partir de datos, lo que las clasifica como tecnologías de Machine Learning.
    

#### **3) Describa las tres alternativas para diseñar la estructura de una Red Bayesiana. ¿Cuál es la mejor? ¿Por qué?**

- **Alternativas para Diseñar la Estructura de una Red Bayesiana:**
    
    1. **A partir de Datos:** La estructura se aprende directamente de los datos disponibles.
    2. **Con Ayuda de un Experto:** La estructura es definida por un experto en el dominio del problema.
    3. **Combinada (Híbrida):** Se genera la estructura inicialmente a partir de los datos, y luego un experto la revisa y ajusta.
    
- **¿Cuál es la mejor? ¿Por qué?**
    
    - La **alternativa combinada (híbrida)** es generalmente considerada la mejor.
    - **Justificación:** Combina el conocimiento objetivo derivado de los datos del problema con la información y experiencia del experto. Esto permite mejorar la topología de la red y los valores de las probabilidades, aprovechando tanto el conocimiento público (datos) como el privado (experto). Aunque puede ser discutible si el experto no está disponible o los datos no están actualizados, la combinación suele ofrecer los mejores resultados.
    

#### **4) ¿En qué tipo de problema aplicaría un algoritmo de Inteligencia de Enjambre? ¿Por qué?**

- **Tipo de Problema:** Principalmente en problemas de **optimización** y **búsqueda**.
- **Justificación:**
    
    - **Optimización:** Permiten encontrar la mejor combinación de valores que maximiza o minimiza una función objetivo (ej., minimizar costos, maximizar ganancias).
    - **Búsqueda:** Algoritmos como el de hormigas son ideales para problemas de búsqueda de caminos, permitiendo explorar un "mapa" de búsqueda, dejando rastros (feromonas) y podando el árbol de búsqueda para encontrar el mejor camino o caminos alternativos.
    - Los algoritmos de abejas y pájaros también se enfocan en optimización, buscando la mejor solución en un espacio de búsqueda.
    

#### **5) Indique por lo menos dos diferencias y dos similitudes entre los algoritmos de Computación Evolutiva y los de Inteligencia de Enjambre.**

- **Diferencias:**
    
    - **Mecanismo de Mejora:** En Computación Evolutiva (CE), las soluciones se "mejoran" a través de operadores de evolución (selección, cruzamiento, mutación) que generan nuevas soluciones a partir de las existentes. En Inteligencia de Enjambre (IE), las soluciones se buscan y se encuentran mejores, pero no se "mejoran" las que se tienen en el mismo sentido evolutivo; se prueban nuevas soluciones de forma pseudoaleatoria.
    - **Filosofía de Trabajo:** CE se basa en el concepto de evolución y "supervivencia del más apto", donde los individuos compiten para generar descendencia. IE se basa en la inteligencia colectiva y la cooperación, donde los individuos se ayudan mutuamente para encontrar la mejor solución.
    - **Operadores:** CE utiliza operadores específicos como selección, cruzamiento y mutación. IE utiliza otros operadores que emulan el comportamiento de búsqueda de alimento de seres vivos.
    - **Representación de Soluciones:** En CE, la posible solución suele estar dada por la estructura de un cromosoma (a menudo binario, aunque puede ser real). En IE, generalmente está dada por una posición o ubicación dentro del espacio de búsqueda (a menudo números reales).
    
- **Similitudes:**
    
    - **Resolución de Problemas de Optimización:** Ambos tipos de algoritmos son ampliamente utilizados para resolver problemas de optimización.
    - **Función de Evaluación:** Ambos necesitan una función para evaluar la calidad de las posibles soluciones (función de aptitud en CE, función heurística en IE), que mide qué tan buena es una solución.
    - **Naturaleza Heurística:** Ninguno de los dos algoritmos garantiza encontrar la solución óptima global; pueden converger a óptimos locales.
    - **Iteración:** Ambos suelen requerir muchas iteraciones o ciclos para generar una solución.
    - **Momento de la Mejor Solución:** La mejor solución no necesariamente aparece en la última iteración; puede encontrarse en cualquier momento de la corrida.
    

#### **6) ¿Qué es el Algoritmo de Abejas? Descríbalo e indique sus principales características.**

- **Descripción:** El Algoritmo de Abejas es un algoritmo de optimización inspirado en el comportamiento de búsqueda de alimento de las abejas. Funciona generando **zonas o áreas** asociadas a abejas exploradoras. Dentro de estas áreas, se ubican abejas obreras. Si una abeja obrera encuentra una solución mejor dentro de su área, esa abeja se convierte en una nueva abeja exploradora y define una nueva área de búsqueda.
- **Principales Características:**
    
    - **Trabajo por Áreas:** Su característica distintiva es que trabaja por regiones o áreas del espacio de búsqueda.
    - **Explotación y Exploración:** Permite explotar intensivamente partes prometedoras del espacio de búsqueda (dentro de las áreas) y también explorar nuevas regiones cuando no se pueden mejorar los resultados en las áreas actuales.
    - **Búsqueda de Soluciones:** Generalmente encuentra buenas soluciones, aunque no siempre garantiza la óptima global.
    - **Adaptación de Áreas:** Las áreas pueden achicarse si no se encuentran mejoras, lo que permite refinar la búsqueda.
    

#### **7) Describa brevemente algún Problema de Optimización (inventado o real) e indique qué tecnología sería la más adecuada para resolverlo. Justifique su respuesta teniendo en cuenta sus características.**

- **Problema de Optimización (Ejemplo):** **Optimización de Rutas de Entrega para una Flota de Camiones.**
    
    - **Descripción:** Una empresa de logística con una flota de camiones necesita determinar las rutas óptimas para entregar paquetes a múltiples clientes en una ciudad, minimizando el costo total (combustible, tiempo de conducción) y el tiempo de entrega, considerando restricciones como la capacidad de los camiones, ventanas de tiempo de entrega de los clientes y posibles cortes de ruta o congestión de tráfico.
    
- **Tecnología más Adecuada:** **Algoritmos de Inteligencia de Enjambre (especialmente el Algoritmo de Hormigas o el de Abejas/Pájaros) o Algoritmos de Computación Evolutiva (ej., Algoritmos Genéticos).**
- **Justificación:**
    
    - **Inteligencia de Enjambre (Hormigas):** El algoritmo de hormigas es ideal para problemas de búsqueda de caminos y optimización de rutas. Las "hormigas" pueden explorar diferentes caminos, dejando un rastro de "feromonas" (información sobre la calidad del camino). Los caminos más eficientes acumulan más feromonas, atrayendo a más hormigas y reforzando esas rutas. Esto permite encontrar el camino óptimo o soluciones subóptimas satisfactorias incluso ante cambios dinámicos (como cortes de ruta).
    - **Computación Evolutiva (Genéticos):** Los algoritmos genéticos también son muy adecuados. Cada "cromosoma" podría representar una posible secuencia de entregas o una ruta. Los operadores de selección, cruzamiento y mutación permitirían explorar y combinar diferentes rutas, evolucionando hacia soluciones más eficientes que minimicen el costo y el tiempo.
    - **Características Relevantes:** Ambos tipos de algoritmos son robustos para problemas complejos con grandes espacios de búsqueda, donde una solución exacta es computacionalmente inviable. Son capaces de encontrar soluciones de buena calidad en un tiempo razonable, incluso si no garantizan la óptima global.
    

#### **8) Describa brevemente algún Problema (inventado o real) donde sería adecuado aplicar un modelo Large Language Model (LLM) justificando su respuesta.**

- **Problema (Ejemplo):** **Generación de Contenido Educativo Personalizado para Estudiantes de Medicina.**
    
    - **Descripción:** Un estudiante de medicina necesita practicar el diagnóstico de enfermedades a partir de imágenes médicas (ej., radiografías) y descripciones de casos clínicos. El problema es que las bases de datos de casos reales son limitadas y repetitivas. Se busca un sistema que pueda generar nuevos casos clínicos y radiografías con variaciones sutiles para ofrecer una práctica ilimitada y diversa.
    
- **Tecnología Adecuada:** **Large Language Model (LLM) combinado con modelos de difusión (Diffusion Models).**
- **Justificación:**
    
    - **LLM para Casos Clínicos:** Un LLM es ideal para generar descripciones de casos clínicos. Puede tomar parámetros de entrada (ej., tipo de enfermedad, síntomas, historial del paciente) y generar texto coherente y realista que simule un caso clínico. Su capacidad para comprender y generar lenguaje natural le permite crear narrativas complejas y variadas.
    - **Modelos de Difusión para Imágenes:** Los modelos de difusión son excelentes para la generación de imágenes realistas a partir de descripciones textuales o condiciones. Se podría usar un modelo de difusión para generar radiografías que correspondan a los casos clínicos generados por el LLM, incluyendo "manchitas" o anomalías específicas que el estudiante deba identificar.
    - **Combinación:** La combinación de un LLM (para el texto del caso) y un modelo de difusión (para la imagen médica) permitiría crear un sistema de entrenamiento altamente interactivo y personalizado, donde el estudiante recibe un caso y una imagen únicos, realiza un diagnóstico, y luego el sistema puede corroborar o proporcionar la respuesta correcta. Esto aprovecha la capacidad de los LLM para el procesamiento y generación de texto y la de los modelos de difusión para la generación de imágenes de alta calidad.
    

#### **9) En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con mejores características para ser aplicado en la resolución de problemas? ¿Por qué?**

- **Nota:** Esta es una pregunta de opinión, y la justificación es clave. La transcripción no da una respuesta única, pero ofrece ejemplos de justificaciones válidas.
- **Ejemplo de Respuesta (basada en la transcripción):**
    
    - **Tecnología:** **Redes Neuronales (en particular, Redes Convolucionales o Large Language Models).**
    - **Justificación:** Considero que las Redes Neuronales, especialmente las convolucionales para imágenes y los LLM para texto y series temporales, poseen las mejores características por su **flexibilidad y capacidad de aprendizaje profundo**.
        
        - Pueden aprender a resolver una amplia gama de problemas complejos (clasificación, estimación, generación) en dominios diversos como visión por computadora, procesamiento de lenguaje natural y análisis de series temporales.
        - Su arquitectura permite extraer características complejas de los datos de forma automática, lo que las hace muy potentes en escenarios donde las reglas explícitas son difíciles de definir.
        - La capacidad de los LLM para generar código o texto a partir de requerimientos, o la de las CNN para identificar objetos en imágenes, demuestra una versatilidad y un potencial de aplicación muy amplio en proyectos de software y sistemas inteligentes.
        
    

#### **10) En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con peores características para ser aplicado en la resolución de problemas? ¿Por qué?**

- **Nota:** Esta es una pregunta de opinión, y la justificación es clave. La transcripción no da una respuesta única, pero ofrece ejemplos de justificaciones válidas.
- **Ejemplo de Respuesta (basada en la transcripción):**
    
    - **Tecnología:** **Redes Bayesianas.**
    - **Justificación:** Aunque las Redes Bayesianas tienen sus ventajas, podrían considerarse con "peores características" en ciertos contextos debido a:
        
        - **Complejidad en el Uso de Probabilidades:** El uso de probabilidades puede ser complicado y propenso a generar contradicciones si no se manejan correctamente, especialmente en problemas muy grandes o con datos ruidosos.
        - **Restricción de Ciclos:** El hecho de que las redes bayesianas no puedan tener ciclos (son grafos acíclicos dirigidos) puede limitar su aplicabilidad en situaciones donde las relaciones causales o de dependencia son inherentemente cíclicas o bidireccionales.
        - **Procesamiento de Datos No Estructurados:** Tienen dificultades para procesar directamente datos no estructurados como texto o imágenes, a diferencia de las redes neuronales, lo que restringe su dominio de aplicación en el panorama actual de la IA.