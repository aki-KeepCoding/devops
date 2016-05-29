# Práctica DevOps

## URLs

**Práctica 1: API NODEPOP**
- Base de urls de API con DNS: **ec2-23-22-4-4.compute-1.amazonaws.com/nodepop/api/v1/**
- Base con subdominio: **projects.akixe.info/nodepop/api/v1/**
- Ejemplo de fichero estático: [ http://projects.akixe.info/nodepop/images/bici.png ](http://projects.akixe.info/nodepop/images/bici.png)

**Práctica 2: Página WEB**
- Con la IP: [23.22.4.4](http://23.22.4.4)
- Con un dominio personal: [akixe.info](http://akixe.info)


## Sobre la práctica 1

Para realizar peticiones a la API es necesario obtener un token de acceso:

Petición POST
> projects.akixe.info/nodepop/api/v1/usuarios/auth

En body x-www-form-urlencoded
- email : akixe.otegi@gmail.com
- clave : 1234


El token obtenido se deberia de adjuntar como parámetro en siguientes peticiones al API.

Ejemplo petición GET:
> projects.akixe.info/nodepop/api/v1/anuncios?token=XXXXXXXXXXXXX

*Nota*: Las url de las imágenes de los anuncios se generan en las respuestas del API son del estilo *127.0.0.1/path/al/recurso*. Claramente es un error y lo corregiré cuando tenga el resultado del módulo DevOps. Por ahora para esta práctica incluyo la url directa a los recursos estáticos tal como se indicaba en el enunciado [ (http://projects.akixe.info/nodepop/images/bici.png) ](http://projects.akixe.info/nodepop/images/bici.png).

Más info sobre el uso del API Nodepop en el Readme.md del [repo oficial de la práctica](https://github.com/aki-KeepCoding/practica_nodepop).

## Notas sobre la práctica 2

Mi idea es  usar esta instancia AWS para montar mi sitio personal y por eso he usado una plantilla de mi elección en vez de la que se proponía en el ejercicio original.

La arquitectura que quiero montar es la siguiente:
- **akixe.info**: página de portada con enlaces a diferente páginas personales (github, linkedin...) y modos de contacto.
- **blog.akixe.info**: Mi blog oficial. Todavía no operativo.
- **projects.akixe.info/_[nombre de proyecto]_**: Será como una especie de portfolio donde pretendo ir colgando distintos proyectos que me interese destacar.


Para el blog y la página de portada usaré [Jekyll](https://jekyllrb.com/), un generador de sitios estático. De hecho la página estática de la práctica 2 ha sido generada con esta herramienta y un *"theme"* descargado de [JekyllThemes.org](http://jekyllthemes.org/)

## Configuración NGINX

**sites-available/akixe.info:**

```txt
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /var/www/akixe.info;
    index index.html index.htm;

    # Make site accessible from http://localhost/
    server_name localhost;

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ =404;
        # Uncomment to enable naxsi on this location
        # include /etc/nginx/naxsi.rules
    }

}
```


**sites-available/projects.akixe.info**

```txt
server {
    listen 80;
    listen [::]:80;

    root /var/www/projects;
    index index.html index.htm;

    server_name projects.akixe.info ec2-23-22-4-4.compute-1.amazonaws.com;


    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ =404;
        # Uncomment to enable naxsi on this location
        # include /etc/nginx/naxsi.rules
    }
    location ~ ^/nodepop/(images/|stylesheets/|js/)(.*) {
        alias /var/www/projects/nodepop/public/$1/$2;
        access_log off;
        expires max;
        add_header X-Owner @akixeOtegi;
    }
    location /nodepop/ {
        proxy_pass http://127.0.0.1:3000/;
        proxy_redirect off;
    }
}
```

