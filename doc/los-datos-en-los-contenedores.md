# Los datos en los contenedores Docker

## Introducción

En Docker, los datos almacenados dentro de un contenedor se eliminan cuando este se detiene o se elimina. Para gestionar datos de manera persistente, Docker ofrece diferentes soluciones, como volúmenes y bind mounts.

---

## Tipos de almacenamiento en Docker

Docker proporciona dos métodos principales para gestionar los datos en contenedores:

1. **Volúmenes**: Administrados por Docker y almacenados en `/var/lib/docker/volumes/`.
2. **Bind mounts**: Permiten mapear un directorio del host dentro del contenedor.

---

## Uso de volúmenes

Los volúmenes permiten que los datos persistan independientemente del ciclo de vida de los contenedores.

- **Crear un volumen:**
  ```sh
  docker volume create mi_volumen
  ```

- **Montar un volumen en un contenedor:**
  ```sh
  docker run -v mi_volumen:/datos ubuntu
  ```
  Esto almacena los datos en `/var/lib/docker/volumes/mi_volumen/_data` en el host.

- **Ver volúmenes existentes:**
  ```sh
  docker volume ls
  ```

- **Eliminar un volumen:**
  ```sh
  docker volume rm mi_volumen
  ```

---

## Uso de bind mounts

Los bind mounts permiten mapear una carpeta específica del host dentro del contenedor.

- **Ejecutar un contenedor con un bind mount:**
  ```sh
  docker run -v /ruta/del/host:/datos ubuntu
  ```
  En este caso, los datos en `/ruta/del/host` estarán accesibles dentro del contenedor en `/datos`.

---

## Diferencias entre volúmenes y bind mounts

| Característica | Volúmenes | Bind Mounts |
|--------------|-----------|------------|
| Administrado por Docker | ✅ Sí | ❌ No |
| Almacenamiento en `/var/lib/docker/volumes/` | ✅ Sí | ❌ No |
| Mayor flexibilidad en gestión | ✅ Sí | ❌ No |
| Acceso directo a archivos del host | ❌ No | ✅ Sí |

---

## Conclusión

La gestión de datos en Docker es crucial para mantener información persistente. Dependiendo de la necesidad, se pueden usar volúmenes para almacenamiento gestionado por Docker o bind mounts para acceso directo a archivos en el host.
