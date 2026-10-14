# Activiadad2.1.md

Pon en marcha el servidor Apache y lleva a cabo los siguientes cambios en el archivo de configuración. Se recomienda leer previamente el siguiente documento:
[Enlace1](https://httpd.apache.org/docs/2.4/getting-started.html)

La distribución de los archivos de configuración puedes consultarla aquí:
[Enlace2](http://wiki.apache.org/httpd/DistrosDefaultLayout#Win32_.28Apache_httpd_2.2.29)

Si tienes problemas con Apache consulta el siguiente enlace:
[Enlace3](https://docs.bluehosting.cl/troubleshooting/servidores/guia-de-solucion-de-problemas-comunes-de-apache.html)

## Apache utilizará el puerto 81 además del 80
   Lo primero que hay que hacer es entrar en la carpeta apache2 para ello nos desplazamos a **/etc/apache2** una vez dentro de la carpeta editaremos el fichero **ports.conf** como root para ello ponemos
   ```
   $ sudo nano ports.conf
   ```
   
   Una vez dentro ponemos ``Listen 81`` dentro del fichero guardamos y salimos
   ![APACHECONF1](/)
   
   Para que los cambios surtan efecto ponemos el comando `` $sudo systemctl restart apache2``
   
## Añadir el dominio “marisma.intranet” en el fichero “hosts”
   Para añadir el dominio marisma.intranet tenemos que editar el fichero host y añadir el dominio para ello nos tenemos que colocar en el directorio **/etc** y editar el fichero **hosts**
  Tendríamos que poner los siguientes comandos:
  ```
  $ cd /etc
  $ sudo nano hosts
  ```

  Una vez dentro escribimos lo siguiente: ``127.0.0.1 marisma.intranet`` una vez escrito guardamos y probamos a entrar en el navegador
  ![APACHECONF2](/)

  Para acceder en el navegador hay que poner **http://marisma.intranet**
  ![APACHECONF3](/)

## Cambia la directiva “ServerTokens” para mostrar el nombre del producto.
  Para cambiar la directiva "ServerTokens" tenemos que entrar en el archivo de configuración ``apache2.conf`` para ello nos tenemos que colocar en **/etc/apache2** y a partir de ahí editar como root el archivo para ello ponemos el siguiente comando:
  ```
  $ cd /etc/apache2
  $ sudo nano apche2.conf
  ```
  
  Una vez dentro del archivo tendremos que poner la siguiente lineal ``ProductOnly`` esto hará que solo salga la información esencial una vez puesta reiniciamos apache y ya estaría aplicada la configuración
  ![APACHECONF4](/)

  Aqui se muestra la prueba de que funciona
  ![APACHECONF5](/)
  
## Comprueba si se visualiza el pie de página en las páginas generadas por Apache (por ejemplo, en las páginas de error). Cambia el valor de la directiva “ServerSignature” y comprueba que funciona correctamente.

Crea un directorio “prueba” y otro directorio “prueba2”. Incluye un par de páginas en cada una de ellas.
Redirecciona el contenido de la carpeta “prueba” hacia “prueba2”
Es posible redireccionar tan solo una página en lugar de toda la carpeta. Pruébalo.
Usa la directiva userdir
Usa la directiva alias para redireccionar a una carpeta dentro del directorio de usuario.
¿Para qué sirve la directiva Options y dónde aparece. Comprueba si apache indexa los directorios. Si es así, ¿cómo lo desactivamos?
    
Nota: Para ver la respuesta http podemos usar cURL
[Enlace4](https://curl.haxx.se/docs/httpscripting.html)
[Enlace5](https://www.rosehosting.com/blog/curl-command-examples/)

Nota: Utiliza el comendo grep para localizar la ubicación de las directivas en los ficheros de configuración: https://geekland.eu/uso-del-comando-grep-en-linux-y-unix-con-ejemplos/

Nota: Si tienes que instalar un módulo en Apache utiliza a2enmod.Ejemplo “sudo a2enmod” userdir
