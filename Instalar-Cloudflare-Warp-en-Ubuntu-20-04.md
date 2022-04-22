---
author: 'Luis Alberto Zambrana'
slug: 'Instalar_Cloudflare_Warp_en_Ubuntu_20-04'
title: 'Instalar Cloudflare Warp en Ubuntu 20-04'
---

# Navegación segura con Cloudflare Warp

Cloudflare es una de las redes más grandes que opera en Internet. Los  usuarios utilizan sus soluciones con el fin de aumentar la  seguridad y el rendimiento de sus sitios web y servicios.

Dentro de los servicios tienen mitigación de ataques DDOS para tus web, entre un monton de cosas más que tal vez proximamente realize un tutorial pero en este momento la idea es hablarles de WARP

Warp establece una conexión VPN en el dispositivo para enrutar el  tráfico a través de los servidores Cloudflare; esto oculta la dirección  IP del dispositivo y puede mejorar el rendimiento y asegurar el tráfico  de DNS e Internet. Cloudflare sugiere que los usuarios de Warp+ ven una  mejora media del 30% en el rendimiento al cargar sitios web.

Ahora, si lo queremos instalar en los telefonos con android solo basta ir al playstore, buscarlo, instalar, y luego activar, con lo cual asi de facil empezas a navegar a traves de cloudflare.

En ubuntu la instalación es de la siguiente manera:

- Agregamos el repo

```
echo 'deb [arch=amd64  signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg]  https://pkg.cloudflareclient.com/ focal main' | sudo tee  /etc/apt/sources.list.d/cloudflare-client.list
```

- Actualizamos:
```
sudo apt update
```

- Instalamos:
```
sudo apt install cloudflare-warp
```

En el menu, en este caso en ubuntu 20-04 podremos buscar la aplicación y aparecerá cerquita de la hora.

Lo activamos y charan! ya podremos disfrutar de nuestro servicio de internet mucho más seguro estes donde estes!

Les recomiendo el plan 0 pesos o FREE de cloudflare, muy muy bueno y hasta 50 clientes.