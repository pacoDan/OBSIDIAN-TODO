#### Criterios para elegir un router como AP

- **Modo AP**: Debe soportar "modo puente" o "AP" en su firmware (desactiva DHCP, NAT y WAN).
- **Alcance**: WiFi potente (802.11ac/ax), antenas externas/removibles para mejor señal. Para distancias largas (>100m), busca routers con antenas de alta ganancia (5-9dBi) o compatibles con antenas externas.
- **Puertos**: Múltiples LAN para conectar más dispositivos.
- **Compatibilidad**: Fácil de configurar vía web. Opcional: Soporte para OpenWRT/DD-WRT si quieres más control, pero como prefieres mini PCs, routers con firmware estándar bastan.
- **Precio**: Económicos (~$30-100), con buen rendimiento.
- **Otros**: Bajo consumo de energía, actualizaciones de firmware para seguridad.

#### Mejores routers recomendados

Aquí una lista de routers probados y populares para este propósito. Priorizo alcance, facilidad de configuración y compatibilidad con extensiones largas. Todos soportan modo AP.

1. **TP-Link Archer C7 (AC1750)**
    
    - **Alcance**: Excelente para interiores (hasta 100-200m en línea de vista; con antenas externas, hasta 500m+). 3 antenas removibles (5dBi cada una).
    - **Características**: WiFi dual-band (2.4/5GHz), 5 puertos Gigabit LAN. Modo AP fácil en la interfaz web.
    - **Precio**: ~$50-70.
    - **Por qué para tu setup**: Conecta por Ethernet a la mini PC, configura SSID/password para el portal. Extiende a habitaciones o pisos.
    - **Configuración básica**: Accede a 192.168.0.1 (o IP asignada), ve a "Advanced > Network > LAN" y activa "Access Point" mode. Desactiva DHCP.
    
2. **Netgear Nighthawk AC1750 (R6700)**
    
    - **Alcance**: Muy potente (hasta 300m en exteriores con antenas; antenas externas de 5dBi). Ideal para jardines o edificios cercanos.
    - **Características**: WiFi AC, 4 puertos Gigabit, USB para storage. Modo AP nativo.
    - **Precio**: ~$70-90.
    - **Por qué para tu setup**: Robusto para extensiones largas; integra bien con portales cautivos. Soporta QoS para priorizar tráfico del portal.
    - **Configuración**: Similar a TP-Link; en "Advanced Setup > Router/AP Mode", elige AP.
    
3. **ASUS RT-AX55 (AX1800)**
    
    - **Alcance**: WiFi 6 para mejor cobertura en áreas densas (hasta 200-400m con antenas externas). 4 antenas (4x4 MU-MIMO).
    - **Características**: Rápido y futuro-proof, 4 puertos Gigabit, AiProtection. Modo AP simple.
    - **Precio**: ~$80-100.
    - **Por qué para tu setup**: Extiende eficientemente el portal a más dispositivos sin lag. Bueno para redes con muchos usuarios.
    - **Configuración**: En "Administration > Operation Mode", selecciona "Access Point".
    
4. **Ubiquiti UniFi AP AC Lite (para distancias muy largas)**
    
    - **Alcance**: Profesional; hasta 1-2km con antenas direccionales (no incluidas, compra por separado). 2x2 MIMO.
    - **Características**: Diseñado para extensiones; PoE para alimentación remota. Gestionable con app UniFi (gratuita).
    - **Precio**: ~$80-120 (más caro, pero escalable).
    - **Por qué para tu setup**: Si necesitas kilómetros (ej. granjas o campus), este es top. Conecta a mini PC por Ethernet y extiende el portal a áreas remotas.
    - **Configuración**: Usa el controlador UniFi para modo AP; no maneja DHCP.
    
5. **Opciones económicas/básicas**:
    
    - **TP-Link TL-WR841N**: ~$20-30, alcance básico (50-100m), 4 puertos LAN. Bueno para empezar.
    - **D-Link DIR-615**: Similar, barato, pero firmware limitado.
    

#### Integración con tu portal cautivo en mini PC

- **Conexión**: Conecta el puerto WAN/LAN del router a la Ethernet de la mini PC (ej. en la subred 192.168.10.x). El router actúa como switch/AP, pasando todo tráfico al servidor.
- **Configuración en mini PC**: Asegura que dnsmasq/iptables redirijan a dispositivos conectados al router. El portal aparecerá automáticamente en WiFi del router.
- **Extensión a kilómetros**: Para distancias largas, usa routers con antenas externas o combina con repetidores WiFi (ej. conecta un segundo router en modo AP a otro). Evita interferencias con canales WiFi separados.
- **Monitoreo**: Desde la mini PC, usa `nmap` o `iwconfig` para ver dispositivos conectados al AP.

#### Consejos adicionales

- **Pruebas de alcance**: Usa apps como WiFi Analyzer para medir señal. Para kilómetros, considera antenas parabólicas o enlaces punto-a-punto.
- **Seguridad**: Configura WPA3 en el AP. Actualiza firmware para parches.
- **Alternativas no-router**: Si quieres algo más barato, un Raspberry Pi con adaptador WiFi USB (ej. Alfa AWUS036N) puede actuar como AP con `hostapd`, pero los routers dedicados son más simples.
- **Dónde comprar**: Amazon, eBay o tiendas locales. Verifica reseñas para compatibilidad.

