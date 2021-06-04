UNIX
    Que era UNIX? Un SO. AT&T. Laboratior Bell. MULTICS. 300 versiones
    2 estandar: POSIX, SUS. Austin Group
    Unix a dia de hoy es un estandar que dicta cómo debe realizarse un SO

    SO UNIX: 
        HP-UX UNIX®
        IBM AIX UNIX®
        ORACLE Solaris UNIX®
        APPLE MacOS UNIX®

    SO Tipo UNIX:
        386BSD 
            FreeBSD
        GNU
        Linus Torwalds -> LinuX + GNU -> GNU/Linux
                                            Redhat Enterprise Linux 
                                                Fedora
                                                CentOS
                                            Debian
                                                Ubuntu
                                            Suse
                        -> LinuX + GOOGLE = ANDROID 

Entorno de Producción:
- Alta Disponibilidad 100%
- Escalabilidad - Adaptarse a las necesidades de cada momento (crecer, decrecer)

Cluster - Grupo
    Activo-Activo ---- 17 servidores
    Activo-Pasivo
TODA LA GESTION DE LOS CLUSTER QUIERO - Automatizar
Corriente/Filosofía que me anima, empuja, mueva, a automatizar TODOS LOS TRABAJOS
    en el mundo IT dentro de una organización: DEVOPS

Desarrollador de Software -> Programador
Administrador de Sistemas -> Hacer programas que Administran sistemas
    Ansible, Puppet, Cheff, Kubernets, Openshift
Tester                    -> Hacer programas que prueban de sistemas
    Selenium, Appium, SoapUI, Posman, JMeter, SonarQube, TestMaster

- Seguridad           100%
>>>>>> Alquiler       <<<<<      Cloud

A que llamamos un "Cloud"
    - Máquina virtual en la nube    X
    - Lo que necesite

Cloud < Conjunto de servicios IT que ofrece una empresa a través de Internet
- Cloud de AWS
- Cloud de Microsoft - AZURE
- Cloud de Google GCL

PROCESO: Dentro de un SO
Una aplicación en ejecución dentro de un SO

C:\
   Windows
   Archivos de Programa\
                        Office\
                                word.exe
                        Chrome
   Usuarios
    usuario1\
        Documentos
        Imagenes
        Descargas
        Escritorio

chroot
/
/home
/usuario
/bin
/tmp
/etc
/opt/httpd/httpd   >>>> Proceso.
                        chroot.. cuando este proceso pida el / del FileSystem
/var/httpd/carpeta1
          /carpeta2


Desarrollo de software:
    Metodologías: En Cascada: Waterfall
        En el mundo IT no las podemos aplicar: UTOPIA
            Requisitos > Dia 1 > Listado de requisitos perfecto e invariante
                Analizar > 
                    Desarrollo >
                        Pruebas >
                            Documetacion >
                                Implantación

manifiesto agil:
    agilemanifesto.org

Entrega Continua: Continuos Delivery           CI/CD  << DEVOPS

Integración continua / Entrega/Despliegue Continuo

> Jenkins: Servidor de CI/CD

SCRUM: Sprints 15-60 dias ~30 dias -> instalación en producción 100% funcional desde la semana 3 del proyecto.
                                                                  5% funcionalidad
                                                                  8% funcionalidad

1 año - 1 instalación                      
1 año - 15-20 instalaciones en produccion
        15-20 instalaciones en pre-produccion / integracion / testing

Como cada 15-30 dias coy a instalar en producción <<< PRUEBAS

    AUTOMATIZAR <<< DEVOPS

Los contenedores son una forma de ayudar a la automatización de instalaciones
    y de su operación/monitorización/mantemnimiento

Diseño/Arquitectura de una APP:
    - Sistemas Monolíticos: Toda la funcionalidad está unida totalmente... es un bloque
        Y de distribuye como tal.
    - Servicios y MicroServicios
Ya no tengo un megaproyecto de 1 año..
    Tengo 30-50-100 miniproyectos que coy a ir actualizando perodicamente.
    500 instalaciones en producción  ... QUE HAS TOMADO ???? 

GESTION DE APIs - apigee
    Servicio 1
    Servicio 2
    Servicio 3
    ...
    Servicio 50 v1 v2



Redhat
    - RHEL - Linux    <     DE PAGO   pero es Opensource. Subscripción - SOPORTE
        ^^^^^^ upstream
        Fedora            GRATUITA  y también Opensource. Más moderna y con más funcionalidad.
                No se si tendrá bugs
        CentOS > Gratuitamente <<<<<<<      LEGAL= SI TOTALMENTE 
            Quien los financia principalmente? Redhat
    - OpenShift Container Plantform   <     DE PAGO
        Openshift Origin   GRATIS <<<< PRODUCCION ???
    - Ansible
    - Satellite
    
    
apt instalar nginx 

apt instalar:
   mysql Configuracion Usuario BD scripts
    Replicacion
        Maestro
        Esclavo
   tomcat <<<<^^^Driver JDBC   x4 replicas Load Balancer
    Version APP 
    Servidor MAIL <<<<<
   redis cache acceso BBD
   
   
   
Docker engine

apt install docker -> DEBIAN/UBUNTU
yum install docker
Windows MAC: Descargar el instalador docker desktop




