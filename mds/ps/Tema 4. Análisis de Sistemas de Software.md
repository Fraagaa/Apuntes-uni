# Análisis de Sistemas Software
## Objetivos del análisis
- Especificar las funciones del software
- Especificar la información que se maneja.
- Especificar las interfaces con otros elementos del sistema.
- Establecer restricciones que debe cumplir el software.
## Resultados del análisis
El análisis ha de plasmar los requisitos del usuario en modelos del sistema, estos modelos dependerán del enfoque seguido (estructurado o objetual).
## Modelos de análisis
### ¿Por qué es necesario hacer modelos?
Principalmente por las siguientes 3 razones:
- Permiten concentrarse en las propiedades importantes del sistema.
- Favorecen la comunicación con el usuario.
- Permiten verificar que el analista ha comprendido el problema / entorno a abordar.

### ¿Qué aportan los modelos?
Entre sus aportaciones destacan:
- Reflejar lo que requiere el usuario del sistema; normalmente de forma gráfica.
- Establecer la base para la creación de un diseño del software.
- Definir un modelo contra el que validar una vez construido el software.

# Análisis Estructurado
## Origen
- Crisis del software.
- Aparecen los primeros lenguajes estructurados.
- Aparecen técnicas de análisis y diseño estructurado.
## Productos a obtener
El análisis proporciona modelos del sistema derivados de los requisitos del usuario:
- Modelos de Datos (E/R)
- Modelos de Procesos (DFD)
- Diccionario de Datos (DD)
- Especificación de Procesos (EP)
Estos modelos se obtienen a partir de las Técnicas de Análisis.
## Objetivos
- Dejar constancia de los límites del sistema considerado.
- Construir un modelo lógico de procesos del sistema basándose en explosiones por nivel.
- Reflejar los procesos que transforman la información.
- Simplificar la complejidad del sistema y su compresión.
- Facilitar el mantenimiento del sistema
## Conceptos
Entidad Externa:
- Refleja una interfaz entre el sistema considerado y su entorno.
- Son entes ajenos al sistema considerado (personas, unidades organizativas, sistemas o cualquier otro elemento que no forme parte del sistema).
- Aportan o reciben información desde el punto de vista del sistema tratado.
Proceso:
- Refleja una actividad que transforma datos de entrada en datos de salida.
- Sólo es lugar de transformación y no es origen ni final de datos.
Almacén de datos:
- Representa un depósito de información en el sistema. Es un contenedor de paquetes de información cuyo nombre lo suele identificar.
- Se emplea si es necesario por los requisitos o si los procesos que lo manejan actúan con diferente temporalidad.
- No puede crear, destruir ni transformar datos. Sólo los almacena estáticamente.
Flujo de datos:
- Transportan la información desde/hasta los otros componentes de un DFD (procesos, almacenes y entidades externas) estableciendo la comunicación entre ellos.
- Siempre tendrán un proceso como origen y/o destino.
- Pueden transportar datos (elementos lógicos) o materiales (elementos físicos).
- Si están claros y/o empleamos el DD, se pueden consolidar flujos por claridad.
- El mismo contenido puede tener diferentes significados en diferentes partes del sistema.
- Tipos:
    - Divergentes: el flujo fluye por diferentes caminos.
    - Convergentes: se combinan flujos para formar uno de mayor complejidad.
