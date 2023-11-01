# RoundRobinyLogsService-DockeryAWS

## Descripción

Este proyecto consta de un acercamiento basico de la creación de un servicio web que retorna un mensaje ```Hello Docker!``` el cual se va a distribuir en distintos contenedores e imagenes de docker y posteriormente poder desplegar la imagen docker en un servicio ec2 de aws

En el laboratorio se indico crear los contenedores ```firstdockercontainer```, ```firstdockercontainer2``` y ```firstdockercontainer3``` manualmente, pero para facilidad de la prueba se agrego al archivo ```docker-compose.yml``` la configuración necesaria para crear todos los contenedores solo ejecutando el comando ```docker compose up -d```

## Prerrequisitos

Para  elaborar este proyecto requerimos las siguientes tecnologias:
* [Maven](https://es.wikipedia.org/wiki/Maven): Herramienta la cual permite realizar la construción de proyectos, realizarles pruebas y otras funciones.
* [Git](https://es.wikipedia.org/wiki/Git): Software de control de versionamiento centralizado.
* [Docker](https://es.wikipedia.org/wiki/Docker_(software)): Es un proyecto de código abierto que automatiza el despliegue de aplicaciones dentro de contenedores de software, proporcionando una capa adicional de abstracción y automatización de virtualización de aplicaciones en múltiples sistemas operativos
 
También necesitamos tener instalado y habilitado el protocolo SSH en nuestro computador 
* [SSH](https://es.wikipedia.org/wiki/Secure_Shell): Es el nombre de un protocolo y del programa que lo implementa cuya principal función es el acceso remoto a un servidor por medio de un canal seguro en el que toda la información está cifrada

Para asegurar que el usuario cumple con todos los prerrequisitos para poder ejecutar el programa, es necesario disponer de un Shell o Símbolo del Sistema para ejecutar los siguientes comandos para comprobar que todos los programas están instalados correctamente, para así compilar y ejecutar tanto las pruebas como el programa correctamente.

```
docker --version
mvn --version
git --version
java --version
```

## Instalación

Para realizar la instalcaión de nuestro programa debemos ir a la linea de comandos de nuestro sistema operativo y hacer uso del siguiente comando
```
git clone https://github.com/RichardUG/RoundRobinyLogsService-DockeryAWS.git
```

## Ejecución

Para realizar la ejecución del programa debemos seguir los siguientes pasos:

```
cd RoundRobin
```

```
mvn clean install
```

```
mvn package
```

```
cd ..
```

```
cd LogService
```

```
mvn clean install
```

```
mvn package
```

```
cd ..
```

```
mvn clean install
```

```
mvn package
```

## Compilación y pruebas

Para compilar y verificar que nuestro proyecto se encuentre bien construido debemos seguir los siguientes pasos:

```
cd RoundRobin
```

```
mvn compile
```

```
mvn test
```

```
cd ..
```

```
cd LogService
```

```
mvn compile
```

```
mvn test
```

```
cd ..
```

```
mvn compile
```

```
mvn test
```

## Despliegue en locahost

Lo primero que debemos hacer tras construir nuestro proyecto mvn en nuestro computador es desplegar nuestras imagenes y contenedores, para lo cual en nuestra linea de comandos nos ubicaremos en la carpeta raiz de nuestro proyecto y haremos uso del siguiente comando:

```
docker-compose up -d
```

El cual al finalizar de hacer la construcción de las imagenes y los contenedores nos mostrara en consola el siguiente resultado

![](/img/build.PNG)

En consola podemos revisar que nuestras imagenes se hayan creado con el siguiente comando 

```
docker images
```

Que nos mostrara el siguiente resultado

![](/img/imagesConsole.PNG)

En consola también podemos revisar que nuestros contenedores se hayan creado con el siguiente comando 

```
docker ps
```

Que nos mostrara el siguiente resultado

![](/img/containersConsole.PNG)


Y si tenemos vista grafica de nuestro docker, en mi caso ```portainer``` también podemos ir a revisar si se encuentran creadas nuestras imagenes, que en este caso son las que se encuentran seleccionadas:

![](/img/image.PNG)

y también podemos revisar que nuestros contenedores esten creados, que son los que se encuentran seleccionados

![](/img/containers.PNG)

## Prueba en localHost

Para acceder a nuestro proyecto desplegado en localhost, consultamos la siguiente URL

[http://localhost:35000](http://localhost:35000)

Que nos mostrara esta pagina

![](/img/localnomensaje.PNG)

Ahora podemos hacer la prueba ingresando dos mensajes

> ### Prueba1
> 
> Primer mensaje
> 
> ![](/img/prueba1localsinresultado.PNG)
> 
> Resultado primer mensaje
> 
> ![](/img/prueba1localconresultado.PNG)
> 
> ### Prueba2
> 
> Segundo mensaje
> 
> ![](/img/prueba2localsinresultado.PNG)
> 
> Resultado segundo mensaje
> 
> ![](/img/prueba2localconresultado.PNG)


## Despliegue en AWS

Ahora iniciaremos el proceso para desplegar nuestro proyecto en ```AWS```, par inciar con esto lo primero que debemos hacer es crear un repositorio en ```Docker hub```, para subir nuestro proyecto en él, en mi caso este sera mi repositorio

* Nombre usuario: richardug
* Nombe repositorio: roundrobinylogservices-dockeryaws
* Link: [https://hub.docker.com/repository/docker/richardug/roundrobinylogservices-dockeryaw](https://hub.docker.com/repository/docker/richardug/roundrobinylogservices-dockeryaws)

Ahora crearemos nuevos tag para cada una de nuestras imagenes con el nombre de la nueva imagen como "Nombre usuario Docker"/"Nombre repositorio" es decir richardug/roundrobinylogservices-dockeryaws y con tag el nombre de cada recurso, que sera los siguientes comandos:

```
docker tag roundrobinylogservice-awsydocker_roundrobin:latest richardug/roundrobinylogservices-dockeryaws:roundrobin
```

```
docker tag roundrobinylogservice-awsydocker_logservice1:latest richardug/roundrobinylogservices-dockeryaws:logservice1
```

```
docker tag roundrobinylogservice-awsydocker_logservice2:latest richardug/roundrobinylogservices-dockeryaws:logservice2
```

```
docker tag roundrobinylogservice-awsydocker_logservice3:latest richardug/roundrobinylogservices-dockeryaws:logservice3
```

```
docker tag mongo:latest richardug/roundrobinylogservices-dockeryaws:mongo
```

Lo cual en consola lo veriamos así

![](/img/newtags.PNG)

Y tras ejecutar los  comandos podemos verificar que se hayan creado las imagenes con el siguiente comando

```
docker images
```

Y nos mostrara el siguiente resultado

![](/img/newtagsImages.PNG)

Ahora empujaremos las imagenes a nuestro repositorio de ```Docker hub```


```
docker push richardug/roundrobinylogservices-dockeryaws:roundrobin
```

```
docker push richardug/roundrobinylogservices-dockeryaws:logservice1
```

```
docker push richardug/roundrobinylogservices-dockeryaws:logservice2
```

```
docker push richardug/roundrobinylogservices-dockeryaws:logservice3
```

```
docker push richardug/roundrobinylogservices-dockeryaws:mongo
```

Podemos visualizar que las imagenes se hayan subido dirigiendonos a nuestro repositorio en ```Docker hub``` y nos debe mostrar algo así

![](/img/imagesDockerhub.PNG)


