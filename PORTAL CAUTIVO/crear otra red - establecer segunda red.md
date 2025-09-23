herramientas: nmcli, netctl
```sh
sudo pacman -S networkmanager
```

```sh
sudo systemctl enable NetworkManager
sudo systemctl restart NetworkManager
sudo systemctl status NetworkManager
```
### 1. Configurar la segunda interfaz de red
- Asegúrate de que la segunda placa de red esté activa y configurada correctamente.
- En WSL, puedes listar las interfaces con `ip a` o `nmcli device`.
- Usa `nmcli` para crear una nueva conexión en la segunda interfaz, por ejemplo:
```sh
nmcli device status  # para ver las interfaces
nmcli connection add type wifi ifname wlan1 con-name portal2 ssid "NombreRed2"
nmcli connection modify portal2 802-11-wireless.mode ap 802-11-wireless.band bg ipv4.method shared
nmcli connection up portal2
```
Ajusta `wlan1` al nombre real de la segunda interfaz.

### 2. Configurar el portal cautivo

- El portal cautivo normalmente se implementa con un servidor web que intercepta las peticiones HTTP y redirige a una página de login.
- Puedes usar software como **nodogsplash**, **CoovaChilli** o **Chillispot** en Linux.
- Instala y configura uno de estos en WSL o en una máquina Linux dedicada.
- Configura el servidor DHCP y DNS para la segunda interfaz para que los clientes reciban IP y sean redirigidos al portal.

### 3. Configurar reglas de iptables o firewall

- Para interceptar el tráfico HTTP y redirigirlo al portal, necesitas reglas de firewall.
- Ejemplo básico con iptables:
```sh
iptables -t nat -A PREROUTING -i wlan1 -p tcp --dport 80 -j DNAT --to-destination 192.168.2.1:80
iptables -t nat -A POSTROUTING -o wlan1 -j MASQUERADE
```
Donde `192.168.2.1` es la IP del portal cautivo en la segunda red.

### 4. Configurar DHCP y DNS

- Usa `dnsmasq` o el servicio DHCP de `nmcli` para asignar IPs en la segunda red.
- Configura el DNS para que todas las consultas apunten al portal cautivo.

---

### Resumen rápido para crear la segunda red y portal cautivo:

1. Crear y activar la segunda red con `nmcli`.
2. Configurar DHCP/DNS para esa red.
3. Instalar y configurar un software de portal cautivo (nodogsplash, CoovaChilli).
4. Configurar reglas de firewall para redirigir tráfico HTTP al portal.
5. Probar conectando un cliente a la segunda red y verificar que aparece el portal.

---

### Crear dos redes en la misma placa de red (virtualización de interfaces)

Sí, es posible crear múltiples redes virtuales en una sola interfaz física usando **interfaces virtuales** o **APs virtuales** (en modo Access Point múltiple). Esto depende del soporte del driver y hardware.

Para crear dos redes WiFi (APs) en la misma placa, puedes usar:

- **Virtual interfaces (VIFs)** con `iw` o `hostapd`.
- Configurar `hostapd` para crear múltiples SSIDs en la misma interfaz física.

Ejemplo básico para crear una interfaz virtual:
```sh
sudo iw dev wlan0 interface add wlan0_1 type __ap
```
Luego puedes configurar `hostapd` para que `wlan0` y `wlan0_1` sean dos APs diferentes con SSIDs distintos.

---

### Pasos para listar y crear interfaces virtuales:

1. Listar interfaces:

bash

RunCopy code

`1nmcli device status`

2. Ver interfaces con `iw`:

bash

RunCopy code

`1iw dev`

3. Crear interfaz virtual:

bash

RunCopy code

`1sudo iw dev wlan0 interface add wlan0_1 type __ap`

4. Configurar `hostapd` para cada interfaz con SSID y seguridad diferentes.

---

Si quieres, puedo ayudarte a crear la configuración de `hostapd` para dos APs en la misma placa, o a crear dos conexiones con `nmcli` si prefieres usar dos interfaces físicas. ¿Qué prefieres?