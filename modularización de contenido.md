# Modularización de contenido

Una práctica muy buena para manejar contenidos es empaquetarlos en modulos los cuales podemos controlar.
    
    Leer updates base de datos.md
    
Si vamos a modularizar un contenido que no hayamos creado aun, una buena idea es primero volcar las configuraciones que tenemos en el sitio, de esta forma por consola solo se reportaran las configuraciones que pertenezcan al contenido que creemos, para volcar y recuperar las configuraciones usamos:

    drush cex
    
 # Ejemplo practico
 
    Supongamos queremos crear un módulo que tenga la información del tipo de contenido Ejemplo, primero crearemos la carpeta del modulo:
    
    cd modules/custom
    mkdir NombreModuloCustom
    cd NombreModuloCustom
    
    Una vez creada la carpeta del módulo, debemos crear el archivo NombreModuloCustom.info.yml
    
    En el se guardará la información básica de nuestro módulo:
    
    ```json
        name: 'Ejemplo'
        description: 'Módulo de ejemplo'
        type: module
        core_version_requirement: '^9'
        dependencies:
          - ...
        version: 1.0.0
        package: NAME
        
    ```
    
    name: Corresponde al nombre que mostrará el módulo al buscarlo para instalar
    description: Breve descripción de que es o su funcionamiento
    type: Tipo de contenido que se alberga, module, theme, profile... en este caso module.
    core_version_requirement: Version de drupal en la que correrá el módulo.
    dependencies: Dependencias necesarias para el correcto funcionamiento del módulo, 
    pueden pertenecer al core, en ese caso se llaman _"drupal:NombreModule"_ o 
    pertenecer a otro modulo custom, en ese caso "ModuloCustom:ModuloCustom"
