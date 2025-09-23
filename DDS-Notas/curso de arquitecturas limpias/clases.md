```insta-toc
---
title:
  name: Table of Contents
  level: 1
  center: false
exclude: ""
style:
  listType: dash
omit: []
levels:
  min: 1
  max: 6
---

# Table of Contents

- clase 4 cuando aplicar y cuando ignorar este tipo de arquitecturas
    - Sistemas donde la mantenibilidad es un atributo crucial
    - Sistemas donde la testeabilidad es muy importante
    - Sistemas con múltiples integraciones
    - Flexibilidad para cambiar una implementación
- ¿Cuándo ignorar arquitecturas limpias?
    - Sistemas sencillos
    - Sistemas con un tiempo de vida corto
    - Sistemas con ninguna o muy pocas integraciones
- clase 5 principios de diseño
- clase 6 arquitectura hexagonal  puertos y adaptadores
    - ¿Por qué un hexágono?
- clase 7 arquitectura cebolla, otra arq de referencia
    - Datos adicionales:
- clase 8 Clean Architecture hay 4 grandes capas en esta arq
    - Datos adicionales:
- clase 9 ejemplos del mundo real
    - Caso Netflix
    - Elementos en el dominio:
    - Elementos en la capa externa:
    - Caso Makrwatch
    - ¿De que le ha servido a esta startup construir arquitecturas limpias?
- clase 11 Detalles sobre el dominio
    - ¿Qué no corresponde al dominio?
    - Situaciones a evitar con el dominio
    - Formas de organizar el dominio
- Clase 12 Organizando el dominio con Script de transacción, manera de organizar el dominio
    - ¿Cuándo usar script de transacción? es cuando se comparta lo menos posible el código y procedimientos de gran tamaño
    - Problemas del script de transacción
- clase 13 Inyección de dependencias
    - Inversión de Control (IoC)
    - Inyección de Dependencias (DI)
    - Formas de hacer inyección de dependencias
- clase 14 Modelo de dominio
- clase 16 capa de servicios
- Capa de servicios, tambien llamada capa de aplicacion
- Casos de uso
- clase 17 CQRS, otra forma de como podemos organizar el dominio
- clase 18 acceso a datos, en la capa externa
    - ¿Qué sentido tiene sacar la base de datos a la infraestructura?
- clase 19 Patrón Repository: separando el dominio con acceso a datos
    - ¿Cómo separar el dominio del acceso a datos?
- clase 20 Aplicaciones web y APIs
    - Errores a evitar
- clase 21 Integraciones y patrón Adapter
    - Ejemplos comunes
    - Patrones de diseño
    - Patrón Adapter
- clase 22 Pruebas
- clase 23 Dobles de prueba, en como se pueden hacer pruebas de la capa de aplicación en las pruebas de integración, alguna de las pruebas de integración sean unitarias
```

### clase 4 cuando aplicar y cuando ignorar este tipo de arquitecturas

#### Sistemas donde la mantenibilidad es un atributo crucial
Es un sistema que existirá mucho tiempo o será manipulado por mucha personas, lo cual es esencial poder habilitar la posibilidad de realizar cambios dentro del software de manera sostenible.
#### Sistemas donde la testeabilidad es muy importante
Claro que todo debe ser testeable, pero hay contextos en donde la testeabilidad debe ser mucho más prolija y segura, como lo puede ser en proyectos bancarios o de salud. pero otras que pueden no necesitar testeos como aplicaciones multimedia o de video.
#### Sistemas con múltiples integraciones
Si tenemos múltiples integraciones y que no nuestro dominio no se vea afectado por nuestras integraciones, una gran alternativa es utilizar arquitecturas limpias.
#### Flexibilidad para cambiar una implementación
Pueden haber dependencias inestables que en algún momento queramos cambiar, entonces, para proteger nuestro dominio podemos usar arquitectura limpia por la desacoplable que es.
### ¿Cuándo ignorar arquitecturas limpias?
Claro que no sirven para todos los escenarios
#### Sistemas sencillos
Si hablamos de un simple CRUD, no tiene mucho beneficio mas que traer complejidad al mismo.
#### Sistemas con un tiempo de vida corto
Por ejemplo, una prueba de concepto o un proyecto MVP, ya que es muy posible que tal proyecto terminémoslo desechando o upgradearlo por uno mejor cuando las condiciones lo permitan.
#### Sistemas con ninguna o muy pocas integraciones
Si el sistema solo tiene una pura conexión a la base de datos y nada más, o nos relacionamos con solo una o dos aplicaciones, no es muy relevante utilizar arquitecturas limpias.
### clase 5 principios de diseño 
**Principios SOLID**

