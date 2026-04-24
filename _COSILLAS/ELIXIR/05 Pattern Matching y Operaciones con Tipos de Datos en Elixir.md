
Este capítulo es una inmersión práctica en dos pilares fundamentales de Elixir: el **Pattern Matching** y la manipulación de los tipos de datos básicos del lenguaje. Para desarrolladores acostumbrados a la desestructuración en JavaScript o la programación orientada a objetos, Elixir ofrece un enfoque funcional y declarativo que simplifica la extracción y transformación de datos.

#### 1. Pattern Matching: Más Allá de la Asignación

El _Pattern Matching_ es una característica central de Elixir que va mucho más allá de una simple asignación de variables. Es un mecanismo poderoso para:

- **Extracción de Valores:** Permite desestructurar y extraer valores de estructuras de datos complejas (listas, tuplas, mapas) de forma declarativa y concisa.
- **Control de Flujo Implícito:** Se utiliza para dirigir la ejecución del código basándose en la forma y el contenido de los datos, a menudo reemplazando sentencias `if/else` o `switch/case` complejas.
- **El Operador `=` como Match:** En Elixir, el operador `=` no es de asignación, sino de _match_. Intenta hacer que el patrón del lado izquierdo coincida con el valor del lado derecho. Si hay una coincidencia, las variables en el patrón se enlazan a los valores correspondientes. Si no hay coincidencia, se produce un `MatchError`.

**Ejemplos Clave de Pattern Matching:**

- **Listas:**
    
    - **Extracción de elementos específicos:** Aunque tedioso para listas largas, permite extraer elementos por posición.
```ex
[_, value, _, _, _] = [1, 2, 3, 4, 5] # Extrae el 2
# value es 2
```

- **Listas Anidadas:** Permite desestructurar estructuras complejas.
```ex
[_, _, [_, _, target_value]] = [1, 2, [5, 6, 7]] # Extrae el 7
# target_value es 7
```
**Tuplas (Casos de Uso Comunes):**

- **Retornos de Funciones:** Es el uso más idiomático. Las funciones a menudo devuelven tuplas `{:ok, value}` o `{:error, reason}`. El _pattern matching_ permite manejar estos casos elegantemente.
```ex
{:ok, result} = {:ok, "Success!"} # result es "Success!"
# {:error, reason} = {:ok, "Success!"} # Esto causaría un MatchError
```

**Mapas (Diccionarios):**

- **Extracción por Clave:** Permite extraer valores de mapas basándose en sus claves.
```ex
%{name: person_name, age: person_age} = %{name: "Alice", age: 30, city: "NY"}
# person_name es "Alice", person_age es 30
```
**Extracción de Claves Específicas:** Puedes extraer solo las claves que te interesan, ignorando el resto.
```ex
%{age: person_age} = %{name: "Alice", age: 30}
# person_age es 30
```
**El Operador `_` (Ignorar):** Se usa para indicar que no nos interesa un valor en una posición o clave específica.
```ex
{_, value} = {:ok, 123} # Ignora el primer elemento, extrae el segundo
```

- **Pin Operator (`^`):**
    
    - **Re-binding vs. Matching:** Cuando una variable ya está enlazada a un valor, el operador `=` intenta _coincidir_ con ese valor, no re-enlazar la variable. El `^` (pin operator) fuerza a Elixir a usar el _valor actual_ de la variable en el patrón, en lugar de intentar re-enlazarla.
    - **Uso:** Útil cuando quieres que un patrón coincida con el valor de una variable existente, en lugar de asignar un nuevo valor a esa variable.
```ex
name = "Martín"
# Esto intenta que el valor de 'name' (que es "Martín") coincida con el segundo elemento de la tupla.
{:ok, ^name, _} = {:ok, "Martín", 40} # Coincide
# {:ok, ^name, _} = {:ok, "Carlos", 40} # MatchError, porque "Carlos" != "Martín"
```
#### 2. Operaciones con Tipos de Datos Básicos

Elixir proporciona módulos específicos para trabajar con cada tipo de dato, y un módulo genérico para colecciones enumerables.

