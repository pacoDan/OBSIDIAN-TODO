Teórico
### 1)
#### a)
Una característica es lograr una alta cohesión, es decir saber bien la responsabilidad de una clase por ejemplo, con verlo saber que es lo que hace y que solo haga eso
Por ejemplo la clase `EnviarMail`, viendo esa clase sabemos que hace, sabemos su responsabilidad y no hace otra cosa mas que eso, si tiene mas responsabilidades menos cohesivo será
Otra característica es que pensar en la Flexibilidad
Tenemos dos tipos de flexibilidad que es la `Extensibilidad` y `Mantenibilidad`
La Extensibilidad es agregar nuevas características o nuevas features pero con poco impacto
Ejemplo si a la clase `Tramite` le agrego mas métodos a esa clase de deberia impactar menos.
La mantenibilidad es modificar nuevas características pero que se haga con menos esfuerzo
Por ejemplo si a la clase `Tramite` le modificamos el método `costoFinal()` esa modificación nos tendría que costar poco en modificarlo.
#### b)
Un principio solid es es la primera
la Single Responsability Principle o principio de responsabilidad única: 
cada clase solo debe tener *una* sola responsabilidad  o una  sola parte de la funcionalidad del sistema, un ejemplo de esto es evitar la clase "Dios", una clase que esta llena de funcionalidades vitales del sistema
Esa responsabilidad debe estar y ser vista en la clase misma.
Un Code smells
es el parámetro largo, es decir no recibir por ejemplo 10 parámetros que ni bien eso se puede encapsular con un solo parámetro con una clase aparte
por ejemplo en los controlller o clase service si queremos recibir datos de un producto, no recibimos precio, ni nombre, ni genero y mas datos por cada parámetro
sino que estaría encapsulado en una clase aparte llamada por ejemplo `BusquedaProducto`
### 2)
#### a)
Falso, el Diseño de sistemas incluye al Diseño de software., ya que Diseño de software se encarga de la parte mas intangible de diseño de sistemas.
#### b)
Verdadero, mas bien lo que se encuentra categorizado es el atributo *Fiabilidad* como subcaracteristica de esta característica.
#### c)
Falso. Solo en paradigma orientado a objetos ya que no solo atributos, sino que permite encapsular métodos.
#### d)
Falso, solo dice que  una prueba fu exitosa (ya que encontró fallas), no que el diseño fue correcto, ya que la falla es solo la manifestación de un defecto.
#### e)
Falso. Solo es una herramienta que permite abstraer el uso de código fuente de algún lenguaje, por ejemplo Spring en en lenguaje Java.
#### f)
Falso, pueden hacer también referencia a los requisitos funcionales, por ejemplo que el sistema funcione en otro sistema operativo también, que es un req no funcional (suponiendo que el sistema le funcione en almenos en un sistema operativo) y que  esta en los atributos de `Compatibilidad` mas precisamente en la **Interoperabilidad**  (sub característica de Compatibilidad) que permite que dos componentes puedan intercambiar información y utilizar información intercambiada.
### 3)
#### a)
Es la *Recuperabilidad*, ya que esta sub característica de Fiabilidad indica que un nivel especificado de funcionamiento, en este caso 10 horas año
#### b)
es la *Confidencialidad*, dentro de Seguridad, que indica protección de acceso a datos.
#### c)
*Capacidad para ser modificado* teniendo en cuenta la cualidad de diseño de Mantenibilidad (esta cualidad permite hacer cambios con menos esfuerzo) pero al tener menos esfuerzo suponemos que se hará en menos tiempo.
