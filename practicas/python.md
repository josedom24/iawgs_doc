# Entorno de desarrollo y producción con aplicaciones web python

## Tarea 1: Entrono de desarrollo 

Formas parte del equipo de desarrollo de la aplicación "Gestión IESGN", aplicación web desarrollada con python, con el framework django. Vamos a configurar tu equipo como entorno de desarrollo para trabajar con la aplicación, para ello:

* Realiza un fork del repositorio de GitHub: [https://github.com/jd-iesgn/iaw_gestionGN](https://github.com/jd-iesgn/iaw_gestionGN).
* Clona el repositorio en tu equipo.
* Crea un entorno virtual e instala las dependencias necesarias para que funcione el proyecto (fichero `requierements.txt`).
* Comprueba que vamos a trabajar con una base de datos sqlite (`gestion\settings.py`). ¿Cómo se llama la base de datos que vamos a crear?
* Crea la base de datos: `python manage.py migrate`. A partir del modelo de datosse crean las tablas de la base de datos.
* Añade los datos de prueba a la base de datos. Para más información: [https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata](https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata). Utiliza el fichero `datos.json`.
* Entra en la zona de administración para comprobar que los datos se han añadido correctamente. Usuario: `admin` ontraseña: `asdasd1234`).
* Ejecuta el servidor web de desarrollo y comprueba en el navegador que la aplicación está funcionando. Accede con el usuario `usuario` (contraseña: `asdasd1234`).

```eval_rst
.. note:: 
	En este momento, muestra al profesor la aplicación funcionando. Entrega una documentación resumida donde expliques los pasos fundamentales para realizar esta tarea. (3 puntos)
```

## Tarea 2: Desarrollando nuestra aplicación

Vamos a realizar un cambio en la aplicación y comprobar que los cambios se realizan correctamente.

* Modifica la página inicial de la aplicación para que aparezca tu nombre.
* Sube los cambios al repositorio

```eval_rst
.. note:: 
	Muestra una captura de pantalla donde sea la modificación realizada. (1 punto)
```

## Tarea 3: Entorno de producción

Vamos a realizar el despliegue de nuestra aplicación en un entorno de producción, para ello vamos a utilizar una instancia del cloud, para ello:

* Instala en el servidor los servicios necesarios (apache2, mysql, ...). Instala el módulo de apache2 para ejecutar código python.
* Clona tu repositorio en el `DocumentRoot` de tu virtualhost.
* Crea un entorno virtual e instala las dependencias de tu aplicación.
* Instala en el entorno virtual el módulo que permite que python trabaje con mysql: 

		$ apt-get build-dep python-mysqldb

	Y en el entorno virtual:

		(env)$ pip install mysql-python

* Configura un virtualhost en apache2 con la configuración adecuada para que funcione la aplicación. El punto de entrada de nuestro servidor será `iaw_gestionGN/gestion/wsgi.py`.
* Crea una base de datos y un usuario en mysql.
* Configura la aplicación para trabajar con mysql, para ello modifica la configuración de la base de datos en el archivo `settings.py`:

		DATABASES = {
		    'default': {
		        'ENGINE': 'django.db.backends.mysql',
		        'NAME': 'myproject',
		        'USER': 'myprojectuser',
		        'PASSWORD': 'password',
		        'HOST': 'localhost',
		        'PORT': '',
		    }
		}

* Crea las tablas de la base de datos y carga los datos de pruebas. Accede a mysql y comprueba que se han creado de forma adecuada.
* Desactiva en la configuración (fichero `settings.py`) el modo debug a False. Para que los errores de ejecución no den información sensible de la aplicación.
* Muestra la página funcionando.

```eval_rst
.. note:: 
	En este momento, muestra al profesor la aplicación funcionando. Entrega una documentación resumida donde expliques los pasos fundamentales para realizar esta tarea. (4 puntos)
```

## Tarea 4: Modificación de la aplicación en el entorno de producción

Vamos a realizar cambios en el entorno de desarrollo y posteriormente vamos a subirlas a producción.

* Modifica la página inicial para que muestre otra imagen. Despliega los cambios en el servidor de producción.
* Vamos a crear una nueva tabla en la base de datos, para ello sigue los siguientes pasos:
	
1. Añade un n uevo modelo al fichero `centro/models.py`:

		class Modulo(models.Model):	
			Abr = models.CharField(max_length=4)
			Nombre = models.CharField(max_length=50)
			Unidad = models.ForeignKey(Cursos,blank=True,null=True,on_delete=models.SET_NULL)
			
			def __unicode__(self):
				return self.Abr+" - "+self.Nombre 		

			class Meta:
				verbose_name="Modulo"
				verbose_name_plural="Modulos"

2. Crea una nueva migración: `python manage.py makemigrations`. 
3. Y realiza la migración: `python manage.py migrate`
4. Añade el nuevo modelo al sitio de administración de djanfo, para ello añade la siguiente línea en el fichero `centro/admin.py`:

	






```eval_rst
.. note:: 
	Entrega una documentación resumida donde expliques los pasos fundamentales para realizar esta tarea.
	En este momento, muestra al profesor la aplicación funcionando en el otro hosting. (4 puntos)
```

## Tarea 5: 

* ¿Cómo harías una copia de seguridad de tu aplicación? ¿Crees que se puede automatizar dicha tarea?
realizar el despliegue de nuestra aplicación en un entorno de producción, para ello vamos a utilizar 
```eval_rst
.. note:: 
	Entrega una documentación donde indiques los pasos para realizar una copia de seguridad. Si puedes realiza un pequeño script que automatice dicha tarea. (1 punto)
```

```eval_rst
.. warning:: 
	* Identificación de problemas: los cambios se realizan directamente en el servidor en producción
	* Identificrealizar el despliegue de nuestra aplicación en un entorno de ación de problemas: los hosting producción, para ello vamos a utilizar compartidos no son escalables ni elásticos
	* Identificación de problemas: el uso de FTP no me permite control de versiones y no es el mecanismo más eficiente.
	* Identificación de problemas: Este esquema no funciona si tenemos un equipo de desarrollo construyendo una aplicación web a medida.
	* Identificación de problemas: Las copias de seguridad pueden ser complicadas de realizar y además es complicado la automatización.
```

