## ¿Qué es un SSO?
Es un componente que permite tener acceso a múltiples aplicaciones ingresando solo con una cuenta a los diferentes sistemas y recursos.
Es posible acceder mediante una única “contraseña” y se desea evitar el ingreso repetitivo de estas cada vez que el usuario se desconecte del servicio.
Para los usuarios supone una gran comodidad ya que identiﬁcándose solo una vez es posible mantener la sesión válida para el resto de las aplicaciones que hacen uso del SSO.
## Características
• Acelera el acceso de los usuarios a sus aplicaciones
• Reduce la carga de memorizar diversas contraseñas
• Fácil de implementar y conectar a nuevas fuentes de datos
• Al fallar SSO se pierde acceso a todos los sistemas relacionados
• Suplantación de identidades en los accesos externos de los usuarios
## Componentes: CDN
• Una red de entrega de contenido (CDN) está formada por un grupo de servidores distribuidos geográﬁcamente que trabajan juntos para ofrecer una entrega rápida de contenido de Internet.
• Permite la transferencia rápida de activos necesarios para cargar contenido de Internet, incluidas páginas HTML, archivos js, css, imágenes y vídeos.
• Puede ayudar a proteger sitios web contra algunos ataques maliciosos comunes, como los ataques de denegación de servicio distribuido (DDOS).
## CDN: Ventajas
• Mejora de los tiempos de carga del sitio web
• Reducción de los costos de ancho de banda
• Aumento de la disponibilidad de contenido y la redundancia
• Mayor seguridad del sitio web
## Atributos de Calidad (Arquitectónicos)
Aquellos atributos de calidad que –casi- siempre podemos evaluar son:
• Eficiencia de Desempeño – Utilización de recursos (“Performance”)
• Fiabilidad – Disponibilidad
• Fiabilidad – Tolerancia a fallos
• Seguridad (en general)
### Tradeoffs entre Atributos de Calidad
Los Atributos de Calidad pueden entrar en conflicto unos con otros:
• Performance vs. Seguridad
• Seguridad vs. Disponibilidad (aunque están vinculados)
• Performance vs. Modificabilidad
Se deben evaluar los múltiples atributos de calidad con el objetivo de Diseñar un Sistema “Good Enough” para los Stakeholders.
# _Bonus - Posible Estrategia de Abordaje para decisiones a realizar sobre Arquitectura_
**1.**     Plantear o Comprender el Escenario de Aplicación 
**2.**     Plantear el Problema a Resolver.
**3.**     Enumerar el Atributo de Calidad que está en juego, y definirlo, de esa manera entendemos que nos referimos a lo mismo.
**4.**     Justificar con aspectos técnicos la solución/abordaje propuesto. 
## Ejemplo para aplicar:
_Suponiendo y considerando que el Sistema cuenta con una arquitectura web Stateful, con varios servidores atendiendo solicitudes de forma simultánea, ¿Cómo resolvería el siguiente problema reportado por los usuarios?_
_“Varios usuarios han reportado que, mientras utilizan la plataforma (previamente logueados), el Sistema los vuelve a llevar a la pantalla de Inicio de Sesión, teniendo que volver a ingresar sus credenciales para continuar con su labor.”_
**1.**  **Escenario de Aplicación:** Se cuenta con una arquitectura de varios servidores que guardan (de alguna manera) la sesión del usuario. Delante de estos Servidores tengo un Balanceador de Carga. 
**2.**  **Problema a Resolver:** Que el Usuario no tenga que loguearse nuevamente o que no se pierda su sesión.
**3.** **Atributo de calidad en juego:** En este caso podemos analizarlo desde la Disponibilidad o Usabilidad (si consideramos que el sistema sigue funcionando, pero se pierde calidad en la experiencia del usuario)
- **Disponibilidad**: Se trata de la capacidad de un sistema, a ser accesible y utilizable por los usuarios/procesos cuando ellos lo requieran.
**4.** Para resolver esta situación se pueden proponer diferentes abordajes:
- **Balanceador con Sticky-Session:** El balanceador de carga enviará al Usuario siempre al mismo Servidor que lo envió por primera vez. En caso de que el Servidor no se encuentre disponible, seguirá perdiendo la sesión.
- **Espacio de Almacenamiento de Sesión Compartida**: Sumar un Componente a la Arquitectura que guarde las sesiones y sea compartido por todas las instancias de Servidor. Por ejemplo, una Base de Datos Clave-Valor como Redis.



