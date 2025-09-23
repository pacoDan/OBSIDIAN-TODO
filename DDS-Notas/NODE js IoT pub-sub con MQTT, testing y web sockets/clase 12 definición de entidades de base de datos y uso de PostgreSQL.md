### Resumen
Lo primero que tenemos que hacer es definir las entidades de las bases de datos que vamos a utilizar. En nuestro proyecto vamos a usar **PostgreSQL,** una base de datos relacional.
El Agente va a conectarse al servidor en tiempo real y cada cierto tiempo va a reportar una métrica.  
La Métrica es cualquier valor que tiene un tipo, que va a ser almacenado en la base de datos.
![[Pasted image 20250106215911.png]]


Uso en TypeORM -> https://typeorm.io/#installation:~:text=%23-,Quick%20Start,-The%20quickest%20way
```
MyProject
├── src                   // place of your TypeScript code
│   ├── entity            // place where your entities (database models) are stored
│   │   └── User.ts       // sample entity
│   ├── migration         // place where your migrations are stored
│   ├── data-source.ts    // data source and all connection configuration
│   └── index.ts          // start point of your application
├── .gitignore            // standard gitignore file
├── package.json          // node module dependencies
├── README.md             // simple readme file
└── tsconfig.json         // TypeScript compiler options
```
 y para armar esa estructura se hace:
```sh
npx typeorm init
```

---
docker compose para el postgres:
```yml
services:
  postgres:
    image: postgres:13
    container_name: postgres
    environment:
      - POSTGRES_DB=store
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=admin123
    ports:
      - 5000:5432
    volumes:
      - ./postgres_data:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    environment:
      - PGADMIN_DEFAULT_EMAIL=admin@mail.com
      - PGADMIN_DEFAULT_PASSWORD=root
    ports:
      - 5050:80
```
para levantarlo es (docker):
```sh
docker compose up -d
```
y para conectarse es (con docker tambien):
```sh
docker run -it --rm --network platziverse-db_default postgres psql -h postgres -U admin -d store
```
```sh
Unable to find image 'postgres:latest' locally
latest: Pulling from library/postgres
fd674058ff8f: Already exists 
1eab12a50bdf: Pull complete 
5a81b4aedb94: Pull complete 
502eeeb4a17b: Pull complete 
e9e19177b318: Pull complete 
2068838cf5fa: Pull complete 
45a271dbb114: Pull complete 
8f9ac4ec849d: Pull complete 
9d8b60e88ddb: Pull complete 
3ec4ef471804: Pull complete 
16d755b48cd4: Pull complete 
3d5d11fb541c: Pull complete 
d8ab5fe30360: Pull complete 
d19370fe7a12: Pull complete 
Digest: sha256:888402a8cd6075c5dc83a31f58287f13306c318eaad016661ed12e076f3e6341
Status: Downloaded newer image for postgres:latest
Password for user admin: 
psql (17.2 (Debian 17.2-1.pgdg120+1), server 13.18 (Debian 13.18-1.pgdg120+1))
Type "help" for help.
store=# 
```
Mostrar bases de datos disponibles:
```sql
\l
```
Conectar a la base de datos store (aunque ya estás conectado, este comando sirve para cambiar de base de datos):
```sql
\c store
```
Mostrar tablas dentro de la base de datos actual:
```sql
\dt
```
Ejemplo  de como se fue usamos las cosas:
![[Pasted image 20250106213319.png]]




