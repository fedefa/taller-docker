# Ejercicio 05

## HEALTHCHECK

HEALTHCHECK es una instrucción de docker que sirve para comunicar si el container está realmente en buen estado. Este comando, junto con un orquestador puede tomar acciones correctivas como reemplazar el contenedor que no está funcionando correctamente.

Un ejemplo sencillo usando CURL podría ser:

`HEALTHCHECK --interval=30s --timeout=5s CMD curl --fail --retries=3 http://localhost/ping || exit 1`

De esta manera el container puede tener 3 estados:

1. Starting: Estado inicial cuando el container está iniciando.
2. Healthy: Si el ping corre exitosamente
3. Unhealthy: Si luego de intentar 3 veces el ping con los parámetros especificados sigue fallando. 
 

## ONBUILD

ONBUILD es una instrucción de docker que nos permite ejecutar una instrucción de manera diferida, cuando se usa como imagen base. Los comandos que se especifican con esta instrucción son ejecutados como primera linea luego del FROM de nuestra nueva imagen.
De esta manera podemos por ejemplo automatizar procesos de building y hacer que las imágenes sean más chicas (menos instrucciones) y eficientes (buenas practicas) para los usuarios de nuestras imágenes. 

Un ejemplo de una aplicación de Node podría ser esta secuencia:

<code>
<br/>FROM node:0.12.6
<br/>RUN mkdir -p /usr/src/app
<br/>WORKDIR /usr/src/app
<br/>
<br/>ONBUILD COPY package.json /usr/src/app/
<br/>ONBUILD RUN npm install
<br/>ONBUILD COPY . /usr/src/app
<br/>CMD [ "npm", "start" ]
<br/>
</code>

Podemos ver que las instrucciones son diferidas, pues no podriamos usar el RUN o COPY directamente porque aún no tenemos acceso a al package.json.

De esta manera estaríamos automatizando el proceso de building y evitando la molestia de que los usuarios de nuestra imagen los escriban por si mismos.

## VOLUME

Las imagenes en docker tienen a ser inmutables, no debería tener que rebuildear la imagen al cambiar de ambiente, una opción para lograr esto es pasar lo que difiere en un volumen.
Por otro lado, los contenedores en docker tienen que ser descartables por lo que toda la información que se tenga que persistir tiene que vivir en otro lado para que al ser eliminados o reemplazados pueda seguir teniendo acceso a ellos.
Dicho esto, basicamente los volúmenes nos servirán para compartir información entre el host y el contenedor.

Un ejemplo útil podemos verlo al explorar el Dockerfile de mysql y ver la siguiene instrucción:

`VOLUME /var/lib/mysql`

A partir de este comando, y luego de correr el contenedor y hacer un `docker inspect` deberíamos ver un volumen con un atributo `source` que corresponde a la ubicación dentro del host (por defecto /var/lib/docker/volumes) y otro `destination` que corresponderá a la ubicación de la información dentro del contenedor.
De esta manera lograremos la independencia de los datos de la DB y el contenedor.

Otros usos comunes para volúmenes de docker son logs y para compartir el codebase en el ambiente de desarrollo. 
