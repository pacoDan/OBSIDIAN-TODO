Lo que buscas es **GNU Screen** con la funcionalidad de **compartir sesiones**. Esto permite que múltiples usuarios vean y colaboren en la misma sesión de terminal en tiempo real.

## Configuración básica de Screen compartido

### 1. Instalar Screen (si no está instalado)
```sh
# Ubuntu/Debian
sudo apt install screen
# CentOS/RHEL
sudo yum install screen
```
### 2. Configurar permisos para compartir
```sh
# Hacer que screen sea ejecutable por el grupo
sudo chmod u+s /usr/bin/screen
sudo chmod 755 /var/run/screen
```
### 3. Crear una sesión compartida
```sh
# Crear sesión con nombre específico
screen -S sesion_compartida

# O con permisos multiusuario desde el inicio
screen -S sesion_compartida
# Dentro de screen, presionar Ctrl+A, luego :
:multiuser on
:acladd usuario2
```
### 4. Conectarse a la sesión compartida
```sh
# Ver sesiones disponibles
screen -ls

# Conectarse a la sesión compartida
screen -x sesion_compartida

# O si hay múltiples usuarios
screen -x usuario1/sesion_compartida
```
## Comandos útiles de Screen

### Comandos básicos (Ctrl+A + tecla)
```sh
Ctrl+A + D    # Desconectarse (detach) sin cerrar la sesión
Ctrl+A + C    # Crear nueva ventana
Ctrl+A + N    # Siguiente ventana
Ctrl+A + P    # Ventana anterior
Ctrl+A + "    # Listar ventanas
Ctrl+A + K    # Cerrar ventana actual
```
### Comandos de modo comando (Ctrl+A + :)
```sh
:multiuser on          # Habilitar modo multiusuario
:acladd username       # Agregar usuario con permisos
:aclchg username +rwx  # Dar permisos completos
:wall "mensaje"        # Enviar mensaje a todos los usuarios
```
## Ejemplo práctico paso a paso

### En el servidor (Usuario 1):
```sh
# 1. Iniciar sesión screen
screen -S trabajo_colaborativo

# 2. Habilitar multiusuario (Ctrl+A, luego :)
:multiuser on
:acladd juan
:acladd maria
```
### Usuario remoto (Usuario 2):

bash

RunCopy code

`# Conectarse vía SSH primero ssh usuario@servidor # Luego conectarse a la sesión screen screen -x trabajo_colaborativo`

## Alternativas más modernas

### 1. **tmux** (más moderno que screen)
```sh
# Conectarse vía SSH primero
ssh usuario@servidor

# Luego conectarse a la sesión screen
screen -x trabajo_colaborativo
```
### 2. **tmate** (tmux para compartir)
```sh
# Instalar tmate
sudo apt install tmate

# Iniciar sesión compartida
tmate

# Obtener comando para que otros se conecten
tmate show-messages
```
### 3. **Teleconsole** (más simple)
```sh
# Instalar
curl https://www.teleconsole.com/get.sh | sh

# Iniciar sesión compartida
teleconsole
# Te dará un comando para que otros se conecten
```
## Configuración avanzada de Screen

### Archivo ~/.screenrc para personalizar:
```sh
# Configuración básica
startup_message off
defscrollback 10000
hardstatus alwayslastline
hardstatus string '%{= kG}[%{G}%H%? %1`%?%{g}][%= %{= kw}%-w%{+b yk} %n*%t%?(%u)%? %{-}%+w %=%{g}][%{B}%m/%d %{W}%C%A%{g}]'

# Habilitar multiusuario por defecto
multiuser on
```