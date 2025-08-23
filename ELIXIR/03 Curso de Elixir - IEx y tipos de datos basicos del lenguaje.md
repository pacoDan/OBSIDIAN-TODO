### IEx y Tipos de Datos Básicos en Elixir: Un Resumen Esencial
Para un desarrollador acostumbrado a la consola de Node.js o al REPL de Python/Ruby, el **IEx (Elixir Interactive Shell)** será una herramienta familiar y fundamental. Es el REPL (Read-Eval-Print Loop) de Elixir, y es donde la exploración del lenguaje y la depuración interactiva cobran vida.
#### IEx: El REPL de Elixir
- **Propósito:** IEx es tu laboratorio interactivo para Elixir. Permite ejecutar comandos, probar expresiones, inspeccionar valores, depurar funciones y explorar la documentación del lenguaje sin necesidad de "ensuciar" tu código fuente. Es análogo al REPL de Node.js (`node`) o la consola del navegador.
- **Funcionalidades Clave:**
    - **Ayuda Integrada (`h`):** Presionar `h` y `Enter` en IEx muestra una lista de "IEx Helpers" (ayudantes de IEx). Esto es increíblemente útil para descubrir comandos como `i` (inspect), `c` (clear), o cómo reusar líneas anteriores.
    - **Inspección de Tipos (`i`):** Similar a `typeof` en JavaScript, `i <valor>` en IEx te permite inspeccionar el tipo de dato de cualquier término, mostrando su tipo, módulo de referencia y protocolos implementados. Esto es crucial para entender la naturaleza de los datos en Elixir.
    - **Reutilización de Líneas:** Puedes reusar el resultado de una línea anterior usando `v(<número_de_línea>)`. Por ejemplo, `v(4)` re-evaluará o mostrará el resultado de la línea 4. Esto es una comodidad que no siempre se encuentra en otros REPLs.
#### Tipos de Datos Básicos en Elixir
Elixir, siendo un lenguaje funcional, maneja tipos de datos de manera inmutable y clara. Aquí los tipos fundamentales, con comparaciones a Node.js donde sea relevante:

1. **Números:**
    
    - **Enteros (Integers):** Comportamiento estándar. Soportan números de precisión arbitraria (no hay límites de `MAX_SAFE_INTEGER` como en JS).
        
        - **Ejemplo:** `10`, `12345678901234567890`
        - **Notaciones:** Soporta hexadecimal (`0x10`), octal (`0o10`), y binario (`0b10`).
        
    - **Flotantes (Floats):** Representados con punto decimal.
        
        - **Ejemplo:** `3.14`, `1.0`
        - **División:** La división con el operador `/` **siempre** devuelve un flotante (ej: `15 / 3` es `5.0`). Para división entera, usa la función `div/2` (ej: `div(15, 3)` es `5`). Para el resto, usa `rem/2` (ej: `rem(15, 4)` es `3`).
        
    
2. **Booleanos (Booleans):**
    
    - `true` y `false`. Comportamiento idéntico a JavaScript.
    - **Operadores:** `and`, `or`, `not`.
    
3. **Átomos (Atoms):**
    
    - **Concepto Clave:** Un átomo es una constante cuyo nombre es su propio valor. Son inmutables y se usan para representar nombres simbólicos, estados o identificadores únicos. Son similares a los `Symbol`s en JavaScript (aunque con un uso más extendido y fundamental en Elixir) o los `Symbol`s de Ruby.
    - **Uso:** Frecuentemente utilizados para indicar el éxito o fracaso de una operación (ej: `:ok`, `:error`), o como claves en mapas (diccionarios).
    - **Ejemplo:** `:my_atom`, `:ok`, `:error`
    - **Inspección (`i :my_atom`):** Mostrará `Type: atom`.
    
4. **Cadenas (Strings):**
    
    - Representadas con comillas dobles.
    - **Codificación:** Son binarios codificados en UTF-8. Esto significa que Elixir maneja Unicode de forma nativa y eficiente.
    - **Ejemplo:** `"Hello, Elixir!"`
    

#### Tipos de Datos Compuestos (Introducción)

La transcripción introduce brevemente los tipos compuestos, que son esenciales para estructurar datos:

1. **Listas (Lists):**
    
    - Colecciones ordenadas de elementos, encerradas en corchetes `[]`.
    - **Heterogéneas:** Pueden contener elementos de diferentes tipos (similar a los arrays en JavaScript).
    - **Inmutables:** Las operaciones en listas devuelven nuevas listas, no modifican la original.
    - **Ejemplo:** `[1, "hello", :world, true]`
    - **Longitud:** `length([1, 2, 3])` devuelve `3`.
    
2. **Tuplas (Tuples):**
    
    - Colecciones ordenadas de elementos, encerradas en llaves `{}`.
    - **Tamaño Fijo:** A diferencia de las listas, las tuplas tienen un tamaño fijo una vez creadas.
    - **Uso:** Comúnmente usadas para retornar múltiples valores de una función, especialmente para indicar éxito/error (ej: `{:ok, result}` o `{:error, reason}`). Esto es una convención muy fuerte en Elixir.
    - **Ejemplo:** `{1, "hello", :world}`
    - **Inspección (`i {1, 2}`):** Mostrará `Type: tuple`.
    
3. **Mapas (Maps / Diccionarios):**
    
    - Colecciones de pares clave-valor, similares a los objetos literales en JavaScript o los diccionarios/hashes en Python/Ruby.
    - **Sintaxis:** `%{key => value}`. Las claves pueden ser de cualquier tipo, aunque los átomos son muy comunes.
    - **Sintaxis Corta para Átomos:** Si la clave es un átomo, se puede usar la sintaxis `%{atom_key: value}` (ej: `%{name: "Martín"}`).
    - **Ejemplo:** `%{name: "Alice", age: 30}`, `%{1 => "one", :two => 2}`
    

**En Resumen:**

El IEx es tu puerta de entrada interactiva a Elixir, permitiéndote explorar y entender el lenguaje en tiempo real. Los tipos de datos básicos, especialmente los **átomos** y la distinción entre **listas y tuplas**, son fundamentales para comprender la estructura y el flujo de datos en Elixir, y son pilares de su diseño funcional e inmutable. La familiaridad con estos conceptos te permitirá sumergirte rápidamente en la construcción de aplicaciones robustas con Elixir.
