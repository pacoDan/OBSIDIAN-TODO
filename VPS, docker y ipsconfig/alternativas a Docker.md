## **2. Podman** 🔹 _(Docker sin demonio y sin root)_

- **Qué es:** Alternativa a Docker más segura (no requiere demonio ni root).
    
- **Ventajas:**
    
    - Comandos casi idénticos a Docker.
        
    - Compatible con rootless containers.
        
    - Ideal para entornos de seguridad estricta.
        
- **Ejemplo:**
```sh
podman build -t miapp .
podman run -d -p 4000:4000 miapp
```
## **LXD / LXC** 📦 _(Contenedores de sistema completo)_

- **Qué es:** Contenedores que simulan un sistema operativo completo (no solo una app).
    
- **Ventajas:**
    
    - Más parecido a una máquina virtual, pero ligero.
        
    - Útil para entornos que necesitan _systemd_, múltiples servicios o configuraciones complejas.
        
- **Ejemplo:**
```sh
lxc launch images:ubuntu/22.04 miapp
lxc exec miapp -- bash
```
## **4. Distrobox** 🖥️ _(Entornos Linux dentro de Linux)_

- **Qué es:** Usa Podman/Docker para crear contenedores con cualquier distro Linux.
    
- **Ventajas:**
    
    - Puedes ejecutar Fedora, Arch, Debian… dentro de tu servidor.
        
    - Mantiene integración con tu sistema host.
        
- **Ejemplo:**
```sh
distrobox-create --name arch --image archlinux
distrobox-enter arch
```
## **5. Kubernetes (K3s o MicroK8s)** ☸️ _(para despliegues más grandes)_

- **Qué es:** Orquestador de contenedores para múltiples servicios.
    
- **Ventajas:**
    
    - Escalabilidad y resiliencia.
        
    - Ideal si tienes varios servicios o microservicios.
        
- **Ligero:** _K3s_ y _MicroK8s_ permiten usarlo incluso en un VPS pequeño.
    
- **Ejemplo K3s:**
```sh
curl -sfL https://get.k3s.io | sh -
```
## **6. NixOS / Nix** 📜 _(despliegues declarativos)_

- **Qué es:** Sistema y gestor de paquetes inmutable y reproducible.
    
- **Ventajas:**
    
    - Despliegues declarativos que se reconstruyen exactamente igual en cualquier servidor.
        
    - Ideal para CI/CD y reproducibilidad.
        
- **Ejemplo:**
```sh
nix-shell -p nodejs
```
## **7. Ansible + Docker** ⚙️ _(Infraestructura como código + contenedores)_

- **Qué es:** Herramienta para automatizar despliegues en múltiples servidores.
    
- **Ventajas:**
    
    - Controlas toda la configuración desde un playbook YAML.
        
    - Perfecto si manejas varios VPS.
        
- **Ejemplo:**
```sh
- hosts: servidor
  tasks:
    - name: Desplegar contenedor
      docker_container:
        name: miapp
        image: miimagen
        state: started
        ports:
          - "4000:4000"
```
💡 **Mi recomendación para algo rápido y portable:**

- Si es **una sola app** → **Docker** o **Podman**.
    
- Si quieres **un entorno de sistema completo** → **LXD**.
    
- Si necesitas **muchos servicios en producción** → **K3s** o **MicroK8s**.
    
- Si buscas **reproducibilidad extrema** → **Nix**.

