# Despligue de aplicaciones web en PaaS (Cloud Computing)

## Objetivos

* Conocer las caracterśiticas que nos ofrece el cloud computing.
* Conocer las características y funcionalidades que obtenemos al usar la capa de PaaS
* Realizar un despliegue en un sistema PaaS: Heroku

## Contenidos

Caracterísitcas del Cloud Computing:

* Servicio disponible de forma automática y a demanda
* Accesible a través de la red
* Modelo multi-tenancy
	* Se comparten los recursos con otros usuarios
	* Debe garantizarse aislamiento y seguridad entre usuarios
* Los recursos se agrupan en pools
* Elasticidad
* Pago por uso

Platform as a Service (PaaS)

Plataforma de desarrollo web en la nube:

* Utilizado por desarrolladores de software
* Se proporciona toda la plataforma de desarrollo y despliegue de una aplicación al desarrollador
* Ejemplos: Google App Engine, Windows Azure, Heroku, Openshift, CloudFoundry 

* [Google App Engine](https://developers.google.com/appengine/)
* [Red Hat OpenShift](https://www.openshift.com/)
* [Heroku](http://www.heroku.com/)
* [Microsoft Windows Azure](http://www.windowsazure.com/)
* [Cloud Foundry](https://cloudfoundry.org/)

### Heroku

[Heroku](https://www.heroku.com/) es una aplicación que nos ofrece un servicio de Cloud Computing [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) (Plataforma como servicio). Como leemos en la Wikipedia es propiedad de Salesforce.com y es una de las primeras plataformas de computación en la nube, que fue desarrollada desde junio de 2007, con el objetivo de soportar solamente el lenguaje de programación Ruby, pero posteriormente se ha extendido el soporte a Java, Node.js, Scala, Clojure y Python y PHP. La funcionalidad ofrecida por heroku esta disponible con el uso de dynos, que son una adaptación de los contenedores Linux y nos ofrecen la capacidad de computo dentro de la plataforma.

Vamos a utilizar la capa gratuita de Horoku:

* Podemos crear un dyno, que puede ejecutar un máximo de dos tipos de procesos.
* Nuestro dyno utiliza 512 Mb de RAM
* Tras 30 minutos de inactividad el dyno se para (sleep), además debe estar parado 6 horas cada 24 horas.
* Podemos utilizar una base de datos postgreSQL con no más de 10.000 registros
* Para más información: [planes ofrecido por heroku](https://www.heroku.com/pricing#dynos-table-modal)


## Enlaces

* [Introducción a Heroku](https://www.linkedin.com/pulse/introduccion-heroku-jose-ramon-huerga-ayuso/)
