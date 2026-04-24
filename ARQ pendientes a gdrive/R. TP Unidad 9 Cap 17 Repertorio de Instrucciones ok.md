1. Indique brevemente los 4 tipos de datos que maneja Pentium.
R.:
**Byte u octeto**: Consiste en ocho bits.
**Palabra** (_Word_): Compuesta por dos bytes, lo que equivale a 16 bits.
**Doble palabra** (_Double Word_): Consiste en cuatro bytes (32 bits).
**Cuádruple palabra** (_Quadruple Word_): Consiste en ocho bytes (64 bits).

2. Indique brevemente los 3 grupos en los cuales se clasifican los 7 tipos de datos que pueden manejar el coprocesador matemático
R.:
**Enteros (Integers)**: Este grupo comprende tres tipos de datos según su longitud en bits:
    ◦ **Palabra** (16 bits).
    ◦ **Corto** (32 bits).
    ◦ **Largo** (64 bits). Estos formatos de enteros son representaciones en complemento a 2 (con signo).
**Decimal empaquetado**: Este grupo se compone de un formato único, que son los datos **BCD empaquetados de 80 bits**. Este formato está diseñado para guardar 18 dígitos BCD empaquetados.
**Coma flotante (Floating-point)**: En este grupo se distinguen tres precisiones:
    ◦ **Simple precisión** (32 bits).
    ◦ **Doble precisión** (64 bits).
    ◦ **Precisión extendida** (80 bits).
    
3. Indique brevemente las 3 categorías en que se agrupan las formas de referenciar los operandos por el microprocesador Pentium.
R.:
**Modo de direccionamiento inmediato**: En esta categoría, el operando reside en la propia instrucción. Un ejemplo de esto es la instrucción `IMUL ECX, -4`, donde `-4` es el operando inmediato.
**Por registro**: El operando que se va a utilizar reside en un registro interno del procesador. Un ejemplo es la instrucción `INC EBX`, donde el operando es el valor contenido en el registro `EBX`.
**Modo de direccionado en memoria**: El operando reside en la memoria y este modo admite múltiples variantes para expresar la posición donde se encuentra. Para calcular la dirección efectiva del operando, el Pentium aplica un algoritmo fundamental que puede incluir variables, registro base, registro índice, factor de escala y un desplazamiento.

4. Explique las instrucciones privilegiadas, la razón de su uso y los 4 grupos.
R.:
Las **instrucciones privilegiadas** son un conjunto de instrucciones especializadas dentro del repertorio de los microprocesadores que operan bajo un esquema de protección, como el Pentium, y están sujetas a estrictas restricciones de acceso.

Razón y Uso de las Instrucciones Privilegiadas

La **razón fundamental** de su existencia y uso restringido es que estas instrucciones controlan las funciones esenciales del sistema y, por lo tanto, **comprometen la integridad del sistema** si son ejecutadas por programas de aplicación comunes.

• **Restricción de acceso:** Las instrucciones privilegiadas están protegidas de los programas de aplicaciones. **Solo pueden ejecutarse desde el nivel de mayor privilegio (CPL=0)**, que corresponde a las funciones del núcleo del Sistema Operativo (S.O.).

• **Función de control:** Estas instrucciones están destinadas a **controlar las funciones del sistema**, como, por ejemplo, la carga de los registros del sistema.

• **Contexto de uso:** Se utilizan exclusivamente en el **Sistema Operativo (S.O.)** y **nunca en las aplicaciones**.

• **Consecuencia de la violación:** Si se intenta ejecutar una instrucción privilegiada cuando el Nivel de Privilegio en Curso (CPL) no es igual a 0, se genera una **excepción de protección general (GP)**.

