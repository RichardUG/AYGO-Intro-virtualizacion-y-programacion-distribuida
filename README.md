# TALLER DE INTRODUCCIÓN A VIRTUALIZACIÓN Y PROG. DISTRIBUIDA

## Descripción

Este proyecto consta de un acercamiento básico de la creación de un servicio web que retorna un mensaje ```Hello Docker!``` el cual se va a distribuir en distintos contenedores e imagenes de docker y posteriormente poder desplegar la imagen docker en un servicio ec2 de aws

## Arquitectura

El proyecto es un servicio web, contenerizado en una instancia docker, que se despliega en un servicio EC2 del cloud aws 

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
git clone https://github.com/RichardUG/AYGO-Intro-virtualizacion-y-programacion-distribuida.git
```

## Ejecución

Para realizar la ejecución del programa debemos seguir los siguientes pasos:

```
cd AYGO-Intro-virtualizacion-y-programacion-distribuida
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
mvn compile
```

```
mvn test
```

## Despliegue a través del repositorio descargado

Este despliegue lo podemos hacer de dos formas, en ambas los comandos que se van a ejecutar van a ser desde la raiz del repositorio descargado 

* La primera es que vamos a crear primero una imagen y posteriormente 3 contenedores:

    primero vamos a ejecutar el siguiente comando para crear la imagén a través del archivo ```Dockerfile```

    ```
    docker build -f src/Dockerfile --tag dockersparkprimer .
    ```

    En nuestro docker desktop podemos ver la imagén creada

    ![](/img/imagenManual.PNG)
      
    Ahora vamos a crear los contenedores para la imagén

    ```
    docker run -d -p 34000:6000 --name firstdockercontainer dockersparkprimer
    ```
    ```
    docker run -d -p 34001:6000 --name firstdockercontainer2 dockersparkprimer
    ```
    ```
    docker run -d -p 34002:6000 --name firstdockercontainer3 dockersparkprimer
    ```

    En nuestro docker desktop podemos ver los contenedores creados

    ![](/img/contenedoresManual.PNG)  
  
    Y podemos consultar las siguientes urls para validar:

  * [http://localhost:34000/hello](http://localhost:34000/hello)

    ![](/img/depliegueManual1.PNG)
  
  * [http://localhost:34001/hello](http://localhost:34001/hello)

    ![](/img/depliegueManual2.PNG)

  * [http://localhost:34002/hello](http://localhost:34002/hello)

    ![](/img/depliegueManual3.PNG)

* La segunda es desplegar una imagen y un contenedor a través del archivo ```docker-compose.yml```:
    
    Vamos a ejecutar el siguiente comando

    ```
    docker-compose up -d
    ```

    En nuestro docker desktop podemos ver la imagen creada y el contenedor creado

    ![](/img/contenedoresManual.PNG)

    Y nos vamos a dirigir a la siguiente url: 

  * [http://localhost:8087/hello](http://localhost:8087/hello)

    ![](/img/depliegueAuto.PNG)


## Despliegue a través de la imagén de docker hub

Este despliegue se basa en crear una imagen y un contenedor a raíz de un docker hub, los datos del repositorio de la imagen son los siguientes:

  * Nombre usuario: richardug
  * Nombe repositorio: firstsprkwebapprepo
  * Link: [https://hub.docker.com/repository/docker/richardug/firstsprkwebapprepo/general](https://hub.docker.com/repository/docker/richardug/firstsprkwebapprepo/general)

Vamos a ejecutar el siguiente comando

```
docker run -d -p 42000:6000 --name firstdockerimageaws richardug/firstsprkwebapprepo
```

Ahora podemos consultar la imagén creada con el comando

```
docker images
```

y el contenedor creado con el comando

```
docker ps
```

![](/img/CreaAWS.PNG)

Trás ejecutar el comando dependiendo si estamos ejecutándolo en aws o en nuestro local la url va a variar:

  * En el caso de ser local la url va a ser la siguiente:

    [http://localhost:42000/hello](http://localhost:42000/hello)

  * En el caso de ser en aws la url va a tener la siguiente estructura:

    ```
    http://(DNS público maquina EC2):42000/hello
    ```

    ![](/img/despliegueAWS.PNG)


## Autor
[Richard Santiago Urrea Garcia](https://github.com/RichardUG)
## Licencia & Derechos de Autor
**©** Richard Santiago Urrea Garcia, Ingeniero de Sistemas

Licencia bajo la [GNU General Public License](https://github.com/RichardUG/AYGO-Intro-virtualizacion-y-programacion-distribuida/blob/main/LICENSE).