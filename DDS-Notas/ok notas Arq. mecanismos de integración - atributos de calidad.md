- Integración por base de datos:
	- hay pool  o Polling != de webhooks
	- Un componente puede insertar en otra tabla
	- -Seguridad
	- Asincrónica
- Cola de Mensajes: a veces solamente si el proceso  o la aplicación es asincrónico
	- Acumula transacciones 
	- Cuanto resuelve asincrónicamente 
	- Cuando el sistema el que hago request no quiere escalar y limita la cantidad de Requests
- API REST:
	- Puede venir la factura o datos para hacer la factura 
	- MANTENIBILIDAD: cambia algo de los REQs debo cambiar algo de mi código como para mandar un nuevo JSON

Atributos de calidad: compara en que requerimientos puede chocar y luego decidir en base a eso
- MANTENIBILIDAD: Es bastante acoplado
- INTEROPERABLE: En ambos sistemas debe funcionar sin transformaciones
- EXTENSIBILIDAD:
- PERFORMANCE o Eficiencia: 
	- En tiempo de respuesta, uso de recursos en el lado de cliente o servidor 
	- Eficiencia en tiempo de respuesta
	- Escalabilidad:
	-  -> TIEMPO DE RESPUESTA
	- Ejemplo: el ingreso de un invitado al abastecimiento debe realizar en menos de 3 segundos desde que el mismo exhibe su elemento de ingreso.
- DISPONIBILIDAD: 
	- Ejemplo: el sistema deberá estar en funcionamiento sin sufrir caídas durante los eventos.
- SEGURIDAD:
	- Ejemplo: garantiza autenticidad
- ESCALABILIDAD: 
- USABILIDAD: 
- STATELESS:
	- Ejemplo: HTTP, sin estado
- STATEFUL: guarda dato
	- Si al correr guarda datos
	- El chip o SIM cuando se guarda el numero de CHIP o celular

pull / push-based -> espera activa "se molesta mucho a la otra parte"



En ventas si o si pensar en trazabilidad (pensar todos los cambios de estado)

Desnormalizar: 
	- Por performance: con datos calculados, pero despues hay que actualizar ese dato por cada cierta frecuencia



