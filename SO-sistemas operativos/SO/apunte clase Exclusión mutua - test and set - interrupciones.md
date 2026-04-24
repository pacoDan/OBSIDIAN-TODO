Deshabilitar interrupciones no garantiza la exclusión mutua
por que esto no funcionaria en una arquitectura multiprocesador

### Exclusión mutua: 
- Soporte de hardware: 
Una es deshabilitar interrupciones, ejemplo:
```c
while(1){
//deshabilitar int
//seccion critica
//habilitar interrupciones

//test
}
```
- Aunque haya muchos procesadores, tendrían en común la memoria principal. 
Ejemplo de **instrucciones atómicas**.
	- leer y escribir
	- leer y comprobar 
#### Instrucciones maquinas especiales
##### Instrucción Test and Set  (comprueba y establece)
```c
//esta funcion se realiza atomicamente, no está sujeta a una interrupcion
boolean testAndSet(int i ){
	if(i==0){
		i=1;
		return true;
	}
	else return false;
}
```