4 Grupos de Clasificación
Las instrucciones privilegiadas se clasifican en **cuatro grupos principales**:
 - 1. **Instrucciones que pueden modificar el IOPL** (Nivel de Privilegio de E/S):

    ◦ Estas incluyen `POPF` (carga los 32 bits de la cima de la pila en el registro de _flags_, afectando al IOPL) e `IRET` (retorno de interrupción, que además carga una parte en el registro de estado). También se incluyen las relacionadas con la conmutación de tarea (TS).

 - 2. **Instrucciones que escriben los registros que controlan las tablas del sistema al operar en modo protegido:**

    ◦ Estas instrucciones afectan a los registros que hacen referencia a tablas que controlan el sistema en Modo Protegido.

    ◦ Ejemplos incluyen `LGDT` (carga el registro GDT), `LLDT` (carga el registro LDT), `LTR` (carga el registro de tareas), `LIDT` (carga el registro IDT), `MOV` (registros de control).

 - 3. **Instrucciones que afectan al contenido de la palabra de estado (MSW)**:

    ◦ La MSW (Machine Status Word) es la palabra baja del registro de control CR0.

    ◦ Ejemplos de estas instrucciones son `LMSW` (carga la MSW con el valor del operando) y `CLTS` (pone a cero el _flag_ de conmutación de tareas del registro CR0).

 - 4. **Instrucción de paro HLT:**

    ◦ La instrucción `HLT` es privilegiada y tiene la función de pasar temporalmente el procesador a un estado de parada, bloqueando la ejecución de instrucciones. El procesador sale de este estado de parada mediante un _RESET_ o una interrupción.
    

5. Si AX = 3330 y DX = 4879, al ejecutarse ADD AX, DX como queda AX. Justifique.
R.:
NO, DX esta igual que antes
6. Si AX = 99FF y DX = 4879, al ejecutarse SUB AX, DX como queda AX. Justifique.
R.:
idem
7. Si AX = 99FF y DX = 4879, al ejecutarse CMP AX, DX como queda el reg. EFLAGS. Justifique
R.:
=5176h​ (El resultado de la resta es positivo).
Estado del Registro EFLAGS
Los bits señalizadores (flags) más relevantes del registro EFLAGS quedan de la siguiente manera:

|   |   |   |
|---|---|---|
|Flag|Valor|Justificación|
|**ZF** (Cero)|**0**|El resultado de la resta (5176h​) **no es cero**.|
|**SF** (Signo)|**0**|El bit más significativo (bit 15) del resultado (5176h​) es **0**. Esto indica que el resultado es positivo.|
|**CF** (Acarreo)|**0**|Puesto que AX>DX, la resta no requirió un acarreo (_borrow_).|
|**OF** (Sobrepasamiento)|**1**|Se produce _overflow_ porque la resta de un número negativo (AX, MSB=1) menos un número positivo (DX, MSB=0) dio como resultado un número positivo (5176h​, MSB=0). Esto indica un resultado erróneo para la aritmética con signo.|
|**PF** (Paridad)|**1**|El _flag_ de paridad se activa (se pone a 1) si la paridad es par en el byte de menos peso del resultado. El byte de menos peso es 76h​ (0111 0110b​), que tiene **cuatro** unos (paridad par), por lo tanto, PF=1.|

**Justificación Adicional (Signo y Acarreo):**
La comparación `CMP AX, DX` se utiliza a menudo junto con instrucciones de salto condicionales, como `JS` (salta si SF=1) o `JE` (salta si ZF=1).
En este caso, la comparación establece que AX (99FFh​) es **mayor** que DX (4879h​) cuando se consideran números sin signo. Sin embargo, si se consideran números con signo (complemento a dos), AX es un número negativo (debido a que su bit 15 es 1) y DX es un número positivo (su bit 15 es 0). Dado que la resta de un negativo menos un positivo resultó en un positivo, el _flag_ **OF** se activa (1), señalando que el resultado está fuera del rango de 16 bits para operaciones con signo.

8. Explique brevemente que hacen las instrucciones aritméticas DEC, INC, MUL e IMUL
R.:
• **DEC (Decrement):**
    ◦ Esta instrucción se utiliza para **decrementar el operando**.
    ◦ Pertenece al grupo de instrucciones aritméticas binarias.

• **INC (Increment):**
    ◦ Esta instrucción se utiliza para **incrementar el operando**.
    ◦ Suma directamente **uno al valor que está guardado en el acumulador y lo guarda en el mismo acumulador** (código 9).
    ◦ Su funcionamiento es equivalente a poner `EAX = EAX + 1` o `ADD EAX, 1`.
    ◦ Un ejemplo es `INC EBX`, que incrementa el valor contenido en el registro `EBX`.
    ◦ Pertenece al grupo de instrucciones aritméticas binarias.

