El discurso se centra en la introducción de los agentes inteligentes, su definición, y las tecnologías utilizadas para implementarlos, especialmente aquellas basadas en _machine learning_ y aprendizaje por refuerzo.

- **Definición de Agentes Inteligentes:** Una entidad capaz de actuar de manera autónoma para satisfacer objetivos y metas, situada persistentemente en su entorno. A diferencia de los sistemas inteligentes que operan por reflejos, los agentes inteligentes consideran objetivos y buscan maximizar recompensas.
- **Interacción Agente-Entorno:** El agente recibe información del entorno (percepciones u observaciones), determina qué acción realizar de su lista de capacidades, y aplica esa acción al entorno para orientarlo hacia un objetivo.
- **Tecnologías de Implementación:** para implementar el agente
    
    - **Q-Learning:** Un modelo de aprendizaje por refuerzo _offline_ que utiliza una matriz Q para aprender la mejor acción en cada estado, basándose en recompensas y castigos. Se ajusta mediante la ecuación de Bellman. Elije la mejor opcion para un conjunto de estado finitos, hace muchas  simulaciones, aprende cual  es la mejor opcion de un campo determinado.
		• Modelo offline que puede usarse para encontrar una política de selección de acciones óptima para cualquier proceso de decisión finito. 
		•Se basa en una exploración errática de las posibles acciones para aprender automáticamente a seleccionar las acciones que, en última instancia, deberían generar el mejor valor de utilidad para un problema dado. 
		•Ventajas: 
			- Es capaz de comparar la utilidad esperada de las acciones disponibles mediante simulaciones. 
			- Puede manejar problemas con transiciones estocásticas y recompensas, sin requerir ninguna adaptación.
		![[Pasted image 20250626155930.png]]![[Pasted image 20250626160104.png]]
- ![[Pasted image 20250626160133.png]]
![[Pasted image 20250626160356.png]]



- 



    - **DQN (Deep Q-Network):** Combina Q-Learning con redes neuronales profundas. La matriz Q se transforma en una red neuronal que estima el valor Q para cada acción. Se entrena generando datos a través de la interacción con el entorno.
    - **AlphaZero:** Basado en AlphaGo, combina un método de búsqueda Montecarlo con redes neuronales convolucionales. Aprende jugando contra sí mismo y prioriza caminos prometedores, logrando resultados superiores en juegos complejos como el Go.
    - **MuZero:** Una evolución de AlphaZero que elimina la necesidad de simular el entorno directamente, utilizando redes neuronales adicionales para modelar el entorno y predecir estados futuros.
    - **World Models:** Otro enfoque que utiliza _deep autoencoders_ y redes recurrentes para modelar el entorno y determinar acciones.
    - **Agentes LLM (Large Language Model):** Utilizan modelos de lenguaje grandes (LLM) como motor, interactuando con entornos virtuales pero reales (ej., Gmail, calendarios). Incorporan componentes de memoria, planificación (descomposición de tareas, auto-reflexión) y herramientas (_tools_) para interactuar con otros sistemas o agentes.
    



### **Tipos de Entornos de los Agentes**

Los entornos en los que operan los agentes inteligentes pueden clasificarse según varias características:

- **Totalmente Observable vs. Parcialmente Observable:**
    
    - **Totalmente Observable:** El agente puede percibir toda la situación del entorno en un momento dado. Ejemplo: un juego de ajedrez o Tatetí, donde todas las piezas y su posición son visibles.
    - **Parcialmente Observable:** El agente solo tiene acceso a una parte de la información del entorno. Ejemplo: un juego de póker, donde el agente conoce sus cartas y las cartas comunitarias, pero no las de los oponentes.
    
- **Determinista vs. Estocástico:**
    
    - **Determinista:** El entorno se comporta siempre de la misma manera; una acción en un estado dado siempre produce el mismo resultado. Ejemplo: un crucigrama.
    - **Estocástico:** El entorno incorpora el azar, lo que significa que la misma acción en el mismo estado puede producir resultados diferentes. Ejemplo: el mundo real, juegos de cartas.
    
- **Episódico vs. Secuencial:**
    
    - **Episódico:** Cada acción del agente y la observación resultante son independientes de las acciones y estados anteriores. El estado actual no depende de la historia.
    - **Secuencial:** El estado anterior puede influir en el estado actual, requiriendo que el agente tenga memoria de situaciones pasadas para tomar decisiones óptimas.
    
- **Estático vs. Dinámico:**
    
    - **Estático:** El entorno solo cambia cuando el agente realiza una acción. Ejemplo: un crucigrama.
    - **Dinámico:** El entorno sigue cambiando incluso si el agente no realiza ninguna acción, lo que añade complejidad al proceso de toma de decisiones del agente. Ejemplo: el mundo real.
    
