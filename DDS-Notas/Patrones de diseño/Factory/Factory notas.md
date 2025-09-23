para crear **objetos basado en una superclase**, posibilitando que las subclases creadoras alteren el tipo de objetos a retornar en su proceso de fabricación.

1)
El patrón sugiere que en lugar de usar el operador `new()` se invoque a un método **fabrica** que se encargue de la creación de los objetos. Estos objetos son llamado **productos**. 
2)
Internamente el método usara el operador `new()`
3)
Las clases fabricas, estarán basadas `en una  clase/interfaz comun`, esto nos permite intercambiarlas según sea requerido.
4)
Los `productos` retornados por `fabricas` deben estar basados `en una  clase base o una interfaz`.
Ejemplo:

### Pasos 1 y 2
Creamos una super clase/interfaz Product que definirá la estructura base de todos los productos. Todas las sub clases/implementaciones de la super clase/interfaz Product se consideran de tipo Product también, pues comparten la misma estructura (no sé si sería bueno mencionar las relaciones de herencia/implementación vistas en el curso anterior).
### Pasos 3 y 4
Creamos una super clase/interfaz Factory que devuelva objetos que sean de tipo Product. No importa cuál. Por último, creamos fabricas concretas (o también fabricas especificas) para cada producto en particular. Estas fabricas concretas heredan/implementan de la super clase/interfaz Factory. . De esta forma, todos nuestros productos siguen una estructura base, y todas nuestras fabricas siguen una estructura base también.

![[explicacion diagrama factory.png]]

![[diagrama factory.png]]


Implementación:

[[Factory JS implementación]]
[[Factory TS implementación]]


Pros de Factory:
- No nos preocupamos de como están construidos
- **Evitamos** acoplamiento alto entre los elementos creadores y los productos
- La creación de productos sucede en **un único punto**
- agregar nuevos productos no requiere modificar el código existente, **lo extiende**.
Contras de patrón Factory

