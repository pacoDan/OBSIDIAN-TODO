diagrama tecnico:
```scss
[Proveedor de Internet / Router Principal]
             │
             │ (Puerto Ethernet)
             ▼
      [Equipo Punto A - Radioenlace]
      (Antena parabólica + CPE)
             ≈≈≈≈≈≈≈≈≈≈≈  ENLACE 5 GHz (o 2.4 GHz si es muy largo)
             ≈≈≈≈≈≈≈≈≈≈≈
      [Equipo Punto B - Radioenlace]
      (Antena parabólica + CPE)
             │
             │ (Puerto Ethernet)
             ▼
       [Router Wi-Fi local en el campo]
         (Distribuye Internet a equipos locales)
```
**Leyenda:**

- **CPE (Customer Premises Equipment)**: equipo de cliente, radio inalámbrico especializado (ej. Ubiquiti PowerBeam, Mikrotik LHG).
    
- **Enlace**: comunicación punto-a-punto, en este caso **radioenlace** usando antenas parabólicas.
    
- **Router local**: reparte Internet en el destino por Wi-Fi o cable.
    

---

## **2️⃣ Materiales necesarios**

### **En la ubicación de origen (Punto A)**

- **Router principal** (ya existente de tu proveedor).
    
- **Antena parabólica de radioenlace** (ejemplo: Ubiquiti PowerBeam 5AC, Mikrotik LHG XL 5AC).
    
- **Soporte/tubo metálico** o mástil para instalar la antena.
    
- **PoE injector** (Power over Ethernet) para alimentar la antena desde el router.
    
- **Cable UTP Cat6** (exterior) desde el router hasta la antena.
    

### **En la ubicación de destino (Punto B - Campo)**

- **Antena parabólica de radioenlace** (igual que la del Punto A, mismo modelo).
    
- **Soporte/tubo metálico** o torre para montaje.
    
- **PoE injector**.
    
- **Cable UTP Cat6** (exterior) desde la antena al router.
    
- **Router Wi-Fi** (para distribuir Internet localmente en el campo).
    
- **UPS o batería** si el lugar no tiene electricidad estable.
    

### **Herramientas**

- Llaves y herramientas para montaje.
    
- Brújula y nivelador para alinear antenas.
    
- Notebook para configurar los equipos.
    

---

## **3️⃣ Proceder de implementación**

1. **Estudio de línea de vista (LOS - Line of Sight)**
    
    - Asegurarte que entre Punto A y Punto B no haya obstáculos (árboles, edificios, cerros).
        
    - Usar herramientas como **Ubiquiti Link Planner** o **Google Earth** para calcular altura y orientación.
        
2. **Instalación física**
    
    - Montar mástiles/tubos o torres en ambos puntos.
        
    - Instalar antenas parabólicas fijas, firmes y con vista directa.
        
3. **Conexión eléctrica y de datos**
    
    - Desde el router principal al PoE injector y de ahí a la antena (UTP exterior Cat6).
        
    - En el punto B, desde la antena al PoE injector y de ahí a un router Wi-Fi local.
        
4. **Configuración de radioenlace**
    
    - Entrar a la interfaz web de cada antena (normalmente `192.168.1.20` por defecto).
        
    - Configurar un modo como **Access Point** (Punto A) y otro como **Station** (Punto B).
        
    - Elegir frecuencia (recomendado 5 GHz para velocidad, 2.4 GHz si hay mucha distancia y obstáculos).
        
    - Ajustar canal y ancho de banda (20/40 MHz para estabilidad).
        
    - Poner **seguridad WPA2-AES** y una clave fuerte.
        
5. **Alineación fina**
    
    - Con ayuda de otra persona en el otro extremo, ajustar la orientación de las antenas hasta lograr **máxima señal y mínimo ruido** (usando los indicadores LED o software del fabricante).
        
6. **Pruebas de conexión**
    
    - Hacer pruebas de ping y velocidad.
        
    - Comprobar que el Wi-Fi del campo entrega la velocidad esperada.
        

---

## **4️⃣ Diagrama técnico (visual)**

Aquí te hago el diagrama tipo red técnica:
```csharp
                INTERNET
                   │
        ┌──────────┴──────────┐
        │ Router principal    │
        └──────────┬──────────┘
                   │
            [PoE Injector]
                   │
             Cable UTP Cat6
                   │
        ┌───────────────────────┐
        │ Antena parabólica PtoA│◄──────────────┐
        └───────────────────────┘               │
                   ▲                             │
                   │      ENLACE RADIO 5GHz      │
                   ▼                             │
        ┌───────────────────────┐               │
        │ Antena parabólica PtoB│───────────────┘
        └───────────────────────┘
                   │
             Cable UTP Cat6
                   │
            [PoE Injector]
                   │
        ┌──────────┴──────────┐
        │ Router Wi-Fi Campo  │
        └─────────────────────┘
                   │
             Distribución Wi-Fi
```
💡 **Notas técnicas importantes**:

- Si la distancia es **> 20 km**, conviene usar equipos **con alto dBi** y analizar curvatura terrestre (altura mínima).
    
- Para campos con más de un punto a cubrir, en el Punto B puedes instalar un **Access Point sectorial**.
    
- Si quieres **alta estabilidad**, usar equipos profesionales tipo **Mikrotik LHG XL 5 AC** o **Ubiquiti PowerBeam AC Gen2**.
    

---

Si quieres, te puedo hacer **un plano real con medidas y especificaciones exactas** de acuerdo a tu distancia y topografía para que sepas qué potencia de antena y altura de torre usar.