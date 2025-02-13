## 1️⃣ Crear una red `bridge` llamada `redbd`.

En Docker, los contenedores pueden comunicarse entre sí usando una **red personalizada**.

```bash
docker network create redbd
```

### 📷 Imagen:

![creacion-red.png](attachment:ab35a2b8-347b-4963-829c-aff2ad4c84bf:creacion-red.png)

### 📌 **Explicación**:

`docker network create redbd` → Crea una red llamada `redbd` de tipo `bridge` (para conectar contenedores entre sí).

## 2️⃣ Crear un contenedor con MariaDB en la red `redbd`, accesible en el puerto `3306`, con contraseña y volumen persistente.

MariaDB es el motor de base de datos que usaremos. Para ejecutarlo en un contenedor:

```bash
docker run -d --name mariadb-container --network redbd -p 3306:3306 -v datos-mariadb:/var/lib/mysql -e MYSQL_PASSWORD=daw -e MYSQL_USER=daw -e MYSQL_DATABASE=base -e MYSQL_ROOT_PASSWORD=root mariadb:latest
```

### 📷 Imagen:

![contenedor-mariadb.png](attachment:9d9a8ba4-f6ef-4460-928d-0db1d95b2506:contenedor-mariadb.png)

### 📌 **Explicación de los parámetros**:

- `d` → Ejecuta el contenedor en segundo plano.
- `-name mariadb-container` → Nombre del contenedor.
- `-network=redbd` → Lo conecta a la red `redbd`.
- `e MYSQL_ROOT_PASSWORD=root` → Establece la contraseña del usuario `root`.
- `e MYSQL_DATABASE=base` → Crea una base de datos llamada `base`.
- `e MYSQL_USER=daw` → Crea un usuario llamado `daw`.
- `e MYSQL_PASSWORD=daw` → Asigna la contraseña `daw` al usuario `daw`.
- `v datos-mariadb:/var/lib/mysql` → Usa un **volumen persistente** llamado `datos-mariadb` para almacenar la BD.
- `p 3306:3306` → Expone el puerto `3306` para conexiones externas.

## 3️⃣ Crear otro contenedor con **Adminer** o **phpMyAdmin** en la misma red.

Adminer es una interfaz gráfica para gestionar bases de datos.

```bash
docker run -d --name adminer-container --network redbd -p 8080:8080 adminer
```

### 📷 Imagen:

![contenedor-adminer.png](attachment:cf53bb34-e91b-4c9c-8128-ccb230c2af67:contenedor-adminer.png)

### 📌 **Explicación de los parámetros**:

- `d` → Ejecuta en segundo plano.
- `-name adminer-container` → Nombre del contenedor.
- `-network=redbd` → Lo conecta a la misma red `redbd`.
- `p 8080:8080` → Expone Adminer en el puerto `8080`.

## 4️⃣ Desde la interfaz web, crear una base de datos y una tabla.

Ahora puedes entrar a la interfaz de Adminer desde un navegador:

🔗 Abre http://localhost:8080

📌 **Datos de acceso**:

- **Servidor**: `mariadb-container`
- **Usuario**: `daw`
- **Contraseña**: `daw`
- **Base de datos**: `base`

### 📷 Imagen: Panel Login

![adminer-panel.png](attachment:a02268be-8f94-4b31-bc11-babc8dd8ebbb:cd9ad88f-86f1-4bd2-9bbb-1eb42bb0032c.png)

### 📷 Imagen: Panel BD

![sesion-adminer.png](attachment:f8d2b7e6-d5d4-4ec0-bc5c-5611804e387c:sesion-adminer.png)

### 📷 Imagen: Crear tabla

![creacion-tabla.png](attachment:fbbd5b83-a9ff-41ba-a4f6-b191b3673f1f:creacion-tabla.png)

### 📷 Imagen: Tabla usuarios

![tabla-usuarios.png](attachment:86e56d26-ef29-4f3d-9102-c54587376a3a:tabla-usuarios.png)

## 5️⃣ Borrar contenedores, red y volúmenes utilizados.

```bash
docker rm -f mariadb-container adminer-container
docker network rm redbd
docker volume rm datos-mariadb
```

![image.png](attachment:0bdcad7f-990b-4d05-8066-816fa559f379:image.png)

### 📌 **Explicación**:

- `docker rm -f mariadb-container adminer-container` → Borra los contenedores.
- `docker network rm redbd` → Elimina la red `redbd`.
- `docker volume rm datos-mariadb` → Borra los datos almacenados.