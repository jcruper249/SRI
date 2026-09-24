# Actividad 0.3
Para esta actividad vamos a hacer una petición a **google.com** con ``telnet``
Para ello lo primero hay que habilitar telnet para ello hay que entrar en ``Panel de control > programas > Activar o desactivar características de Windows > Telnet client``
Una vez activado nos dirigimos al ``cmd`` y ponemos el siguiente comando:
```
telnet www.google.com 80
```
![Comando conexión](/img/comando-conexion-telnet.png)

Esto nos conectara para podre hacer la petición, el comando tendremos que introducirlo sin ver lo que escribimos pero hay que escribir el siguiente comando:
```
GET / HTTP/1.1
```
![Introducir comando](/img/Introducir-comando.png)

Por ultimo le daremos enter dos veces y nos respondera
![Respuesta](/img/Respuesta-telnet.png)