• **MUL (Multiply):**
    ◦ Realiza la **multiplicación de operandos sin signo**.
    ◦ La operación multiplica el operando especificado por **AL**, **AX** o **EAX**, dependiendo del tamaño del operando.
    ◦ El resultado se deja en **AX**, **EAX** o el par de registros **EDX:EAX**, según el tamaño de los operandos. Por ejemplo, si los operandos son de 8 bits, el resultado se obtiene en el registro AX. Si los operandos son de 16 bits, el resultado se almacena en el par DX:AX.

• **IMUL (Integer Multiply):**
    ◦ Realiza la **multiplicación de operandos con signo**.
    ◦ Permite la multiplicación entre dos entidades de **8 o 16 bits con signo**. Un número se considera negativo si su bit más significativo es igual a 1.
    ◦ Por ejemplo, `IMUL ECX, -4` multiplica el entero contenido en el registro `ECX` por el operando inmediato `-4`.

9. Si AX = 3330 y DX = 4879, al ejecutarse AND AX, DX como queda el reg. EFLAGS. Justifique
R.:
Primero, se convierten los valores hexadecimales a binario y se aplica la operación AND bit a bit (dado que AX y DX son registros de 16 bits):

|   |   |   |
|---|---|---|
|Registro|Valor Hexadecimal|Valor Binario (16 bits)|
|**AX**|3330h​|0011 0011 0011 0000b​|
|**DX**|4879h​|0100 1000 0111 1001b​|
|**AX AND DX**|0030h​|0000 0000 0011 0000b​|

El resultado final que queda en AX es 0030h​.

Estado del Registro EFLAGS

La ejecución de la instrucción `AND` actualiza los siguientes _flags_:

|   |   |   |
|---|---|---|
|Flag|Valor|Justificación|
|**ZF** (Zero Flag)|**0**|El resultado de la operación (0030h​) **no es cero**.|
|**SF** (Sign Flag)|**0**|El bit de más peso (bit 15) del resultado es **0**, indicando un resultado positivo.|
|**CF** (Carry Flag)|**0**|Las operaciones lógicas como `AND` típicamente ponen a **cero** el _flag_ de acarreo.|
|**OF** (Overflow Flag)|**0**|Las operaciones lógicas como `AND` típicamente ponen a **cero** el _flag_ de sobrepasamiento.|
|**PF** (Parity Flag)|**1**|El _flag_ de paridad se activa si el byte de menos peso del resultado contiene un número **par** de unos. El byte bajo del resultado es 30h​ (0011 0000b​), el cual contiene dos '1's (paridad par), por lo tanto, **PF = 1**.|

En resumen, el registro **EFLAGS** se actualiza principalmente con **ZF=0** y **SF=0**, reflejando el resultado positivo y no nulo de la operación lógica, y con **CF=0** y **OF=0** (comportamiento estándar para operaciones lógicas).

10. Si AX = AFE4, al ejecutarse ROL AX, 1 como queda AX. Justifique
R.:
**Valor inicial en binario (16 bits):** AX=1010 1111 1110 0100b​

**Bit más significativo (MSB):** El bit 15 es **1**. Este bit se movería al _flag_ de Acarreo (CF) y envolvería al Bit 0.
Al ejecutarse `ROL AX, 1`, el registro **AX** queda con el valor 5DC8h​.
Este resultado específico se muestra en los ejemplos de las fuentes que ilustran la rotación a la izquierda de AFE4

11. Explique brevemente que hacen las instrucciones TEST, SAL y SAR.
R.:
TEST
La instrucción **TEST** realiza la **operación lógica AND de los operandos**. Sin embargo, a diferencia de la instrucción `AND`, **TEST** **desecha el resultado de la operación**.

• **Función Principal:** Se utiliza únicamente para **afectar a los señalizadores (flags)** del registro de estado (EFLAGS). Permite chequear o comprobar el estado de ciertos bits o si el resultado sería cero o negativo, sin alterar el valor de los operandos involucrados.

