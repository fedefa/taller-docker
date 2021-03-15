# Ejercicio 4

DockerHub link:
 
`docker pull fedefarina/password-api:1.0`

## Build and run

1. `docker build -t fedefarina/password-api:1.0`
2. `docker run -p 8080:8080 -d fedefarina/password-api:1.0`
3. `curl -i http://localhost:8080/swagger-ui.html` to test it.

## Observaciones

1. Como no hay necesidad de compilar usamos directamente una imagen base que tenga solo la JRE.

