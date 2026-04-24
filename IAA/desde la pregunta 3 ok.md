### 3. Describa las tres alternativas para diseñar la estructura de una Red Bayesiana. ¿Cuál es la mejor? ¿Por qué?

**RTA.:** Las tres alternativas para diseñar la estructura de una Red Bayesiana son:

1. **A partir de datos:** La estructura de la red se infiere y aprende directamente de los datos disponibles.
2. **Con ayuda de un experto:** La estructura es definida por un experto en el dominio del problema, basándose en su conocimiento y experiencia. 
3. **Combinada (Híbrida):** Se genera la estructura inicialmente a partir de los datos, y luego un experto la revisa y realiza los ajustes o cambios necesarios para mejorar los resultados. aca  el experto la revisa los conocimientos objetivos segun los datos

**¿Cuál es la mejor? ¿Por qué?** La alternativa **combinada** es generalmente considerada la mejor.

- **Justificación:** Porque combina el conocimiento objetivo que proviene de los datos del problema con la información y la experiencia del experto. Esto permite aprovechar lo mejor de ambos mundos: la objetividad de los datos y la valiosa información cualitativa del experto. Esta combinación puede aplicarse tanto a la topología de la red como a los valores de las probabilidades, resultando en un modelo más robusto y preciso.
- **Consideraciones:** Sin embargo, la "mejor" opción puede depender de la disponibilidad de datos actualizados o de la disposición y disponibilidad del experto para colaborar en el proyecto.

### 4. ¿En qué tipo de problema aplicaría un algoritmo de Inteligencia de Enjambre? ¿Por qué?

**RTA.:** Un algoritmo de Inteligencia de Enjambre (como abejas, hormigas o pájaros) se aplicaría principalmente en problemas de **optimización** y **búsqueda** (relacionado al algoritmo de hormiga).

- **Optimización:** Permiten encontrar la mejor combinación de valores que maximiza o minimiza una función.
    
    - **Ejemplo:** Optimización de los tiempos de los semáforos en una ciudad para maximizar el flujo de vehículos y evitar la congestión.
    
- **Búsqueda:** Permiten encontrar el mejor camino o solución en un espacio de búsqueda.
    Ejemplo también problemas de optimización en estos algoritmos de abejas
    - **Ejemplo:** Encontrar la ruta óptima en un GPS, donde el algoritmo de hormigas puede barrer el mapa de búsqueda, probando caminos y dejando rastros de feromonas para encontrar el mejor camino, incluso si hay obstáculos (como cortes de ruta) que obligan a buscar alternativas.
algoritmo de pájaros, para  control transito, ejemplo en semáforos
**Justificación:** Estos algoritmos son adecuados porque están diseñados para explorar eficientemente grandes espacios de soluciones, imitando el comportamiento colectivo de grupos en la naturaleza para converger hacia soluciones óptimas o casi óptimas.
Acá se puede hablar de algoritmos híbridos
### 5. Indique por lo menos dos diferencias y dos similitudes entre los algoritmos de Computación Evolutiva y los de Inteligencia de Enjambre.
**RTA.:**
**Diferencias:**
- **Mecanismo de Mejora de Soluciones:**
    - **Computación Evolutiva:** Trata de mejorar las soluciones a través de la evolución, aplicando ==operadores como selección==, cruzamiento y mutación. Los individuos compiten entre sí para prosperar y generar descendencia (supervivencia del más apto), ==compiten para buscar comida, para prosperar y generar ascendencia, es mas individual==.
    - **Inteligencia de Enjambre:** Busca soluciones y las mejora a través de la cooperación y la inteligencia colectiva. Los agentes se ayudan mutuamente, o cooperativo ==compartiendo información para encontrar la mejor solución==.
    
- **Operadores Utilizados:**
    
    - **Computación Evolutiva:** Utiliza operadores inspirados en la genética: selección, cruzamiento (recombinación) y mutación.
    - **Inteligencia de Enjambre:** Utiliza otros operadores que copian o emulan la forma en que algunos seres vivos buscan comida (e.g., movimiento de partículas, rastro de feromonas).
    
- **Representación de la Solución:**
    
    - **Computación Evolutiva:** La posible solución está dada por la estructura de un cromosoma (que puede ser binario o real).
    - **Inteligencia de Enjambre:** La posible solución está dada por una posición o ubicación dentro del espacio de búsqueda. ==se puede  representar directamente con números reales , a cada uno de los valores de las posiciones==.
