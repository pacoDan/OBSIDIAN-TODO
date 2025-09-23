https://testclient-cloud.mqtt.cool/
~~instalacion desde docker~~
```sh
docker run -it hivemq/mqtt-cli shell
```
### Flujo5
1. Con el colaborador físico, dar de alta una solicitud de apertura de heladera para donar una vianda.
2. Enviar, mediante el Broker, un mensaje al Sistema para simular que la heladera se abrió correctamente con la tarjeta del colaborador; suponiendo que el mismo “pasó a dejar/donar la vianda”.
3. Verificar que los puntos obtenidos hayan incrementado.

1)
user:
```
daniel_personafisica
```
contraseña:
```
Pi3141592654
```
crear heladera
http://localhost:8082/heladeras/nueva
agregar vianda
http://localhost:8082/viandas/nueva
ver viandas para solicitar la apertura
http://localhost:8082/viandas


2)
http://localhost:8082/viandas/nueva

ver puntos
http://localhost:8082/productosYservicios


suscribirse a heladera
```sh
mqtt-cli sub --host broker.mqtt.cool --port 1883 --topic heladera/abrir -d
```

publicador 
```sh
mqtt-cli pub --host broker.mqtt.cool --port 1883 --topic heladera/abrir --message 1287654786523674 -d
```
#### Explicación:
1. **`pub`**: Indica que estás publicando un mensaje.
2. **`--host broker.mqtt.cool`**: Dirección del broker MQTT al que te estás conectando.
3. **`--port 1883`**: El puerto del broker MQTT (1883 es el estándar para conexiones sin TLS).
4. **`--topic heladera/abrir`**: El topic en el que estás publicando.
5. **`--message 1287654786523674`**: El contenido del mensaje que estás publicando.
6. **`-d`**: Activa la salida en modo detallado (debug) para obtener más información durante la ejecución.
#### Nota:
- Si necesitas autenticarte con un usuario y contraseña, puedes agregar las opciones `--username` y `--password` al comando. Por ejemplo:
```sh
mqtt-cli pub --host broker.mqtt.cool --port 1883 --topic heladera/abrir --message 1287654786523674 --username usuario --password contraseña -d
```