SAL (Shift Arithmetic Left)

La instrucción **SAL** realiza un **desplazamiento aritmético a la izquierda**. Se emplea específicamente para operar con **valores signados**.

• **Operación de Bits:** `SAL` (y su equivalente lógico `SHL`) desplaza todos los bits del operando hacia la izquierda.

• **Signo y Acarreo:** El **bit más significativo** (bit 15 para una palabra o bit 7 para un _byte_) es insertado en el **bit de acarreo** (_Carry Flag_) del registro de banderas. Se coloca un **cero en el bit menos significativo** (bit 0).

• **Efecto Aritmético:** El desplazamiento aritmético a izquierda es equivalente a **multiplicar el contenido del registro por la base** (es decir, por dos).

SAR (Shift Arithmetic Right)

La instrucción **SAR** realiza un **desplazamiento aritmético a la derecha**. Al igual que `SAL`, se utiliza para manipular **valores signados**. Es la forma de desplazamiento que permite conservar el signo del operando, a diferencia de los desplazamientos lógicos.

• **Operación de Bits:** `SAR` desplaza todos los bits a la derecha.

• **Signo y Acarreo:** El bit menos significativo (bit 0) es insertado en el **bit de acarreo**. Lo más importante de `SAR` es que **no modifica el bit más significativo (bit de signo)**, sino que **mantiene el valor del signo**.

• **Efecto Aritmético:** El desplazamiento aritmético a la derecha es equivalente a **dividir el contenido del registro por la base** (por dos). Si la división produce un resto, `SAR` realiza un **redondeo 'por defecto' del resultado**.

12. Si AX = 3330 y DX = 4879, al ejecutarse SHLD AX, DX, 2 como queda AX y DX.
R.:
La instrucción **SHLD AX, DX, 2** (Shift Left Double) realiza un **desplazamiento lógico a la izquierda de 2 bits** sobre el contenido de los dos operandos (AX y DX) tomados conjuntamente como una entidad de 32 bits. Los bits se desplazan del segundo operando (DX, la fuente) hacia el primer operando (AX, el destino).

Dados los valores iniciales AX=3330h​ y DX=4879h​, tras ejecutarse `SHLD AX, DX, 2`, los registros quedan con los siguientes valores:

• **AX** queda con el valor CC00h​.

• **DX** queda con el valor 21E4h​.

**Justificación:**

La instrucción `SHLD` modifica tanto el registro destino (AX) como el registro fuente (DX) al desplazar sus contenidos de forma conjunta. Al realizar el desplazamiento a la izquierda por 2, los bits de mayor peso de AX se pierden (entrando en el _Carry Flag_), y los bits de mayor peso de DX se desplazan a las posiciones de menor peso de AX. Simultáneamente, los bits de DX también se desplazan 2 posiciones hacia la izquierda, y las posiciones de menor peso de DX se rellenan con ceros.

13. Explique cómo queda el registro PC al ejecutarse la instrucción JMP FF456781. Justifique 
R.:
La instrucción **JMP** (Jump) pertenece al grupo de instrucciones de **transferencia de control** y provoca un **salto incondicional** que resulta en una **ruptura de secuencia** en la ejecución del programa.

Al ejecutarse la instrucción **JMP FF456781**, el registro **PC** (Program Counter, también conocido como IP o EIP) queda con el valor FF456781h​.

Justificación

La función del registro **PC** (o puntero de instrucción) es contener la **dirección de memoria de la próxima instrucción a ejecutarse**.

**Naturaleza de JMP:** Las instrucciones de salto, como `JMP`, se utilizan precisamente para **romper la secuencia** normal de ejecución.

**Mecanismo de Salto:** Cuando una instrucción es una instrucción de salto, la **parte Data** de la instrucción (que contiene la dirección a la que se debe saltar) se **carga directamente en el IP** (o PC). En este caso, el valor `$FF456781_{\text{h}}$` es la dirección de destino.

