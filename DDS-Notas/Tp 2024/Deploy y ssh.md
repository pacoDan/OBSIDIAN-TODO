como poner las variables de entorno en algún linux o dentro del container
```sh
export DB_URL="jdbc:mysql://autorack.proxy.rlwy.net:13447/db_dds?serverTimezone=UTC"
export DB_USERNAME="root"
export DB_PASSWORD="hqFHHPZdQtiyYECnYkVsqAxzjmuYUYVx"
```

nueva vianda
[[https://tpdds-production.up.railway.app/viandas/nueva]]


creación y pusheo de la imagen (estando en la carpeta del proyecto, en nuestro caso dentro de la carpeta  **tp-dds**, y mi usuario en docker  hub es jhonpaco, tuve que crear un repositorio dentro de docker hub llamado **tp-dds** tambien)
```sh
mvn clean
docker build -t jhonpaco/tp_dds .
docker push jhonpaco/tp_dds
```


nuevo persistence.xml si usara las variables de entorno
```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://java.sun.com/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://java.sun.com/xml/ns/persistence
    http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd"
             version="2.0">

    <persistence-unit name="simple-persistence-unit" transaction-type="RESOURCE_LOCAL">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>

        <properties>
            <property name="hibernate.archive.autodetection" value="class"/>
            <property name="hibernate.connection.driver_class" value="com.mysql.cj.jdbc.Driver"/>
            <property name="hibernate.connection.url" value="${env:DB_URL}"/>
            <property name="hibernate.connection.username" value="${env:DB_USERNAME}"/>
            <property name="hibernate.connection.password" value="${env:DB_PASSWORD}"/>
            <property name="hibernate.hikari.connectionTimeout" value="20000"/>
            <property name="hibernate.hikari.minimumIdle" value="10"/>
            <property name="hibernate.hikari.maximumPoolSize" value="20"/>
            <property name="hibernate.hikari.idleTimeout" value="300000"/>
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.format_sql" value="true"/>
            <property name="use_sql_comments" value="true"/>
            <property name="hibernate.hbm2ddl.auto" value="update"/>
        </properties>
    </persistence-unit>
</persistence>
```



.ssh/config


```
Host pc
Hostname 192.168.0.139
	User daniel
```


```sh
scp carpetaMia/1.mov server1:/root/
```
es igual a esta:
```sh
rsync  --partial --progress -rsh=ssh carpetaMia/1.mov server1:1.mov
```
con ssh-add -l se muestras las keys cargadas



acceso a otra maquina con mis keys (de mi maquina local) con el método de forwardeo de puertos con Jump

```sh
ssh -J server1 server2
```

ahora pasando a través de varios servers a la remota llamada linux

```sh
ssh -J server1,server2 linux
```


copiar los archivos a 
en el archivo ``` /etc/ssh/sshd_config ``` ver que estén estas lineas y no comentadas:
```
PubkeyAuthentication yes
AuthorizedKeysFile     .ssh/authorized_keys
```

