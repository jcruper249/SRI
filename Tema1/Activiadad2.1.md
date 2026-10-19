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
   
![APACHECONF1](/img/Tema1/Act2/Confapache1.png)
   
   Para que los cambios surtan efecto ponemos el comando `` $sudo systemctl restart apache2``
   
## Añadir el dominio “marisma.intranet” en el fichero “hosts”
   Para añadir el dominio marisma.intranet tenemos que editar el fichero host y añadir el dominio para ello nos tenemos que colocar en el directorio **/etc** y editar el fichero **hosts**
  Tendríamos que poner los siguientes comandos:
  ```
  $ cd /etc
  $ sudo nano hosts
  ```

  Una vez dentro escribimos lo siguiente: ``127.0.0.1 marisma.intranet`` una vez escrito guardamos y probamos a entrar en el navegador
  
![APACHECONF2](/img/Tema1/Act2/Confapache2.png)

  Para acceder en el navegador hay que poner **http://marisma.intranet**
  
![APACHECONF3](/img/Tema1/Act2/Confapache3.png)

## Cambia la directiva “ServerTokens” para mostrar el nombre del producto.
  Para cambiar la directiva "ServerTokens" tenemos que entrar en el archivo de configuración ``apache2.conf`` para ello nos tenemos que colocar en **/etc/apache2** y a partir de ahí editar como root el archivo para ello ponemos el siguiente comando:
  ```
  $ cd /etc/apache2
  $ sudo nano apche2.conf
  ```
  
  Una vez dentro del archivo tendremos que poner la siguiente lineal ``ProductOnly`` esto hará que solo salga la información esencial una vez puesta reiniciamos apache y ya estaría aplicada la configuración
  
![APACHECONF4](/img/Tema1/Act2/Confapache4.png)

  Aqui se muestra la prueba de que funciona
  
![APACHECONF5](/img/Tema1/Act2/Confapache5.png)
  
## Comprueba si se visualiza el pie de página en las páginas generadas por Apache (por ejemplo, en las páginas de error). Cambia el valor de la directiva “ServerSignature” y comprueba que funciona correctamente.
   Para comprobarlo entramos en http://localhost y ponemos una URL equivocada
   Después hacemos un grep -r "ServerSignature" /etc/apache2 esto nos mostrara las coincidencias de las palabras "ServerSignature" en todos los ficheros de apache2
   
![APACHECONF6](/img/Tema1/Act2/Confapache6.png)

  Una vez comprobado eso vamos a editar el fichero apache2.conf y poner la directiva "ServerSignature OFF"
  
![APACHECONF7](/img/Tema1/Act2/Confapache7.png)
  
  Al poner la directiva si entramos en http://localhost y ponemos una URL equivocada no nos saldra el pie de pagina que generaba automaticamente
  
![APACHECONF8](/img/Tema1/Act2/Confapache8.png)


## Crea un directorio “prueba” y otro directorio “prueba2”. Incluye un par de páginas en cada una de ellas.
   Para crear un directorio hay que utilizar el comando mkdir por lo tanto vamos a poner los siguientes comandos:
   Antes de poner estos comandos exactos tendríamos que estar en el directorio /var/www/html si no hay que poner la ruta completa
   ```
   $ sudo mkdir prueba
   $ sudo mkdir prueba2
   ```

![APACHECONF9](/img/Tema1/Act2/Confapache9.png)

Despues utilizaremos el comando nano para crear archivos index.html para cada carpeta unos 2 por carpeta

![APACHECONF10](/img/Tema1/Act2/Confapache10.png)

Ahora comprobamos que todo este creado:

![APACHECONF11](/img/Tema1/Act2/Confapache11.png)


## Redirecciona el contenido de la carpeta “prueba” hacia “prueba2”
   Paso1: Poner sudo nano etc/apache2/apache2.conf
   Paso2: Añadimos al final
      ``Redirect /prueba /prueba2``
   Paso3 reiniciamos apache con `` $sudo systemctl restart apache2``
   
## Es posible redireccionar tan solo una página en lugar de toda la carpeta. Pruébalo.
   Paso1: Poner ``sudo nano etc/apache2/apache2.conf``
   
   Paso2: Redirect agregamos ``Redirect /prueba/"pagina a elegir" /prueba2/"pagina a elegir"``
## Usa la directiva userdir
Paso 1: Para hacer esto primero activamos el userdir escribiendo "sudo a2enmod userdir":
Ahora reiniciamos el servicio de apache2:

![APACHECONF8.1](/img/Tema1/Act2/Confapache8.1.png)

Paso 2: Ahora creamos el directorio con: ``mkdir /home/usuario/public_html``

![APACHECONF8.2](/img/Tema1/Act2/Confapache8.2.png)

El usuario que pongas debe de ser el tuyo propio

Paso 3: Y ahora nos hacemos un index.html en el directorio que acabamos de crear con un nano ``/home/usuario/public_html/index.html:``

![APACHECONF8.3](/img/Tema1/Act2/Confapache8.3.png)

Paso 4: Ahora para ver si está bien hacemos un sudo apachectl configtest

![APACHECONF8.4](/img/Tema1/Act2/Confapache8.4.png)

Paso 5: Procedemos a reinicar el servicio con un service apache2 restart

Paso 6: Ahora tenemos que darle permisos para poder meternos con el comando de chmod 755 /home/usuario

![APACHECONF8.5](/img/Tema1/Act2/Confapache8.5.png)



## Usa la directiva alias para redireccionar a una carpeta dentro del directorio de usuario.
## ¿Para qué sirve la directiva Options y dónde aparece. Comprueba si apache indexa los directorios. Si es así, ¿cómo lo desactivamos?
    
Nota: Para ver la respuesta http podemos usar cURL
[Enlace4](https://curl.haxx.se/docs/httpscripting.html)
[Enlace5](https://www.rosehosting.com/blog/curl-command-examples/)

Nota: Utiliza el comendo grep para localizar la ubicación de las directivas en los ficheros de configuración: https://geekland.eu/uso-del-comando-grep-en-linux-y-unix-con-ejemplos/

Nota: Si tienes que instalar un módulo en Apache utiliza a2enmod.Ejemplo “sudo a2enmod” userdir
