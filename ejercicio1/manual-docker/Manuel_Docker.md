# 📌 Manual Paso a Paso para el Uso de Docker Desktop

## 🚀 Introducción

**Docker Desktop** es una aplicación que permite la gestión y ejecución de contenedores Docker en sistemas operativos Windows y macOS. Este manual proporciona una guía paso a paso para instalar, configurar y utilizar Docker Desktop de manera eficiente.

------

## ✅ Requisitos Previos

Antes de instalar Docker Desktop, asegúrate de cumplir con los siguientes requisitos:

🔹 **Windows:** Windows 10 (versión 1903 o superior) o Windows 11 con WSL 2 habilitado.

🔹 **Mac:** macOS 11 (Big Sur) o superior con Apple Silicon o procesador Intel.

🔹 **Memoria RAM:** Mínimo **4 GB** recomendados.

🔹 **Espacio en Disco:** Al menos **10 GB** de espacio libre.

🔹 **Conexión a Internet:** Requerida para la descarga e instalación.

------

## 🛠 Instalación de Docker Desktop

### 🔽 Descargar Docker Desktop

1️⃣ Ve al sitio oficial de Docker: [🌐 Docker Desktop](https://www.docker.com/products/docker-desktop)

2️⃣ Descarga la versión correspondiente a tu sistema operativo (Windows o macOS).

### 📥 Instalar Docker Desktop

### 🖥 **Windows:**

1️⃣ Ejecuta el archivo **.exe** descargado.

2️⃣ Selecciona la opción para habilitar **WSL 2** (si es compatible con tu sistema).

3️⃣ Sigue las instrucciones del instalador y **reinicia** tu equipo si es necesario.

### 🍏 **Mac:**

1️⃣ Abre el archivo **.dmg** descargado.

2️⃣ Arrastra el icono de **Docker** a la carpeta `Aplicaciones`.

3️⃣ Abre Docker Desktop desde `Aplicaciones` y sigue las instrucciones de configuración inicial.

------

## ⚙️ Configuración Inicial

✅ Abre **Docker Desktop** tras la instalación.

✅ Acepta los términos y condiciones.

✅ *(Opcional)* Configura el uso de recursos en "Settings" (**CPU, memoria y disco**).

✅ Asegúrate de que **Docker Engine** esté corriendo (**verás el icono de Docker en la barra de tareas o menú superior**).

------

## 🏗 Uso Básico de Docker

### 🔍 Verificar la Instalación

Abre una terminal (**PowerShell en Windows**, **Terminal en macOS**) y ejecuta:

```bash
docker --version
```

Si ves un número de versión, significa que **Docker está instalado correctamente**. ✅

### 🎯 Ejecutar un Contenedor de Prueba

Para comprobar que Docker funciona, ejecuta:

```bash
docker run hello-world
```

📢 Esto descargará y ejecutará un contenedor de prueba, mostrando un mensaje de confirmación.

### 📷 Imagen:

![contenedor-prueba.png](attachment:8b9bece9-e7f2-4073-9b99-5ce228d879ae:contenedor-prueba.png)

### 📦 Descargar y Ejecutar una Imagen de Docker

Ejemplo con **Nginx**:

```bash
docker pull nginx
```

Para ejecutar el contenedor:

```bash
docker run -d -p 8080:80 nginx
```

🌍 Accede a `http://localhost:8080` para ver el servidor web en ejecución.

### 📷 Imagen:

![ejecucion-nginx.png](attachment:204ee9a8-c8d5-420c-88d7-29321971f403:ejecucion-nginx.png)

### 📜 Listar Contenedores Activos

```bash
docker ps
```

Para ver **todos** los contenedores, incluyendo los detenidos:

```bash
docker ps -a
```

### 📷 Imagen:

![listado-contendedores.png](attachment:ff8b3de2-28a4-48c0-8896-c259be3365c0:listado-contendedores.png)

### ⏹ Detener y Eliminar Contenedores

Para **detener** un contenedor:

```bash
docker stop <ID_DEL_CONTENEDOR>
```

Para **eliminarlo**:

```bash
docker rm <ID_DEL_CONTENEDOR>
```

------

### 📷 Imagen:

![eliminacion-contendedores.png](attachment:1fd24754-0c06-4e93-84a6-83045e51ac67:eliminacion-contendedores.png)

## 🔧 Configuración Avanzada

### 📂 Configurar Volúmenes

Para persistir datos entre reinicios de contenedores:

```bash
docker volume create mi-volumen
```

Para montar el volumen en un contenedor:

```bash
docker run -d -v mi-volumen:/app/data nginx
```

### 📷 Imagen:

![configuracion-volumenes.png](attachment:c3cdf0ee-28aa-48c7-ae8d-84f5c0e1288b:configuracion-volumenes.png)

### 🌐 Configurar Redes Personalizadas

Para crear una red personalizada:

```bash
docker network create mi-red
```

Para conectar un contenedor a la red:

```bash
docker run -d --network mi-red nginx
```

### 📷 Imagen:

![configuracion-redes.png](attachment:ba1db377-b6b5-4b0d-bf93-767154cf371c:configuracion-redes.png)

### 🏗 Construir una Imagen Personalizada

Crea un archivo `Dockerfile` con el siguiente contenido:

```bash
FROM ubuntu:latest
RUN apt-get update && apt-get install -y curl
CMD ["bash"]
```

### 📷 Imagen:

![dockerfile.png](attachment:4b95b561-ade4-4938-b114-64df170d466c:dockerfile.png)

Construye la imagen con:

```bash
docker build -t mi-imagen .
```

Ejecuta un contenedor basado en la imagen:

```bash
docker run -it mi-imagen
```

### 📷 Imagen:

![construccion-imagen-dockerfile.png](attachment:e5772028-7526-4b18-bc30-24c86cfec9f3:construccion-imagen-dockerfile.png)

### **🧑‍💻 Responsables:**  @Diego Suárez