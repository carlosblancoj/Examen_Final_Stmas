# Examen final Sistemas Informáticos
## · Introducción
Para el despliegue de la aplicación se ha optado por usar el proyecto de ejemplo ofrecido por el docente, debido a que mi proyecto personal usaba Oracle y en términos de eficiencia es preferible usar MySQL.

De este modo, tras realizar la clonación del repositorio se empezará con el desarrollo de la documentación.
## · Configuración del archivo docker-compose.yml
Para llevar a cabo la configuración del archivo docker-compose, en el cual se definirán los distintos contenedores con los servicios que conformarán la aplicación. 
En este caso, se va a emplear un contenedor con una imagen de Apache Tomcat para el despliegue de la capa de presentación y de proceso, y otros dos con MySQL y phpMyAdmin para el despliegue de la capa de datos, formando un modelo de tres capas.
### Tomcat
Para la configuración del servicio web, definimos la imagen que va a usar, en este caso Tomcat. 
Después es necesario definir el volumen a utilizar, en el cual se declara el archivo LoginWebApp.war que contiene todos los componentes necesarios para ejecutar la aplicación.
Una vez hecho esto, solo queda establecer los puertos para realizar esa ejecución y la conexión con la base de datos.

![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/1.png)
### MySQL
Para la configuración del servicio de almacenamiento de datos, definimos la imagen que va a usar, en este caso MySQL versión 5.7.
Después es necesario definir el volumen donde se realizará la gestión de datos, a partir de la instrucción *Entrypoint* de Docker.
Una vez hecho esto, solo queda establecer los puertos y la configuración del entorno para la gestión de la base de datos desde el siguiente servicio.

![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/2.png)
### PHPMyAdmin
Para la configuración del servicio de gestión de datos, definimos la imagen que va a usar, en este caso phpmyadmin y que depende del servicio anterior *db*.
Tras esto, solo falta establecer los puertos para la conexión del usuario con la base de datos y configurar el entorno para su acceso.

![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/3.png)
## · Pasos para el despliegue de la aplicación
Una vez se ha configurado el archivo docker-compose.yml se procede a su ejecución. Para ello, desde el terminal nos colocamos en el directorio en el que se encuentra el archivo y lanzamos el siguiente comando:
~~~
docker-compose up -d
~~~
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/4.png)
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/6.png)

Una vez lanzado, para comprobar que lo contenedores han sido creados y están en ejecución empleamos el siguiente comando:
~~~
docker ps
~~~
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/12.png)

De esta forma, si el usuario accede  `localhost:8082/LoginWebApp`, se encontrará con la página principal de la aplicación totalmente funcional.

![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/7.png)
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/10.png)
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/11.png)

Por otro lado, si accede a `localhost:8081`, se encontrará con el servicio phpMyAdmin desde el cual podrá realizar la gestión de la base de datos accediendo como usuario *root*.

![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/8.png)
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/9.png)

## · Preparación y subida a Docker Hub
Por último, es necesario construir una imagen personalizada local a partir del DockerFile usando el siguiente comando:
~~~
docker build -t carlesbj/final_stmas .
~~~
Tras esto, se debe realizar el login a DockerHub usando el siguiente comando:
~~~
docker login --username=carlesbj
~~~
Una vez logeados, estamos preparados para subir la imagen a DockerHub usando el siguiente comando:
~~~
docker push carlesbj/final_stmas
~~~
![FOTO](https://github.com/carlosblancoj/Examen_Final_Stmas/blob/main/ExamenFinalStmas/13.png)

## · Anexos
El comando para descargar la imagen es el siguiente:
~~~
docker pull carlesbj/final_stmas:latest
~~~
La URL al Docker Hub:
~~~
https://hub.docker.com/repository/docker/carlesbj/final_stmas/
~~~