- _**S** : **Principio de Única Responsabilidad.**_ Un módulo debería tener una sola razón para cambiar.
- _**O** : **Principio de Abierto Cerrado.**_ Un módulo debería estar abierto a extensiones y cerrado a modificaciones.
- _**L** : **Principio de Sustitución de Liskov.**_ Las clases derivadas deben poder sustituirse por sus clases base.
- _**I** : **Principio de Segregación de la Interfaz**_ Haz interfaces que sean específicas para un tipo de cliente
- _**D** : **Principio de Inversión de Dependencias**_ Los módulos de alto nivel no deberían depender de los módulos de bajo nivel.
Ejemplo de O:
![[Pasted image 20250122123005.png]]
Ejemplo de D:
La idea no debe ser esta
![[Pasted image 20250122124719.png]]
pero la idea si debe ser esta
![[Pasted image 20250122124704.png]]
### clase 6 arquitectura hexagonal = puertos y adaptadores
Esta arquitectura está compuesta por:
1. **Aplicación:** Es la capa de negocio diseñada como un hexágono.
2. **Puertos:** Son aquellos puentes hacia la aplicación.
3. **Adaptador:** Realizan la conversión de algo externo hacia lo que la aplicación entiende, es decir, será el ajuste hacia algo que el puerto pueda entender.

**Regla de la dependencia:** Los elementos externos tienen conocimiento de lo que hay hacia dentro (en la aplicación), pero nunca al revés, la aplicación no tiene conocimiento de estos adaptadores que se están construyendo alrededor de la aplicación.

**Actos primarios:** Son aquellos adaptadores que son capaces de iniciar interacciones en el sistema, por ejemplo una interfaz gráfica o un API Rest que se comunican con una API de clientes y ésta finalmente es quien interactúan con la aplicación.
![[Pasted image 20250123102640.png]]
****************************************Actores secundarios:**************************************** Son aquellos adaptadores que son de alguna forma notificados de acciones que ocurren en la aplicación. Son parte del flujo.
![[Pasted image 20250123102703.png]]
#### **¿Por qué un hexágono?**
Para dar espacio para insertar los puertos y adaptadores que sean necesarios.
![[Pasted image 20250123100526.png]]


### clase 7 arquitectura cebolla, otra arq de referencia
El modelo de dominio es la capa mas interior de la cebolla.
Las entidades deben estar amarradas a la persistencia.
El modelo de dominio solo debe depender de si mismo.
![[Pasted image 20250123103109.png]]
Importante: el modelo de dominio solo depende de sí mismo, en ningún momento tiene dependencia hacia las capas que lo están rodeando. Se denomina “modelo de objetos”, “capa de dominio” o “entidades de dominio”.
- **Servicios de dominio o servicio de objetos o capa de repositorio**: una capa más arriba. Aquí encontramos las interfaces de esos repositorios (base de datos) para acceder a los datos. Están definidas pero no implementadas. Contiene reglas del negocio, pero un elemento fundamental es que habrán interfaces que van a representar repositorios para acceder a los datos. Se van a definir las interfaces pero no se van a implementar. Se denomina “servicio de objetos” o “capa de repositorio”
    ![[Pasted image 20250123105339.png]]
- **Servicios de aplicación o capa de servicios**: una capa más arriba, envuelve la capa anterior, aca hay lógica también, donde se encuentran las operaciones específicas. Aquí no hay interfaces. Lógica de la aplicación puede estar repartida entre los servicios de aplicación y servicios de dominio. Se denomina “capa de servicios”.
	![[Pasted image 20250123103302.png]]
