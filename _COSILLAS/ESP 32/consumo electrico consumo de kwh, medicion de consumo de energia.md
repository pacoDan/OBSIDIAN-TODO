Para medir **consumo eléctrico (kW y kWh)** en tu casa con **ESP32**, necesitas un **sensor de corriente no invasivo** + **sensor de voltaje** (o un medidor completo). Aquí te doy los **top modelos** más usados y efectivos:

## 🏆 **TOP 5 Sensores/Medidores para ESP32**

### 1. **PZEM-004T V3.0** ⭐ **MEJOR OPCION**
```
📊 Mide: Voltaje, Corriente, Potencia (kW), Energía (kWh), Factor PF, Frecuencia
🔌 Rango: 100A, 80-260V AC
💰 Precio: ~$8-12 USD
🛠️ Conexión: UART (TX/RX) - PLUG & PLAY
```
```cpp
// Librería: PZEM004Tv30
PZEM004Tv30 pzem(Serial2, 16, 17); // RX=16, TX=17
float power = pzem.power();    // kW
float energy = pzem.energy();  // kWh
```

### 2. **SCT-013-000** (Sensor de Corriente) + **ZMPT101B** (Voltaje)
```
🔌 SCT-013: 100A/1V (no invasivo)
🔌 ZMPT101B: 250V/1kV
💰 Precio: ~$10-15 USD total
🛠️ Precisión: ±1%
```
```cpp
// Librería: EmonLib
EnergyMonitor emon1;
emon1.current(1, 111.1);     // Pin analógico A1
emon1.voltage(2, 234.7, 1.7); // Pin A2
```

### 3. **HLW8032** (Chip single-phase)
```
📊 Mide: Todo (V, I, P, kWh)
🔌 Rango: 100A, 230V
💰 Precio: ~$5-8 USD (blinds como Sonoff POW)
🛠️ Conexión: UART
```

### 4. **ACS712** (Corriente) + **ZMPT101B**
```
🔌 ACS712: 5A/20A/30A
💰 Precio: ~$3-6 USD
⚠️ Menos preciso para casa (~±1.5%)
```

### 5. **INA219** + **Transformador CT**
```
📊 Mide corriente alta precisión
🔌 Rango: Hasta 26A directo
💰 Precio: ~$5 USD
🛠️ I2C muy fácil
```

## 🎯 **RECOMENDACIÓN #1: PZEM-004T**

**Por qué es el MEJOR:**
```
✅ Precisión ±1%
✅ Mide kWh directamente (acumula energía)
✅ No calibrar
✅ Mide todo (V, I, kW, kWh, PF)
✅ Barato y disponible
✅ UART simple con ESP32
```

## 🔌 **Conexión ESP32 + PZEM-004T**

```
PZEM-004T    ESP32
VCC    →    5V/3.3V
GND    →    GND
TX     →    GPIO16 (RX2)
RX     →    GPIO17 (TX2)
CT     →    Pinza al cable de fase
```

## 💻 **Código Completo ESP32**

```cpp
#include <PZEM004Tv30.h>
#include <WiFi.h>
#include <PubSubClient.h>

PZEM004Tv30 pzem(Serial2, 16, 17);

void setup() {
  Serial.begin(115200);
  Serial2.begin(9600, SERIAL_8N1, 16, 17);
  
  // WiFi y MQTT...
}

void loop() {
  float voltage = pzem.voltage();
  float current = pzem.current();
  float power = pzem.power();      // kW
  float energy = pzem.energy();    // kWh TOTAL
  float pf = pzem.pf();
  
  Serial.printf("V:%.1f I:%.2f P:%.1f kWh:%.3f PF:%.2f\n", 
                voltage, current, power, energy, pf);
  
  // Reset kWh si quieres: pzem.resetEnergy();
  delay(2000);
}
```

## 🏠 **Instalación Física (IMPORTANTE)**

```
⚠️  DESCONECTA LA LUZ ANTES ⚠️

1. Pinza SCT-013/SCT del PZEM SOLO en CABLE FASE (negro/marron)
2. NO cortes cables
3. NO toques neutro ni tierra
4. Verifica con multímetro
```

## 📈 **Para Dashboard Web**
```
- Blynk
- Home Assistant
- Grafana + InfluxDB
- ThingSpeak
```

## 💡 **Alternativas Comerciales**
```
🏪 Shelly EM: ~$60 (WiFi integrado)
🏪 Sonoff POW R3: ~$25
🏪 Tuya Zigbee: ~$20
```

**¿Cuál necesitas?** Para casa completa usa **PZEM-004T** en cuadro eléctrico (corriente total). Para circuitos específicos, usa varios SCT-013.

**¡Pregunta si necesitas el esquemático completo o código MQTT!** ⚡