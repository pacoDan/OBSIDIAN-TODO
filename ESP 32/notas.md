# Confirma que el puerto /dev/ttyUSB0 está disponible y que tu usuario tiene los permisos necesarios:
ls -l /dev/ttyUSB0

#Si el puerto existe pero sigue dando problemas, asegúrate de que tu usuario tenga permisos para acceder al puerto:
sudo chmod a+rw /dev/ttyUSB0

# Asegúrate de que tu usuario esté en el grupo adecuado para acceder a puertos serie:
sudo usermod -a -G dialout $USER


# https://programarfacil.com/esp32/esp32-cam/

# Configuración de Baud Rate Incorrecta: Asegúrate de que la velocidad de transmisión (baud rate) en el monitor serial coincida con la que has configurado en el código del ESP32. Por ejemplo, si has configurado 115200 baudios en el código, asegúrate de que el monitor serial también esté configurado a 115200 baudios.
# https://github.com/espressif/arduino-esp32/issues/8775

# https://devjaime.medium.com/explorando-los-modelos-de-lenguaje-ollama-mistral-llama-gemini-y-claude-90b378fcc343

# activar idf.py
 . $HOME/esp/esp-idf/export.sh   

❯ cp -r $IDF_PATH/examples/get-started/blink/ .

