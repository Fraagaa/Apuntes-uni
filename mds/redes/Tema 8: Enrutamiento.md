# Enrutamiento
## Tabla de enrutamiento
Contiene la información de la tabla de enrutamiento. Todo dispositivo conectado a Internet tiene su tabla de enrutamiento en memoria.
Cada entrada de la tabla de enrutamiento contiene la siguiente información:
- Dirección IP de **destino**: puede ser un host (host ID != 0) o una dirección de red (host ID = 0)
- **Gateaway**: dirección IP del siguiente router, en caso de ser necesario.
- **Máscara** de subred.
- **Flags**:
    - Up (U): indica que esa entrada está activada.
    - Host (H): activado si la dirección IP de destino es de un host.
    - Gateaway (G): activado si es necesario pasar por un router para llegar al destino.
- Especificación de la **interfaz** de red a la que se debe pasar el datagrama para su envío.

| Destino   | Gateway    | Máscara        | Flags | Interfaz |
|-----------|------------|----------------|-------|----------|
| 10.51.1.0 | 0.0.0.0    | 255.255.255.0  | U     | eth0     |
| 0.0.0.0   | 10.51.1.1  | 0.0.0.0        | UG    | eth0     |
## Algoritmo de enrutamiento
Algoritmo de enrutamiento: a partir de la IP de destino de un datagrama, busca la entrada correcta en la tabla para su enrutamiento.
- Establece la manera en que se busca en la tabla de enrutamiento.
- No importa el orden de las entradas en la tabla.
1. Para cada entrada de la tabla de enrutamiento, se aplica la Máscara a la IP de destino y el resultado se compara con la columna Destino. Si coinciden, la entrada es válida para ese destino.
- Si el destino está directamente conectado, Flag G desactivado, se envía directamente a la interfaz de salida.
- Si no, Flag G activado, es necesario pasar a través de un router. Se envía por la interfaz de salida indicada al router.
- En caso de empate entre varias entradas, se selecciona aquella con una máscara mayor (más unos). **Longest match prefix**.
2. Se busca en la tabla de enrutamiento una entrada "default". Si se encuentra, se envía el paquete al router indicado.
- En realidad, todas las IPs coincidirán con la entrada default.
- Pero siempre pierde el longest match prefix contra cualquier máscara.
3. Si ninguno de los pasos anteriores tiene éxito, se genera el error "Red inalcanzable". Ha sido imposible entregar el datagrama.
### Enrutamiento estático
En **enrutamiento estático, las tablas de enrutamiento se mantienen mediante intervención humana. Válido para entornos reducidos y más o menos estables.
Para las redes directamente conectadas:
- Cuando se crea una interfaz, manualmente o por DHCP, se crea automáticamente una entrada para la red o subred.
Para las rutas indirectas:
- Se definen mediante el comando route.
- Cuando se obtiene el router por defecto, manualmente o por DHCP, route add default gw 10.51.1.1
- O cualquier otra ruta. route add -net 192.16.20.0 netmask 255.255.255.0 gw 192.168.0.2
En **enrutamiento dinámico**, los routers actualizan sus tablas de enrutamiento en función de los cambios de la red o de la carga de tráfico.
### Enrutamineto CIDR
**Classless Interdomain Routing**
Las direcciones IP de clase B se están agotando, por lo que se asignan direcciones clase C a sitios con demandas de redes tipo B, lo que provoca un aumento vertiginoso en el tamaño de las tablas de enrutamiento.
CIDR, especificado en los RFC 1518 y 1519, también conocido como superredes o supernetting, ayuda a prevenir este problema, aunque se considera una solución temporal.
Las superredes consisten en agregar direcciones y se definen mediante máscaras aplicadas sobre el identificador de red. Por ejemplo, la red 194.10.160.0/20 (máscara 255.255.240.0) incluye las siguientes redes clase C: desde 194.10.160.0/24 hasta 194.10.175.0/24, lo que representa un total de 16 redes.
El valor decimal 160 equivale en binario a 1010 0000 y 175 a 1010 1111, lo que indica que las superredes agrupan múltiples redes en un solo bloque a través de una máscara más general.
A nivel visual, el identificador de red y el de host pueden dividirse en una estructura como esta:
|   Id. red   |      Id. host     |
| Superredes  |     Subredes     |
Por ejemplo, el RFC 1466 propone la siguiente división por zonas geográficas:
|       Europa        | 194.0.0.0 - 195.255.255.255 |
|    Norteamérica     | 196.0.0.0 - 197.255.255.255 |
| Centro y Sudamérica | 198.0.0.0 - 199.255.255.255 |
|   Anillo Pacífico   | 200.0.0.0 - 201.255.255.255 |
|        Otros        | 202.0.0.0 - 203.255.255.255 |
Las redes tipo C europeas serían las 194.0.0.0/7, máscara 254.0.0.0. Con una sola entrada en las tablas de enrutamiento, fera de Europa, se englobarian 131072 redes de tipo C.
**Classless**: las clases de direcciones IP, A,B o C; no se tienen en cuenta. Se utiliza la dirección completa y máscaras de 32 bits.
Enrutamiento basado en **longest match prefix**: en caso de dos entradas correctas en una tabla de enrutamiento se selecciona la máscara de "mayor longitud".

