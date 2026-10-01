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
