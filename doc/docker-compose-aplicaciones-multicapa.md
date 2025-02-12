# Docker Compose: Aplicaciones multicapa

## Introducción

Docker Compose es una herramienta que permite definir y gestionar aplicaciones multicontenedor mediante un archivo de configuración YAML. Esto facilita la orquestación de servicios interdependientes en un entorno controlado.

---

## Instalación de Docker Compose

Docker Compose suele estar incluido en Docker Desktop. En sistemas Linux, se puede instalar con:

```sh
sudo apt install docker-compose
```

Para verificar la instalación:

```sh
docker-compose --version
```

---

## Creación de un archivo `docker-compose.yml`

Un archivo `docker-compose.yml` define los servicios, redes y volúmenes de una aplicación Dockerizada. 

Ejemplo de un `docker-compose.yml` para una aplicación con Nginx y una base de datos MySQL:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    depends_on:
      - db
  
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
      MYSQL_DATABASE: app_db
```

---

## Comandos básicos de Docker Compose

- **Levantar los servicios en segundo plano:**
  ```sh
  docker-compose up -d
  ```

- **Ver los contenedores en ejecución:**
  ```sh
  docker-compose ps
  ```

- **Ver logs de los servicios:**
  ```sh
  docker-compose logs
  ```

- **Detener y eliminar los contenedores:**
  ```sh
  docker-compose down
  ```

---

## Definiendo redes y volúmenes en Docker Compose

### Redes
Se pueden definir redes personalizadas para la comunicación entre servicios:

```yaml
networks:
  mi_red:
    driver: bridge

services:
  web:
    image: nginx
    networks:
      - mi_red
  db:
    image: mysql
    networks:
      - mi_red
```

### Volúmenes
Para persistir datos entre reinicios:

```yaml
volumes:
  db_data:

services:
  db:
    image: mysql
    volumes:
      - db_data:/var/lib/mysql
```

---
