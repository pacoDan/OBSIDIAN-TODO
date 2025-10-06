Claro, aquí tienes una estructura detallada de la transcripción, recopilando las preguntas y respuestas clave para exámenes, las lecciones aprendidas y un análisis específico de las tres preguntas que te interesan, todo basado en las fuentes proporcionadas.

Estructura de la Transcripción y Temas Clave

La sesión se divide en dos partes principales:

1. **Discusión sobre el Trabajo Práctico (TP) Final**: Se abordan dudas de los estudiantes sobre la última entrega del TP, enfocándose en la presentación de un proyecto de inversión a posibles inversores. Los temas clave incluyen:

    ◦ **Financiamiento del proyecto**: Cómo obtener fondos, ya sea a través de préstamos bancarios, capital de inversores o autofinanciamiento. Se destaca la importancia de presentar una estrategia financiera realista y transparente.

    ◦ **Flujo de Caja y Capital de Trabajo**: Se explica cómo determinar la inversión inicial (C0) y cómo manejar el capital de trabajo.

    ◦ **Desarrollo de Software/Apps**: Se discute que para buscar inversión, es necesario presentar algo tangible, como una demo o un prototipo, no solo una idea.

    ◦ **Proyección de la Demanda**: Se advierte sobre hacer proyecciones de mercado poco realistas, como capturar un 70% del mercado en dos años con un producto nuevo.

2. **Análisis de Sensibilización y Resolución de Ejercicio**: Se explica el concepto de análisis de sensibilización utilizando un ejercicio práctico (Flamingo) como ejemplo. El objetivo es entender cómo varía el Valor Actual Neto (VAN) del proyecto al modificar variables clave como el precio, la cantidad vendida o los costos.

    ◦ **Uso de Herramientas (Excel/Google Sheets)**: Se detalla el uso de la función "Buscar Objetivo" (Goal Seek) para realizar el análisis de forma automática.

    ◦ **Conceptos del Ejercicio**: Se aclaran dudas sobre el capital de trabajo, la depreciación de terrenos (no se deprecian), y la recuperación del capital de trabajo.

Preguntas y Respuestas para Exámenes

Aquí se recopilan las dudas y aclaraciones más importantes que podrían aparecer en un examen:

|   |   |
|---|---|
|**Pregunta**|**Respuesta Detallada**|
|**¿Cómo se determina la inversión inicial mínima (C0) en un flujo de fondos?**|El valor de C0 representa la inversión mínima necesaria para iniciar el proyecto. Si C0 y los primeros flujos (ej. C1) son negativos, se deberá conseguir financiamiento para cubrir ambos.|
|**¿Los terrenos se deprecian?**|**No, los terrenos no se deprecian** para fines de esta materia. Incluir su depreciación en los cálculos es un error.|
|**¿Qué significa "valor de salvamento" o "valor de rezago"?**|Son términos antiguos que significan **"valor de venta"** al final del proyecto. Si se proporciona este valor, se debe registrar la venta del activo.|
|**¿El capital de trabajo se recupera siempre al 100%?**|Si el enunciado no especifica lo contrario, se asume que **se recupera el 100%**. Sin embargo, podría haber casos donde se indique un porcentaje menor de recuperación, por ejemplo, debido a sobre stock que no se pudo vender.|
|**¿Qué hacer si la capacidad de producción es menor a la demanda proyectada?**|Se deben analizar dos escenarios con flujos de caja separados: 1) comprar la nueva maquinaria para cubrir la demanda y 2) no comprarla y perder esas ventas. Se elige el escenario con el VAN más alto. El precio de la máquina se considera en el momento de la necesidad, no se puede proyectar a futuro.|
|**¿Qué es una "desinversión" de un activo?**|Es el acto de dar de baja una parte del activo, lo que equivale a una **venta a valor cero** por esa porción. Contablemente, se debe registrar la pérdida del valor libro de esa parte como un egreso afecto a impuestos en el año de la desinversión.|
|**¿Cómo se tratan los activos "viejos" o preexistentes que se usan en un nuevo proyecto?**|No se registra su compra (es un "costo hundido"), pero sí **se debe registrar su depreciación** durante el proyecto, ya que su uso genera un desgaste.|
|**Si el enunciado dice "estar indiferente" entre ejecutar o no el proyecto, ¿qué significa?**|Significa que el **Valor Actual Neto (VAN) debe ser igual a cero**.|

Análisis Detallado de las Preguntas de Sensibilización

Para responder a estas preguntas, se utiliza el **análisis de sensibilización**, específicamente la herramienta "Buscar Objetivo" de Excel. El método consiste en definir la celda del VAN como objetivo con un valor de cero y cambiar una celda variable (precio, cantidad o costo) para encontrar el punto de equilibrio.

**1. ¿Cuál es el precio de equilibrio de largo plazo?**

• **Concepto**: Se busca el precio de venta que hace que el VAN del proyecto sea cero a lo largo de todo el horizonte de evaluación (en este caso, 3 años).

• **Método de Cálculo**:

    1. Se utiliza la herramienta "Buscar Objetivo" en Excel.

    2. Se define la celda del **VAN** para que sea igual a **0**.

    3. Se selecciona la celda del **precio del primer año (Año 1)** como la variable a cambiar.

    4. **Es crucial que los precios de los años siguientes (Año 2, Año 3) estén vinculados al precio del primer año** (por ejemplo, con un porcentaje de incremento), para que al cambiar el primero, todos varíen proporcionalmente.

• **Respuesta**: El resultado será el precio mínimo para el Año 1 que asegura que el proyecto no genere pérdidas. Los precios de los años siguientes se ajustarán automáticamente según la relación definida. La respuesta sería, por ejemplo: "El precio de equilibrio es de $X para el primer año".

**2. ¿Cuál es la cantidad mínima vendida anual para estar indiferente entre ejecutar o no el proyecto?**

• **Concepto**: Se busca determinar las unidades mínimas que se deben vender cada año para que el VAN sea cero.

• **Método de Cálculo**:

    1. El proceso es idéntico al anterior, usando "Buscar Objetivo".

    2. Se define la celda del **VAN = 0**.

    3. La celda a cambiar es la **cantidad de unidades vendidas en el Año 1**.

    4. Al igual que con el precio, las cantidades de los años posteriores deben estar vinculadas proporcionalmente a las del primer año para mantener la tendencia de la demanda proyectada.

• **Respuesta**: La herramienta calculará la cantidad necesaria para el Año 1, y las cantidades para los años 2 y 3 se derivarán de esa. La respuesta se presenta año por año: "La cantidad mínima anual es X unidades para el Año 1, Y para el Año 2, y Z para el Año 3".

**3. ¿Cuál es el costo máximo por unidad producida que podría alcanzar los saborizantes?**

• **Concepto**: Se busca el costo unitario máximo del insumo "saborizantes" que el proyecto puede soportar antes de que el VAN se vuelva negativo (es decir, VAN = 0).

• **Método de Cálculo**:

    1. Nuevamente, se utiliza "Buscar Objetivo".

    2. Se establece **VAN = 0**.

    3. La celda a cambiar es la que contiene el **costo unitario del saborizante** (en el ejemplo, la celda C6).

    4. Si el costo del saborizante es el mismo para todos los años, el análisis es directo. Si variara, habría que vincular los costos para que el análisis sea consistente.

• **Respuesta**: El resultado será el costo máximo que puede tener el saborizante. Si el costo real supera este valor, el proyecto dejará de ser rentable. La respuesta es un valor único si el costo no varía: "El costo máximo que pueden alcanzar los saborizantes es de $X por unidad".

Lecciones Aprendidas y Consejos Clave

• **Presentación a Inversores**: Un proyecto de inversión debe ser presentado como un informe comercial sólido y transparente. No se puede ocultar información.

• **Realismo en las Proyecciones**: Las proyecciones de demanda y financiamiento deben ser creíbles y estar basadas en la realidad del mercado. No es realista esperar obtener un préstamo millonario para una empresa nueva sin garantías o capturar una porción masiva del mercado rápidamente.