hasta ahora va quedando asi, Esto se denomina el **núcleo del sistema**:
![[Pasted image 20250123110355.png]]

- La capa externa o las pruebas o pruebas unitarias o pruebas de integración:  esto es externo al núcleo, incluye las diferentes pruebas que queremos usar en nuestra aplicación, así como la interfaz gráfica y la infraestructura.
	- Pruebas: Unitarias, de Integración y ayudar a testear que todo este funcionando correctamente
	 ![[Pasted image 20250123103345.png]]
	- Interfaz grafica: Ajeno al dominio del problema y que es algo que puede cambiar con el tiempo
		![[Pasted image 20250123110704.png]]
	- Infraestructura: tambien capa externa, se tienen elementos como acceder a un sistema de archivos, aplicaciones de terceros e integraciones varias que de alguna forma no quepan en la interfaz grafica y pruebas.
	 ![[Pasted image 20250123104053.png]]
    
Esta capa externa rodea al **************dominio**************.
#### **Datos adicionales:**

- Propuesta por **********Jeffrey Palermo********** en ********2008********.
- Arquitectura conocida principalmente en el ecosistema ********.NET********.
Se utiliza principalmente en el ecosistema .NET.


### clase 8 Clean Architecture hay 4 grandes capas en esta arq
Existen las siguientes capas:
![[Pasted image 20250123111813.png]]
1. **Entidades:** Capa central, son reglas de negocio que aplican a nivel empresarial y que son comunes a múltiples aplicaciones.
2. **Casos de uso:** Reglas de negocio más específicas de la aplicación, reglas mas generales de la aplicación.
3. **Adaptadores de interfaz:** Son el puente entre elementos muy específicos o detalles hacia lo que entendemos en el core de nuestra aplicación, principalmente en los casos de uso y las entidades.
4. **Frameworks y drivers:** Detalles puntuales del sistema, tales como la base de datos, la web, sistema de archivos y todo lo que ocurre allí será convertidor por la capa previa para que pueda ser utilizada por los casos de uso y las entidades.

#### ************************************Datos adicionales:************************************

- Fue descrita por ************************Robert Martin************************ en ********2012********.
- Se apoya en las ideas de la ********************************************arquitectura hexagonal********************************************, **************cebolla************** y otras.
- El mayor reto que tiene es que presenta huecos en su implementación, no se profundiza en grandes detalles,  por lo que se busca tener una apreciación por parte de diferentes arquitectos de software para llevarla a cabo.


### clase 9 ejemplos del mundo real
#### Caso Netflix
Necesitaban crear una arquitectura que les permitiría trabajar con **datos de múltiples fuentes** y para ello crearon una arquitectura que denominaron “hexagonal” y esta arquitectura limpia esta  compuesta y definida por los siguientes elementos:
#### **Elementos en el dominio:**
- Entidades.
- Repositorios.
- *Interactors*. Hacen referencia a los casos de uso
#### **Elementos en la capa externa:**
- Fuentes de datos (data sources).
- Capa de transporte.
![[Pasted image 20250123120305.png]]
Se dieron cuenta que tenían unas dependencias inestables y que estaban sujetas a cambios.
![[Pasted image 20250123120355.png]]
![[Pasted image 20250123120520.png]]

#### Caso Makrwatch

Tenían una arquitectura de 3 capas que no daba lugar a múltiples integraciones, por lo que optaron por construir una nueva aplicación con arquitectura limpia compuesta por los siguientes elementos:
- Entidades.
- Servicios.
- Infraestructura (Plataforma, redes sociales, mensajería, REST).
![[Pasted image 20250123120855.png]]
![[Pasted image 20250123121031.png]]
Un ejemplo de proyecto que usa arquitectura limpia tiene la siguiente estructura de directorios:
.
├── main
│   ├── domain
│   │   ├── services
│   │   ├── interfaces
│   │   ├── entities
│   │   └── common
│   └── infraestructure
│       ├── rest
│       └── messaging
└── test
    ├── unit
    └── integration
