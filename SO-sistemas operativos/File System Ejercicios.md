Ejercicio 11

### a) Tipo de link a crear

Se debe crear un **link simbólico (Soft Link)**. Esto se debe a que, cuando los archivos se encuentran en **diferentes volúmenes** (o sistemas de archivos), no es posible utilizar un _hard link_. Los enlaces simbólicos funcionan apuntando a una ruta, la cual el sistema operativo puede interpretar incluso si cruza límites de particiones o volúmenes.

### b) Cantidad de archivos en el sistema para ejecutar Java 8

En el caso de un **soft link**, existen **dos archivos** distintos en el sistema que permiten la ejecución:

1. El archivo binario original (`/usr/lib/java-8/bin/java`).
2. El archivo del enlace simbólico mismo (`/etc/alternatives/java`), el cual es un archivo independiente con su propio inodo que contiene la ruta al original.

### c) Escenario con versiones en el mismo volumen

Si ambas versiones están en el mismo volumen, se pueden utilizar tanto enlaces simbólicos como **enlaces duros (Hard Links)**.

- **Si se usa un Hard Link:** No existen dos archivos, sino **un único archivo** (un mismo inodo) al que se puede acceder a través de **dos entradas de directorio** diferentes.
- **Si se usa un Soft Link:** La situación es idéntica al punto anterior: **dos archivos** (binario y enlace).

### d) Situaciones basadas en el punto a) (Soft Link)

- **i) Se elimina el binario original:** El enlace simbólico queda **roto**. El archivo `/etc/alternatives/java` seguirá existiendo, pero al intentar usarlo fallará porque su contenido (la ruta) apunta a un destino inexistente.
- **ii) Se elimina el link:** Solo se borra el acceso directo. El archivo binario original en `/usr/lib/java-8/bin/java` **permanece intacto** y funcional.
- **iii) Se eliminan ambos:** Se pierden tanto el acceso directo como el binario original; el programa ya no existe en el sistema.

### e) Situaciones basadas en el punto c) (asumiendo Hard Link)

Cuando se utiliza un enlace duro, el sistema mantiene un **contador de enlaces** para el inodo.

- **i) Se elimina `/usr/lib/java-8/bin/java`:** El archivo **no se borra del disco**. Como todavía existe la entrada `/etc/alternatives/java` apuntando al mismo inodo, el contador de enlaces baja a 1 y el archivo sigue siendo totalmente ejecutable desde la ruta del link.
- **ii) Se elimina `/etc/alternatives/java`:** Similar al caso anterior, el archivo **sigue existiendo** en su ruta original. Solo se ha eliminado una de las formas de acceder a él.
- **iii) Se eliminan ambos:** Solo cuando el contador de enlaces **llega a cero** el sistema operativo procede a liberar los bloques de datos y borrar definitivamente el archivo del sistema.