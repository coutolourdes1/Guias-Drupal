#  Modularización de bloques

Los bloques son entidades de contenido, por lo cual no podemos de forma secilla guardarlas o impactarlas en una base de datos a traves de hooks_updates 
como haciamos con taxonomias, menus, etc.., las cuales son entidades de configuración.

Para esto entonces, el camino mas optimo es crear un modulo que guarde el archivo de configuración del o los bloques que querramos mantener en nuestro sitio, para ello
usaremos el módulo defaul content, el cual se instala de la sigueinte manera:

    ddev composer require drupal/default-content
    (la version estable minima del módulo puede variar)
    
    ddev drush en default-content
    
Una vez instalado podemos hacer uso de él a través de drush, de la siguiente manera:

    ddev drush dce
    
Esta es la forma en la que drush hace refencia al módulo.

#  Ejemplo con un bloque simple

Supongamos que tenemos un bloque personalizado de cualquier tipo, lo primero es ver el ID del bloque, eso lo podemos ver si editamos ese bloque, en la url deberíamos
ver algo por el estilo:

    https://name-website.ddev.site/block/1?destination=/admin/structure/block/block-content
    
Donde el número 1 representa el ID del bloque, si editáramos el siguiente bloque creado apacería un número de ID 2.

Una vez localizado el ID del bloque que queremos guardar como configuración, volvemos a nuestra consola de comandos y ejecutamos:

    ddev drush dcer block_content 1 --folder=profiles/contrib/XXX/modules/custom/test/content
    
Donde block_content representa el tipo de entidad a guardar, 1 el ID, y el --folder es la carpeta donde se alojará la configuración.
    
drush dcer a diferencia de drush dce exporta todas las configuraciones y sus referencias

# Otros tipos de entidades posibles

    $ drush dce node <node id>
    $ drush dce taxonomy_term <taxonomy term id> 
    $ drush dce file <file id> 
    $ drush dce media <media id>
    $ drush dce menu_link_content <menu link id>
    $ drush dce block_content <block id>