## Aplicación
Un sistema puede llegar a tener numerosos procesos, almacenes, flujos y entidades externas.
Por ello, el DFD es necesario organizarlo en niveles:
- TOP-DOWN
- BOTTOM-UP
- MIDDLE-UP
La aproximación más común es TOP-DOWN, ya que facilita la aproximación y compresión del sistema no sólo por el usuario, sino también por el analista.
Lo que se obtiene es una jerarquía de niveles de explosión: Diagrama de Contexto, Diagrama de Sistema, Nivel 2, Nivel 3...
El primer nivel (nivel 0 o Diagrama de Contexto), mostrando:
- Las interfaces de éste con las entidades externas.
- Los almacenes externos (si los hubiera).
El segundo nivel (Diagrama de Sistema) consiste en tantos procesos (burbujas) como subsistemas (funciones más importantes del sistema), por lo tanto, representa una visión a alto nivel del sistema global.
Los siguientes niveles de explosión refinan/explican/detallan, si hiciese falta, los procesos identificados en el nivel anterior.
<br>
No todas las partes del sistema deben tener el mismo nivel de explosión; es decir, la "altura del árbol de explosión" no tiene que ser homogénea.
Si la especificación de un proceso primitivo (burbuja de último nivel) no puede hacerse en una sola página, generalmente indicará la necesidad de explosionarlo.
Un nivel de DFD no debería contener más de media docena de procesos (burbujas) en un caso general. Regla genérica: 6±1, que si no se cumple puede indicar la necesidad de un nivel intermedio.
Los almacenes se muestran por primera vez en el nivel más alto donde actúan como interfaz entre dos o más procesos.
Los niveles deben ser necesariamente consistentes entre sí; esto es, deben estar balanceados: Principio de Conservación de Flujo.
Los flujos de datos de salida y entrada de una burbuja (proceso) en un nivel dado deben corresponderse con los que salen y entran en el DFD que refleja la explosión de ese proceso (siguiente nivel).
## Características de un buen DFD
- ¿Hay consistencia entre niveles? Principio de conservación de flujo.
- ¿Faltan procesos en el DFD obtenido?
- ¿Faltan flujos de datos que un proceso requiere para "hacer su trabajo"?
- ¿Sobran flujos de datos que para el proceso no son necesarios?
- ¿Hay redundancias en el DFD obtenido?
- ¿Hay cruces que dificultan la legibilidad del DFD?
- Por último, no deben reflejarse "subsistemas" que sólo se vayan a emplear una vez; esto es, al poner en marcha el sistema. Esto será objeto de otro sistema.
## Temporalidad
Un DFD es una red de procesos asíncronos que se comunican; esto es, no se especifica temporalidad.
En un DFD no se refleja o modela ninguna secuencia de ejecución ni alternativas o bifurcaciones.
Tan solo la ausencia o existencia de información puede implícitamente establecer una secuencia entre procesos.
## Recomendaciones
- Evitar la complejidad, un DFD debería caber cómodamente en un DIN A4 apaisado.
- Escoger nombres significativos para todos los elementos: entidades, procesos, almacenes y flujos.
- Numerar correctamente los procesos: así se muestra la jerarquía de explosión.
- El DFD ha de ser consistente.
## Consistencia
Evitar sumideros infinitos o agujeros negros; no puede haber procesos que tengan flujos de entrada pero no de salida.
Evitar procesos de "generación espontánea", generalmente no son correctos los procesos que tienen salidas pero no entradas.
Evitar flujos y procesos no etiquetados; permite que uno no se pierda al explosionar y asegurarse de que las cosas son coherentes y razonables.
Evitar almacenes de "sólo lectura" o "sólo escritura"; el único caso en que es posible almacenes con sólo entradas o sólo salidas es el de los almacenes externos.
# Análisis Estructurado
## Notación
=       está compuesto de<br>
\+      y<br>
()      optativo<br>
{}      iteración (0 o más veces) Se puede poner límite inferior, superior o ambos.<br>
[]      seleccionar una de varias alternativas. A escoger sólo una.<br>
|       separa opciones alternativas<br>
**      comentario<br>
@       identificador (campo clave) para un almacén.<br>
Alias   Se referencia en el DD para que sea completo y se referencia al nombre "oficial" del dato: computador = \*alias de cliente\*. Sólo si los usuarios no se ponen de acuerdo en un solo nombre. Mejor no usar alias.
## Definición de un dato
Para definir por completo un dato, se debe incluir:
- El significado del dato dentro del contexto de la aplicación considerada (normalmente se ofrece como comentario).
- La composición del dato, si se compone de partes elementales con significado.
- Los valores que puede tomar el dato, si es un dato elemental que no se puede descomponer más.
## Balanceo del DFD y DD
Cada flujo y almacén de datos del DFD debe estar incluido en DD.
Cada dato y almacén del DD deben estar en alguna parte del DFD.
Cada burbuja del DFD tiene que estar asociada con un DFD de nivel inferior o en una EP, pero no con ambos.
Cada EP debe tener una burbuja de nivel inferior asociada en el DFD.
Las entradas y salidas deben de coincidir en la EP y en el DFD.
Cada referencia de un dato en la EP tiene que cumplir una de las siguientes reglas:
- Coincidir con el nombre de un flujo o almacén de datos conectado a la burbuja descrita por la EP.
- Es un término local, definido explícitamente en la EP.
- Aparece como componente en una entrada del DD para un flujo o almacén de datos conectado a la burbuja.
Cada entrada de DD tiene que tener una referencia en una EP, un DFD o en el propio DD.
El E/R debe ser consistente con el DFD:
- Cada almacén del DFD debe corresponderse con una entidad, una relación del E/R o una combinación de entidades y relaciones.
- Análogamente, toda entidad y relación del E/R tiene que tener su reflejo en el DFD
- Los nombres de entidades y relaciones en el E/R deben coincidir con los nombres de los almacenes de datos en el DFD.
El E/R debe ser consistente con las EP:
- Las EP deben crear y eliminar instancias de cada entidad y relación que aparece en el E/R.
- Algún proceso del DFD tiene que usar o leer los valores de cada dato.
En general, las entidades se nombran en singula y los almacenes en plural.
Todos los atributos de una entidad aparecerán en el DD.
# Análisis Estructurado
## Pasos recomendados
1. Obtener el conocimiento del entorno:
- Breve descripción iniciañ deñ entorno, preferiblemente escrita por el usuario. Inicialmente llegarán unas pocas páginas
- Mantener entrevistas estructuradas con el usuario / grupo de usuarios.
- Revisar/Refinar las entrevistas hasta que no existan puntos conflictivos.
- Recoger los requisitos por escrito en un documento.
- Obtener el consenso con respecto al documento elaborado.
2. Obtener los modelos de análisis:
- Obtención en paralelo de modelos de procesos, modelos de datos, diccionario de datos para recoger los elementos de los DFD y el E/R
- Continuar explosionando el DFD hasta el nivel adecuado sin "matar moscas a cañonazos".
- Blancear el DFD, el E/R y el DD a lo largo de todo el proceso.
3. Obtener las EP:
- Obtención de las EP de al menos las burbujas primitivas.
- Evaluar la necesidad de elaborar las EP de las burbujas del resto de niveles.
- Balancear la EP con el resto de modelos.
