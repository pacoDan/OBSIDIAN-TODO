#### Arquitectura
1)
a)
Los componentes que son necesarios son un balanceador de carga, para que pueda soportar 3 instancias mas es un **API Gateway**
Entiendo que estas alertas deben darse a usuarios específicos, lo cual se contempla funciones como **autenticación, el registro, el SLL y el equilibrio de carga**.
También puede ser **Service Registry** dado que puede ayudar a **identificar servicios y para tiempo real** y es importante distinguir el servicio de Alerta  

b)
No grafique la base de datos, esta prohibido que use una misma base de datos para los tres?
**Si o si deben usar cada Alerta su propia base de datos?**
El servicio de **Alerta, como no tiene estado interno como para guardar o procesar**, sino solamente para poder notificar. Lo cual **no es necesario tener una base de datos propia**, y **sino las tres bases de datos deben sincronizarse**.
![[Pasted image 20241220181218.png]]
2)
a)
El tipo de cliente que usare es ligero o server side rendering
por que no necesito procesamiento, mucho menos en los tótems
También necesito que la pagina se actualice cada momento ya que el usar tótem (si el tótem funciona pesado puede no funcionar en algunos momentos lo cual esta afectado la disponibilidad)
De la misma forma en la cual comunico con el tótem se debe implementar el cliente ligero en los BackOffice de los vigilantes y para reportes (mas aun aprovechando el servicio de alertas)

---
Considero que las peticiones que deben llegar son solo los contenidos de los videos, imágenes, avisos, no el contenido de la pagina en si, además como es vigilancia, priorizo la usabilidad, escalabilidad (por ejemplo se usan varios servicios de API Gateway) y mantenibilidad como para elegir cualquier tipo de datos o protocolos como para transferir datos multimedia (por el servicio de streaming multimedia).

b)
Solo si fuera hibrida, ya que si fuera nativa llevaría mucho mas tiempo en desarrollarlo. En cambio si fuera hibrida me puede simplificar el tiempo ya que esa misma interfaz la usaría para que lo usen los vigiladores también esa misma UI de usuario.

3)
a)

Persistencia:
