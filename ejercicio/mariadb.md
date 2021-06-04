Tener un contenedor con MariaDB:
- BBDD: prueba
- Usuario: usuario
- Contraseña: password
- Contraseña del usuario root: password

Esa BBDD quiero que sea accesible a mi y a todos mis compañeros, pero yo primero.

Además, quiero que los datos que guarde en esa MariaDB tengan persistencia en una carpeta de mi host:
    /home/ubuntu/environment/datos/mariadb
    
SOLUCION:
docker rm mimariadb 

docker container create \
    --name mimariadb \
    -p 3307:3306 \
    -e MARIADB_ROOT_PASSWORD=password \
    -e MARIADB_USER=usuario \
    -e MARIADB_PASSWORD=password \
    -e MARIADB_DATABASE=prueba \
    -v /home/ubuntu/environment/datos/mariadb:/var/lib/mysql \
    mariadb:latest

docker start mimariadb 

docker rm mimariadb 

docker exec -it mimariadb mysql -u usuario -p