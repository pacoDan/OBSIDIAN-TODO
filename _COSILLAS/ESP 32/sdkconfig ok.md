
#### Causas Probables del Reinicio
- **Build limpia**: Comandos como `idf.py fullclean` o borrar la carpeta `build/` eliminan `sdkconfig` y lo recrean desde defaults.
- **Cambio de target**: Al cambiar de chip (ej. de ESP32 a ESP32-S3), IDF carga `sdkconfig.defaults.esp32s3`, sobrescribiendo el actual.
- **Archivo corrupto o faltante**: Si `sdkconfig` se daña, IDF lo regenera automáticamente.
- **Prioridad de defaults**: IDF siempre usa `sdkconfig.defaults` como base si no hay `sdkconfig` guardado.

#### Soluciones para Mantener Configuración Personalizada
- **Guarda cambios con menuconfig**:
  - Ejecuta `idf.py menuconfig`.
  - Haz cambios (ej. configura WiFi o pines).
  - Guarda (Ctrl+S) y sal (Ctrl+X). Esto actualiza `sdkconfig` permanentemente.

- **Edita sdkconfig manualmente**:
  - Abre `sdkconfig` con un editor: `nvim sdkconfig`.
  - Cambia valores (ej. `CONFIG_WIFI_SSID="MiRed"`).
  - No edites si prefieres menuconfig para evitar conflictos.

- **Personaliza sdkconfig.defaults**:
  - Copia tu `sdkconfig` configurado al archivo defaults correspondiente.
  - Ejemplo para ESP32-S3: `cp sdkconfig sdkconfig.defaults.esp32s3`.
  - Al cambiar target, mantendrá tus settings.

- **Evita reinicios innecesarios**:
  - No uses `idf.py fullclean` a menos que cambies dependencias.
  - Versiona `sdkconfig` en Git: `git add sdkconfig` para no perderlo.

- **Verifica y cambia target**:
  - Target actual: `idf.py get-target` (ej. esp32s3).
  - Cambia si es necesario: `idf.py set-target esp32s3` (usa el defaults correspondiente).

#### Archivos en tu Listado
- `sdkconfig`: Config actual (editable; se regenera si falta).
- `sdkconfig.defaults`: Base general para todos los chips.
- `sdkconfig.defaults.esp32*`: Específicos (ej. `sdkconfig.defaults.esp32s3` para ESP32-S3; úsalo para tu modelo).

Si el problema continúa, comparte qué valores se reinician o el output de `idf.py build`. ¡Con estos pasos, tu config se mantendrá estable!