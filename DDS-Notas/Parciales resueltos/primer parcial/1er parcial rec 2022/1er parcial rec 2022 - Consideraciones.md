![[1er parcial rec 2022.png]] 

Dudas
- en el punto 2.5 sobre si use bien el criterio para poder responder justificar el req de la trazabilidad de los elementos puntos
-  la clase ConfiguracionAccesoria use una clase abstracta pero sin métodos ni atributos pero necesito esa herencia por si los demas elementos tienen configuraciones como Notebook
- si hay mas atributos de calidad a tener en cuenta
-  la clase *Operador* es una clase hija de *Usuario*, *Admin* tambien es una clase hija de Usuario
1. diagrama 
2. Decisiones de Diseño:
	2.1) en el campo de la clase reserva`#Reserva>>espacioEspecifico` puede ser numero de piso del edificio para el evento como algún numero de zona o superficie del lugar del evento, o numero de sala o galpon, que como puede ser muchas cosas la puse como string
	2.2) para conocer la trazabilidad de cuando la reserva pasó de solicitud a Reserva hecha es cuando objetos de la clase `SolicitudDeReserva` pasa a ser atributo de `Reserva`
	2.3 cuando el interesado solicita espacio cuando es necesario, con necesario entiendo que puede que no se tenga o no se de esa info, entonces el campo `#Reserva>>espacioEspecifico puede valer ""`
	2.4  cuando el interesado puede configurar los elementos tipo Notebook me refiero a la clase ConfiguracionNotebook que se detallas esos elementos el campo `#ConfiguracionNotebook>>preconfiguradoPor`  puede valer null ya que es opcional segun el enunciado cuando dice que "puede existir"
	2.5) para conocer la trazabilidad de los elementos  tipo notebooks entiendo que puede referirse a las cantidades que el `SolicitudDeReserva` tener, eso esta encapsulado en el campo `List<ElementoDeReserva>` ya que List da la cantidad, y si se refiere a los tipos de elementos también ya que de List podes sacar e insertar cualquier Elemento
	2.6) 
	Sobre el bloqueo  de los usuarios, se contempla si esta contemplado en alguna lista de tipo  `List<UsuarioBloqueadoPorReserva>`
	2.7)
	sobre la exportación usaría un strategy de la siguiente manera en la que el atributo que comparten  es la reserva, y tener cada clase el tipo de exportación hace que se sepa mas el objetivo a realizar es decir mas cohesión

3.  
La *mantenibilidad* la destaco debido a que puedo modificar mejor los algoritmos de exportacion y notificación con strategy
Tambien le da mas extensibilidad
4. 


#### ejemplos de clases y sus objetos (en las viñetas)
TipoDeEvento
- salaDeReunion
- espacioDeTrabajoPrivado
- espacioDeTrabajoCompartido

EspacioColaborativo
- salaDeReunion
- estadoDeTrabajoColaborativo
- espacioCompartido

ElementoDeReserva // o Elementos su lista de esto en el enunciado seria *Series de elementos o Tipos de elementos*
- sillaExtra
- notebook
- proyector
- conectividad
- audiovisual

MedioDeComunicacion (aca las clases hijas, no objetos)
- Mail
- SMS
- WhatsApp

Accion // esto es un string, ejemplos de estos son
- "descargar archivo"
- "reiniciar equipo"
- etc

Sede -> (tiene) espacio
EspacioColaborativo -> (tiene) ElementoDeReserva

EstadoDeSolicitud (enum)
- AConfirmar
- Confirmado
- Rechazada