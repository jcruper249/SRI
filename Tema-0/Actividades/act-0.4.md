# Actividad 0.4
cURL es una herramienta de línea de comandos y una biblioteca que sirve para transferir datos hacia o desde un servidor utilizando una gran variedad de protocolos (como HTTP, HTTPS, FTP, etc.). Permite simular peticiones web, descargar archivos, probar o consumir APIs, y ver códigos fuente o respuestas en formatos como JSON o XML.

Vamos a probar 5 comando de cURL, El primero permite obtener la pagina principal de la web o servidor al que apuntemos:

**Comando**

```
curl https://www.google.com/
```

![curl1](/img/Curl_1.png)

El segundo comando conecta al servidor FTP público de RedIRIS y lista el contenido del directorio raíz directamente en la pantalla

```
curl ftp://ftp.rediris.es
```

![curl2](/img/curl_2.png)

El tercero nos permite obtener la pagina web atreves del puerto 8000, Este se queda pillado pensando hasta que rechace la conexión

**Comando**

```
curl http://www.example.com:8000/
```

![curl3](/img/curl_3.png)

El cuarto comando sirve obtener una página web y guárdarla en un archivo local, hay que hacer un archivo local para guarda el archivo remoto (si no se especifica ninguna parte del nombre del archivo en la URL, esto falla)

```
curl -O https://www.example.com/index.html
```

![curl4](/img/curl_4.png)

El quinto comando sigue redirecciones automáticamente

```
curl -L https://dominio.com
```

![curl5](/img/curl_5.png)
