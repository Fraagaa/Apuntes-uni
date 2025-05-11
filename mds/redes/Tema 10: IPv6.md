# Limitaciones IPv4
Pocas direcciones, unas 4000 millones.
- Estructura de dos niveles, id de red y de host.
- Gran proliferación de redes. Crecimiento exponencial de Internet.
- Uso de TCP/IP en nuevas tecnologías. Móviles, tablets, TV...
- Múltiples IP por ordenador.
Saturación del espacio de direcciones:
- Limita el crecimiento de Internet
- Enrutamiento ineficiente. Tablas de enritamiento muy grandes en la red troncal. Tiempos de respuesta grandes.
- Uso de Network Address Translation, NAT.
Soporte inadecuado para aplicaciones con restricciones de calidad de servicio. No garantiza anchos de banda, tiempos de respuesta, seguridad.
Se requieren mecanismos de seguridad en la capa de red:
- No fue diseñado para ser seguro. IPsec.
- Seguridad en los niveles superiores. TLS.
# Características de IPv6
Espacio de direcciones ampliado y mecanismos de autoconfiguración: **Direcciones de 128 bits**, incremento en 2⁹⁶. Permite una arquitectura jerárquica de direcciones. Agregación de direcciones en el backbone. **Autoconfiguración** de los equipos. Mejora del multicast e introducción de las direcciones **anycast**.
**Simplificación** del formato de la cabecera, tamaño fijo de 40 bytes, dos direcciones IP de 16 bytes y 6 campos más. Procesamiento más rápido y barato en los routers.
Sporte mejorado de extensiones y opciones usando **Cabeceras de Extensión**.
**Seguridad** intrínseca en el núcleo del protocolo: soporta autenticación y dispone de extensiones para la integridad y confidencialidad de los datos.
Capacidad para **etiquetado de flujos**. Paquetes del mismo flujo de datos pueden ser etiquetados en origen, Calidad de Servicio, QoS.
## Cabecera IPv6
Solo se requiere una cabecera. Se definen varias cabeceras de extensión opcionales:
- Cabecera de opciones salto-a-salto.
- Cabecera de encaminamiento.
- Cabecera de fragmentación
- Cabecera de las opciones para el destino
- Cabecera de autenticación
- Cabecera Encapsulating Security Security Payload (ESP)
**Versión**, 4 bits que designan la versión del protocolo.
**Clase de tráfico**: identifica diferentes clases o prioridades de paquetes.
**Etiqueta de flujo**, 20 bits, permite diferenciar aquellos paquetes que requieren un tratamiento similar. Especialmente útil para tráfico multimedia y en tiempo real. Etiqueta de flujo + clase de tráfico: mecanismo potente de control de flujo y de asignación de prioridades diferenciadas según los tipos de servicios.
**Longitud de carga**: longitud del paquete después de la cabecera IP. En IPv4, el campo longitud incluía la longitud de la cabecera + datos. En IPv6, no se considera la cabecera IPv6, y las cabeceras de extensión se consideran parte de la carga. Máximo tamaño de carga: 2¹⁶ = 64Kbytes. IPv6 permite la definición de Jumbogramas, paquetes de más de 64KB, que solo tienen sentido si el MTU de nivel de enlace es superior a 64 KB.
**Cabecera siguiente**, 1 bit, identifica el tipo de cabecera que sigue a la cabecera IPv6. Las cabeceras deben ser procesadas en el orden riguroso en que aparecen. Las sucesivas cabeceras no son examinadas en cada nodo de la ruta, sino sólo en el nodo o nodos destino finales, excepto cuando se trata de la cabecera de opciones salto a salto.
**Límite de saltos**, 1 byte, número de saltos permitidos. Análogo al campo TTL.
**Dirección de origien**: 16 bytes
**Dirección destino**: 16 bytes: normalmente, dirección IP del destino del paquete. Puede no ser el último destinatario del paquete, si está presente la cabecera de enrutamiento.
Se eliminan 5 campos de la cabecera IPv4:
- Longitud cabecera: necesario en IPv4 al incluirse las opciones en la cabecera. Inútil en IPv6, cabecera fija de 40 bytes + cabeceras de extensiones.
- Identificación, flags y offset de fragmentación: necesarios para la fragmentación en IPv4. Si es necesaria, se realiza extremo a extremo (Path MTU discovery), utilizando la cabecera de extensión para fragmentación. **¡LOS ROUTERS NO SE FRAGMENTAN!**
- Checksum cabecera: eliminado para mejorar el rendimiento, así los routers no tienen que calcular y actualizar el checksum. Ya se realiza en el nivel de enlace, probablemente, y en el nivel de transporte. IP no es fiable.
## Direccionamiento IPv6: Notación
Se representan mediante 8 bloques de 16 bits en hexadecimal, separados por ":"
- FEDC:BA98:7653:3210:FEDC:BA98:7654:3210
- FE80:0000:0000:0000:0202:B3FF:FE1E:8329
Se pueden eliminar los ceros por la izquierda en cada bloque
- FE80:0:0:0:202:B3FF:FE1E:8329
Se eliminan bloques consecutivos de ceros utilizando el carácter "::"
- FE80::202:B3FF:FE1E:8329
Solo pueden aparecer una vez en la dirección
- CAFF:CA01:0000:0056:0000:ABCD:EF12:1234
- CAFF:CA01::56:0:ABCD:EF12:1234
- CAFF:CA01:0:56::ABCD:EF12:1234
## Direccionamiento IPv6: Tipos
Hay tres tipos de direcciones
- **Unicast**: identifica unívocamente **una** interfaz de un nodo IPv6. Un paquete dirigido a una dirección unicast se envía a la interfaz asociada a esa dirección.
- **Multicast**: identifica un grupo de interfaces IPv6. Procesado por **todos** los miembros del grupo, sustituye a las direcciones de broadcast. Prefijo **FFxx**/8.
- **Anycast**: se asgina a múltiples interfaces, típicamente en múltiples nodos. Enviado a sólo **una de esas** interfaces, normalmente la más próxima.
Las direcciones IP se asginan a interfaces, como en IPv4, cada interfaz necesita, al menos, una dirección unicast y puede tener asignadas múltiples direcciones de cualquier tipo.
**Unicast global**: 2000::/3 - rango asignable actualmente, similares a las IPv4 públicas y enrutables en Internet.
**Link-local**: FE80::/10, utilizadas en un mismo enlace local y limitada a un único enlace.
**Local única**: FC00::/7 - FDFF::/7, similares a las IPv4 privadas. Se usan para direccionamiento dentro de un sitio o entre una cantidad limitada de sitios.
**Loopback** ::1/128 y dirección sin especificar, ::/128.
## IPv6: DNS e ICMPv5
**DNS**: se requieren unos cambios para resolver las peticiones de direcciones IPv6.
- Petición DNS IPv6: AAAA
- A partir de un nombre, obtendrá la dirección IPv6 asociada.
- dig @8.8.8.8 www.udc.es AAAA
**ICMPv6** se define una nueva versión del protocolo.
- Reorganiza los tipos y códigos existentes, y define nuevos tipos.
- Incorpora funciones de Internet Group Managment Protocol, IGMP.
- Introduce el protocolo Neightbor Discovery Protocol, NDP.
- Incorpora funciones ARP.
**Autoconfiguración**: dos mecanismos
- Stateless Address Autoconfiguration, SLAAC.
- DHCPv6.
## Transición IPv4 a IPv6
IPv6 e IPv4 van a coexistir durante muchos años.
Se han definido múltiples técnicas para la transición, que sae agrupan en tres categorías:
- Pila dual: permiten a IPv4 e IPv6 coexistir en los mismos dispositivos y redes. Soporte completo de las dos versiones de los protocolos en los nodos.
- Tunneling: permiten transportar tráfico IPv6 sobre infraestructuras IPv5 existentes. El tráfico IPv6 sobre infraestructuras IPv5 existentes. El tráfico IPv6 se encapsula en paquetes IPv4.
- NAT: permiten a los nodos IPv6 puros comunicarse con los nodos IPv4 puros. Traducen una dirección IPv6 en una dirección UPv4.
Estas técnicas pueden y deben utilizarse de manera combinada.
