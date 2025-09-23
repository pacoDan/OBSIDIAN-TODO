Final ZonaPropi
ARQ
1) 
	1) un crontask que verifique cada hora y revisando las N horas restantes de cada plan de los usuarios
	2) Se le puede notificar por mail, considerando agregar un componente (otro backend conectado por api rest) solo para poder notificar
	   Aclaracion teorica:
	   en WebHooks o Push based B o el servidor avisa cuando haya terminado, es decir cuando haya recibido la notificacion
	   A  o un interesado le enviar un callback a B(el servidor) para que ejecute luego de haber terminado la ejecución
2) 
	1) ==se le notificaria de forma asincronica las consultas es decir NO es necesario por ejemplo que desde el servidor se pregunte cada momento si hay notificación  y menos que se ejecute todo el tiempo metido en un loop infinito  (por si jamas llega haber notificacion), generaría una carga innecesaria.==
   ==Se podría implementar webhooks o push based y el usuario esporadico envia un callback al componente notificador para avisar al usuario.==
	2)  El objetivo también es notificar de forma inmediata.
3) Para acelerar el trafico estatico lo podemos alojar en una CDN para acelerar la entrega de estos archivo hacie el cliente y acelerar el trafico, bajando el consumo de trafico del servidor.
   Despues el tema de los archivos no estaticos, como por ejemplo las consultas a la base de datos, se puede usar una cache, que este entre el servidor  y la base de datos.

Persistencia
A)
Como me quedo los Planes,  lo de joined en la parte de planes, preguntar en PlanGratuito

Dominio
Como queda la clase PlanGratuito

Final DataCat







---















Final Mis Gastos




