# 📌 Manual Paso a Paso para el Uso de Docker Desktop

## 🚀 Introducción

**Docker Desktop** es una aplicación que permite la gestión y ejecución de contenedores Docker en sistemas operativos Windows y macOS. Este manual proporciona una guía paso a paso para instalar, configurar y utilizar Docker Desktop de manera eficiente.

------

## ✅ Requisitos Previos

Antes de instalar Docker Desktop, asegúrate de cumplir con los siguientes requisitos:

- **Windows:** Windows 10 (versión 1903 o superior) o Windows 11 con WSL 2 habilitado.
- **Mac:** macOS 11 (Big Sur) o superior con Apple Silicon o procesador Intel.
- **Memoria RAM:** Mínimo **4 GB** recomendados.
- **Espacio en Disco:** Al menos **10 GB** de espacio libre.
- **Conexión a Internet:** Requerida para la descarga e instalación.

------

## 🛠 Instalación de Docker Desktop

### 🔽 Descargar Docker Desktop

1. Ve al sitio oficial de Docker: [🌐 Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Descarga la versión correspondiente a tu sistema operativo (Windows o macOS).

### 📥 Instalar Docker Desktop

#### 🖥 **Windows:**

1. Ejecuta el archivo **.exe** descargado.
2. Selecciona la opción para habilitar **WSL 2** (si es compatible con tu sistema).
3. Sigue las instrucciones del instalador y **reinicia** tu equipo si es necesario.

#### 🍏 **Mac:**

1. Abre el archivo **.dmg** descargado.
2. Arrastra el icono de **Docker** a la carpeta `Aplicaciones`.
3. Abre Docker Desktop desde `Aplicaciones` y sigue las instrucciones de configuración inicial.

------

## ⚙️ Configuración Inicial

- Abre **Docker Desktop** tras la instalación.
- Acepta los términos y condiciones.
- *(Opcional)* Configura el uso de recursos en "Settings" (**CPU, memoria y disco**).
- Asegúrate de que **Docker Engine** esté corriendo (**verás el icono de Docker en la barra de tareas o menú superior**).

------

## 🏗 Uso Básico de Docker

### 🔍 Verificar la Instalación

Abre una terminal (**PowerShell en Windows**, **Terminal en macOS**) y ejecuta:

```sh
docker --version
```

Si ves un número de versión, significa que **Docker está instalado correctamente**. ✅

### 🎯 Ejecutar un Contenedor de Prueba

Para comprobar que Docker funciona, ejecuta:

```sh
docker run hello-world
```

📢 Esto descargará y ejecutará un contenedor de prueba, mostrando un mensaje de confirmación.

### 📦 Descargar y Ejecutar una Imagen de Docker

Ejemplo con **Nginx**:

```sh
docker pull nginx
```

Para ejecutar el contenedor:

```sh
docker run -d -p 8080:80 nginx
```

🌍 Accede a `http://localhost:8080` para ver el servidor web en ejecución.

### 📜 Listar Contenedores Activos

```sh
docker ps
```

Para ver **todos** los contenedores, incluyendo los detenidos:

```sh
docker ps -a
```

### ⏹ Detener y Eliminar Contenedores

Para **detener** un contenedor:

```sh
docker stop <ID_DEL_CONTENEDOR>
```

Para **eliminarlo**:

```sh
docker rm <ID_DEL_CONTENEDOR>
```

------

## 🔧 Configuración Avanzada

### 📂 Configurar Volúmenes

Para persistir datos entre reinicios de contenedores:

```sh
docker volume create mi-volumen
```

Para montar el volumen en un contenedor:

```sh
docker run -d -v mi-volumen:/app/data nginx
```

### 🌐 Configurar Redes Personalizadas

Para crear una red personalizada:

```sh
docker network create mi-red
```

Para conectar un contenedor a la red:

```sh
docker run -d --network mi-red nginx
```

### 🏗 Construir una Imagen Personalizada

Crea un archivo `Dockerfile` con el siguiente contenido:

```dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y curl
CMD ["bash"]
```

Construye la imagen con:

```sh
docker build -t mi-imagen .
```

Ejecuta un contenedor basado en la imagen:

```sh
docker run -it mi-imagen
```

------