**Similitudes:**

- **Resolución de Problemas de Optimización:** Ambos tipos de algoritmos se pueden usar para resolver problemas de optimización.
- **Necesidad de Función de Evaluación:** Ambos necesitan tener definida una función para evaluar las posibles soluciones (llamada ==función de aptitud== en Computación Evolutiva, y simplemente función en Inteligencia de Enjambre, pero con el mismo propósito de indicar qué tan buena es una solución). y la otra función heurística
- **Naturaleza Heurística:** Ninguno de los dos garantiza encontrar la solución óptima global, y a menudo requieren muchas iteraciones (ciclos) para converger a una buena solución.
- **Momento de Encontrar la Mejor Solución:** En ninguno de los dos algoritmos la mejor solución tiene que aparecer en la última iteración; puede aparecer en cualquier momento de la corrida (segunda vuelta, ultima etc, la solución pueden aparecer en cualquier vuelta). ==Ambas ciclan muchas veces para encontrar la solución==

### 6. ¿Qué es el Algoritmo de Abejas? Descríbalo e indique sus principales características.

**RTA.:** El Algoritmo de Abejas es un algoritmo de optimización inspirado en el comportamiento de búsqueda de alimento de las abejas en la naturaleza.

**Descripción:** El algoritmo funciona generando **zonas o áreas** asociadas a las **abejas exploradoras**. Dentro de cada una de estas áreas, se ubican otras abejas llamadas **obreras**. Lo importante es que si una abeja obrera encuentra una solución mejor dentro de su área que la que se tenía antes, esa abeja se convierte en una nueva abeja exploradora y define una nueva área. De esta manera, el algoritmo va tomando regiones o partes del espacio de búsqueda para **explotarlas** (buscar intensivamente) hasta que considera que no se pueden mejorar los resultados. Luego, comienza a probar en otras regiones. Si la solución encontrada es peor, el área se reduce.

**Principales Características:**

- **Trabaja por Áreas:** Su característica principal es que trabaja por áreas, lo que le permite explotar partes específicas del espacio de búsqueda de manera intensiva.
- **Exploración y Explotación:** Balancea la exploración de nuevas regiones con la explotación de las regiones prometedoras.
- **Búsqueda de Soluciones:** Generalmente encuentra buenas soluciones, aunque no siempre garantiza encontrar la solución óptima global.
https://youtu.be/G_LKYGbmzKQ?t=3193

==que es un LLM (arquitecturas/transformers llm) , describa e indica sus principales características:==
es una red neuronal orientado a procesamiento de texto, sobre todo de series temporales, donde hay gran cantidad de capas y hay modulos de encoder y  uno de decoder, y el componente principal es el mecanismo de atencion que le permite al modelo aprender identificar lcuales son los elementos mas relevantes de los datos de entrada para luego generar la salida correspondiente, se podría hablar del mecanismo de atención, el multihead atention... todo estos destaca el LLM de una red neuronal
### 7. Describa brevemente algún Problema de Optimización (inventado o real) e indique qué tecnología sería la más adecuada para resolverlo. Justifique su respuesta teniendo en cuenta sus características.

**RTA.:**

- **Problema:** **Optimización de la distribución de productos en una cadena de suministro.** Una empresa de logística necesita determinar las rutas más eficientes para sus camiones, considerando múltiples depósitos, puntos de entrega, capacidades de los vehículos, ventanas de tiempo de entrega y características de los productos (e.g., peligrosos, perecederos) para minimizar el costo total y el tiempo de entrega.
- **Tecnología más adecuada:** **==Algoritmos de Inteligencia de Enjambre==** (como el Algoritmo de Hormigas o el Algoritmo de Enjambre de Partículas) o **Algoritmos Genéticos** (parte de la ==Computación Evolutiva==).
- **Justificación:** Este es un problema de optimización combinatoria con un espacio de soluciones extremadamente grande y múltiples restricciones. Los algoritmos de Inteligencia de Enjambre y Computación Evolutiva son ideales para este tipo de problemas porque:
    
    - Son capaces de explorar grandes espacios de búsqueda de manera eficiente.
    - Pueden manejar múltiples objetivos (minimizar tiempo y costo) y restricciones complejas.
    - Son robustos para encontrar soluciones cercanas al óptimo global en un tiempo razonable, incluso si el óptimo exacto es intratable computacionalmente.
    - El algoritmo de hormigas, por ejemplo, es particularmente apto para problemas de ruteo debido a su inspiración en la búsqueda de caminos.
    
