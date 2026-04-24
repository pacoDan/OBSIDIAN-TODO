
acá no hay operadores de selección y cruzamiento
### Resumen General de la Transcripción

La transcripción aborda los algoritmos de inteligencia de enjambre, que emulan el comportamiento colectivo de seres vivos para resolver problemas de búsqueda y optimización. Se presentan tres algoritmos principales: bandada de pájaros (Particle Swarm Optimization - PSO), colonia de abejas y colonia de hormigas. Además, se introducen dos algoritmos híbridos: el clonal G (basado en el sistema inmunológico) y el memético (basado en la teoría del meme), que combinan ideas de computación evolutiva con inteligencia de enjambre. Se explica el funcionamiento, aplicaciones y consideraciones prácticas de cada algoritmo, incluyendo ejemplos en Colab.

INTELIGENCIA DE ENJAMBRE
"Sistema Computacional que permite resolver problemas de búsqueda y
optimización. Se encuentra basado en la 'inteligencia colectiva' la cual
emerge por la cooperación de gran cantidad de agentes homogéneos en
un ambiente determinado."

hay muchos algoritmos de inteligencia de enjambre:
Tipos:
• Bandada de Pájaros
• Colmena de Abejas
• Colonia de Hormigas
• Colonia de Bacterias
• Manada de Lobos
• Cardumen de Peces
• Colonia de Murciélagos
• Colmena de Avispas
• Fluido de Líquidos
• Ley de la Gravedad y mas algoritmos


![[Pasted image 20250706222931.png]]
al final se queda con la mejor parte
![[Pasted image 20250706223121.png]]
![[Pasted image 20250706223345.png]]
https://youtu.be/jHwT5zOIPZc?t=1810
aplicación:
![[Pasted image 20250708135536.png]]
### Ventajas y Desventajas de los Algoritmos de Inteligencia Artificial
**Ventajas:**
- ==**Algoritmo de Bandada de Pájaros (PSO):**==
    - **Simplicidad:** Relativamente fácil de entender e implementar.
    - **Eficiencia:** Rápido en la ejecución de ciclos, incluso para un gran número de iteraciones.
    - **Versatilidad:** Puede usarse para maximizar o minimizar problemas de optimización combinatoria. Lo que cambia es la interpretación de la solución 
https://youtu.be/jHwT5zOIPZc?t=759
![[Pasted image 20250706204631.png]]
    - **Exploración:** Permite que las partículas evalúen distintas posiciones de forma pseudoaleatoria, evitando búsquedas exhaustivas.
    - **Adaptabilidad:** Puede ==soportar múltiples dimensiones== en el espacio de búsqueda sin grandes cambios.
    
- ==**Algoritmo de Colonia de Abejas o basado en abejas:**==

    ![[Pasted image 20250708135628.png]]
    ![[Pasted image 20250708135706.png]]
    luego een las mejores areas:
    ![[Pasted image 20250708135732.png]]
    ![[Pasted image 20250708135801.png]]
    ![[Pasted image 20250708135958.png]]
    ![[Pasted image 20250708140058.png]]
    ![[Pasted image 20250708140112.png]]
    ![[Pasted image 20250708140154.png]]
    
	 - **Confiabilidad:** Tiende a converger más rápido y encontrar soluciones óptimas con menos ciclos que PSO.
    - **Robustez:** ==Más adecuado para problemas con funciones heurísticas complejas==.
    - **Exploración y Explotación:** Combina la búsqueda de nuevas áreas (abejas exploradoras) con la explotación de áreas prometedoras (abejas obreras).
    
- ==**Algoritmo de Colonia de Hormigas:**==
    ![[Pasted image 20250708151910.png]]
    ![[Pasted image 20250708151937.png]]
    ![[Pasted image 20250708152026.png]]
example de mejor camino de conmutación de enlaces en redes:
![[Pasted image 20250708152052.png]]
arbol de busqueda (si abria mas nodos y rutas)
![[Pasted image 20250708152206.png]]
![[Pasted image 20250708152248.png]]
![[Pasted image 20250708152302.png]]
![[Pasted image 20250708152317.png]]
evaporacion de feromonas:
![[Pasted image 20250708152619.png]]
![[Pasted image 20250708153603.png]]
nos quedamos con el mejor de los mejore caminos (suele ser de la mejor feromonas):
![[Pasted image 20250708153649.png]]
![[Pasted image 20250708153716.png]]
![[Pasted image 20250708160622.png]]
![[Pasted image 20250708160639.png]]
![[Pasted image 20250708160701.png]]
    - **Optimización de Rutas:** Muy orientado a encontrar la mejor ruta entre un origen y un destino.
    - **Consideración de Costos y Heurísticas:** Puede incorporar el costo de los caminos y la heurística de los nodos para encontrar soluciones más útiles.
    - **Aplicaciones Diversas:** Útil en navegación de vehículos, envío de paquetes, enrutamiento de redes y problemas del viajero.
    - **Adaptabilidad a la Información del Dominio:** Funciona mejor con información del dominio, pero puede operar sin ella.
    
