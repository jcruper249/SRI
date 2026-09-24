# Actividad 0.5
Lo primero que tenemos que hacer es iniciar el servidor web python, si no lo tenemos instalado habrá que instalarlo

![Ejecucion_Server_web_python](/img/Ejecucion-servidor-web-python.png)

Lo siguiente que hay que hacer es crear un archivo ``index.html`` que pondremos en el directorio en el que tenemos en marcha el servidor el cual seria el del usuario esto hará que el servidor sirva de manera predeterminada el archivo ``index.html``

![Codigo_pagina_web](/img/codigo-pagina.png)
![Meter index.html en capeta del usuario](/img/Poner-pagina-en-la-carpeta-del-usuario.png)

Por ultimo vamos a entrar en ``http://localhost:8000`` esto nos dará acceso a nuestro servidor python y como se puede ver en la imagen de abajo nos esta dando ``index.html`` directamente.
![index.html](/img/Servidor-con-index.png)

## python -m http.server 8000
Para ejecutar este servidor primero hay que descargarlo desde github [Server python](https://github.com/freelamb/simple_http_server) una vez te descargues el zip lo extraes y lo pones en la carpeta usuario o lo dejas donde esta teniendo en cuenta que si lo dejas donde esta te vas a tener que mover en el cmd hasta el directorio en la que este el archivo ``simple_http_server.py``.
Una vez estemos en el directorio en la que este el archivo ponemos el comando para que arranque que esta indicado justo debajo y lo arrancamos, el comando debe ejecutarse donde este el archivo si no dara error
```
$ python simple_http_server.py 8000
```
![run_python](/img/Ejecucion-python-github-simple.png)
Después de arrancarlo comprobamos en el navegador, si no esta en el mismo directorio que index.html habrá que mover index.html a la carpeta o copiarlo y así es como se veria
![index.html](/img/Servidor-con-index.png).

## 
Para el siguiente servidor python tendremos que copiar el código de este github [Codigo](https://gist.github.com/kabinpokhrel/6fd1275603e9d5f1e284be717cbd1bff)
Una vez copiado lo pondremos en el cmd después de ejecutar Python y así es como tendría que quedar:
![Codigo_python](/img/Server_Por_codigo.png)
**Ejemplo codigo**
```python
import http.server as httpserver
import socketserver

def main(port=None):
	if port is None:
		port = 8000
	handler = httpserver.SimpleHTTPRequestHandler
	try:
		httpd = socketserver.TCPServer(("", port), handler)
		print("serving at port", port)
		httpd.serve_forever()
	except OSError:
		print("Given PORT:{} is unavailable.Try running with diffrent PORT Number!".format(port))

if __name__ == '__main__':
	main()
```
Asi es como se ve en el navegador
![index.html](/img/Servidor-con-index.png).
