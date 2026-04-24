
Parece que estás trabajando en un proyecto de refrigeración portátil alimentado por 5V (probablemente un enfriador termoeléctrico, como uno basado en el efecto Peltier, que usa corriente eléctrica para enfriar sin compresor). Sin embargo, mencionas usar gas butano o el de un encendedor (que suele ser una mezcla de butano y propano). Esto sugiere que podrías estar experimentando con un sistema de enfriamiento por expansión de gas (como el efecto Joule-Thomson) o algo similar, donde el gas se expande para crear frío. Si es para un enfriador termoeléctrico puro, el gas no es necesario, pero si lo usas para potenciar o complementar el enfriamiento, aquí va la info.

**Advertencia importante:** Los gases refrigerantes son inflamables y pueden ser peligrosos si no se manejan correctamente. No uses gases tóxicos o ilegales. Consulta leyes locales sobre refrigerantes (por ejemplo, en la UE o EE.UU., algunos están regulados por el Protocolo de Montreal). Siempre prioriza la seguridad: usa en espacios ventilados, evita llamas abiertas y prueba en pequeña escala.

### Requisitos que debe cumplir el gas
Para un sistema DIY de enfriamiento por gas (como expansión o absorción), el gas ideal debe ser:
- **Refrigerante eficiente:** Capaz de expandirse rápidamente para absorber calor (bajo punto de ebullición, alta presión de vapor).
- **Disponible y accesible:** Fácil de obtener en tiendas de camping, ferreterías o como combustible.
- **Seguro:** No tóxico, no corrosivo, con baja inflamabilidad si es posible (aunque la mayoría son inflamables).
- **Compatible:** Debe ser inerte con los materiales de tu setup (tubos, sellos) y presurizable (hasta 100-200 psi en contenedores pequeños).
- **Económico y portátil:** Ligero, en botellas pequeñas para uso móvil.

El butano funciona porque es un hidrocarburo ligero con punto de ebullición bajo (-0.5°C), ideal para enfriamiento por evaporación.

### Alternativas a gas disponibles
Aquí van opciones comunes y accesibles, similares al butano/propano de un encendedor. Estas se usan en refrigeradores portátiles de camping, aerosoles o sistemas DIY. Evita gases como freón (CFC/HFC) si no tienes experiencia, ya que son regulados y pueden dañar el ozono.

| Gas | Disponibilidad | Ventajas | Desventajas | Ejemplos de uso |
|-----|---------------|----------|-------------|-----------------|
| **Propano** | Botellas de camping (como las de hornillos), gas de soldadura o aerosoles. | Muy eficiente, punto de ebullición bajo (-42°C), alta presión. | Altamente inflamable; requiere reguladores de presión. | Enfriadores de expansión DIY; similar a tu encendedor. |
| **Isobutano** | En cartuchos de gas para cocinas portátiles o refrigerantes ecológicos (como en algunos aerosoles). | Menos tóxico que propano, buen rendimiento en frío. | Inflamable; no tan común en tiendas generales. | Alternativa directa al butano en sistemas pequeños. |
| **Mezcla butano-propano** | Encendedores recargables, cartuchos de gas comprimido (disponibles en Amazon o tiendas de camping). | Fácil de encontrar, ya lo probaste. | Inflamable; rendimiento varía con la mezcla. | Tu setup actual; ideal para prototipos. |
| **Aire comprimido (nitrógeno o CO2)** | Bombas de aire, cartuchos de CO2 para bicicletas o pintura en aerosol. | Seguro (no inflamable), barato y abundante. | Menos eficiente para frío extremo; necesita alta presión (hasta 3000 psi). | Para enfriamiento por expansión en proyectos simples; no tan "frío" como hidrocarburos. |
| **Éter dietílico (éter de arranque)** | En tiendas de automóviles o como solvente. | Punto de ebullición muy bajo (-24°C), rápido enfriamiento. | Altamente inflamable y volátil; puede causar explosiones. | Usado en algunos DIY extremos, pero no recomendado para principiantes. |

### Consejos para tu proyecto
- **Cómo probar:** Usa un contenedor sellado con el gas, un tubo de expansión y un termómetro para medir el enfriamiento. Para 5V, integra un ventilador o Peltier para potenciar.
- **Mejoras:** Combina con aislamiento (espuma) y un termostato para eficiencia. Si es termoeléctrico, el gas podría ser innecesario; enfócate en baterías USB.
- **Fuentes:** Busca tutoriales en YouTube o foros como Reddit (r/DIY) sobre "Joule-Thomson cooler" o "portable gas fridge". Evita experimentos sin conocimientos básicos de física y seguridad.

Si me das más detalles sobre tu setup (¿es termoeléctrico o por gas puro?), puedo refinar la respuesta. ¡Mantén la seguridad primero!