**Resultado Específico:** Las fuentes indican que para la instrucción `JMP FF456781`, el registro PC se carga con dicho valor: PC=FF456781h​

El registro PC se actualiza para apuntar a la dirección `$FF456781_{\text{h}}$`, que será la próxima instrucción que la CPU buscará y ejecutará.

14. Explique brevemente que hacen las instrucciones de salto JA, JC y JE
R.:
Las instrucciones **JA**, **JC** y **JE** forman parte del grupo de instrucciones de **transferencia de control** o **salto condicional**. Estas instrucciones provocan una **ruptura en la secuencia de la ejecución del programa** si se cumple una condición específica determinada por los _flags_ (bits señalizadores) en el registro **EFLAGS**.

A continuación, se explica brevemente la función de cada una:

- **JA (Jump if Above / Saltar si es Superior):**
    
    - Esta instrucción provoca un salto si **el primer operando es mayor que el segundo**, específicamente en el contexto de la **aritmética sin signo**.
    - Junto con otras instrucciones similares, el código de condición (CC) en `Jcc` representa la condición que se evalúa.
- **JC (Jump if Carry / Saltar si hay Acarreo):**
    
    - Esta instrucción provoca un salto si el **bit de Acarreo (CARRY Flag, CF) del registro EFLAGS es igual a 1**.
    - La activación del _flag_ de acarreo ocurre, por ejemplo, cuando una operación aritmética excede el límite de capacidad del registro o requiere un acarreo (_borrow_).
- **JE (Jump if Equal / Saltar si es Igual):**
    
    - Esta instrucción provoca un salto si el **bit Z (Zero Flag, ZF) del registro EFLAGS es igual a 1**.
    - Si el resultado de la operación anterior (generalmente una comparación o resta, como `CMP`) es **cero**, el _flag_ Z se pone a 1, y la instrucción `JE` ejecuta el salto. Esto implica que los operandos comparados son iguales. La instrucción `JZ` (Jump if Zero) es similar a `JE` y salta si el resultado es cero (ZF=1).

15. Explique brevemente que hacen las instrucciones de transferencia de datos MOV, IN, POP y PUSH
R.:
Las instrucciones **MOV**, **IN**, **POP** y **PUSH** son fundamentales en la transferencia de datos en la arquitectura de computadores:

 MOV (Move / Mover)

La instrucción `MOV` se clasifica como una **instrucción de transferencia de datos**. Su propósito es **copiar el valor del segundo operando (fuente) al primer operando (destino)**. Realiza una operación de "copy past" y **no cambia el valor del operando fuente**.

- **Función:** Se utiliza para **copiar información de un lugar a otro**, ya sea **entre registros**, o **de memoria a registro y viceversa**.
- **Sintaxis:** Generalmente sigue el formato `MOV destino, fuente`.
- **Usos comunes:** Transferir una **constante a un registro** (`MOV AX, 0000h`), **memoria a registro** (`MOV AX, [FFFF]`) o entre dos registros (`MOV AX, BX`).

 IN (Input / Entrada)

La instrucción `IN` es una instrucción de **Entrada/Salida (E/S)** que permite la **entrada de un dato desde el exterior**.

- **Función:** Su propósito es **tomar un valor** que viene de algún **periférico de entrada** y **cargarlo en el registro acumulador (EAX/AL)**.
- **Manejo de E/S:** Carga en el registro destino (típicamente $AL$) el valor de la **puerta de E/S** apuntada (a menudo por $DX$).

 PUSH (Push to Stack / Empujar a Pila)

`PUSH` es una instrucción de transferencia de datos utilizada para **almacenar información en la pila**.

- **Estructura:** La pila es una estructura de datos en memoria que opera bajo el criterio **LIFO** (Last In, First Out / Último en Entrar, Primero en Salir).
- **Operación:** Se utiliza para **empujar o producir el almacenamiento** de una palabra o dato en la pila.
- **Puntero de Pila (SP):** Cuando se inserta un elemento a la pila, el procesador **decrementa el puntero de pila (ESP/SP)**. Si se guardan dos _bytes_ (16 bits), el puntero se decrementa en dos unidades.
- **Utilidad:** `PUSH` se usa para **guardar temporalmente registros** (como `PUSHA` para guardar ocho registros generales) o el **registro de señalizadores** (`PUSHF`/`PUSHFD`), así como para **almacenar direcciones de retorno** de subrutinas.

 POP (Pop from Stack / Extraer de Pila)

