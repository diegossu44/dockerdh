## 1️⃣ Crear un contenedor con la imagen `php:7.4-apache`, llamado `web`, accesible en `localhost:8000`.

Ejecuta el siguiente comando para iniciar el contenedor:

```bash
docker run -d --name web -p 8000:80 php:7.4-apache
```

### 📷 Imagen:

![contenedor-imagen.png](attachment:5a7addb4-33d6-4547-8063-dc5cb3134e05:contenedor-imagen.png)

![imagen-docker.png](attachment:4fe797b1-dd9b-4785-89b8-5a338e155e13:imagen-docker.png)

### 📌 **Explicación**:

- `d` → Ejecuta el contenedor en segundo plano.
- `-name web` → Nombra el contenedor como `web`.
- `p 8000:80` → Asigna el puerto **8000** de tu máquina al puerto **80** del contenedor (Apache).
- `php:7.4-apache` → Usa la imagen de PHP 7.4 con Apache.

## 2️⃣ Subir al directorio `/var/www/html` un sitio web con:

Primero, crea una carpeta en tu sistema con los archivos necesarios:

```bash
mkdir -p mi_sitio_web
cd mi_sitio_web
```

### 📷 Imagen:

![creacion-carpeta.png](attachment:a4ace564-fa67-4913-bcbd-3d52c677cf56:creacion-carpeta.png)

### 📄 **Archivo `index.html`**

Crea el archivo `index.html` con los nombres del equipo:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Equipo de Desarrollo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Bienvenidos al Proyecto</h1>
    <p>Equipo: Diego y Hugo</p>
    <p>Este sitio está alojado en un contenedor Docker con PHP y Apache.</p>
    <p>Hora actual del servidor:</p>
    <?php include 'hora.php'; ?>
</body>
</html>
```

### 🎨 **Archivo `styles.css`**

Crea el archivo `styles.css` para darle estilo:

```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f4f4f4;
}
h1 {
    color: blue;
}
```

🕒 **Archivo `hora.php`**

Crea un archivo PHP que muestre la fecha y hora:

```php
<?php
date_default_timezone_set("Europe/Madrid");
echo "<p>" . date("Y-m-d H:i:s") . "</p>";
?>
```

### 📂 **Copiar los archivos al contenedor**

Para copiar los archivos al directorio `/var/www/html` del contenedor:

```bash
docker cp index.html web:/var/www/html/
docker cp styles.css web:/var/www/html/
docker cp hora.php web:/var/www/html/
```

### 📷 Imagen:

![copiar-archivos.png](attachment:141a2e3c-6903-4311-b41c-c88fd77870d4:copiar-archivos.png)

## 3️⃣ Verificar el sitio en el navegador.

🔗 Abre http://localhost:8080

### 📷 Imagen:

![sitio-web.png](attachment:bcddce93-1a8c-4859-93c3-28eee1bd6ab9:sitio-web.png)

### 📌 **Explicación**:

- Si todo está bien, deberías ver tu página web con la fecha y hora actualizada.

## 4️⃣ Verificar el sitio en el navegador.

Crea un archivo llamado `Dockerfile` en la carpeta `mi_sitio_web`:

```docker
# Usar la imagen base de PHP con Apache
FROM php:7.4-apache

# Copiar los archivos del sitio al contenedor
COPY index.html /var/www/html/
COPY styles.css /var/www/html/
COPY hora.php /var/www/html/

# Exponer el puerto 80
EXPOSE 80
```

### 📌 **Construir la imagen Docker**

Ejecuta este comando desde la carpeta donde está el `Dockerfile`:

```bash
docker build -t mi-sitio-web .
```

Esto creará una imagen llamada `mi-sitio-web`.

### 📷 Imagen:

![dockerfile.png](attachment:974f97d6-4d1e-4c03-b020-cfc244fefc36:dockerfile.png)

## 6️⃣ Subir la imagen a **Docker Hub**.

Primero, inicia sesión en Docker Hub:

```bash
docker login
```

### 📷 Imagen:

![docker-login.png](attachment:e10ae8b3-70ed-47b1-bcd6-30f3cf6ceb5b:docker-login.png)

**Etiqueta la imagen con tu usuario de Docker Hub**:

```bash
docker tag mi-sitio-web diegossu44/mi-sitio-web
```

### 📷 Imagen:

![etiqueta-imagen.png](attachment:4a403e8d-29a3-4f71-94b8-baaa926caf26:etiqueta-imagen.png)

**Sube la imagen a Docker Hub**:

```bash
docker push diegossu44/mi-sitio-web
```

### 📷 Imagen:

![subir-imagen.png](attachment:edb2053a-e495-4898-ba21-9ac31f9766ed:subir-imagen.png)

## 5️⃣ Descargar la imagen desde otra cuenta y ejecutar un contenedor con ella.

Desde otra computadora o cuenta de Docker Hub, puedes descargar y ejecutar la imagen con:

```bash
docker pull TU_USUARIO/mi-sitio-web
docker run -d -p 8000:80 TU_USUARIO/mi-sitio-web
```

### 📷 Imagen:

![descarga-imagen.png](attachment:e9d5756e-9666-43d8-abdc-cd4b50dbd2bf:descarga-imagen.png)

### 📷 Imagen:

![sitio-web-descargada-imagen.png](attachment:24b0db73-4c58-42f2-8fbd-7e0f7ce9f088:sitio-web-descargada-imagen.png)