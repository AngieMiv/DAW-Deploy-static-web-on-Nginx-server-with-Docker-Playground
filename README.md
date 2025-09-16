# 🏁 Objetivo
Desplegar una página web estática en un servidor Nginx utilizando Docker Playground, para comprender los pasos básicos de despliegue en contenedores y servidores de aplicación web.

## 1️⃣ Requisitos previos
Cuenta gratuita en Play with Docker (login con cuenta de Docker Hub).
Conocimientos básicos de HTML y comandos de terminal.
Conexión a Internet.

## 2️⃣ Pasos de la práctica

### Paso 1: Acceso a Docker Playground
Entra en https://labs.play-with-docker.com/.
Inicia sesión creando una cuenta .
Pulsa “Start” y después “+ Add New Instance” para crear un nodo de trabajo. Verás un terminal en el navegador de una maquina linux.

### Paso 2: Crear la estructura de la página
Dentro de la terminal del nodo, crea un directorio para la página web:
```
mkdir miweb
cd miweb
```

Crea un archivo HTML sencillo:
`cat > index.html `

```<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi primera página en Docker</title>
</head>
<body>
  <h1>¡Hola desde Nginx en Docker!</h1>
  <p>Esta es una página estática desplegada en un contenedor.</p>
</body>
</html>
```


### Paso 3: Crear el Dockerfile
Este archivo indicará cómo construir la imagen de nuestro contenedor con Nginx y la página estática:
`cat > Dockerfile `

```
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```
💡 Explicación:
`FROM nginx:alpine`: usa la imagen oficial de Nginx en su versión ligera Alpine.
`COPY index.html ...`: copia tu página en la carpeta por defecto de Nginx.

### Paso 4: Construir la imagen
Ejecuta:
`docker build -t miweb:1.0`
Esto creará una imagen llamada miweb:1.0.

### Paso 5: Ejecutar el contenedor
Lanza el contenedor exponiendo el puerto 80:
`docker run -d -p 80:80 --name contenedor-miweb miweb:1.0`
`-d`: modo detach (en segundo plano)
`-p 80:80`: mapea el puerto 80 del contenedor al 80 del nodo
`--name`: da un nombre al contenedor

### Paso 6: Probar en el navegador
En la parte superior de Docker Playground, haz clic en el botón “80” que aparece (en la barra con los puertos abiertos). ➡️ Se abrirá una nueva pestaña mostrando tu página HTML servida por Nginx.

### Paso 7: Verificar y gestionar
Comprueba que el contenedor está en ejecución:
`docker ps`
Detén el contenedor si quieres:
`docker stop contenedor-miweb`
