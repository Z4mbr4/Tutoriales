---
author: 'Luis Alberto Zambrana'
slug: 'Seguridad_minima_para_nuestro_Servidor'
title: 'Seguridad minima para nuestro Servidor'
---

# Seguridad minima para nuestro Servidor

Vamos a mostrar como con un "par" de cosas podemos dale seguridad a nuestro server, en este caso uso un ubuntu 22.04 pero es igual para 20.04 y otros similares.

## Generar SSHKey:

El sshkey lo generamos en el cliente obviamente, no en nuestro servidor. La idea es no ingresar poniendo claves etc etc sino generar un sshkey y pasarlo a nuestro server. 

```
ssh-keygen
```

Basicamente nos va a pedir un lugar  que por defecto es nuestro usuario y la carpeta **/home/usuario/.ssh/** luego te va a pedir una clave, y trata que sea lo suficientemente fuerte!

Una vez que se creo la clave vamos a ejecutar el siguiente comando:

```
ssh-copy-id usuario@servidor
```

Te va a pedir la clave del usuario (que deberia tener permisos para esta tarea) y luego de un instante terminara.

A partir de este momento cuanto hagas ssh usuario@servidor entrará como por un tubo y sin poner la contraseña delante de personas que esten "mirando" justo el teclado.

## Cambiar puerto ssh

Por defecto el puerto es el 22 y la verdad que obviamente no es seguro. Para cambiarlo vamos a editar el archivo:

```
nano /etc/ssh/sshd_config
```

Buscamos un **#Port 22** y lo cambiamos por **Port 2424**

Fijense que no solo cambie el numero sino tambien quitamos el numeral. 

Del mismo archivo y SOLO SI YA GENERASTE Y ENVIASTE EL SSHKEY tambien podes prohibir el ingreso de root por ssh, para lo cual lo unico que tenes que hacer es comentar la linea:  **PermitRootLogin yes** de este modo: **#PermitRootLogin yes**

<u>Si no generaste el sshkey y no lo enviaste no lo hagas por que no vas a poder ingresar a no ser que tengas un usuario preparado para tal motivo, tene cuidado!</u>

Luego reiniciamos el servicio ssh que en ubuntu es:

```
service ssh restart
```

Ahora para ingresar haremos ssh usuario@servidor -p2424

## Fail2ban

Por último vamos a tirale una onda a nuestro servidor con Fail2ban que es una aplicación escrita en Python para la prevención de intrusos en un sistema, que actúa penalizando o bloqueando las  conexiones remotas que intentan accesos por fuerza bruta. 

Lo instalamos con:

```
sudo apt install fail2ban
```

Luego vamos a editar el archivo jail.conf que se encuentra en /etc/fail2ban:

```
sudo nano /etc/fail2ban/jail.conf
```

En este archivo encontraremos diversas opciones de configuración  interesantes. Un usuario avanzado puede aprovechar muchas de las  características de este programa, pero lo más básico es administrar los  intentos de login por SSH al servidor.

En la sección **DEFAULT** encontramos la configuración global de las  opciones. Allí veremos diversas variables que definir como las  siguientes:

- **bantime:** es el tiempo que una IP será baneada, expresado en segundos.
- **maxretry**: es el número máximo de reintentos de login que podrán realizarse antes de que la IP sea baneada.
- **ignoreip**: una lista de IPs separadas por espacios que serían ignoradas por fail2ban.

Por más #CulturaLibre para todos y todas!