`POP` es la instrucción opuesta a `PUSH`, utilizada para **extraer o sacar una palabra o dato desde la cima de la pila**.

- **Estructura:** Funciona también bajo el principio **LIFO**, accediendo siempre al último elemento introducido.
- **Operación:** **Transfiere la información desde la cima de la pila a un registro destino**.
- **Puntero de Pila (SP):** Cuando se saca un elemento, el procesador realiza la operación contraria a `PUSH`: **incrementa el puntero de pila (ESP/SP)**. Si se extraen dos _bytes_, el puntero se incrementa en dos unidades.
- **Utilidad:** `POP` permite **restaurar valores previamente guardados** en la pila, como registros generales (`POPA`) o el registro de señalizadores (`POPF`/`POPFD`).

16. Explique brevemente que hacen las instrucciones de control de señalizadores CLC y CLI
R.:
Ambas instrucciones pertenecen al grupo de **instrucciones de control de señalizadores** (o _flags_) y se utilizan para modificar directamente bits específicos dentro del registro de estado (EFLAGS).

- **CLC (Clear Carry Flag):**
    
    - Esta instrucción se utiliza para **poner a cero (0) el señalizador de acarreo (CF)** del registro EFLAGS.
    - Es la instrucción opuesta a `STC`, que pone el _flag_ de acarreo a 1.
- **CLI (Clear Interrupt Flag):**
    
    - Esta instrucción **pone a cero (0) el señalizador de interrupción (IF)** del registro de señalizadores.
    - Al desactivar el _flag_ IF (ponerlo a 0), la CPU **prohíbe o inhabilita el reconocimiento de las peticiones de interrupción mascarables**.
    - Junto con `STI` (que pone el _flag_ IF a 1, permitiendo interrupciones mascarables), `CLI` es una de las instrucciones de Entrada/Salida (E/S).

17. Explique y de un ejemplo de la instrucción BT
R.:
La instrucción **BT (Bit Test)** pertenece al grupo de las **Instrucciones de Bit y Byte** y es una de las instrucciones nuevas incorporadas en el repertorio de microprocesadores como el Pentium.

Explicación de la Instrucción BT

La función principal de **BT** es evaluar el estado de un bit específico dentro de un operando (el destino) y copiar ese valor al **Señalizador de Acarreo (Carry Flag, CF)** en el registro **EFLAGS**.

1. **Primer Operando (Destino):** Contiene el dato cuyos bits se van a inspeccionar (por ejemplo, un registro como $AX$).
2. **Segundo Operando (Fuente):** Especifica la **posición** del bit (el índice) que se desea examinar.

El efecto de la instrucción `BT` es **asignar al señalizador CF el valor del bit del primer operando, quedando especificada su posición por el segundo operando**.

**Nota:** Existen instrucciones relacionadas que, además de realizar la prueba de bit, modifican el valor del bit examinado, como `BTC` (complementa el bit), `BTR` (pone el bit a 0), y `BTS` (pone el bit a 1).

Ejemplo de la Instrucción BT

Considere el siguiente ejemplo que demuestra cómo el valor del bit 8 de un registro $AX$ afecta al _Carry Flag_ ($CF$):

1. **Carga Inicial:** Se asume una instrucción previa que carga un valor en el registro $AX$ (por ejemplo, `MOV AX, R6`).
2. **Instrucción BT:** Se ejecuta la instrucción `BT AX, 8`.
    - Esta instrucción examina el **bit en la posición 8** de $AX$.
3. **Resultado en CF:** Si, tras el paso 1, **el octavo bit de AX es igual a UNO**, la instrucción `BT AX, 8` hace que el **CF de EFLAGS se ponga a UNO**.

En este caso, el $CF$ del registro $EFLAGS$ queda activado (valor **1**), reflejando que el bit examinado en la posición 8 de $AX$ contenía un 1.
15. Explique brevemente que hacen las instrucciones multisegmento CALL, RET, INT e IRET
R.:

