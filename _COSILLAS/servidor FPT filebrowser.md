https://filebrowser.org/installation.html#__tabbed_1_3
https://github.com/filebrowser/filebrowser#project-status
#### Opción 2: FileBrowser (Más Ligero, Solo para Navegación y Multimedia Básica)

Si prefieres algo simple sin base de datos, FileBrowser es un gestor de archivos web minimalista. Permite navegar carpetas como en Windows Explorer, abrir imágenes/videos en el navegador y subir archivos. Soporta preview de multimedia vía HTML5.

**Pasos de Instalación:**

- Instala dependencias:
```sh
sudo apt install golang-go
```

- Descarga e instala:
    ```sh
    wget https://github.com/filebrowser/get/releases/download/v2.24.0/linux-amd64-filebrowser.tar.gz tar -xzf linux-amd64-filebrowser.tar.gz sudo mv filebrowser /usr/local/bin/
    ```
- Crea un directorio para config:
    ```sh
    sudo mkdir /srv/filebrowser sudo useradd -r -g www-data -d /srv/filebrowser -s /bin/false filebrowser sudo chown -R filebrowser:www-data /srv/filebrowser
    ```
- Genera config inicial:
    ```sh
    filebrowser config init -c /etc/filebrowser.json
    ```
    Edita `/etc/filebrowser.json` para tu carpeta raíz (ej. `"root": "/home/tu_usuario/archivos"`) y usuario/contraseña.
- Configura como servicio systemd: Crea `/etc/systemd/system/filebrowser.service`:
    
    
    ```json
	[Unit]
	Description=File Browser
	After=network.target
	
	[Service]
	ExecStart=/usr/local/bin/filebrowser -c /etc/filebrowser.json
	Restart=always
	User=filebrowser
	
	[Install]
	WantedBy=multi-user.target
    ```
    
    Inicia:
```sh
sudo systemctl daemon-reload
sudo systemctl enable --now filebrowser
```
- Accede vía navegador en `http://tu_ip:8080`. Configura HTTPS con un proxy como Nginx si necesitas.

**Ventajas:**

- Muy ligero (sin DB), ideal para servidores pequeños.
- Preview de videos/imágenes directamente (soporta MP4, WebM).
- Autenticación simple por usuario/IP.

**Limitaciones:**

- Menos features que Nextcloud (no edita archivos ni colabora).
- Para videos avanzados, integra FFmpeg para conversión.


#### Alternativa Híbrida: FTP + Web GUI (Si Insistes en FTP)

Si quieres FTP tradicional con una capa web, instala vsftpd para transferencias y usa Webmin (GUI web para admin) o Tiny File Manager (simple explorador web).
