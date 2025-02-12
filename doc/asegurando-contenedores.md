# Asegurando contenedores en Docker

## Introducción

La seguridad en Docker es fundamental para evitar vulnerabilidades en contenedores y en el sistema anfitrión. Es importante aplicar buenas prácticas en la gestión de imágenes, ejecución de contenedores y configuración de redes.

---

## Uso de imágenes seguras

Para garantizar la seguridad desde la base, es recomendable:

- **Utilizar imágenes oficiales y verificadas** desde [Docker Hub](https://hub.docker.com/).
- **Evitar imágenes sin mantenimiento**, usando etiquetas de versiones específicas en lugar de `latest`.
- **Escanear imágenes en busca de vulnerabilidades** con:
  ```sh
  docker scan nombre_imagen
  ```
- **Minimizar la superficie de ataque** utilizando imágenes ligeras como `alpine` en lugar de distribuciones completas.

---

## Restricción de permisos y privilegios

Para reducir riesgos, los contenedores no deben ejecutarse con privilegios innecesarios:

- **Evitar ejecutar contenedores como root:**
  ```sh
  docker run --user 1000:1000 nombre_imagen
  ```
- **Utilizar la opción `--security-opt` para restringir privilegios:**
  ```sh
  docker run --security-opt no-new-privileges nombre_imagen
  ```
- **Limitar capacidades de Linux con `--cap-drop` y `--cap-add`**:
  ```sh
  docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE nombre_imagen
  ```

---

## Seguridad en redes Docker

Configurar correctamente las redes reduce la exposición de los contenedores:

- **Usar redes personalizadas en lugar de `default`**:
  ```sh
  docker network create mi_red_segura
  ```
- **Restringir acceso con firewalls** y reglas de `iptables`.
- **No exponer puertos innecesarios** en la configuración de los servicios.
- **Utilizar TLS para proteger la comunicación** entre contenedores y servicios externos.

---

## Gestión segura de volúmenes y datos

- **Evitar exponer archivos sensibles desde el host:**
  ```sh
  docker run -v /etc/passwd:/datos ubuntu
  ```
  (Esto podría comprometer credenciales del sistema).
- **Montar volúmenes en modo de solo lectura cuando sea posible:**
  ```sh
  docker run -v /datos:/app:ro nombre_imagen
  ```
- **Cifrar los datos sensibles** dentro del contenedor o en los volúmenes asociados.

---

## Monitorización y auditoría

Para detectar amenazas, es recomendable monitorear los contenedores:

- **Registrar eventos y logs de los contenedores:**
  ```sh
  docker logs nombre_contenedor
  ```
- **Utilizar herramientas de monitoreo** como `Falco` o `Sysdig` para detectar actividades sospechosas.
- **Auditar imágenes y configuraciones** con herramientas como `Docker Bench for Security`:
  ```sh
  git clone https://github.com/docker/docker-bench-security.git
  cd docker-bench-security
  sudo ./docker-bench-security.sh
  ```

---
