# Configuración de Docker Compose para el Stack de Servicios

Este archivo `docker-compose.yml` define una serie de servicios que se ejecutan en contenedores Docker. A continuación se describe el propósito y configuración de cada servicio:

## Servicios

### Wazuh
- **Imagen:** wazuh/wazuh
- **Puertos:** El puerto 55000 del host se mapea al puerto 55000 del contenedor.
- **Variables de entorno:** Define credenciales para la API de Wazuh.

### Kibana (Versión SDGD)
- **Imagen:** docker.elastic.co/kibana/kibana:7.10.0
- **Puertos:** El puerto 5601 del host se mapea al puerto 5601 del contenedor.
- **Dependencias:** Depende del servicio `wazuh` para su funcionamiento.

### Kibana (Versión Chat)
- **Imagen:** docker.elastic.co/kibana/kibana:7.10.0
- **Puertos:** El puerto 5602 del host se mapea al puerto 5602 del contenedor.

### Fortinet
- **Imagen:** custom_fortinet
- **Puertos:** Reemplazar "port:port" por el mapeo de puertos adecuado.

### Proxy (Nginx)
- **Imagen:** nginx:alpine
- **Puertos:** El puerto 8080 del host se mapea al puerto 80 del contenedor.
- **Volúmenes:** Mapea el archivo local `nginx.conf` al archivo de configuración de Nginx dentro del contenedor.

### osTicket
- **Imagen:** campbellsoftwaresolutions/osticket
- **Puertos:** El puerto 8080 del host se mapea al puerto 80 del contenedor.
- **Variables de entorno:** Define credenciales y configuración para la base de datos de osTicket.

### osTicket Database
- **Imagen:** mysql:5.7
- **Variables de entorno:** Define credenciales y configuración para la base de datos.
- **Volúmenes:** Se define un volumen persistente para almacenar los datos de la base de datos.

## Volúmenes

Se define un volumen llamado `osticket_db_data` que se utiliza para persistir los datos de la base de datos de osTicket.

---

**Notas:**

1. Asegúrate de configurar correctamente las variables de entorno antes de iniciar los contenedores, especialmente las relacionadas con credenciales y configuraciones de base de datos.
2. Reemplaza los valores de marcadores de posición (como "your_password" o "port:port") con valores reales antes de desplegar los servicios.
