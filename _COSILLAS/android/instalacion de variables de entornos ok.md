variables de entorno en Windows
PowerShell:
```sh
$env:ANDROID_HOME = "C:\Users\Daniel\AppData\Local\Android\Sdk"
$env:PATH += ";$env:ANDROID_HOME\emulator"
$env:PATH += ";$env:ANDROID_HOME\platform-tools"
```
cmd:
```sh
set ANDROID_HOME=C:\Users\Daniel\AppData\Local\Android\Sdk
set PATH=%PATH%;%ANDROID_HOME%\emulator
set PATH=%PATH%;%ANDROID_HOME%\platform-tools
```

Linux:
```sh
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

nota: las de Windows son temporales, lo ideal y adecuado es ir a la ventana de variables de entorno y setear desde allí

**Listar los Android Virtual Devices (AVD) disponibles:**
```sh
emulator -list-avds
```
o si no esta bien configurado los entornos:
```sh
$ANDROID_SDK_ROOT/emulator/emulator -list-avds
```
**Dispositivos corriendo actualmente:**
y de paso se identifica el dispositivo conectado con `adb devices`:
```sh
adb devices
```
correr un Android según listado de `emulator -list-avds` : 
```sh
 emulator -avd Pixel_5
```
en lugar de Pixel_5 elijamos una que nos aparece en `emulator -list-avds`

---

o en caso de que no aparesca emulator en la variable de entorno
```sh
$ANDROID_SDK_ROOT/emulator/emulator -list-avds
```