# Qué es IMAGEN DE CONTENEDOR?    <<<<<< GENERA UN DESARROLLADOR (AUTOMATIZAR) <<<<<< DESARROLLADOR: ESCRIBE CODIGO DE UN PROGRAMA/SISTEMA
- Por un lado, un fichero ZIP que contiene una APLICACION YA desplegada, junto con LIBRERIAS adicionales que necesite
- Información de cómo está configurada mi aplicación.

# IMAGENES de contenedor
docker search DESCRIPCION
docker pull NAME:tag (version de una imagen de contenedor) Si no especifico ":tag"   Docker busca el tag ":latest"
docker image list               >       docker images
docker image rm ID              >       docker rmi ID

# CONTENEDORES
docker container create <OTROS_PARAMETROS> NOMBRE_IMAGEN
    OTROS_PARAMETROS:
        --name NOMBRE-DE-CONTENEDOR
        -p 172.31.3.83:974:80           -p 974:80     (en este caso, todas las peticiones que se hagan a cualquier IP del host) EXPONER LOS SERVICIOS
        -v
        -e NOMBRE=VALOR
docker container list --all         docker ps --all
docker container start NAME         docker start NAME
docker container stop NAME          docker stop NAME
docker container restart NAME       docker restart NAME
docker container rm NAME            docker rm NAME
docker container logs NAME          docker logs NAME


# Contenedor es?
    Entorno Aislado donde ejecutar procesos dentro de un SO Linux.
    Aislado?
        - Tiene su propio Sistema de archivo independiente
        - Tiene su propia Configuración de RED - IP - El contenedor se pincha en la red privada de DOCKER
        - Tiene sus propias VARIABLES DE ENTORNO

# Dentro del contenedor voy a ejecutar, que concepto? 1 PROCESO PRINCIPAL (que podrá abrir procesos hijos)
    Si esos procesos quieren que otros programas se puedan comunicar con ellos, deben abrir un puerto en la red suya (en la que están - DOCKER)


-------------------------------------------------------------------- Red de amazon
  |                                     |                    |
  | [ethernet] 172.31.3.83          CLIENTE 1 (su IP)      CLIENTE 2 (su IP)                                                IP Publica del host
  |                                                                                                                             V
HOST ( UBUNTU )                                                                             REGLA DE ENRUTAMIENTO NAT:          V
  |                                                                                             Cuando alguien llame a la IP: 172.31.3.83  :  974
  | [Docker]  172.17.0.1                                                                        Quiero redirigir esa petición a:
  |                                                                                                     IP: 172.17.0.2:80
 ---------------------------------------------- Red de docker
    |                                   |
    | [Docker] 172.17.0.2               |   [Docker] 172.17.0.3
    |                                   |
    CONTENEDOR 1                    CONTENEDOR 2
     nginx :80                          mariaDB: 3306

Ordenador/Computadora:
    - Interfaces de RED (SO) - Un canal de I/O a una red
        VVVV
        - Cable -  Tarjeta de RED de cable RJ45 - Interfaz 1
        - WIFI                                  - Interfaz 2
        - Loopback - localhost - Red Virtual    - Interfaz 3
            Comunicaciones internas

Ordenador de Amazon:
    - Loopback:         127.0.0.1 - localhost
    - Ethernet - ens5   172.31.3.83
    - Docker            172.17.0.1    <<<<< Red privada virtual que Docker monta dentro de mi ordenador
    

Un contenedor?
    Entorno aislado donde se ejecuta un proceso:
        ---> El contenedor tiene su propio SISTEMA DE ARCHIVOS
El FileSystem del Contenedor se guarda en el mismo disco duro del host.

HOST
/
/bin
/home
/etc
/opt
/datos                                                                           /var
/var
    /lib
        /docker
            /image                                                          CONTENEDOR some-mongo
                mongo DESCOMPRIMIDO
                /mongo                  << chroot <<<<<                          /
                    /bin                                                         /bin/prueba.txt
                    /home                                                        /home
                    /etc
                    /opt
            /container
                /some-mongo
                    /bin/prueba.txt
                /897240398r789n298374hf89347h59082347n5d984735f9823
                    /bin/prueba2.txt   
----------------------------------------------------------------------------------------------------------------------------------------
                                                                    O_O
                                                VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
Los datos que quiero persistentes en un contenedor los monto en volumenes                                                
VOLUMEN                                                       var/data ---> HOST (/datos) ---> ELASTIC BLOCK STORAGE AWS, AZURE , GCL, ISCSI, FibreChannel
VOLUMEN                                                       var/logs ---> HOST (/tmp) ---> ELASTIC BLOCK STORAGE AWS, AZURE , GCL, ISCSI, FibreChannel
>CONTENEDOR some-mongo      bin/prueba.txt                                   tmp
IMAGEN MONGO                bin             home              var            tmp             etc              <<<< INALTERABLE... NO SE TOCA NADA

Que pasa si arranco un contenedor, el proceso de dentro del contenedor hace cambios en el FS y despues paro el contenedor
    - Donde se quedan esos cambios
Arranco de nuevo el contenedor
    - Sigo teniendo los datos? SI, claro

Que pasa si borro el contenedor
    Pierdo sus datos.             <<<<<<<<   Lo vamos a estar haciendo de continuo. 

Docker me permite gestionar contenedores en mi maquina    
Kubernetes me permite gestionar contenedores en un cluster de maquinas.
    Nodo 17 - C App
    Nodo 19 - C App
    Nodo 29 - C App    <<<<<<< NFS:/vol27
    
MySQL 11.1
MySQL 11.1.1






docker-compose    PARAMETRIZACION ----> .yaml

docker swarm <<<<