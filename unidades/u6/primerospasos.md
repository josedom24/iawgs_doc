# Nuestro primer contenedor "Hola Mundo"

Para crear nuestro primer contenedor vamos a ejecutar la siguiente instrucción:

	$ sudo docker run ubuntu /bin/echo 'Hello world'
	Unable to find image 'ubuntu:latest' locally
	latest: Pulling from library/ubuntu
	50aff78429b1: Pull complete 
	f6d82e297bce: Pull complete 
	275abb2c8a6f: Pull complete 
	9f15a39356d6: Pull complete 
	fc0342a94c89: Pull complete 
	Digest: sha256:ec0e4e8bf2c1178e025099eed57c566959bb408c6b478c284c1683bc4298b683
	Status: Downloaded newer image for ubuntu:latest
	Hello world

Con el comando `run` vamos a crear un contenedor donde vamos a ejecutar un comando, en este caso vamos a crear el contenedor a partir de una imagen ubuntu. Como todavía no hemos descargado ninguna imagen del registro docker hub, es necesario que se descargue la  imagen. Si la tenemos ya en nuestro ordenador no será necesario la descarga. Más adelante estudiaremos como funcionan las imágenes en docker. Finalmente indicamos el comando que vamos a ejecutar en el contenedor, en este caso vamos a escribir un “Hola Mundo”.

Por lo tanto, cuando se finaliza la descarga de la imagen, se crea un contenedor a partir de la imagen y se ejecuta el comando que hemos indicado, podemos ver la salida en pantalla. Una vez que se ejecuta la instrucción el contenedor se detiene (stop), podemos ver la lista de contenedores detenidos con el siguiente comando:

	$ sudo docker ps -a
	CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                          PORTS               NAMES
	0184aa1058c1        ubuntu              "/bin/echo 'Hello wo…"   About a minute ago   Exited (0) About a minute ago                       zen_tereshkova


## Ejecutando un contenedor interactivo

En este caso usamos la opción `-i` para abrir una sesión interactiva, `-t` nos permite crear un pseoudo-terminal que nos va a permitir interaccionar con el contenedor, indicamos un nombre del contenedor con la opción `--name`, y la imagen que vamos a utilizar para crearlo, en este caso "ubuntu",  y por último el comando que vamos a ejecutar, en este caso /bin/bash, que lanzará una sesión bash en el contenedor:

	$ sudo docker run -i -t --name contenedor1 ubuntu /bin/bash
	root@a3bcd5c3e836:/# ls
	bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
	root@a3bcd5c3e836:/# exit
	exit
	$ 

Como podemos comprobar podemos ejecutar distintos comandos dentro del contenedor, por ejemplo hemos visto el árbol de directorios. Cuando salimos de la sesión, el contenedor se detiene. De nuevo podemos ver los contenedores detenidos:

	$ sudo docker ps -a
	CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES
	a3bcd5c3e836        ubuntu              "/bin/bash"              About a minute ago   Exited (0) 35 seconds ago                       contenedor1
	0184aa1058c1        ubuntu              "/bin/echo 'Hello wo…"   4 minutes ago        Exited (0) 4 minutes ago                        zen_tereshkova

A continuación vamos a iniciar el contenedor y nos vamos a conectar a él:

	$ sudo docker start contenedor1
	contenedor1
	debian@docker:~$ sudo docker attach contenedor1
	root@a3bcd5c3e836:/# 


Para obtener información del contenedor:

	$ sudo docker inspect contenedor1
	[
	    {
	        "Id": "a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46",
	        "Created": "2018-01-03T19:28:12.664192997Z",
	        "Path": "/bin/bash",
	        "Args": [],
	        "State": {
	            "Status": "exited",
	            "Running": false,
	            "Paused": false,
	            "Restarting": false,
	            "OOMKilled": false,
	            "Dead": false,
	            "Pid": 0,
	            "ExitCode": 0,
	            "Error": "",
	            "StartedAt": "2018-01-03T19:30:04.490390766Z",
	            "FinishedAt": "2018-01-03T19:30:44.388262264Z"
	        },
	        "Image": "sha256:00fd29ccc6f167fa991580690a00e844664cb2381c74cd14d539e36ca014f043",
	        "ResolvConfPath": "/var/lib/docker/containers/a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46/resolv.conf",
	        "HostnamePath": "/var/lib/docker/containers/a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46/hostname",
	        "HostsPath": "/var/lib/docker/containers/a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46/hosts",
	        "LogPath": "/var/lib/docker/containers/a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46/a3bcd5c3e8366203dc96e5022651cc401ce40d83a0215280fe15cf3fff8e1a46-json.log",
	        "Name": "/contenedor1",
        ...

## Creando un contenedor demonio

Crear un contenedor que ejecute una sola instrucción y que luego se pare no es muy útil, a continuación vamos a crear un contenedor que funcione como un demonio y este continuamente ejecutándose.

	$ sudo docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
	fec633187247f0d092d046be65606ccc9c046b6486c5841051b8ea10c00b8dee

En esta ocasión hemos utilizado la opción `-d` del comando `run`, para la ejecución el comando en el contenedor se haga en segundo plano. La salida que hemos obtenido el el ID del contenedor que se está ejecutando, aunque cuando visualizamos los contenedores en ejecución sólo vemos un ID corto:

	$ sudo docker ps
	CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
	fec633187247        ubuntu              "/bin/sh -c 'while t…"   36 seconds ago      Up 35 seconds                           priceless_wescoff

Podemos ver la salida del contenedor accediendo a los logs del contenedor, indicando el id o el nombre que se ha asignado:

	$ sudo docker logs priceless_wescoff
	hello world
	hello world
	hello world
	hello world
	...

Por último podemos parar el contenedor y borrarlo con las siguientes instrucciones:

	$ sudo docker stop priceless_wescoff
	$ sudo docker rm priceless_wescoff
