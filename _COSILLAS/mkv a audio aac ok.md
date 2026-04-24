
```sh
ffmpeg -i input.mkv -vn -acodec copy output.aac
```

- `-i input.mkv`: Especifica el archivo de entrada (reemplaza `input.mkv` con el nombre de tu archivo).
- `-vn`: Ignora el video (solo extrae audio).
- `-acodec copy`: Copia el audio sin recodificarlo (rápido y sin pérdida de calidad).
- `output.aac`: El archivo de salida (cambia la extensión según el formato original del audio, como `.aac`, `.ac3` o `.mp3` si quieres convertirlo).


```sh
ffmpeg -i input.mkv -vn -ar 44100 -ac 2 -b:a 192k output.mp3
```

- `-ar 44100`: Frecuencia de muestreo (44.1 kHz, estándar para MP3).
- `-ac 2`: Canales de audio (estéreo).
- `-b:a 192k`: Bitrate de audio (192 kbps, ajusta según necesites calidad/tamaño).