- **Algoritmo Clonal G:**
    se usa para diagnosticar reconocimiento de patrones
    - **Convergencia:** La heurística tiende a aumentar o mantenerse igual, nunca empeora, garantizando que la población final contenga los mejores resultados.
    - **Optimización Multimodal:** Capaz de encontrar múltiples soluciones óptimas o satisfactorias en una misma corrida.
    - **Reconocimiento de Patrones:** Aplicable a problemas de clasificación y reconocimiento, como la identificación de spam.
    - **Hipermutación Inteligente:** La mutación se adapta al valor heurístico del individuo, haciendo pequeños cambios a los buenos y grandes a los malos.
    
- **Algoritmo Memético:** en la memetica
    evoluciond eee una cultura de una sociedad, y como se transmiten esas ideas, y como es ideas se transmiten , como tienden a evolucionar y prosperar
    ![[Pasted image 20250708161701.png]]
    parecido al AG
    ![[Pasted image 20250708161814.png]]
    ![[Pasted image 20250708161844.png]]
    ![[Pasted image 20250708161900.png]]
    ![[Pasted image 20250708163609.png]]
    ![[Pasted image 20250708163721.png]]
    
    - **Mejora Continua:** El operador de optimización garantiza que los individuos resultantes sean iguales o mejores que los originales, nunca peores.
    - **Combinación de Estrategias:** ==Permite integrar otros algoritmos de optimización (como PSO, abejas, genéticos, etc.) para mejorar los resultados del cruzamiento. Se puede meteer ideas de investighacion operativa==
    - **Robustez:** Tiende a dar buenos resultados y a mejorar la aptitud de la población a lo largo de las corridas.
    

**Desventajas:**

- **Algoritmo de Bandada de Pájaros (PSO):**
    
    - **Dependencia del Azar:** Puede requerir un gran número de ciclos para encontrar la solución óptima debido a su naturaleza pseudoaleatoria, lo que puede llevar a resultados inconsistentes entre corridas.
    - **Riesgo de Máximos Locales:** Puede quedar "atrapado" en máximos locales, impidiendo encontrar el máximo óptimo global.
    - **No Adecuado para Espacios Pequeños:** Para espacios de búsqueda muy pequeños (ej. 1000 posiciones), una búsqueda exhaustiva puede ser más eficiente.
    
- **Algoritmo de Colonia de Abejas:**
    
    - **Complejidad de Implementación:** Es más complejo de implementar que el algoritmo de bandada de pájaros debido a la gestión de abejas exploradoras y obreras, y la reducción de áreas.
    - **No Garantiza la Mejor Solución:** Aunque más confiable, no garantiza encontrar la mejor solución en todas las corridas.
    
- **Algoritmo de Colonia de Hormigas:**
    
    - **Orientación Específica:** Principalmente diseñado para problemas de búsqueda de rutas; aunque existen variaciones para optimización, no es su aplicación principal.
    - **Complejidad de Implementación:** Más complicado que PSO debido a los cálculos de probabilidad y la gestión de feromonas.
    - **Sensibilidad a Parámetros:** El rendimiento puede depender de la correcta configuración de coeficientes (alfa, beta) y el factor de evaporación.
    - **Limitación de Pasos:** Requiere una cantidad máxima de pasos para evitar que las hormigas tarden demasiado en encontrar la solución.
    
- **Algoritmo Clonal G:**
    
    - **No Garantiza la Mejor Solución:** Aunque tiende a mejorar, no siempre garantiza encontrar la solución óptima en una sola corrida.
    
- **Algoritmo Memético:**
    
    - **Dependencia del Algoritmo de Optimización Interno:** La calidad de los resultados depende en gran medida del algoritmo de optimización elegido para el operador de "mutación".
    - **Mayor Complejidad:** Al combinar un algoritmo genético con otro algoritmo de optimización, la implementación puede ser más compleja.
    


