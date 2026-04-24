7- En terminos de Deploy ¿ Que significa hacer Rollback?¿ Y Rollfordward?
Explique diferencias y de un ejemplo de cada uno de posibles usos
RTA.:
La diferencia depende de la necesidad del negocio que subre el SW, se puede tener una estratrateia de Deploy
Rollback es cuando estas deployando y justo cae un error, y no hay necesidad de tener ese ultimo Deploy, se puede volver atras
Hay casos en que no se puede volver atraz y si o su debemos dejar algo funcionando en produccion:
Ejemplo: Un sistema de semaforos inteligente en que su principal requerimiento es detectar la cara y obtener los datos, luego su proxima release es foto+el color de cara, si el deploy falla volver a la anterior por que lo importante es sacar la foto, esto es rollback
Con Rollfordward, un sistema de etiquetado de productos, su principal requerimeinto es detallar lo mas posible a un producto, mientras mas detalles tenga, mejor se cumple el requerimeinto  si el deploy falla, hay que sacar un PROXIMO release pronto, si tiene  mas o la misma cantidad de detalles

6- En que consiste un Nightly Build, para que sirve y con que frecuencia se ejecuta durante un proyecto?
RTA.:
sirve para asegurar que siempre cada build este funcionando y generar reportes de informacion de estabilidad, y su frecuencia es cada dia (tarde o noche)

8- ¿ Que diferencias existe entre el enfoque de "diseñar software para ser testeado" y el enfoque tradicional de pruebas
RTA.:
diseñar software para ser testeado abarata pruebas
y el enfoque tradicional de pruebas...

11- ¿ Como puede el uso de oraculos de pruba ayudar a los testers a organizar de manera conveniente la existencia de defecto en el software?
RTA.:
Hay que tener diferentes perspectivas, se mira las diferentes perspectivas para ver si una falla
12- ¿ Cual es la diferencia fundamental entre testing exploratorioy el texting basado en scripts?
RTA.:
Testing Exploratorio
	- se empieza jugando hasta encontrar un error
	- metodo mas rapido e inciso para resolver un test
	- aprende de la aplicacion
- testing basado en scripts
	- Es cuando los casos de prueba los tengo escritos en algun lado, y segun sus deficiones se siguen sus condiciones

13 - Explique las diferencias entre testing estatico vs dinamico, y el testing caja blanca y caja negra, de ejemplos de cada uno
RTA.:
caja blanca: se diseña pruebas leyendo el codigo
caja negra: se orueba lo que el software debe hacer. Esta prueba se basa en los datos que produce la salida
test estatico: que se compile por asi decirlo
test dinamico: cuando se testea el tiempo de ejecucion


14 - Explique el metodo GQM. Agregue que otros factoresson importantes a la hora de armar un plan de metricas
RTA.:
GQM: establece objetivos, luego preguntas o cuestionario y luego metricas que permitan poder explicar la metricas
otros factores: importante en las metricas son , esas metriecas deben poder ayudar a responder las preguntas, y confirmar si los mejoras del proceso cumpliran su objetivo.















