# Ejercicio 7: correr PasswordAPI en Kubernetes

## Build and run

1. Crear un namespace: `kubectl create namespace ej07`
2. Apply deployment: `kubectl apply -f deployment.yaml -n ej07`
3. Apply service: `kubectl apply -f service.yaml -n ej07`
4. Luego debo obtener dos cosas:
    - Cluster IP: `minikube ip`
    - NodePort asignado:  `kubectl describe services password-api -n ej07`
5. Por último puedo verificar el correcto ruteo y balanceo a través de mis nodos con:
    `curl <IP>:<NODE_PORT>/health`


## Observaciones

- A través del servicio expongo el deployment hacia el exterior. Define un mapeo entre puertos que especifica que puertos se exponen (port) y hacia que puerto en los pods se forwardea (targetPort).
- Al usar el tipo de servicio NodePort la capa de control de kubernetes expone el servicio en un puerto estático dentro de cada nodo, este podemos verlo al momento de aplicar el servicio (NodePort).
- El servicio matchea todos los pods que se especifiquen en el selector, podrían ser distintas apps con el mismo label.

