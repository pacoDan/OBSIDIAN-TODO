Spring Security Filter chain : en estos filtros de seg de manera encadenada si se rechaza o se aprueba 
Despues sigue el Dispatcher Servlet para el controlador
![[Pasted image 20250316134356.png]]


puede tener hasta mas de 30 filtros
![[Pasted image 20250316134458.png]]

apenas se instale la dependencia el spring security filter chain automaticamente seran interceptadas todas las peticiones que se realicen y seran tratadas todas las configuraciones de seguridad por defecto, tambien lo que hace es crear un user y contrasenia por defecto

citas esa dependencia desde spring initializr

---
## clase 4 usar la autenticación por defecto
por defecto spring secutiry  usa Basic Autentication
![[Pasted image 20250316222920.png]]
cuando la aplicacion usa Basic Autentication
![[Pasted image 20250316223358.png]]
ahora si estamos autorizados por mandar el usuario y pass
![[Pasted image 20250316223500.png]]


en la consola ver los filtros de filter chain 
## ¿Qué es Spring Security y cómo funciona su autenticación básica?
Spring Security es una poderosa herramienta que agrega una capa de seguridad a nuestras aplicaciones, protegiéndolas contra accesos no autorizados. Al agregar la dependencia de Spring Security a tu proyecto, se habilita una configuración de seguridad por defecto. Esta configuración genera automáticamente un usuario y una contraseña genérica que puedes utilizar para acceder a los servicios de tu aplicación de forma segura durante el desarrollo.
### ¿Cómo se utiliza la autenticación básica con Spring Security?
Por defecto, Spring Security utiliza Basic Authentication. Este tipo de autenticación requiere incluir en el encabezado de cada petición HTTP el término `BASIC`, seguido de un texto codificado en Base64 que combina el usuario y la contraseña separados por dos puntos. Te presentamos el paso a paso para entender el flujo de autenticación con Spring Security:
1. **Realización de una petición GET sin autorización**: Si realizas una petición GET a un recurso que requiere autenticación sin el encabezado adecuado, obtendrás una respuesta con estado 401, indicando falta de autorización.
2. **Incorporación del encabezado Authorization**: Si añades el encabezado Authorization con el formato `BASIC` y las credenciales correctas, recibirás una respuesta positiva con estado 200, proporcionando acceso al recurso deseado, como por ejemplo una lista de pizzas en este caso de estudio.
### ¿Cómo gestionar credenciales y debugging en Spring Security?
Cada vez que inicias tu aplicación, Spring Security genera una nueva contraseña por defecto, facilitando el proceso de desarrollo gracias a su seguridad dinámica. Verás esta contraseña en tu consola; puedes copiarla para realizar tus pruebas de autenticación en herramientas como Postman:
```plaintext
Por defecto, el usuario es `USER` y la contraseña es la generada aleatoriamente que aparece en la consola.
```
Además, puedes mejorar el debugging de tu aplicación ajustando los niveles de logging para obtener información detallada sobre cómo maneja Spring Security las peticiones. Puedes hacerlo agregando la siguiente línea a tu configuración:
```properties
logging.level.org.springframework.security.web=DEBUG
```
### ¿Cómo protege tu aplicación el Spring Security filter chain?
Spring Security incluye una cadena de filtros, conocida como `Spring Security filter chain`, que procesa cada petición de forma escalonada y en cascada. Estos filtros son los responsables de:
- Autenticar cada solicitud
- Autorizar el acceso a los recursos
- Proteger tu aplicación contra diferentes tipos de ataques y vulnerabilidades
Es esencial comprender cómo se configuran y funcionan estos filtros ya que son la base de la seguridad en Spring.
Invierte tiempo explorando y experimentando con estas configuraciones. Esto te proporcionará una sólida base en seguridad para el desarrollo de aplicaciones con Spring. Y no olvides, conocer a fondo el funcionamiento de los sistemas de seguridad te otorgará confianza y competencia en tus proyectos futuros. ¡Sigue aprendiendo y mejorando tus habilidades!


---

