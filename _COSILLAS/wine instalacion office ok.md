office 2010 PACK, el OF2K10SP2.iso contiene el setup.exe junto con las medicinas
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OF2K10SP2.iso /tmp/office_iso

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
sudo cp -r /tmp/office_iso/ ~/.wine/drive_c/

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
office 2013, siempre tratar de que el name este sin espacios
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso_13

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OFFICE_PROFESIONAL_2013.iso /tmp/office_iso_13

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
sudo cp -r /tmp/office_iso_13/ ~/.wine/drive_c/

# 4. Desmontar y limpiar el punto de montaje
sudo umount /tmp/office_iso_13
sudo rmdir /tmp/office_iso_13

# 5. Verificar en Wine (opcional: abre el explorador para ver los archivos en C:)
wine explorer
```
office 2010, siempre tratar de que el name este sin espacios
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso_10

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OFFICE_PROFESIONAL_2010.iso /tmp/office_iso_10

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
sudo cp -r /tmp/office_iso_10/ ~/.wine/drive_c/

# 4. Desmontar y limpiar el punto de montaje
sudo umount /tmp/office_iso_10
sudo rmdir /tmp/office_iso_10

# 5. Verificar en Wine (opcional: abre el explorador para ver los archivos en C:)
wine explorer
```
key 2010 OK: `4DRT4-F2M76-3WDJB-XGTRR-QF8KH`
6QFDX-PYH2G-PPYFD-C7RJM-BBKQ8  
BDD3G-XM7FB-BD2HM-YK63V-VQFDK  
HXJQ4-VT6T8-7YPRK-R2HQG-CYPPY  
6R7J3-K4CB9-PG7BR-TVDBG-YPGBD  
4DDJ8-DM67D-GJPT2-32H93-9MMWK  
82DB6-BXG6H-QKBT6-3G42H-PPWM3  
D34M3-3279D-HHPB3-DQPPQ-JHHFX  
24PR2-JW928-QPKTK-CPD26-RYV3C  
4JPCP-DJF9V-WX7PT-B9WX2-R47C6  
7TF8R-933DG-MCBQR-TXPM7-G4JRM  
6R7J3-K4CB9-PG7BR-TVDBG-YPGBD  
Microsoft Office Pro 2010
Software de procesamiento de textos
J3QMF-FB7TM-GR3XT-QPFKX-CX4K8  
6DC8G-JY2KM-HKKJM-GGGG8-2K4C2  
Microsoft Office Home and Business 2010  
HTYPY-2TTJD-XFKXJ-D839V-FGDR3  
Office Professional Plus 2010  
VYBBJ-TRJPB-QFQRF-QFT4D-H3GVB  
Office Home and Business 2010
D6QFG-VBYP2-XQHM7-J97RH-VVRCK



office 2007, siempre tratar de que el name este sin espacios OK! FUNCIONANDO!
```sh
# 1. Crear punto de montaje temporal en /tmp
sudo mkdir -p /tmp/office_iso_7

# 2. Montar el ISO (ajusta la ruta del ISO si es necesario)
sudo mount -o loop ~/Descargas/OFFICE_PROFESIONAL_2007.iso /tmp/office_iso_7

# 3. Copiar todo el contenido del ISO directamente a C: de Wine
sudo cp -r /tmp/office_iso_7/ ~/.wine/drive_c/

# 4. Desmontar y limpiar el punto de montaje
sudo umount /tmp/office_iso_7
sudo rmdir /tmp/office_iso_7

# 5. Verificar en Wine (opcional: abre el explorador para ver los archivos en C:)
wine explorer
```
Office 2007 All In oNe  By BoRr@sS 2007
Podeis usar cualquiera de estos seriales para instalar los OFFICE
`VB48G-H6VK9-WJ93D-9R6RM-VP7GT`
`KGFVY-7733B-8WCK9-KTG64-BC7D8`
Para el Microsoft SharePoint Designer 2007 Usar este
`HCFPT-K86VV-DCKH3-87CCR-FM6HW`
Nada de lo que hay aqui en esta suite requiere activacion.


winetricks dotnet40 vcrun2008

```sh
sudo apt install winetricks
winetricks dotnet40 corefonts msxml6 riched20 gdiplus
winetricks corefonts msxml6 riched20 gdiplus
winetricks msxml6 msftedit riched20 riched30 vb6run corefonts
```

ESTO QUITA TODO LO QUE TENIAS INSTALADO: básicamente borra todo tu C en windows
error: wine: could not load kernel32.dll, status c0000135
```sh
mv ~/.wine ~/.wine.old  # or rm -r ~/.wine
winecfg                 # This will create a new default Wine prefix
```


mejorar esto: https://www.linuxparty.es/recursos/publicidad/113-wine/4486-instalar-microsoft-office-en-linux-con-wine.html
