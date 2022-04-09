---
author: 'Luis Alberto Zambrana'
slug: 'Iniciar_RaspberryPi3_desde_USB'
title: 'Iniciar RaspberryPi3 desde USB'
---

# Iniciar RaspberryPi3 desde USB

Si contas con una raspberry pi 3 b (no provee esto en otra) y queres usar un pendrive para iniciar la raspberry los pasos  a seguir son:

### 1 - Preparar el pendrive

Este paso no lo voy a explicar por que instalar en la tarjetita o en un pendrive es lo mismo, solo traten de instalarse la ultima versión de Raspbian.

### 2 - Actualizar repositorios

```
sudo apt update && sudo apt upgrade
```

### 3 - Ejecutamos el siguiente codigo para que inicie desde usb

```
echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
```

### 4 - Reiniciamos y antes de que encienda sacamos la tarjeta

### 5 - Comprobamos:

```
vcgencmd otp_dump | grep 17:
```

> De este modo fue como realice la instalación de raspbian en mi raspberry pi desde un disco m2 conectado por usb.
