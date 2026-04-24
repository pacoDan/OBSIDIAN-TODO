escritorio remoto windows 
```sh
# Terminal 1 - TCP (obligatorio)
ngrok tcp 3389
# Terminal 2 - UDP (opcional, para UDP redirection en Win10+)
ngrok udp 3389
```
nomachine
```sh
# Principal (suficiente 95% casos)
ngrok tcp 4000
# Multimedia/audio (opcional)
ngrok udp 4011    # O rango 4011-4020
```

