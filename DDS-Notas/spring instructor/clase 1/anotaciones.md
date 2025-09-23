### Consideraciones

- **Anotación `@Component`**: Esta anotación permite que Spring detecte la clase como un componente y la registre en el contexto de la aplicación. Esto significa que se ejecutará automáticamente cuando la aplicación se inicie.
    
- **Interfaz `CommandLineRunner`**: Al implementar esta interfaz, el método `run` se ejecutará después de que la aplicación haya iniciado, lo que es ideal para inicializar datos.
