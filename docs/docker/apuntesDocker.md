# DOCKERS

## TEORÍA DOCKER

- **Imagen:**
  - Paquete estático (de solo lectura).
  - Contiene el código de la App, dependencias, librerías y herramientas del sistema necesarias para que funcione.
  - Se construyen mediante una acumulación de **capas**.
  
- **Contenedor:**
  - Se crea al ejecutar una imagen.
  - Es un entorno aislado donde la aplicación vive y funciona.

- **Registro / Repositorio:**
  - Lugar en la nube donde se guardan y comparten las **imágenes** (como Docker Hub).

- **Solución a problemas:**
  - Acaba con el clásico problema de *"en mi máquina sí funciona"*.
  - Evita conflictos de versiones de lenguajes, dependencias o incompatibilidades con el S.O.

## DOCKER DESKTOP

- Es una VM que funciona en Linux y ejecuta containers.
- Accede al sistem de archivos y a la red privada o pública.
- Posee Docker Compose y CLI y otras herramientas.
- Funciona en Windows gracias a WSL2 (Windows System For Linux).

## COMANDOS IMAGENES

- `docker images` → Muestra las imagenes descargadas/creadas.
- `docker pull <image>` → Descagar imagen. Si no ponemos versión, instala la última versión existente.
  - Ejemplo: `docker pull node:18` → Descagar la imagen de Node 18.
- `docker image rm <image>` → Borra una imagen.

- `docker build -t <name_image>:<etiqueta> <ruta_DockerFile>` → Crea una imagen a partir del Dockerfile.

## COMANDOS CONTENEDORES

Para crear un contenedor se necesita una imagen.

- `docker create <image>` → Crea un contenedor a partir de una imagen, dando como resultado un ID.
- `docker create --name <nombre> <image>` → Crea un contenedor con un nombre y a partir de una imagen.
- `docker rm <ID|name>` → Elimina el contenedor.

- `docker start <ID|name>` → Inicia el contenedor creado.
- `docker stop <ID|name>` → Detiene un contenedor.

- `docker ps` → Muestra los contenedores iniciados.
- `docker ps -a` → Muestra todos los contenedores.

- `docker logs <ID|name>` → Muestra los logs del contenedor.
- `docker logs --follow <ID|name>` → Muestra los logs en tiempo real del contenedor.

### PORT MAPPING

- `docker create -p<portPC>:<portContainer> --name <name> <image>` → Mapeamos el puerto del PC real (lado izquierdo)
al puerto interno del contenedor (lado derecho).

## COMANDO `DOCKER RUN`

Este comando agrupa 3 pasos en 1: Encuentra/descarga la imagen, crea el contenedor y lo inicia.

- `docker run <image>`→ Hace los 3 pasos y finaliza mostrando los logs en vivo (bloquea terminal).
- `docker run -d <image>`→ Se ejecuta en segundo plano y te devuelve el control de la terminal.
- `docker run --name <name> -p<portPC>:<portContainer> -d <image>` → En segundo plano, con nombre, con puertos mapeados y a partir de una imagen.

### DOCKER NETWORK

Los contenedores están aislados. Permite la comunicación entre contenedores.

- `docker network ls` → Muestra las redes internas de docker.
- `docker network create <name_red>` → Crea una red interna nueva.
- `docker network rm <name_red>` → Borra una red.
- `docker run -d --name <name> -p <portPC>:<portContainer> --network <name_red> <image>` → Inicia un contenedor conectándolo directamente a la red interna que hemos creado.

## DOCKER COMPOSE

Herramienta que nos permite definir y ejecutar aplicaciones Docker de múltiples contenedores usando un archivo YAML (`docker-compose.yml`).

- `docker compose up` → Lee el archivo, crea las redes/volúmenes y levanta todos los contenedores mostrando los logs en vivo.
- `docker compose up -d` → Igual que el anterior, pero en segundo plano (Detached). Te devuelve el control de la terminal.
- `docker compose down` → Apaga y destruye todos los contenedores y redes creadas por el `up`.

### MULTIPLES ENTORNOS (Dev vs Prod)

- **`docker-compose-dev.yml`:**
  - Configuración para Desarrollo (Development).
  - Optimizado para el programador (puertos abiertos, recarga en caliente, muestra errores).

- **`docker-compose-prod.yml`:**
  - Configuración para Producción (Production).
  - Optimizado para el usuario final (seguridad máxima, rendimiento, puertos internos cerrados).

### ENTORNO DE DESARROLLO

`docker compose -f docker-compose-dev.yml up -d --build` → Se usa para la primera vez o modificaciones en los archivos Docker/yml.
`docker compose -f docker-compose-dev.yml up -d` → Inicia la infraestructura de Docker.
`docker compose -f docker-compose-dev.yml down` → Destruye la infraestructura de Docker.

`docker compose -f <archivo.yml> exec <nombre_del_servicio> <tipo_de_terminal>` → Conectarnos a la terminal del contenedor.

`docker compose -f docker-compose-dev.yml ps` → Para ver que todo a iniciado correctamente.

## VOLÚMENES (PERSISTENCIA DE DATOS)

Los contenedores son **efímeros**. Esto significa que, por defecto, si borras o destruyes un contenedor, **todos los datos que se generaron en su interior se pierden para siempre** (por ejemplo, los registros de una base de datos).

Para solucionar esto usamos **Volúmenes**. Un volumen es básicamente una carpeta segura en nuestro ordenador real que se "conecta" como un túnel a una carpeta dentro del contenedor.
