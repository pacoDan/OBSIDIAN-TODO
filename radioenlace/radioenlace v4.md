Perfecto — puedo darte un **plano real con medidas y especificaciones exactas**, pero para hacerlo _exacto_ necesito algunos datos tuyos (coordenadas o distancia real, cota/alturas del terreno, y requisitos de velocidad).  
Mientras me pasás esos datos, te preparo **un plano-tipo detallado** para un caso realista que suele darse en campos: **enlace punto-a-punto de 10 km (ambos extremos con línea de vista razonable)**.  
Este plano-tipo incluye: cálculos de Fresnel y curvatura de la Tierra, alturas mínimas de mástiles, equipos recomendados, materiales, dimensiones de anclaje y procedimiento de instalación paso a paso. Cuando me des tus coordenadas reales yo recalculo azimuts, alturas y cotas exactas y te entrego el plano final.

---

# Plano-tipo (enlace PTP = 10 km, frecuencia 5 GHz, objetivo: ~200–500 Mbps estable)

## 1) Supuestos

- Distancia entre sitios: **10 000 m** (10 km).
    
- Frecuencia usada: **5 GHz** (canal ancho 40–80 MHz según regulaciones y ruido).
    
- Antenas: radios con antena integrada tipo **parabólica direccional / dish** (ej. Ubiquiti PowerBeam / Mikrotik LHG).
    
- Potencia TX típica: 20–27 dBm; ganancia antena típica: **20–25 dBi**.
    
- Línea de vista (LOS) aproximada, sin obstáculos cercanos.
    

---

## 2) Cálculos esenciales (para diseño)

### a) Longitud de onda (λ)

- λ = c / f = 3·10^8 m/s ÷ 5·10^9 Hz = **0.06 m**
    

### b) Primera zona de Fresnel (F1)

Fórmula (para d total = 10 km, d1 = d2 = 5000 m):

- `F1 = sqrt( λ * d1 * d2 / (d1 + d2) ) ≈ 12.25 m`
    

Regla práctica: mantener **al menos 60%** de limpieza de la 1ª Fresnel.

- 60% de F1 ≈ **7.35 m** → es la **altura mínima libre** sobre cualquier obstáculo en la trayectoria central.
    

### c) Curvatura de la Tierra (abultamiento)

Para d = 10 000 m, abultamiento ≈ `d^2 / (8R)` con R ≈ 6 371 000 m:

- Abultamiento ≈ **1.96 m** → añadirlo al requerimiento de altura.
    

### d) Margen de seguridad

Sumamos márgenes por vegetación, temperatura y alineación: **+2–3 m**.

**Conclusión de alturas mínimas sobre el punto más alto del terreno entre ambos extremos:**

- Altura libre requerida ≈ 7.35 (60% Fresnel) + 1.96 (curvatura) + 3 (margen) ≈ **~12.3 m**
    

Por seguridad práctica, se recomienda **torres/mástiles de 12–15 m** en ambos extremos (la altura exacta depende de la topografía local; si un extremo está en alto, la otra puede ser menor).

---

## 3) Especificaciones de equipo (recomendadas)

### Radios / CPE (uno en cada extremo)

- Opción profesional integrada: **Ubiquiti PowerBeam 5AC (o AirFiber para mayores anchos)** o **MikroTik LHG XL/Power**.
    
    - Frecuencia: 5 GHz
        
    - Ganancia antena: 20–25 dBi (según modelo)
        
    - Alimentación: PoE (48 V común)
        
    - Protección: IP55/IP67
        
- Si buscas mayor rendimiento y enlaces muy largos, considerar AirFiber o Cambium.
    

### Router / Distribución en sitio remoto

- Router con NAT/DHCP o modo bridge según arquitectura (p. ej. MikroTik RB o Ubiquiti EdgeRouter).
    
- Punto de acceso Wi-Fi para distribución local (ej. Ubiquiti UniFi AC Pro o similar).
    

### Alimentación y protección

- **Inyector PoE** o switch PoE compatible con el radio.
    
- **Protector contra sobretensiones/descargadores** en línea Ethernet (grounding).
    
- **UPS** (sencillo) o batería/solar si no hay suministro confiable.
    

### Montaje y mecánica

- **Mástil/torre** de 12–15 m (según cálculo final).
    
- Base de hormigón para torre: recomendación básica: **poste anclado en zapata de 0.6 × 0.6 × 0.5 m** (depende de suelo y viento); para torres mayores, diseño estructural por ingeniero.
    
- Tensores, abrazaderas, saddles, pernos inox.
    

### Otros

- Cable UTP exterior Cat6 (directo desde el inyectores PoE al equipo).
    
- Bridas, cinta auto-vulcanizante, tubo corrugado para protección.
    
- Herramientas: brújula, inclinómetro/clinómetro, medidor RSSI (software del radio), portátil.
    

---

## 4) Estimación de rendimiento (orientativa)

Con equipos tipo PowerBeam / LHG y buena alineación:

