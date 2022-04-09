---
author: 'Luis Alberto Zambrana'
slug: 'Pihole_sobre_docker_ en_raspberry'
title: 'Pihole sobre docker en raspberry'
---
# Pihole sobre docker en raspberry

1 - Crear archivo docker-compose.yml con este contenido:


```
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "1080:80/tcp"
      - "10443:443/tcp"
    environment:
      TZ: 'America/Argentina/Buenos_Aires'
      WEBPASSWORD: '@s4ls1pu3d3s2020'
    volumes:
      - './etc-pihole/:/etc/pihole/'
      - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

2 - revisen todos los puertos que se utilizan por que los podes estar utilizando para otra cosa

3 - ejecutar el comando:

```
docker-compose up -d
```

4 - Ingresa mediante un navegador al puerto que le pusiste y ya estas para configurar. Es muy sencillo!
