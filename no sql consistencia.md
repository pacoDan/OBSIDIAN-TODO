6)

Consistencia Fuerte: Prioriza que los datos sean correctos y actualizados en todo momento. Cualquier lectura devuelve el dato más reciente, incluso si para lograrlo se debe sacrificar la disponibilidad. Es típica de sistemas como mongodb.

Consistencia Eventual: Prioriza la disponibilidad, aceptando que los datos pueden ser temporalmente inconsistentes entre réplicas. Asegura que, con el tiempo, todos los nodos convergerán al mismo estado si no hay nuevas escrituras. Es el modelo de bases de datos como Cassandra


8)
 MongoDB está parado en el segmento CP (consistency y partition tolerant) por lo que para satisfacer requerimientos no funcionales de availability (alta disponibilidad) debería escoger un motor como Cassandra, cuyas características nativas lo encuadran en el sector AP (availability y partition tolerant)*

(Indicar verdadero o falso y justificar)

La afirmación es correcta según lo explicado en las fuentes sobre el Teorema CAP.

MongoDB es CP: Sacrifica la disponibilidad.

Cassandra es AP: Se especifica que Cassandra se encuentra en el espacio AP (disponibilidad y tolerancia a particiones), priorizando estas dos propiedades a expensas de la consistencia.

Availability (Alta Disponibilidad): La disponibilidad se define como la garantía de que los datos estén siempre accesibles. Dado que Cassandra (AP) prioriza la disponibilidad nativamente, es la elección lógica cuando la alta disponibilidad es el requisito principal, a diferencia de MongoDB (CP) que la sacrifica.


5) Un cluster es un grupo de servidores interconectados a través de una red que trabajan como si fueran un único dispositivo de procesamiento y permite compartir recursos mediante soluciones de almacenamiento en redes como NAS o SAN.*

Explique:
Basado en las fuentes, un clúster es un grupo de servidores (o nodos) que se configura para trabajar en conjunto.

En MongoDB, esto se manifiesta de dos maneras principales:

**Replica Set (Conjunto de Réplicas):** Un grupo de nodos donde se replican los mismos datos para garantizar disponibilidad y evitar un punto único de falla12. Por ejemplo, un _replica set_ puede tener tres nodos23.

**Sharding (Particionamiento):** Un clúster más complejo donde los datos se distribuyen entre múltiples _replica sets_ (llamados _shards_)45. Esto permite escalar horizontalmente y manejar grandes volúmenes de datos67. Un proceso llamado _Mongo S_ actúa como un proxy o mapeador que permite ver todo el clúster como una única base de datos.
