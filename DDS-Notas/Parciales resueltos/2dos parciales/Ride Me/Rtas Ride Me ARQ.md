### Arquitectura
Consideraciones. 
La aplicación tiene  resultados que mostrar en la pantalla de inicio lo cual esos resultados siempre los debe llevar cargados y calculados, pero como no hace ninguna operación con esos resultados (numero de bicicletas usados por ejemplo) su actualización puede ser asincrónica
además  el sistema debe llevarse en 4 meses, lo cual no lo agrandaría de repente a microservicios por que llevaría mas tiempo desarrollarlo, además los admins  como operan en una oficina aparte es su trabajo es mas dedicado, cuentan con una app desktop mínimamente.
#### 1)
Entendiendo que nuestro Sistema debe poseer una capa de presentación gráfica, ¿Qué tipo de interfaz propondría implementar para los ciclistas? Justifique adecuadamente su respuesta entendiendo que se poseen 4 meses en total para lanzar el Sistema a producción. 
##### a. Aplicación mobile nativa. 
Una aplicación me dará dos proyectos  (la de desktop y la de mobile), habrá dos proyectos a desarrollar y mantener, lo cual llevaría mas tiempo y no se cumplirá en 4 meses
##### b. Aplicación mobile híbrida. 
Esta opción permite que solo se mantenga y desarrolle un solo proyecto,
Esta opción permite que los admins y ciclistas usen el sistema con la misma interfaz lo cual facilitaría mucho en tema de soporte y errores.
##### c. Cliente liviano
Con que el usuario en el navegador perciba que en su navegador pueda gestionar las bicicletas rápido, el hecho de que sea rápido solo resuelve un requerimiento no funcional, lo importante es que pueda sacar la bicicleta y reportar fallas
##### d. Cliente liviano desacoplado de la lógica de negocio.
las mismas consideraciones que la anterior, pero es aun mas desventajosa por que desacoplar la lógica de negocio puede implicar complicar mas los resultados que se deben mostrar en la pantalla de inicio. Desacoplarla será mas reutilizable si pero a costa de un mayor diseño y mayor desarrollo lo que conllevaría mas tiempo.
#### 2)
El sistema da entender de que si se cambiaria la interfaz de usuario para los admins
Da a entender que ya existe u a interfaz
La cual yo no la cambiaria para nada, ya que los admins la usan de manera back-office y no es necesario ninguna modificación alguna para cambiar esta interfaz de usuario.
#### 3)
el proceso de reconocimiento no debe presentar demoras y con la conexión considerablemente penalizada por el costo y conexión
ese reconocimiento facial debe procesarse localmente y esa base de datos de las caras de los ciclistas en cada tótem o app móvil
Lo mismo para el fichaje de retiro y devolución
En todo caso para actualizar las nuevas caras eso se hará de forma periódica en momentos de conexión a internet, es decir cuando no sea penalizada la conexión, para corroborar si el ciclista esta registrado o en el sistema.
#### 4)
Si a los ciclistas se les cobra mensualmente, no hay necesidad de hacerlo de forma sincrónica, sino que puede ser de forma asincrónica con WebHooks,  aunque también es valida por api rest.
Ambas son validas. PEro reafirmo el uso de WebHooks por el hecho de que puede demorarse en la transacción de un ciclista lo cual haría demorar para varios ciclistas si fuera api rest (que es sincrónico), por eso es mas adecuado usa un proceso CRON que ejecute mensualmente el mecanismo de WebHook.