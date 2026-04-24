Nodo: 
-> Dispositivo mobile
-> Smartphone
-> Servidor de base de datos (donde corre el server)

- apache Cassandra se uso como estilo arquitectonico P2P
- Objetivos de  desnormalizacion:
	- no siempre mejora la performance
	- Ej trivial: desnormalizar el precio de kas facturas (por  consistencias de datos)
- Hibernate es un ORM del tipo DataMapper
- Lazy LOADING hidrata los datos al momento de su ejecuciion
- App de tipo Uber  es de tipo hibrido
- VER PATRON PIPELINE
- En ingenieria de Software un FRAMEWROK es un **marco de trabajo**
- Estilo <-> macro
- Patron <-> En detalle
- Vista Logica 
	- Diagrama de clases
	- Diagrama de paquetes
- Vista de Despliegue . Vista de desarrollo
	- Diagrama de componentes 
	- Diagrama de paquetes
- Vista FISICA (nodos en donde se guarda desplegado cada uno)
- SOA: logica funcional a varios servicios
- SOA -> ESB: componente principal (Ejemplo: Spring Integration)
	- -> Se llega a servicio mediante un contrato

Microservicios: mas funcionalidades mejor organizada/organizacion de los equipos
	- agilidad: los equipos pueden hacer cosas distintas al mismo tiempo
	- por cada servicio hay un equipo completo
	- Resiliencia: Adaptabilidad a su entorno, se adapta a lo que necesita el sistema
	- cada servicio es altamente cohesivo
- API GATEWAY: quien va a redirigir a distintos servicios
- Administracion: coloca servicio en los nodos, **identifica errores**
- Deteccion de servicios
- Service Discovery: Vista de Servicios y sus nodos
- Circuit Braker: Saca de la vista un servicio que no esta activo
- Componentes:
	- pueden implementar interfaz
	- podrian tener dependencias
	- Es despegable
	- Es reemplazable
	- Se encapsula la implementacion
	- Expone un conjunto de interfaces
	- pueden tener dentro otros componentes
- Nodo:
	- tiene memoria y servicio de proceso
	- llamado unidad de proceso

---

1) considerando que se quiere implementar una arquitectura de Microservicios
	a) ¿ Que componentes  fundamentales de soporte se deberian de incorporar?
	b) ¿ Cuales son sus funciones principales?
	RTA.:
	Hay mas de un servicio de capacidad empresarial y despleglado independientemente
	Hay minimamente una GESTION CENTRALIZADA
	Hay distintas tecnologiasnde almacenamiento de datos
	Los servicios son son pequeños e independientes y estan debilmente acoplados
	Cada servici se puede implementar de manera independientemente
	Las API se comunican entre si mediante API bien definidos
SOA orientado a arquitectura a servicios nivel enterprise (organizacion u enterprise), dos enfoques diferentes
Microservicios: aplicativo
SOA: comunidad de aplicaciones, lebemente acoplados siempre el valor de negocio por encima de la estrategia tecnica.



ARQ
1) Considerando que se quiiere implementar una arquitectura de Microservicios
	1) Que componentes fundamentales de soprte se  deberian de incorporar?
	2) ¿Cuales son sus funciones principales?
	RTA
	a) Primero que consume tiempo y esfuerzo, pero los componentes necesarios son: 
		Administracion
		Detecciion de servicios
		API Gateway o Puertaa de  Enlace API
	b) ¿ Cuales son  sus funciones principales 
	RTA
	Funciones:
		- Administracion: 
			- coloca el servicio en los nodos
			- indentifica errores
			- reequilibra los servicios entre nodos
		- Deteccion de Servicios:
		- mantiene la lista de servicios y sus nodos donde se encuentran.
	- Puerta de enlace de API: Es que va a redirigir distintos servicios. Los clientes llaman directamente servicios a este componente . Agrega respuesta de varios servicios, también funciona como autenticación, el registro, la terminacion SSL y el equilibrio de carga.


	