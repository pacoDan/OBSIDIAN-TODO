## I. Estructura de Preguntas y Respuestas Clave para Exámenes

### A. Preguntas sobre Flujos de Fondos (VAN, Incrementales y Criterios de Selección)

|Pregunta / Concepto|Respuesta Clave|Citas|
|:--|:--|:--|
|**Criterio de selección** entre dos proyectos.|Se elige el proyecto con el **VAN mayor**. Si ambos VAN son negativos, se elige el del VAN menos negativo (el mayor, ej. -100 sobre -200).||
|¿Qué son los **flujos incrementales**?|Es la diferencia entre la situación con proyecto y la situación sin proyecto. Siempre se debe evaluar la diferencia.||
|¿Es posible calcular el flujo de fondos uniendo dos escenarios?|Sí, se puede reflejar en uno solo, y el VAN resultante será la diferencia entre los VAN individuales de los dos proyectos.||
|¿Cómo afecta un **precio de producto similar** en dos alternativas si solo se proyecta un aumento (ej. 3% mensual) pero no se da el valor inicial?|Si el precio es igual para ambas alternativas, **no cambia el VAN**, por lo cual se puede descartar del cálculo.||
|**Condición** para asumir un precio en el cálculo.|El precio de venta debe ser **mayor al costo variable unitario más el costo fijo unitario** (para evitar operar a pérdida).||
|¿Cómo se calcula el VAN si es un **VAN de costos**?|No se puede pretender que dé mayor que cero, siempre dará **menor que cero**.||
|¿Cómo se debe tratar un **dato irrelevante** que no afecta al proyecto? (Ej. un gerente comprando algo personal).|Es un dato que se puede descartar, ya que no tiene que ver con el proyecto.||

### B. Preguntas sobre Inversión y Depreciación

|Pregunta / Concepto|Respuesta Clave|Citas|
|:--|:--|:--|
|¿Qué costos asociados a la **instalación** se incluyen en la inversión?|Todos los conceptos necesarios para la puesta en marcha se activan como inversión, incluyendo traslado, instalación, y **desinstalación** de la máquina anterior (si es necesaria para instalar la nueva).||
|¿Cómo se trata la **consultoría** necesaria para implementar un sistema (ERP, SAP)?|Si es necesaria para la implementación y activación del sistema, es parte de la inversión y luego se deprecia. La consultoría de **mantenimiento** es un gasto (OPEX).||
|Tratamiento del **Valor Libro (Valor Residual)** de un activo al final del proyecto.|Si el activo se vende, se debe calcular la ganancia o pérdida contable (Venta - Valor Libro). El Valor Libro se incluye como un **gasto no desembolsable** (ajustado posteriormente).||
|¿Qué hacer con el **Valor Libro restante** si la vida útil es mayor al horizonte de evaluación (Ej. máquina a 10 años evaluada a 5)?|Se debe calcular el valor de venta esperado (si se conoce) o, si no se conoce, el valor libre restante de depreciación (Valor Libro) debe ser **incluido como una pérdida** en el último año de evaluación.||
|¿Cómo se maneja una **reinversión** que ocurre al comienzo del Año 3?|Se debe registrar en el **Año 2** del flujo de fondos (al final de ese año) para aplicar el descuento apropiado (es un concepto financiero). Generalmente, se usa el **criterio más pesimista** si es ambiguo.||
|¿Cómo se trata el **costo de oportunidad** de un activo propio utilizado en el proyecto (Ej. un depósito no alquilado o una notebook)?|Se debe considerar un **costo de oportunidad** (como si se estuviera pagando un alquiler o sueldo) para reflejar la realidad económica, aunque no haya salida de efectivo.||

### C. Preguntas sobre Financiamiento y Apalancamiento

|Pregunta / Concepto|Respuesta Clave|Citas|
|:--|:--|:--|
|**Tratamiento de la cuota** de un préstamo en el flujo de fondos.|La cuota **no va junta**. Debe separarse en **Interés** y **Amortización de Capital**.||
|Tratamiento del **Interés** en el flujo de fondos.|Es un **egreso afecto a impuestos** (es deducible de ganancias).||
|Tratamiento de la **Amortización de Capital** en el flujo de fondos.|Es un **egreso no afecto a impuestos**. Esto es porque es un movimiento patrimonial que compensa activo con pasivo, sin generar pérdida o ganancia económica.||
|Definición y efecto del **Apalancamiento Financiero Positivo**.|Ocurre cuando la **tasa del préstamo es menor a la tasa de descuento** del proyecto. Su efecto es que el VAN del proyecto será mayor.||
|¿Qué **tasa** se usa para el cálculo del VAN y del préstamo?|Siempre se usa la **tasa efectiva**. Si la TNA viene con capitalización (Ej. a 60 días), debe pasarse a la tasa efectiva anual (I de 360).||
|¿Cómo se trata la **deuda de proveedores** en el cálculo del Costo Promedio Ponderado de Capital (WACC)?|Los proveedores no suelen incluirse en el cálculo del costo de la deuda (KD) a menos que se les aplique explícitamente un interés.||

