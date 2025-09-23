# Instalación de Office usando Wine en Arch Linux

A continuación se resumen los comandos utilizados para instalar Office desde una imagen ISO usando Wine:

```sh
# Instalar Wine y fastfetch
sudo pacman -S wine fastfetch

# Limpiar pantalla y mostrar información del sistema
clear
fastfetch

# Configurar Wine por primera vez
winecfg

# Abrir consola de Wine
wine cmd

# Navegar a la carpeta Descargas y listar archivos
cd Descargas
ls

# Crear punto de montaje para la ISO
mkdir -p ~/iso_mount

# Montar la imagen ISO en el punto de montaje
sudo mount -o loop ~/Descargas/OF2K10SP2.iso ~/iso_mount

# Configurar Wine para mapear la unidad Z: a la carpeta montada
ln -s ~/iso_mount ~/.wine/dosdevices/z:

# (Si es necesario, usar sudo para crear el enlace simbólico)
sudo ln -s ~/iso_mount ~/.wine/dosdevices/z:

# Abrir el explorador de Windows en Wine
wine explorer

# Copiar el contenido de la ISO a la raíz de la unidad C: de Wine
cp -r ~/iso_mount/* ~/.wine/drive_c/

# Abrir el explorador de Windows para verificar los archivos
wine explorer
```


https://ruados.github.io/articles/2021-05/office365-wine

https://www.reddit.com/r/linux4noobs/comments/1i2uu9y/wine_microsoft_office/

https://forum.winehq.org/viewtopic.php?t=39366

https://appdb.winehq.org/objectManager.php?sClass=version&iId=26323

https://appdb.winehq.org/objectManager.php?sClass=version&iId=37735

https://forum.endeavouros.com/t/has-anyone-managed-to-install-microsoft-office-365-via-wine/10051/12





