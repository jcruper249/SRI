# Activiadad6 | VIRTUAL HOSTS
## Paso Uno - Crear la Estructura del Directorio
El primer paso que necesitamos es crear la estructura de directorios que mantendrán la información de nuestro sitio.
Esto hay que crearlo en ```/var/www``` ya que aquí es donde apache busca el contenido para mostrar, vamos a crear 2 directorios y dentro de esos directorios vamos a crear un archivo llamado ```public_html``` este archivo contendrá toda la información del sitio.
Para crear los directorios con el fichero tendremos que poner el siguiente comando en la terminal:
```bash
sudo mkdir -p /var/www/ejemplo.com/public_html
sudo mkdir -p /var/www/pruebas.com/public_html
```
![VH1](/img/Tema1/Act6/VH1.png)

## Paso Dos - Otorgar Permisos
Ahora hay que cambiar los permisos de los directorios que acabamos de crear para que el usuario regular pueda modificarlo ya que el propietario es root, para ello pondremos los siguientes comandos en la terminal:
```bash
sudo chown -R $USER:$USER /var/www/ejemplo.com/public_html
sudo chown -R $USER:$USER /var/www/pruebas.com/public_html
```

![VH2](/img/Tema1/Act6/VH2.png)

La variable ```$USER``` tomará el valor del usuario con el cual actualmente estás identificado. Al hacer esto, nuestro usuario regular ahora es propietario de los directorios public_html donde se almacenará nuestro contenido.

Tambien hay que modificar los permisos de ```/var/www``` para asegurarnos de que el permiso de lectura pueda ser aplicado correctamente
```bash
sudo chmod -R 755 /var/www
```

![VH3](/img/Tema1/Act6/VH3.png)

## Paso Tres — Crear una Página de Prueba para cada Virtual Host




