# Actividad 0.2

**Diferencias entre udp y tcp? (min 2:46 y 4:15)**
UDP:
* Tamaños de paquete pequeños
  * Encabezado UDP: 8 bytes
  * Encabezado TCP: 20 bytes
* No hay conexión que crear ni mantener
* Mayor control sobre cuándo se envían los datos
* No fiable: No verifica si el paquete llegó ni reintenta enviarlo si se pierde en el camino.
* Sin orden: Los fragmentos pueden llegar cambiados de lugar o dispersos.
* Transmisiones en vivo (streaming), llamadas de voz (VoIP) y videojuegos en línea.

TCP:
* Orientado a la conexión: Establece un diálogo previo entre el emisor y el receptor antes de enviar la información.
* Fiable: Comprueba que los datos lleguen sin errores y retransmite los paquetes perdidos.
* Ordenado: Los paquetes llegan en la secuencia correcta.
* Uso ideal: Páginas web (HTTP), correos electrónicos (SMTP) y transferencia de archivos (FTP).

**¿Qué aplicaciones usan tcp?  http, smtp, pop, imap, ssh**
  
* HTTP (Puerto 80/443): Sirve para cargar páginas web en el navegador. Requiere que cada dato llegue completo y en orden.
* SMTP (Puerto 25/587): Se usa para enviar correos electrónicos entre servidores. TCP garantiza que el mensaje llegue sin   alteraciones.
* POP / POP3 (Puerto 110/995): Permite descargar los correos electrónicos desde un servidor a tu dispositivo local.
* IMAP (Puerto 143/993): Sincroniza y accede al correo directamente en el servidor.
* SSH (Puerto 22): Permite controlar equipos de forma remota de manera segura. Necesita la estabilidad de TCP para
  mantener la sesión de comandos abierta sin cortes.

**¿Qué aplicaciones usan udp?**

Aplicaciones que priorizan la velocidad y la baja latencia por encima de la perfección o la entrega garantizada de cada paquete de datos

**¿Qué capa almacena el puerto?**

La capa 4 la de transporte

**¿Qué capa almacena la dirección IP?**

La capa 3 la de Red

**¿Qué es three-way handshake?**

Es el proceso mediante el cual dos dispositivos en una red —un ordenador y un servidor web por ejemplo— establecen una conexión segura y confiable antes de empezar a enviar datos reales usando el Protocolo de Control de Transmisión (TCP).
