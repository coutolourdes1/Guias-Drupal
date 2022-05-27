#  Kint

Kint es una herramienta que nos permite depurar el codigo en los hook y plantillas Twig, permitiendonos tener total conocimiento de las variables 
que se reciben en los templates.

# Instalación de Kint

Para instalar kint necesitamos previamente instalar el módulo devel, para ello se debe ejecutar:

    composer require drupal/devel
    
    drush en devel devel-generate
    
Posterior a esto instalamos el kint para depurar usando devel:

    composer require kint-php/kint
    
Esto ya nos permite en las plantillas twig o archivos hooks ejecutar la funcion:

    kint($variables)  ---> En caso de hooks
    
    {{ kint($variables) }}  ---> En caso de twig
   
# Alternativa y posibles errores de visualización

Una alternativa, no tan potente para kint es la funcion dump:

    dump($variables)  ---> En caso de hooks
    
    {{ dump($variables) }}  ---> En caso de twig
    
Un posible error de visualización puede ocurrir si contamos con kint como depurador por defecto en devel, lo ideal es que no sea asi.

# Mostrar suggestions y archivos twigs

Al trabajar con kint o dump es muy util conocer sobre que plantilla debemos lanzarlo para ver las variables que se reciben en ella, para ello activaremos
el visualizador de plantillas, siguiendo los pasos siguientes:

    En la carpeta /sites deberemos agregar (o modificar) el archivo development.services.yml, quedandonos de la siguiente manera:
	
    ```json
        parameters:
          http.response.debug_cacheability_headers: true
          twig.config:
            debug: true
            auto_reload: true
            cache: false
        services:
          cache.backend.null:
            class: Drupal\Core\Cache\NullBackendFactory
     ```
     
    Esto nos activa la depuración twig.

