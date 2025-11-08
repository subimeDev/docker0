 # En esta parte explicaremos todo lo que hicimos 

## Lo primero  que hicimos es crear una carpeta donde estará el proyecto 
## despues dentro de la carpeta hicimos

 docker run -d --name wp -p 8082:80 wordpress:6-apache

 ## con esto creamos un contenedor wordpress para poder llegar y usarse, expuesto en el puerto 8082 pero sin base de datos ya que esa la usaremos en el otro 

 ## creamos el docker compose  y dentro de el

Servicio db (MariaDB)

Este servicio es la base de datos que va a usar WordPress.

image: mariadb:11 → imagen oficial de MariaDB.

Variables de entorno:

MYSQL_ROOT_PASSWORD → contraseña del usuario root.

MYSQL_DATABASE → base de datos que se crea automáticamente.

MYSQL_USER y MYSQL_PASSWORD → usuario especial que WordPress va a usar.

volumes: → usamos wp_db para que la base de datos quede guardada y no se borre.

restart: unless-stopped → se reinicia solo si se apaga.

Servicio wordpress

Este servicio levanta WordPress conectado a la base de datos.

image: wordpress:6-apache → imagen de WordPress + Apache.

depends_on: db → espera a que la base esté funcionando.

ports: "8082:80" → el sitio se abre en http://localhost:8082.

Variables de entorno:

WORDPRESS_DB_HOST → le dice a WordPress dónde está MariaDB.

WORDPRESS_DB_NAME, USER y PASSWORD → deben coincidir con las del servicio db.

volumes: → wp_files guarda los archivos del sitio (plugins, temas, imágenes…).

Volúmenes

wp_db → guarda la base de datos.

wp_files → guarda los archivos de WordPress


# luego si no hay ningun error,  hacemos 
docker compose up -d 


