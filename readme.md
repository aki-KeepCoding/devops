# Práctica DevOps

## URLs

- Práctica 1: 
> [ec2-23-22-4-4.compute-1.amazonaws.com](ec2-23-22-4-4.compute-1.amazonaws.com)
> [projects.akixe.info/nodepop](projects.akixe.info/nodepop)
> Fichero estático: [ http://projects.akixe.info/nodepop/images/bici.png ](http://projects.akixe.info/nodepop/images/bici.png)

- Práctica 2:
> [23.22.4.4](23.22.4.4)
> [akixe.info](akixe.info)


## Sobre práctica 1

Para realizar peticiones a la API es necesario obtener un token de acceso:

Petición POST
> [projects.akixe.info/nodepop/api/v1/usuarios/auth]

En body x-www-form-urlencoded
- email : akixe.otegi@gmail.com
- clave : 1234


El token obtenido se deberia de adjuntar como parámetro en siguientes peticiones al API.

*Nota*: Las url de las imágenes de los anuncios se generan como *127.0.0.1/pathAlRecurso*. Claramente es un error y debería corregirlo. Por ello he incluido en la url a un fichero estático 

Más info sobre el uso del API en el Readme.md del [repo oficial de la práctica Nodepop](https://github.com/aki-KeepCoding/practica_nodepop).

## Notas sobre práctica 2

Mi idea es  usar esta instancia AWS para montar mi sitio personal y por eso he usado una plantilla de mi elección en vez de la que se proponía en el ejercicio original.

La arquitectura que quiero montar es la siguiente:
- **akixe.info**: página de portada con enlaces a diferente páginas personales (github, linkedin...) y modos de contacto.
- **blog.akixe.info**: Mi blog oficial. Todavía no operativo.
- ** projects.akixe.info/*[nombre de proyecto]* **: Será como una especie de portfolio donde pretendo ir colgando distintos proyectos que me interese destacar.


Para el blog y la página de portada usaré [Jekyll](https://jekyllrb.com/), un generador de sitios estático. De hecho la página estática de la práctica 2 ha sido generada con esta herramienta y un *"theme"* descargado de [JekyllThemes.org](http://jekyllthemes.org/)

