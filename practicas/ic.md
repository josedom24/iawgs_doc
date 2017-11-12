# Introducción a la integración continua

Antes de comenzar date de alta en el servicio web [travis](https://travis-ci.org/) con tu cuenta de github. Travis nos permite hacer integración continúa en los proyectos que tenemos guardados en nuestros repositorios de GitHub.

## Tarea 1: Corrector ortográfico de documentos markdown (test)

Imaginemos que estamos escribiendo documentos markdown y lo guardamos en un repositorio de github. Queremos que cada vez que hagamos una modificación (commit - push) queremos probar (test) si tienes alguna falta de ortografía. Ese proceso lo vamos a hacer de forma automática y continua con travis. Si tenemos activada la IC en travis sobre nuestro repositorio, cada vez que hagamos un push, travis va a crear una máquina (entorno de pruebas), va a clonar nuestro repositorio y va a realizar la prueba (test) que indiquemos en el fichero `.travis.yml`. Cuando termine la prueba nos va mandar un correo informándonos si la prueba ha tenido éxito o no.

Por lo tanto realiza los siguientes pasos:

* Realiza un fork del repositorio de GitHub: [https://github.com/josedom24/ic-travis-diccionario](https://github.com/josedom24/ic-travis-diccionario).
* Activa la IC en travis de tu repositorio.
* Comprueba la prueba que vamos a realizar estudiando el fichero `.travis.yml`.
* Realiza cambios en los ficheros que están en el directorio `doc` y comprueba en travis como se van ejecutando las pruebas.


```eval_rst
.. note:: 
	Entrega varias capturas de pantalla donde se vea una prueba que termina en éxito (sin faltas de ortografía) y otra que no termine en éxito (1 punto)
```

## Tarea 2: Comprobación de html5 válido y despliegue en surge.sh (test y deploy)

En esta tarea queremos desplegar una página html5 en el servicio surge.sh, además queremos comprobar si el código html5 es válido. Estas dos operaciones: comprobar si el html5 es válido (test) y el despliegue en surge.sh (deploy) lo vamos a hacer con travis de forma automática (IC y DC).

Antes de empezar vamos a aprender a trabajar con [surge.sh](http://surge.sh/):

* Siguiendo las instrucciones de esta [página](https://linuxconfig.org/how-to-install-nodejs-on-debian-9-stretch-linux) instala NodeJS y npm.
* Instala surge.sh
* Despliega una pequeña página web en el dominio `tunombre.surge.sh`.

```eval_rst
.. note:: 
	Entrega una descripción con los pasos fundamentales para la instalación y una captura de la página web que has realizado. (1 punto)
```

Vamos a añadir la funcionalidad de IC y DC con travis, para ello:

* Realiza un fork del repositorio de GitHub: [https://github.com/josedom24/ic-travis-html5](https://github.com/josedom24/ic-travis-html5)
* Activa la IC en travis de tu repositorio.
* Comprueba la prueba y el despliegue que vamos a realizar estudiando el fichero `.travis.yml`.
* Modifica el fichero `.travis.yml` para poner el nombre de dominio que vas a utilziar.
* Para que travis pueda hacer el despliegue en surge le tenemos que indicar un TOKEN. Genera el token:
	
	surge token

* Crea dos variables de entorno en *settings* del proyecto travis:
	
    * SURGE_LOGIN: Indica el correo electrónico que has utilizado como lógin en surge
    * SURGE_TOKEN: Indica el TOKEN que has obtenido en el paso anterior.

* Realiza cambios en el fichero index.html del directorio `_build` y comprueba, que si el código html5 es válido se despliega y puedes aceder a la página web. Si el código html5 no es válido no se realiza el despliegue y te mandan un correo informando de la incidencia.

```eval_rst
.. note:: 
	Entrega una descripción con los pasos fundamentales que has realizado. Entrega varias capturas de pantalla donde se vea una prueba que termina en éxito (sin faltas de ortografía) y otra que no termine en éxito (1 punto)
```
