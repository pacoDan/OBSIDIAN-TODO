**Sequelize** es un modelo de programación de mapeo de _objeto-relacional_ basado en promesas, para **Node.js.**
**Dos tipos de objetos:** modelos _nativos_ de **sequelize** y _servicios._
**Singleton** es un objeto que solo tiene una instancia. Cada vez que llamemos a una función no va a crear múltiples instancias.

Hacer dos entidades, una de `agent` y otra de `metrica`:
![[Pasted image 20250107214250.png]] 
https://platzi.com/home/clases/1151-nodejs-iot/8328-implementacion-de-modelos-con-sequelize/

para poner type ORM al proyecto se hace esto:
> You can also run `typeorm init` on an existing node project, but be careful - it may override some files you already have.
para conectarse:
```sh
docker run -it --rm  postgres psql -h 192.168.0.251 -U test -d test
```
```sh
docker run -it --rm --network platziverse-db_default postgres psql -h postgres -U test -d test
```
por si da error al conectarse y tira que password es incorrecto (Elimina el volumen persistente de datos) :
```sh
sudo rm -rf ./postgres_data
```


---
instalaciones para que funcione:
1. - Install the npm package:
        `npm install typeorm --save`
    - You need to install `reflect-metadata` shim:
        `npm install reflect-metadata --save`
        and import it somewhere in the global place of your app (for example in `app.ts`):
        `import "reflect-metadata"`
    - You may need to install node typings:
        `npm install @types/node --save-dev`
    - Install a database driver:
        - for **PostgreSQL** or **CockroachDB**
            
            `npm install pg --save`
---
para probar desde consola:
Mostrar bases de datos disponibles:
```sql
\l
```
Conectar a la base de datos store (aunque ya estás conectado, este comando sirve para cambiar de base de datos):
```sql
\c store
```
```sql
\c test
```
Mostrar tablas dentro de la base de datos actual:
```sql
\dt
```
Ver contenido de las tablas:
```sql
SELECT * FROM agent;
SELECT * FROM metric;
```
Si quieres verificar la estructura de las tablas, como sus columnas y tipos de datos, puedes usar:
```sql
\d agent
\d metric
```

RESULTADOS DE EJEMPLO::
```
test=# \c test  
psql (17.2 (Debian 17.2-1.pgdg120+1), server 13.18 (Debian 13.18-1.pgdg120+1))  
You are now connected to database "test" as user "test".  
test=# SELECT * FROM agent;  
SELECT * FROM metric;  
id | uuid | username | name | hostname | pid | connected  
----+-------------+------------+------------+-----------+------+-----------  
1 | unique-uuid | agent_user | Agent Name | localhost | 1234 | t  
(1 row)  
  
id | type | value | agentId  
----+------+-------+---------  
1 | CPU | 85% | 1  
(1 row)  
  
test=# \d agent  
\d metric  
Table "public.agent"  
Column | Type | Collation | Nullable | Default  
-----------+------------------------+-----------+----------+-----------------------------------  
id | integer | | not null | nextval('agent_id_seq'::regclass)  
uuid | character varying(255) | | not null |  
username | character varying(255) | | not null |  
name | character varying(255) | | not null |  
hostname | character varying(255) | | not null |  
pid | integer | | not null |  
connected | boolean | | not null | false  
Indexes:  
"PK_1000e989398c5d4ed585cf9a46f" PRIMARY KEY, btree (id)  
"UQ_72d4700019c467b7458aae91df9" UNIQUE CONSTRAINT, btree (uuid)  
Referenced by:  
TABLE "metric" CONSTRAINT "FK_07bba2fba9948ab2825c309dd47" FOREIGN KEY ("agentId") REFERENCES agent(id)  
  
Table "public.metric"  
Column | Type | Collation | Nullable | Default  
---------+------------------------+-----------+----------+------------------------------------  
id | integer | | not null | nextval('metric_id_seq'::regclass)  
type | character varying(255) | | not null |  
value | text | | not null |  
agentId | integer | | |  
Indexes:  
"PK_7d24c075ea2926dd32bd1c534ce" PRIMARY KEY, btree (id)  
Foreign-key constraints:  
"FK_07bba2fba9948ab2825c309dd47" FOREIGN KEY ("agentId") REFERENCES agent(id)
```
Ejemplo  de como se fue usamos las cosas:
![[Pasted image 20250106213319.png]]

