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




