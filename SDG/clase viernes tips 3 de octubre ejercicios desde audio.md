Este documento estructura la transcripción de la sesión, recopilando los conceptos clave, lecciones aprendidas y preguntas frecuentes para la evaluación de proyectos de inversión, con un énfasis particular en los ejercicios relacionados con la implementación de sistemas de gestión (IT).

--------------------------------------------------------------------------------

I. Conceptos Fundamentales y Preguntas de Examen

A. Flujo de Fondos e Impacto Impositivo (Afecto/No Afecto a Impuestos)

|   |   |   |   |
|---|---|---|---|
|Concepto|Tipo de Movimiento|Impacto en Impuestos|Explicación / Lección Aprendida|
|**Indemnización**|Egreso|Afecta (Antes de impuestos)|Representa un egreso que debe ser incluido en el flujo, típicamente en la situación futura (flujos incrementales). Se calcula generalmente como un sueldo completo _full_ por año trabajado más preaviso.|
|**Ahorro de Salario**|Ingreso|Afecta|Cuando se desvincula a una persona (ej. por duplicidad de funciones tras una adquisición), su sueldo deja de pagarse, generando un ahorro que actúa como **Ingreso Afecto a Impuestos**.|
|**Cargas Sociales**|Costo Empresa|Afecta|Deben incluirse, representan aproximadamente el 45% o 1.6x del costo empresa, dependiendo del escenario.|
|**Sueldo Anual**|Costo|Afecta|Para llevar el sueldo mensual al costo anual, se debe multiplicar por **13** (incluyendo el "punto más").|
|**Monotributista/Consultor**|Gasto|Afecta|Si se desvincula, produce un ahorro, ya que se deja de pagar el gasto por el servicio. No genera indemnización al no ser empleado en relación de dependencia.|
|**Intereses del Préstamo**|Pérdida|**Afecta**|Es una **pérdida económica** (un resultado) que deduce impuestos (Escudo Fiscal).|
|**Amortización de Capital**|Movimiento Patrimonial|**No Afecta**|El capital amortizable no se deduce de impuestos porque es un concepto **patrimonial** (pago de deuda), no un resultado de ganancia o pérdida (económico).|
|**Inversión Inicial** (Compra de Maquinaria/Activo)|Egreso|No Afecta|La inversión total (Ej.: el costo de la máquina) es un egreso en el Año 0. Si se financia con deuda, el préstamo asociado entra como ingreso en el Año 0, resultando en el flujo neto de caja.|

B. Depreciación, Amortización y Valor Final del Activo

• **Naturaleza de la Depreciación:** La depreciación (o amortización) es un concepto **económico**, no financiero. Se incluye en el flujo de caja para reducir la base de cálculo del impuesto a la ganancia (**escudo fiscal**). Una vez calculado el impuesto, se debe volver a sumar al flujo (se reingresa) porque no es una salida de caja real.

• **Activación de la Inversión:** Cualquier inversión debe incluir **todos los conceptos necesarios** para que el activo esté listo para producir o funcionar (puesta a punto). Esto incluye transporte, instalación, y para sistemas, licencias, consultoría de implementación e incluso gastos relacionados si son indispensables para el arranque (viáticos, _remises_). El valor activado (Valor de Origen Completo) es el que se deprecia.

• **Valor Libro (Valor Residual Contable):** El valor contable del activo se mantiene en el precio de compra original. La depreciación acumulada se resta para dar el **Valor Libro** o valor real del activo en un momento dado.

• **Venta de Activo antes de Fin de Vida Útil (Valor de Desecho):**

    1. Se calcula el **Valor Libro** al final del horizonte de evaluación (ej. Año 5 si la vida útil es 10 años).

    2. Se determina el **Resultado Económico** de la venta: $\text{Precio de Venta} - \text{Valor Libro}$.

    3. Si el resultado es una **pérdida contable** (Precio de Venta < Valor Libro), se genera un **Escudo Fiscal** (Ahorro de Impuestos = Pérdida $\times$ Tasa Impositiva).

    4. El **Flujo Neto Final** es el Precio de Venta (dinero recibido) sumado al Escudo Fiscal [30.25 millones en el ejemplo discutido].

    5. Si el ejercicio no proporciona un precio de venta (salvamento), se debe asumir **cero**. El **Valor Libro** pendiente se considera entonces una pérdida contable total, generando un Escudo Fiscal.

