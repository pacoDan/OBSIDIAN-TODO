Si quieres un **proyecto Spring Boot listo para exponer un API REST usando repositorios en memoria (sin base de datos todavía)**, podemos usar **Spring Boot CLI** con `spring init` y agregar solo las dependencias necesarias.
Aquí te dejo el comando para generar el scaffolding:
```sh
spring init \
  --dependencies=web \
  --java-version=17 \
  --build=maven \
  --name=demo-api \
  --package-name=com.ejemplo.demo \
  demo-api
```
### **Qué hace esto**
- `--dependencies=web` → añade `spring-boot-starter-web` para crear APIs REST
- Sin `data-jpa` ni drivers → así solo usamos `@Repository` en memoria con listas/mapas
- `--java-version=17` → Java 17
- `--build=maven` → usa Maven (puedes poner `gradle` si prefieres)
- `demo-api` → nombre de la carpeta del proyecto
Ejecutar el proyecto:
```sh
cd demo-api
./mvnw spring-boot:run
```
 ---
 Otro comando cli **Con PostgreSQL y JPA**::
```sh
spring init \
  --dependencies=web,data-jpa,postgresql \
  --java-version=17 \
  --build=maven \
  --name=demo-api \
  --package-name=com.ejemplo.demo \
  demo-api 
```
### 📦 **Qué incluye*
- **`spring-boot-starter-web`** → API REST
- **`spring-boot-starter-data-jpa`** → ORM con Hibernate
- **`postgresql`** → Driver para conectarse a PostgreSQL
- **Java 17**
- **Maven** como build tool
---
💡 Esto te da un **CRUD completo en memoria**, sin tocar base de datos.  
Luego, cuando quieras pasar a **PostgreSQL**, solo reemplazas el repository en memoria por un `JpaRepository` y agregas la dependencia `spring-boot-starter-data-jpa` + el driver `postgresql`.

---
2. **Configurar conexión a PostgreSQL** en `src/main/resources/application.properties`:
```sh
spring.datasource.url=jdbc:postgresql://localhost:5432/mi_basedatos
spring.datasource.username=mi_usuario
spring.datasource.password=mi_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```
Ejecutar:
```sh
./mvnw spring-boot:run
```