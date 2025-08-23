Perfecto, entiendo que quieres **extender tu conexión a Internet en zonas rurales o campos** usando **radioenlace** con antenas parabólicas en lugar de cables UTP, y quieres saber **qué otros materiales y equipos necesitas** para montar todo el sistema.

Vamos a separarlo en **componentes y equipos** para que tengas una guía clara.

---

## 1️⃣ Elementos principales para un radioenlace punto a punto

Si quieres llevar Internet desde un punto con conexión (por ejemplo, tu casa o una torre con acceso) hacia otro punto distante (por ejemplo, tu campo):

### **A. Antenas direccionales**

- Ya tienes **antenas parabólicas** (pueden ser tipo **grid** o **dish**).
    
- Alternativa: antenas **panel direccionales** o **Ubiquiti AirFiber / Mikrotik LHG** que ya vienen con radio integrado.
    

---

### **B. Radios / transceptores de red**

Necesitas equipos que conviertan la señal Ethernet en señal de radio para transmitir por las antenas:

- **Ejemplos recomendados:**
    
    - **Ubiquiti PowerBeam** (alcances de hasta 25-30 km)
        
    - **Mikrotik LHG HP5** o **Mikrotik NetMetal** con antena parabólica externa
        
    - **Ubiquiti AirFiber 5XHD** para distancias largas y alta capacidad (>500 Mbps)
        
- Estos equipos ya integran el **codificador y decodificador** de datos (modulación OFDM, MIMO, etc.) y se conectan por cable UTP a tus routers/switches.
    

---

### **C. Puntos de montaje**

- Torres, mástiles o soportes (mínimo 3–6 metros sobre el suelo para evitar obstáculos).
    
- Tensores y abrazaderas para fijar antenas.
    
- **Nivelación y orientación** con brújula y medidor de alineación.
    

---

## 2️⃣ Equipos de red y alimentación

### **A. Router / Switch**

- En cada extremo necesitarás un router para gestionar la conexión.
    
- Si quieres distribuir Wi-Fi en el destino, añadir un **punto de acceso Wi-Fi**.
    

### **B. PoE (Power over Ethernet)**

- La mayoría de equipos Ubiquiti o Mikrotik usan alimentación PoE.
    
- Necesitarás **inyectores PoE** o switches PoE.
    

### **C. Cables**

- Cable UTP de **categoría 5e o 6** (blindado si es exterior).
    
- Conectores RJ45 de calidad.
    
- Protección contra rayos: **descargadores PoE**.
    

---

## 3️⃣ Equipos opcionales para optimizar y proteger

- **UPS (Sistema de alimentación ininterrumpida)** → para que el enlace no se caiga con cortes de luz.
    
- **Protección contra sobretensiones**.
    
- **Servidor local** (si quieres almacenamiento o servicios propios en el campo).
    
- **Analizador de espectro Wi-Fi** → para evitar interferencias.
    

---

## 4️⃣ Ejemplo de configuración punto a punto

**Escenario:**

- Torre A (con internet de proveedor)
    
- Torre B (en el campo, 10 km de distancia)
    

**Materiales:**

1. **2 × Ubiquiti PowerBeam AC 5 GHz** (una en cada extremo)
    
2. **2 × inyectores PoE**
    
3. **2 × routers o APs Wi-Fi**
    
4. **Cables UTP Cat 6** (exterior, con protección UV)
    
5. **2 × mástiles / soportes**
    
6. **Tensores y abrazaderas**
    
7. **Protecciones PoE contra rayos**
    
8. **UPS o baterías solares** si no hay electricidad estable
    

---

💡 **Importante:**

- Si quieres **máxima velocidad**, usa **5 GHz** (menos interferencias, mayor ancho de banda), pero requiere línea de vista limpia.
    
- Si necesitas **máxima distancia**, usa **2.4 GHz** o equipos **5 GHz de alta potencia** con antenas grandes.
    
- Un **radioenlace profesional** bien alineado puede darte >500 Mbps a más de 10 km.
    

---

Si querés, puedo hacerte **un diagrama técnico** de cómo conectar todos los equipos desde tu proveedor de internet hasta el campo usando radioenlace.  
Eso te serviría como **manual visual de instalación**.