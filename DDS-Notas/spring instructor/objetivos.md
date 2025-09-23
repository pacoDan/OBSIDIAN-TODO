
ver los endpoints
probar  añadir la mascota con la seguridad
crear turno con la seguridad
explicar como spring secutity puede que usuarios no esporádicos interactúen con el servidor backend


http://localhost:8082/swagger-ui/index.html

al añadir swagger
```xml
<!-- https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-starter-webmvc-ui -->
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.5</version>
</dependency>
```
http://localhost:8080/swagger-ui/index.html
http://localhost:8082/v3/api-docs




sin seguridad
```java
@Bean  
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
    http  
            .csrf().disable() // Deshabilitar CSRF si no es necesario  
            .cors().and() // Habilitar CORS  
            .authorizeHttpRequests()  
            .anyRequest() // Permitir todas las peticiones  
            .permitAll() // Sin restricciones de autenticación  
            .and()  
            .httpBasic(); // Autenticación básica  
    return http.build();  
}
```
dentro de 
```java
@Configuration  
public class SecurityConfig {  
    @Bean  
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
        http  
                .csrf().disable() // Deshabilitar CSRF si no es necesario  
                .cors().and() // Habilitar CORS  
                .authorizeHttpRequests()  
                .anyRequest() // Permitir todas las peticiones  
                .permitAll() // Sin restricciones de autenticación  
                .and()  
                .httpBasic(); // Autenticación básica  
        return http.build();  
    }  
    @Bean  
    public PasswordEncoder passwordEncoder() {  
        return new BCryptPasswordEncoder();  
    }  
}
```
### Explicación de los Cambios
1. **`csrf().disable()`**: Deshabilita la protección CSRF. Esto es común en APIs REST, pero asegúrate de que sea seguro en tu contexto.
2. **`cors().and()`**: Habilita CORS (Cross-Origin Resource Sharing), lo que permite que tu API reciba peticiones de diferentes dominios. Asegúrate de configurar CORS adecuadamente si necesitas restringir ciertos orígenes.
3. **`authorizeHttpRequests().anyRequest().permitAll()`**: Permite que cualquier solicitud a cualquier endpoint sea aceptada sin necesidad de autenticación.
4. **`httpBasic()`**: Configura la autenticación básica. Si decides permitir todas las peticiones, es posible que no necesites esta línea, pero la he dejado para que puedas usar autenticación básica si decides implementarla más adelante.
### Consideraciones de Seguridad
- **Seguridad**: Permitir el acceso a todos los endpoints sin autenticación puede ser riesgoso. Asegúrate de que esto sea lo que realmente deseas y considera implementar medidas de seguridad adicionales, como la validación de tokens o la autenticación de usuarios.
- **CORS**: Si decides habilitar CORS, asegúrate de configurarlo adecuadamente para permitir solo los orígenes que consideres seguros.
- **Desarrollo vs. Producción**: Este tipo de configuración puede ser útil durante el desarrollo, pero es recomendable restringir el acceso en un entorno de producción.

aca con la seguridad que es lo mismo que si esto no estaría
```java
@Bean  
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
    http  
            .authorizeHttpRequests()  
            .anyRequest()  
            .authenticated()  
            .and()  
            .httpBasic();
    return http.build();  
}
```

```sh
curl -u admin:admin123 http://localhost:8082/turnos
```