Si me das tu presupuesto o ubicación aproximada (para alcance), puedo refinar recomendaciones. ¿Qué distancia necesitas cubrir? ¿Tienes preferencia por marca? ¡Vamos a extender ese portal!


---

Perfecto, lo resumimos **como si estuvieras armando una PC** pero aplicado a routers/APs.  
Pensá en el datasheet del router como el **datasheet de una motherboard**: no mirás el marketing, mirás el chipset, los buses, los estándares reales.

---

# 🔎 Router = Placa Madre

Así se leen datasheets como ingeniero (no como cliente común)

---

## 🧠 1. Chipset ≈ El “CPU” del router

En una PC mirás:

> ¿Es Intel / AMD? ¿Generación? ¿Arquitectura?

En un router mirás:

> ¿Cuál es el SoC WiFi?

### En datasheet buscás:

- **Qualcomm IPQ**
    
- **Broadcom BCM**
    
- **MediaTek MT79xx**
    
- **HiSilicon**
    
- ❌ Desconfiar si no aclaran chip
    

### Analogía PC:

|PC|Router|
|---|---|
|CPU|SoC WiFi|
|Generación|Familia del chipset|
|Arquitectura|Arquitectura WiFi|
|Benchmark|throughput real|

---

## 📚 2. Estándar WiFi ≈ Generación de arquitectura

En PC mirás:

> DDR4 / DDR5, PCIe 3 / 4 / 5

En router buscás:

✅ **802.11ax** (WiFi 6 mínimo real)  
✅ Ideal: AX3000 o superior  
❌ "WiFi 6 ready" sin especificar = mentira

### Analogía:

|PC|Router|
|---|---|
|DDR5|WiFi 6|
|PCIe 4|OFDMA|
|NVMe|MU-MIMO|
|XMP|Beamforming + BSS|

---

## 📡 3. Antenas ≈ VRMs y disipación

No alcanza el chip si no puede rendir.

En PC:

> VRMs y refrigeración importan

En Router:

> **Antenas + potencia TX**

Buscás en datasheet:

✅ 4–9 dBi  
✅ Antenas externas  
✅ Soporte para antenas reemplazables

### Analogía:

|PC|Router|
|---|---|
|Disipador|Antena|
|Fases VRM|Cadenas MIMO|
|Pasta térmica|Calidad RF|

---

## ⚙️ 4. MU-MIMO / OFDMA / BSS ≈ Instrucciones del CPU

En PC:

> SSE, AVX, PCIe lanes

En Router:  
Buscás literal:

✅ "MU-MIMO"  
✅ "OFDMA"  
✅ "BSS Coloring"  
✅ "Target Wake Time"

Si no aparece textual → NO EXISTE.

### Analogía:

|PC|Router|
|---|---|
|AVX|OFDMA|
|SMT|MU-MIMO|
|NUMA|BSS Coloring|
|C States|TWT|

---

## 🧮 5. MIMO streams ≈ Cores / RAM

En PC mirás:

> Cantidad de núcleos, memoria

En router:

Buscás:

- 2x2
    
- 3x3
    
- 4x4
    

Mientras mayor → más clientes reales sin colgarse.

### Analogía:

|PC|Router|
|---|---|
|Núcleos|Streams MIMO|
|RAM|Buffers|
|Cache|Airtime control|

---

## 🌐 6. Puertos ≈ Expansión de I/O

En una mother:

> SATA, USB, PCIe

En router mirás:

✅ LAN gigabit  
✅ mínimo 4  
✅ PoE (si es profesional)  
✅ USB (opcional)

---

## 🔒 7. Firmware ≈ BIOS / UEFI

En PC:

> BIOS bueno = overclock, estabilidad

En router:

✅ Modo AP  
✅ WPA3  
✅ VLAN  
✅ Control TX  
✅ QoS  
✅ OpenWRT compatible

### Analogía:

|PC|Router|
|---|---|
|BIOS|Firmware|
|UEFI|OpenWRT|
|XMP|QoS|
|Secure Boot|WPA3|

---

# 🧾 CHECKLIST RÁPIDO ANTES DE COMPRAR

Leés datasheet y verificás:

```
✓ Chipset identificado
✓ 802.11ax explícito
✓ MIMO declarado (2x2, 4x4)
✓ OFDMA listado
✓ MU-MIMO explícito
✓ BSS Coloring presente
✓ TWT presente
✓ Antenas declaradas
✓ Potencia TX o sensibilidad RX
✓ Manual disponible
✓ Fotos del firmware
```

Si faltan 2 o más → descartalo.

---

# ✅ Conclusión como técnico

Comprar router es como motherboard:

> El marketing te muestra luces  
> El datasheet te muestra la verdad

---

Si querés, pasame **3 modelos específicos**  
y los destripamos como si fueran placas madre:

✅ bueno  
⚠️ limitado  
❌ humo puro

Y te digo **cuál comprar sin tirar plata**.