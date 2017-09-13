# Implantación de aplicaciones web
## CFGS ASIR (2017-2018)

### Contenidos

1. Introducción a las aplicaciones web
2. Implantación de aplicaciones web en entornos locales
3. Despliegue tradicional de aplicaciones web
4. Integración continua 
5. Entrega continua
6. Despliegue moderno de aplicaciones web (IaaS, PaaS, contenedores)

### Prácticas

1. Implantación de una aplicación web estática en Github Pages

* Aprender a trabajar con git y github
* Aprender lenguaje de marcas markdown
* Comprender que existe un integración continua y un despliegue continuo en el proceso de despliegue de la página

2. Instalación local de un CMS PHP (WordPress)

* Aprender a instalar la pila LAMP en un servidor
* Identificar las características de los CMS más usado
* Descargar e instalar un CMS wordpress
* Separar servidor web y servidor de base de datos en equipos distintos
* Instalación de otros CMS usando virtualhost
* Necesidad de otros servicios: por ejemplo, servidor de correo saliente

3. Despliegue tradicional de CMS (Drupal)

* Seleccionar un hosting compartido e identificar sus características
* Subir ficheros al hosting compartido (FTP)
* Realizar la configuración de la base de datos de forma adecuada
* Modificación (instalación de plugin) en el CMS
* Migración a otro hosting compartido
* Identificación de problemas: los cambios se realizan directamente en el servidor en producción
* Identificación de problemas: los hosting compartidos no son escalables ni elásticos
* Identificación de problemas: el uso de FTP no me permite control de versiones y no es 
* Identificar problemas: Este esquema no funciona si tenemos un equipo de desarrollo construyendo una aplicación web a medida

4. Entorno de desarrollo aplicaciones web python

* Identificar las características entre los distintos entornos (desarrollo, producción)
* Identificar la necesidad de utilizar sistemas de control de versión como git
* Identificar la problemática de que el entono de desarrollo se tiene asemejar lo máximo posible al de producción: infraestructura y dependencias (vagrant y entornos virtuales).
* Valorar el uso de los framework para el desarrollo de aplicaciones web
* Utilizar servidores web de desarrollo para probar la aplicación.
* Entender que los datos de la aplicación son distintos en desarrollo y producción (base de datos de desarrollo y base de datos en producción), incluso con motores de base de datos distintos.
* Identificación de problemas: si estamos desarrollando una aplicación es necesario probarla, realizar test.
* Identificación de problemas: además de lo anterior el equipo de desarrollo necesita ir haciendo otros procesos: analizando el código generado, generar documentación,...
* Identificación de problemas: Nuestro equipo de desarrollo las componen varios miembros: es fundamental utilizar un repositorio común (git)
* Identificación de problemas: Si seguimos una metodología ágil es deseable que todos los cambios que vayan realizando los programadores se vayan probando, analizando, ... de forma continúa
* Identificación de problemas: ¿Y si esas tareas las automatizamos? -> Integración continúa

5. Integración y despliegue automático de páginas estáticas con Travis y surge

* Conocer el software de integración continúa más utilizados
* Tener una primera experiencia con travis para realizar la integración continúa (en este caso simplemente realizar de forma automática que todos los cambios en nuestra página web estática es válida)
* Despliegue manual de nuestra página en el servicio surge.sh
* Entender el concepto de despliegue continúo y comprobar la función de despliegue de travis sobre surge.sh

6. Integración continua de una aplicación web python

7. Despliegue de aplicación web python en IaaS
8. Despliegue de aplicación web python en PaaS
9. Despliegue de aplicación web python en contenedores
10. Implantación de aplicación web JAVA en un entorno local
11. Integración continúa de una aplicación Java




