# Portal Express
Perfil de instalación de Drupal 9 para un sitio general de una intendencia.

Instalar Drupal desde cero (1) o clonar repositorio con instalacion (2)

	(1) Iniciar proyecto ddev --> ddev config --project-type=drupal9 --docroot=web --create-docroot
		ddev start
		ddev ssh
		composer create drupal/recommended-project
		composer require drush/drush

	(2) git clone REPOSITORIO
		ddev config --project-type=drupal9 --docroot=web --create-docroot
		ddev start
		ddev ssh

Clonar el perfil de instalacion en la carpeta web/profile/contrib/isa

	git clone https://gitlab.isaltda.com.uy/portal/isa-portal-express.git /contrib/isa

Dentro del composer.json de la instalacion de drupal:

	Copiar los "require" del composer.json del perfil

Cambiar en el fichero composer.json
	
	"minimum-stability": "stable",
por

	"minimum-stability": "dev",


Agregar al fichero composer.json en la sección "extra" la linea
	
    "patches-file": "web/profiles/contrib/isa/composer.patches.json"

Ejemplo:
```json
	...
	"config": {	"sort-packages": true	},
	"extra": {
		"patches-file": "web/profiles/contrib/isa/composer.patches.json",
	...
```
 Ejecutar el comando

	composer install

 Levantar el sitio usando drush

	drush si



