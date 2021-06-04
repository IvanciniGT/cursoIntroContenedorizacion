# Docker

docker TIPO_DE_OBJETO OPERACION OTROS

## Imagenes

### Buscar imagenes

docker search TEXTO

### Descarga de imagenes

docker image pull NOMBRE_IMAGEN             >>>>>           docker pull NOMBRE_IMAGEN

### Listado de imagenes

docker image list                           >>>>>           docker images

### Borra imagen

docker image rm ID_DE_IMAGEN                >>>>>           docker rmi ID_IMAGEN


## Contenedores

### Crear un contenedor

docker container create ARGS NOMBRE_IMAGEN

ARGS:
    - --name NOMBRE
    - -e VARIABLE=VALOR
    - -p IP_HOST:PUERTO_HOST:PUERTO_DESTINO(container)        PUERTO_HOST:PUERTO_CONTENEDOR (se abre en todas las IP del host)
    - -v RUTA_HOST:RUTA_CONTENEDOR

### Operaciones sobre el estado de ejecución de un contenedor

docker container start NOMBRE_CONTENEDOR    >>>>>>            docker start NOMBRE_CONTENEDOR
docker restart NOMBRE_CONTENEDOR
docker stop NOMBRE_CONTENEDOR

### Borra un contenedor

docker container rm NOMBRE_CONTENEDOR      >>>>>>    docker rm NOMBRE

### Listar los contenedores

docker container list --all                 >>>>      docker ps

### Ver los logs de un contenedor

docker container logs NOMBRE_CONTENEDOR

### Ejecutar un proceso dentro del contenedor

docker exec NOMBRE_CONTENEDOR COMANDO
docker exec -it NOMBRE_CONTENEDOR COMANDO     --- Cuando el comando requiere de Interacción por mi parte desde la Terminal

### Docker RUN:

Hace varias cosas:
    - Descargar una imagen de contenedor: docker pull
    - Crear un contenedor: docker container create
    - Arrancar el contenedor: docker start
    - Vincular mi consola de sistema a la salida estandar del contenedor (log). A no ser que ponga -d

### Ver la información completa de configuración del contenedor

docker inspect NOMBRE_CONTENEDOR

# PRUNE  ---> BORRAN COSAS

docker container prune
docker image prune --all
docker system prune