- **Inmutabilidad de Datos:**
    
    - **Concepto Clave:** Todos los tipos de datos en Elixir son **inmutables**. Esto significa que cualquier operación que "modifique" un dato (ej: añadir un elemento a una lista, actualizar un valor en un mapa) en realidad devuelve una _nueva_ versión del dato con los cambios, dejando el original intacto.
    - **Impacto:** Para persistir los cambios, siempre debes reasignar el resultado de la operación a una variable (ya sea la misma o una nueva). Esto es fundamental para la programación funcional y la concurrencia.
    
- **Módulos de Referencia (`i` en IEx):**
    
    - Para saber qué funciones están disponibles para un tipo de dato, usa `i <tipo_de_dato_vacío>` en IEx (ej: `i []` para listas, `i {}` para tuplas, `i %{}` para mapas). Esto te indicará el módulo de referencia (ej: `List`, `Tuple`, `Map`).
    
- **Listas (`List` Module):**
    
    - **Agregar Elementos:**
        
        - **Al final:** Usando el operador de concatenación `++`.
```ex
[1, 2] ++ [3, 4] # [1, 2, 3, 4]
```
**Al inicio:** Usando el operador `|` (cons operator). Es más eficiente para añadir al principio.
```ex
0 | [1, 2, 3] # [0, 1, 2, 3]
```


- - **Obtener Elementos:**
        
        - `hd(list)`: Obtiene el primer elemento (head).
        - `tl(list)`: Obtiene el resto de la lista (tail).
        
    - **Eliminar Elementos:**
        
        - `List.delete_at(list, index)`: Elimina el elemento en un índice específico.
        
    
- **Tuplas (`Tuple` Module):**
    
    - **Tamaño Fijo:** Las tuplas tienen un tamaño fijo y no están diseñadas para agregar o eliminar elementos dinámicamente.
    - **Obtener Elementos:** `elem(tuple, index)`: Obtiene el elemento en un índice específico.
    - **Modificar Elementos:** `put_elem(tuple, index, new_value)`: Devuelve una _nueva_ tupla con el valor modificado en el índice dado.
    - **Eliminar Elementos:** `Tuple.delete_at(tuple, index)`: Devuelve una _nueva_ tupla sin el elemento en el índice.
    
- **Mapas (`Map` Module):**
    
    - **Sintaxis Abreviada:** `%{key: value}` para claves átomo.
    - **Insertar/Actualizar:** `Map.put(map, key, value)`: Inserta una nueva clave-valor o actualiza una existente.
    - **Extraer Valores:**
        
        - Acceso directo por clave (si es átomo): `map.key` (ej: `person.name`).
        - `Map.fetch(map, key)`: Devuelve `{:ok, value}` o `:error`.
        
    - **Eliminar Elementos:** `Map.delete(map, key)`: Elimina una clave-valor.
    
- **Módulo `Enum` (Colecciones Enumerables):**
    
    - **Concepto:** Tanto las listas como los mapas (y otras colecciones) implementan el protocolo `Enumerable`. Esto significa que el módulo `Enum` proporciona un conjunto común de funciones para trabajar con cualquier colección enumerable.
    - **Funciones Comunes:** `Enum.at(collection, index)`, `Enum.find(collection, predicate)`, etc. Esto promueve la reutilización de código y la consistencia.
    - **Tuplas NO son Enumerables:** Es importante notar que las tuplas **no** implementan `Enumerable` porque su tamaño fijo y su propósito las hacen diferentes de las colecciones iterables.
    

**Conclusión:**

El _Pattern Matching_ es una herramienta expresiva y poderosa para la desestructuración y el control de flujo en Elixir, fundamental para escribir código funcional y legible. La comprensión de la **inmutabilidad** de los datos es clave para trabajar eficazmente con los tipos básicos del lenguaje, ya que todas las "modificaciones" resultan en nuevas estructuras de datos. El uso de módulos específicos (`List`, `Tuple`, `Map`) y el módulo genérico `Enum` proporciona un conjunto rico y consistente de herramientas para la manipulación de datos.





