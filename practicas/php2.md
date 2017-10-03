# Despliegue tradicional de CMS PHP

Esta tarea consiste en instalar un CMS de tecnología PHP (elige un CMS que no hayas usado en la práctica anterior) en un hosting compartido. Los pasos que tendrás que dar los siguientes:

## Tarea 1: Elección de un hosting compartido

* Elige un servicio de hosting compartido con las caracterísitcas necesarias para instalar un CMS PHP (soporte PHP, base de datos,...)
* Date de alta en el servicio.

```eval_rst
.. note:: 
	Indica que servicio de hosting has elegido. Indica la URL que tendrá tu página web. Indica el CMS que vas a instalar.
```

## Tarea 2: Instalación del CMS PHP en el hosting compartido.

* Descarga en tu ordenado el CMS PHP que vas a instalar.
* Sube los ficheros al hosting compartido por FTP.
* Realizar la configuración de la base de datos de forma adecuada.
* Realiza la instalación.
* Realiza una configuración mínima de la aplicación (Cambia la plantilla, crea algún contenido, ...)
* Instala un módulo para añadir alguna funcionalidad al CMS PHP.

```eval_rst
.. note:: 
	En este momento, muestra al profesor la aplicación funcionando. Entrega un documentación resumida donde expliques los pasos fundamentales para realizar esta tarea.
```

## Tarea 3: Migración de la apliación web

* Elige otro servicio de hosting para PHP.
* Realiza el proceso de migración.

```eval_rst
.. note:: 
	Entrega un documentación resumida donde expliques los pasos fundamentales para realizar esta tarea.
	En este momento, muestra al profesor la aplicación funcionando en el otro hosting.
```

## Tarea 4: Copia de seguridad de tu aplicación

* ¿Cómo harías una copia de seguridad de tu aplicación? ¿Crees que se puede automatizar dicha tarea?

```eval_rst
.. note:: 
	Entrega una documentación donde indiques los pasos para realizar una copia de seguridad. Si puedes realiza un pequeño script que automatice dicha tarea.
```

```eval_rst
.. warning:: 
	* Identificación de problemas: los cambios se realizan directamente en el servidor en producción
	* Identificación de problemas: los hosting compartidos no son escalables ni elásticos
	* Identificación de problemas: el uso de FTP no me permite control de versiones y no es el mecanismo más eficiente.
	* Identificación de problemas: Este esquema no funciona si tenemos un equipo de desarrollo construyendo una aplicación web a medida.
	* Identificación de problemas: Las copias de seguridad pueden ser complicadas de realizar y además es complicado la automatización.
```

