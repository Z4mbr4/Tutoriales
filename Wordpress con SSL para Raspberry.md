---
author: 'Luis Alberto Zambrana'
slug: 'Wordpress_con_SSL_en_Raspberry_Pi'
title: 'Wordpress con SSL en Raspberry Pi'
---
# Wordpress con SSL en Raspberry Pi

1 - Crear archivo docker-compose.yml con este contenido:


```
version: "3"

services:
  db:
    image: yobasystems/alpine-mariadb
    ports:
      - "3306:3306"
    volumes:
      - ./mariadb:/var/lib/mysql
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: huevo2020!
      MYSQL_USER: huevo2020
      MYSQL_PASSWORD: huevo2020!
      MYSQL_DATABASE: basewp

  wplz:
    depends_on:
      - db
    image: wordpress:latest
    expose:
      - "80"
      - "443"
    restart: unless-stopped
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: huevo2020
      WORDPRESS_DB_PASSWORD: huevo2020!
      WORDPRESS_DB_NAME: basewp
      VIRTUAL_HOST: culturalibre.ar
      LETSENCRYPT_HOST: culturalibre.ar
      LETSENCRYPT_EMAIL: lazambrana@gmail.com
    volumes:
      - ./wordpress:/var/www/html
 
  jwilder-proxy:
    image: budry/jwilder-nginx-proxy-arm
    ports:
      - "80:80"
      - "443:443"
    environment:
      DEFAULT_HOST: patagoniait.ar
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
      - certs:/etc/nginx/certs:ro
      - vhostd:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
    labels:
      - "com.github.jrcs.letsencrypt_nginx_proxy_companion.nginx_proxy"
    restart: unless-stopped
      
  letsencrypt:
    image: jrcs/letsencrypt-nginx-proxy-companion:stable
    restart: always
    environment:
      - NGINX_PROXY_CONTAINER=jwilder-proxy
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - certs:/etc/nginx/certs:rw
      - vhostd:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
    depends_on:
      - "jwilder-proxy"

volumes:
 certs:
 vhostd:
 html:
 db-data:
 db-data2:      
```

2 - revisen todas las variables para poner un dominio que funcione, y un mail valido.

3 - ejecutar el comando:

```
docker-compose up -d
```

