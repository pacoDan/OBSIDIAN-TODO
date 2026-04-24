```sh
. $HOME/esp/esp-idf/export.sh
```

ejemplo parcial de configuración
```c
// ===========================

// Enter your WiFi credentials

// ===========================

const char *ssid = "Infinix";

const char *password = "3141592654";

  

void startCameraServer();

void setupLedFlash();

  

void setup() {

Serial.begin(115200);

Serial.setDebugOutput(false);

esp_log_level_set("*", ESP_LOG_NONE); // Suprime logs del sistema (WiFi, etc.)

  

// Serial.println();

Serial.println("Iniciando..."); // Tu mensaje personalizado
```