ver problemas de generación con modelos de imagen con difusion
ver redes tipo encoder/outcoder para completar datos faltantes
ver modelos difusion para generar radiografias para determinar diagnostico, con modelos difusion
### 8. Describa brevemente algún Problema (inventado o real) donde sería adecuado aplicar un modelo Large Language Model (LLM) justificando su respuesta.

**RTA.:**

- **Problema:** **Asistente de escritura creativa para guionistas de cine y televisión.** Un LLM podría ser utilizado para ayudar a guionistas a generar ideas para tramas, desarrollar personajes, escribir diálogos coherentes y en el estilo deseado, o incluso generar borradores de escenas completas a partir de una breve descripción.
- **Justificación:** Los Large Language Models (LLMs) son extremadamente adecuados para este problema debido a sus características principales:
    
    - **Procesamiento y Generación de Texto:** Su capacidad fundamental es entender y generar texto de alta calidad, lo cual es esencial para la escritura creativa.
    - **Manejo de Contexto:** Pueden mantener el contexto a lo largo de conversaciones o documentos extensos, lo que les permite generar diálogos y tramas coherentes.
    - **Adaptación de Estilo:** Pueden ser ajustados (fine-tuning) para emular estilos de escritura específicos o para generar contenido que se adapte a un género particular (comedia, drama, ciencia ficción).
    - **Gran Cantidad de Parámetros:** Su vasta cantidad de parámetros y el entrenamiento en enormes volúmenes de texto les permiten tener un conocimiento amplio sobre narrativas, personajes y estructuras lingüísticas, lo que es invaluable para la creatividad asistida.
    - analisis de sentimientos
    - incluir ideas de distintos autores
    - escribir un tp para una materia
    


---
estas dos preguntas son subjetivas:
### 9. En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con mejores características para ser aplicado en la resolución de problemas? ¿Por qué?

**RTA.:** (Esta es una pregunta de opinión, la justificación es clave).

- **Ejemplo de Respuesta:** En mi opinión, los **Large Language Models (LLMs)** son el tipo de tecnología de IA con mejores características para ser aplicada en la resolución de una amplia gama de problemas.
- **Justificación:** Su versatilidad es inigualable. Pueden procesar y generar texto, resumir información, traducir idiomas, escribir código, responder preguntas complejas, y hasta generar ideas creativas. Su capacidad para entender el lenguaje natural y producir respuestas coherentes y contextualmente relevantes los hace aplicables a casi cualquier dominio que involucre información textual o simbólica. Además, la posibilidad de realizar "fine-tuning" sobre modelos pre-entrenados permite adaptarlos a tareas muy específicas con menos recursos que entrenar un modelo desde cero.

### 10. En su opinión, ¿cuál es el tipo de tecnología de la Inteligencia Artificial con peores características para ser aplicado en la resolución de problemas? ¿Por qué?

**RTA.:** (Esta es una pregunta de opinión, la justificación es clave).

- **Ejemplo de Respuesta:** En mi opinión, las **Redes Bayesianas** tienen algunas de las peores características para la resolución de problemas en ciertos contextos, especialmente cuando se comparan con redes neuronales modernas.
- **Justificación:** Aunque son interpretables y manejan bien la incertidumbre, su principal desventaja radica en la **dificultad para escalar a problemas con un gran número de variables o relaciones complejas**. La definición de las probabilidades condicionales puede volverse intratable, y la necesidad de que el grafo sea acíclico puede ser una limitación en situaciones donde las dependencias son más dinámicas o cíclicas. Además, su rendimiento en tareas como el procesamiento de imágenes o texto es muy limitado en comparación con las redes neuronales especializadas.

que tecnología es apropiada para algún proyecto de software
rta: LLM entrenado para generar código para cumplir con reqs



==como funciona los algoritmos de agente==, las Qlearing, DQN, y alphazero
ver programación genetica
inteligencia de enjambre
la red kohone  som, por que se usa para clustering, la LBQ esta incluida en la red muultiperceptron
deep autoconcer que es y como funciona
las LCSTM y gru
LLM y difusión características  principales en aplicaciones
RNN y diferencia con LCTM
