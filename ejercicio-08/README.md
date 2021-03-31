# Ejercicio 08

## Build and run
1. Crear un namespace: `kubectl create namespace ej08`
2. Apply deployment: `kubectl apply -f deployment.yaml -n ej08`
3. Apply secret: `kubectl apply -f secret.yaml -n ej08`
4. Message bot with /version to obtain a response

## Observaciones
- En lugar de usar un config map, usar secrets ofusca la información por lo que es preferible al almacenar datos sensibles en las variables de ambiente. (Sin embargo la doc dice que solo encodea en base64. ¿Sirve esto de algo?)
- No necesitamos un servicio para acceder al container pues el bot solo necesita poder salir a internet.
