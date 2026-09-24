# Actividad 0.1
## ¿Quién, dónde y cuándo se crea el primer servidor web?
Lo Creo Tim Berners-Lee en 1990 y lanzado públicamente el 
## ¿Qué es pila de protocolos usados por http?
Es el conjunto de capas de comunicación de la arquitectura TCP/IP que permite que los datos viajen desde un navegador hasta un servidor web
## ¿Componentes de una URL?
    * El esquema o protocolos
    * Server domain name
    * puerto
    * path to resource w/name & extension
    * Query string (Opcional)
    * Fragment ID (Opcional)
## ¿Pasos en la recuperación de una página web mediante HTTP?
Mediante Peticiones y respuestas HTTP
##Diferencia entre páginas dinámicas y estáticas
La diferencia es que las dinamicas estan hablando constantemente con el servidor para actualizar sus datos según las solicitudes del cliente(PHP por ejemplo) y las dinamicas son paginas de solo texto (HTML,CSS,JS)
## ¿Cómo usar telnet para acceder a un servidor web?
(solución en actividad 0.3)
### Request. Métodos principales

* GET: Solicita un recurso específico del servidor (como una página HTML o imagen). No altera el estado del servidor.
* POST: Envía datos al servidor para que los procese (por ejemplo, un formulario de registro o inicio de sesión).
* HEAD: Pide la misma respuesta que un GET, pero sin el cuerpo (solo las cabeceras). Útil para verificar si un archivo existe o ha cambiado.
* PUT: Reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición.
* DELETE: Borra el recurso especificado en el servidor.
### Response. Códigos
* 2xx (Éxito)
  * 200 OK: La solicitud ha tenido éxito y el servidor devuelve el recurso.
* 3xx (Redirección)
  * 301 Moved Permanently: El recurso se ha mudado permanentemente a una nueva URL.
	* 302 Found: El recurso se encuentra temporalmente en otra URL.
* 4xx (Errores del Cliente)
  * 400 Bad Request: El servidor no entiende la petición (por ejemplo, sintaxis incorrecta).
	* 401 Unauthorized: Se requiere autenticación para acceder al recurso.
	* 403 Forbidden: El cliente no tiene permisos para ver ese contenido.
	* 404 Not Found: El servidor no puede encontrar el recurso solicitado.
* 5xx (Errores del Servidor)
  * 500 Internal Server Error: El servidor encontró una condición inesperada que le impide cumplir la solicitud.
	* 503 Service Unavailable: El servidor no está listo para manejar la petición (por mantenimiento o sobrecarga).


### Content type. Tipos principales
La cabecera Content-Type le indica al navegador (o al cliente Telnet) qué tipo de datos está enviando el servidor para que sepa cómo renderizarlos. Utiliza la estructura tipo/subtipo (MIME types).
* Texto plano y código
  * text/html: Páginas web estructuradas en HTML.
	* text/plain: Texto sin formato.
	* text/css: Hojas de estilo para el diseño web.
	* application/javascript: Archivos de código JavaScript.
* Aplicaciones y datos
  * application/json: Formato de intercambio de datos ligero, muy usado en APIs.
	* application/xml: Datos estructurados en formato XML.
	* application/pdf: Documentos PDF electrónicos.
* Imágenes y Multimedia
  * image/jpeg / image/png / image/gif: Formatos de imagen estándar.
	* audio/mpeg: Archivos de audio (MP3).
	* video/mp4: Archivos de video digital.