- **Banda usable esperada**: 150–600 Mbps (dependiendo ancho de canal, interferencia y calidad de equipo).
    
- Latencia: **< 5–20 ms** en este tipo de enlaces.
    

---

## 5) Plano con medidas y pasos de instalación (detallado)

### A — Preparación (en ambos extremos)

1. Obtener **coordenadas GPS** (lat,long) y cota de cada extremo.
    
2. Hacer estudio LOS y perfil de terreno (Google Earth o SRTM): detectar obstáculos en la línea.
    
3. Determinar **azimut** entre ambos puntos y altura relativa.
    

> _Necesito tus coordenadas para calcular azimut y perfil exacto._

### B — Fundaciones y torre

4. Excavar y armar zapata de hormigón (mínimo 0.6×0.6×0.5 m) para mástil de 12–15 m. (Si suelos sueltos o vientos fuertes: pilar mayor y/o anclajes profundos).
    
5. Instalar mástil/tubo galvanizado vertical y asegurar con tensores radiales (mín. 3 tensores por dirección).
    

### C — Montaje de antena y equipo

6. Montar radio/antena en el mástil; orientar inicialmente con azimut calculado.
    
7. Conectar cable UTP Cat6 exterior al inyector PoE; sellar con cinta vulcanizante.
    
8. Conectar tierra/puesta a tierra directa del gabinete/radio a una varilla de puesta a tierra (mín. 2.4 m de varilla de cobre) y colocar arrestador de sobretensión PoE.
    

### D — Alineación fina

9. Desde el extremo A, transmitir y observar RSSI/Throughput mientras en B mueves la antena lentamente para máximo nivel de señal y mínima relación SNR.
    
10. Ajustar elevación y azimut hasta optimizar SNR. Usar incremento/decremento de potencia si saturación.
    

### E — Configuración de red

11. Configurar radios:
    

- Punto A: modo **AP / PtP master**, IP estática (ej. 192.168.10.1)
    
- Punto B: modo **Station / PtP slave**, IP estática (ej. 192.168.10.2)
    
- Seguridad: WPA2-AES con clave fuerte.
    
- Ancho de canal: elegir 40/80 MHz según espectro y regulaciones.
    

12. Conectar router local en Punto B al puerto LAN del radio, configurar NAT/Firewall y AP para Wi-Fi interna.
    

### F — Verificaciones finales

13. Medir throughput con iperf3 entre ambos extremos.
    
14. Monitoreo: configurar SNMP o logs para verificar estabilidad.
    

---

## 6) Lista de materiales con cantidades (para 1 enlace de 10 km)

- 2 × Radios tipo **Ubiquiti PowerBeam 5AC** (o Mikrotik LHG XL 5) — 1 por extremo.
    
- 2 × Inyectores PoE (compatibles).
    
- 2 × Routers (o 1 en origen si ya tienes router del ISP).
    
- 1 × AP Wi-Fi en Punto B (si quieres cobertura local).
    
- 2 × Mástiles / torres de **12–15 m** (según topografía); con sus tensores y anclajes.
    
- Materiales de cimentación (hormigón, varillas): estimar según diseño.
    
- Cable UTP exterior Cat6 (longitud según distancia internamente, p. ej. 30 m en cada extremo como reserva).
    
- 2 × arrestadores / protectores de sobretensión PoE.
    
- 2 × varillas de puesta a tierra (2.4 m).
    
- 1 × UPS (según consumo de equipos, p. ej. 600–1000 VA).
    
- Accesorios: bridas, cinta vulcanizante, conectores RJ45 industriales, herramientas.
    

---

## 7) Recomendaciones regulatorias y de seguridad

- Verificar **regulaciones locales** para potencia y uso de bandas en 5 GHz.
    
- Instalar **pararrayos y puesta a tierra** obligatoria: los equipos en mástil quedan expuestos.
    
- Si el enlace cruza caminos o zonas con acceso público, señalizar y proteger la base.
    

---

## 8) ¿Qué necesito de vos para el plano _real y exacto_?

Por favor envíame:

1. **Coordenadas (lat, long)** de ambos puntos (origen y destino), preferible en grados decimales.
    
2. **Alturas/cotas** (si las conoces) o fotos desde ambos puntos mirando hacia el otro extremo.
    
3. **Objetivo de throughput** (ejemplo: 50 Mbps / 200 Mbps / 500 Mbps).
    
4. **Limitaciones**: presupuesto aproximado, disponibilidad de electricidad en el campo, preferencia de marcas.
    
5. Si querés, muéstrame un enlace de Google Maps o Google Earth con los puntos marcados.
    

Con eso te devuelvo:

- Un **plano topográfico** simple (perfil del terreno), con **altura recomendada de mástil en cada extremo**, **azimut** (en grados), **modelo exacto de equipo sugerido**, **longitudes de cable**, **especificación de cimentación** y un **checklist de instalación** con medidas exactas y materiales listos para comprar.