C. Énfasis en Sistemas de Gestión (IT CAPEX y OPEX)

La implementación de sistemas (como SAP) y la infraestructura de TI requiere diferenciar entre inversión (CAPEX) y gastos operativos (OPEX).

• **CAPEX (Capital Expenditure):** Inversiones de capital que deben ser amortizadas (depreciadas).

    ◦ **Ejemplos:** Licencias de _software_ (intangible, se amortizan), la inversión en implementación (horas de consultoría, _manpower_ necesario para la puesta en marcha), porque sin ellos el sistema no funciona.

• **OPEX (Operating Expenditure):** Todos los gastos de ejecución y mantenimiento.

    ◦ **Ejemplos:** Pago de la línea punto a punto, licencias de Office 365 (si son recurrentes), consultoría de mantenimiento posterior a la implementación. Estos se tratan como **Gasto** anual en el flujo.

D. Capital de Trabajo (Inversión y Componentes)

El capital de trabajo es la inversión necesaria para financiar las operaciones diarias debido al desfase entre pagos (costos) y cobros (ventas).

1. **Factores de Desfase:** Incremento en el volumen de unidades, incremento en los costos o cambio en los plazos de cobranza y pago (ej. cobrar a 60/90 días en lugar de 30/60).

2. **Concepto de Inventario y Producción:**

    ◦ **Ingresos:** Siempre se basan en las unidades **vendidas** (ej. 300,000 unidades vendidas).

    ◦ **Costos Variables para Capital de Trabajo:** Si el producto es no perecedero, los costos variables para el cálculo del capital de trabajo se basan en las unidades **producidas** (ej. 500,000 unidades producidas).

    ◦ El exceso de producción no vendida (200,000 unidades en el ejemplo) se convierte en **inventario**, que es un **activo corriente** y, por lo tanto, una inversión en capital de trabajo.

3. **Inversión Requerida:** La inversión adicional en capital de trabajo solo se requiere cuando la necesidad **se incrementa** con respecto al año anterior (por ejemplo, si se incrementan las unidades vendidas, los costos o los plazos).

4. **Componentes Clave:** Cuentas por Cobrar (clientes), Inventario (stock de productos) y Cuentas por Pagar (pedalear al proveedor).

II. Lecciones Aprendidas y Conceptos Avanzados

A. Adquisiciones y Valor de la Acción

• **Aumento del Precio de la Acción:** Una adquisición (M&A) o reestructuración (recorte de cabezas) generalmente aumenta el precio de la acción porque el mercado anticipa un aumento en los flujos de fondos futuros.

    ◦ Se logra aumentando el numerador (facturación) o bajando el denominador (recorte de cabezas).

    ◦ La reducción de personal por **duplicidad de funciones** genera ahorro, que aumenta el flujo de fondos.

• **Indicadores de Gestión (CEO/Gerentes):** Los gerentes suelen ser responsables del **EBITDA** (ganancias antes de intereses, impuestos, depreciación y amortización), ya que impuestos y deuda (intereses) suelen estar definidos corporativamente. El indicador clave de un CEO es la **facturación recurrente** versus la **estructura salarial** (buscando que la facturación recurrente cubra 1.5 veces los salarios).

B. Préstamos y Tasas

• **Tasa Nominal Anual (TNA) vs. Tasa Efectiva Anual (TEA):** Si no se especifica el período de capitalización, la TNA es igual a la TEA. Generalmente, para la formulación del VAN (o la cuota de préstamo), se usa la **Tasa Efectiva**.