#### **¿De que le ha servido a esta startup construir arquitecturas limpias?**
- Proteger la lógica de negocio de cambios en las integraciones. Ya que empezó a  haber muchísimas integraciones y esas integraciones pueden cambiar, se traen aplicaciones y se traen otras.
- Probar más fácil la lógica de negocio.
- Crear buenos hábitos en el equipo de desarrollo. Es bueno que una arq ayude a crear buenos hábitos en el equipo. Es mas valiosa en personas junios en el equipo, reduce la carga mental de pensar y revisiones de código.

### clase 11 Detalles sobre el dominio
El dominio es la razón de ser del sistema. Es la razón por la cual existe
Tiene varios nombres:
- Lógica de negocio.
- Lógica de dominio.
- Negocio.
**“El dominio involucra lo que debe hacer el negocio, haya o no sistemas de información”.**

****************Ejemplo:**************** Un sistema de supermercado
**¿Qué corresponde al dominio?**:
- Calcular descuentos.
- Verificar inventario.
#### **¿Qué no corresponde al dominio?**
- Si los empleados usan una aplicación web o una consola para procesar una compra. Esto esta en la capa de interfaz.
- Si los empleados tienen lectores de códigos de barras o no. (por que esto puede estar en la capa externa o la capa de infraestructura)
#### Situaciones a evitar con el dominio
- Referenciar la capa externa desde el dominio.
```js
import Correo from 'external'; 
const Servicio = () => {};
```
Siempre va de afuera hacia adentro y no de adentro hacia afuera
![[Pasted image 20250123131148.png]]
- Mencionar elementos de la capa externa.
```js
function notificarUsuario() { 	
	let enviarSMS = true; 	
	// ... 
}
```
- Retornar datos con un formato específico (datos que sean específicos a una interfaz algo a la capa externa del cliente).
```js
return '<span>Cliente ' + 'no existe</span>';
```
- Permitir que la lógica de negocio se filtre.
    - Se tiene un botón “Guardar usuario” en un formulario y en el manejador de evento de click pueden ocurrir cosas como:
        - Validar campos del formulario.
        - Validar si el usuario existe.
        - Decide si insertar el usuario o actualizarlo.
#### Formas de organizar el dominio
- Script de transacción.
- Modelo de dominio. Que es un enfoque fuerte orientado a objetos.
- Capa de servicios.
- Casos de uso.
- CQRS. Que es otra forma de arquitecturas limpias.

### Clase 12 Organizando el dominio con Script de transacción, manera de organizar el dominio
_Patterns of Enterprise Application Architecture. Martin Fowler._
Este script de transacción organiza la lógica en procedimientos. **Cada procedimiento maneja una única solicitud de la capa externa**. De esa forma manejamos nuestro código de manera transaccional.
Hay dos maneras de organizar estos procedimientos:
**una es por, una jerarquia de herencia:**
	Se estaría viendo de esta forma:
![[Pasted image 20250123143934.png]]
**Después una clase por cada procedimiento que se muestra en la aplicación**: funciona bien en aplicaciones pequeñas, pero es fácil tener problemas de cohesión
![[Pasted image 20250207182009.png]]
Una estructura general usando arquitecturas limpias, ver las carpetas domain, external etc:
![[Pasted image 20250207182240.png]]
![[Pasted image 20250207182249.png]]

#### **¿Cuándo usar script de transacción? es cuando se comparta lo menos posible el código y procedimientos de gran tamaño**
- Aplicaciones con poca lógica de negocio.
- Problemas simples.
#### Problemas del script de transacción
- Se vuelve difícil de mantener cuando la lógica crece.
- Lleva a código duplicado.
- No aprovecha la programación orientada a objetos.

### clase 13 Inyección de dependencias
pero antes 
inversión de control: es cuando un objeto o un programa cede el control a alguien más.
Una forma , popular, de hacer o implementar  inversión de control, es inyección de dependencias,
#### Inversión de Control (IoC)
Un objeto o programa cede el control a alguien más.
#### Inyección de Dependencias (DI)
Es una forma de implementar inversión de control. Es una técnica donde a un objeto le proveen las dependencias que necesita.
#### Formas de hacer inyección de dependencias
- Por constructor.
- Por setter.
- Por método.
- Por interfaz. (menos común, también llamado inyector)
![[Pasted image 20250123151249.png]]