• **Tangibilidad de la Propuesta**: Los inversores quieren ver algo tangible, no solo una idea. Para proyectos de software, esto significa tener una demo, un prototipo o al menos un diseño funcional (mockups).

• **Análisis de Sensibilización**: Es una herramienta clave para entender los límites y riesgos de un proyecto. Permite definir "márgenes de seguridad" para variables críticas como precios, costos y demanda.

• **Organización en Exámenes**: Para los puntos que requieren análisis de sensibilización, se recomienda **crear una copia de la hoja de cálculo original** para cada variable analizada. Esto evita errores y deja claro el procedimiento de resolución. La prolijidad y claridad en la presentación de los cálculos es fundamental para la corrección.


---

**Preguntas y Respuestas de Examen**

Durante la clase, se mencionaron explícitamente algunas preguntas conceptuales que podrían aparecer en un examen. Aquí están recopiladas:

1. **Pregunta:** **¿Qué imaginan o por qué imaginan que tenemos que sensibilizar los flujos de fondos?**

    ◦ **Respuesta:** La sensibilización se realiza para **generar distintos escenarios** (pesimista, optimista, realista) que permitan analizar cómo se comporta el proyecto de inversión ante impactos de riesgo. Ayuda a identificar qué amenazas pueden afectar al proyecto (ej. una baja en las ventas) y proporciona más datos para tomar mejores decisiones. Si un proyecto tiene un Valor Actual Neto (VAN) positivo pero muy cercano a cero, una pequeña variación en una variable clave podría volverlo no rentable (VAN < 0).

2. **Pregunta:** **¿Qué es sensibilizar?**

    ◦ **Respuesta:** Es el proceso de **cambiar una o más variables clave** ("un poquito más, un poquito menos") para observar cómo impactan en el resultado final del proyecto, como el VAN.

3. **Pregunta:** **¿Cuál es la diferencia entre riesgo e incertidumbre?**

    ◦ **Respuesta:**

        ▪ **Riesgo:** Existe cuando se puede predecir el comportamiento de una variable, ya que se conoce o se puede asimilar a una función de distribución de probabilidad (como la de Poisson, triangular o beta simplificada). Esto permite estimar un valor medio y una dispersión. Un riesgo es un evento posible que, si se materializa, suele tener resultados negativos, aunque también pueden ser oportunidades.

        ▪ **Incertidumbre:** Ocurre cuando se conoce un posible evento futuro, pero **no se conoce el comportamiento de la variable ni las probabilidades de suceso asociadas**. No hay una función de distribución conocida.

4. **Pregunta (de una fuente complementaria):** **¿El mantenimiento de máquina y lubricantes están incluidos en los costos de producción?**

    ◦ **Respuesta:** **Sí, son costos de producción**. Sin embargo, se consideran **costos indirectos** si se utilizan en varias líneas de productos o procesos, ya que no se pueden asignar directamente a un producto específico.

5. **Pregunta (de una fuente complementaria):** **¿La computadora de una empresa de software es un costo?**

    ◦ **Respuesta:** **No, la computadora es una inversión en un activo fijo**, que forma parte de la capacidad máxima instalada de la empresa. El costo asociado sería el consumo de energía eléctrica o la mano de obra que la utiliza.

**Recomendaciones y Buenas Prácticas**

A lo largo de la clase, se dieron varios consejos clave para realizar la sensibilización y estructurar el análisis financiero en el ejercicio.

• **Aislar las Variables Clave:** Es una recomendación importante colocar las variables principales (como precios, costos, unidades) en la parte superior del flujo de caja en Excel. Esto facilita enormemente el proceso de sensibilización, ya que se pueden referenciar directamente.

• **Referenciar Celdas en Fórmulas:** En lugar de escribir valores fijos (hard-coding) en el flujo de fondos (ej. 110 y 120 para los precios de los años 2 y 3), se deben referenciar a la celda del valor inicial (ej. el precio del año 1 multiplicado por un factor de crecimiento). Esto permite que la herramienta de sensibilización (como "Buscar Objetivo") ajuste todos los años de manera proporcional y correcta.

