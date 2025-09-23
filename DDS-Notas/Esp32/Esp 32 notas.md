Copy the project [get-started/hello_world](https://github.com/espressif/esp-idf/tree/v5.3.2/examples/get-started/hello_world) to `~/esp` directory:
```sh
cd ~/esp
cp -r $IDF_PATH/examples/get-started/hello_world .
```
```sh
cd ~/esp
cp -r $IDF_PATH/examples/get-started/blink .
```


pagina get started
https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/linux-macos-setup.html

install in Arch:
```sh
sudo pacman -S --needed gcc git make flex bison gperf python cmake ninja ccache dfu-util libusb
```
```sh
mkdir -p ~/esp
cd ~/esp
git clone -b v5.3.2 --recursive https://github.com/espressif/esp-idf.git
```

Aside from the ESP-IDF, you also need to install the tools used by ESP-IDF, such as the compiler, debugger, Python packages, etc, for projects supporting ESP32.
In order to install tools for all supported targets please run the following command:
```sh
cd ~/esp/esp-idf
./install.sh all
```


## Step 4. Set up the Environment Variables
```sh
. $HOME/esp/esp-idf/export.sh
alias get_idf='. $HOME/esp/esp-idf/export.sh'
```


ejemplo usando el arduino:
```c
// Definimos el pin del LED incorporado
#define LED_BUILTIN 4  // El pin 4 es el pin del LED en la mayoría de las placas ESP32-CAM

void setup() {
  // Inicializamos el pin del LED como salida
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  // Encender el LED
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000); // Esperar 1 segundo

  // Apagar el LED
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000); // Esperar 1 segundo
}
```

funciona con 115200 baudios
![[Pasted image 20241224095939.png]]

```sh
sudo chmod 666 /dev/ttyUSB0
sudo usermod -a -G dialout $USER
sudo usermod -a -G tty $USER
```


![[Pasted image 20241224103508.png]]



A continuación, se muestra un ejemplo de circuito de rectificador de puente para convertir 220V AC a 220V DC:
**Circuito de Rectificador de Puente**
*   4 diodos de alta potencia (1N4007 o similares)
*   1 condensador de filtro (100uF o mayor)
*   1 resistencia de carga (10kΩ o mayor)
**Conexiones**
*   Conectar los diodos en forma de puente, con los extremos conectados a la fuente de alimentación AC.
*   Conectar el condensador de filtro en serie con la resistencia de carga.
*   Conectar la salida del circuito a la carga (sensor o dispositivo).

![[Pasted image 20241224180215.png]]

![[Pasted image 20241224180251.png]]