### clase 14 Modelo de dominio
Es una representación en objetos del dominio, que incluye comportamiento y datos de manera simultánea y no **anémicos** (con datos pero sin comportamiento y viceversa, es como OOP a medias).
Modelo de dominio ≠ Modelo de base de datos
Ejemplo, de una clase ligada con persistencia, no es un modelo de dominio:
![[Pasted image 20250123152506.png]]

**¿Qué puede incluir un modelo de dominio?**
- Entidades.
- Objetos de valor.
- Herencia.
- Relaciones. Donde conectan las entidades entre si
- Patrones de diseño. Distintos enfoques entre clases.

### clase 16 capa de servicios
### Capa de servicios, tambien llamada capa de aplicacion

Es un buen complemento para un modelo de dominio, porque permite abstraer el dominio y hacerlo más fácil de consumir.
Ofrece una fachada para consumir fácilmente el modelo y de dominio y coordinar la respuesta.
Con la fachada podemos esconder los detalles que No son relevantes para un Entidad Externa.
![[Pasted image 20250203175402.png]]

### Casos de uso

Contiene reglas de negocio específicas de la aplicación. Coordinan el flujo de datos desde y hacia el modelo de dominio.

Se suele implementar una clase por caso de uso.

**********Nota:********** Los casos de uso se suelen encontrar con los sufijos ********************Interactor********************, **************Service************** o **************************CommandHandler**************************.



### clase 17 CQRS, otra forma de como podemos organizar el dominio
_Command Query Reponsability Segregation_
Se divide en, dos ideas,  ****************comandos**************** y **consultas**.
****************Comandos****************
- Escritura.
- Cambian el estado.
******************Consultas******************
- Lectura.
- Retornan resultados.
Esta idea se puede aplicar a varios niveles:
- Métodos.
- Clases.
- Servicios. (puede haber backend para leer y otro backend para escribir)
- Bases de datos.

modelo normalmente como la tenemos
![[Pasted image 20250203183100.png]]
ahora, para leer y escribir es, tener dos modelos, un modelo para consulta y otro modelo para comandos:
![[Pasted image 20250203183214.png]]
un ejemplo de la estructura es:
![[Pasted image 20250203183408.png]]
![[Pasted image 20250203183533.png]]


![[Pasted image 20250203183553.png]]
un proyecto especifico para la interfaz:
![[Pasted image 20250203183614.png]]

----
Por que en el ejemplo el comando esta retornando el tipo ActionResult<int> no deberia ser void ya que los comandos no retornan nada?
RTA.: Esta es una duda frecuente con los comandos en CQRS. Sin embargo, el punto crítico aquí es que **no hagan consultas**.

Para facilitar el desarrollo con CQRS, es válido regresar información que nos ayude a saber el resultado del comando (en este caso, el ID del objeto que se creó).