• **Utilizar Herramientas de Excel para Sensibilizar:**

    ◦ **Análisis Unidimensional ("Buscar Objetivo"):** Es ideal para responder preguntas como "¿cuál es el precio mínimo que hace el VAN=0?". Se define una celda objetivo (el VAN), se le asigna un valor (ej. 0) y se selecciona la celda de la variable a cambiar (ej. precio, cantidad o un costo específico).

    ◦ **Análisis Bidimensional ("Tabla de Datos"):** Es útil para analizar el impacto simultáneo de dos variables sobre el VAN (ej. precio vs. costo del saborizante). Permite visualizar en una matriz en qué combinaciones de valores el proyecto sigue siendo rentable.

• **Fundamentar Decisiones con Datos:** El objetivo de la sensibilización es obtener datos argumentativos para defender la viabilidad de un proyecto ante inversores o directivos. Por ejemplo, demostrar que el proyecto soporta una caída del precio hasta un cierto valor o que requiere vender una cantidad mínima de unidades para ser rentable.

• **Entender el Equilibrio a Largo Plazo:** En la evaluación de proyectos, el "punto de equilibrio a largo plazo" se alcanza cuando el **VAN es igual a cero**. Este es el punto donde el proyecto es indiferente, ya que cubre la inversión y el costo de oportunidad, pero no genera valor adicional.

• **Capital de Trabajo Dinámico:** El capital de trabajo debe estar correctamente vinculado a las variables que lo afectan (como costos variables o cantidad de unidades). Si al sensibilizar una de estas variables esta cambia, el capital de trabajo también debería ajustarse, lo cual es una práctica más precisa.

**Qué NO Hacer (Errores a Evitar)**

• **NO Escribir Valores Fijos (Hard-Coding):** Evita introducir números directamente en las celdas del flujo de fondos. Si no referencias las variables, la sensibilización solo afectará al primer año o al valor específico que modifiques, llevando a resultados incorrectos.

• **NO Olvidar el Valor de Recupero de Activos:** Al finalizar el horizonte de evaluación de un proyecto, se deben "desactivar" los activos. Si un activo como un terreno tiene un valor de recupero, este debe incluirse en el último año del flujo de fondos. Omitirlo puede hacer que el VAN sea incorrectamente bajo o incluso negativo.

• **NO Confundir Depreciación con Valor de Activo:** Un terreno no se deprecia, por lo tanto, su valor libro al final del proyecto es igual a su valor de origen, a menos que su valor de mercado haya cambiado.

• **NO Limitar el Análisis a una Sola Variable si hay Múltiples Riesgos:** Si un proyecto tiene varios costos significativos o variables de riesgo, un análisis unidimensional es insuficiente. En ese caso, lo correcto sería utilizar un análisis multidimensional como el método de Montecarlo.




PARA EL PROX VIERNES:

• **Conceptos generales de evaluación de inversión:** Se revisarán ideas fundamentales sobre proyectos de inversión, como la diferencia entre un proyecto incremental y uno no incremental.

• **Popurrí de temas en el pizarrón:** El profesor mencionó su preferencia por enseñar en el pizarrón y que aprovecharán la clase para hacer un repaso variado de conceptos clave.

• **Resolución de ejercicios (o partes de ejercicios):** Se abordarán ejercicios para aplicar la teoría, enfocándose en los aspectos que presenten mayor dificultad o sean distintos a lo visto hasta ahora. Un tema específico que se mencionó es:

    ◦ **Estimación de la demanda:** Se analizará cómo construir un polinomio para estimar la demanda en función de múltiples variables, como la población económicamente activa o la inversión en marketing.

• **Revisión del capital de trabajo:** Se repasará la lógica detrás del cálculo y la importancia del capital de trabajo, posiblemente utilizando como ejemplo un ejercicio tomado en un examen final reciente