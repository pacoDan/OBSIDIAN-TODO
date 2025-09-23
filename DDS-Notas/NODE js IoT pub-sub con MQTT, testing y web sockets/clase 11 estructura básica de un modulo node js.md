Desarrollo de PLATZIVERSE DB que es el componente que gestiona la base de datos

```sh
npm init
```
```sh
npm init -y #te ahorra muchos pasos
```
comando para la terminal que facilita un poco la vida, crea el archivo LICENSE, el .gitignore con la config para node, y el package.json
```sh
npx license mit && npx gitignore node && git init && npm init -y && touch index.js readme.md
```
ejemplo de uso de un archivo js en la consola (en version antes de node 16):
![[Pasted image 20250106191634.png]]
 el proyecto estaría quedando asi:
```sh
 ╰─❯ tree
.
├── index.js
├── LICENSE
├── package.json
└── readme.md

1 directory, 4 files

╰─❯ node
Welcome to Node.js v22.11.0.
Type ".help" for more information.
> const setupDatabase =  require('./')
undefined
> setupDatabase()
Promise {
  { Agent: {}, Metric: {} },
  [Symbol(async_id_symbol)]: 94,
  [Symbol(trigger_async_id_symbol)]: 6
}
>
```
```node
╰─❯ cat index.js
'use strict'
module.exports = async function (config) {
  const Agent = {}
  const Metric = {}
  return {
    Agent,
    Metric
  }
}
```


Instalar standard: 
```sh
npm i --save-dev standard
```
configurar en el package.json nuestro script para visualizar posibles errores de escritura nuestra:
```json
...
scripts: { 
	...
	"lint": "standard",
	...
}
...
```
Ejecutar en terminal:
```sh
npm run lint
```
y corregir errores con: 
```sh
npx standard --fix
```
