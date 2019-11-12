# XYMBOT:
Xymbot is an effort to develop a fault detection system based on the detection of outliers. Being an easy way to modularly integrate a powerful anomaly detection engine in IoT architectures. Variable and static parameters can be monitored as well as scaled as customers need it.

## Versiones disponibles.

| Funciones                                  | v1.0  |
| :---                                       | :---: |
| Data integration through Api-REST          | D     |
| Failure Detection Modules                  | D     |  
| Definition of optimal architecture         | D     |

OK: Built-in functionality
X : Functionality removed
D : Functionality in development
I : Intended to develop
































































NAGEL: bW91bnQgLXQgY2lmcyAtbyB1c2VyPWNlY2lsaW8tZGlheixwYXNzd29yZD1TaXNhbWV4LjE4IC8vMTcyLjI4LjE2LjMvbmFnZWwgL3NtaV92b2x1bWVfZGphbmdvL2RhdGFfcGllemFz
```

### Servidor Linux.
Se tiene que instalar en el servidor los siguientes servicios:
1. Docker [https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#os-requirements]
2. Docker-compose [https://docs.docker.com/compose/install/]

### Ejecutar de servicios de docker.


### 1   Construir imagenes.

### 1.0 Configurar credenciales de conexión:
```
# RUTA: smi_hxh\smi_hxh\backend\django\mtc_etedjmodel\.env

# LOCALHOST.
DB_URL       = "postgres://postgres:galileo.1564@10.0.75.1:35432/smx_mt_connect_app"
DB_URL_REDIS = "postgres://postgres:galileo.1564@10.0.75.1:6379/smx_mt_connect_app"


# SERVIDOR SMI-PRODUCCION (SERVIDOR DE DB LABORATORIO).

#DB_URL       = "postgres://cecilio-diaz:Sisamex.17@172.28.13.57:4000/smx_mt_connect_app_v2"
#DB_URL_REDIS = "postgres://cecilio-diaz:Sisamex.17@172.16.100.99:6379/smx_mt_connect_app_v2"

```

### 1.1 Construir bases de datos.
### Ejecutar desde la siguiente ruta: /backend
```
docker-compose -f backend_produccion.yml   up -d postgres
docker-compose -f backend_produccion.yml   up -d redis
```
## 1.2 Construir Backend
```
docker-compose -f backend_produccion.yml   up -d django
docker-compose -f backend_produccion.yml   up -d celery_worker
docker-compose -f backend_produccion.yml   up -d celery_beat
docker-compose -f backend_produccion.yml   up -d flower
```

## 1.3 Integración de frontend mediante GRAFANA [https://grafana.com/grafana/]
```
docker-compose -f build_all_images.yml up -d grafana
```


## Maquetado del backend
### Herramientas utilizadas en el backend.
[![DJANGO](https://www.djangoproject.com/](DJANGO)
[![POSTGRESQL](https://www.postgresql.org/)](POSTGRESQL)
[![REDIS](https://redis.io/)](REDIS-NOSQL)


En esta sección se puede observar como esta estructurado el backend.
### Herramientas de Backend []
Maquetado
![maquetado_backend](documentación/maquetado_backend.png)


## Datos del acceso al servidor de producción.
```
IP:   172.16.100.99
USER: administrator
PASW: U2lzYW1leC4jMjAxOQ==
```
## Accesos directos:

django-admin[http://172.16.100.99:38000/admin/]

### Entrar al contenedor de forma interactiva:
```
docker exec -it celery_worker bash
```
### Revisar volumen:
1. Dentro del docker [cd /data_piezas/data_nagel/]


### Probar Manualemente tarea celery [http://172.16.100.99:8888].
```
docker exec -it celery_worker bash
python manage.py shell
```
# Comandos utiles backend.
## Comprobación de tareas de forma manual:
Lectura de número de piezas.

```
docker exec -it django_rfid bash
python manage.py shell
from apps.piezas.tasks import find_new_pieces
find_new_pieces()
```

Detección de conteo de ciclos:
```
python manage.py shell
from machine_services.tasks import get_data_mtconnect
```

### Imagenes de referencia:
CARBUSENSE_HOME[http://172.16.100.99:8000/media/scripts/WhatsApp_Image_2019-10-22_at_10.33.53_AM.jpeg]
