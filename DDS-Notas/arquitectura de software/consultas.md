Buenas
tengo consulta sobre del final  20241221, de la tercera de diciembre pasado
en la parte de arquitectura, tengo una confusión en cuando a que se pide

1)entiendo que habla de arquitectura de microservicios en general
a) cuando se pide fundamentar que componentes, se refiere a componente dentro de un nodo como api gateway y service registry (y explicarla que hacen y por que usaría un service registry) , mencionar el balanceador de carga, Circuit breaker, Service Register (como alguna de esta slide de Componentes concretos)
![[Pasted image 20250210140845.png]]
o 
se refiere a Administración , Detección de Servicios y api gateway? tal como esta slide de componentes necesarios, estoy confundido
![[Pasted image 20250210140422.png]]
es bastante confuso/ambiguo como me pide

luego en la 
2)b)
sobre el componente arquitectónico que pide, a priori diría CDN (ya que imágenes y videos son archivos estáticos), pero no se me explicita si solo consistiría solo mostrar y solo peticiones GET o  si en el fondo hay mínimo un ABM de carga de imágenes por parte del usuario lo cual almenos hay un POST y existe un componente llamado "Galería"  (que se encarga de los regalos y la galería valga la redundancia), lo cual ¿es correcto suponer y mencionar que puede existir un componente con su backend ?? (por que otra estrategia para mejorar el escenario seria escalarla horizontalmente con balanceador de carga y minimizar la request  de los cliente a cada componente de "Galería")
3)
esta duda es conceptual, siempre que me mencionen alguna api externa como en este ejercicio siempre esta el patrón Fachada? osea esta mal si no llego a mencionar el patrón fachada
4)
cuando me dice que mecanismos propongo para motivar a los usuarios y sabiendo que los usuarios no vuelven a interactuar, puedo asumir que no se almacena la información de la sesión y fundamentar el stateless, 
o para obtener todos los datos de la sesión a fin de obtener el feedback (como regalos vistos, cual foto se vio por las tiempo para calcular  métricas dentro de la sesión y calcular un feedback), no entiendo como puedo relacionar una estrategia de engagement, esta mal el ejercicio si no menciono alguna estrategia de engagement?



----
Easy tech

![[Pasted image 20250212182336.png]]
![[Pasted image 20250212183527.png]]


---
Hola
una pequeña duda en arquitectura, me genera mucho ruido
En el final de Centro Comerciales Abiertos CCA del la segunda fecha de diciembre
Cuando me hablan de una base de datos "Datos Maestros"
estoy pensando dos cosas
una es que si me dice de forma implícita que hay redundancia en medio y que hay bases "esclavo", según los métodos de replicación ¿puede ser que esa replicación pida minimo  un balanceador para replicar la base de datos y asegurar la disponibilidad en cuanto a datos?
o 
Solo es un nombre y que como toda tabla maestra en esa base de datos hay una tabla desnormalizada?