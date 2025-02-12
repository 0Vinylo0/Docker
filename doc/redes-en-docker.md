# Redes en Docker

## Introducción

Docker permite la comunicación entre contenedores y el acceso a redes externas mediante diferentes tipos de redes. Gestionar adecuadamente las redes en Docker es crucial para la seguridad y el rendimiento de las aplicaciones.

---

## Tipos de redes en Docker

Docker proporciona varios tipos de redes para diferentes escenarios:

### 1. **Bridge (puente)**
- Es la configuración predeterminada.
- Los contenedores en la misma red bridge pueden comunicarse entre sí.
- Se asigna una dirección IP interna a cada contenedor.
- Ejemplo de creación y uso:
  ```sh
  docker network create mi_red_bridge
  docker run --network=mi_red_bridge -d nginx
  ```

### 2. **Host**
- El contenedor comparte la pila de red del host.
- No se asigna una IP separada al contenedor.
- Ejemplo de uso:
  ```sh
  docker run --network host -d nginx
  ```

### 3. **Overlay**
- Se usa en entornos Docker Swarm para conectar contenedores en diferentes nodos.
- Necesita un clúster Docker Swarm activo.
- Ejemplo de creación:
  ```sh
  docker network create -d overlay mi_red_overlay
  ```

### 4. **Macvlan**
- Permite asignar direcciones IP únicas de la red física a los contenedores.
- Se utiliza para integrar contenedores con redes físicas externas.
- Ejemplo de creación:
  ```sh
  docker network create -d macvlan \
    --subnet=192.168.1.0/24 \
    --gateway=192.168.1.1 \
    -o parent=eth0 mi_red_macvlan
  ```

### 5. **None**
- El contenedor no tiene acceso a ninguna red.
- Útil para entornos aislados.
- Ejemplo de uso:
  ```sh
  docker run --network none -d ubuntu
  ```

---

## Listado y gestión de redes

- **Listar redes disponibles:**
  ```sh
  docker network ls
  ```

- **Inspeccionar una red:**
  ```sh
  docker network inspect nombre_red
  ```

- **Eliminar una red:**
  ```sh
  docker network rm nombre_red
  ```

- **Eliminar todas las redes no utilizadas:**
  ```sh
  docker network prune
  ```

---

## Conclusión

Las redes en Docker permiten la comunicación entre contenedores y la integración con redes externas. Elegir el tipo de red adecuado para cada caso mejora el rendimiento y la seguridad de los despliegues en Docker.
