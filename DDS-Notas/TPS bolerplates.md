
## Comando Maven (Archetype oficial más simple):

```bash
mvn archetype:generate \
  -DgroupId=com.tuempresa \
  -DartifactId=proyecto-dominio \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```
```bash
mvn archetype:generate \
  -DgroupId=ar.edu.utn.frba.ddsi \
  -DartifactId=ddsi-tp-Macowins \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```
## Estructura generada (muy simple):

```md
proyecto-dominio/
├── pom.xml
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/tuempresa/
│   │           └── App.java
│   └── test/
│       └── java/
│           └── com/tuempresa/
│               └── AppTest.java
```

2. **Crea la carpeta de dominio/models:**
```bash
mkdir -p src/main/java/com/tuempresa/dominio/models
mkdir -p src/test/java/com/tuempresa/dominio/models
```

## Comandos útiles después:

```bash
# Compilar
mvn clean compile

# Ejecutar tests
mvn test

# Compilar + tests
mvn clean test

# Empaquetar
mvn clean package
```
