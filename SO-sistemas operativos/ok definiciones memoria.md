- Segmentación: 
	- No tiene fragmentación externa, de hecho por ser segmento de tamaño variable no tiene fragmentación interna.
	- Sufre fragmentación externa por que pueden dejar huecos
	- No tiene asignación contigua, una petición puede tener distintos segmentos y estos pueden no estar necesariamente contiguos. ==Permite,  múltiples segmentos debidos a programación modular.==
	- No tiene complejidad, para saber la dirección física comprende desde la base hasta base+ limite.
- Paginación:
	- Es sencillo, para buscar espacio vacío para cada pagina se comprobara en un bitmap el espacio libre
	- Fragmentación interna en la ultima pagina

