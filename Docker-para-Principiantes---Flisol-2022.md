---
author: 'Luis Alberto Zambrana'
slug: 'Docker_para_Principiantes_-_Flisol_2022'
title: 'Docker para Principiantes - Flisol 2022'

---

# Docker para Principiantes - Flisol 2022
<p align="center">
<img src="https://lh4.googleusercontent.com/qzU0oa1Et16dQ6fyWw40fW12tw1WpvTJcX_cde0RDq2twepehkF9kAFzRE4Yan91biIZX_n1o5d5NJbt_pDRcpVGL26ZnKEpj3L9QgF_cxMlVwHcUhQzhOjsKjy1cuxZTDEqzieu">
</p>

## DOCKER

\- - - - X

Docker es un proyecto de **código abierto** que automatiza el despliegue de aplicaciones dentro de contenedores de software, proporcionando una capa adicional de abstracción y automatización de virtualización de aplicaciones en múltiples sistemas operativos. Docker utiliza características de **aislamiento de recursos del kernel** Linux, tales como cgroups y espacios de nombres (**namespaces**) para permitir que 'contenedores' independientes se ejecuten dentro de una sola instancia de Linux, evitando la sobrecarga de iniciar y mantener máquinas virtuales.

<p align="center">
<img src="https://lh5.googleusercontent.com/z9sYMtui-bIGE0Yr4yt-nhkJBSZrOFxNyZwbwP2nhFQwbKU4Rt0m4shhv1KixRhSrSttwkL2HSTLEoqsQRoaEePmmr03mQ_scNhZ1gV_EiF6J3eOdxdbuOj23rCQUPd4V-l5KMNX">
</p>

## ESTRUCTURA DE DOCKER

\- - - - X

En vez de hacer un **docker** vs máquina virtual veremos que no existe un hipervisor sino que usamos el **Kernel del hos**t. Cada vez que armábamos una máquina virtual teníamos que disponer de disco, redes, instalar el sistema operativo e instalar todo lo que se requiere para la aplicación 1 (podría ser una aplicación que utiliza php3) ¿y que pasa si necesito algo en php4? ¿Tengo que instalar otra máquina virtual? Así nos vamos adentrando a los contenedores donde van a estar nuestras aplicaciones por separado, no vamos a tener que instalar el sistema operativo cada vez que se requiere de una aplicación y la utilización de imágenes para creación de contenedores hará que disminuya nuestro tiempo de instalación de aprox 1 hora a 5 minutos.

## CONCEPTOS BÁSICOS

\- - - - X

### ¿QUÉ ES UNA IMAGEN EN DOCKER?

Una imagen es “como un snapshot de una máquina virtual”. Esta imagen que alimenta al contenedor al momento de su creación puede ser creada por nosotros mismos o bien podemos utilizar una que ya fuera creada por alguien más y que pueden estar alojadas en https://hub.docker.com/ o simplemente nos la pasan por algún medio.

### ¿QUÉ ES UN CONTENEDOR EN DOCKER?

Los contenedores son instancias de las imágenes que hemos creado o descargado y que se ejecutan de forma aislada. A partir de una imagen podríamos ejecutar varios contenedores.

### ¿QUÉ ES DOCKER-COMPOSE?

Es una herramienta que simplifica el uso de docker. Lo suelen llamar “recetario” porque es un simple archivo del estilo YAML que utilizaremos para definir la configuración de la/s aplicación/es en cuestión. El archivo se llama docker-compose.yml y en él se encontrarán los servicios, configuraciones como exposición de puertos y redes, volúmenes para hacer que nuestro contenidos sean persistentes entre otros. Docker Compose no se instala junto a docker ya que como dijimos es una herramienta aparte.

### ¿QUÉ ES DOCKER REGISTRY?

Como les conte anteriormente en https://hub.docker.com/ podremos encontrar imágenes de muchísimas aplicaciones, que pueden ser oficiales (creadas por las mismas empresas como wordpress, python, etc) o bien otras que crean usuarios de la comunidad.

Un docker Registry es un si se quiere REPOSITORIO donde hostear nuestras imágenes sin depender de docker hub el cual tiene sus reglas y seguramente si es una imagen que no se descargue demasiado suela perderse en el tiempo.

