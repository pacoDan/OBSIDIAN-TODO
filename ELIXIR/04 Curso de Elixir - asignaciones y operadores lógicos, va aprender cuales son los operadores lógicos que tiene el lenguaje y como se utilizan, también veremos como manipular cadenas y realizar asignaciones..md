### Asignaciones y Operadores Lógicos en Elixir: Un Resumen
Este capítulo profundiza en cómo Elixir maneja la asignación de variables, los tipos de datos y las operaciones binarias, incluyendo comparaciones y lógica booleana. Para un programador experimentado, la clave está en entender las sutilezas que Elixir introduce, especialmente en la inmutabilidad y el _pattern matching_ implícito en las "asignaciones".
#### 1. Asignaciones (El Operador `=`)
En Elixir, el operador `=` no es una simple asignación en el sentido imperativo tradicional (como `let` o `var` en JavaScript). Es un **operador de _match_** (coincidencia).
- **Operador de Match (`=`):**
    - Intenta hacer que el lado izquierdo coincida con el lado derecho. Si el lado izquierdo es una variable no asignada, la variable se "enlaza" al valor del lado derecho. Si la variable ya tiene un valor, el operador `=` intentará que el valor actual de la variable coincida con el valor del lado derecho. Si no coinciden, se produce un error.
    - **Inmutabilidad:** Una vez que una variable se enlaza a un valor, ese valor es inmutable. Si "reasignas" una variable, en realidad estás creando un nuevo enlace para esa variable a un nuevo valor, dejando el valor original intacto en memoria (si aún es referenciado). Esto es similar a cómo `const` funciona con tipos primitivos en JavaScript, pero es la regla general para todos los tipos en Elixir.
    - **Ejemplo:**
```ex
name = "Martín"  # 'name' se enlaza a "Martín"
age = 40         # 'age' se enlaza a 40

# El operador de match en acción:
# Intenta que el patrón `{:ok, value}` coincida con el resultado de la función.
# Si coincide, 'value' se enlaza al segundo elemento de la tupla.
{:ok, result} = {:ok, 123}
# result ahora es 123

# Esto causaría un error de MatchError porque el patrón no coincide:
# {:error, reason} = {:ok, 123}
```
- **Variables con `?` (Predicados):**
    - Elixir permite usar `?` al final de los nombres de variables (ej: `is_valid?`). Esta es una convención para funciones que devuelven `true` o `false` (predicados). No tiene un significado sintáctico especial para la asignación, pero es una buena práctica de nomenclatura.
#### 2. Operaciones Aritméticas y Precedencia
- **Operadores Estándar:** `+`, `-`, `*`, `/`.
- **Precedencia:** La multiplicación y división tienen mayor precedencia que la suma y resta, como es estándar en la mayoría de los lenguajes.
- **Paréntesis:** Se usan para redefinir la precedencia, aplicando la propiedad asociativa.
    - **Ejemplo:** `(25 * 9) + (11 - 3)`
#### 3. Operadores de Comparación (Predicados)
Estos operadores devuelven un booleano (`true` o `false`). Se les conoce como "predicados".
- **Menor que:** `<`
- **Mayor que:** `>`
- **Menor o igual que:** `<=`
- **Mayor o igual que:** `>=`
- **Igualdad (`==`):**
    - Compara solo el **valor**.
    - **Ejemplo:** `21 == 21.0` devuelve `true` (similar a `==` en JavaScript, que realiza coerción de tipo).
- **Desigualdad (`!=`):**
    - Compara solo el **valor**.
    - **Ejemplo:** `21 != 21.0` devuelve `false`.
- **Igualdad Estricta (`===`):**
    - Compara el **valor y el tipo de dato**.
    - **Ejemplo:** `21 === 21.0` devuelve `false` (porque `21` es un entero y `21.0` es un flotante). Esto es análogo a `===` en JavaScript.
- **Desigualdad Estricta (`!==`):**
    - Compara el **valor y el tipo de dato**.
    - **Ejemplo:** `21 !== 21.0` devuelve `true`.
#### 4. Operadores Lógicos Binarios

Elixir utiliza palabras clave para sus operadores lógicos, lo que mejora la legibilidad.

- **AND Lógico (`and`):**
    
    - Devuelve `true` si **ambos** operandos son `true`.
    - **Cortocircuito:** Si el primer operando es `false`, no evalúa el segundo.
    - **Ejemplo:** `true and true` devuelve `true`; `false and true` devuelve `false`.
    
- **OR Lógico (`or`):**
    
    - Devuelve `true` si **al menos uno** de los operandos es `true`.
    - **Cortocircuito:** Si el primer operando es `true`, no evalúa el segundo.
    - **Ejemplo:** `true or false` devuelve `true`; `false or false` devuelve `false`.
    
- **NOT Lógico (`not`):**
    
    - Invierte el valor booleano.
    - **Ejemplo:** `not true` devuelve `false`; `not false` devuelve `true`.
    - **Falsy/Truthy:** En Elixir, solo `false` y `nil` son "falsy". Cualquier otro valor (números, cadenas, listas, tuplas, átomos, etc.) es "truthy".
        
        - **Ejemplo:** `not 0` devuelve `false` (porque `0` es truthy en Elixir, a diferencia de JavaScript donde `0` es falsy). `not nil` devuelve `true`.
        
    

#### 5. Cadenas (Strings) y Concatenación

- **Representación:** Las cadenas se definen con comillas dobles (`"..."`).
- **Interpolación:** Se usa `#{}` para interpolar expresiones dentro de cadenas, similar a los _template literals_ de JavaScript.
    
    - **Ejemplo:** `name = "Alice"`, `"Hello, #{name}!"`
    
- **Concatenación:** El operador `++` se usa para concatenar cadenas.
    
    - **Ejemplo:** `"Hello" ++ " World"`
    
- **Strings como Binarios:** La transcripción menciona que los strings son internamente binarios (`<<...>>`). Esto es una característica avanzada que permite una manipulación de bajo nivel eficiente y es fundamental para la comunicación de red. La representación `<<104, 111, 108, 97>>` es el string "hola" en su forma binaria (valores ASCII/UTF-8).
    
    - **`?` para ASCII:** El operador `?` puede usarse en IEx para obtener el valor ASCII de un carácter (ej: `?h` devuelve `104`).
    

#### 6. `IO.puts` vs. Evaluación de IEx

- **`IO.puts`:** Es una función para imprimir en la salida estándar (la terminal). Siempre devuelve el átomo `:ok` (o `:error` si falla), ya que interactúa con el "mundo exterior" (es una función impura).
    
    - **Ejemplo:** `IO.puts("Hello World")` imprime "Hello World" y devuelve `:ok`.
    
- **Evaluación de IEx:** Cuando escribes una expresión directamente en IEx (ej: `"Hello World"`), IEx evalúa la expresión y te muestra su resultado directamente, sin imprimirlo en la salida estándar. El color amarillo en la transcripción indica que es el resultado de la evaluación de IEx.

**Conclusión para el Desarrollador Experimentado:**

La "asignación" en Elixir es en realidad un _pattern matching_ que enlaza variables a valores inmutables. Los operadores lógicos son explícitos (`and`, `or`, `not`) y tienen reglas de "truthiness" más estrictas que JavaScript. La comprensión de los strings como binarios y el uso de `IO.puts` para efectos secundarios son cruciales para escribir código idiomático en Elixir. La inmutabilidad es el hilo conductor que une todos estos conceptos, simplificando el razonamiento sobre el estado de la aplicación.