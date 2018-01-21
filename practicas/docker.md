# Introducción a docker

En estas práctica vamos a empezar a trabajar con la tecnología de contenedores docker.

## Tarea 1: Ejecutando un servicio en un contenedor Docker

* Elige una imagen docker como base para crear un contenedor interactivo. Accede a él y realiza la instalación de un servicio nginx. 
* Crea una nueva imagen a partir del contenedor anterior.
* A partir de la nueva imagen crea un contenedor y comprueba que el servidor web esté funcionando.
* Suponiendo que has instalado docker en tu entorno de desarrollo/prueba, realiza un despliegue del contenedor a un entorno de producción (otra máquina con docker instalado). Para ello guarda la imagen generada en docker hub y bájala en el entorno de producción, para crear un nuevo contenedor. Este ejercicio lo podeís hacer entre compañeros.
* A continaución queremos cambiar la página web que sirve el servidor web, describe los pasos que deberíamos realizar para realizarlo. A coninuación realiza el cambio.

```eval_rst
.. note:: 
	* Entrega una breve documentación de los pasos que has dado para realizar el ejercicio. Entrega una captura de pantalla donde se vea el acceso al servidor web. (2 puntos).
	* Repite el ejercicio con un servidor mysql (no es necesario hacer el último punto). Demuestra que puedes acceder al servidor mysql. (2 puntos)
```

## Tarea 2: Creación de una imagen docker con Dockerfile

Realiza un `Dockerfile` que nos permita crear una imagen desde la que se puedan crear contenedores que sirvan una página web en un servidor web nginx. La página web que se sirve debe ser una plantilla html5.

```eval_rst
.. note:: 
	* Entrega el fichero `Dockerfile`.
	* Documenta los pasos que has dado para crear un contenedor que sirva la página web.
	* ¿Qué pasos tienes que dar para modificar el contenido dela página? Documenta brevemente los pasos que has dado.
	(2 puntos)
```

## Tarea 3: Configuración de contenedores por medio de variables de entorno

Queremos configurar el servidor nginx por medio del uso de variables de entorno, para ello:

* Crea en el fichero `Dockerfile` las variables de entorno siguiente:
	* `DOCUMENTROOT`: Indica el directorio raiz del servidor, por defecto será `/var/www/html`.
	* `SERVER_NAME`: Indica el nombre del servidor, (directiva `server_name`), por defect es `_`.
* Tendrás que crear un script `run.sh` que será el encargado de configurar nginx antes de ejectura el proceso, y será el proceso que ejecuta el contenedor.
* Recuerda que los ficheros tendrán que ser copiados al directorio donde se indica en la variable de entorno `DOCUMENTROOT`.

```eval_rst
.. note:: 
	* Crea un contenedor si modificar ninguna variable de entorno. 
	* A continuación crea otro contenedor pero modificando las dos variables de entorno.
	(3 puntos)
```


## Tarea 4: Creación automática de una imagen docker en Docker Hub

Realiza los siguinetes pasos:

* Crea un repositorio en GitHub, y sube desde una máuina donde no tengas docker instalado el contexto (`Dockerfile` y ficheros necesarios) del ejercicio anterior.
* Crea desde Docker Hub un "Automated build" y da permisos a Docker Hub para que acceda a tu respositorio GitHub.
* Comprueba que se ha creado la nueva imagen.
* Descarga la nueva imagen en tu servidor Docker y crea un nuevo contenedor.

```eval_rst
.. note:: 
	* Documenta los pasos que has dado para realizar la tarea.
	* ¿Qué pasos tienes que dar para modificar el contenido dela página? Documenta brevemente los pasos que has dado. Y muestra la nueva página con los cambios que has introducido.
	(3 puntos)
```