### ¿QUÉ ES UN VOLUMEN EN DOCKER?

Los contenedores pueden ejecutarse sin un volumen, pero ¿Se imaginan un contenedor de Nextcloud que no guarde nuestros archivos sincronizados? Claramente sería un servicio inutil.

El volumen es la forma de hacer que los datos sean persistentes luego de que el contenedor cambie de estado (Apagado, reinicio, etc).

Los volúmenes pueden ser un mapeo de carpetas (de origen de la app a origen del contenedor) o bien un simple mapeo de carpetas al estilo backup. Imaginate que tenes un contenedor con el servicio de PostgreSql sería lógico hacer un respaldo de la carpeta principal y el mismo se vería algo así:

`volumes:`

   `./postgres-data:/var/lib/postgresql/data`

Aquí distinguimos a ./postgres-data: como carpeta del host y /var/lib/postgresql/data como carpeta del contenedor. Siempre tenemos que tener en cuenta la pregunta ¿Qué es lo que quiero guardar? ¿Dónde se guardaría la aplicación original?.

## INSTALACIÓN DE DOCKER

\- - - - X

### ¿COMO INSTALAR DOCKER Y DOCKER COMPOSE PASO A PASO?

Para esta instalación estoy utilizando como host principal una maquina con ubuntu 20.04

El tutorial completo lo pueden ver en el siguiente link: https://github.com/Z4mbr4/Tutoriales/blob/main/Instalaci%C3%B3n%20de%20Docker%20sobre%20Ubuntu%2020.04.md

Van a encontrar que muchos hablan de **docker-ce** y de **docker.io** Las versiones anteriores del binario de Docker se llamaban docker o docker-engine o docker-io. 

El paquete **docker-io** sigue siendo el nombre utilizado por **Debian / Ubuntu** para la versión de Docker proporcionada en sus **repositorios oficiales**. El Paquete **docker-ce** es una versión certificada **proporcionada** directamente por **docker.com** y también se puede compilar desde la fuente.

> La razón principal para usar el nombre docker-io en la plataforma Debian / Ubuntu fue evitar un conflicto de nombres de binarios.

## CREANDO NUESTRO PRIMER CONTENEDOR

\- - - - X

La idea es muy sencilla, solo copien y ejecuten este código para ver la magia:

`sudo docker run docker/whalesay cowsay "Docker para Inciantes #Flisol2022 #Curza"`

Ahora ejecutaremos el comando:
`docker ps`
¿Ya tenemos para apreciar algun resultado?
Probemos mejor con el comando:

`docker ps -a`

Como vemos en la imagen anterior, al ejecutar el comando **docker ps** el cual nos permite ver los contenedores que se están ejecutando no lo encontramos. Ahora si buscamos los contenedores que se encuentran apagados con el comando **docker ps -a** ahí estará presente obviamente ocupando un poco de espacio en disco.

Antes de ver un gran listado de comandos disponible vamos a ver algo sencillo como borrar ese contenedor que está "detenido"

`docker rm idcontenedor`

Hasta acá tiramos un par de comandos para sacudir los dedos y ver que pasa. Ahora vamos a ir paso a paso como corresponde desde la imagen hasta nuestros servicios en distintos contenedores.

## CREANDO NUESTRA PRIMER IMAGEN

\- - - - X