- **Discreto vs. Continuo:**
    
    - **Discreto:** Los estados del entorno se pueden diferenciar fácilmente y son finitos. Ejemplo: el juego del mono con botones, donde los estados son específicos y limitados.
    - **Continuo:** El entorno tiene una cantidad infinita de estados posibles, y los cambios pueden ser muy sutiles. Ejemplo: el mundo real, donde las variaciones son constantes y graduales.



### Implementación de un Agente Inteligente: 
• Consiste en diseñar y desarrollar al agente que funcionará (sólo o con otros) dentro de un entorno de software ejecutado sobre algún hardware. 
• Dicho agente podrá resolver una serie de tareas mediante la aplicación de una serie de acciones. 
			→ CAPACIDADES DEL AGENTE 
• Para implementar un agente es posible descomponerlo en un conjunto de módulos o componentes que interactúan para proveer respuestas a las preguntas de cómo los datos de los sensores y el estado interno del agente determina sus acciones y también sus futuros estados internos. 
			→ ARQUITECTURA DEL AGENTE
• En general, se podria decir quue 
			AGENTE  = CAPACIDADES + ARQUITECTURA

### Agente Inteligente vs Sistema Inteligente: 
• Una Sistema Inteligente no tiene tanto "objetivos" sino que posee "reflejos". or ejemplo: Si recibe el texto "Hola, cómo" seguramente completará el texto con "estás?" 
• Un Agente Inteligente determina la mejor acción a aplicar de sus CAPACIDADES teniendo en cuenta las Observaciones recibidas buscando que se maximice el resultado en un Entorno determinado. 
Por ejemplo: juega O: jugada de tateti
Un agente tiene una capacidad mas, tiene cierta capacidad de razonamiento


### APRENDIZAJE POR REFUERZO 
- Sub-campo de Machine Learning que describe maneras en que un algoritmo que puede aprender a en actuar procesos de guiados solamente por recompensas y castigos. decisión desconocidos no especificados, guiados por recompensas y castigos
- Este aprendizaje refleja de cerca la intuición humana sobre mediante el condicionamiento y permite que los algoritmos dominen de otro modo serían difíciles o imposibles de especificar. aprendizaje sistemas que de otro modo serian difíciles o imposibles de especificar
				→ Aprendizaje Emocional

![[Pasted image 20250626154228.png]]
secuencial, es determinista, estatifico  , es observable por que se puede ver.
![[Pasted image 20250626154244.png]]
![[Pasted image 20250626154414.png]]
![[Pasted image 20250626154502.png]]
![[Pasted image 20250626154644.png]]
![[Pasted image 20250626154656.png]]
para implementar los agentes:
![[Pasted image 20250628004225.png]]
![[Pasted image 20250628004328.png]]
![[Pasted image 20250628004401.png]]
![[Pasted image 20250628004522.png]]
![[Pasted image 20250628004545.png]]la ecuacion de bellman paecida a los pesos de la RNA
![[Pasted image 20250628004831.png]]


### **Temas Clave para el Examen**

Para el examen, los temas principales a considerar son:

- **Q-Learning:**
    
    - Concepto y funcionamiento.
    - Uso de la matriz Q y la ecuación de Bellman.
    - Ventajas y limitaciones (ej., problemas con estados infinitos).
    
- **DQN (Deep Q-Network):**
    
    - Cómo combina Q-Learning con redes neuronales profundas.
    - Estructura básica de la red (capas de entrada y salida).
    - Proceso de entrenamiento y generación de datos.
    - Ventajas sobre Q-Learning tradicional.
    
- **AlphaZero:**
    
    - Concepto general y su relación con AlphaGo.
    - Combinación del método de búsqueda Montecarlo con redes neuronales convolucionales.
    - Filosofía de aprendizaje (jugar contra sí mismo).
    - Ventajas en juegos complejos y eficiencia computacional.
    
- **Conceptos Generales de Agentes Inteligentes:**
    
    - Definición de agente inteligente y su diferencia con sistemas inteligentes.
    - Relación entre agente, entorno, observaciones, acciones y recompensas.
    - Importancia del aprendizaje por refuerzo (recompensas y castigos).
    
- **Tipos de Entornos:**
    
    - Comprender las características de los entornos (observable/parcialmente observable, determinista/estocástico, episódico/secuencial, estático/dinámico, discreto/continuo) y cómo afectan el diseño del agente.
    

**Nota:** Los modelos más avanzados como MuZero, World Models y los agentes LLM, aunque mencionados, no serán evaluados en detalle en el examen. El enfoque estará en Q-Learning, DQN y AlphaZero, así como en los conceptos fundamentales de los agentes inteligentes y sus entornos.