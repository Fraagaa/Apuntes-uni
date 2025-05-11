# ICMP
El protocolo IP no cuenta con mecanismos para obtener información de diagnóstico, por lo que se utiliza ICMP para cubrir esa necesidad.
ICMP se encarga de comunicar mensajes de error y otras condiciones que requieren atención. Existen dos tipos principales de mensajes: los de error y los de consulta.
Los mensajes ICMP se transmiten dentro de datagramas IP, tal como se define en el RFC 792.
Entre los mensajes ICMP más utilizados se encuentran los siguientes:
- La petición y respuesta de eco, que se usa comúnmente en el comando ping
- Los mensajes de destino inalcanzable, que incluyen:
- Puerto inalcanzable, usado principalmente por UDP cuando el destino no tiene un proceso escuchando en el puerto especificado
- Máquina o red inalcanzable, que es generado por un router cuando no puede entregar o reenviar un datagrama IP
También se utilizan mensajes como Redirect, Fragmentación requerida y Tiempo excedido
En la arquitectura de red, ICMP opera a nivel del protocolo IP, siendo invocado tanto por TCP como por UDP desde la capa de transporte, y apoyado por Ethernet en la capa de enlace
## Ping
Packet InterNet Groper. Herramienta de diagnóstico que comprueba si un nodo de la red es alcanzable. El cliente envía ICMP echo request, el servidor responde con ICMP echo reply. El formato de los mensajes ICMP echo request y reply contiene un identificador, en UNIX es  el identificador del proceso, y un número de secuncia, inicalmente 0, y se incrementa con cada echo request.
Existen variedad de implementaciones.
## Traceroute
Problemas del ping con registro de ruta:
- Falta de espacio en la cabecera IP
    - Registro de ruta: máximo 9 routers
    - Timestamp: máximo 4 routers, o 9 timestamps sin direcciones IP.
- No todos los routers soportan la opción de registro de ruta.
- No hay control sobre los relojes de los routers.
Solución: **traceroute**: herramienta de diagnóstico que permite ver la ruta que sigue un datagrama hacia un destino. Se basa en datagramas UDP, el campo TTL de la cabecera IP y los mensajes de error ICMP Puerto inalcanzable y Tiempo excedido.
- Solo requiere que el protocolo UDP esté operativo en el destinatario.
- Cuando un router al decrementar el campo TTL obtiene 0, genera un mensaje de error ICMP Tiempo excedido.
- Cuando UDP recibe un datagrama para un puerto vacío genera un mensaje de error ICMP Puerto inalcanzable.
## Fragmentación IP
El nivel de enlace de la red impone un límite superior al tamaño de la trama que se puede transmitir: **Maximum Transmisions Unit, MUT**.
- Ethernet, 1500 bytes.
- Token Ring, 4440 bytes.
Cuando el nivel de red (IP) recibe un datagrama, identifica la interfaz de red a utilizar y la interroga sobre su MTU:
- Compara la respuesta con la longitud del datagrama.
- Se hace fragmentación si la longitud del datagrama es mayor que el MTU.
El **reensamblado** de datagramas IP fragmentados se produce cuando los fragmentos alcanzan el **destino final**:
- Lo hace IP en el destino.
- La fragmentación es transparente al nivel de transporte.
En la cabecera IP se almacena la información relacionada con la fragmentación IP.
**Identificación**: valor único para cada datagrama IP transmitido. Todos los fragmentos de un datagrama contienen el mismo valor.
Flags:
- El primer bit está reservado.
- Bit **Don't Fragment, DF**: a 1 si se prohíbe fragmentar el datagrama IP.
- Bit **More Fragments, MF**: a 1 si hay más fragmentos a continuación. Se pone a 0 en el último fragmento.
**Offset de fragmento**: desplazamiento en **múltiplos de 8 bytes** del fragmento desde el origen del datagrama original.
**Longitud total**: se cambia la longitud total del datagrama por longitud total del fragmento.
El tamaño de cada fragmento debe ser múltiplo de 8 bytes, excepto el último fragmento, por el campo offset de fragmento
### Error ICMP
Error ICMP Unreacheble Error (Fragmentación Required)
- Mensaje de error utilizado por un router cuando tiene que fragmentar un datagrama IP pero tiene el flag DF activado.
- Incluye el MTU de la red que provocó el error y una copia de la cabecera del mensaje descartado.
### Path MTU Discovery
Este mensaje de error es utilizado en un mecanismo denominado **Path MTU discovery** que permite averiguar el MTU mínimo durante una comunicación y reducir la fragmentación IP.
- Solo se implementa en el host origen.
- Path MTU: MTU mínimo en cualquier red en el camino entre dos hosts.
Funcionamiento del Path MTU discovery:
1. Se habilita el bit DF en los datagramas enviados.
2. Si algún router en el camino necesita fragmentar, generará el mensaje ICMP Fragmentación requerida.
3. Si se recibe un mensaje ICMP Fragmentación requerida con el nuevo MTU:
- Si eran datos TPC, TPC debe reducir el tamaño del segmento, en base al nuevo MTU, y retransmitir.
- Sino, IP fragmenta los datagramas en base al nuevo MTU.
4. Como las rutas cambian dinámicamente, se puede probar un MTU mayor pasado cierto intervalo.

