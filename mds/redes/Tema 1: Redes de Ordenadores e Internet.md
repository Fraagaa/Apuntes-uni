# Redes de Ordenadores e Internet
## ¿Qué es Internet?
Es una red de comunicación global que interconecta millones de redes.
- Host, routers y enlaces de comunicación.
- Protocolos TCP/IP
Es una infraestructura que proporciona servicios a las aplicaciones distribuidas.
- E-mail, Web, aplicaciones P2P, juegos, VolP, streaming de vídeo, ...
- Internet proporciona dos tipos de servicios:
    - Fiable y orientado a conexión,
    - No fiable y no orientado a conexión.
## ¿Qué es una red?
Una red de ordenadores es una red de comunicación digital que permite a sus nodos compartir recursos y comunicarse.
- Nodo: host (PC, teléfono, servidores, ...) y hardware de red (routers, switchs, ...)
Tipos de redes, cableadas o inalámbricas, según el canal de comunicación:
- Broadcast: canal de comunicación compartido. Posibilidad de múltiples destinatarios (broadcast o multicast). Redes pequeñas en general.
- Punto a punto: canales de comunicación dedicados para la comunicación entre dos máquinas.
### Tipos de redes seguún su longitud
Redes de Área Local, LAN
- Medio compartido, 10 Mbps, 100 Mbps, 1 Gbps
- Incluyen las MAN (Metropolitan Area Network)
Redes de Área Extendida, WAN
- Compuestas por circuitos de telecomunicación compartidos.
### Tipos de tecnologías de red
Comunicación de circuitos: cuando dos nodos se quieren comunicar se establece una conexión terminal a terminal.
- Los recursos (buffers, ancho de banda, ...) necesarios se reservan a lo largo del recorrido.
- La reserva se mantiene durante la sesión.
Computación de paquetes
- No hay reserva de recursos
- Los mensajes de la sesión utilizan los recursos bajo demanda, es decir, pueden tener que esperar para poder utilizar los recursos.
### Redes de conmutación de paquetes
Los mensajes originales se dividen en paquetes para su transmisión. Estos paquetes se envían a través de enlaces y routers dentro de la red. Los routers utilizan una técnica llamada almacenamiento y reenvío, lo que significa que cada router debe recibir por completo un paquete antes de poder transmitir el primer bit hacia el siguiente destino. Este proceso introduce un retardo conocido como retardo de almacenamiento y reenvío.
Cada router dispone de un búfer en sus enlaces de salida, donde se almacenan temporalmente los paquetes que esperan ser enviados. Si el enlace está ocupado transmitiendo otro paquete, los nuevos paquetes deben esperar en la cola, lo que provoca un retardo adicional conocido como retardo de cola. En caso de que la cola esté llena, el router no puede almacenar más paquetes y se produce una pérdida de paquetes, lo que obliga a descartar alguno, generalmente el último en llegar.

**Redes de datagramas:** el envío de paquetes se realiza en base a la dirección de destino.
- No se mantiene información sobre el estado de las conexiones en los routers.
**Redes de Circuito Virtual (CV):** el envío de paquetes se realiza en base al número de circuito virtual.
- Los conmutadores mantienen información del estado de las comunicaciones entrantes: interfaz de entrada - etiqueta de entrada - interfaz de salida - etiqueta de salida.
#### Tipos de retardo en las redes de conmutación de paquete
**Retardo de procesamiento**: tiempo requerido por el router para examinar la cabecera y determinar hacia donde seguir el paquete.
**Retardo de cola**: tiempo de espera para ser transmitido en le buffer de salida.
**Retardo de transmisión**: timepo para transmitir todos los bits del paquete al enlace.
**Retardo de propagación**: tiempo necesario para propagarse desde el inicio del enlace hasta el final del enlace.
### Redes de acceso y medio físico
#### El acceso a la red se divide en tres clases:
Acceso residencial, conecta sistemas terminales del hogar a la red a través de un ISP, Internet Service Protocol
- Banda ancha con fibra óptica.
- Sino, vía satélite, 4G, 5G, WiMax.
Acceso de empresa, conecta sistemas terminales de una empresa u organización a la red.
- Se utilizan LANs para conectar el sistema terminal al router.
- Ethernet para redes cableadas y WiFi para redes inalámbricas.
Acceso inalámbrico de área extensa: emplear la misma infraestructura inalámbrica de la red de telefonía móvil para enviar/recibir datos.
#### Medios de transmisión
Guiados
- Par trenzado: UDP, STP y FTP
- Cable coaxial
- Fibra óptica
No guiados
- Canales de radio terrestres
- Canales de radio satélite
## ¿Qué es un protocolo?
Toda actividad en Internet que implica a dos o más entidades remotas que se cominican está gobernada por un protocolo.
Un protocolo se puede ver como un proveedor de servicio -> Diferencia entre **Servicio y Protocolo**:
- Las entidades utilizan los protocolos para implementar el servicio que ha sido solicitado por el usuario.
- **Independencia**: podía cambiarse el protocolo sin necesidad de que lo note el usuario.
**Arquitectura de red**: conjunto de protocolos y capas que permiten la comunicación entre ordenadores.
**Interfaz**: comunicación definida por un conjunto de primitivas y servicios que ocurre entre pares de capas adyacentes.
### Arquitectura de red
Ventajas de la estructuración en nivel y protocolos:
- Un problema complejo se descompone en piezas pequeñas.
- Abstracción de los detalles de implementación.
- Compartición por multiples niveles superiores de los servicios de una capa inferior.
Inconvenientes:
- Ocultación de información y principio de layering.
- Balance entre ocupación de información y rendimiento del sistema, una capa superior puede optimizar su rendimiento conociendo el funcionamiento de la capa inferior.
# Modelo de referencia OSI
Un conjunto de protocolos es abierto si el diseño del protocolo es de dominio público y los cambios los gestiona una organización cuyos miembros y actividades están abiertos al público.
Un sistema que implementa protocolos abiertos es un sistema abierto.
International Organization for Standards, ISO, define un estándar para conectar sistemas abiertos, OSI.
Ha tenido gran influencia en el diseño de pilas de protocolos
## Nivel físico
Transmitir bits entre entidades conectadas físicamente.
Estandarización, esquema de codificación para la representación de bits, sincronización a nivel de bit.
No existe el concepto de paquete o trama.

