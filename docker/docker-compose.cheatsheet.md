# docker-compose

# Crear y arrancar contenedores
docker-compose -f FICHERO up 

NOTA: Si lo escribo tal cual, además mostrará en la consola el log de los contenedores, dejando la consola bloqueada
      Si le añado -d, no genera los logs por pantalla y libera la consola
      
      

# Arrancar contenedores
docker-compose -f FICHERO start

# Parar contenedores
docker-compose -f FICHERO stop

# Parar y eliminar contenedores
docker-compose -f FICHERO down
