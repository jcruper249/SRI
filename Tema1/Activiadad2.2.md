# Actividad 2.2 - Scripts
Primero hay que crear el script para ello nos vamos a colocar en el directorio ``/ete/apache2`` con el siguiente comando:
```
cd /etc/apache2
```
Una vez estemos en ese directorio crearemos el archivo ports.sh con el comando ``sudo nano ports.sh``
Una vez hayamos creado el archivo tendremos que poner el siguiente codigo:
```sh
#!/bin/sh
if [$# -ne 1]; then
  echo "Falta numero de puerto"
  echo "Sintaxis: ./puerto.sh num"
  echo "Ejemplo : ./puerto.sh 81"
else
    grep "Listen $1" ports.conf >> null
    if [$? -eq o]; then
        echo "Error. Existe ese numero de puerto en ports.conf"
    else
        echo "No existe ese puerto en ports.conf"
        cp ports.conf ports.bak
        echo "Listen $1" >> ports.conf
        echo "Puerto añadido"
        service apache2 restart
        echo "Apache reiniciado"

    fi

fi
```
Al ejecutar esto nos añadirá el puerto a ports.conf

![Ports1](/img/Tema1/ACT2.2/ports1.png)

Para comprobar que funciona nos metemos al navegador y entramos en la url ``localhost:82`` al poner esto deberíamos poder acceder al servidor de apache por el puerto 82
![Ports2](/img/Tema1/ACT2.2/ports2.png)

Ahora vamos a hacer el segundo este nos pide hacer un script para añadir un dominio y una ip al fichero host para ello tendremos que cambiar un poco el script anterior adaptandolo a las necesidades que tenemos.
```sh                                    
#!/bin/sh
if [$# -ne 1]; then
        echo "Faltan los datos"
        echo "Sintaxis: ./hosts.sh ip dominio"
        echo "Ejemplo : ./hosts.sh 172.0.0.1 prueba.com"
else
        grep -w "$2" /etc/hosts > /dev/null
        if [$? -eq 0]; then
                echo "Error. Existe ese dominio"
        else
                echo "No existe el host"
                cp hosts hosts.bak
                echo "$1 $2" >> hosts
                echo "Dominio añadido"
                service apache2 restart
                echo "Apache reiniciado"
        fi
fi

```
Con este script podremos añadir un host al fichero hosts

Ejecución:
![script1](/img/Tema1/ACT2.2/script1.png)

Vista una vez ya añadido:
![script2](/img/Tema1/ACT2.2/script2.png)

Para el tercer script necesitaremos hacer el siguiente script:
```sh
#!/bin/sh

if [ $# -ne 3 ]; then
        echo "Faltan parametros"
        echo "Sintaxis: ./crear_web.sh titulo cabecera mensaje"
        echo "Ejemplo: ./crear_web.sh MiWeb Bienvenidos Hola"
else
        echo "<html>" > /var/www/your_domain/index.html
        echo "<head>" >> /var/www/your_domain/index.html
        echo "<title>$1</title>" >> /var/www/your_domain/index.html
        echo "</head>" >> /var/www/your_domain/index.html
        echo "<body>" >> /var/www/your_domain/index.html
        echo "<h1>$2</h1>" >> /var/www/your_domain/index.html
        echo "<p>$3</p>" >> /var/www/your_domain/index.html
        echo "</body>" >> /var/www/your_domain/index.html
        echo "</html>" >> /var/www/your_domain/index.html

        echo "Pagina web creada correctamente"
        echo "Archivo creado: index.html"
fi
```
Con este script podremos crear una pagina web aunque bastante basica y limitada la estoy creando para el dominio your_domain que creamos anteriormente.

Ejecución:
![script3](/img/Tema1/ACT2.2/script3.png)

Vista una vez ya añadido:
![script4](/img/Tema1/ACT2.2/script4.png)

Vista del codigo:
![script5](/img/Tema1/ACT2.2/script5.png)






