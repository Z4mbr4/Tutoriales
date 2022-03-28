---
author: 'Luis Alberto Zambrana'
slug: 'Instalación_de_Docker'
title: 'Instalación de Docker sobre Ubuntu 20.04'
---

# Instalación de Docker sobre Ubuntu 20.04

```
sudo apt update && sudo apt upgrade
sudo apt install curl python3-pip apt-transport-https ca-certificates software-properties-common
sudo apt install docker.io
sudo usermod -aG docker tuusuario
sudo systemctl enable --now docker
docker --version
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

# Instalación de Docker sobre RaspberryPi

```
sudo apt update && sudo apt upgrade
sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common python3 python3-pip

sudo curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -

sudo echo "deb [arch=armhf] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
     $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list
    
sudo apt update
sudo apt install docker-ce

sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker piousuario

sudo pip3 -v install docker-compose

```

# Instalar Docker sobre Windows 10

Lo primero que necesitamos es tener Windows 10 actualizado a la versión  2004 o superior. Podemos comprobar esto pulsando Windows + X y  seleccionando Sistema en el menú que se abre. Aquí encontraremos toda la información sobre nuestro sistema operativo.

Importante: 

- si vamos a usar windows como entorno de trabajo deberíamos usar hyperv en vez de virtualbox ya que es recomendable para el wsl2 y debido a que traen conflicto los dos hipervisores.
- El primer paso será actualizar windows 10 llevandolo a la version 2004 o superior para lo cual les dejo un link: https://support.microsoft.com/es-es/windows/obtener-la-%C3%BAltima-windows-actualizaci%C3%B3n-7d20e88c-0568-483a-37bc-c3885390d212#WindowsVersion=Windows_10

Ahora instalamos la característica opcional del Windows Subsystem for  Linux (WSL) y a plataforma de maquina virtual. Esta instalación nos dará acceso a la versión de WSL 1. Desde la  PowerShell, ejecutamos el siguiente comando como administrador (o sea, buscar powershell y antes de abrir pones boton derecho ejecutar como administrador)

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
dism.exe /online /enable-feature /featurename:Hyper-V /all /norestart
```

Una vez instalada las dos características reiniciamos la maquina. 

Luego pasamos a la version 2

```
wsl --set-default-version 2
```

Ahora descargamos DOCKER Desktop bajando el ejecutable de la web. Les recomiendo la lectura de: https://docs.docker.com/desktop/windows/install/

Una vez descargado se instala con siguiente siguiente siguiente. Finalizada la instalación reinician la maquina.

Ahora vamos a armar un ubuntu 20.04 rapidamente para lo cual desde el store de microsoft (no hace falta tener cuenta) vamos a ingresar a https://www.microsoft.com/store/apps/9n6svws3rx71

Le damos descargar e instalar!

Una vez que concluya nos va a pedir un usuario y contraseña y luego repetir la contraseña.

Para acceder vamos a la terminal y escribimos wsl y se debería abrir una consola de de Ubuntu 20.04

Mientras tantos nos vamos a docker desktop y en configuración tildamos la opcion como se ve en la siguiente imagen:

![](C:\Users\luiz\Documents\MEGA\BlogZeta\TodoEnMD\dockerdesktopactivarwls2.png)

Reiniciamos la maquina y si los pasos fueron los que se hicieron hasta aca nuestra ballena va a estar al lado de la hora del reloj sin ningún problema.

Si te pide actualizar el kernel es por que no tenias la ultima version de windows o bien instalaste alguna maquina virtual con wsl1 y al actualizar a 2 siempre queda el kilombo.

https://www.tenforums.com/tutorials/164301-how-update-wsl-wsl-2-windows-10-a.html

Algo que use para solucionar el problema del kernel fue:

```
# Descargar y actualizar  wsl2
& curl.exe -f -o wsl_update_x64.msi "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi"
powershell -Command "Start-Process msiexec -Wait -ArgumentList '/a ""wsl_update_x64.msi"" /quiet /qn TARGETDIR=""C:\Temp""'"
Copy-Item -Path "$env:TEMP\System32\lxss" -Destination "C:\System32" -Recurse

# Instalar todo
powershell -Command "Start-Process msiexec -Wait -ArgumentList '/i','wsl_update_x64.msi','/quiet','/qn'"

```

