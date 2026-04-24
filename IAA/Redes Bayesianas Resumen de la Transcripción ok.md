La transcripción se centra en las **Redes Bayesianas** como el único modelo de razonamiento aproximado a estudiar en la asignatura, contrastándolas con la lógica difusa y mencionando brevemente los modelos de Markov.

**Conceptos Fundamentales:**

- Las Redes Bayesianas se basan en el **Teorema de Bayes** y el manejo de la **probabilidad**, permitiendo hacer predicciones y análisis de incertidumbre.
- Se las describe como un **grafo acíclico dirigido**, donde cada "circulito" o "cuadradito" representa un **estado** (variable del problema) y las flechas indican relaciones de influencia.
- Cada estado debe tener valores **discretos (no puede usar valores continuos), mutuamente excluyentes (no tiene ningún tipo de solapamiento) y exhaustivos(que tiene que estar completo), a los que se asocian probabilidades.** 
Funciona mejor ante la incertidumbre
**Diferencias con Redes Neuronales:**
- A diferencia de las redes neuronales, donde cada neurona es una unidad de procesamiento, en las Redes Bayesianas cada nodo es una **variable del problema**.
- Son mucho más **flexibles y dinámicas** que una red neuronal: se puede poner **evidencia** (información conocida) en cualquier nodo y obtener resultados de cualquier otro, sin una interfaz de entrada/salida fija. Esto las hace muy útiles para situaciones cambiantes o **diagnósticos** (medicos, de equiopos , de linea de mntaje).

**Limitaciones:**
- No soportan **ciclos** en su grafo.
- No manejan directamente información **continua**; los datos deben ser discretizados.
- No representan la "incompletitud" o grados de pertenencia tan bien como la lógica difusa.
- No son adecuadas para procesar directamente imágenes o texto sin una compleja discretización.

**Algoritmos de Propagación:**
![[Pasted image 20250709131849.png]]
- La inferencia se realiza mediante la **propagación de probabilidades** a través de mensajes (vector de valores numéricos) (pi de padre a hijo, lambda es el mensaje de hijo a padre).
![[Pasted image 20250709080711.png]]
- Se utilizan **algoritmos exactos** para estos cálculos, aplica las fórmulas matemáticas que  pueden ser complejas, las herramientas computacionales las resuelven automáticamente.
![[Pasted image 20250709080945.png]]
**Construcción y Validación:**
- La **estructura** de la red y sus **valores probabilísticos** pueden definirse:
    - definido **Manualmente** (con un experto).
    - definido **Automáticamente** (a partir de una base de datos, usando algoritmos de aprendizaje estructural y paramétrico).
    - **Combinando** ambas (generar automáticamente y refinar con un experto).
- Se utilizan herramientas como **Jenny** (gráfica e intuitiva) o librerías en **Google Colab** (como PGMPI) para crear, visualizar y validar las redes.
- Se ejemplifica la creación de redes con algoritmos como **Naive Bayes (Nive Valles)**, **Tree Augmented Naive Bayes (TAN)** y **Grid**, mostrando cómo difieren en sus conexiones y cómo se validan sus resultados (ej., co
**Aplicaciones:**
- Son especialmente útiles para **diagnóstico** (médico, de equipos, de impresoras) y **predicción** (ej., ozono).
En resumen, las Redes Bayesianas son una herramienta poderosa para el razonamiento bajo incertidumbre, destacando por su flexibilidad, capacidad de diagnóstico y la posibilidad de integrar conocimiento experto con aprendizaje a partir de datos, aunque requieren la discretización de variables continuas.