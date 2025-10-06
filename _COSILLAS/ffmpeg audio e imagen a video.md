```sh
ffmpeg -loop 1 -i imagen.png -i "sdg 20251003_190655.aac" -c:v libx264 -pix_fmt yuv420p -c:a copy -shortest output.mp4
```

### Explicación paso a paso:

1. `-loop 1 -i imagen.png`: Lee la imagen y la repite indefinidamente para crear un video estático.
2. `-i "sdg 20251003_190655.aac"`: Lee el archivo de audio (usa comillas por el espacio en el nombre; si no hay espacio, quítalas).
3. `-c:v libx264`: Codifica el video con H.264 (buena calidad y compresión).
4. `-pix_fmt yuv420p`: Asegura compatibilidad con la mayoría de reproductores (evita errores de color).
5. `-c:a copy`: Copia el audio tal cual, sin recodificar, para no perder calidad.
6. `-shortest`: El video termina cuando acaba el audio (o la imagen, pero el audio es más largo).
7. `output.mp4`: Nombre del archivo de salida (cámbialo si quieres, e.g., `mi_video.mp4`).


