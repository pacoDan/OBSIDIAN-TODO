### Persistencia
![[Pasted image 20241220223412.png]]
Sera necesario persistir las entidades.
Motivaciones y la motivación principal
las rutinas generadas según la motivación personalizado de la persona
El der debe verse maso menos asi:
![[Pasted image 20241220091107.png]]
#### para mapear la colección de contactos
En la clase Deportista
agregar las líneas antes en la lista de mails
```java
class Deportista{
	//todo
	@ElementCollection  
	@CollectionTable(name="deportista_contactos", joinColumns = @JoinColumn(name="deportista_id"))  
	@Column(name="contacto")  
	private List<String> contactos;
	//todo
}
```
luego quedaría asi para que el Deportista soporte muchos contactos:
![[Pasted image 20241219185548.png]]
![[Pasted image 20241219185048.png]]
##### mapear las motivaciones
se debe usar un converter para mapear las clases hijas
```java
@Converter(autoApply = true)  
public class MotivacionConverter implements AttributeConverter<Motivacion, String> {  
    @Override  
    public String convertToDatabaseColumn(Motivacion motivo) {  
        if(motivo instanceof BajarDePeso) return "BajarDePeso";  
        if(motivo instanceof Mantener) return "Mantener";  
        if(motivo instanceof Tonificar) return "Tonificar";  
        else return null;  
    }  
    @Override  
    public Motivacion convertToEntityAttribute(String dbData) {  
        if(dbData.equals("BajarDePeso")) return new BajarDePeso();  
        if (dbData.equals("Mantener")) return new Mantener();  
        if(dbData.equals("Tonificar")) return new Tonificar();  
        else return null;  
    }  
}
```
Y en la clase Deportista las anotaciones en `motivacionPrincipal`:
```java
@Getter  
@Setter  
@Entity  
@Table(name = "Deportista")  
public class Deportista {  
	// ...
    @Convert(converter= MotivacionConverter.class)  
    @Column(name="motivacion")  
    private Motivacion motivacionPrincipal;
    // ...
}
```
para aca se ve la columna
![[Pasted image 20241219200940.png]]
![[Pasted image 20241219201936.png]]
#### mapeo los ejercicios como clases recursivas, los ejercicios que combinan 
debo mapear la lista de ejercicios que mapean con la misma clase Ejercicio
```java
@Getter  
@Setter  
@Entity  
@Table(name = "Ejercicio")  
public class Ejercicio {  
	// ...
	@ManyToMany  
    private List<Ejercicio> ejerciciosQueCombinan;  
	// ...
}
```
el der resultante queda asi:
![[Pasted image 20241219204535.png]]