algoritmos hibridos
![[Pasted image 20250708160812.png]]
![[Pasted image 20250708160831.png]]
![[Pasted image 20250708160855.png]]
![[Pasted image 20250708160931.png]]
cantiad de individuos: anticuerpos
![[Pasted image 20250708160955.png]]
generamos una copia
![[Pasted image 20250708161022.png]]
tomamos en cuenta el valor heurístico:
![[Pasted image 20250708161050.png]]
![[Pasted image 20250708161128.png]]
![[Pasted image 20250708161153.png]]
aca en la poblacion final tengo los mejores rsultados
![[Pasted image 20250708161223.png]]



### Preguntas y Respuestas en la Transcripción

- **¿Qué son los algoritmos de inteligencia de enjambre?**
    
    - Sirven para resolver problemas de búsqueda y optimización, basándose en el concepto de inteligencia colectiva de un conjunto de elementos homogéneos (agentes). Buscan emular el comportamiento de seres vivos en la naturaleza, especialmente al buscar alimento.
    
- **¿Cuáles son los tres algoritmos principales de inteligencia de enjambre?**
    
    - Bandada de pájaros (Particle Swarm Optimization - PSO), colonia de abejas y colonia de hormigas.
    
- **¿Para qué se utiliza el algoritmo de bandada de pájaros (PSO)?**
    
    - Principalmente para resolver problemas de optimización combinatoria.
    
- **¿Qué es una función heurística en el contexto de PSO?**
    
    - Es una función que indica qué tan buena es una posición dentro del espacio de búsqueda, similar a la función de aptitud en algoritmos genéticos.
    
- **¿Se puede usar PSO para maximizar o minimizar?**
    
    - Es indistinto; se puede usar para ambos, cambiando solo la interpretación de la "mejor" solución.
    
- **¿Es necesario saber de memoria los pasos de un algoritmo?**
    
    - No es imprescindible. Lo importante es saber para qué sirve, cómo conviene aplicarlo, y cuáles son sus beneficios y puntos débiles.
    
- **¿Cuál es el criterio de paro común para PSO?**
    
    - Generalmente, una cantidad de ciclos, pero también puede ser cuando se encuentra una solución con un valor heurístico superior a un umbral definido.
    
- **¿Cuándo no conviene usar algoritmos de enjambre o computación evolutiva?**
    
    - Cuando el espacio de búsqueda es muy pequeño (ej. 1000 posiciones), ya que una búsqueda exhaustiva puede ser más rápida.
    
- **¿Qué tipos de abejas existen en el algoritmo de colonia de abejas?**
    
    - Abejas exploradoras y abejas obreras.
    
- **¿Para qué se utiliza el algoritmo de colonia de hormigas?**
    
    - Está más orientado a problemas de búsqueda, específicamente para encontrar la mejor ruta desde un origen a un destino.
    
- **¿Qué es el Antnet?**
    
    - Un protocolo que implementa el algoritmo de hormigas en redes para encontrar el mejor camino de comunicación para enviar paquetes.
    
- **¿Cómo se actualiza la cantidad de feromonas en el algoritmo de hormigas?**
    
    - Mediante dos procesos: evaporación (disminución general) y acumulación (aumento en los caminos más frecuentemente recorridos por las hormigas).
    
- **¿Qué son los algoritmos híbridos?**
    
    - Algoritmos que combinan ideas de inteligencia de enjambre con computación evolutiva, como los algoritmos inmunológicos y meméticos.
    
- **¿En qué se basa el algoritmo clonal G?**
    
    - En el sistema inmunológico humano adquirido, específicamente en la identificación de patógenos por comportamiento anormal.
    
- **¿Qué es la hipermutación en el algoritmo clonal G?**
    
    - Es una mutación que tiene en cuenta el valor heurístico de cada individuo (anticuerpo): cuanto mejor es el valor, menos se muta; cuanto peor, más se muta.
    
- **¿Qué tipo de problemas puede resolver el algoritmo clonal G?**
    
    - Problemas de optimización multimodales (con múltiples soluciones óptimas) y reconocimiento de patrones.
    
- **¿En qué se basa el algoritmo memético?**
    
    - En la teoría del meme de Dawkins, que representa la evolución de ideas y la cultura de una sociedad.
    
- **¿Cuál es la diferencia principal del algoritmo memético con un algoritmo genético tradicional?**
    
    - En lugar de un operador de mutación, utiliza un operador de optimización que aplica otro algoritmo de optimización para mejorar los individuos.
    
- **¿El operador de optimización en el algoritmo memético puede empeorar un individuo?**
    
    - No, garantiza que el individuo resultante sea igual o mejor que el original.
    
- **¿Las preguntas del examen son conceptuales o prácticas?**
    
    - Son preguntas bastante conceptuales y abiertas, no requieren saber fórmulas de memoria ni ejercicios prácticos.