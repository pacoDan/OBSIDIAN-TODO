**Problemas de la SPA**
Indexación y el SEO: Como las SPA cargan todo su contenido dinámicamente a través de JavaScript, los motores de búsqueda como Google pueden tener dificultades para indexar y clasificar el contenido. Esto se debe a que los motores de búsqueda generalmente escanean el HTML estático de una página web para encontrar contenido relevante y palabras clave, lo que puede ser difícil con una SPA. Como resultado, el SEO (Search Engine Optimization) puede ser un desafío para las SPA. 
Alta dependencia de JavaScript: Las SPA se basan en JavaScript para generar el contenido, lo que significa que si un usuario deshabilita JavaScript en su navegador o si el navegador no admite JavaScript, la aplicación no funcionará correctamente. Esto puede ser un problema para los usuarios que tienen una conexión de internet lenta o para aquellos que utilizan navegadores antiguos o dispositivos con recursos limitados. Necesita más recursos del navegador: Las SPA suelen ser aplicaciones complejas que requieren una gran cantidad de recursos del navegador para funcionar correctamente. Esto puede hacer que las aplicaciones sean lentas y poco receptivas en dispositivos más antiguos o en dispositivos con una capacidad de procesamiento limitada. Además, las SPA suelen requerir una gran cantidad de memoria del navegador, lo que puede llevar a problemas de rendimiento si se utilizan varias aplicaciones SPA en la misma sesión de navegación. 
Seguridad: Como las SPA se basan en JavaScript para generar el contenido, existe la posibilidad de que un atacante pueda inyectar código malicioso en la aplicación. Esto puede ser especialmente preocupante si la SPA se utiliza para transmitir información confidencial, como datos de tarjetas de crédito o información de inicio de sesión. Además, dado que las SPA suelen comunicarse con el servidor a través de API (Interfaces de Programación de Aplicaciones) en lugar de páginas web tradicionales, los desarrolladores deben ser especialmente cuidadosos para garantizar que la comunicación entre la SPA y el servidor sea segura.

Se refiere al uso de diversas estrategias y técnicas, y no necesariamente se limita a los microfrontends. La elección de la estrategia dependerá de la naturaleza específica de la aplicación y de los problemas de rendimiento que se estén tratando de abordar.

Algunas técnicas o estrategias pudieran ser:

- Optimización de código.
- Lazy Loading.
- Optimización de imágenes y recursos.
- División o partición en bundles más pequeños.

Cuando el profe dice que tenemos que cortar el SPA, probablemente se refiera a estas técnicas para aliviar las cargas iniciales de un SPA:

1. La más común, el uso de componentes asíncronos mediante el acceso con el router del frameworks a usar
2. Con microfrontends, personalmente prefiero con el mismo framework de frontend para no tener un sancocho con espagueti
3. Microservicio con escalamiento vertical donde cada servicio tenga su propio frontend SPA

