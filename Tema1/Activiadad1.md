# Instalar Apache
Para instalar apache tenemos que entrar en la terminal de una maquina linux y poner el siguiente comando
```
$ sudo apt install apache2
```

![sudo apt install](/img/Tema1/Intalacionapache1.png)

Ahora vamos a comprobar si el servidor esta activo entrando en **http://localhost** esto nos dará acceso al servidor apache local desde el navegador

![navegador_apache1](/img/Tema1/navegadorapache1.png)

Ahora vamos ha averiguar cual es la ip publica del servidor para ello tendremos que poner el siguiente comando hay que tener en cuanta que debes de conocer el nombre de tu tarjeta de red en mi caso no es eth0 como seria de costumbre por lo cual si no la sabes deberías utilizar el comando ``ifconfig`` para mirar esta información
```
$ ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```

![ippublica](/img/Tema1/verippublica.png)

# Instalar MySQL
Lo siguiente que vamos hacer es instalar MySQL para ello vamos a utilizar nuevamente el comando ``apt`` el comando completo seria el siguiente.
```
$ sudo apt install mysql-server
```

![InstalarMySQL-SERVER](/img/Tema1/instalarmysql.png)

Lo siguiente no es necesario pero si recomendable ya que son una serie de comandos de seguridad que viene preinstalada en MySQL, esto hara que se eliminen algunos ajustes y se bloqueara el acceso. El comando es el siguiente:
```
$ sudo mysql_secure_installation
```
Lo primero que nos dirá después de ejecutar el comando será una medida de seguridad parar el nivel de validación de contraseñas vamos a ponerlo en el mas bajo ya que estamos practicando aunque normalmente en entornos profesionales se utiliza el mas alto.

![nivel-valid-contra](/img/Tema1/seguridad1Mysql.png)

Y a partir de ahí la mayoría de cosas son quitar configuraciones y permisos que venían de forma predeterminada

![del-perm](/img/Tema1/del-per.png)

Ahora vamos a iniciar sesión en la consola de MySQL el comando es el siguiente:
```
$ sudo mysql
```
Esto es lo que debería salir al ejecutar el comando

![salida-del-com](/img/Tema1/ejecucion-mysql.png)

Para salir de la consola MySQL ponemos el comando ``exit`` y nos sacaria.

# Instalar PHP
Para instalar PHP tenemos que entrar en la terminal y poner el comando:
```
$ sudo apt install php libapache2-mod-php php-mysq
```
Esto nos instalara el PHP de apache y MySQL

![Instalar-PHP](/img/Tema1/instalarPHP.png)

Una vez terminado ejecutaremos el comando ``php -v`` para ver la versión de php que tenemos

![Versión-PHP](/img/Tema1/phpversion.png)

# Crear un host virtual para su sitio web

Vamos a crear un host virtual para el domino llamado ``your_domain`` para ello primero vamos a crear la carpeta para el dominio para ello crearemos una estructura de directorio dentro de ``/var/www`` para el sitio your_domain y dejaremos ``/var/www/html`` establecido como directorio predeterminado que se presentará si una solicitud de cliente no coincide con ningún otro sitio.
Para crear el directorio /var/www/your_domain pondremos el siguiente comando:

```
$ sudo mkdir /var/www/your_domain
```
![crear carpeta de dominio](/img/Tema1/CrearVH1.png)

Ahora tenemos que cambiar la propiedad de el directorio que acabamos de crear ya que actualmente es de root a nuestro usuario para poder editarlo.
Para ello utilizaremos el siguiente comando:

```
$ sudo chown -R $USER:$USER /var/www/your_domain
```
Como se puede ver en la imagen de abajo el propietario a cambiado a nuestro usuario:
![Cambio de propietario](/img/Tema1/CrearVH2.png)

Lo siguiente que vamos a hacer es abrir un nuevo archivo de configuración en el directorio ``sites-available`` de Apache usando el editor de línea de comandos que queramos. En este caso, utilizaremos ``nano``:

```
$ sudo nano /etc/apache2/sites-available/your_domain.conf
```

