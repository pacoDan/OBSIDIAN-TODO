Estructura bien esta transcripción, recopila todas las preguntas y respuestas para exámenes, las lecciones aprendidas,  no olvides cada detalle de esta transcripción en base a las preguntas, y ten mas en cuenta sobre: 
ANÁLISIS DE SENSIBILIDAD • MODIFICACIONES SOBRE - COEFICIENTES DE EFICIENCIA (g) - TÉRMINOS INDEPENDIENTES (b;) • AGREGADO DE - NUEVOS PRODUCTOS - NUEVAS RESTRICCIONES • RANGOS DE VALIDEZ DE LA SOLUCIÓN ÓPTIMA - DIRECTA - DUAL

los casos de sensibilidad, lo que representa cada variable


### 1. Conceptos Fundamentales y Representación de Variables

El **análisis de sensibilidad** (o análisis post-optimal) estudia cómo cambian los resultados de un modelo de programación lineal ante variaciones en sus parámetros, sin necesidad de resolver el problema desde el principio.

**¿Qué representan las variables?**

- **$x_j$ (Variables de decisión/Reales):** Representan actividades, productos o servicios que la empresa decide elaborar (ej. unidades de producto A o B).
- **$c_j$ (Coeficientes de eficiencia):** Son los beneficios unitarios (o costos) asociados a cada variable en la función objetivo.
- **$b_i$ (Términos independientes/Right Hand Side):** Representan la disponibilidad limitada de recursos (ej. segundos de tiempo de soldado o pintado).
- **$y_i$ (Variables duales/Valores marginales):** Indican cuánto mejora la función objetivo por cada unidad adicional que se relaje de una restricción agotada.
- **$z_j$ (Costo marginal de un producto):** Representa la valorización de los recursos necesarios para elaborar una unidad de un nuevo producto, calculada mediante el producto de los coeficientes tecnológicos por los valores marginales.
- **$z_j - c_j$ (Costo de oportunidad):** En problemas de maximización, si es positivo para una variable no básica, indica cuánto disminuiría el beneficio si decidiéramos fabricar una unidad de ese producto.

---

### 2. Casos de Análisis de Sensibilidad

#### **A. Modificaciones sobre Coeficientes de Eficiencia ($c_j$)**

- **Ubicación:** Se analiza sobre la **tabla óptima del directo**.
- **Efecto Gráfico:** Modifica la **pendiente** de la recta del funcional, haciéndola girar (pivotear) sobre el punto óptimo.
- **Criterio Simplex:** La solución actual sigue siendo óptima mientras los nuevos $z_j - c_j$ sigan siendo no negativos (en maximización) o no positivos (en minimización).
- **Resultado:** Si el cambio es muy grande, aparece un $z_j - c_j$ con signo opuesto, lo que obliga a iterar para encontrar una nueva estructura de solución (un nuevo vértice).

#### **B. Modificaciones sobre Términos Independientes ($b_i$)**

- **Ubicación:** Se analiza sobre la **tabla óptima del dual**.
- **Efecto Gráfico:** Consiste en **trasladar paralelamente** la recta de la restricción. Si se relaja una restricción saturada, el polígono se expande y el funcional mejora según el valor marginal.
- **Vínculo con el Dual:** Cambiar un $b_i$ en el directo equivale a cambiar un $c_j$ en el dual.
- **Resultado:** Si el recurso empieza a sobrar, su valor marginal cae a cero y la solución puede volverse degenerada en el directo (lo que implica soluciones alternativas en el dual).

#### **C. Agregado de Nuevos Productos**

- **Ubicación:** Tabla óptima del **directo**.
- **Procedimiento de Evaluación:**
    1. Calcular el **costo marginal** ($z_j$) multiplicando los coeficientes tecnológicos del nuevo producto por los valores marginales de los recursos actuales.
    2. Comparar $z_j$ con el beneficio unitario ($c_j$).
    3. **Regla de decisión:** Si $c_j > z_j$ (el beneficio supera el costo de los recursos), el producto **conviene** y se debe introducir en la base.
- **Transformación:** Para incluirlo en la tabla óptima, se debe multiplicar el vector original del producto por la **matriz inversa** (ubicada bajo la identidad en la tabla inicial).

