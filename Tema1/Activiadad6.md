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