Y ahora tenemos que poner la configuración basica la cual seria la siguente
```
<VirtualHost *:80>
    ServerName your_domain
    ServerAlias www.your_domain
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/your_domain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Con esta configuración de VirtualHost, le indicamos a Apache que proporcione your_domain usando /var/www/your_domain como directorio root web.

![configuración basica](/img/Tema1/CrearVH3.png)

Ahora, vamos a usar ``a2ensite`` para habilitar el nuevo host virtual:

```
$ sudo a2ensite your_domain
```

![Habilitar virtualhost](/img/Tema1/CrearVH4.png)

Ahora vamos a deshabilitar el sitio web por defecto de apache para que no de conflicto con el hostvirtual que hemos creado esto es conveniente cuando no se usa un nombre de dominio personalizado
Comando para deshabilitar el sitio por defecto:

```
$ sudo a2dissite 000-default
```
Para asegurarse de que su archivo de configuración no contenga errores de sintaxis ejecutamos el siguiente comando:

```
$ sudo apache2ctl configtest
```
Lo siguiente es recargar apache para que los cambios surtan efecto

```
$ sudo systemctl reload apache2
```
![recarga-verifi-deshabily](/img/Tema1/CrearVH5.png)

Ahora que ya esta activo vamos ha crear un archivo index.html:

```
$ nano /var/www/your_domain/index.html
```
Y pondremos lo siguiente en el archivo:

```HTML
<h1>It works!</h1>

<p>This is the landing page of <strong>your_domain</strong>.</p>
```
Después probaremos a entrar por el navegador poniendo ``http://localhost ``

![vista-nav](/img/Tema1/CrearVH6.png)

Con la configuración predeterminada de DirectoryIndex en Apache, un archivo denominado index.html siempre tendrá prioridad sobre un archivo index.php. Esto es útil para establecer páginas de mantenimiento en aplicaciones PHP, dado que se puede crear un archivo index.html temporal que contenga un mensaje informativo para los visitantes. Como esta página tendrá precedencia sobre la página index.php, se convertirá en la página de destino de la aplicación. Una vez que el mantenimiento se completa, el archivo index.html se elimina del root de documentos, o se le cambia el nombre, para volver mostrar la página habitual de la aplicación.

Si desea cambiar este comportamiento, deberá editar el archivo /etc/apache2/mods-enabled/dir.conf y modificar el orden en el que el archivo index.php se enumera en la directiva DirectoryIndex:

```
$ sudo nano /etc/apache2/mods-enabled/dir.conf
```
```
<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

Después de guardar y cerrar el archivo, ahora recargamos apache para que los cambios surtan efecto
En el siguiente paso, crearemos una secuencia de comandos PHP para probar que PHP esté correctamente instalado y configurado en el servidor.

![dir.conf](/img/Tema1/CrearVH7.png)

# Probar el procesamiento de PHP en su servidor web
Ahora que disponemos de una ubicación personalizada para alojar los archivos y las carpetas de su sitio web, crearemos una secuencia de comandos PHP de prueba para verificar que Apache pueda gestionar solicitudes y procesar solicitudes de archivos PHP.

Creamos un archivo nuevo llamado ``info.php`` dentro de su carpeta root web personalizada:

```
$ nano /var/www/your_domain/info.php
```
Añadimos el siguiente texto:
```
<?php
phpinfo();
```
![info.php](/img/Tema1/CrearVH8.png)

Para probarlo entramos en ``http://localhost/info.php ``.
Tras comprobar la información pertinente sobre del servidor PHP a través de esa página, es recomendable que eliminar el archivo que creó, dado que contiene información confidencial sobre su entorno PHP y su servidor de Ubuntu. Puede usar rm para hacerlo
```
$ sudo rm /var/www/your_domain/info.php
```

![info.php-local](/img/Tema1/CrearVH9.png)

# Probar la conexión con la base de datos desde PHP

Ahora vamos a comprobar que php puede establecer conexión con MySQL vamos a crear una tabla de prueba con datos ficticios y realizar consultas relacionadas con su contenido con una secuencia de comandos PHP. Para poder hacerlo, debemos crear una base de datos de prueba y un nuevo usuario de MySQL debidamente configurado para acceder a ella.

La biblioteca PHP nativa de MySQL mysqlnd no admite caching_sha2_authentication, el método de autenticación predeterminado de MySQL 8. Vamos a tener que crear un usuario nuevo con el método de autenticación mysql_native_password para poder establecer conexión con la base de datos de MySQL desde PHP.

Crearemos una base de datos denominada example_database y un usuario llamado example_user, pero podemos sustituir estos nombres por valores diferentes.