#### **D. Agregado de Nuevas Restricciones**

- **Ubicación:** Tabla óptima del **dual**.
- **Procedimiento de Evaluación:**
    1. Verificar si la solución óptima actual satisface la nueva restricción.
    2. Si la satisface, es **no limitativa** y nada cambia.
    3. Si no la satisface, es **limitativa** (el óptimo queda fuera), el funcional empeorará y se debe agregar la fila a la tabla dual para iterar.

---

### 3. Rangos de Validez de la Solución Óptima

El objetivo es hallar el límite superior e inferior dentro de los cuales un parámetro puede variar sin que cambie la **estructura** de la solución (las variables que están en la base).

- **Rango de $c_j$ (Directo):** Se busca el valor que genere un **cero asterisco** en los $z_j - c_j$, lo que marca la aparición de soluciones alternativas.
    - _Ayuda nemotécnica (Maximización):_ Para el límite superior se busca un coeficiente negativo en la fila; para el inferior, uno positivo.
- **Rango de $b_i$ (Dual):** Se analiza en la tabla dual.
    - Si un recurso **sobra**, su límite superior es **infinito** (puede sobrar más y nada cambia) y su límite inferior es la disponibilidad actual menos el sobrante.
    - Si un recurso está **agotado**, se calculan los límites de forma análoga a los $c_j$, buscando el cociente mínimo cuando hay varios candidatos para evitar que la solución cambie antes de tiempo.

---

### 4. Recopilación de Preguntas y Respuestas para Exámenes

**P1: ¿Para qué sirve el planteo Dual en la práctica?**

- **R:** Facilita el análisis de sensibilidad de los términos independientes ($b_i$) y el agregado de nuevas restricciones, ya que estos se comportan como coeficientes del funcional en el dual.

**P2: ¿Cómo se sabe mediante el Simplex si un cambio de coeficiente funcional ($c_j$) altera el óptimo?**

- **R:** Se recalculan los $z_j - c_j$. Si alguno cambia de signo (ej. se vuelve negativo en un problema de maximización), la tabla actual deja de ser óptima y se debe iterar.

**P3: ¿Qué representa un valor marginal igual a cero?**

- **R:** Significa que el recurso asociado es **sobrante** (no saturado). Tener más de ese recurso no mejora el beneficio total porque ya hay exceso.

**P4: ¿Cuál es el beneficio mínimo necesario para fabricar un nuevo producto?**

- **R:** El beneficio unitario debe ser al menos igual a su **costo marginal** ($z_j$). En ese punto, el $z_j - c_j$ es cero (solución alternativa) y es indiferente producirlo o no.

**P5: En el agregado de una restricción, ¿qué ocurre si el óptimo actual no la cumple?**

- **R:** La restricción es **limitativa**. Se debe transformar el vector mediante la matriz inversa del dual, añadir la fila y realizar una iteración; el valor del funcional inevitablemente disminuirá o se mantendrá igual, pero nunca mejorará.

**P6: ¿Cómo se obtiene el transformado de un vector para la tabla óptima?**

- **R:** Multiplicando el vector de la tabla inicial por la **matriz inversa** que se encuentra en la tabla óptima.

---

### 5. Lecciones Aprendidas

1. **Visión de Ingeniero:** Antes de hacer cálculos complejos (como transformar vectores con matrices inversas), siempre se debe realizar la **verificación lógica** de si el cambio realmente afecta (ej. ver si el producto conviene o si la restricción es limitativa).
2. **Relación entre Modelos:** Existe un "hilo conductor" donde todo está relacionado: un cambio en un recurso en el directo impacta los valores del dual, y viceversa.
3. **Simulación de Escenarios:** Los modelos reales no se resuelven una vez; se usan para simular situaciones ("¿Qué pasa si...?") frecuentes en la toma de decisiones empresariales.
4. **Precisión en la Matriz Inversa:** Al trabajar con el dual, hay que tener extremo cuidado con los **signos** de la matriz inversa, especialmente cuando provienen de restricciones de tipo "mayor o igual" que generan variables artificiales.
