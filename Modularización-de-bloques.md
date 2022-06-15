#  Modularización de bloques áóíúé

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

