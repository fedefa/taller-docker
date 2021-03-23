# Nginx load balancing

## Build and run

1. Pra iniciar nginx y los app servers: `docker-compose up`
2. Luego, para verificar el correcto round-robin se pueda usar:
 
`curl http://localhost:8080/actuator/health`  


## Observaciones

- La configuración de Nginx propuesta utiliza un fixed round-robin como estrategia de balancing entre las dos instancias de la aplicación.
- Nginx redireccionará equitativamente la carga entre las dos instancias de la aplicación.
- Al usar docker-compose se configura una default-network para la aplicación. Por defecto cada container se une a la default network y es alcanzable por los demás containers usando como hostname el nombre del servicio.
 


