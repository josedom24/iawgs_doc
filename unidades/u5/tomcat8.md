# Introducción a Tomcat 8

En el siguiente documento se explicará como implantar un contenedor de servlets Tomcat versión 8 en un sistema Linux Debian Stretch.

## Instalación

Para instalar tomcat8 desde repositorios:
	
	# apt install tomcat8

Por dependecia va a instalar el paquete `openjdk-8-jre-headless`, que corresponde a una implementación de la JVM mínima para poder ejecuar nuestros programas java.

Desde este momento tendremos Tomcat ejecutandose y sirviendo en el puerto 8080.

![tomcat](img/tomcat.1.png)