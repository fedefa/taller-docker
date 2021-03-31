# Ejercicio 08

## Build and run
1. Crear un namespace: `kubectl create namespace ej08`
2. Apply deployment: `kubectl apply -f deployment.yaml -n ej08`
3. Apply secret: `kubectl apply -f ./secret.yaml -n ej08`
4. Apply service: `kubectl apply -f service.yaml -n ej08`
5. Luego debo obtener dos cosas:
    - Cluster IP: `minikube ip`
    - NodePort asignado:  `kubectl describe services telegram-bot -n ej08`
6. Por último puedo verificar el correcto ruteo y balanceo a través de mis nodos con:
   `curl <IP>:<NODE_PORT>/health`

## Observaciones
- En lugar de usar un config map, usar secrets ofusca la información por lo que es preferible al almacenar datos sensibles en las variables de ambiente. (Sin embargo la doc dice que solo encodea en base64. ¿Sirve esto de algo?)
