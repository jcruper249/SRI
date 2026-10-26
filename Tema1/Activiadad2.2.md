# Actividad 2.2 - Scripts
Primero hay que crear el script para ello nos vamos a colocar en el directorio ``/ete/apache2`` con el siguiente comando:
```
cd /etc/apache2
```
Una vez estemos en ese directorio crearemos el archivo ports.sh con el comando ``sudo nano ports.sh``
Una vez hayamos creado el archivo tendremos que poner el siguiente codigo:
```
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
        echo "Listen $1" >> ports.bak
        echo "Puerto añadido"
        service apache2 restart
        echo "Apache reiniciado"

    fi

fi
```