---

## II. Lecciones Aprendidas y Conceptos Clave (Detalles de la Transcripción)

### A. Conceptos Financieros

1. **Valoración y VAN:**
    
    - **VAN Puro (Flujo Puro):** Flujo de fondos construido **sin financiamiento externo** (presuponiendo capital propio).
    - **VAN del Accionista (Flujo del Accionista):** Flujo de fondos que **incluye el préstamo**. Este es el que interesa al accionista para saber cuánto gana con la deuda incluida.
    - **Valor Terminal:** Se utiliza para valorar los flujos de fondos posteriores al horizonte de evaluación (ej. después del Año 5), proyectando a perpetuidad. La fórmula incluye la tasa de crecimiento (G) y el WACC (Valor Terminal / (WACC - G)).
2. **Impuestos y Contabilidad:**
    
    - **Depreciación como Escudo Fiscal:** La depreciación es un gasto económico (no salida de caja) que **reduce la base impositiva** (pago menos impuestos a las ganancias). Luego debe volverse a sumar como ajuste.
    - **UAII y Ganancias:** Si un proyecto tiene utilidad negativa pero la **compañía total tiene utilidades positivas**, se debe calcular el impuesto a las ganancias del proyecto con su signo negativo para reflejar el ahorro tributario (menor base imponible).
3. **Capital de Trabajo e Inventario:**
    
    - **Stock Inmovilizado:** Producir de más (stock) inmoviliza capital de trabajo, lo que puede aumentar la necesidad de financiamiento.
    - **Impacto de Plazos:** Cambiar los plazos de venta o cobro (ej. pasar de cobrar a 30 días a 60 días) genera una necesidad adicional de capital de trabajo porque se debe financiar la operación durante más tiempo.
    - **Productos Perecederos:** La capacidad productiva no debe maximizarse si el producto es perecedero (Ej. 18 meses de vencimiento), ya que el stock podría perderse, lo cual debe tenerse en cuenta en la toma de decisiones.

### B. Lecciones sobre Gestión Comercial y Marketing (Story Brand)

1. **La Narrativa de la Marca:**
    - La **marca** es **el guía** del cliente (el héroe). El guía debe inspirar **confianza** y **empatía**.
    - La comunicación debe ser simple para el cerebro y **centrarse en el deseo del cliente** (supervivencia y prosperidad).
    - Los deseos de supervivencia incluyen preservar recursos financieros, obtener tiempo, crear redes sociales, adquirir estatus, y desear significado.
    - El **problema** (el villano) es el **gancho de la historia**. Las marcas deben enfrentar los problemas en tres niveles: **externo, interno, y filosófico** (siendo los internos los más motivadores para el cliente).
2. **Venta y Planificación:**
    - El guía (marca) debe tener un **plan claro** (3 a 6 pasos) para disipar las dudas del cliente.
    - La **Postventa** es crucial para afianzar la marca y generar referencias positivas, que es el **mejor marketing**.
    - Los clientes no actúan si no se les desafía: el **Llamado a la Acción (CTA)** es obligatorio (Comprar ahora, concierte una cita).
    - Se debe mostrar el **costo de no hacer negocio** con nosotros (evitar fracasar) para motivar al cliente.