18  Explique brevemente que hacen las instrucciones multisegmento CALL, RET, INT e IRET

R.:
Las instrucciones **CALL**, **RET**, **INT** e **IRET** son catalogadas como **instrucciones multisegmento** o pertenecen a las **instrucciones de transferencia de control**. Su propósito es gestionar las llamadas a procedimientos y el manejo de interrupciones, transfiriendo el flujo de ejecución del programa.

 CALL (Llamada a Rutina/Procedimiento)

- La instrucción `CALL` se usa para realizar una **llamada o salto a una rutina o procedimiento**.
- Al ejecutarse, automáticamente **almacena en la pila la dirección de retorno** (la instrucción siguiente a la llamada, a menudo referenciada como $CS:IP$).
- Es el inicio de un procedimiento convocado, donde el programa llamador retoma el procesamiento al finalizar la subrutina.
- Puede implicar transferencias de control a otro segmento de código.
- En entornos protegidos, permite acceder a rutinas de mayor nivel de privilegio (PL) a través de un recurso llamado **"Puerta de Llamada" (PLL)**.
- La ejecución de `CALL` puede iniciar una **conmutación de tarea** si se dirige a un descriptor TSS o puerta de tarea. Si llama a una tarea, el procesador pone el _flag_ de Tarea Anidada ($NT$) a 1.

 RET (Retorno de Rutina/Procedimiento)

- La instrucción `RET` (Return) indica el **final de un procedimiento** convocado por `CALL`.
- **Extrae o "retira" la dirección de retorno** que estaba almacenada en la pila.
- Actualiza el valor del **puntero de instrucción (IP)** para que la CPU continúe la ejecución en la instrucción inmediatamente posterior al `CALL`.
- En transferencias de control internivel, `RET` solo puede **disminuir el nivel de privilegio** o mantenerlo.

 INT (Interrupción)

- `INT` se utiliza para la **llamada a un programa de manejo de una interrupción**.
- Se convoca de forma **sincrónica** dentro de un programa (interrupción de _software_) para solicitar una función determinada.
- El formato `INT n` utiliza $n$ como número de entrada de la Tabla de Interrupciones ($IDT$). Por ejemplo, `INT 20` se usa para finalizar el programa y devolver el control.
- Cuando se produce, guarda automáticamente en la pila la **dirección de retorno** ($CS:IP$) y, eventualmente, el **estado de los _flags_** (_Status Register_) del procesador.

 IRET (Retorno de Interrupción)

- `IRET` (Interrupt Return) se utiliza para el **retorno de un programa de interrupción**. Es la instrucción final de la rutina de servicio de una interrupción o excepción.
- **Recupera (saca de la pila)** los datos previamente guardados, como $CS$, $EIP$, $SS$, $ESP$ y el registro $EFLAGS$, para continuar la ejecución del programa suspendido.
- Puede **modificar el campo IOPL** (Nivel de Privilegio de E/S) del registro $EFLAGS$.
- Si el _flag_ $NT$ (Tarea Anidada) está activo (a 1), la instrucción `IRET` puede **provocar una conmutación de tarea**, utilizando el registro de Tarea Previa ($TR$ previo) guardado en el Segmento de Estado de la Tarea ($TSS$).
- Puede **activar el _flag_ $VM$** (Modo Virtual 8086) si se ejecuta con CPL = 0.

19 Explique brevemente que hacen las instrucciones HLT, LGDT, LIDT y LLDT
R.:
Las instrucciones **HLT**, **LGDT**, **LIDT** y **LLDT** son instrucciones fundamentales, generalmente clasificadas como **instrucciones privilegiadas** o del sistema operativo, con las siguientes funciones:

 HLT (Halt / Parar)

La instrucción `HLT` (Halt) es una **instrucción de fin de programa** y es un ejemplo de una **instrucción sin dirección** que representa solo el Código de Operación (COP).

