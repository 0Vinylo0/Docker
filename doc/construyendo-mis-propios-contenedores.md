# Construyendo mis propios contenedores en Docker

## Introducción

Docker permite crear imágenes personalizadas a partir de un contenedor en ejecución o mediante un `Dockerfile`. Esto facilita la creación de entornos específicos para aplicaciones con todas sus dependencias.

---

## Creación de una imagen desde un contenedor en ejecución

Se puede crear una nueva imagen a partir de un contenedor en ejecución utilizando `docker commit`.

- **Ejemplo:**
  ```sh
  docker run -it ubuntu /bin/bash
  # Instalar software dentro del contenedor
  apt update && apt install -y nginx
  exit
  ```

- **Guardar el estado del contenedor en una imagen:**
  ```sh
  docker commit id_contenedor mi_imagen_nginx
  ```

- **Verificar la nueva imagen:**
  ```sh
  docker images
  ```

---

## Creación de una imagen con un Dockerfile

Un `Dockerfile` permite automatizar la construcción de imágenes, facilitando su reproducción y mantenimiento.

- **Ejemplo de `Dockerfile` para una imagen con Nginx:**
  ```Dockerfile
  # Usar la imagen base de Ubuntu
  FROM ubuntu:latest

  # Instalar Nginx
  RUN apt update && apt install -y nginx

  # Exponer el puerto 80
  EXPOSE 80

  # Comando por defecto al iniciar el contenedor
  CMD ["nginx", "-g", "daemon off;"]
  ```

- **Construcción de la imagen:**
  ```sh
  docker build -t mi_nginx .
  ```

- **Ejecutar un contenedor basado en la nueva imagen:**
  ```sh
  docker run -d -p 8080:80 mi_nginx
  ```

---

## Optimizaciones en la construcción de imágenes

Para crear imágenes más eficientes y seguras, se recomienda:

1. **Usar imágenes base livianas:**
   ```Dockerfile
   FROM alpine:latest
   ```
2. **Minimizar el número de capas:**
   ```Dockerfile
   RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/lists/*
   ```
3. **Especificar versiones de dependencias para mayor estabilidad.**
4. **Utilizar archivos `.dockerignore` para excluir archivos innecesarios en la imagen.**

---
