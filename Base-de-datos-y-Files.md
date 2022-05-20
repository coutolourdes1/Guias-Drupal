# Actualizacion base de datos y files

Crear a la altura de web la carpeta backups, dentro prod:

    mkdir backups
    cd backups
    mkdir prod

Dentro de la carpeta prod se guardará la base de datos con el nombre db.sql

Además, se puede en esta carpeta colocar los files.

En caso de tener archivos para instalar ejecutar los siguientes comandosÑ

    rm -rf web/sites/default/files/* 
    (Esto eliminará los archivos actuales de la carpeta files)

    tar -xf backups/prod/files.tar.gz -C ./
    (Esto descomprimirá el los archivos en backups/prod y los colocará en web/sites/default/files/)
  
Para actualizar la base de datos primero:

    drush sql-drop --yes
    (esto elimina las tablas de la base de datos actual)

    drush sqlq --file=/var/www/html/backups/prod/db.sql
    (esto coloca la base de datos que colocamos en prod)

    drush cr
    (Limpia el cache)

# Si existen updates...

    leer updates base de datos.md


# Backup de la base de datos y files

En la carpeta creada al principio se utilizará una carpeta local donde se colocará el backup de la base de datos y files

    drush cex --yes
    (Esto nos exportará las configuraciones que tenemos en el sitio a la carpeta web/sites/default/files/)
  
    DIR=backups/local/$(date '+%d-%m-%Y__%H-%M-%S')
    mkdir -p $DIR
    (Con estos comandos creamos la carpeta local/(carpeta con fecha y hora del backup))

    drush sql:dump > ${DIR}/db.sql
    (Nos crea un dump de la base de datos (una copia) y la manda a la carpeta creada bajo el nombre de db)

    tar -zcf ${DIR}/files.tar.gz web/sites/default/files
    (Esto comprime los files que existan en el sitio y los manda a la carpeta en el files.tar.gz)

