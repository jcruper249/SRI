# Actividad 3 - Dir
1. Crea un directorio llamado "dir1" y otro llamado "dir2"
	Lo primero que tenemos que hacer es acceder al directorio ``/var/www/html`` y después de acceder al directorio tenemos que poner el siguiente comando para crear los siguientes directorios
  ```console
  sudo mkdir /var/www/html/dir1
  sudo mkdir /var/www/html/dir2
  ```

![dir1](/)

2. Explica qué diferencia existe entre ambos y muestra su equivalencia con la directiva Require:
<Directory /var/www/example1>
Order Deny,Allow
Deny from All
Allow from 192.168.1.100
</Directory>
  **Esta niega el acceso a todos excepto a 192.168.1.100**

<Directory /var/www/example1>
Order Allow,Deny
Deny from All
Allow from 192.168.1.100
</Directory>
**Y esta niega el acceso a todos**
		
3. Para dir1
  a) Permite el acceso de las peticiones provenientes de 10.3.0.100

  b) Permite el acceso desde "marisma.intranet"

  c) Permite el acceso desde cualquier subdominio de "marisma.intranet"

  D) Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"

4. Modifica la configuración de forma que el acceso a dir1:
  a) Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"
	
5. Modifica la configuración de forma que el acceso a dir2:
  a) Se permita a "10.3.0.100/8" y no a "marisma.intranet"
