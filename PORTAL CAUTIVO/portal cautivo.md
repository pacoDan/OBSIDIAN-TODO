Perfecto, te daré una guía avanzada para montar un portal cautivo en Raspberry Pi 4, asumiendo que usas **Raspberry Pi OS (basado en Debian)**, que es el sistema operativo más común y recomendado.

---

## Resumen de la arquitectura

- **eth0:** conectado a la red principal (internet o LAN).
- **wlan0:** configurado como Access Point (AP), crea la red WiFi para clientes.
- La Pi hace NAT entre wlan0 y eth0.
- Portal cautivo intercepta peticiones HTTP y redirige a página local.

---

# Paso 1: Preparar Raspberry Pi OS

Actualiza el sistema:
```sh
sudo apt update && sudo apt upgrade -y
```
Instala paquetes necesarios:
```sh
sudo apt install hostapd dnsmasq iptables-persistent lighttpd -y
```
---

# Paso 2: Configurar la interfaz WiFi como Access Point

Edita `/etc/dhcpcd.conf` para asignar IP estática a wlan0:
```sh
sudo nano /etc/dhcpcd.conf
```
Agrega al final:
```sh
interface wlan0
    static ip_address=192.168.50.1/24
    nohook wpa_supplicant
```
Reinicia el servicio dhcpcd:
```sh
sudo service dhcpcd restart
```
---

# Paso 3: Configurar hostapd (Access Point)

Edita `/etc/hostapd/hostapd.conf`:
```sh
sudo nano /etc/hostapd/hostapd.conf
```
Ejemplo básico:
```sh
interface=wlan0
driver=nl80211
ssid=MiPortalCautivo
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=TuClaveSegura
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
```
Luego indica a hostapd dónde está el archivo de configuración:
```sh
sudo nano /etc/default/hostapd
```
Descomenta y modifica la línea:
```sh
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```
Inicia y habilita hostapd:
```sh
sudo systemctl unmask hostapd
sudo systemctl enable hostapd
sudo systemctl start hostapd
```
---

# Paso 4: Configurar dnsmasq (DHCP y DNS)

Primero renombra el archivo original para evitar conflictos:
```sh
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```
Crea uno nuevo:
```sh
sudo nano /etc/dnsmasq.conf
```
Ejemplo:
```sh
interface=wlan0
dhcp-range=192.168.50.10,192.168.50.100,12h
address=/#/192.168.50.1
```
- `dhcp-range`: rango de IPs para clientes.
- `address=/#/192.168.50.1`: fuerza a que todas las consultas DNS apunten a la IP del portal (redirección DNS para portal cautivo).

Reinicia dnsmasq:
```sh
sudo systemctl restart dnsmasq
```
---

# Paso 5: Configurar NAT y reglas iptables

Habilita el reenvío de paquetes:
```sh
sudo nano /etc/sysctl.conf
```
Descomenta o agrega:
```sh
net.ipv4.ip_forward=1
```
Aplica el cambio:
```sh
sudo sysctl -p
```
Configura iptables para NAT y redirección HTTP:
```sh
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
```
Redirige tráfico HTTP (puerto 80) hacia el portal local (192.168.50.1):
```sh
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 80 -j DNAT --to-destination 192.168.50.1:80
```

Guarda las reglas para que persistan tras reinicio:
```sh
sudo netfilter-persistent save
```
---

# Paso 6: Configurar servidor web (lighttpd)

El servidor web ya está instalado. Coloca tu portal cautivo en:
```sh
/var/www/html/
```

Por ejemplo, crea un archivo `index.html` con la página de bienvenida o login.

---

# Paso 7: Portal cautivo avanzado para desarrolladores (con sockets)

Para un portal cautivo avanzado, puedes crear un servidor en Python que maneje conexiones TCP/HTTP y controle la lógica de autenticación.

Ejemplo básico usando Python y sockets:
```py
import socket

HOST = ''  # Escuchar en todas las interfaces
PORT = 80  # Puerto HTTP

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen(5)
    print("Servidor portal cautivo escuchando en puerto 80...")
    while True:
        conn, addr = s.accept()
        with conn:
            print(f"Conexión de {addr}")
            request = conn.recv(1024).decode('utf-8')
            print(f"Request:\n{request}")

            # Aquí puedes parsear la request HTTP y responder con tu página
            response = """HTTP/1.1 200 OK
Content-Type: text/html

<html><body><h1>Bienvenido al Portal Cautivo</h1></body></html>
"""
            conn.sendall(response.encode('utf-8'))

```

Este script puede reemplazar o complementar el servidor web ligero para tener control total sobre las conexiones, sesiones, autenticación, etc.

---

# Notas finales

- El portal cautivo intercepta peticiones HTTP (puerto 80). Para HTTPS (puerto 443) es más complejo porque el tráfico está cifrado y no se puede redirigir fácilmente sin errores de certificado.
- Puedes usar herramientas como `nodogsplash` o `CoovaChilli` para portales cautivos más completos.
- Para desarrollo avanzado, manejar sockets te permite implementar autenticación personalizada, sesiones, y comunicación en tiempo real.

---

Si quieres, puedo ayudarte a armar un script completo en Python para el portal cautivo o a integrar autenticación con base de datos, etc. ¿Quieres que siga por ese camino?