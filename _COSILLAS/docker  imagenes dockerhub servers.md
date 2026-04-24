Start a `mssql-server` instance using the latest update for SQL Server 2022:
```sh
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Pi3141592654" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
```

```sh
# Detener todos los contenedores
docker stop $(docker ps -aq)
# Borrar todos los contenedores
docker rm $(docker ps -aq)
# Borrar todas las imágenes
docker rmi $(docker images -q)
# Limpiar archivos temporales (incluyendo volúmenes)
docker system prune -a --volumes
```


