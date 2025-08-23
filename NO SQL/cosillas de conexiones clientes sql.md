### **MariaDB (Reemplazo directo de MySQL)**

- Es el fork oficial de MySQL que viene en los repositorios de Arch
- Sintaxis idéntica a MySQL para consultas y comandos
- Instalación: `sudo pacman -S mariadb`
- Conexión: `mysql -u usuario -p`
- Compatible al 100% con aplicaciones MySQL existentes

### **PostgreSQL**

- Base de datos robusta y avanzada con excelente soporte de terminal
- Cliente de consola: `psql`
- Instalación: `sudo pacman -S postgresql`
- Conexión: `psql -U usuario -d basedatos`
- Sintaxis SQL estándar con extensiones avanzadas

### **SQLite**

- Base de datos ligera sin servidor, perfecta para desarrollo
- Cliente integrado: `sqlite3`
- Instalación: `sudo pacman -S sqlite`
- Uso: `sqlite3 archivo.db`
- Ideal para aplicaciones pequeñas y prototipos

### **MySQL Shell (Alternativa moderna)**

- Cliente oficial más avanzado que el mysql tradicional
- Soporte para JavaScript, Python y SQL
- Instalación desde AUR: `yay -S mysql-shell`
- Conexión: `mysqlsh usuario@servidor`
- Interfaz más interactiva y moderna

### **Bases de Datos NoSQL**

**MongoDB**

- Base de datos de documentos con cliente `mongosh`
- Instalación: `sudo pacman -S mongodb-bin`
- Conexión: `mongosh`

**Redis**

- Base de datos en memoria con `redis-cli`
- Instalación: `sudo pacman -S redis`
- Conexión: `redis-cli`

### **Recomendación Principal**

Para migrar desde MySQL en Arch, **MariaDB es tu mejor opción** ya que:

- Mantiene la misma sintaxis y comandos
- No requiere cambios en tus scripts existentes
- Está oficialmente soportado en Arch Linux
- Rendimiento igual o superior a MySQL