![img](https://lh4.googleusercontent.com/jIvJfvL8hVUbmLT803aIV9juWvNi0IQf4uhljfnuzkg7eQEAW0j_gPRs3Li4DduuaL5CXI71YPKCwdmxvcNfhei7hFQmIvhIvC-4veofDFTJYwC23oB--kFXyWYDn2Z9aRtg2FpR)

Y por fin llegamos al punto donde vamos a crear nuestra primera imagen. 

Antes que nada tenemos que tener en cuenta que “estamos aprendiendo docker” por ende hay cosas de infraestructura que ya deberíamos conocer al menos un poco. Si la imagen que creamos es de 64 bit funcionara en una imagen de 32? y en un equipo armfh? Es importante saber que se pueden crear imágenes multiplataformas pero pasito a pasito.

Vamos a trabajar ordenados, por lo que lo primero es crear una carpeta que se llame MisImagenesDocker, dentro vamos a crear una nueva carpeta que se llame imagen1 y dentro un archivo sin extensión llamado Dockerfile

### ¿Para que me sirve crear una imagen?

Recordamos al inicio que nos preguntabamos ¿cuanto tiempo nos lleva instalar siertas herramientas? si hacemos un buen trabajo podremos contar con imagenes propias y/o recetas (por asi decirlo) que nos ayuden en el día a día. Hoy con herramientas como docker y un orquestador como Kubernetes podriamos montar 100 servidores web en escasos minutos, pero claramente no podria hacer una imagen de por ejemplo mysql sino se la idiosincracia del mismo, quiere decir que, por querer hacer algo rapido luego "puedo no saber como solucionar siertos problemas"

**`Para crear una imagen necesito:**`

`**1 - Un archivo de texto plano**`

`**2 - Un poco de scripting y servicios**`

`**3 - Cafe y mucha practica`**

### Estructura del DockerFIle

Tenemos que conocer cómo es la estructura de nuestro **DOCKERFILE** ya que de ella y de lo que pongamos dentro va depender la imagen que vamos a crear.

### **Instrucciones:**

**FROM** (requerido) Aquí especificamos **la imagen de base** que vayamos a utilizar. Esta puede ser una aplicación ya funcionando o simplemente un sistema operativo a utilizar como base. Para crear algo multiplataforma debemos recordar que la imagen de base debe ser multiplataforma

**RUN** <comando> ejecuta el comando en el momento de la creación de la imagen

**CMD** <comando> (requerido) ejecuta el comando en el momento de ejecución del contenedor. 

**WORKDIR** <ruta> especifica la carpeta de trabajo dentro del contenedor. A partir del momento en que se ejecuta esta instrucción, todos los comandos siguientes se ejecutarán de forma relativa a <ruta>. Si <ruta> no existe, se creará automáticamente. Esta es una buena práctica cara a evitar conflictos de ficheros con la imagen base utilizada.

**COPY** Copia los ficheros de <origen> en <destino>. Los parámetros son relativos al contexto de construcción (la carpeta donde se encuentra Dockerfile):

<origen> se encuentra en el sistema de archivos fuera del contenedor

<destino> se encuentra en el sistema de archivos dentro del contenedor

**EXPOSE** <puerto> especifica el o los puertos que el contenedor habilitará para conexión

**VOLUME** <carpeta> indica una carpeta cuyos datos persistirán en el sistema de archivos del host (muy utilizado al momento de crear contenedores)

**HEALTHCHECK** Indica el comando a utilizar para el healthcheck del contenedor (estado de salud)

En el interior del dockerfile vamos a introducir:

```yaml
FROM debian
MAINTAINER Luis Zambrana "patagonialibre@protonmail.com"
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
EXPOSE 80
ADD ["index.html","/var/www/html/"]
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

```

Explicamos un poquito el archivo:

**FROM debian**

Debian será nuestra base inicial. Si no contamos con la imagen en nuestra máquina lo va a tener que bajar del Docker Registry, o sea: https://hub.docker.com/_/debian

**MAINTAINER Luis Zambrana "**[**patagonialibre@protonmail.com**](mailto:patagonialibre@protonmail.com)**"**

Es solo el dato de la persona que crea y mantiene la imagen.

**RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/***

Es un comando que ejecutaremos en nuestro servidor con debian. Básicamente actualizamos los repos, instalamos apache, borramos cache de paquetes y la lista de paquetes descargada.

**ENV APACHE_RUN_USER www-data**

**ENV APACHE_RUN_GROUP www-data**

**ENV APACHE_LOG_DIR /var/log/apache2**

Creamos variables de entorno que en este caso no se utilizan pero luego seguramente se necesiten.

**EXPOSE 80**

Exponemos el puerto 80. Podríamos exponer el 443 o una gran lista de los puertos que quisiéramos exponer.

**ADD ["index.html","/var/www/html/"]**

Vamos a agregar un archivo index.html (que luego creamos en un minutito) desde la carpeta donde esta guardado el Dockerfile hasta la carpeta de la imagen /var/www/html con el objetivo de que como es un servidor apache levante nuestro index.html

**ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]**