• **Sistema de Amortización:** Aunque no se especifique, el sistema **Francés** es el usado comúnmente en la práctica.

C. Economía de Escala y Producción

• **Economía de Escala (Concepto General):** Lograr mejores precios unitarios por compras al volumen. A nivel de planta, implica diluir los costos fijos sobre una mayor cantidad de unidades, lo que reduce el **costo fijo unitario**.

• **Punto de Equilibrio:** A partir de este punto se comienza a ganar dinero.

• **Costo Fijo Unitario:** Se calcula dividiendo el costo fijo total entre la cantidad de unidades que se estima vender en el año.

• **Paradoja de Costos:** En las líneas de producción, los costos variables por unidad son fijos, mientras que el costo fijo unitario es variable (depende del volumen de producción).

• **Riesgo por Capacidad Ociosa:** Si una máquina de gran capacidad se compra, pero la demanda inicial es baja, se está incurriendo en un **costo fijo unitario enorme**, impactando la rentabilidad (ejemplo de mercados recesivos, como el 2001, con baja capacidad instalada en uso). La solución es optimizar la producción, quizás mediante **turnos productivos** (mañana/tarde/noche).

D. Riesgo e Incertidumbre (Pregunta de Examen)

• **Definición:** Si un analista conoce todos los posibles escenarios futuros, sus probabilidades de ocurrencia y los flujos de caja asociados, la decisión de inversión se toma bajo **Riesgo, pero no bajo Incertidumbre**.

    ◦ El **Riesgo** implica que se conoce la función de probabilidad y las consecuencias.

    ◦ La **Incertidumbre** implica que las probabilidades son desconocidas.

E. Estudios Preliminares y Terrenos

• **Estudios Preliminares (Diagnósticos):** Si un estudio previo (ej. diagnóstico de maquinaria) se realiza y el proyecto **no** avanza, el costo de ese estudio debe ser cargado como **Gasto** en el período actual. Si el proyecto avanza, se considera parte de la inversión inicial (CAPEX).

• **Terrenos:** Los terrenos **no se deprecian**, aunque su valor final (valor de desecho) puede depender del mercado (ej. si es un campo o un mercado en crecimiento).

III. Resumen de Ejercicios y Casos Mencionado

|   |   |   |
|---|---|---|
|Ejercicio/Caso|Concepto Ilustrado|Detalles Relevantes|
|**Ejercicio 19** (Venta de activos)|Valor de Venta Final (Salvamento) y Flujo de Caja.|La vida útil (10 años) difiere del horizonte de evaluación (5 años). Es crucial calcular el **Valor Libro** al Año 5 para determinar el escudo fiscal sobre la venta (pérdida contable).|
|**Ejercicio de la Máquina** (Desinversión)|Desinversión Parcial de Activos.|Muestra cómo la depreciación (amortización) debe ajustarse anualmente si una parte de la inversión (ej. 20%) se vende (desinvierte) antes del final del período.|
|**Ejercicio 31** (Préstamo)|Estructura de deuda y cálculo de cuota.|Se destaca la importancia de especificar el horizonte del préstamo y el sistema de amortización.|
|**Ejercicio 18**|Economía de Escala (Capacidad Máxima)|Evalúa comprar una máquina grande (1.6 millones de unidades) versus dos máquinas pequeñas (900,000 unidades cada una), mostrando que la opción de máquinas pequeñas puede ser mejor en VAN si la demanda inicial es baja (para evitar la capacidad ociosa y altos costos fijos unitarios).|
|**Casos de Producción/Inventario**|Capital de Trabajo (Producción vs. Venta)|Destaca la regla de que los ingresos se calculan por unidades **vendidas** (ej. 300,000) pero los costos variables del capital de trabajo se calculan por unidades **producidas** (ej. 500,000), si el producto es no perecedero.|
|**Piletazo S.A.**|Estudios Preliminares.|Caso donde se evalúa si los costos de un estudio de mercado deben ser capitalizados o tratados como gasto.|