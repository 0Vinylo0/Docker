# Ejecutando y gestionando contenedores en Docker

## Ejecutando contenedores

Para ejecutar un contenedor en Docker, utilizamos el comando `docker run`. Este comando permite crear y ejecutar un contenedor basado en una imagen específica.

### Comandos básicos

- **Ejecutar un contenedor:**
  ```sh
  docker run nombre_imagen
  ```
  Esto descarga la imagen si no está disponible localmente y la ejecuta.

- **Ejecutar un contenedor en segundo plano:**
  ```sh
  docker run -d nombre_imagen
  ```
  La opción `-d` (detached) permite ejecutar el contenedor en segundo plano.

- **Ejecutar un contenedor con una terminal interactiva:**
  ```sh
  docker run -it nombre_imagen /bin/bash
  ```
  La opción `-it` permite interactuar con el contenedor.

- **Asignar un nombre al contenedor:**
  ```sh
  docker run --name mi_contenedor nombre_imagen
  ```

- **Mapear puertos entre el contenedor y el host:**
  ```sh
  docker run -p 8080:80 nombre_imagen
  ```
  Esto asigna el puerto 80 del contenedor al puerto 8080 del host.

---

## Gestionando contenedores

### Listar contenedores

- **Ver contenedores en ejecución:**
  ```sh
  docker ps
  ```

- **Ver todos los contenedores (incluidos los detenidos):**
  ```sh
  docker ps -a
  ```

### Detener y eliminar contenedores

- **Detener un contenedor en ejecución:**
  ```sh
  docker stop id_contenedor
  ```

- **Reiniciar un contenedor:**
  ```sh
  docker restart id_contenedor
  ```

- **Eliminar un contenedor detenido:**
  ```sh
  docker rm id_contenedor
  ```

- **Eliminar todos los contenedores detenidos:**
  ```sh
  docker container prune
  ```

### Ver logs de un contenedor

- **Mostrar logs de un contenedor:**
  ```sh
  docker logs id_contenedor
  ```

### Acceder a un contenedor en ejecución

- **Abrir una terminal dentro de un contenedor en ejecución:**
  ```sh
  docker exec -it id_contenedor /bin/bash
  ```

- **Ejecutar un comando dentro de un contenedor:**
  ```sh
  docker exec id_contenedor comando
  ```

---

## Conclusión

Docker facilita la ejecución y gestión de contenedores a través de comandos simples. Aprender a usarlos eficientemente permite optimizar el desarrollo y la administración de aplicaciones en entornos aislados y portátiles.
