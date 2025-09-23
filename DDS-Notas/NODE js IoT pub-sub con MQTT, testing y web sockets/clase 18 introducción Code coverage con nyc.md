el chiste aca es saber cuanto de nuestro código es usado en las pruebas
ejemplo:
![[Pasted image 20250108213659.png]]

agregar esto en el package.json  en scripts
```sh
"test": "set DEBUG=platziverse:* && nyc --reporter=lcov --report-dir=coverage/ ava tests/* --verbose && start coverage/lcov-report/index.html"
```
