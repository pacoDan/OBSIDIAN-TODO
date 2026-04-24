![[Pasted image 20250117070744.png]]
diferencia entre programa y proceso es el punto cuando cargo en memoria.
activa= que se usa en memoria ram y consume cpu
pasiva es que no consume cpu ni memoria ram por que solo esta almacenada como archivo ejecutable y allí están las instrucciones
En el stack están las las variables auxiliares como las que fueron pedidas con malloc y las que se van liberando en el transcurso del programa.
heap, data y text son fijas, el stack es variable
estas 4 cosas se le llama imagen del proceso.
![[Pasted image 20250117072355.png]]
Diagrama de estados:
![[Pasted image 20250117072910.png]]
Las transiciones las maneja el planificador (el sistema operativo).
cantidad de procesos en running al mismo tiempo: **multiprocesamiento**.
cantidad de procesos que tengo en mi sistema actualmente, no necesariamente están ejecutando: **multiprogramación**.
Planificaciones
![[Pasted image 20250123171659.png]]
blocked=en espera= waiting es lo mismo.
Cuando esta suspendido, esos dos estados de abajo, indice que el proceso no esta en memoria ram no es tan asi pero para entender es mejor explicar primero así.
Running a waiting : puede deberse a una syscall, que puede ser de una e/s, y de repente tenga que ejecutar algo externo.
largo plazo: de new a ready y de running a terminated.
mediano plazo: meter a swap o traer  de swap
corto plazo: grado de multiprocesamiento, entre running y ready., Determina quienes estan en running.
extra largo plazo: lo hace el admin del sistema, es cuando limitad el grado de multiprogramacion. Es cuando incidimos en el algoritmo que utiliza, manejar el tamaño de swap y que tanta agresividad queres que haga.

max grado de multiprocesamiento: nro de cores que tengo.
tiempo desperdiciado= es perder tiempo de cosas que son importante pero no es lo principal= overhead.

Ahora a nivel de estructura: PCB
![[Pasted image 20250123175244.png]]
Con el contador de programa: el SO sabe donde se quedo el proceso.
el PSW esta el carry.
Información contable: que cosas fue haciendo, y para auditar el proceso.
el stack heap no esta en el PCB.
pero el PCB si sabe donde buscar el stack.
la imagen es todo lo que necesit para ejcutar el proceso, que es el PCB + stack, heap, data y text.

Cambio de contexto
![[Pasted image 20250123180337.png]]
Contexto: todo lo que necesita el SO para ejecutar un proceso
Un cambio de contexto no implica cambio de proceso, por ejemplo debido a una interrupción o atender una E/S.

pila de sistema == CPU
Si se guarda el contexto pero se que vuelvo a ejecutar el proceso rápidamente, se guarda en la CPU.

![[Pasted image 20250123190210.png]]
la flecha azul es running o ejecutando, y la negra es overhead, osea desperdicio de tiempo.
EL PCB siempre esta en memoria
![[Pasted image 20250123200308.png]]


----
### apuntes de clase ok
SO procesos
Si no hay PCB no se sabe que el procesos existe
#### Cambio de contexto:
- Cambiar el estado, guardar los registros de CPU
- Este tiempo es OVERHEAD -> idle
- Se tratara de minimizar
- podría tener un cambio de modo
```
imagen de como aparece el idle:
----->|------|------->
 exec | idle |exec
```

#### Hilos o procesos ligeros
No comparten esto: 
- stack
- punteros
El context switch es mas rápido
- El PCB tiene punteros a los TCB propios
Hilo main  -> si se termina este, los demás mueren 
Hilo no tiene accesos a la TCB
Que haya paralelismo NO IMPLICA que haya concurrencia

KLT- ULT
KLT: hilos a nivel de kernel,. el SO los conoce => puede controlar
ULT: Bi9blioteca de funciones, se puede planificar de otra forma
**-> ver quien se ocupa de la gestión de KLT y UTL** 
`phtread.join()` // espera a que el hilo termine
`SIGTERM`: al matar el proceso pregunta a sus hijos
Si el hilo se bloquea => todo el proceso también se bloquea.
