# Nginx load balancing

## Build and run

1. Pra iniciar nginx y los app servers: `docker-compose up`
2. Luego, para verificar el correcto round-robin se pueda usar:
 
`curl http://localhost:8080/actuator/health`  


## Observaciones

- La configuración de Nginx propuesta utiliza un fixed round-robin como estrategia de balancing entre las dos instancias de la aplicación.
- Nginx redireccionará equitativamente la carga entre las dos instancias de la aplicación.


