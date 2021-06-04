Contenedores:
- Entorno aislado para ejecutar uno o más procesos. Tiene:
    - Su propio FileSystem
    - Su propia IP
    - Sus propias variables de entorno
    - Y más:
        - Limitación del acceso a recursos: CPU, Memoria,...

Los contenedores se crean a partir de una imagen de contenedor, que tiene:
    - Un archivo comprimido que dentro lleva: una app ya instalada, sus recursos (configuración) y las librerias (dependencias) que necesite.
    - La información de como debe usarse esa imagen de contenedor, y sus valores por defecto.
    
De donde sacaba las imágenes de contenedor? 
    - Un repositorio de imágenes de contenedor. El más utilizado: Docker Hub

Las imagenes tienen versiones, llamadas: TAGS

Al descargar una imagen de contenedor:
    - Se descomprime e una carpeta del host

Crear un contenedor:
    - Se crea una carpeta que tiene:
        A priori nada, pero después irá teniendo los cambios sobre el FileSystem original de la imagen. 
        Esos cambios a priori son volatiles: Al borrar el contenedor, los piedo.
        Para evitar esa perdida, creamos volumenes, que son ubicaciones persistentes donde guardar determinadas carpetas / archivos
            del FileSystem del contenedor

Al arrancar un contenedor:
    - Se limitan los recursos del contenedor
        - Se asignan las variables de entorno
        - LA RED: Se le asigna una determinada IP, que pertenece a una red virtual PRIVADA que gestiona el ejecutor de contenedores.
    - Se pone un proceso en marcha, definido bajo el nombre COMMAND dentro de los parámetros de la imagen de contenedor.
        - Ese proceso puede abrir un puerto
            En este caso, opcionalmente, exponerlo publicamente.

FileSystem del contenedor:
    Esta contruido en CAPAS:
        La primera de esas capas: La de la imagen
        Sobre esa tenemos:        La del container
        Por encima:               La de los volumenes
----
El proceso quien lo arranca? El ejecutor de contenedores, que se ejecuta en el SO del host.
Mi proceso, el que he abierto dentro del contenedor, se ejecuta en el SO del host, en un entorno limitado/aislado del resto.


----------
App en Casa . App WEB Java, NodeJS
    - Servidor de Aplicaciones WEB: Tomcat, JBoss, Weblogic, WAS <<<< Applicación instalada
    - Servidor BBDD
    - KAFKA : Comuncaciones
    
    Imágenes de contenedor - Parametrización

Producción:
    Nodo 1                          |
        Contenedor Tomcat  70%      |    Cabina de almacenamiento EMC2
    Nodo 2   puff                   |
        Contenedor BBDD             |
    Nodo 3                          |    Azure: Volumenes:
        Contenedor Kafka            |       SSD €€€€
    Nodo 4                          |       Volumen BBDD, KAFKA, Tomcat
        Contenedor Tomcat  70%
    Nodo 5
        Contenedor Tomcat  70%
    Nodo 6      
        LoadBalancer (nginx, HAProxy)
    Nodo 7
        Contenedor BBDD
        
Donde se guardan los datos?

---------------------------------
Imagenes de contenedor
Contenedores
    Volumenes
    Variables de entorno: configurar contenedores /aplicaciones
    Puertos <<< Exponer servicios que ofrece una app que hay en un contenedor
---------------------------------
Docker engine:
    Servidor <<<   dockerd
                      ^    
    Cliente  <<<   docker
---------------------------------
Kubernetes -> Cluster - Va en cada maquina 
    
    Nodo 1 - Linux - ROL: MAESTRO DEL CLUSTER :32500                                        | Red cluster PRIVADA, VIRTUAL
        dockerd                                                                             |
            ^                                                                               |
        kubelet                                                                             |
        Contenedores:                                                                       |
            api-server              Comunicarnos con Kubernetes                             |
            scheduller              Donde instalo un pod                             |
            etcd                    Base de datos Kubernetes                                |
            controllerManager       Toda la gestion posterior runtime                       |
            coreDNS                 DNS interno para los servicios del cluster              |
            kubeproxy               Gestión de la red virtual                               |
                                                                                            |
    Nodo 2 - Linux   :32500                                                                 |
        dockerd                                                                             |
           ^                                                                                |
        kubelet                                                                             |
        Contenedores:                                                                       |
            kubeproxy               Gestión de la red virtual                               |
            mysql: 3306      >>>>> DATOS? (VOLUMEN AZURE ID: 0294739274)                  --|   IP: 172.17.0.2
            nginx:80     INGRESS                                                          --|   IP: 172.17.0.6 -->EXTERNAL VIP
    Nodo 3 - Linux  :32500                                                                  |                       VVVVVV
        dockerd                                                                             |                       33.54.21.98
           ^                                                                                |                       L.B. > Nodos del cluster 
        kubelet                                                                             |
        Contenedores:                                                                       |
            kubeproxy               Gestión de la red virtual                               |
            tomcat :8080                                                                  --|   IP: 172.17.0.3
                La BBDD que vas usar va a usar: 172.17.0.2:3306                             |
            tomcat :8080                                                                  --|   IP: 172.17.0.4
                La BBDD que vas usar va a usar: 172.17.0.2:3306                             |
            tomcatpiratilla                                                               --|   IP: 172.17.0.7

SERVICE ACCOUNTS - Roles - Permisos

NETWORK Policies

CONFIGMAP

SECRET

PROVISIONADOR DE VOLUMENES PERSISTENTES   <<<< Adminitrador del cluster
    VV 
VOLUMEN PERSISTENTE: VOLUMEN AZURE ID:0294739274 <<<< Administrador del cluster
    x
PETICION DE VOLUMEN PERSISTENTE: MySQL, necesito 30Gbs rapiditos redundantes  <<<< Desarrollo

INGRESS: nginX  <<<<< KUBERNETES    ||||||    OPENSHIFT    >>>>  ROUTE

SERVICIO: Tiene su propia dirección IP: 172.17.1.100:3306 > LB IP Contenedor(es):3306. Esta IP, es la que tiene asociado un Nombre DNS
    Me ofrece un nombre con el que poder identificar "un" "pod"
    Balanceador de carga que me regala Kubernetes: Reglas netFilter < programa montado dentro del KERNEL DE Linux

HORIZONTAL_POD_AUTOSCALER:
    Me permite configurar como quiero escalar mis contenedores

Cliente de kubernetes (equivalente al comando docker): kubectl

kubectl instala mysql


OpenStack <<<<   Redhat

------------
POD: 
    Un POD es un conjunto de contenedores, que:
        - 1ª Comparten IP. Entre ellos, como se hablan mediante localhost: COMUNIACIONES SON INTERNAS, no pisan una RED.
        - 2º Tengo asegurado que SIEMPRE se vana a ejecutar en el mismo NODO FISICO
        
PRODUCCION
    Tomcat ---> Log ---> Fluentd     ----->   Kafka   ---->    Sistema centralizado LOGs  (ElasticSearch, Prometheus)
    Tomcat ---> 
    
    Tomcat lo tengo en un Contenedor:
        POD 
          CT:
            Tomcat --- Ficheros de log  >>> VOLUMEN       Rotar entre 2 fichero de log 500Kb   1Mb
          CT                                            >>>>    RAM                                         SIDECAR
            Fluentd --                      VOLUMEN
            
PLANTILLAS DE PODs
   * DEPLOYMENT             < NGINX, TOMCAT 
   * STATEFULSET            < MARIADB
    DAEMONSET
    CRONJOBS