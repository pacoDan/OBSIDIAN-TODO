### 🔁 **Alternativas Similares a Ngrok**

1. **LocalTunnel**
    
    - 📌 Sitio: [https://github.com/localtunnel/localtunnel](https://github.com/localtunnel/localtunnel)
        
    - ✅ Fácil de usar, open source.
        
    - 🚀 Comando típico:
        ```sh
        npm install -g localtunnel
        ```
        `npx localtunnel --port 5000`
    - 🟡 A veces es inestable o lento.
Clients in other languages
_go_ [gotunnelme](https://github.com/NoahShen/gotunnelme)
_go_ [go-localtunnel](https://github.com/localtunnel/go-localtunnel)
_C#/.NET_ [localtunnel-client](https://github.com/angelobreuer/localtunnel.net)
_Rust_ [rlt](https://github.com/kaichaosun/rlt)

1. **Cloudflare Tunnel (antes Argo Tunnel)**
    
    - 📌 Sitio: https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/
        
    - ✅ Seguro, gratuito, sin límite de tiempo.
        
    - 💡 Necesita una cuenta Cloudflare y configuración previa.
        
    - 🚀 Comando típico: en https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/create-remote-tunnel-api/#4-install-and-run-the-tunnel
        ```sh
        docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token <TUNNEL_TOKEN>
        ```
        `cloudflared tunnel --url http://localhost:5000`
        
2. **Expose**
    
    - 📌 Sitio: https://beyondco.de/docs/expose/
        
    - 🛠 Requiere instalación (PHP, Composer).
        
    - 🎁 Tiene plan gratuito (autenticación, HTTPS, subdominios).
        
    - 🚀 Comando típico:
        
        `expose share localhost:5000`
        
3. **Teleport**
    
    - 📌 Sitio: https://goteleport.com/teleport/
        
    - 🔒 Más orientado a acceso seguro a infraestructura.
        
    - No es tan simple como ngrok o localtunnel, pero es potente.
        
4. **Serveo**
    
    - 📌 Sitio: https://serveo.net _(puede estar inactivo en ocasiones)_
        
    - 🔁 Sin instalación, se usa con SSH.
        
    - 🚀 Comando típico:
        
        `ssh -R 80:localhost:5000 serveo.net`

---
## PARA TCP
|Necesitas...|Opción recomendada|
|---|---|
|Solución rápida y sin instalación|Serveo (SSH)|
|Seguridad y túneles privados confiables|Cloudflare Tunnel|
|Acceso completo y seguro con control de rol|Teleport|
|Control total en tu propio VPS|FRP|

### 1. **Cloudflare Tunnel (con `cloudflared`)**

🔒 **Seguro**, gratuito y muy estable.

- Por defecto funciona con HTTP/S, **pero también puedes tunearlo para TCP** con un túnel personalizado.
    
- Ideal para exponer puertos como PostgreSQL (5432), Redis (6379), etc.
    

📌 Requiere crear un túnel en Cloudflare y configurarlo.

**Docs TCP tunneling:**  
👉 Cloudflare TCP tunnel setup

---

### 2. **Serveo.net (con SSH)**

✅ Fácil y sin instalación, si estás en Linux/macOS.

`ssh -R 5432:localhost:5432 serveo.net`

Esto expondrá tu base de datos PostgreSQL local al puerto remoto que te asigne Serveo.  
⚠️ No siempre está disponible y tiene limitaciones de ancho de banda y seguridad.

---

### 3. **Teleport**

🔐 Solución empresarial para acceso a infra remota (bases de datos, SSH, etc.).

- Admite **acceso seguro a PostgreSQL, MySQL, MongoDB**, etc.
    
- Enfocado en auditoría, permisos, roles, etc.
    

📌 Más complejo de configurar, ideal para producción segura.

Docs: https://goteleport.com/docs/database-access/

---

### 4. **Expose (BeyondCode)**

👉 Solo **HTTPS**, no soporta TCP nativamente. _(no aplica para bases de datos)_

---

### 5. **PageKite**

🟡 Obsoleto pero funcional. A veces usado para SSH y puertos TCP.

`pagekite.py 5432 yourname.pagekite.me`

Docs: https://pagekite.net

---

### 6. **FRP (Fast Reverse Proxy)**

🧰 Open source, muy potente para túneles TCP/UDP. Necesita un servidor remoto VPS.

- Puedes tunear lo que quieras: HTTP, HTTPS, SSH, MySQL, etc.
    
- Requiere configuración del cliente y servidor.
    

🔧 Proyecto: [https://github.com/fatedier/frp](https://github.com/fatedier/frp)

---

### 7. **Ngrok TCP (clásico)**

✔️ Aunque estás buscando alternativas, si tienes cuenta Ngrok y usas el plan pago, puedes seguir usando:

`ngrok tcp 5432`

---
## ✅ Lo mínimo que necesitas para crear tu propio túnel inverso

### 1. **Un servidor (hosting o VPS público)**

- **Obligatorio** si quieres que el túnel funcione desde cualquier lugar.
    
- Debe tener una IP pública accesible desde internet.
    
- Ejemplos:
    
    - VPS barato de DigitalOcean, Linode, Hetzner, Contabo, Oracle Cloud Free Tier.
        
    - También podrías usar una Raspberry Pi con IP pública o expuesta por DMZ.
        

📌 Este servidor actuará como "relay" o "punto de acceso" a tu red local.

---

### 2. **Dominio (opcional pero recomendado)**

- Puedes usar la IP pública del VPS directamente, pero un **dominio facilita el acceso** y la configuración de SSL.
    
- Puedes usar dominios gratuitos (como `freenom.com` o subdominios de `duckdns.org`) si estás empezando.
    

---

### 3. **Un software de túnel inverso**

Puedes:

- 🔧 **Crear uno desde cero** (más complejo)
    
- 🛠 O usar herramientas como:
    

#### Opción A: **Usar FRP (Fast Reverse Proxy)**
![architecture](https://github.com/fatedier/frp/raw/dev/doc/pic/architecture.png)
- Muy usado para esto.
- Cliente se instala en tu PC (localhost).
- Servidor se instala en el VPS.
[FRP GitHub](https://github.com/fatedier/frp)

#### Opción B: **Escribir tu propio túnel con Node.js, Go o Python**

- Puedes usar WebSockets, TCP Sockets o SSH Tunnels.
    
- Pero deberás manejar:
    
    - Persistencia
        
    - Autenticación
        
    - Multiplexación de puertos
        
    - Seguridad (TLS)
        
    - Gestión de clientes, reconexión, etc.
        

---

## 🚧 ¿Y si no tienes VPS?

Entonces **no puedes crear tu propia red pública**, porque no tienes un punto de entrada a Internet. Pero puedes:

- Usar servicios externos como:
    
    - `Ngrok`, `Cloudflare Tunnel`, `Serveo`, etc.
        
- O exponer tu IP doméstica (no recomendable para producción):
    
    - Configurar **port forwarding** en tu router.
        
    - Usar **DDNS** (No-IP, DuckDNS).
        
    - Exponer puertos como `5432`, `80`, etc., directamente.
        

⚠️ Esto tiene muchos riesgos de seguridad.

---

## ✅ En resumen

|Recurso|Necesario|Notas|
|---|---|---|
|**Servidor con IP pública**|✅ Obligatorio|Para actuar como relay (como hace Ngrok)|
|**Dominio propio**|❌ Opcional|Útil para accesibilidad, SSL, branding|
|**Software de túnel**|✅ Obligatorio|Puedes usar FRP, SSH, o programar el tuyo|
|**Certificados SSL**|❌ Opcional|Solo si vas a exponer tráfico HTTPS|