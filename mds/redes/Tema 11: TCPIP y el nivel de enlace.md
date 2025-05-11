# Direcciones MAC
En internet, cada host tiene una dirección lógica IP. En las redes físicas, cada host tiene una dirección hardware, física o MAC. En la mayoría de redes LAN, una dirección MAC son 48 bits. por ejemplo, 1A:23:F9:CD:06:9B. Los primeros 24 bits son el Organizationally Unique Identifier, OUI, y los últimos 24 bits son asignados por el fabricante. La dirección de una tarjeta de red es única a nivel mundial. Al transmitir una trama, se indica la dirección MAC de destino.
En una red de broadcast: Todos los nodos reciben la trama. La interfaz comprueba si la dirección de destino coincide con la suya, de coincidir se envía al nivel de red, por el contrario, se descarta.
Dirección MAC de broadcast: FF:FF:FF:FF:FF:FF
## ARP
¿Cómo se convierte/mapea una dirección lógica en una dirección MAC? Es decir, ¿cómo se convierte una dirección IP de 32 bits en una dirección Ethernet de 48 bits?
Adress Resoluton Protocol, ARP, proporciona la correspondencia entre direcciones IP y direcciones MAC.
ARP proporciona correspondencia dinámica, no concierne al usuario ni al administrador de la red, entre distracciones IP y direcciones MAC usadas por distintas tecnologías de red.
### ARP caché
El broadcast de los ARP Request es costoso ya que todos los receptores tienen que procesar este paquete.
El caché ARP mantiene las conversaciones entre direcciones hardware. En un mensaje ARP Request, si la IP del emisor ya está en la cache, se actualiza con la dirección HW del emisor. El tiempo normal de vida es de 20 minutos.
