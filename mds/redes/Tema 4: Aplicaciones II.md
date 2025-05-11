# Tema 4: Protocolos de nivel de aplicación II
## DNS: Introducción
Domain Name System
Nosotros utilizamos nombres para las maquinas, pero TCP/IP se comunican utilizando direcciones IP. DNS es el sistema que se encarga de hacer la correspondencia entre nombres de máquinas y direcciones IP, también proporciona información de los servidores de correo.
Modelo cliente-servidor: Se implementa sobre UDP, aunque también puede utilizar TCP. Antes del DNS, se usaba un fichero de hosts.
### Cliente DNS
DNS también es el protocolo que permite a los clientes y servidores comunicarse.
**Cliente DNS**: cada máquina tiene un cliente DNS, cada vez que cualquier aplicación necesita averiguar una dirección IP, le pasa la pregunta al cliente DNS, el cliente DNS le envía la conuslta a su servidor DNS, cuando obtiene la respuesta, se la pasa a la aplicación.
### Servidor DNS
Cada red tiene un servidor DNS.
El servidor recibe consultas DNS de clientes, averigua la dirección IP y la envía a los clientes.
¿Cómo averigua mi servidor DNS una dirección IP?
El DNS es una base de datos distribuida, no hay un servidor que conozca todos los nombres y sus IPS, Hay múltiples servidores DNS organizados jerárquicamente.
### Espacio de nombres DNS
- Estructura de nombres jerárquica en forma de arbol:
Top-Level Domains, TLDs.
.com, .net, .es, .uk
Second-Level Domains, SLDs
.ibm, .google, .udc, .usc
Third-Level Domains
.tic, .fic
- Nombre de dominio: www.fic.udc.es
    - No se distinguen mayúsculas y minusculas.
- FQDNs (fully qualified domain names): nombre de dominio completo, formalmente acabado en ".", si está imcompleto se "rellena" con nuestro dominio.
### Servidores de nombres
Hay servidores DNS en cada nivel de la jerarquía de los nombres de dominio:
- **Distribuir** la carga entre los servidores de nombres.
- **Delegación** de la administración de los servidores de nombres.
Servidores **raíz**
- Existen 13 servidores raíz (A-M), replicados por seguridad y fiabilidad.
- Conocen a todos los TLDs y delegan en ellos.
Servidores TLD
- Cada dominio de primer nivel tiene su servidor TLD asociado.
- Delegan en servidores de 2º nivel la gestión de sub-dominios.
Servidores DNS inferiores:
- Conocen a todos los equipos de su dominio.
- Conocen a los servidores DNS raíz.
- Ante una consulta, si no conoce una IP, le pregunta a un servidor raíz.
### Funcionamiento DNS
Consultas recursivas:
El servidor DNS hará todo el trabajo necesario para devolver la respuesta completa a la petición. Puede implicar múltiples transacciones del servidor con otros servidores DNS. No es obligatorio que los servidores DNS soporten este tipo de consultas.
Consultas iterativas:
Si el servidor DNS tiene la respuesta, entonces la devulve. En caso contrario, devolverá la información útil, pero no hará peticiones adicionales a otros servidores DNS. Los servidores raíz y TLD son no recursivos.
### Caché DNS
Para reducir los mensajes DNS se utilizan cachés, cada par dirección IP - nombre que se resuelve se almacena en la caché, esta tiene un tiempo de vida, TTL, de varios días. También se almacenan las peticiones incorrectas.
**Respuesta autoritativa**: responde directamnte el servidor DNS que "conoce" la información.
### Servidor DNS de Forwarding
Servidores DNS de Forwarding:
No es responsable de ninguna zona, no almacena información en disco. Sólo reenvía las consultas a otros servidores DNS. Almacena las respuestas en caché, implica una respuesta rápida para consultas frecuentes.
Un router inalámbrico, lo normal es que incorpore un servidor DNS de forwarding:
- Reenvía las consultas al servidor DNS de mi ISP.
- Las consultas en caché se resulven en mi LAN, evito accesios a la red de ISP.
## P2P
Los protocolos anteriores se basaban en el modelo cliente-servidor: el servidor proporciona un servicio y el cliente cosnumeese servicio.
El modelo P2P, peer to peer, está compuesto por pares (peers) que realizan ambas funciones: consumir y proporcionar un servicio.
Se basa en equipos de usuarios
- No son propiedad de un proveedor de servicio.
- Conectados intermitentemente
- Proporcionan acceso a una parte de sus recursos.
Ventajas:
- Compartición de recursos.
- Gran tolerancia a fallos.
Inconvenientes:
- Seguridad: acceso a los recursos de un equipo, aumento de las medidas de seguridad en los últimos años.
- Gran uso de ancho de banda, a veces restringidos por los ISPs

