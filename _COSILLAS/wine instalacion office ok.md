office 2010 PACK
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OF2K10SP2.iso /tmp/office_iso

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
cp -r /tmp/office_iso/ ~/.wine/drive_c/

# 4. Desmontar y limpiar el punto de montaje
sudo umount /tmp/office_iso
sudo rmdir /tmp/office_iso

# 5. Verificar en Wine (opcional: abre el explorador para ver los archivos en C:)
wine explorer
```
office 16, siempre tratar de que el name este sin espacios
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso_16

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OFFICE_PROFESIONAL_2016.iso /tmp/office_iso_16

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
sudo cp -r /tmp/office_iso_16/ ~/.wine/drive_c/

# 4. Desmontar y limpiar el punto de montaje
sudo umount /tmp/office_iso_16
sudo rmdir /tmp/office_iso_16

# 5. Verificar en Wine (opcional: abre el explorador para ver los archivos en C:)
wine explorer
```

winetricks dotnet40 vcrun2008

```sh
sudo apt install winetricks
winetricks dotnet40
```