3. **Pricing y Elasticidad:**
    - El precio se define idealmente por el **valor percibido** y no solo por los costos.
    - Se debe considerar el **contexto** del canal y el cliente (5 C's: Competencia, Costo, Cliente, Canal, Contexto).
    - En el cálculo de **elasticidad**, si se reduce el precio, la cantidad demandada debe aumentar (pendiente negativa). La elasticidad se debe usar con su valor negativo, aunque se exprese en positivo.
    - Si el producto está en etapa de **crecimiento**, se puede deslizar el precio hacia arriba; si está en etapa de **declive** (perro), se debe descontinuar.

---

## III. Análisis Detallado de Temas Solicitados

### A. SDG Consultas Final Septiembre (Ejercicio Limpieza) y Recomendaciones en Flujos de Fondos

El ejercicio de "limpieza de plásticos" (probablemente el Ejercicio 51) sirvió para repasar conceptos cruciales de la formulación financiera:

1. **VAN Puro vs. VAN Accionista:** Es fundamental distinguir entre el VAN puro (sin deuda) y el VAN del accionista (con deuda), especialmente si hay **apalancamiento financiero**.
    
2. **Cálculo de la Elasticidad (Caso Específico):** En el contexto de un ejercicio donde la demanda esperada caía un 6%, pero se bajaba el precio un 5% para **mantener las unidades**:
    
    - La **variación de la cantidad (Q)** se considera **cero** (ya que el objetivo es mantener las ventas a pesar de la caída del mercado).
    - Si se da un aumento de unidades por **acciones comerciales** (Ej. promoción) y otro por **variación de precio** (elasticidad), solo la variación por precio se usa para calcular la nueva estructura de precios. Las unidades ganadas por promoción se valorizan al precio completo, mientras que las unidades ganadas por descuento se valorizan al precio que resulte del cálculo de elasticidad.
3. **Recomendaciones en los Flujos de Fondos (Financiamiento):**
    
    - **Priorizar el VAN:** El objetivo es que el proyecto agregue valor, por lo que la decisión se basa en el VAN mayor.
    - **Tasa de Descuento (WACC/ROE/CAPM):** La tasa de descuento se calcula usando datos de mercado (CAPM) si es posible. Si no hay datos de mercado (beta, tasa libre de riesgo), el Costo de Equity (Ke) se puede calcular con el ROE.
    - **Métodos de Amortización:** El método **Francés** mantiene la **cuota fija** (interés decreciente, capital creciente). El método **Alemán** mantiene la **amortización de capital fija** (cuota decreciente, interés decreciente). El interés se deduce de impuestos, por lo que afecta la utilidad neta.
    - **Plazo de Préstamo vs. Horizonte:** Si se toma un préstamo a un plazo mayor que el horizonte de evaluación del proyecto (Ej. préstamo a 5 años, evaluación a 3), el **saldo de capital restante** (amortización faltante) debe cargarse como un **egreso no afecto a impuestos** en el último año de la evaluación.

### B. Ejercicio de Limpieza: Despidos y Ahorro de Erogación de Sueldos

El ejercicio de la empresa de limpieza donde se despiden empleados (Director Comercial y Consultor Externo) es un caso paradigmático de la aplicación de flujos incrementales y el tratamiento de los costos de personal en el flujo de fondos:

1. **Erogación por Despido (Indemnización):**
    
    - La **indemnización** (calculada como un sueldo mensual con cargas sociales por año trabajado) es una **salida de efectivo inmediata** que debe registrarse como un **Egreso Afecto a Impuestos** en el **Año Cero**.
    - El **consultor externo (monotributista)** no se indemniza, ya que no tiene relación de dependencia; simplemente se deja de facturar.
2. **Ahorro por Salario (Escudo Fiscal y Ahorro Genuino):**
    
    - El **ahorro del sueldo** del director comercial (13 sueldos anuales más cargas sociales) y el ahorro del costo del consultor (12 sueldos anuales sin SAC) se registran como un **Ingreso Afecto a Impuestos** en los años subsiguientes.
    - Este ahorro es una **ventaja para el proyecto** (un flujo incremental positivo) porque la empresa ya no incurrirá en esos gastos operativos.
    - **Relación con Adquisiciones (M&A):** Este concepto explica por qué el precio de las acciones sube tras una adquisición: la eliminación de **duplicidad de funciones** genera ahorros (ingresos futuros) que aumentan el valor actual de los flujos y, por ende, el precio de la acción.
    - La lógica es que la empresa reduce el denominador de su _headcount_ o la estructura de costos (OPEX) para aumentar la facturación por empleado, mejorando sus indicadores de mercado.
3. **El Caso del Empleado vs. Consultor:**
    
    - **Sueldo (Director):** El sueldo (salario más cargas sociales) se anualiza (13 sueldos con cargas, o 1.6 o 1.7 veces el sueldo, dependiendo del escenario).
    - **Honorarios (Consultor):** Se registra simplemente el ahorro de los 12 honorarios mensuales, sin cargas sociales ni SAC.