- **Función:** Su propósito es **detener temporalmente el procesador** o **detener la ejecución de un programa**.
- **Mecanismo:** Al ejecutarse, **inhibe la generación de los pulsos de _clock_**. Esto significa que todos los instantes de tiempo ($t_i$) se ponen a cero, impidiendo que se generen más microoperaciones.
- **Clasificación:** Es una instrucción privilegiada y el procesador sale del estado de parada mediante un _RESET_ o una interrupción.

 LGDT (Load Global Descriptor Table Register / Cargar Registro de Tabla de Descriptores Globales)

- **Función:** Se utiliza para **cargar el registro GDTR** (Global Descriptor Table Register), cargándolo desde una posición de memoria.
- **Propósito:** Se emplea para **instalar la Tabla de Descriptores Globales (GDT)** en la memoria. El registro GDTR apunta a la base y al límite de la GDT.
- **Detalles:** La instrucción carga una estructura de 48 bits, donde el campo de **límite** son los primeros 16 bits y el campo de **base** son los últimos 32 bits. El GDTR solo debe cargarse durante la inicialización del sistema. Es una instrucción privilegiada.

 LIDT (Load Interrupt Descriptor Table Register / Cargar Registro de Tabla de Descriptores de Interrupción)

- **Función:** Se utiliza para **cargar el registro IDTR** (Interrupt Descriptor Table Register). Carga la **dirección base y el límite** de la Tabla de Descriptores de Interrupción (IDT) en el IDTR.
- **Propósito:** El IDTR almacena el valor de la base y el límite de la IDT, cuyos descriptores se utilizan cuando se producen interrupciones y excepciones.
- **Requisitos:** Es una instrucción privilegiada que puede ser ejecutada únicamente cuando el **CPL (Nivel de Privilegio en Curso) es 0**. Se usa generalmente para la inicialización del código del sistema operativo cuando se crea una IDT.

 LLDT (Load Local Descriptor Table Register / Cargar Registro de Tabla de Descriptores Locales)

- **Función:** Se utiliza para **cargar el registro LDTR** (Local Descriptor Table Register).
- **Propósito:** Carga en el LDTR la dirección de la **Tabla de Descriptores Locales (LDT)** de la tarea que está en curso. El LDTR apunta a la base de la LDT activa.
- **Requisitos:** Esta instrucción debe referenciar a un **descriptor de segmento de una LDT**, y debe cargarse de forma explícita durante la inicialización del sistema. Es una instrucción privilegiada.
20. Explique brevemente que hacen la instrucción del coprocesador WAIT
R.:
La instrucción **`WAIT`** (Espera) es una instrucción diseñada para **sincronizar el procesador principal (CPU) con el coprocesador matemático (FPU)**.

Su función es **detener temporalmente la ejecución** de la CPU. El Pentium se detiene y **espera** hasta que el pin **BUSY# se desactive**. Esto indica que el coprocesador ha terminado la operación que estaba realizando.

Si el procesador detecta que el coprocesador no está disponible para realizar operaciones, la ejecución de `WAIT` o `FWAIT` puede provocar una **excepción por coprocesador no disponible** (#NM), identificada como Vector 7. El control de la función de esta instrucción está relacionado con el _flag_ $MP$ (Monitor de Coprocesador) en el registro $CR0$.

21. Explique brevemente que hacen y para que se usa la instrucción NOP 
R.:
La instrucción **NOP** (No Operation) es una instrucción fundamental en la arquitectura de computadores:
 ¿Qué hace?

La instrucción **NOP** (No Operation o "no operación") **no efectúa operación alguna**.
 ¿Para qué se usa?

`NOP` es una de las instrucciones **más simples** y se clasifica como una **Instrucción sin dirección**.

- **Formato:** Al ser una instrucción sin dirección, `NOP` **representa solo al Código de Operación (COP)**.
- **Ejemplo:** Se puede observar en listados de código, por ejemplo, donde se representa en el desensamblador como `90 NOP`.

Aunque las fuentes no detallan sus aplicaciones específicas en programación, se utiliza en general para rellenar espacios de código, alinear datos o instrucciones, o crear demoras de tiempo controladas, ya que no realiza ninguna tarea funcional más allá de consumir un ciclo de ejecución.