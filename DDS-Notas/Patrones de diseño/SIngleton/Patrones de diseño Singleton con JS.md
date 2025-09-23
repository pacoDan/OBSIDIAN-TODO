# Patrones creacionales
## - Singleton
Patron que asegura una única instancia a un objeto garantizando un punto global de acceso.

- Optimización. Recursos compartidos. > Asegura que la modificaciones de software se haga desde un unico punto de acceso
- Constructor (C) operador new(). Solución crear un método estático que actúa como C este llamara a C privado que creara y guardara un objeto en una variable estática ("cache")
#### **¿De que se trata singleton?**

En un patrón que nos permite asegurarnos **que no se pueda crear mas de una instancia de un objeto.**

Con esto aseguramos un **único punto global de acceso** a la instancia.

Este también tiene elementos por los que podría ser conocido como un anti-patrón.

#### **¿A que problemáticas podría dar solución?**

- Cuando queremos asegurar el acceso a un recurso compartido en diferentes partes de la app.
    Suena similar a lo que hace una Biblioteca de Manejo de Estados (Como Vuex, Redux, o NgRx)
- Cuando queremos que la modificación al recurso compartido se lleve a cabo en un solo punto de acceso.
    Un ejemplo para ello seria crear un método en la clase, donde se pueda modificar el estado interno de ese único objeto.
    

#### **Solución**
- El patrón sugiere hacer privado el constructor de la clase para evitar hacer uso del operador new().
- Crear un método estático que actué como “constructor” y que tras bambalina llame al constructor privado, para crear un objeto que estará guardado en una variable estática que funcionara como caché.


Código:
[[Singleton JS]]
[[Singleton TS]]
Contras:
- Vulnera el principio de la responsabilidad única: el patrón resuelve dos problemas al mismo tiempo (creación de las instancias y acceso de esa instancia)
- Complejidad incrementada en ambientes de múltiples hilos. ¿ Como hacer que muchos hilos no creen un objeto Singleton múltiples veces?
- Complejidad a la hora de crear pruebas unitarias. Debido al uso de elementos estáticos.
- Si en las 10 mil peticiones, usan una única instancia de acceso a la base de datos.
Pros:
- es inicializada **solo cuando se requiere** por primera vez
- **Certeza** de que solo existira una sola instancia de esa clase
Cuando usarlo:
- Cuando se requiera un único punto de acceso compartidos
- Ejemplo: bibliotecas de manejo del estado.

Reto:
![[reto patron de diseño.png]]

## - Factory
- Abstract Factory
- Builder
- Prototipe
