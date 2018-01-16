# Ejecutando un servicio en docker

## Trabajando con imágenes

Vamos a descargar una imagen del sistema operativo GNU/Linux Ubuntu del registro público docker hub. Normalmente el nombre de las imágenes tienen la forma *usuario/nombre:etiqueta*, si no indicamos la etiqueta será `latest`. Por ejemplo el nombre de una imagen puede ser **nuagebec/ubuntu:15.04**.

	$ sudo docker pull ubuntu 
	Unable to find image 'ubuntu:latest' locally
	latest: Pulling from library/ubuntu
	50aff78429b1: Pull complete 
	f6d82e297bce: Pull complete 
	275abb2c8a6f: Pull complete 
	9f15a39356d6: Pull complete 
	fc0342a94c89: Pull complete 
	Digest: sha256:ec0e4e8bf2c1178e025099eed57c566959bb408c6b478c284c1683bc4298b683
	Status: Downloaded newer image for ubuntu:latest

Como podemos ver cada imagen está formado por distintas capas, que corresponden a parte del sistema de fichero que forman la imagen. Las capas que son comunes a varias imágenes se comparten entre ellas y por lo tanto no es necesario bajarlas. Vamos a bajar otra imagen:

	$ sudo docker pull ubuntu:14.04

Y podemos ver todas las imágenes que tenemos en nuestro equipo local con:

	$ sudo docker images
	REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
	ubuntu                latest              00fd29ccc6f1        4 weeks ago         111MB
	ubuntu                14.04               67759a80360c        4 weeks ago         221MB
	debian                latest              da653cee0545        4 weeks ago         100MB

Para obtener información sobre una imagen, ejecutamos el siguiente comando:

	$ sudo docker inspect ubuntu

Para buscar imágenes en **docker hub**, podemos utilizar la siguiente instrucción:

	$ sudo docker search ubuntu

Si queremos buscar laas imágenes oficiales:

	$ sudo docker search --filter "is-official=true" debian

Y para borrar una imagen:

	$ sudo docker rmi ubuntu:14.04

## "Dockerizando" un servidor web apache

Como primera aproximación para crear una imagen desde la que podamos crear un contenedor que ofrezca un servicio, como, por ejemplo, un servidor web, daremos los siguientes pasos:

* Crearemos un contenedor desde una imagen base, por ejemplo desde la imagen "debian".
* Accederemos a ese contenedor e instalaremos un servidor web apache2.
* Crearemos una nueva imagen a partir de este contenedor que nos permitirá crear nuevos contenedores con el servidor web instalado.

Hay que indicar que el método que vamos a utilizar no es el que se usa habitualmente y que en estudiaremos el procedimiento habitual para conseguirlo, que será generar directamente una imagen con un servidor web instalado utilizando para ello un fichero Dockerfile y el comando docker build. De todas maneras vamos a mostrar este ejemplo que nos puede ser muy útil para seguir profundizando en el funcionamiento de docker.

En primer lugar vamos a crear un contenedor desde la imagen “debian” que habíamos descargado, para ello vamos a ejecutar la siguiente instrucción:

	$ sudo docker run -i -t --name primero debian /bin/bash
	root@61ee5966f2f3:/# apt-get update
	root@61ee5966f2f3:/# apt-get install apache2
	root@61ee5966f2f3:/# exit

Como vemos, hemos instalado en el contenedor el servidor web apache. Cuando se crea un contenedor, su sistema de fichero estará formado por la unión de las capas de la imagen origen, es decir tendrá el sistema de ficheros que tiene la imagen. Estas capas que forman el sistema de archivo del contenedor tienen dos características: son compartidas entre contenedores distintos que se crean desde la misma imagen, y son de sólo lectura, no se pueden modificar, por lo que cuando se crea un nuevo contenedor se añade una nueva capa de lectura y escritura donde se va registrando la creación de los nuevos ficheros y la modificación y borrado de los ficheros existentes.

Por lo tanto el sistema de archivo de nuestro contenedor estará formado por dos capas: la original de la imagen “debian”, y una segunda donde hemos creado los ficheros al instalar el servidor web. Cuando salimos de un contenedor de una sesión interactiva el contenedor se detiene (stop). Podemos ver la lista de contenedores detenidos:

	$ sudo docker ps -a
	 CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
	 61ee5966f2f3        debian              "/bin/bash"         8 minutes ago       Exited (0) 3 seconds ago                       primero

Una vez que hemos hecho una modificación en nuestro contenedor, si queremos utilizar el servidor web deberíamos crear una nueva imagen a partir del contenedor, para ello:

	$ sudo docker commit -m "Añadido apache" -a "José Domingo" 61ee5966f2f3 jose/apache:v1

Con `commit` vamos a crear una nueva imagen en nuestro repositorio local, se indica un comentario con la opción `-m`, el autor con la opción `-a`, el identificador del contenedor y finalmente el nombre de la nueva imagen.

	$ sudo docker images
	 REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	 jose/apache         v1                  81aeeac1781a        9 seconds ago       193.3 MB
	 debian              latest              9a02f494bef8        12 days ago         125.1 MB
	 ...

### Creando un nuevo contenedor con el servidor web

Ahora vamos a crear un nuevo contenedor a partir de la imagen que hemos creado anteriormente: jose/apache:v1. Este contenedor lo vamos a crear usando la opción `-d` que nos permite "demonizar" el contenedor, es decir que se ejecute indefinidamente, para ello:

	$ sudo docker run -d -p 8000:80 --name segundo jose/apache:v1 /usr/sbin/apache2ctl -D FOREGROUND
 	85218e86d6e48f360eb1c6e49c62da5e4ffd94b00308734e84f0253e72ec647d

	$ sudo docker ps
 	CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
 	85218e86d6e4        jose/apache:v1      "/usr/sbin/apache2ctl"   3 seconds ago       Up 2 seconds        0.0.0.0:8000->80/tcp   segundo

Vemos que el contenedor se está ejecutando, además con la opción `-p` mapeamos un puerto del equipo donde tenemos instalado el **docker engine**, con un puerto del contenedor. Además la instrucción que se ejecuta en el contenedor es la que nos permite ejecutar apache2 en segundo plano. En este caso podemos ver que accediendo al puerto 8000 de nuestro servidor docker accederemos al puerto 80 del contenedor.

Podemos ver los procesos que se están ejecutando en nuestro contenedor:

	$ sudo docker top segundo
	 UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
	 root                11211               7597                0                   20:49               ?                   00:00:00            /bin/sh /usr/sbin/apache2ctl -D FOREGROUND
	 root                11227               11211               0                   20:49               ?                   00:00:00            /usr/sbin/apache2 -D FOREGROUND
	 www-data            11228               11227               0                   20:49               ?                   00:00:00            /usr/sbin/apache2 -D FOREGROUND
	 www-data            11229               11227               0                   20:49               ?                   00:00:00            /usr/sbin/apache2 -D FOREGROUND

Para para nuestro contenedor:

	$ sudo docker stop segundo

Y lo podemos volver a ejecutar:

	$ sudo docker start segundo

O en un solo paso:

	$ sudo docker restart segundo

Y finalmente para borrar el contenedor:

	$ sudo docker stop segundo
	$ sudo docker rm segundo