Primero, establecemos conexión con la consola de MySQL usando la cuenta root:
```
$ sudo mysql
```

Para crear una base de datos nueva, ejecutamos el siguiente comando desde la consola de MySQL:

```
mysql> CREATE DATABASE example_database;
```
![probar1-mysql](/img/Tema1/Probarmysql1.png)

Ahora podemos crear un nuevo usuario y concederle privilegios completos sobre la base de datos personalizada que acaba de crear.

El siguiente comando crea un usuario nuevo llamado ``example_user``, que utiliza ``mysql_native_password`` como método de autenticación predeterminado. Definimos la contraseña de este usuario como ``password``, pero debe sustituir este valor por una contraseña segura de nuestra elección.

```
mysql> CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```
![Crearusuariomsql](/img/Tema1/Probarmysql2.png)

Ahora, debemos darle permiso a este usuario a la base de datos ``example_database``, en mi caso ``jesus_database``:

```
mysql> GRANT ALL ON jesus_database.* TO 'jesus_user'@'%';
```
![permisosusuariomsql](/img/Tema1/Probarmysql3.png)

Esto proporcionará al usuario jesus_user privilegios completos sobre la base de datos jesus_database y, al mismo tiempo, evitará que este usuario cree o modifique otras bases de datos en el servidor.

Ahora cerramos el shell:

```
mysql> exit
```
Podemos verificar si el usuario nuevo tiene los permisos adecuados al volver a iniciar sesión en la consola de MySQL, esta vez, con las credenciales de usuario personalizadas:

```
$ mysql -u jesus_user -p
```
El indicador -p en este comando, que solicitara la contraseña que se utilizo cuando se creó el usuario jesus_user. Después de iniciar sesión en la consola de MySQL, confirmamos que tengamos acceso a la base de datos jesus_database:

```
mysql> SHOW DATABASES;
```
Eso generara el siguiente resultado:
```mysql
Output
+--------------------+
| Database           |
+--------------------+
| example_database   |
| information_schema |
+--------------------+
2 rows in set (0.000 sec)
```

![permisosusuariomsql](/img/Tema1/Probarmysql4.png)

A continuación, crearemos una tabla de prueba denominada todo_list: Desde la consola de MySQL, ejecutamos la siguiente instrucción:

```
mysql> CREATE TABLE jesus_database.todo_list (
mysql>	item_id INT AUTO_INCREMENT,
mysql>	content VARCHAR(255),
mysql>	PRIMARY KEY(item_id)
mysql> );
```
Insertamos algunas filas de contenido en la tabla de prueba:

```
mysql> INSERT INTO jesus_database.todo_list (content) VALUES ("My first important item");
```
Para confirmar que los datos se guardaron correctamente en la tabla, ejecutamos lo siguiente:

```
mysql> SELECT * FROM jesus_database.todo_list;
```

Aparecera el siguiente resultado:

```mysql
Output
+---------+--------------------------+
| item_id | content                  |
+---------+--------------------------+
|       1 | My first important item  |
|       2 | My second important item |
|       3 | My third important item  |
|       4 | and this one more thing  |
+---------+--------------------------+
4 rows in set (0.000 sec)
```

![creaciondetabla](/img/Tema1/Probarmysql5.png)

Después de confirmar que haya datos válidos en la tabla de prueba, cerramos la consola de MySQL:

```
mysql> exit
```

Ahora, podremos crear una secuencia de comandos PHP que se conecte a MySQL y realice consultas relacionadas con su contenido. Vamos a crear un nuevo archivo PHP en su directorio web root personalizado. En este caso, usaremos nano:

```
$ nano /var/www/your_domain/todo_list.php
```

La siguiente secuencia de comandos PHP establece conexión con la base de datos de MySQL, realiza consultas relacionadas con el contenido de la tabla todo_list y muestra los resultados en una lista. Si hay un problema con la conexión de la base de datos, generará una excepción:

```php
<?php
$user = "jesus_user";
$password = "Miyabi_nangong1";
$database = "jesus_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```

![todo_list.php](/img/Tema1/Probarmysql6.png)

Ahora, podemos acceder a esta página en el navegador web al visitar el nombre de dominio o la dirección IP pública del sitio web seguido de /todo_list.php:

```
http://localhost/todo_list.php
```

![navegador](/img/Tema1/Probarmysql7.png)


