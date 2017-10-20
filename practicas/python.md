# Entorno de desarrollo y producción con aplicaciones web python

## Tarea 1: Entrono de desarrollo 

Formas parte del equipo de desarrollo de la aplicación "Gestión IESGN", aplicación web desarrollada con python, con el framework django. Vamos a configurar tu equipo como entrono de desarrollo para trabajar con la aplicación, para ello:

* Clona el repositorio de GitHub
* Crea un entorno virtual e instala las dependencias necesarias para que funcione el proyecto (fichero `requierements.txt`).
* Comprueba que vamos a trabajar con una base de datos sqlite (`gestion\settings.py`). ¿Cómo se llama la base de datos que vamos a crear?
* Crea la base de datos: `python manage.py migrate`. Este comando convierte el módelo de datos (ficheros `models.py`) en las tablas de la base de datos.
* Añade los datos de prueba a la base de datos. Para más información: [https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata](https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata).
* Crea un usuario administrador: python manage.py createsuperuser, y entra en la zona de administración para comprobar que los datos se han añadido correctamente.
* Ejecuta el servidor web de desarrollo y comprueba en el navegador que la aplicación está funcionando. Accede con el usuario `usuario`.

```eval_rst
.. note:: 
	En este momento, muestra al profesor la aplicación funcionando. Entrega un documentación resumida donde expliques los pasos fundamentales para realizar esta tarea. (3 puntos)
```

## Tarea 2: Desarrollando nuestra aplicación

Vamos a realizar un cambio en la aplicación y comprobar que los cambios se realizan 

```eval_rst
.. note:: 
	Indica que servicio de hosting has elegido. Indica las características del hosting que vas a utilizar. Indica la URL que tendrá tu página web. Indica el CMS que vas a instalar. (1 punto)
```

## Tarea 3: Instalación del CMS PHP en el hosting compartido.

* Descarga en tu ordenado el CMS PHP que vas a instalar.
* Sube los ficheros al hosting compartido por FTP.
* Realizar la configuración de la base de datos de forma adecuada.
* Realiza la instalación.
* Realiza una configuración mínima de la aplicación (Cambia la plantilla, crea algún contenido, ...)
* Instala un módulo para añadir alguna funcionalidad al CMS PHP.

```eval_rst
.. note:: 
	En este momento, muestra al profesor la aplicación funcionando. Entrega un documentación resumida donde expliques los pasos fundamentales para realizar esta tarea. (2 puntos)
```

## Tarea 4: Migración de la apliación web

* Elige otro servicio de hosting para PHP.
* Realiza el proceso de migración.

```eval_rst
.. note:: 
	Entrega un documentación resumida donde expliques los pasos fundamentales para realizar esta tarea.
	En este momento, muestra al profesor la aplicación funcionando en el otro hosting. (4 puntos)
```

## Tarea 5: Copia de seguridad de tu aplicación

* ¿Cómo harías una copia de seguridad de tu aplicación? ¿Crees que se puede automatizar dicha tarea?

```eval_rst
.. note:: 
	Entrega una documentación donde indiques los pasos para realizar una copia de seguridad. Si puedes realiza un pequeño script que automatice dicha tarea. (1 punto)
```

```eval_rst
.. warning:: 
	* Identificación de problemas: los cambios se realizan directamente en el servidor en producción
	* Identificación de problemas: los hosting compartidos no son escalables ni elásticos
	* Identificación de problemas: el uso de FTP no me permite control de versiones y no es el mecanismo más eficiente.
	* Identificación de problemas: Este esquema no funciona si tenemos un equipo de desarrollo construyendo una aplicación web a medida.
	* Identificación de problemas: Las copias de seguridad pueden ser complicadas de realizar y además es complicado la automatización.
```

