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

    ddev drush dcer block_content 1 --folder=profiles/contrib/XXX/modules/custom/nombre_modulo/content
    
Donde block_content representa el tipo de entidad a guardar, 1 el ID, y el --folder es la carpeta donde se alojará la configuración.
En este caso usaremos como nombre_modulo, test.
    
drush dcer a diferencia de drush dce exporta todas las configuraciones y sus referencias

# Creación y ejecución del módulo.

Una vez tenemos en este caso la carpeta test/content lo que nos queda es crear el .info para que el módulo pueda funcionar y ser instalado.
Dentro de test.info.yml deberiamos tener una estructura como esta:

```json
	    name: 'module name'
	    type: module
	    description: 'module description'
	    core_version_requirement: '^8.9 || ^9'
	    package: 'name'
```        
Adicional a esto, es necesario agregar una configuracion mas, la cual sera default-content:

```json
	    name: 'module name'
	    type: module
	    description: 'module description'
	    core_version_requirement: '^8.9 || ^9'
	    package: 'name'

	    default_content:
		block_content:
		    - e0af1c39-d8b1-4d22-8371-f0a41f065447
```   
Donde block_content lleva dentro de si todas las configuraciones que se encuentran en la carpeta test/content/block_content, "e0af1c39-d8b1-4d22-8371-f0a41f065447" es en este caso el nombre del archivo que el módulo generó para este bloque.
En caso de tener otros tipos de entidades deben estar a la altura de block_content, por ejemplo, node.

Posterior a esto restaría instalar y probar que todo funcione.

# Otros tipos de entidades posibles

    $ drush dce node <node id>
    $ drush dce taxonomy_term <taxonomy term id> 
    $ drush dce file <file id> 
    $ drush dce media <media id>
    $ drush dce menu_link_content <menu link id>
    $ drush dce block_content <block id>