[Este es un artículo](https://vladikk.com/2017/03/20/tackling-complexity-in-cqrs/) muy interesante si deseas profundizar en este y otros temas adicionales de CQRS.



### clase 18 acceso a datos, en la capa externa
#### **¿Qué sentido tiene sacar la base de datos a la infraestructura?**
Migrar de base de datos NO es la mejor razón.
Las razones para realizar este procedimiento son:
1. No es tu única fuente de datos. Puedes llegar a tener diversas fuentes como:
    1. Bases de datos legacy (Utilizadas en otras aplicaciones en un esquema organizacional).
    2. Archivos (formato JSON, XML o TXT).
    3. Sistemas de terceros, por ejemplo CRM.
    4. Motores de búsqueda, por ejemplo Algolia o Elasticsearch.
2. Necesitas probar bien. Esto significaría tener una base de datos o tener dichas fuentes de datos a la mano para poder realizar las pruebas.
![[Pasted image 20250203194915.png]]
### clase 19 Patrón Repository: separando el dominio con acceso a datos
#### ¿Cómo separar el dominio del acceso a datos?
Una forma es usando el **patrón Repository**, el cual ofrece una fachada que da la apariencia de estar usando colecciones y esconde los detalles específicos sobre el funcionamiento de la persistencia.
La interfaz hace parte de la **capa de la aplicación** mientras que la implementación hace parte de la capa externa.
![[Pasted image 20250203210008.png]]
**************Ejemplo de como esta estructurado un repositorio**************:
![[Pasted image 20250203205318.png]]
Se tiene una interfaz denominada **************************************ProductRepository**************************************, la cual define la firma de los métodos:
- add(Product)
- findById(int)
- remove(Product)
Se tiene una clase que implementa la interfaz **************************************ProductRepository************************************** y es denominada ******************************ProductoRepositoryImpl******************************, la cual tiene la implementación de cada uno de los métodos mencionados con anterioridad:
- add(Product)
- findById(int)
- remove(Product)
De esta forma se podría crear una nueva clase que implemente esa interfaz y pueda realizar operaciones de lectura o escritura de diferentes fuentes de datos, sin tener el dominio atado a una implementación en específico, que es básicamente lo que se busca en un arquitectura limpia.
### clase 20 Aplicaciones web y APIs

Hacen parte de la *capa externa*
#### Errores a evitar
1. Poner lógica de negocio en la vista. Evitar que la logica de negocio se filtre.
2. Poner lógica de negocio en los controladores. Ejemplo cuando se recibe solicitud de la vista, y ver a que parte del dominio invocar la operacion, es importante que los controladores sean pasarellas.

Con @RestController ya hace la inyeccion de dependenciaas:
![[Pasted image 20250203213043.png]]
con @Bean busca y toma dinamicamente esas dependencias:
![[Pasted image 20250203213127.png]]


### clase 21 Integraciones y patrón Adapter
#### **************************Ejemplos comunes**************************
1. Envío de mensajes.
    1. Correos electrónicos.
    2. Mensajes de texto.
    3. Notificaciones push (web o móvil).
    4. Mensajes de chat (WhatsApp o Telegram).
2. Escritura y lectura de archivos.
    1. Disco.
    2. Almacenamiento de objetos.
    3. Servidor FTP.
3. Comunicación con otros servicios.
    1. Colas de mensajería.
    2. REST.
    3. Llamado de procedimientos remotos (RPC).

#### ************************************Patrones de diseño************************************

Son soluciones recurrentes a un problema de diseño.

#### ******************************Patrón Adapter******************************

Convierte la interfaz de una clase en otra interfaz que el cliente espera. Permite que objetos con interfaces incompatibles trabajen juntos.

****************Ejemplo:****************

Se tiene una clase ************Client************ que utiliza la interfaz **********************************GestorArchivo**********************************, la cual tiene la firma del siguiente método:

- guardar(ruta, contenido)

Se crea una nueva interfaz denominada **********AdaptadorS3********** la cual tiene la firma del mismo método:

- guardar(ruta, contenido)

Se crea una clase ******S3****** que implementa la intefaz **********************AdaptadorS3********************** con la implementación del método:

- put()

Dicho método contiene la implementación propia para guardar o actualizar archivos en S3.

De esta forma cuando el dominio utilice la interfaz **GestorArchivo** estará accediendo a una **interfaz genérica** sin preocuparse por la implementación de la misma, que es básicamente lo que se busca en una arquitectura limpia.


### clase 22 Pruebas
Una característica principal de las arquitecturas limpias es la facilidad de probar (testability, es decir que tan fácil es verificar un programa), ya que tienen separada la lógica de negocio de la capa externa.
ejemplo de como se separa las pruebas  por aplicación y por modelo:
![[Pasted image 20250205191937.png]]
Hay que tener en cuenta que existe una pirámide de pruebas que podemos abarcar en toda una aplicación:
- **Unitarias:** Ubicadas en la parte inferior, las cuales son rápidas, baratas y abundantes. **Son las mas especificas de nuestro código, verifican métodos, clases  y elementos muy puntuales**.
- **Integración:** Ubicadas en la parte media, las cuales no son tan rápidas, consumen más recursos y no suelen ser tan abundantes. **Se tienen una seria de dependencias y tenemos que ver como la manejamos.**
- **Extremo a extremo:** Ubicas en la parte superior, las cuales son lentas, costosas y escasas. **Aca ya hacemos verificación mucho mas completa, UI, base de datos, son pruebas mas elaboradas **
	
**Nota:** Las pruebas sobre el modelo de dominio **deberían ser unitarias** porque éste modelo sólo depende de sí mismo, gracias a que las dependencias van de afuera hacia adentro.
![[Pasted image 20250203221748.png]]
y entre mas pruebas unitarias mejor:
![[Pasted image 20250205193506.png]]

En que parte de la piramide se ubican las pruebas de rendimiento?
a pirámide de automatización de pruebas está pensada desde el punto de vista de funcionalidad, más que de medir atributos como rendimiento.
No trabajo en temas de testing, así que puedo estar equivocado, pero tendería a pensar que están más cerca de la cima de la pirámide.

### clase 23 Dobles de prueba, en como se pueden hacer pruebas de la capa de aplicación en las pruebas de integración, alguna de las pruebas de integración sean unitarias
![[Pasted image 20250205194159.png]]
![[Pasted image 20250205194223.png]]
Problemas con el CDD:
- Acceso lento: ejemplo si al base datos esta alojada lejos y tarda las consultas en las pruebas, luego las pruebas son mas lentas de ejecutar
- Control de resultado: es muy importante saber que respuesta podre obtener para poder testear que  parametros podemos dar, a los elementos de terceros que no CONTROLO.
- Efectos colaterales: imaginemos que testeamos la funcionalidad de testear correros electrónicos y de repente enviamos correo a mucha gente.
- Disponibilidad en ambiente: tener disponibilidad del componente. por ejemplo puede funcionar en produccion  pero no dev y se limita  hacer pruebas locales.
- Acceso costoso: puede existir un componente como una api, en el que no se puede probarlo pero por el hecho de que sea costoso (tiempo y plata), que además de tiempo, la plata es un factor importante ya que  nos puede cobrar por cuantos llamados se hacen. **Osea hay que testear pero tenemos limitaciones**.

y los **dobles de prueba**, son cruciales para hacer pruebas de integración  que superan las limitaciones anteriores.
- Mocks y Stubs: dos de los objetos de pruebas comunes.
	- Desafíos comunes::

- 
Los dobles de prueba (pruebas de integración) son una técnica utilizada en las Arquitecturas Limpias para el desarrollo de software. Estas pruebas se enfocan en validar la interacción y la integración correcta entre los diferentes componentes del sistema. Aquí tienes un ejemplo de cómo se podrían implementar los dobles de prueba en el contexto de las Arquitecturas Limpias:

Supongamos que tenemos una aplicación que sigue la arquitectura limpia y consta de las siguientes capas: la capa de dominio, la capa de aplicación y la capa de infraestructura.

En la capa de dominio, tenemos una clase llamada UserService que es responsable de la lógica relacionada con los usuarios. Esta clase depende de un repositorio para acceder a los datos de los usuarios.

En lugar de utilizar directamente el repositorio real en las pruebas de integración, podemos crear un doble de prueba (mock) del repositorio. Este doble de prueba simula el comportamiento del repositorio real, pero en lugar de acceder a una base de datos, puede devolver datos de prueba predefinidos.

Aquí hay un ejemplo de cómo se podría implementar el doble de prueba del repositorio en Java utilizando un framework de pruebas como Mockito:
```java
import org.example.domain.User;
import org.example.domain.UserRepository;
import java.util.ArrayList;
import java.util.List;
public class UserRepositoryMock implements UserRepository {
    private List<User> users = new ArrayList<>();
    @Override
    public void save(User user) {
        users.add(user);
    }
    @Override
    public User findById(int id) {
        return users.stream()
                .filter(user -> user.getId() == id)
                .findFirst()
                .orElse(null);
    }
    // Otros métodos del repositorio simulados...
}
```

