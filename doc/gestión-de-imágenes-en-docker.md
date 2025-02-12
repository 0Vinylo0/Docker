# Gestión de imágenes en Docker

## Introducción

Las imágenes en Docker son la base de los contenedores y contienen todo lo necesario para ejecutar una aplicación, incluyendo el código, bibliotecas y dependencias. Docker permite descargar, listar, eliminar y crear imágenes personalizadas.

---

## Descarga de imágenes

Las imágenes pueden descargarse desde Docker Hub u otros registros de imágenes utilizando el comando `docker pull`.

- **Descargar una imagen:**
  ```sh
  docker pull nombre_imagen
  ```
  Esto descarga la última versión de la imagen especificada.

- **Descargar una versión específica:**
  ```sh
  docker pull nombre_imagen:etiqueta
  ```
  Las etiquetas (`tag`) permiten seleccionar versiones específicas de una imagen.

---

## Listado y detalles de imágenes

- **Ver todas las imágenes disponibles en el sistema:**
  ```sh
  docker images
  ```

- **Obtener detalles de una imagen específica:**
  ```sh
  docker inspect nombre_imagen
  ```

---

## Eliminación de imágenes

Para liberar espacio, es posible eliminar imágenes que ya no se utilizan.

- **Eliminar una imagen específica:**
  ```sh
  docker rmi nombre_imagen
  ```

- **Eliminar todas las imágenes no utilizadas:**
  ```sh
  docker image prune
  ```

---

## Creación de imágenes personalizadas

Docker permite construir imágenes personalizadas utilizando un `Dockerfile`, que define los pasos necesarios para crear una imagen.

Ejemplo de `Dockerfile`:
```Dockerfile
FROM ubuntu:latest
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

- **Construir una imagen a partir de un `Dockerfile`:**
  ```sh
  docker build -t mi_imagen .
  ```

---

## Etiquetado y almacenamiento de imágenes

Las imágenes pueden etiquetarse para facilitar su identificación y almacenamiento en un registro.

- **Etiquetar una imagen:**
  ```sh
  docker tag mi_imagen usuario/mi_imagen:v1
  ```

- **Subir una imagen a Docker Hub:**
  ```sh
  docker push usuario/mi_imagen:v1
  ```

---
