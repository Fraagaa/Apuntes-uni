# Introducción a TCP/IP
La familia de procolos TCP/IP permite a ordenadores de todos los tamaños, de diferentes fabricantes, ejecutando sistemas operativos diferentes, comunicarse entre ellos. Es un proyecto financiado por el gobierno amerciano para investigar en redes de comunicación de paquetes, **ARPANET**.
## Niveles y protocolos
Para interconectar dos o más redes, y crear una interred o internet, necesito un **router**: Hardware y software de propósito específico que permite conectar diferentes tipos de redes físicas. Implementa los niveles de red, enlace y físico.
Los niveles de transporte y aplicación utilizan protocolos **extremo a extremo**.
El nivel de red utiliza un protocolo **salto a salto** que se utiliza en los sistemas finales y en cada router.
Hay otros tipos de dispositivos de interconexión de LANs: concentradores, puentes y conmutadores.
- Niveles físico y de enlace.
- Se basan en las direeciones del nivel de enlace, las direeciones MAC
**Concentrador, hub**: repite cada trama recibida por sus puertos de entrada por el resto de puertos de salida.
- Sólo implementa nivel físico.
- La red se comporta como si fuese un único segmento LAN.
**Conmutador, switch**: permite conectar distintos equipos para formar una LAN.
- Una trama de entrada es enviada, conmutada, sólo al equipo destino, usando la dirección MAC.
- Permite obtener una mayor velocidad efectiva.
**Puente, bridge**: permite conectar distintos segmentos LAN. Una trama de entrada sólo es reenviada al segmento destino si es necesario.
- Puede realizar conversiones entre distintos protocolos de enlace.
- Realiza comprobación de errores.
## Direcciones IP
Los dispositivos en Internet se identifican mediante **direcciones IP**. Cada **interfaz** debe tener una dirección IP, en relidad IPv4. Una dirección IP consta de 32 bits y se representa cada byte en decimal, separado por un punto. Por ejemplo 192.168.1.100
### Clases de IP

| Clase | Bits iniciales | Identificador       | Rango de Direcciones        |
|-------|----------------|---------------------|-----------------------------|
| A     | 0              | Id. red / Id. host  | 1.0.0.0 a 127.255.255.255   |
| B     | 10             | Id. red / Id. host  | 128.0.0.0 a 191.255.255.255 |
| C     | 110            | Id. red / Id. host  | 192.0.0.0 a 223.255.255.255 |
| D     | 1110           | Dirección de multicast | 224.0.0.0 a 239.255.255.255 |
| E     | 1111           | Reservado           | 240.0.0.0 a 247.255.255.255 |
Para cada una de estas IPs, indica de qué clase es, su identificador de red y su identificador de host:
10.25.100.10        86.23.187.240
172.16.25.30        145.76.231.48
192.168.10.26       193.144.57.60
### IPs públicas y privadas
Direcciones **IP públicas**: identifican unívocamente un dispositivo en Internet. Por ejemplo, 193.144.60.171
Direcciones **IP privadas**: exclusivamente para uso interno. Necesitamos algo que convierta las IPs privadas en públicas para comunicarse en Internet. Network Address Translation.
- Clase A: **10.0.0.0**, 1 red
- Clase B: **172.16.0.0 - 172.31.0.0**, 16 redes
- Clase C: **192.168.0.0 - 192.168.255.0**, 256 redes
### Loopback
Se reserva la dirección IP tipo A 127.X.X.X para la interfaz de loopback. Normlamente será la dirección **127.0.0.1** y el nombre asociado es **localhost**. Pretende ser una interfaz a la que se envían los paquetes dirigidos a la misma máquina. Un datagrama cuyo destino sea la propia máquina no debe llegar físicamente a la red.
Utilización de la interfaz de loopback:
- Todo paquete dirigido a la dirección de loopback aparece directamente como una entrada en la capa de red.
- Todo datagrama enviado a una dirección IP de la máquina se envía a la interfaz de loopback.
- Los datagramas de broadcast y multicast se copian a la interfaz de loopback y se envían a la red.
## Direcciones IP
En IPv4 se definen tres tipos de direcciones:
- **unicast**: una dirección IP, una única máquina
- **broadcast**: una dirección IP, todas las máquinas en una red.
- **multicast**: una dirección IP, un grupo de máquinas denominado grupo multicast.
Broadcasting y multicasting realizan una comunicación desde una máquina a un conjunto. Sólo es válido con UDP.
Direcciones de broadcast: 255.255.255.255 e <Id. red> .255
- El paquete es recibido por todas las máquinas interesadas o no en el paquete. No se puede descartar hasta que la capa de transporte.
- Produce una fuerte sobrecarga cuando el broadcast es muy acusado. Suele estar filtrado en la mayoría de las máquinas.
Este problema lo soluciona el multicast ya que para recibir estos paquetes la máquina tiene que estar suscrita a un grupo multicast. Si no está suscrito, los paquetes son directamente descartados por la interfaz de red.
Algunas direcciones multicast (netstat -gn. Suele estar filtrado en la mayoría de las máquinas.
Este problema lo soluciona el multicast ya que para recibir estos paquetes la máquina tiene que estar suscrita a un grupo multicast. Si no está suscrito, los paquetes son directamente descartados por la interfaz de red.
Algunas direcciones multicast (netstat -gn):
- 224.0.0.1 = todas las máquinas de la red que soportan multicast.
- 224.0.0.2 = todos los routers de la red.
### DNS
Nosotros usamos nombres para identificar las máquinas, pero TCP/IP usan direccipnes IP. **Domain Name System, DNS**, es el sistema que realiza la correspondencia. Importancia del DNS:
- Base de datos distribuida que almacena información sobre nombres de máquinas y direcciones IP.
- También proporciona de los servidores de correo electronico.
- Cada organización gestiona su propia base de datos, su propio servidor DNS.
- Los clientes consultan a su servidor DNS cada vez que necesitan averiguar una dirección IP.
### Números de puerto
Una dirección IP identifica un ordenador pero, de todas las aplicaciones que hay en un ordenador, ¿Cómo sé con cuál me tengo que comunicar? Con los **números de puerto**.
Un número de puerto es un número de 16 bits, 1 - 65535. TCP y UDP tienen puertos independientes. Los **servidores** usan puertos fijos y conocidos, **well known ports**, del 1 al 1023. Los **clientes** usan puertos **efímeros**: para cada servicio usan un puerto libre cualquiera y al finalizar el servicio se deja libre.
