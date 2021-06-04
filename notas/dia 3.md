CLUSTER: Supermercado
Productos: Datos
--------------------------------------------------
SERVICIO: Fruteria
SERVICIO: Carnicería
    DEPLOYMENT carnicer@s: Cada carnicero, los volumenes que usa, no están ligados a él
    BALANCEO DE CARGA: Tomar número, estoy en una cola, esperando.
    NODO: Puesto de trabajo 1 
        VOLUMENES:
            EFIMEROS: TABLA: Corto y preparo la carne
            PERSISTENTES: VITRINA/NEVERA: Guardan la carne fresquita hasta que la compro
        POD: 
            CONTENEDOR: Carnicero 1
            SERVICE ACCOUNTS: Tarjeta de Identificación / Acceso
    NODO: Puesto de trabajo 2
        POD: 
            CONTENEDOR: Carnicero 2
    NODO: Puesto de trabajo 3
SERVICIO: Pescadería
SERVICIO: Lacteos
SERVICIO: Cajas - BALANCEO DE CARGA:  Cola
    STATEFULSET: Cada cajero tien ligado los volumenes que está utilizando.
    NODO: Caja 1
        POD: 
            VOLUMEN: BANDEJA (dinero)
            CONTENEDOR: Cajero 1
    NODO: Caja 2
        POD: 
            CONTENEDOR: Cajera 2
    NODO: Caja 3
            CONTENEDOR: Cajero 3     <<<<<< Principal
            CONTENEDOR: Guia, profesor <<<< SIDECAR
    NODO: Caja 4
NETWORK Policies: Seguridad
SERVICIO INTERNO: Reponedores
    POD: 
            CONTENEDOR: Reponedor 1 - Alimentacion
    POD: 
            CONTENEDOR: Reponedora 2 - Electrodomesticos
            CONTENEDOR: Reponedora 3 - Electrodomesticos
            CONFIGMAP: Instrucciones donde deben estar trabajando

SERVICIO INTERNO: Limpieza
    POD: 
            CONTENEDOR: Limpieza 1
            CONFIGMAP: Instrucciones donde deben estar trabajando
    POD: 
            CONTENEDOR: Limpieza 2
            CONFIGMAP: Instrucciones donde deben estar trabajando
    Limpieza 3
        CONFIGMAP: Instrucciones donde deben estar trabajando
KUBERNETES: Manager organizando
INGRESS: Puerta para los clientes 1
INGRESS: Puerta para los clientes 2
INGRESS: Puerta para las mercancias
DNS: Carteles con las ubicaciones de:
    - La carniceria
    - La pescaderia

PLANTILLA DE POD: 
    Caractectisticas, aptitudes que tiene un trabajador
        IMAGEN DE CONTENEDOR
        
HELM
    Chart <<< Plantilla