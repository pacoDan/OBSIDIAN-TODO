probando
Ejemplo parpadeo con dos leds:
```c
int amarillo = 13;
int rojo = 7;
int milisegundos = 300;
void setup() {
  pinMode(amarillo, OUTPUT);
  pinMode(rojo, OUTPUT);
}
void loop() {
  digitalWrite(amarillo, HIGH);
  digitalWrite(rojo, LOW);
  delay(milisegundos);
  digitalWrite(amarillo, LOW);
  digitalWrite(rojo, HIGH);
  delay(milisegundos * 2);
}
```
para SUBIR EL CODIGO JS AL ARDUINO
**prepara el firmware que le permite conectar al johnny-five**
![[Pasted image 20241223171028.png]]
código de la clase (funciona):
```js
var jf = require("johnny-five");
var circuito = new jf.Board();
circuito.on("ready", prender);
function prender() {
	var led_amarillo = new jf.Led(13);
	var led_azul = new jf.Led(7);
	led_amarillo.blink(200);
	led_azul.blink(700);
	console.log("Hay cuarentena y no plata, no hay pal Arduino");
}
```
![[Pasted image 20241223172248.png]]
código blink de su pagina (también funciona):
```js
const {Board, Led} = require("johnny-five");
const board = new Board();
board.on("ready", () => {
const led = new Led(13);
led.blink(200);
});
```

la de la clase es:
![[Pasted image 20241223165858.png]]
y
![[Pasted image 20241223165942.png]]
![[Pasted image 20241223165949.png]]





https://platzi.com/home/clases/1050-basico-programacion/5134-programacion-de-circuitos-con-c-arduino-y-sketch/ 
![[Pasted image 20241223141019.png]]
con JS
https://platzi.com/home/clases/1050-basico-programacion/5135-como-programar-un-arduino-con-javascript-y-node/
![[Pasted image 20241223141337.png]]


errores y soluciones:
permiso `sudo chmod 666 /dev/ttyUSB0`: 
```sh
╰─❯ node blink.js
1734985490833 Available /dev/ttyUSB0  
1734985490835 Connected /dev/ttyUSB0  
1734985490835 Error Error: Permission denied, cannot open /dev/ttyUSB0  
node:events:507
    const err = new ERR_UNHANDLED_ERROR(stringifiedEr);
                ^

Error [ERR_UNHANDLED_ERROR]: Unhandled error. ({
  type: 'error',
  timestamp: 1734985490835,
  class: 'Error',
  message: 'Error: Permission denied, cannot open /dev/ttyUSB0',
  data: null
})
    at Board.emit (node:events:507:17)
    at Board.log (/home/daniel/PROYECTOS/johnny-five/node_modules/johnny-five/lib/board.js:637:8)
    at Board.<computed> [as error] (/home/daniel/PROYECTOS/johnny-five/node_modules/johnny-five/lib/board.js:648:14)
    at Board.finalizeAndBroadcast (/home/daniel/PROYECTOS/johnny-five/node_modules/johnny-five/lib/board.js:363:12)
    at /home/daniel/PROYECTOS/johnny-five/node_modules/johnny-five/lib/board.js:147:18
    at SerialPort.<anonymous> (/home/daniel/PROYECTOS/johnny-five/node_modules/firmata-io/lib/firmata.js:613:9)
    at SerialPort.emit (node:events:518:28)
    at SerialPort.emit (node:domain:489:12)
    at SerialPort._error (/home/daniel/PROYECTOS/johnny-five/node_modules/@serialport/stream/lib/index.js:200:10)
    at /home/daniel/PROYECTOS/johnny-five/node_modules/@serialport/stream/lib/index.js:242:12 {
  code: 'ERR_UNHANDLED_ERROR',
  context: {
    type: 'error',
    timestamp: 1734985490835,
    class: 'Error',
    message: 'Error: Permission denied, cannot open /dev/ttyUSB0',
    data: null
  }
}

Node.js v22.11.0
╰─❯ sudo chmod 666 /dev/ttyUSB0
╰─❯ node blink.js              
1734985522925 Available /dev/ttyUSB0  
1734985522927 Connected /dev/ttyUSB0  
1734985526912 Repl Initialized  
>> Hay cuarentena y no plata, no hay pal Arduino

(To exit, press Ctrl+C again or Ctrl+D or type .exit)
>> 
```