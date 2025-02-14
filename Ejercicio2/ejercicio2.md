### **📌 Paso 1: Descargar la imagen de MariaDB**

Ejecuta el siguiente comando para descargar la imagen oficial de MariaDB:

```bash
docker pull mariadb
docker images 
```

---

### **🚀 Paso 2: Crear y Configurar el Contenedor**

Ejecuta este comando para **crear y ejecutar** el contenedor con MariaDB:

```bash
docker run -d \  
--name bbdd \  
-p 3306:3306 \  
-v datos-mariadb:/var/lib/mysql \  
-e MYSQL_ROOT_PASSWORD=base \  
-e MYSQL_DATABASE=daw \  
-e MYSQL_USER=daw \  
-e MYSQL_PASSWORD=password \  
mariadb

docker ps  # Para ver si el contenedor está corriendo
```

---

### **▶️ Paso 3: Acceder a la Base de Datos**

Abre el cliente MySQL (no pudimos acceder, así que optamos por usar MariaDB) dentro del contenedor:

```bash
docker exec -it bbdd mariadb -u daw -ppassword
```

Ejecuta los siguientes comandos SQL:

```sql
SHOW DATABASES;
USE daw;
CREATE TABLE alumnos (
    id INT AUTO_INCREMENT PRIMARY KEY, 
    nombre VARCHAR(50), 
    edad INT
);

INSERT INTO alumnos (nombre, edad) VALUES ('Juan', 20), ('Ana', 22);

SELECT * FROM alumnos;
```

---

### **🗱️ Paso 4: Detener y Eliminar el Contenedor**

Detén el contenedor:

```bash
docker stop bbdd
docker ps  # Para verificar que se detuvo
```

Elimina el contenedor y verifica que el volumen persiste:

```bash
docker rm bbdd 
docker volume ls  # Verifica que el volumen 'datos-mariadb' sigue existiendo
```

---

### **♻️ Paso 5: Crear un Nuevo Contenedor con el Mismo Volumen**

Ejecuta un nuevo contenedor con el mismo volumen para verificar la persistencia de los datos:

```bash
docker run -d \  
--name bbdd-2 \  
-p 3306:3306 \  
-v datos-mariadb:/var/lib/mysql \  
-e MYSQL_ROOT_PASSWORD=base \  
-e MYSQL_DATABASE=daw \  
-e MYSQL_USER=daw \  
-e MYSQL_PASSWORD=password \  
mariadb
```

Conéctate al nuevo contenedor y verifica que los datos siguen ahí:

```bash
docker exec -it bbdd-2 mariadb -u daw -ppassword -e "SELECT * FROM daw.alumnos;"
```

✅ La persistencia del volumen funciona correctamente.

---

### **❌ Paso 6: Intentar Borrar la Imagen**

Prueba eliminar la imagen de MariaDB:

```bash
docker rmi mariadb
docker ps
```

📌 **Resultado esperado:** No puede eliminar la imagen porque el contenedor `bbdd-2` aún la está usando.

---

### **💥 Paso 7: Eliminar Todo (Contenedores, Volumen e Imagen)**

1️⃣ **Eliminar contenedores**  
2️⃣ **Eliminar el volumen**  

```bash
docker stop bbdd-2
docker rm bbdd-2
```

3️⃣ **Eliminar la imagen de MariaDB**  
4️⃣ **Verificar que todo se ha eliminado**  

```bash
docker rmi mariadb
docker ps -a 
docker images
docker volume ls
```

✅ ¡Todo ha sido eliminado correctamente! 🚀