Aquí tienes las **top 5 herramientas open source** para generar código Java a partir de diagramas PlantUML de clases (o viceversa, ingeniería inversa):

## 🥇 **1. PlantUML + PlantUmlJavaGenerator (Recomendado)**
```
@startuml
class User {
  -id: Long
  +getName(): String
  +setEmail(email: String)
}
@enduml
```
**Plugin**: [plantuml-java-generator](https://github.com/plantuml/plantuml-java-generator)
- Genera código Java real desde PlantUML
- Soporta paquetes, herencia, interfaces
- Integración con IDEs

## 🥈 **2. Structurizr CLI**
```bash
structurizr export --format plantuml --output diagram.puml
structurizr generate --workspace workspace.dsl
```
- **GitHub**: [structurizr-cli](https://github.com/structurizr/cli)
- Bidireccional: Java → PlantUML → Java
- Excelente para C4 Model + PlantUML

## 🥉 **3. yWorks yEd + PlantUML Export**
```
!theme plain
class Car {
  -engine: Engine
  +accelerate(): void
}
```
- **Descarga**: [yEd Graph Editor](https://www.yworks.com/products/yed)
- Importa PlantUML → genera Java
- Editor visual + exportación código

## 4️⃣ **4. Modelio (UML Modeling Tool)**
```
class Customer {
  +name: String
  +orders: Order[0..*]
}
```
- **GitHub**: [modelio](https://github.com/Modeliosoft/Modelio)
- PlantUML import + Java codegen
- Soporte completo UML 2.5
- Gratuito y profesional

## 5️⃣ **5. Papyrus + PlantUML Integration**
```java
// Generado automáticamente
public class Product {
    private Long id;
    private String name;
    
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```
- **Eclipse Plugin**: Papyrus + PlantUML
- Ingeniería inversa completa
- Generación de código Java/JUnit

## 🚀 **Implementación Rápida (PlantUML → Java)**

```bash
# 1. Instalar PlantUML Java Generator
git clone https://github.com/plantuml/plantuml-java-generator
cd plantuml-java-generator

# 2. Generar código
java -jar plantuml.jar -Sfile=diagram.puml
java PlantUmlJavaGenerator diagram.puml output/
```

## 📊 **Comparativa Rápida**

| Herramienta | PlantUML→Java | Java→PlantUML | IDE | Complejidad |
|-------------|---------------|---------------|-----|-------------|
| **PlantUML Generator** | ✅ Excelente | ❌ | VSCode/IntelliJ | ⭐⭐ |
| **Structurizr** | ✅ Muy bueno | ✅ Excelente | CLI | ⭐⭐⭐ |
| **yEd** | ✅ Bueno | ✅ Bueno | Desktop | ⭐ |
| **Modelio** | ✅ Excelente | ✅ Excelente | Desktop | ⭐⭐⭐⭐ |
| **Papyrus** | ✅ Muy bueno | ✅ Muy bueno | Eclipse | ⭐⭐⭐⭐ |

## 💡 **Recomendación**
Para **diagramas PlantUML → Java rápido**: **PlantUML Java Generator**
Para **proyectos enterprise**: **Modelio** o **Structurizr**

¿Necesitas el **código exacto** para alguna herramienta específica? 😎