El problema que estás experimentando se debe a que las firmas PGP de algunos paquetes no son reconocidas como confiables por `pacman`. Esto puede suceder por varias razones, como que las claves de los mantenedores de los paquetes no estén en tu llavero de claves o que haya un problema con la base de datos de claves.

Primero, intenta actualizar el llavero de claves de `pacman`:
```sh
sudo pacman-key --init
sudo pacman-key --populate archlinux
```
Verifica y actualiza las claves:
Si el paso anterior no resuelve el problema, puedes intentar actualizar las claves manualmente:
```sh
sudo pacman-key --refresh-keys
```
Elimina los paquetes dañados:
Si aún tienes problemas, puedes eliminar los paquetes dañados que se mencionan en los errores. Puedes hacerlo manualmente o usando el siguiente comando:
```sh
sudo pacman -Rns adwaita-icon-theme-legacy python-charset-normalizer gperftools v4l-utils dbus-glib libimobiledevice-glue python-pillow libspiro gnome-system-monitor libgme neon libmanette libmusicbrainz5 libsixel lollypop mesa-utils python-typeguard
```

```sh
sudo pacman -Syyu
```

###  Si el problema persiste

Si el problema persiste, puedes intentar eliminar el caché de paquetes y forzar la descarga de los paquetes nuevamente:
```sh
sudo pacman -Scc
```
### Considera deshabilitar la verificación de firmas (no recomendado)

Si nada de lo anterior funciona y necesitas urgentemente actualizar, puedes deshabilitar temporalmente la verificación de firmas. Sin embargo, esto no es recomendable por razones de seguridad:

Edita el archivo de configuración de `pacman`:
```sh
sudo nano /etc/pacman.conf
```
Busca la línea que dice `SigLevel` y cámbiala a:
```conf
SigLevel = Never
```