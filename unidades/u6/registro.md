# Gestionando el registro Docker Hub

Para transferir la imagen de un equipo a otro tenemos dos posibilidades:

* Podríamos guardar la imagen en un fichero tar, que podemos copiar al otro equipo para restaurarlo en él.
* Podríamos guardar la imagen en un registro docker. Podemos instalar un registro en nuestra infraestructura o utilizar **docker hub**, que es una aplicación web que nos proporciona la posibilidad de guardar nuestras imágenes. Una vez que la imagen esta guardada en el registro podemos descargarla desde el entorno de producción.

Para ver las distintas opciones que tenemos a nuestra disposición vamos a partir de la siguiente imagen que hemos creado:

	$ sudo docker images 
	REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	josedom24/apache2   latest              04800781aed6        17 seconds ago      183.7 MB

## Exportación/importación de imágenes

Como hemos indicado anteriormente una imagen la podemos guardar en un fichero tar para exportarla a otro equipo.

Para exportar una imagen ejecutamos el siguiente comando:

	$ sudo docker save -o apache2.tar josedom24/apache2

Y se genera un fichero tar, que podemos ver:

	$ ls -alh
	-rw-r--r-- 1 usuario usuario 184M feb 17 21:02 apache2.tar

Este fichero lo podemos guardar en cualquier medio de almacenamiento, o enviarlo por internet a otro equipo, donde realizaríamos la importación:

	$ docker load -i apache2.tar josedom24/apache2

## Guardando nuestras imágenes en docker hub

Otra opción que tenemos es guardar nuestra imagen en el registro docker hub, de esta forma sería muy sencillo descargarlo en otro equipo. Es necesario tener una cuenta en docker hub, nosotros ya tenemos una cuenta con el usuario *josedom24*.

Para poder subir una imagen a nuestra cuenta de docker hub es necesario autentificarnos, para ello:

	$ sudo docker login
	Username: josedom24
	Password: 
	Email: xxxxxxxx@gmail.com
	WARNING: login credentials saved in /home/usuario/.docker/config.json
	Login Succeeded

Y podemos subir nuestra imagen con el comando:

	$ docker push josedom24/apache2
	The push refers to a repository [docker.io/josedom24/apache2]
	3155f6b09710: Pushed 
	67331ad8a75e: Pushed 
	5f70bf18a086: Pushed 
	78dbfa5b7cbc: Pushed
	latest: digest: sha256:bfe4d16f3e8d7f31b5f1bc0e1d989cbe6d762d1f4770fedf435685e24ee7bf8c size: 644

Podemos comprobar que la imagen se ha subido a docker hub buanscando en la [página de docker hub](https://hub.docker.com/r/josedom24/apache2/).

Ya podemos buscar la nueva imagen que hemos subido y bajarla en otro servidor:

	$ sudo docker search josedom24
	NAME                DESCRIPTION   STARS     OFFICIAL   AUTOMATED
	josedom24/apache2                 0

	$ docker pull josedom24/apache2

	