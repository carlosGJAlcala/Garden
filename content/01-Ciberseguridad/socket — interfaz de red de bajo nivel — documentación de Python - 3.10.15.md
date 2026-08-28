---
created: 2024-11-22T11:10:15 (UTC +01:00)
tags: []
source: https://docs.python.org/es/3.10/library/socket.html
author: 
---

# socket — interfaz de red de bajo nivel — documentación de Python - 3.10.15

> ## Excerpt
> Código fuente: Lib/socket.py

---
**Código fuente:** [Lib/socket.py](https://github.com/python/cpython/tree/3.10/Lib/socket.py)

___

Este módulo proporciona acceso a la interfaz BSD _socket_. Está disponible en todos los sistemas Unix modernos, Windows, MacOS y probablemente plataformas adicionales.

Nota

Algunos comportamientos pueden depender de la plataforma, ya que las llamadas se realizan a las API de socket del sistema operativo.

La interfaz de Python es una transcripción sencilla de la llamada al sistema Unix y la interfaz de la biblioteca para sockets al estilo orientado a objetos de Python: la función `socket()` devuelve a _socket object_ cuyos métodos implementan las diversas llamadas al sistema de socket. Los tipos de parámetros tienen un nivel algo más alto que en la interfaz C: como con `read()` y `write()` en las operaciones en los archivos Python, la asignación del buffer en las operaciones de recepción es automática y la longitud del buffer está implícita en las operaciones de envío.

Ver también

Módulo [`socketserver`](https://docs.python.org/es/3.10/library/socketserver.html#module-socketserver "socketserver: A framework for network servers.")

Clases que simplifican la escritura de servidores de red.

Módulo [`ssl`](https://docs.python.org/es/3.10/library/ssl.html#module-ssl "ssl: TLS/SSL wrapper for socket objects")

Un contenedor TLS/SSL para objetos de socket.

## Familias Socket

Dependiendo del sistema y de las opciones de compilación, este módulo admite varias familias de sockets.

El formato de dirección requerido por un objeto de socket determinado se selecciona automáticamente en función de la familia de direcciones especificada cuando se creó el objeto de socket. Las direcciones de socket se representan de la siguiente manera:

- La dirección de un socket [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") enlazado a un nodo del sistema de archivos es representado como una cadena de caracteres, utilizando la codificación del sistema de archivos y el controlador de errores `'surrogateescape'` (Observar [**PEP 383**](https://www.python.org/dev/peps/pep-0383)). Una dirección en el espacio de nombre abstracto de Linux es devuelvo como un [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object) con un byte inicial nulo; tenga en cuenta que los sockets en este nombre de espacio puede comunicarse con sockets normales del sistema de archivos, así que los programas destinados a correr en Linux podrían necesitar tratar con ambos tipos de direcciones. Se puede pasar un objeto similar a una cadena de caracteres o bytes para cualquier tipo de dirección al pasarlo como argumento.

    Distinto en la versión 3.3: Anteriormente, se suponía que las rutas de socket [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") utilizaban codificación UTF-8.

    Distinto en la versión 3.5: Ahora se acepta la grabación [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object).

- Se utiliza un par `(host, port)` para la familia de direcciones [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET"), donde _host_ es una cadena que representa un nombre de host en notación de dominio de Internet como `'daring.cwi.nl'` o una dirección IPv4 como `'100.50.200.5'`, y _port_ es un número entero.
    - Para direcciones IPv4, se aceptan dos formas especiales en lugar de una dirección de host: `’’` representa `INADDR_ANY`, que se utiliza para enlazar a todas las interfaces, y la cadena de caracteres `'<broadcast>'` representa `INADDR_BROADCAST`. Este comportamiento no es compatible con IPv6, por lo tanto, es posible que desee evitarlos sí tiene la intención de admitir IPv6 con sus programas Python.
- Para la familia de direcciones [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"), se utiliza una `(host, port, flowinfo, scope_id)` de cuatro tuplas, donde _flowinfo_ y _scope\_id_ representan los miembros `sin6_flowinfo` y `sin6_scope_id` en `struct sockaddr_in6` en C. Para los métodos de los módulos [`socket`](https://docs.python.org/es/3.10/library/socket.html#module-socket "socket: Low-level networking interface."), _flowinfo_ y _scope\_id_ pueden ser omitidos solo por compatibilidad con versiones anteriores. Sin embargo la omisión de _scope\_id_ puede causar problemas en la manipulación de direcciones IPv6 con ámbito.

    Distinto en la versión 3.7: Para direcciones de multidifusión (con _scopeid_ significativo) _address_ puede no contener la parte `%scope` (o `zone id`). Esta información es superflua y puede omitirse de forma segura (recomendado).

- `AF_NETLINK` sockets se representan como pares `(pid, groups)`.
- La compatibilidad con LINUX solo para TIPC está disponible mediante la familia de direcciones `AF_TIPC`. TIPC es un protocolo en red abierto y no basado en IP diseñado para su uso en entornos informáticos agrupados. Las direcciones se representan mediante una tupla y los campos dependen del tipo de dirección. El formulario de tupla general es `(addr_type, v1, v2, v3 [, scope])`, donde:
    - _addr\_type_ es uno de `TIPC_ADDR_NAMESEQ`, `TIPC_ADDR_NAME`, o `TIPC_ADDR_ID`.
    - _scope_ es una de `TIPC_ZONE_SCOPE`, `TIPC_CLUSTER_SCOPE`, y `TIPC_NODE_SCOPE`.
    - Si _addr\_type_ es `TIPC_ADDR_NAME`, entonces _v1_ es el tipo de servidor, _v2_ es el identificador de puerto, y _v3_ debe ser 0.

        Si _addr\_type_ es `TIPC_ADDR_NAMESEQ`, entonces _v1_ es el tipo de servidor, _v2_ es el numero de puerto inferior, y _v3_ es el numero de puerto superior.

        Si _addr\_type_ es `TIPC_ADDR_ID`, _v1_ es el nodo, _v2_ es la referencia y _v3_ debe establecerse en 0.

- Una tupla `(interface, )` es usada para la dirección de familia [`AF_CAN`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_CAN "socket.AF_CAN"), donde _interface_ es una cadena de caracteres representando a un nombre de interfaz de red como `’can0’`. La interfaz de red llamada `''` puede ser usada para recibir paquetes de todas las interfaces de red de esta familia.
    - Protocolo [`CAN_ISOTP`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_ISOTP "socket.CAN_ISOTP") requiere una tupla `(interface, rx_addr, tx_addr)` donde ambos tiene parámetros adicionales son enteres largos sin símbolos que representan una identificador CAN (estándar o extendido).
    - Protocolo [`CAN_J1939`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_J1939 "socket.CAN_J1939") requiere una tupla `(interface, name, pgn, addr)` donde los parámetros adicionales son números enteros sin signo de 64 bits representando el nombre ECU, los enteros sin signo de 32-bits representan el numero de grupo de parámetros(PGN), y los enteros de 8-bit representan la dirección.
- A string or a tuple `(id, unit)` is used for the `SYSPROTO_CONTROL` protocol of the `PF_SYSTEM` family. The string is the name of a kernel control using a dynamically assigned ID. The tuple can be used if ID and unit number of the kernel control are known or if a registered ID is used.

    Nuevo en la versión 3.3.

- `AF_BLUETOOTH` admite los siguientes protocolos y formatos de dirección:
    - `BTPROTO_L2CAP` acepta `(bdaddr, psm)` donde `bdaddr` es la dirección Bluetooth como una cadena de caracteres y `psm` es un entero.
    - `BTPROTO_RFCOMM` acepta `(bdaddr, channel)` donde `bdaddr` es la dirección Bluetooth como una cadena de caracteres y `channel` es un entero.
    - `BTPROTO_HCI` acepta `(device_id,)` donde `device_id` es un numero entero o una cadena de caracteres con la dirección Bluetooth de la interfaz. (Esto depende de tu OS; NetBSD y DragonFlyBSD supone una dirección Bluetooth mientras todo lo demás espera un entero.)

        Distinto en la versión 3.2: Se ha añadido compatibilidad con NetBSD y DragonFlyBSD.

    - `BTPROTO_SCO` acepta `bdaddr` donde `bdaddr` es un objeto [`bytes`](https://docs.python.org/es/3.10/library/stdtypes.html#bytes "bytes") que contiene la dirección Bluetooth en un formato cadena. (ex. `b’12:23:34:45:56:67’`) este protocolo no es admitido bajo FreeBSD.
- [`AF_ALG`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_ALG "socket.AF_ALG") es una interfaz basada en socket sólo Linux para la criptografía del núcleo. Un socket de algoritmo se configura con una tupla de dos a cuatro elementos `(type, name [, feat [, mask]])`, donde:
    - _type_ es el tipo de algoritmos como cadenas de caracteres, e.g. `aead`, `hash`, `skcipher` o `rng`.
    - _name_ es el nombre del algoritmo y el modo de operación como cadena de caracteres, e.g. `sha256`, `hmac(sha256)`, `cbc(aes)` o `drbg_nopr_ctr_aes256`.
    - _feat_ y _mask_ son enteros de 32 bits sin signo.

    [Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux 2.6.38, some algorithm types require more recent Kernels.

    Nuevo en la versión 3.6.

- [`AF_VSOCK`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_VSOCK "socket.AF_VSOCK") permite comunicación entre maquinas virtuales y sus hosts. Los sockets están representando como una tupla `(CID, port)` donde el contexto del ID o CID y el puerto son enteros.

    [Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 4.8 QEMU >= 2.8 ESX >= 4.0 ESX Workstation >= 6.5.

    Nuevo en la versión 3.7.

- [`AF_PACKET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_PACKET "socket.AF_PACKET") es una interfaz de bajo nivel directa con los dispositivos de red. Los paquetes están representados por la tupla `(ifname, proto[, pkttype[, hatype[, addr]]])` donde:
    - _ifname_ - Cadena que especifica el nombre del dispositivo.
    - _proto_ - Un entero en orden de byte de red que especifica el número de protocolo Ethernet.
    - _pkttype_ - Entero opcional especificando el tipo de paquete:
        - `PACKET_HOST` (por defecto) - Paquetes diseccionado al local host.
        - `PACKET_BROADCAST` - Paquete de transmisión de la capa física.
        - `PACKET_MULTIHOST` - Paquete enviado a una dirección de multidifusión de capa física.
        - `PACKET_OTHERHOST` - Paquete a otro host que haya sido capturado por un controlador de dispositivo en modo promiscuo.
        - `PACKET_OUTGOING` - Paquete originalmente desde el local host que se enlaza de nuevo a un conector de paquetes.
    - _hatype_ - Entero opcional que especifica el tipo de dirección de hardware ARP.
    - _addr_ - Objeto opcional en forma de bytes que especifica la dirección física del hardware, cuya interpretación depende del dispositivo.
- [`AF_QIPCRTR`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_QIPCRTR "socket.AF_QIPCRTR") es una interfaz basada en sockets solo para Linux para comunicarse con servicios que se ejecutan en co-procesadores en plataformas Qualcomm. La familia de direcciones se representa como una tupla `(node, port)` donde el _node_ y _port_ son enteros no negativos.

    Nuevo en la versión 3.8.

- `IPPROTO_UDPLITE` es una variante de UDO que te permite especificar que porción del paquete es cubierta con la suma de comprobación. Esto agrega dos opciones al socket que pueden cambiar. `self.setsockopt(IPPROTO_UDPLITE, UDPLITE_SEND_CSCOV, length)` cambiara que parte de los paquetes salientes están cubierta por la suma de comprobación y `self.setsockopt(IPPROTO_UDPLITE, UDPLITE_RECV_CSCOV, length)` filtrara los paquetes que permitirá cubrir una pequeña parte de tu datos. En ambos casos `length` deben estar en `range(8, 2**16, 8)`.

    Tal socket debe construirse como `socket(AF_INET, SOCK_DGRAM, IPPROTO_UDPLITE)` para IPV4 o socket(AF\_INET6, SOCK\_DGRAM, IPPROTO\_UDPLITE)\` para IPV6.

    [Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.20, FreeBSD >= 10.1-RELEASE

    Nuevo en la versión 3.9.

Si utiliza un nombre de host en la parte _host_ de la dirección de socket IPv4/v6, el programa puede mostrar un comportamiento no determinista, ya que Python utiliza la primera dirección devuelta por la resolución DNS. La dirección del socket se resolverá de manera diferente en una dirección IPv4/v6 real, dependiendo de los resultados de la resolución DNS y/o la configuración del host. Para un comportamiento determinista, utilice una dirección numérica en la parte _host_.

All errors raise exceptions. The normal exceptions for invalid argument types and out-of-memory conditions can be raised. Errors related to socket or address semantics raise [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") or one of its subclasses.

El modo de no bloqueo es compatible a través de [`setblocking()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.setblocking "socket.socket.setblocking"). Se admite una generalización de esto basada en los tiempos de espera a través de [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout").

## Contenido del módulo

El módulo [`socket`](https://docs.python.org/es/3.10/library/socket.html#module-socket "socket: Low-level networking interface.") exporta los siguientes elementos.

### Excepciones

_exception_ `socket.``error`

Un alias en desuso de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError").

Distinto en la versión 3.3: Siguiendo [**PEP 3151**](https://www.python.org/dev/peps/pep-3151), es clase fue creada como un alias de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError").

_exception_ `socket.``herror`

Una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError"), esta excepción se produce para los errores relacionados con la dirección, es decir, para las funciones que utilizan _h\_errno_ en la API de POSIX C, incluidas [`gethostbyname_ex()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyname_ex "socket.gethostbyname_ex") y [`gethostbyaddr()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyaddr "socket.gethostbyaddr"). El valor adjunto es un par `(h_errno, string)` que representa un error devuelto por una llamada a la biblioteca. _h\_errno_ es un valor numérico, mientras que _string_ representa la descripción de _h\_errno_, devuelta por la función `hstrerror()` C.

Distinto en la versión 3.3: Esta clase fue creada como una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError").

_exception_ `socket.``gaierror`

Una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError"), esta excepción se genera por errores relacionados a la dirección por [`getaddrinfo()`](https://docs.python.org/es/3.10/library/socket.html#socket.getaddrinfo "socket.getaddrinfo") y [`getnameinfo()`](https://docs.python.org/es/3.10/library/socket.html#socket.getnameinfo "socket.getnameinfo"). El valor de acompañamiento es un par `(error, string)` representado un error retornado por una llamada de librería. _string_ representa la descripción del _error_, tal como es retornado por la función C `gai_strerror()`. El valor numérico _error_ coincide con una de las constantes `EAI_*` definidas en este modulo.

Distinto en la versión 3.3: Esta clase fue creada como una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError").

_exception_ `socket.``timeout`

Un alias obsoleto de [`TimeoutError`](https://docs.python.org/es/3.10/library/exceptions.html#TimeoutError "TimeoutError").

Una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError"), esta excepción se genera cuando ocurre un _timeout_ en un socket que ha tenido tiempos de espera habilitados a través de una llamada previa a [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout") ( o implícitamente mediante [`setdefaulttimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.setdefaulttimeout "socket.setdefaulttimeout")). El valor del acompañamiento es una cadena de caracteres cuyo valor es actualmente siempre “tiempo de espera”.

Distinto en la versión 3.3: Esta clase fue creada como una subclase de [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError").

Distinto en la versión 3.10: Esta clase se convirtió en un alias de [`TimeoutError`](https://docs.python.org/es/3.10/library/exceptions.html#TimeoutError "TimeoutError").

### Constantes

> Las constantes AF\_\* y SOCK\_\* ahora son colecciones: `AddressFamily` y `SocketKind` [`IntEnum`](https://docs.python.org/es/3.10/library/enum.html#enum.IntEnum "enum.IntEnum").
>
> Nuevo en la versión 3.4.

`socket.``AF_UNIX`

`socket.``AF_INET`

`socket.``AF_INET6`

Estas constantes representan la familias de direcciones (y protocolos), usados para el primer argumento para `socket()`. Si la constante [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") no esta definida entonces este protocolo no es compatible. Mas constantes podrían estar disponibles dependiendo del sistema.

`socket.``SOCK_STREAM`

`socket.``SOCK_DGRAM`

`socket.``SOCK_RAW`

`socket.``SOCK_RDM`

`socket.``SOCK_SEQPACKET`

Estas constantes representan los tipos de socket, usadas por el segundo argumento para `socket()`. Mas constante podrían estar disponibles dependiendo del sistema. ( Solamente [`SOCK_STREAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_STREAM "socket.SOCK_STREAM") y [`SOCK_DGRAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_DGRAM "socket.SOCK_DGRAM") parecen ser útiles en general.)

`socket.``SOCK_CLOEXEC`

`socket.``SOCK_NONBLOCK`

Estas dos constantes, si se definen, se pueden combinar con los tipos de socket y le permiten establecer algunas banderas atómicamente (evitando así posibles condiciones de carrera y la necesidad de llamadas separadas).

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.27.

Nuevo en la versión 3.2.

`SO_*`

`socket.``SOMAXCONN`

`MSG_*`

`SOL_*`

`SCM_*`

`IPPROTO_*`

`IPPORT_*`

`INADDR_*`

`IP_*`

`IPV6_*`

`EAI_*`

`AI_*`

`NI_*`

`TCP_*`

Muchas constantes de estos formularios, documentadas en la documentación de Unix en sockets y/o el protocolo IP, también se definen en el módulo de socket. Generalmente se utilizan en argumentos de los métodos `setsockopt()` y `getsockopt()` de objetos socket. En la mayoría de los casos, solo se definen los símbolos definidos en los archivos de encabezado Unix; para algunos símbolos, se proporcionan valores predeterminados.

Distinto en la versión 3.6: `SO_DOMAIN`, `SO_PROTOCOL`, `SO_PEERSEC`, `SO_PASSSEC`, `TCP_USER_TIMEOUT`, `TCP_CONGESTION` han sido agregados.

Distinto en la versión 3.6.5: En Windows, `TCP_FASTOPEN`, `TCP_KEEPCNT` aparecen si el tiempo de ejecución de Windows lo admite.

Distinto en la versión 3.7: `TCP_NOTSENT_LOWAT` ha sido agregada.

En Windows, `TCP_KEEPIDLE`, `TCP_KEEPINTVL` aparecen si el tiempo de ejecución de Windows lo admite.

Distinto en la versión 3.10: Se agregó `IP_RECVTOS`. Se agregó `TCP_KEEPALIVE`. En MacOS, esta constante se puede utilizar de la misma forma que `TCP_KEEPIDLE` en Linux.

`socket.``AF_CAN`

`socket.``PF_CAN`

`SOL_CAN_*`

`CAN_*`

Muchas constantes de estos formularios, documentadas en la documentación de Linux, también se definen en el módulo de socket.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.25.

Nuevo en la versión 3.3.

`socket.``CAN_BCM`

`CAN_BCM_*`

CAN\_BCM, en la familia de protocolo CAN, es el protocolo del administrador de difusión (BCM. Las constantes del administrador de difusión, documentada en la documentación de Linux, también esta definidos en el modulo socket.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.25.

Nota

El indicador `CAN_BCM_CAN_FD_FRAME` esta solamente disponible en Linux >= 4.8.

Nuevo en la versión 3.4.

`socket.``CAN_RAW_FD_FRAMES`

Habilita la compatibilidad con CAN FD en un socket CAN\_RAW. Esta opción está deshabilitada de forma predeterminada. Esto permite que la aplicación envíe tramas CAN y CAN FD; sin embargo, debe aceptar las tramas CAN y CAN FD al leer desde el socket.

Esta constante se documenta en la documentación de Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 3.6.

Nuevo en la versión 3.5.

`socket.``CAN_RAW_JOIN_FILTERS`

Se une a los filtros CAN aplicados de modo que solo las tramas CAN que coinciden con todos los filtros CAN dados se pasan al espacio del usuario.

Esta constante se documenta en la documentación de Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 4.1.

Nuevo en la versión 3.9.

`socket.``CAN_ISOTP`

CAN\_ISOTP, en el protocolo de familia CAN, es el protocolo ISO-TP (ISO 15765-2). Constantes ISO-TP, documentadas en la documentación Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.25.

Nuevo en la versión 3.7.

`socket.``CAN_J1939`

CAN\_J1939, en el protocolo de familias CAN, es el protocolo SAE J1939. Constantes J1939, documentadas en el documentación Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 5.4.

Nuevo en la versión 3.9.

`socket.``AF_PACKET`

`socket.``PF_PACKET`

`PACKET_*`

Muchas constantes de estos formularios, documentadas en la documentación de Linux, también se definen en el módulo de socket.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.2.

`socket.``AF_RDS`

`socket.``PF_RDS`

`socket.``SOL_RDS`

`RDS_*`

Muchas constantes de estos formularios, documentadas en la documentación de Linux, también se definen en el módulo de socket.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.30.

Nuevo en la versión 3.3.

`socket.``SIO_RCVALL`

`socket.``SIO_KEEPALIVE_VALS`

`socket.``SIO_LOOPBACK_FAST_PATH`

`RCVALL_*`

Constantes para Windows’ WSAIoctl(). Las constantes se utiliza como argumentos al método [`ioctl()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.ioctl "socket.socket.ioctl") de objetos de sockets.

Distinto en la versión 3.6: `SIO_LOOPBACK_FAST_PATH` ha sido agregado.

`TIPC_*`

LAS constantes relacionadas con TIPC, que coinciden con las exportadas por la API de socket de C. Consulte la documentación de TIPC para obtener más información.

`socket.``AF_ALG`

`socket.``SOL_ALG`

`ALG_*`

Constantes para la criptográfica del Kernel de Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.38.

Nuevo en la versión 3.6.

`socket.``AF_VSOCK`

`socket.``IOCTL_VM_SOCKETS_GET_LOCAL_CID`

`VMADDR*`

`SO_VM*`

Constantes para la comunicación host/invitado de Linux.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 4.8.

Nuevo en la versión 3.7.

`socket.``AF_LINK`

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): BSD, macOS.

Nuevo en la versión 3.4.

`socket.``has_ipv6`

Esta constante contiene un valor booleano que indica si IPv6 se admite en esta plataforma.

`socket.``BDADDR_ANY`

`socket.``BDADDR_LOCAL`

Estas son constantes de cadenas que contienen direcciones Bluetooth con significados especiales. Por ejemplo [`BDADDR_ANY`](https://docs.python.org/es/3.10/library/socket.html#socket.BDADDR_ANY "socket.BDADDR_ANY") son usados para indicar cualquier dirección al especificar el socket vinculante con `BTPROTO_RFCOMM`.

`socket.``HCI_FILTER`

`socket.``HCI_TIME_STAMP`

`socket.``HCI_DATA_DIR`

Para usar con `BTPROTO_HCI`. [`HCI_FILTER`](https://docs.python.org/es/3.10/library/socket.html#socket.HCI_FILTER "socket.HCI_FILTER") no esta disponible para NetBSD o DragonFlyBSD. [`HCI_TIME_STAMP`](https://docs.python.org/es/3.10/library/socket.html#socket.HCI_TIME_STAMP "socket.HCI_TIME_STAMP") y [`HCI_DATA_DIR`](https://docs.python.org/es/3.10/library/socket.html#socket.HCI_DATA_DIR "socket.HCI_DATA_DIR") no esta disponible para FreeBSD, NetBSD, o DragonFlyBSD.

`socket.``AF_QIPCRTR`

Constante para el protocolo de router IPC de Qualcomm, que se utiliza para comunicarse con procesadores remotos que brindan servicios.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 4.7.

### Funciones

#### Creación de sockets

Todas las siguientes funciones crean [socket objects](https://docs.python.org/es/3.10/library/socket.html#socket-objects).

_class_ `socket.``socket`(_family\=AF\_INET_, _type\=SOCK\_STREAM_, _proto\=0_, _fileno\=None_)

Crear un nuevo socket usando la dirección de familia dada, tipo de socket y el numero de protocolo. La dirección de familia debería ser [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET") (por defecto), [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"), [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX"), [`AF_CAN`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_CAN "socket.AF_CAN"), [`AF_PACKET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_PACKET "socket.AF_PACKET"), o [`AF_RDS`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_RDS "socket.AF_RDS"). El tipo de socket debería ser [`SOCK_STREAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_STREAM "socket.SOCK_STREAM") (por defecto), [`SOCK_DGRAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_DGRAM "socket.SOCK_DGRAM"), [`SOCK_RAW`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_RAW "socket.SOCK_RAW") o quizás una de las otras constantes `SOCK_`. El numero de protocolo es usualmente cero u omitirse o en el caso donde la familia de dirección es [`AF_CAN`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_CAN "socket.AF_CAN") el protocolo debería ser uno de `CAN_RAW`, [`CAN_BCM`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_BCM "socket.CAN_BCM"), [`CAN_ISOTP`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_ISOTP "socket.CAN_ISOTP") o [`CAN_J1939`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_J1939 "socket.CAN_J1939").

Si _fileno_ esta especificado, el valor de _family_, _type_, y _proto_ son detectados automáticamente por el descriptor especificado de archivo. La detección automática se puede anular llamado la función con los argumentos explícitos _family_, _type_, o _proto_. Esto solamente afecta como Python representa e.g. el valor de retorno de [`socket.getpeername()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.getpeername "socket.socket.getpeername") pero no del recurso actual del OS. Diferente a [`socket.fromfd()`](https://docs.python.org/es/3.10/library/socket.html#socket.fromfd "socket.fromfd"), _fileno_ retornara el mismo socket y no un duplicado. Esto puede ayudar a cerrar un socket desconectado usando [`socket.close()`](https://docs.python.org/es/3.10/library/socket.html#socket.close "socket.close").

El socket recién creado es [non-inheritable](https://docs.python.org/es/3.10/library/os.html#fd-inheritance).

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.__new__` con los argumentos `self`, `family`, `type`, `protocol`.

Distinto en la versión 3.3: Se añadió la familia AF\_CAN. Se añadió la familia AF\_RDS.

Distinto en la versión 3.4: El protocolo CAN\_BCM ha sido agregado.

Distinto en la versión 3.4: Los sockets devueltos ahora no son heredables.

Distinto en la versión 3.7: El protocolo CAN\_ISOTP ha sido agregado.

Distinto en la versión 3.7: When [`SOCK_NONBLOCK`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_NONBLOCK "socket.SOCK_NONBLOCK") or [`SOCK_CLOEXEC`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_CLOEXEC "socket.SOCK_CLOEXEC") bit flags are applied to _type_ they are cleared, and [`socket.type`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.type "socket.socket.type") will not reflect them. They are still passed to the underlying system `socket()` call. Therefore,

```
<span></span><span>sock</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span>
    <span>socket</span><span>.</span><span>AF_INET</span><span>,</span>
    <span>socket</span><span>.</span><span>SOCK_STREAM</span> <span>|</span> <span>socket</span><span>.</span><span>SOCK_NONBLOCK</span><span>)</span>
```

seguirá creando un socket sin bloqueo en los sistemas operativos que admiten `SOCK_NONBLOCK`, pero `sock.type` se establecerá en `socket.SOCK_STREAM`.

Distinto en la versión 3.9: El protocolo CAN\_J1939 ha sido agregado.

Distinto en la versión 3.10: Se agregó el protocolo IPPROTO\_MPTCP.

`socket.``socketpair`(\[_family_\[, _type_\[, _proto_\]\]\])

Cree un par de objetos de socket conectados utilizando la familia de direcciones, el tipo de socket y el número de protocolo especificados. La familia de direcciones, el tipo de socket y el número de protocolo son los siguientes para la función `socket()` anterior. La familia predeterminada es [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") si se define en la plataforma; de lo contrario, el valor predeterminado es [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET").

Los sockets creados recientemente son [non-inheritable](https://docs.python.org/es/3.10/library/os.html#fd-inheritance).

Distinto en la versión 3.2: Los objetos de socket devueltos ahora admiten toda la API de socket, en lugar de un subconjunto.

Distinto en la versión 3.4: Los sockets devueltos ahora no son heredables.

Distinto en la versión 3.5: Se ha agregado compatibilidad con Windows.

`socket.``create_connection`(_address_\[, _timeout_\[, _source\_address_\]\])

Se conecta a un servicio TCP que esté escuchando en Internet _address_ (un `(host, port)` de 2 tuplas) y retorna el objeto de socket. Esta es una función de nivel superior que [`socket.connect()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.connect "socket.socket.connect"): si _host_ es un nombre de host no numérico, intentará resolverlo para [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET") y [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"), y luego intentará conectarse a todas las direcciones posibles sucesivamente hasta que la conexión se realice correctamente. Esto facilita la escritura de clientes que sean compatibles con IPv4 e IPv6.

Pasando el parámetro opcional _timeout_ establece el tiempo de espera dentro de la instancia del socket. Si no es proporcionado _timeout_, la configuración global de tiempo de espera predeterminada retornada por [`getdefaulttimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.getdefaulttimeout "socket.getdefaulttimeout") es usada.

Si se suministra, _source\_address_ debe ser una “”(host, puerto)”” de 2 tuplas para que el socket se enlace como su dirección de origen antes de conectarse. Si el host o el puerto son “” o 0 respectivamente, se utilizará el comportamiento predeterminado del sistema operativo.

Distinto en la versión 3.2: _source\_address_ ha sido agregado.

`socket.``create_server`(_address_, _\*_, _family\=AF\_INET_, _backlog\=None_, _reuse\_port\=False_, _dualstack\_ipv6\=False_)

Función de conveniencia que crea un socket TCP enlazado a _address_ (una tupla de 2 `(host, puerto)`) y devuelve el objeto de socket.

_family_ should be either [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET") or [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"). _backlog_ is the queue size passed to [`socket.listen()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.listen "socket.socket.listen"); if not specified , a default reasonable value is chosen. _reuse\_port_ dictates whether to set the `SO_REUSEPORT` socket option.

Si _dualstack\_ipv6_ es true y la plataforma lo admite el socket podrá aceptar conexiones IPv4 e IPv6, de lo contrario lanzará [`ValueError`](https://docs.python.org/es/3.10/library/exceptions.html#ValueError "ValueError"). Se supone que la mayoría de las plataformas POSIX y Windows admiten esta funcionalidad. Cuando esta funcionalidad está habilitada, la dirección devuelta por [`socket.getpeername()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.getpeername "socket.socket.getpeername") cuando se produce una conexión IPv4 será una dirección IPv6 representada como una dirección IPv4 asignada6. Si _dualstack\_ipv6_ es false, deshabilitará explícitamente esta funcionalidad en las plataformas que la habilitan de forma predeterminada (por ejemplo, Linux). Este parámetro se puede utilizar junto con [`has_dualstack_ipv6()`](https://docs.python.org/es/3.10/library/socket.html#socket.has_dualstack_ipv6 "socket.has_dualstack_ipv6"):

```
<span></span><span>import</span> <span>socket</span>

<span>addr</span> <span>=</span> <span>(</span><span>""</span><span>,</span> <span>8080</span><span>)</span>  <span># all interfaces, port 8080</span>
<span>if</span> <span>socket</span><span>.</span><span>has_dualstack_ipv6</span><span>():</span>
    <span>s</span> <span>=</span> <span>socket</span><span>.</span><span>create_server</span><span>(</span><span>addr</span><span>,</span> <span>family</span><span>=</span><span>socket</span><span>.</span><span>AF_INET6</span><span>,</span> <span>dualstack_ipv6</span><span>=</span><span>True</span><span>)</span>
<span>else</span><span>:</span>
    <span>s</span> <span>=</span> <span>socket</span><span>.</span><span>create_server</span><span>(</span><span>addr</span><span>)</span>
```

Nota

En plataformas POSIX la opción del socket `SO_REUSEADDR` está configurado para inmediatamente rehusar los sockets previos que estaban vinculados la misma _address_ y permanecer en estado TIME\_WAIT.

Nuevo en la versión 3.8.

`socket.``has_dualstack_ipv6`()

Retorna `True` si la plataforma admite la creación de un socket TCP que pueda manejar conexiones IPv4 e IPv6.

Nuevo en la versión 3.8.

`socket.``fromfd`(_fd_, _family_, _type_, _proto\=0_)

Duplica el descriptor de archivo _fd_ (un entero retornado por el método `fileno()` de un objeto archivo) y crea un objeto socket a partir del resultado. La familia de direcciones, el tipo de socket y el número de protocolo son como para la función `socket()` anterior. El descriptor de archivo debe hacer referencia a un socket, pero esto no se comprueba — las operaciones posteriores en el objeto pueden fallar si el descriptor de archivo no es válido. Esta función rara vez se necesita, pero se puede usar para obtener o establecer opciones de socket en un socket pasado a un programa como entrada o salida estándar (como un servidor iniciado por el demonio inet de Unix). Se supone que el socket está en modo de bloqueo.

El socket recién creado es [non-inheritable](https://docs.python.org/es/3.10/library/os.html#fd-inheritance).

Distinto en la versión 3.4: Los sockets devueltos ahora no son heredables.

`socket.``fromshare`(_data_)

Cree una instancia de un socket a partir de los datos obtenidos del método [`socket.share()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.share "socket.socket.share"). Se supone que el socket está en modo de bloqueo.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Windows.

Nuevo en la versión 3.3.

`socket.``SocketType`

Este es un tipo de objeto Python que representa el tipo de objeto del socket. Es lo mismo que decir `type(socket(…))`.

#### Otras funciones

El modulo [`socket`](https://docs.python.org/es/3.10/library/socket.html#module-socket "socket: Low-level networking interface.") también ofrece varios servicios de red relacionados:

`socket.``close`(_fd_)

Cierre un descriptor de archivo de socket. Esto es como [`os.close()`](https://docs.python.org/es/3.10/library/os.html#os.close "os.close"), pero para sockets. En algunas plataformas (la mayoría notable de Windows) [`os.close()`](https://docs.python.org/es/3.10/library/os.html#os.close "os.close") no funciona para descriptores de archivos de socket.

Nuevo en la versión 3.7.

`socket.``getaddrinfo`(_host_, _port_, _family\=0_, _type\=0_, _proto\=0_, _flags\=0_)

Traduce el argumento _host_/_port_ dentro de una secuencia de 5 tuplas que contiene todo los argumentos necesarios para crear un socket conectado a ese servicio. _host_ es un nombre de dominio, una cadena en representación de una dirección IPV4/IPV6 o `None`. _port_ es una nombre de una cadena de servicio como `'http'`, un numero de puerto numérico o `None`. Pasando `None` como el valor del _host_ y _port_, pasando `NULL` a la API C subyacente.

Los argumentos _family_, _type_ y _proto_ se puede especificar opcionalmente para reducir la lista de direcciones retornadas. Pasando cero como un valor para cada uno de estos argumentos se selecciona la gama completa de resultados. El argumento _flags_ puede ser uno o varios de los argumentos `AI_*`, y pueden influenciar como los resultados son computados y devueltos. Por ejemplo, `AI_NUMERICHOST` desactivará la resolución de nombres de dominio y lanzará un error sí _host_ es un nombre de dominio.

La función devuelve una lista de 5 tuplas con la siguiente estructura:

`(family, type, proto, canonname, sockaddr)`

En estas tuplas, _family_, _type_, _proto_ son todos enteros y están destinados a ser pasados por la función `socket()`. _canonname_ debe ser una cadena que representa el nombre canónico del _host_ si `AI_CANONNAME` es parte de el argumento _flags_; de lo contrario _canonname_ estará vacía. _sockaddr_ es un tupla describiendo una dirección de socket, cuyo formato depende del devuelto _family_ (una `(address, port)` tupla de 2 para [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET"), una `(address, port, flowinfo, scope_id)` una tupla de 4 para una [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6")), y está destinado a ser pasado a el método [`socket.connect()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.connect "socket.socket.connect").

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.getaddrinfo` con los argumentos `host`, `port`, `family`, `type`, `protocol`.

En el ejemplo siguiente se obtiene información de dirección para una conexión TCP hipotética a `example.org` en el puerto 80 (los resultados pueden diferir en el sistema si IPv6 no está habilitado):

\>>>

```
<span></span><span>&gt;&gt;&gt; </span><span>socket</span><span>.</span><span>getaddrinfo</span><span>(</span><span>"example.org"</span><span>,</span> <span>80</span><span>,</span> <span>proto</span><span>=</span><span>socket</span><span>.</span><span>IPPROTO_TCP</span><span>)</span>
<span>[(&lt;AddressFamily.AF_INET6: 10&gt;, &lt;AddressFamily.SOCK_STREAM: 1&gt;,</span>
<span> 6, '', ('2606:2800:220:1:248:1893:25c8:1946', 80, 0, 0)),</span>
<span> (&lt;AddressFamily.AF_INET: 2&gt;, &lt;AddressFamily.SOCK_STREAM: 1&gt;,</span>
<span> 6, '', ('93.184.216.34', 80))]</span>
```

Distinto en la versión 3.2: los parámetros ahora se pueden pasar mediante argumentos de palabra clave.

Distinto en la versión 3.7: para direcciones de multidifusión IPv6, la cadena que representa una dirección no contendrá partes `%scope_id`.

`socket.``getfqdn`(\[_name_\])

Retorna un nombre de dominio completo para _name_. Si _name_ se omite o está vacío, se interpreta como el host local. Para encontrar el nombre completo, se comprueba el nombre de host retornado por [`gethostbyaddr()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyaddr "socket.gethostbyaddr"), seguido de los alias del host, si están disponibles. Se selecciona el primer nombre que incluye un punto. En caso de que no haya disponible un nombre de dominio completo y se haya proporcionado _name_, se retorna sin cambios. Si _name_ estaba vacío o era igual a `'0.0.0.0'`, se retorna el nombre de host de [`gethostname()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostname "socket.gethostname").

`socket.``gethostbyname`(_hostname_)

Traduce un nombre de host a un formato de dirección IPV4. La dirección IPV4 es retornada como una cadena, como `’100.50.200.5’`. Si el nombre de host es una dirección IPV4 en sí, se devuelve sin cambios. Observa [`gethostbyname_ex()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyname_ex "socket.gethostbyname_ex") para una interfaz mas completa. [`gethostbyname()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyname "socket.gethostbyname") no soporta la resolución de nombres IPV6, y [`getaddrinfo()`](https://docs.python.org/es/3.10/library/socket.html#socket.getaddrinfo "socket.getaddrinfo") debe utilizarse en su lugar para compatibilidad con doble pila IPv4/v6.

Genera un evento [auditing](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.gethostbyname` con el argumento `hostname`.

`socket.``gethostbyname_ex`(_hostname_)

Traduce un nombre de host al formato de dirección IPv4, interfaz ampliada. Retorna un triple `(hostname, aliaslist, ipaddrlist)` donde _hostname_ es el nombre de host principal del host, _aliaslist_ es una lista (posiblemente vacía) de nombres de host alternativos para la misma dirección y _ipaddrlist_ es una lista de direcciones IPv4 para la misma interfaz en el mismo host (a menudo, pero no siempre una sola dirección). [`gethostbyname_ex()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyname_ex "socket.gethostbyname_ex") no es compatible con la resolución de nombres IPv6 y, en su lugar, se debe utilizar [`getaddrinfo()`](https://docs.python.org/es/3.10/library/socket.html#socket.getaddrinfo "socket.getaddrinfo") para el soporte de pila dual IPv4 / v6.

Genera un evento [auditing](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.gethostbyname` con el argumento `hostname`.

`socket.``gethostname`()

Retorna una cadena que contenga el nombre de host de la máquina donde se está ejecutando actualmente el intérprete de Python.

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.gethostname` sin argumentos.

Nota: [`gethostname()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostname "socket.gethostname") no siempre retorna el nombre de dominio completo, usa [`getfqdn()`](https://docs.python.org/es/3.10/library/socket.html#socket.getfqdn "socket.getfqdn") para eso.

`socket.``gethostbyaddr`(_ip\_address_)

Retorna un triple `(hostname, aliaslist, ipaddrlist)` donde _hostname_ es el nombre del host primario respondiendo de la misma _ip\_address_, _aliaslist_ es una (posiblemente vacía) lista de nombres de hosts alternativa, y _ipaddrlist_ es una lista de direcciones IPV4/IPV6 para la misma interfaz y en el mismo host ( lo más probable es que contenga solo una dirección ). Para encontrar el nombre de dominio completo, use la función [`getfqdn()`](https://docs.python.org/es/3.10/library/socket.html#socket.getfqdn "socket.getfqdn"). [`gethostbyaddr()`](https://docs.python.org/es/3.10/library/socket.html#socket.gethostbyaddr "socket.gethostbyaddr") admite tanto IPv4 como IPv6.

Generar un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.gethostbyaddr` con los argumentos `ip_address`.

`socket.``getnameinfo`(_sockaddr_, _flags_)

Translate a socket address _sockaddr_ into a 2-tuple `(host, port)`. Depending on the settings of _flags_, the result can contain a fully qualified domain name or numeric address representation in _host_. Similarly, _port_ can contain a string port name or a numeric port number.

Para las direcciones IPv6, `%scope` se anexa a la parte del host si _sockaddr_ contiene _scopeid_ significativo. Generalmente esto sucede para las direcciones de multidifusión.

Para mas información sobre _flags_ pueden consultar _[getnameinfo(3)](https://manpages.debian.org/getnameinfo(3))_.

Plantea un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.getnameinfo` con el argumento `sockaddr`.

`socket.``getprotobyname`(_protocolname_)

Traduzca un nombre de protocolo de Internet (por ejemplo, `'icmp'`) a una constante adecuada para pasar como tercer argumento (opcional) a la función `socket()`. Esto normalmente sólo es necesario para sockets abiertos en modo «raw» ([`SOCK_RAW`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_RAW "socket.SOCK_RAW")); para los modos de conexión normales, el protocolo correcto se elige automáticamente si el protocolo se omite o se pone a cero.

`socket.``getservbyname`(_servicename_\[, _protocolname_\])

Traduzca un nombre de servicio de Internet y un nombre de protocolo a un número de puerto para ese servicio. El nombre de protocolo opcional, si se proporciona, debe ser `'tcp'` o `'udp'`; de lo contrario, cualquier protocolo coincidirá.

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.getservbyname` con los argumentos `servicename`, `protocolname`.

`socket.``getservbyport`(_port_\[, _protocolname_\])

Traduzca un número de puerto de Internet y un nombre de protocolo a un nombre de servicio para ese servicio. El nombre de protocolo opcional, si se proporciona, debe ser `'tcp'` o `'udp'`; de lo contrario, cualquier protocolo coincidirá.

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.getservbyport` con los argumentos `port`, `protocolname`.

`socket.``ntohl`(_x_)

Convierta enteros positivos de 32 bits de red a orden de bytes de host. En equipos donde el orden de bytes de host es el mismo que el orden de bytes de red, se trata de un no-op; de lo contrario, realiza una operación de intercambio de 4 bytes.

`socket.``ntohs`(_x_)

Convierta enteros positivos de 16 bits de red a orden de bytes de host. En equipos donde el orden de bytes de host es el mismo que el orden de bytes de red, se trata de un no-op; de lo contrario, realiza una operación de intercambio de 2 bytes.

Distinto en la versión 3.10: Lanza [`OverflowError`](https://docs.python.org/es/3.10/library/exceptions.html#OverflowError "OverflowError") si _x_ no cabe en un entero sin signo de 16 bits.

`socket.``htonl`(_x_)

Convierta enteros positivos de 32 bits del host al orden de bytes de red. En equipos donde el orden de bytes de host es el mismo que el orden de bytes de red, se trata de un no-op; de lo contrario, realiza una operación de intercambio de 4 bytes.

`socket.``htons`(_x_)

Convierta enteros positivos de 16 bits del host al orden de bytes de red. En equipos donde el orden de bytes de host es el mismo que el orden de bytes de red, se trata de un no-op; de lo contrario, realiza una operación de intercambio de 2 bytes.

Distinto en la versión 3.10: Lanza [`OverflowError`](https://docs.python.org/es/3.10/library/exceptions.html#OverflowError "OverflowError") si _x_ no cabe en un entero sin signo de 16 bits.

`socket.``inet_aton`(_ip\_string_)

Convert an IPv4 address from dotted-quad string format (for example, “123.45.67.89”) to 32-bit packed binary format, as a bytes object four characters in length. This is useful when conversing with a program that uses the standard C library and needs objects of type `in_addr`, which is the C type for the 32-bit packed binary this function returns.

Ademas ``inet_aton`acepta cadena de caracteres con menos de tres puntos, observar la pagina del manual Unix :manpage:`inet(3)()`` para mas detalles.

Si la cadena de dirección IPv4 es pasada a esta función es invalido, [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") se lanzará. Tenga en cuenta que exactamente lo que es valido depende de la implementación C de `inet_aton()`.

[`inet_aton()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_aton "socket.inet_aton") no admite IPV6, y [`inet_pton()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_pton "socket.inet_pton") deberían utilizarse en su lugar para compatibilidad con doble pilas IPV4/v6.

`socket.``inet_ntoa`(_packed\_ip_)

Convert a 32-bit packed IPv4 address (a [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object) four bytes in length) to its standard dotted-quad string representation (for example, “123.45.67.89”). This is useful when conversing with a program that uses the standard C library and needs objects of type `in_addr`, which is the C type for the 32-bit packed binary data this function takes as an argument.

Si la secuencia de byte pasada a esta función no es exactamente 4 bytes de longitud [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") podría generarse [`inet_ntoa()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_ntoa "socket.inet_ntoa") no soporta IPV6, y [`inet_ntop()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_ntop "socket.inet_ntop") debe utilizarse en su lugar para compatibilidad con doble pila IPv4 / v6.

Distinto en la versión 3.5: Ahora se acepta la grabación [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object).

`socket.``inet_pton`(_address\_family_, _ip\_string_)

Convert an IP address from its family-specific string format to a packed, binary format. [`inet_pton()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_pton "socket.inet_pton") is useful when a library or network protocol calls for an object of type `in_addr` (similar to [`inet_aton()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_aton "socket.inet_aton")) or `in6_addr`.

Los Valores soportados para _address\_family_ son actualmente [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET") y [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"). Si la cadena de dirección IP _ip\_string_ no es válida, [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") se genera. Tenga en cuenta que exactamente lo que es válido depende tanto del valor de _address\_family_ como de la implementación subyacente de `inet_pton()`.

[Disponibilidad](https://docs.python.org/es/3.10/library/intro.html#availability): Unix(Tal vez no todas las plataformas), Windows.

Distinto en la versión 3.4: Se ha añadido compatibilidad con Windows

`socket.``inet_ntop`(_address\_family_, _packed\_ip_)

Convert a packed IP address (a [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object) of some number of bytes) to its standard, family-specific string representation (for example, `'7.10.0.5'` or `'5aef:2b::8'`). [`inet_ntop()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_ntop "socket.inet_ntop") is useful when a library or network protocol returns an object of type `in_addr` (similar to [`inet_ntoa()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_ntoa "socket.inet_ntoa")) or `in6_addr`.

Los valores soportados para _address\_family_ actualmente son [`AF_INET`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET "socket.AF_INET") y [`AF_INET6`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_INET6 "socket.AF_INET6"). Si los objetos de bytes _packed\_ip_ no tienen la longitud correcta para la familia de direcciones especificas, [`ValueError`](https://docs.python.org/es/3.10/library/exceptions.html#ValueError "ValueError") podría generarse. [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") se genera para errores desde la llamada a [`inet_ntop()`](https://docs.python.org/es/3.10/library/socket.html#socket.inet_ntop "socket.inet_ntop").

[Disponibilidad](https://docs.python.org/es/3.10/library/intro.html#availability): Unix(Tal vez no todas las plataformas), Windows.

Distinto en la versión 3.4: Se ha añadido compatibilidad con Windows

Distinto en la versión 3.5: Ahora se acepta la grabación [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object).

`socket.``CMSG_LEN`(_length_)

Retorna la longitud total, sin relleno de arrastre, de un elemento de datos auxiliares con datos asociados del _length_. Este valor se puede utilizar a menudo como tamaño de búfer para [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") para recibir un solo valor de datos auxiliares, pero [**RFC 3542**](https://datatracker.ietf.org/doc/html/rfc3542.html) requiere aplicaciones portables para usar [`CMSG_SPACE()`](https://docs.python.org/es/3.10/library/socket.html#socket.CMSG_SPACE "socket.CMSG_SPACE") y así incluir espacio para el relleno, incluso cuando el elemento será el último en el búfer. Genera [`OverflowError`](https://docs.python.org/es/3.10/library/exceptions.html#OverflowError "OverflowError") si _length_ está fuera del rango de valores permitido.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): la mayoría de plataformas Unix, posiblemente otras.

Nuevo en la versión 3.3.

`socket.``CMSG_SPACE`(_length_)

Retorna el tamaño del buffer necesario por [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") para recibir un elemento de datos auxiliares con datos asociados del _length_ dado, junto con cualquier relleno final. El espacio de buffer necesario para recibir múltiples elementos es la suma de los valores de [`CMSG_SPACE()`](https://docs.python.org/es/3.10/library/socket.html#socket.CMSG_SPACE "socket.CMSG_SPACE") para los datos asociados con la longitudes. Genera [`OverflowError`](https://docs.python.org/es/3.10/library/exceptions.html#OverflowError "OverflowError") si _length_ está fuera del rango de valores permitido.

Tenga en cuenta que algunos sistemas pueden admitir datos auxiliares sin proporcionar esta función. Tenga en cuenta también que establecer el tamaño del búfer utilizando los resultados de esta función puede no limitar con precisión la cantidad de datos auxiliares que se pueden recibir, ya que los datos adicionales pueden caber en el área de relleno.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): la mayoría de plataformas Unix, posiblemente otras.

Nuevo en la versión 3.3.

`socket.``getdefaulttimeout`()

Retorna el tiempo de espera por defecto en segundos (flotante) para los objetos de un nuevo socket. Un valor de `None` indicada que los objetos del nuevo socket no tiene un tiempo de espera. Cuando el modulo socket es importado primero, por defecto es `None`.

`socket.``setdefaulttimeout`(_timeout_)

Selecciona el tiempo de espera por defecto en segundos (flotante ) para los objetos nuevos del socket. Cuando el modulo socket es importado primero, el valor por defecto es `None`. Observar [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout") para posible valores y sus respectivos significados.

`socket.``sethostname`(_name_)

Establece el nombre de host de la maquina en _name_. Esto genera un [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") si no tiene suficientes derechos.

Plantea un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.sethostname` con el argumento `name`.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Unix.

Nuevo en la versión 3.3.

`socket.``if_nameindex`()

Retorna una lista de tuplas de información de interfaz de red (índice int, cadena de nombre). [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") si se produce un error en la llamada del sistema.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Unix, Windows.

Nuevo en la versión 3.3.

Distinto en la versión 3.8: Se ha agregado compatibilidad con Windows.

Nota

En Windows las interfaces de redes tienen diferentes nombres en diferentes contextos (todos los nombres son ejemplos):

- UUID: `{FB605B73-AAC2-49A6-9A2F-25416AEA0573}`
- nombre: `ethernet_32770`
- nombre amigable: `vEthernet (nat)`
- descripción: `Hyper-V Virtual Ethernet Adapter`

Esta función retorna los nombres del segundo formulario de la lista, en este caso de ejemplo `ethernet_32770`.

`socket.``if_nametoindex`(_if\_name_)

Retorna un número de índice de interfaz de red correspondiente a un nombre de interfaz. [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") si no existe ninguna interfaz con el nombre especificado.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Unix, Windows.

Nuevo en la versión 3.3.

Distinto en la versión 3.8: Se ha agregado compatibilidad con Windows.

Ver también

“”Interface name” es un nombre como se documenta en [`if_nameindex()`](https://docs.python.org/es/3.10/library/socket.html#socket.if_nameindex "socket.if_nameindex").

`socket.``if_indextoname`(_if\_index_)

Retorna un nombre de interfaz de red correspondiente a un número de índice de interfaz. [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") si no existe ninguna interfaz con el índice dado.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Unix, Windows.

Nuevo en la versión 3.3.

Distinto en la versión 3.8: Se ha agregado compatibilidad con Windows.

Ver también

“”Interface name” es un nombre como se documenta en [`if_nameindex()`](https://docs.python.org/es/3.10/library/socket.html#socket.if_nameindex "socket.if_nameindex").

`socket.``send_fds`(_sock_, _buffers_, _fds_\[, _flags_\[, _address_\]\])

Envíe la lista de descriptores de archivo _fds_ a través de un conector [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") _sock_. El parámetro _fds_ es una secuencia de descriptores de archivo. Consulte `sendmsg()` para obtener la documentación de estos parámetros.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Soporte para Unix [`sendmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.sendmsg "socket.socket.sendmsg") con el mecanismo `SCM_RIGHTS`.

Nuevo en la versión 3.9.

`socket.``recv_fds`(_sock_, _bufsize_, _maxfds_\[, _flags_\])

Reciba descriptores de archivo hasta _maxfds_ desde un socket [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") _sock_. Retorna `(msg, list(fds), flags, addr)`. Consulte `recvmsg()` para obtener la documentación de estos parámetros.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Soporte para Unix [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") y el mecanismo `SCM_RIGHTS`.

Nuevo en la versión 3.9.

Nota

Cualquier número entero truncado al final de la lista de descriptores de archivo.

## Objetos Socket

Los objetos socket tienen los siguientes métodos. Excepto para [`makefile()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.makefile "socket.socket.makefile"), esto corresponde al sistema de llamadas Unix para sockets.

Distinto en la versión 3.2: El soporte para el protocolo [context manager](https://docs.python.org/es/3.10/glossary.html#term-context-manager) ha sido agregado. Salir del gestor de contexto es equivalente para el llamado [`close()`](https://docs.python.org/es/3.10/library/socket.html#socket.close "socket.close").

`socket.``accept`()

Acepta una conexión. El socket debe estar vinculado a una dirección y estar escuchando las conexiones. El valor de retorno es el par `(conn, address)` cuando _conn_ es un _new_ objeto socket usado para enviar y recibir información en la conexión, y _address_ es la dirección vinculada al socket en el extremo de la conexión.

El socket recién creado es [non-inheritable](https://docs.python.org/es/3.10/library/os.html#fd-inheritance).

Distinto en la versión 3.4: El socket ahora no es heredable.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``bind`(_address_)

Enlaza el socket a _address_. El socket no debe estar ya unido. (El formato de _address_ depende de la familia de direcciones, consulte más arriba).

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.getaddrinfo` con los argumentos `host`, `port`, `family`, `type`, `protocol`.

`socket.``close`()

Marca el socket cerrado. El recurso del sistema subyacente (ej. un descriptor de archivo) también se cierra cuando todos los objetos de archivo de [`makefile()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.makefile "socket.socket.makefile") están cerrados. Una vez que eso suceda, todas las operaciones futuras en el objeto socket fallarán. El extremo remoto no recibirá más datos (después de que se vacíen los datos en cola).

Los sockets se cierran automáticamente cuando se recogen basura, pero se recomienda `cerrarlos()` explícitamente, o usar una instrucción [`with`](https://docs.python.org/es/3.10/reference/compound_stmts.html#with) alrededor de ellos.

Distinto en la versión 3.6: [`OSError`](https://docs.python.org/es/3.10/library/exceptions.html#OSError "OSError") ahora se lanza si se produce un error cuando se realiza la llamada `close()` subyacente.

Nota

[`close()`](https://docs.python.org/es/3.10/library/socket.html#socket.close "socket.close") libera el recurso asociado a una conexión, pero no necesariamente cierra la conexión inmediatamente. Si desea cerrar la conexión a tiempo, llame a [`shutdown()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.shutdown "socket.socket.shutdown") antes de [`close()`](https://docs.python.org/es/3.10/library/socket.html#socket.close "socket.close").

`socket.``connect`(_address_)

Conectar a un socket remoto en _address_. (El formato de _address_ depende de la familia de direcciones — ver arriba.)

Si la conexión es interrumpida por una señal, el método espera hasta que se complete la conexión, o lanza un [`TimeoutError`](https://docs.python.org/es/3.10/library/exceptions.html#TimeoutError "TimeoutError") en el tiempo de espera, si el manejador de señales no lanza una excepción y el socket se bloquea o tiene un tiempo de espera. Para sockets sin bloqueo, el método lanza una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") si la conexión es interrumpida por una señal (o la excepción lanzada por el manejador de señales).

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.connect` con los argumentos `self`, `address`.

Distinto en la versión 3.5: El método ahora espera hasta que se completa la conexión en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") si la conexión se interrumpe por una señal, el controlador de señal no genera una excepción y el socket está bloqueando o tiene un tiempo de espera (consulte el [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la razón de ser).

`socket.``connect_ex`(_address_)

Similar a connect(address)\`, pero retorna un indicador de error en lugar de generar una excepción para los errores retornados por la llamada de nivel C `connect()` (otros problemas, como “host no encontrado”, aún pueden generar excepciones). El indicador de error es `0` si la operación tuvo éxito, caso contrario es el valor de la variable `errno`. Esto es útil para admitir, por ejemplo, conexiones asincrónicas.

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.connect` con los argumentos `self`, `address`.

`socket.``detach`()

Coloque el objeto de socket en estado cerrado sin cerrar realmente el descriptor de archivo subyacente. Se devuelve el descriptor de archivo y se puede reutilizar para otros fines.

Nuevo en la versión 3.2.

`socket.``dup`()

Duplica el socket.

El socket recién creado es [non-inheritable](https://docs.python.org/es/3.10/library/os.html#fd-inheritance).

Distinto en la versión 3.4: El socket ahora no es heredable.

`socket.``fileno`()

Retorna un archivo descriptor del socket (un entero pequeño), o -1 si falla. Esto es útil con [`select.select()`](https://docs.python.org/es/3.10/library/select.html#select.select "select.select").

En Windows el pequeño entero retornado por este método no puede ser usado donde un descriptor de un archivo pueda ser usado (como una [`os.fdopen()`](https://docs.python.org/es/3.10/library/os.html#os.fdopen "os.fdopen")). Unix no tiene esta limitación.

`socket.``get_inheritable`()

Obtiene el [inheritable flag](https://docs.python.org/es/3.10/library/os.html#fd-inheritance) del descriptor del archivo del socket o el controlador del socket: `True` si el socket puede ser heredada en procesos secundarios, `False` si falla.

Nuevo en la versión 3.4.

`socket.``getpeername`()

Retorna la dirección remota a la que esta conectado el socket. Esto es útil para averiguar el número de puerto de un socket IPv4/v6 remoto, por ejemplo. (El formato de la dirección devuelta depende de la familia de direcciones, consulte más arriba). En algunos sistemas, esta función no es compatible.

`socket.``getsockname`()

Retorna la dirección del propio socket. Esto es útil para descubrir el numero de puerto de un socket IPv4/IPv6, por ejemplo. (El formato de la dirección devuelta depende de la familia de direcciones, consulte más arriba).

`socket.``getsockopt`(_level_, _optname_\[, _buflen_\])

Retorna el valor de la opción de socket dada (consulte la página de comando man de Unix _[getsockopt(2)](https://manpages.debian.org/getsockopt(2))_). Las constantes simbólicas necesarias (`SO_*` etc.) se definen en este módulo. Si _buflen_ está ausente, se asume una opción de entero y la función retorna su valor entero. Si _buflen_ está presente, especifica la longitud máxima del búfer utilizado para recibir la opción y este búfer se devuelve como un objeto bytes. Depende del autor de la llamada descodificar el contenido del búfer (consulte el módulo integrado opcional [`struct`](https://docs.python.org/es/3.10/library/struct.html#module-struct "struct: Interpret bytes as packed binary data.") para obtener una manera de decodificar las estructuras C codificadas como cadenas de bytes).

`socket.``getblocking`()

Retorna `True` si el socket está en modo de bloqueo, `False` si está en sin bloqueo.

Esto es equivalente a comprobar `socket.gettimeout() == 0`.

Nuevo en la versión 3.7.

`socket.``gettimeout`()

Retorna el tiempo de espera en segundos (flotante) asociado con las operaciones del socket, o `None` si el tiempo de espera no es seleccionado. Esto refleja la ultima llamada al [`setblocking()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.setblocking "socket.socket.setblocking") o [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout").

`socket.``ioctl`(_control_, _option_)

plataforma

Windows

El método [`ioctl()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.ioctl "socket.socket.ioctl") es una interfaz limitada para el sistema de interfaces WSAIoctl. Por favor refiérase a [Win32 documentation](https://msdn.microsoft.com/en-us/library/ms741621%28VS.85%29.aspx) para mas información.

En otras plataformas, las funciones genéricas [`fcntl.fcntl()`](https://docs.python.org/es/3.10/library/fcntl.html#fcntl.fcntl "fcntl.fcntl") y [`fcntl.ioctl()`](https://docs.python.org/es/3.10/library/fcntl.html#fcntl.ioctl "fcntl.ioctl") podrían ser usadas; ellas aceptan un objeto socket como su primer argumento.

Actualmente solo el siguiente control de códigos está soportados: `SIO_RCVALL`, `SIO_KEEPALIVE_VALS`, y `SIO_LOOPBACK_FAST_PATH`.

Distinto en la versión 3.6: `SIO_LOOPBACK_FAST_PATH` ha sido agregado.

`socket.``listen`(\[_backlog_\])

Habilita un servidor para aceptar conexiones. Si _backlog_ es especifico, debe ser al menos 0 (si es menor, se establece en 0); especifica el número de conexiones no aceptadas que permitirá el sistema antes de rechazar nuevas conexiones. Si no se especifica, se elige un valor razonable predeterminado.

Distinto en la versión 3.5: El parámetro _backlog_ ahora es opcional.

`socket.``makefile`(_mode\='r'_, _buffering\=None_, _\*_, _encoding\=None_, _errors\=None_, _newline\=None_)

Retorna un [file object](https://docs.python.org/es/3.10/glossary.html#term-file-object) asociado con el socket. El tipo exacto retornado depende de los argumentos dados a [`makefile()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.makefile "socket.socket.makefile"). Estos argumentos se interpretan de la misma forma que la función [`open()`](https://docs.python.org/es/3.10/library/functions.html#open "open"), excepto que los únicos valores de _mode_ admitidos son `’r’` (default), `’w’` and `’b’`.

El socket debe estar en modo de bloqueo; puede tener un tiempo de espera, pero el búfer interno del objeto de archivo puede terminar en un estado incoherente si se produce un tiempo de espera.

Cerrar el objeto de archivo devuelto por [`makefile()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.makefile "socket.socket.makefile") no cerrará el socket original a menos que se hayan cerrado todos los demás objetos de archivo y [`socket.close()`](https://docs.python.org/es/3.10/library/socket.html#socket.close "socket.close") se haya llamado al objeto socket.

Nota

En Windows, el objeto similar a un archivo creado por [`makefile()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.makefile "socket.socket.makefile") no se puede utilizar cuando se espera un objeto de archivo con un descriptor de archivo, como los argumentos de secuencia de [`subprocess.Popen()`](https://docs.python.org/es/3.10/library/subprocess.html#subprocess.Popen "subprocess.Popen").

`socket.``recv`(_bufsize_\[, _flags_\])

Recibir datos del socket. El valor devuelto es un objeto bytes que representa los datos recibidos. _bufsize_ especifica la cantidad máxima de datos que se recibirán a la vez. Consulte la página del manual de Unix _[recv(2)](https://manpages.debian.org/recv(2))_ para conocer el significado del argumento opcional _flags_; por defecto es cero.

Nota

Para una mejor coincidencia con las realidades de hardware y red, el valor de _bufsize_ debe ser una potencia relativamente pequeña de 2, por ejemplo, 4096.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``recvfrom`(_bufsize_\[, _flags_\])

Recibe datos desde el socket. El valor de retorno es un par `(bytes, address)` donde _bytes_ es un objeto de bytes que representa los datos recibidos y _address_ es la dirección de el socket enviando los datos. Observar la pagina del manual Unix _[recv(2)](https://manpages.debian.org/recv(2))_ para el significado del argumento opcional _flags_; por defecto es cero. (El formato de _address_ depende de la familia de direcciones, consulte más arriba).

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

Distinto en la versión 3.7: Para direcciones IPv6 de multidifusión, el primer elemento de _address_ ya no contiene la parte `%scope_id`. Para obtener la dirección IPV6 completa, use [`getnameinfo()`](https://docs.python.org/es/3.10/library/socket.html#socket.getnameinfo "socket.getnameinfo").

`socket.``recvmsg`(_bufsize_\[, _ancbufsize_\[, _flags_\]\])

Reciba datos normales (hasta _bufsize_ bytes) y datos auxiliares del socket. El argumento _ancbufsize_ establece el tamaño en bytes del búfer interno utilizado para recibir los datos auxiliares; el valor predeterminado es 0, lo que significa que no se recibirán datos auxiliares. Los tamaños de búfer adecuados para los datos auxiliares se pueden calcular mediante [`CMSG_SPACE()`](https://docs.python.org/es/3.10/library/socket.html#socket.CMSG_SPACE "socket.CMSG_SPACE") o [`CMSG_LEN()`](https://docs.python.org/es/3.10/library/socket.html#socket.CMSG_LEN "socket.CMSG_LEN"), y los elementos que no caben en el búfer pueden truncarse o descartarse. El valor predeterminado del argumento _flags_ es 0 y tiene el mismo significado que para [`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv").

El valor de retorno es una tupla de 4: `(data, ancdata, msg_flags, address)`. El valor _data_ es un objeto [`bytes`](https://docs.python.org/es/3.10/library/stdtypes.html#bytes "bytes") que contiene los datos no auxiliares recibidos. El valor _ancdata_ es una lista de cero o mas tuplas `(cmsg_level, cmsg_type, cmsg_data)` representado los datos auxiliares (control de mensajes) recibidos: _cmsg\_level_ y _cmsg\_type_ son enteros especificando el nivel de protocolo y tipo específico de protocolo respectivamente, y _cmsg\_data_ es un objeto [`bytes`](https://docs.python.org/es/3.10/library/stdtypes.html#bytes "bytes") sosteniendo los datos asociados. El valor _msg\_flags_ es el OR bit a bit de varios indicadores que indican condiciones en el mensaje recibido; consulte la documentación de su sistema para obtener más detalles. Si la toma de recepción no está conectada, _address_ es la dirección de el socket enviado, si está disponible; de lo contrario, su valor no se especifica.

On some systems, [`sendmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.sendmsg "socket.socket.sendmsg") and [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") can be used to pass file descriptors between processes over an [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX") socket. When this facility is used (it is often restricted to [`SOCK_STREAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_STREAM "socket.SOCK_STREAM") sockets), [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") will return, in its ancillary data, items of the form `(socket.SOL_SOCKET, socket.SCM_RIGHTS, fds)`, where _fds_ is a [`bytes`](https://docs.python.org/es/3.10/library/stdtypes.html#bytes "bytes") object representing the new file descriptors as a binary array of the native C `int` type. If [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") raises an exception after the system call returns, it will first attempt to close any file descriptors received via this mechanism.

Algunos sistemas no indican la longitud truncada de los elementos de datos auxiliares que solo se han recibido parcialmente. Si un elemento parece extenderse más allá del final del búfer, [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") emitirá un [`RuntimeWarning`](https://docs.python.org/es/3.10/library/exceptions.html#RuntimeWarning "RuntimeWarning"), y devolverá la parte de él que está dentro del búfer siempre que no se haya truncado antes del inicio de sus datos asociados.

En sistemas donde soporta el mecanismo `SCM_RIGHTS`, la siguiente función recibirá un descriptor de archivos _maxfds_, devolviendo el mensaje de datos y un lista que contiene los descriptores (mientras se ignoran las condiciones inesperadas, como la recepción de mensajes de control no relacionados). Ver también [`sendmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.sendmsg "socket.socket.sendmsg").

```
<span></span><span>import</span> <span>socket</span><span>,</span> <span>array</span>

<span>def</span> <span>recv_fds</span><span>(</span><span>sock</span><span>,</span> <span>msglen</span><span>,</span> <span>maxfds</span><span>):</span>
    <span>fds</span> <span>=</span> <span>array</span><span>.</span><span>array</span><span>(</span><span>"i"</span><span>)</span>   <span># Array of ints</span>
    <span>msg</span><span>,</span> <span>ancdata</span><span>,</span> <span>flags</span><span>,</span> <span>addr</span> <span>=</span> <span>sock</span><span>.</span><span>recvmsg</span><span>(</span><span>msglen</span><span>,</span> <span>socket</span><span>.</span><span>CMSG_LEN</span><span>(</span><span>maxfds</span> <span>*</span> <span>fds</span><span>.</span><span>itemsize</span><span>))</span>
    <span>for</span> <span>cmsg_level</span><span>,</span> <span>cmsg_type</span><span>,</span> <span>cmsg_data</span> <span>in</span> <span>ancdata</span><span>:</span>
        <span>if</span> <span>cmsg_level</span> <span>==</span> <span>socket</span><span>.</span><span>SOL_SOCKET</span> <span>and</span> <span>cmsg_type</span> <span>==</span> <span>socket</span><span>.</span><span>SCM_RIGHTS</span><span>:</span>
            <span># Append data, ignoring any truncated integers at the end.</span>
            <span>fds</span><span>.</span><span>frombytes</span><span>(</span><span>cmsg_data</span><span>[:</span><span>len</span><span>(</span><span>cmsg_data</span><span>)</span> <span>-</span> <span>(</span><span>len</span><span>(</span><span>cmsg_data</span><span>)</span> <span>%</span> <span>fds</span><span>.</span><span>itemsize</span><span>)])</span>
    <span>return</span> <span>msg</span><span>,</span> <span>list</span><span>(</span><span>fds</span><span>)</span>
```

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): la mayoría de plataformas Unix, posiblemente otras.

Nuevo en la versión 3.3.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``recvmsg_into`(_buffers_\[, _ancbufsize_\[, _flags_\]\])

Recibir datos normales y datos auxiliares desde el socket, comportándose como [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg") lo haría, pero dispersar los datos no auxiliares en una serie de buffers en lugar de devolver un nuevo objeto bytes. El argumento _buffers_ debe ser un iterable de objetos que exportan buffers de escritura (por ejemplo, objetos [`bytearray`](https://docs.python.org/es/3.10/library/stdtypes.html#bytearray "bytearray")); estos se llenarán con fragmentos sucesivos de los datos no auxiliares hasta que se hayan escrito todos o no haya más buffers. El sistema operativo puede establecer un límite ([`sysconf()`](https://docs.python.org/es/3.10/library/os.html#os.sysconf "os.sysconf") valor `SC_IOV_MAX`) en el número de buffers que se pueden utilizar. Los argumentos _ancbufsize_ y _flags_ tienen el mismo significado que para [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg").

El valor de retorno es tupla de 4: `(nbytes, ancdata, msg_flags, address)`, donde _nbytes_ es el numero total de bytes de datos no auxiliares escrito dentro de los bufetes, y _ancdata_, _msg\_flags_ y _address_ son lo mismo que para [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg").

Ejemplo:

\>>>

```
<span></span><span>&gt;&gt;&gt; </span><span>import</span> <span>socket</span>
<span>&gt;&gt;&gt; </span><span>s1</span><span>,</span> <span>s2</span> <span>=</span> <span>socket</span><span>.</span><span>socketpair</span><span>()</span>
<span>&gt;&gt;&gt; </span><span>b1</span> <span>=</span> <span>bytearray</span><span>(</span><span>b</span><span>'----'</span><span>)</span>
<span>&gt;&gt;&gt; </span><span>b2</span> <span>=</span> <span>bytearray</span><span>(</span><span>b</span><span>'0123456789'</span><span>)</span>
<span>&gt;&gt;&gt; </span><span>b3</span> <span>=</span> <span>bytearray</span><span>(</span><span>b</span><span>'--------------'</span><span>)</span>
<span>&gt;&gt;&gt; </span><span>s1</span><span>.</span><span>send</span><span>(</span><span>b</span><span>'Mary had a little lamb'</span><span>)</span>
<span>22</span>
<span>&gt;&gt;&gt; </span><span>s2</span><span>.</span><span>recvmsg_into</span><span>([</span><span>b1</span><span>,</span> <span>memoryview</span><span>(</span><span>b2</span><span>)[</span><span>2</span><span>:</span><span>9</span><span>],</span> <span>b3</span><span>])</span>
<span>(22, [], 0, None)</span>
<span>&gt;&gt;&gt; </span><span>[</span><span>b1</span><span>,</span> <span>b2</span><span>,</span> <span>b3</span><span>]</span>
<span>[bytearray(b'Mary'), bytearray(b'01 had a 9'), bytearray(b'little lamb---')]</span>
```

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): la mayoría de plataformas Unix, posiblemente otras.

Nuevo en la versión 3.3.

`socket.``recvfrom_into`(_buffer_\[, _nbytes_\[, _flags_\]\])

Reciba datos del socket, escribiéndolo en _buffer_ en lugar de crear una nueva cadena de bytes. El valor devuelto es un par `(nbytes, address)` donde _nbytes_ es el número de bytes recibidos y _address_ es la dirección del socket que envía los datos. Consulte la página del manual de Unix _[recv(2)](https://manpages.debian.org/recv(2))_ para conocer el significado del argumento opcional _flags_; por defecto es cero. (El formato de _address_ depende de la familia de direcciones — ver arriba.)

`socket.``recv_into`(_buffer_\[, _nbytes_\[, _flags_\]\])

Recibe hasta _nbytes_ bytes desde el socket, almacenado los datos en un búfer en lugar de crear una nueva cadena de bytes. Si _nbytes_ no esta especificado (o 0), recibir hasta el tamaño disponible en el búfer dado. Retorna el número de bytes recibidos. Ver la página del manual de Unix _[recv(2)](https://manpages.debian.org/recv(2))_ para el significado del argumento opcional _flags_; por defecto es cero.

`socket.``send`(_bytes_\[, _flags_\])

Enviar datos al socket. El socket debe estar conectado a un socket remoto. El argumento opcional _flags_ tiene el mismo significado que para [`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") arriba. Retorna el número de bytes enviados. Las aplicaciones son responsables de comprobar que se han enviado todos los datos; si sólo se transmitieron algunos de los datos, la aplicación debe intentar la entrega de los datos restantes. Para obtener más información sobre este tema, consulte [HOW TO - Programación con sockets](https://docs.python.org/es/3.10/howto/sockets.html#socket-howto).

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``sendall`(_bytes_\[, _flags_\])

Enviar datos al socket. El socket debe estar conectado a un socket remoto. El argumento opcional _flags_ tiene el mismo significado que para [`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") arriba. A diferencia de [`send()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.send "socket.socket.send"), este método continúa enviando datos desde _bytes_ hasta que se han enviado todos los datos o se produce un error. `Ninguno` se devuelve en caso de éxito. Por error, se genera una excepción y no hay forma de determinar cuántos datos, si los hay, se enviaron correctamente.

Distinto en la versión 3.5: The socket timeout is no longer reset each time data is sent successfully. The socket timeout is now the maximum total duration to send all data.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``sendto`(_bytes_, _address_)

`socket.``sendto`(_bytes_, _flags_, _address_)

Enviar datos al socket. El socket no debe estar conectado a un socket remoto, ya que el socket de destino se especifica mediante _address_. El argumento opcional _flags_ tiene el mismo significado que para [`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") arriba. Devolver el número de bytes enviados. (El formato de _address_ depende de la familia de direcciones — ver arriba.)

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.sendto` con los argumentos `self`, `address`.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``sendmsg`(_buffers_\[, _ancdata_\[, _flags_\[, _address_\]\]\])

Enviar datos normales y auxiliares al socket, recopilar los datos no auxiliares de una serie de buffers y concatenando en un único mensaje. El argumento _buffers_ especifica los datos no auxiliares como un iterable de [bytes-como objetos](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object) (por ejemplo: objetos [`bytes`](https://docs.python.org/es/3.10/library/stdtypes.html#bytes "bytes")); el sistema operativo puede establecer un límite ([`os.sysconf()`](https://docs.python.org/es/3.10/library/os.html#os.sysconf "os.sysconf") valor `SC_IOV_MAX`) en el número de buffers que se pueden utilizar. El argumento _ancdata_ especifica los datos auxiliares (mensajes de control) como un iterable de cero o más tuplas `(cmsg_level, cmsg_type, cmsg_data)`, donde _cmsg\_level_ y _cmsg\_type_ son enteros que especifican el nivel de protocolo y el tipo específico del protocolo respectivamente, y _cmsg\_data_ es un objeto similar a bytes que contiene los datos asociados. Tenga en cuenta que algunos sistemas (en particular, sistemas sin [`CMSG_SPACE()`](https://docs.python.org/es/3.10/library/socket.html#socket.CMSG_SPACE "socket.CMSG_SPACE")) pueden admitir el envío de solo un mensaje de control por llamada. El valor predeterminado del argumento _flags_ es 0 y tiene el mismo significado que para [`send()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.send "socket.socket.send"). Si se proporciona _address_ y no `None`, establece una dirección de destino para el mensaje. El valor devuelto es el número de bytes de datos no auxiliares enviados.

La siguiente función envía la lista de descriptores de archivos _fds_ sobre un socket [`AF_UNIX`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_UNIX "socket.AF_UNIX"), estos sistemas pueden soportar la mecánica `SCM_RIGHTS`. Observar también [`recvmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recvmsg "socket.socket.recvmsg").

```
<span></span><span>import</span> <span>socket</span><span>,</span> <span>array</span>

<span>def</span> <span>send_fds</span><span>(</span><span>sock</span><span>,</span> <span>msg</span><span>,</span> <span>fds</span><span>):</span>
    <span>return</span> <span>sock</span><span>.</span><span>sendmsg</span><span>([</span><span>msg</span><span>],</span> <span>[(</span><span>socket</span><span>.</span><span>SOL_SOCKET</span><span>,</span> <span>socket</span><span>.</span><span>SCM_RIGHTS</span><span>,</span> <span>array</span><span>.</span><span>array</span><span>(</span><span>"i"</span><span>,</span> <span>fds</span><span>))])</span>
```

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): la mayoría de plataformas Unix, posiblemente otras.

Genera un [auditing event](https://docs.python.org/es/3.10/library/sys.html#auditing) `socket.sendmsg` con los argumentos `self`, `address`.

Nuevo en la versión 3.3.

Distinto en la versión 3.5: Si se interrumpe la llamada del sistema y el controlador de señal no genera una excepción, el método ahora vuelve a intentar la llamada del sistema en lugar de generar una excepción [`InterruptedError`](https://docs.python.org/es/3.10/library/exceptions.html#InterruptedError "InterruptedError") (consulte [**PEP 475**](https://www.python.org/dev/peps/pep-0475) para la lógica).

`socket.``sendmsg_afalg`(\[_msg_, \]_\*_, _op_\[, _iv_\[, _assoclen_\[, _flags_\]\]\])

Versión especializada de [`sendmsg()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.sendmsg "socket.socket.sendmsg") para el socket [`AF_ALG`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_ALG "socket.AF_ALG"). Modo de ajuste, IV, longitud de datos asociados a AEAD y banderas para el socket [`AF_ALG`](https://docs.python.org/es/3.10/library/socket.html#socket.AF_ALG "socket.AF_ALG").

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Linux >= 2.6.38.

Nuevo en la versión 3.6.

`socket.``sendfile`(_file_, _offset\=0_, _count\=None_)

Enviar un archivo hasta que se alcance EOF mediante el uso de alto rendimiento [`os.sendfile`](https://docs.python.org/es/3.10/library/os.html#os.sendfile "os.sendfile") y devolver el número total de bytes que se enviaron. _file_ debe ser un objeto de archivo normal abierto en modo binario. Si [`os.sendfile`](https://docs.python.org/es/3.10/library/os.html#os.sendfile "os.sendfile") no está disponible (por ejemplo, Windows) o _file_ no es un archivo normal [`send()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.send "socket.socket.send") se utilizará en su lugar. _offset_ indica desde dónde empezar a leer el archivo. Si se especifica, _count_ es el número total de bytes para transmitir en lugar de enviar el archivo hasta que se alcance EOF. La posición del archivo se actualiza a la vuelta o también en caso de error en cuyo caso [`file.tell()`](https://docs.python.org/es/3.10/library/io.html#io.IOBase.tell "io.IOBase.tell") se puede utilizar para averiguar el número de bytes que se enviaron. El socket debe ser de tipo [`SOCK_STREAM`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_STREAM "socket.SOCK_STREAM") No se admiten sockets sin bloqueo.

Nuevo en la versión 3.5.

`socket.``set_inheritable`(_inheritable_)

Selecciona el [inheritable flag](https://docs.python.org/es/3.10/library/os.html#fd-inheritance) descriptor del archivo del socket o el controlador del socket.

Nuevo en la versión 3.4.

`socket.``setblocking`(_flag_)

Establecer el modo de bloqueo o no bloqueo del socket: si _flag_ es false, el socket se establece en modo sin bloqueo, de lo contrario en modo de bloqueo.

El método es una abreviatura para ciertas llamadas [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout"):

- `sock.setblocking(True)` es equivalente a `sock.settimeout(None)`
- `sock.setblocking(False)` es equivalente a `sock.settimeout(0.0)`

Distinto en la versión 3.7: El método ya no aplica la bandera [`SOCK_NONBLOCK`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_NONBLOCK "socket.SOCK_NONBLOCK") en [`socket.type`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.type "socket.socket.type").

`socket.``settimeout`(_value_)

Establece un tiempo de espera para bloquear las operaciones de socket. El argumento _value_ puede ser un número de punto flotante no negativo que exprese segundos, o `None`. Si se da un valor distinto de cero, las operaciones subsiguientes de socket lanzarán una excepción [`timeout`](https://docs.python.org/es/3.10/library/socket.html#socket.timeout "socket.timeout") si el período de tiempo de espera _value_ ha transcurrido antes de que se complete la operación. Si se da cero, el socket se pone en modo sin bloqueo. Si se da `None`, el enchufe se pone en modo de bloqueo.

Para obtener más información, consulte las notas [notas sobre los tiempos de espera del socket](https://docs.python.org/es/3.10/library/socket.html#socket-timeouts).

Distinto en la versión 3.7: El método ya no cambia la bandera [`SOCK_NONBLOCK`](https://docs.python.org/es/3.10/library/socket.html#socket.SOCK_NONBLOCK "socket.SOCK_NONBLOCK") en [`socket.type`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.type "socket.socket.type").

`socket.``setsockopt`(_level_, _optname_, _value: [int](https://docs.python.org/es/3.10/library/functions.html#int "int")_)

`socket.``setsockopt`(_level_, _optname_, _value: buffer_)

`socket.``setsockopt`(_level_, _optname_, _None_, _optlen: int_)

Establece el valor de la opción de socket dada (consulte la página de manual de Unix _[setsockopt(2)](https://manpages.debian.org/setsockopt(2))_). Las constantes simbólicas necesarias se definen en el modulo [`socket`](https://docs.python.org/es/3.10/library/socket.html#module-socket "socket: Low-level networking interface.") (`SO_*` etc.). El valor puede ser un entero, `None` o un [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object) representan un buffer. En el último caso, depende de la persona que llama asegurarse de que la cadena de bytes contenga los bits adecuados (consulte el módulo integrado opcional [`struct`](https://docs.python.org/es/3.10/library/struct.html#module-struct "struct: Interpret bytes as packed binary data.") para una forma de codificar estructuras C como cadenas de bytes). Cuando _value_ se establece en `None`, el argumento _optlen_ es requerido. Esto es equivalente a llamar a una función C `setsockopt()` con `optval=NULL` y `optlen=optlen`.

Distinto en la versión 3.5: Ahora se acepta la grabación [bytes-like object](https://docs.python.org/es/3.10/glossary.html#term-bytes-like-object).

Distinto en la versión 3.6: setsockopt(level, optname, None, optlen: int) form added.

`socket.``shutdown`(_how_)

Apague una o ambas mitades de la conexión. Si _how_ es `SHUT_RD`, más recibe no se permiten. Si _how_ es `SHUT_WR`, mas recibe no se permiten. Si _how_ es `SHUT_RDWR`, más recibe no se permiten.

Duplica un socket y lo prepara para compartirlo con el proceso de destino. El proceso de destino debe estar provisto de _process\_id_. el objeto de bytes resultante luego se puede pasar al proceso de destino usando alguna forma de comunicación entre procesos y el socket se puede recrear allí usando [`fromshare()`](https://docs.python.org/es/3.10/library/socket.html#socket.fromshare "socket.fromshare"). Una vez que se ha llamado a este método, es seguro cerrar el socket ya que el sistema operativo ya lo ha duplicado para el proceso de destino.

[Availability](https://docs.python.org/es/3.10/library/intro.html#availability): Windows.

Nuevo en la versión 3.3.

Tenga en cuenta que no hay métodos `read()` o `write()`; use [`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") y [`send()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.send "socket.socket.send") sin el argumento _flags_ en su lugar.

Los objetos de socket también tienen estos atributos (de solo lectura) que corresponden a los valores dados al constructor [`socket`](https://docs.python.org/es/3.10/library/socket.html#socket.socket "socket.socket").

`socket.``family`

La familia Socket.

`socket.``type`

El tipo de socket.

`socket.``proto`

The socket protocol.

## Notas sobre los tiempos de espera del socket

Un objeto de socket puede estar en uno de los tres modos: bloqueo, no bloqueo o tiempo de espera. Los sockets se crean de forma predeterminada siempre en modo de bloqueo, pero esto se puede cambiar llamando a [`setdefaulttimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.setdefaulttimeout "socket.setdefaulttimeout").

- En el modo _bloqueo_, las operaciones se bloquean hasta que se completan o el sistema devuelve un error (como tiempo de espera de conexión agotado).
- In _non-blocking mode_, operations fail (with an error that is unfortunately system-dependent) if they cannot be completed immediately: functions from the [`select`](https://docs.python.org/es/3.10/library/select.html#module-select "select: Wait for I/O completion on multiple streams.") module can be used to know when and whether a socket is available for reading or writing.
- En _timeout mode_, las operaciones fallan si no se puede completan el tiempo de espera especifico para el socket (ellos lanzan una excepción [`timeout`](https://docs.python.org/es/3.10/library/socket.html#socket.timeout "socket.timeout")) o si el sistema devuelve un error.

Nota

En el nivel del sistema operativo, los sockets en el _timeout mode_ se establecen internamente en modo sin bloqueo. Además, los modos de bloqueo y tiempo de espera se comparten entre descriptores de archivo y objetos de socket que hacen referencia al mismo punto de conexión de red. Este detalle de implementación puede tener consecuencias visibles si, por ejemplo, decide utilizar el [`fileno()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.fileno "socket.socket.fileno") de un socket.

### Tiempos de espera y el método `connect`

La operación [`connect()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.connect "socket.socket.connect") también está sujeta a la configuración de tiempo de espera, y en general se recomienda llamar a [`settimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.settimeout "socket.socket.settimeout") antes de llamar a [`connect()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.connect "socket.socket.connect") o pasar un parámetro de tiempo de espera a [`create_connection()`](https://docs.python.org/es/3.10/library/socket.html#socket.create_connection "socket.create_connection"). Sin embargo, la pila de red del sistema también puede devolver un error de tiempo de espera de conexión propio independientemente de cualquier configuración de tiempo de espera del socket de Python.

### Tiempos de espera y el método `accept`

Si [`getdefaulttimeout()`](https://docs.python.org/es/3.10/library/socket.html#socket.getdefaulttimeout "socket.getdefaulttimeout") no es una [`None`](https://docs.python.org/es/3.10/library/constants.html#None "None"), los sockets devuelto por el método [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept") heredan ese tiempo de espera. De lo contrario, el comportamiento depende de la configuración de la toma de escucha:

- si los sockets están escuchando en _blocking mode_ o en el _timeout mode_, el socket devuelve el [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept") en un _blocking mode_;
- si los sockets están escuchando en _non-blocking mode_, ya sea el socket devuelto por [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept") es un modo de bloqueo o no bloque depende del sistema operativo. Si desea garantizar un comportamiento multiplataforma, se recomienda que se anule manualmente esta configuración.

## Ejemplo

Aquí están cuatro programas mínimos usando el protocolo TCP/IP: un servidor que hace eco de todos los datos que reciban de vuelta ( Servicio a un solo cliente), y un cliente usando esto. Recuerde que un servidor debe llevar a cabo la secuencia `socket()`, [`bind()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.bind "socket.socket.bind"), [`listen()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.listen "socket.socket.listen"), [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept") (posiblemente repitiendo la [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept") para un servicio mas que un cliente), mientras un cliente solamente necesita la secuencia `socket()`, [`connect()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.connect "socket.socket.connect"). También recuerde que el servidor no [`sendall()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.sendall "socket.socket.sendall")/[`recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") en el socket esta escuchando pero en el nuevo socket devuelto por [`accept()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.accept "socket.socket.accept").

Los dos primeros ejemplos solo admiten IPv4.

```
<span></span><span># Echo server program</span>
<span>import</span> <span>socket</span>

<span>HOST</span> <span>=</span> <span>''</span>                 <span># Symbolic name meaning all available interfaces</span>
<span>PORT</span> <span>=</span> <span>50007</span>              <span># Arbitrary non-privileged port</span>
<span>with</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_INET</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_STREAM</span><span>)</span> <span>as</span> <span>s</span><span>:</span>
    <span>s</span><span>.</span><span>bind</span><span>((</span><span>HOST</span><span>,</span> <span>PORT</span><span>))</span>
    <span>s</span><span>.</span><span>listen</span><span>(</span><span>1</span><span>)</span>
    <span>conn</span><span>,</span> <span>addr</span> <span>=</span> <span>s</span><span>.</span><span>accept</span><span>()</span>
    <span>with</span> <span>conn</span><span>:</span>
        <span>print</span><span>(</span><span>'Connected by'</span><span>,</span> <span>addr</span><span>)</span>
        <span>while</span> <span>True</span><span>:</span>
            <span>data</span> <span>=</span> <span>conn</span><span>.</span><span>recv</span><span>(</span><span>1024</span><span>)</span>
            <span>if</span> <span>not</span> <span>data</span><span>:</span> <span>break</span>
            <span>conn</span><span>.</span><span>sendall</span><span>(</span><span>data</span><span>)</span>
```

```
<span></span><span># Echo client program</span>
<span>import</span> <span>socket</span>

<span>HOST</span> <span>=</span> <span>'daring.cwi.nl'</span>    <span># The remote host</span>
<span>PORT</span> <span>=</span> <span>50007</span>              <span># The same port as used by the server</span>
<span>with</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_INET</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_STREAM</span><span>)</span> <span>as</span> <span>s</span><span>:</span>
    <span>s</span><span>.</span><span>connect</span><span>((</span><span>HOST</span><span>,</span> <span>PORT</span><span>))</span>
    <span>s</span><span>.</span><span>sendall</span><span>(</span><span>b</span><span>'Hello, world'</span><span>)</span>
    <span>data</span> <span>=</span> <span>s</span><span>.</span><span>recv</span><span>(</span><span>1024</span><span>)</span>
<span>print</span><span>(</span><span>'Received'</span><span>,</span> <span>repr</span><span>(</span><span>data</span><span>))</span>
```

Los dos ejemplos siguientes son idénticos a los dos anteriores, pero admiten IPv4 e IPv6. El lado del servidor escuchará la primera familia de direcciones disponible (debe escuchar ambas en su lugar). En la mayoría de los sistemas listos para IPv6, IPv6 tendrá prioridad y es posible que el servidor no acepte tráfico IPv4. El lado del cliente intentará conectarse a todas las direcciones devueltas como resultado de la resolución de nombres y enviará el tráfico al primero conectado correctamente.

```
<span></span><span># Echo server program</span>
<span>import</span> <span>socket</span>
<span>import</span> <span>sys</span>

<span>HOST</span> <span>=</span> <span>None</span>               <span># Symbolic name meaning all available interfaces</span>
<span>PORT</span> <span>=</span> <span>50007</span>              <span># Arbitrary non-privileged port</span>
<span>s</span> <span>=</span> <span>None</span>
<span>for</span> <span>res</span> <span>in</span> <span>socket</span><span>.</span><span>getaddrinfo</span><span>(</span><span>HOST</span><span>,</span> <span>PORT</span><span>,</span> <span>socket</span><span>.</span><span>AF_UNSPEC</span><span>,</span>
                              <span>socket</span><span>.</span><span>SOCK_STREAM</span><span>,</span> <span>0</span><span>,</span> <span>socket</span><span>.</span><span>AI_PASSIVE</span><span>):</span>
    <span>af</span><span>,</span> <span>socktype</span><span>,</span> <span>proto</span><span>,</span> <span>canonname</span><span>,</span> <span>sa</span> <span>=</span> <span>res</span>
    <span>try</span><span>:</span>
        <span>s</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>af</span><span>,</span> <span>socktype</span><span>,</span> <span>proto</span><span>)</span>
    <span>except</span> <span>OSError</span> <span>as</span> <span>msg</span><span>:</span>
        <span>s</span> <span>=</span> <span>None</span>
        <span>continue</span>
    <span>try</span><span>:</span>
        <span>s</span><span>.</span><span>bind</span><span>(</span><span>sa</span><span>)</span>
        <span>s</span><span>.</span><span>listen</span><span>(</span><span>1</span><span>)</span>
    <span>except</span> <span>OSError</span> <span>as</span> <span>msg</span><span>:</span>
        <span>s</span><span>.</span><span>close</span><span>()</span>
        <span>s</span> <span>=</span> <span>None</span>
        <span>continue</span>
    <span>break</span>
<span>if</span> <span>s</span> <span>is</span> <span>None</span><span>:</span>
    <span>print</span><span>(</span><span>'could not open socket'</span><span>)</span>
    <span>sys</span><span>.</span><span>exit</span><span>(</span><span>1</span><span>)</span>
<span>conn</span><span>,</span> <span>addr</span> <span>=</span> <span>s</span><span>.</span><span>accept</span><span>()</span>
<span>with</span> <span>conn</span><span>:</span>
    <span>print</span><span>(</span><span>'Connected by'</span><span>,</span> <span>addr</span><span>)</span>
    <span>while</span> <span>True</span><span>:</span>
        <span>data</span> <span>=</span> <span>conn</span><span>.</span><span>recv</span><span>(</span><span>1024</span><span>)</span>
        <span>if</span> <span>not</span> <span>data</span><span>:</span> <span>break</span>
        <span>conn</span><span>.</span><span>send</span><span>(</span><span>data</span><span>)</span>
```

```
<span></span><span># Echo client program</span>
<span>import</span> <span>socket</span>
<span>import</span> <span>sys</span>

<span>HOST</span> <span>=</span> <span>'daring.cwi.nl'</span>    <span># The remote host</span>
<span>PORT</span> <span>=</span> <span>50007</span>              <span># The same port as used by the server</span>
<span>s</span> <span>=</span> <span>None</span>
<span>for</span> <span>res</span> <span>in</span> <span>socket</span><span>.</span><span>getaddrinfo</span><span>(</span><span>HOST</span><span>,</span> <span>PORT</span><span>,</span> <span>socket</span><span>.</span><span>AF_UNSPEC</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_STREAM</span><span>):</span>
    <span>af</span><span>,</span> <span>socktype</span><span>,</span> <span>proto</span><span>,</span> <span>canonname</span><span>,</span> <span>sa</span> <span>=</span> <span>res</span>
    <span>try</span><span>:</span>
        <span>s</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>af</span><span>,</span> <span>socktype</span><span>,</span> <span>proto</span><span>)</span>
    <span>except</span> <span>OSError</span> <span>as</span> <span>msg</span><span>:</span>
        <span>s</span> <span>=</span> <span>None</span>
        <span>continue</span>
    <span>try</span><span>:</span>
        <span>s</span><span>.</span><span>connect</span><span>(</span><span>sa</span><span>)</span>
    <span>except</span> <span>OSError</span> <span>as</span> <span>msg</span><span>:</span>
        <span>s</span><span>.</span><span>close</span><span>()</span>
        <span>s</span> <span>=</span> <span>None</span>
        <span>continue</span>
    <span>break</span>
<span>if</span> <span>s</span> <span>is</span> <span>None</span><span>:</span>
    <span>print</span><span>(</span><span>'could not open socket'</span><span>)</span>
    <span>sys</span><span>.</span><span>exit</span><span>(</span><span>1</span><span>)</span>
<span>with</span> <span>s</span><span>:</span>
    <span>s</span><span>.</span><span>sendall</span><span>(</span><span>b</span><span>'Hello, world'</span><span>)</span>
    <span>data</span> <span>=</span> <span>s</span><span>.</span><span>recv</span><span>(</span><span>1024</span><span>)</span>
<span>print</span><span>(</span><span>'Received'</span><span>,</span> <span>repr</span><span>(</span><span>data</span><span>))</span>
```

El siguiente ejemplo muestra cómo escribir un rastreador de red muy simple con sockets sin procesar en Windows. El ejemplo requiere privilegios de administrador para modificar la interfaz:

```
<span></span><span>import</span> <span>socket</span>

<span># the public network interface</span>
<span>HOST</span> <span>=</span> <span>socket</span><span>.</span><span>gethostbyname</span><span>(</span><span>socket</span><span>.</span><span>gethostname</span><span>())</span>

<span># create a raw socket and bind it to the public interface</span>
<span>s</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_INET</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_RAW</span><span>,</span> <span>socket</span><span>.</span><span>IPPROTO_IP</span><span>)</span>
<span>s</span><span>.</span><span>bind</span><span>((</span><span>HOST</span><span>,</span> <span>0</span><span>))</span>

<span># Include IP headers</span>
<span>s</span><span>.</span><span>setsockopt</span><span>(</span><span>socket</span><span>.</span><span>IPPROTO_IP</span><span>,</span> <span>socket</span><span>.</span><span>IP_HDRINCL</span><span>,</span> <span>1</span><span>)</span>

<span># receive all packets</span>
<span>s</span><span>.</span><span>ioctl</span><span>(</span><span>socket</span><span>.</span><span>SIO_RCVALL</span><span>,</span> <span>socket</span><span>.</span><span>RCVALL_ON</span><span>)</span>

<span># receive a packet</span>
<span>print</span><span>(</span><span>s</span><span>.</span><span>recvfrom</span><span>(</span><span>65565</span><span>))</span>

<span># disabled promiscuous mode</span>
<span>s</span><span>.</span><span>ioctl</span><span>(</span><span>socket</span><span>.</span><span>SIO_RCVALL</span><span>,</span> <span>socket</span><span>.</span><span>RCVALL_OFF</span><span>)</span>
```

En el ejemplo siguiente se muestra cómo utilizar la interfaz de socket para comunicarse con una red CAN mediante el protocolo de socket sin procesar. Para utilizar CAN con el protocolo de gestor de difusión en su lugar, abra un socket con:

```
<span></span><span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_CAN</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_DGRAM</span><span>,</span> <span>socket</span><span>.</span><span>CAN_BCM</span><span>)</span>
```

After binding (`CAN_RAW`) or connecting ([`CAN_BCM`](https://docs.python.org/es/3.10/library/socket.html#socket.CAN_BCM "socket.CAN_BCM")) the socket, you can use the [`socket.send()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.send "socket.socket.send") and [`socket.recv()`](https://docs.python.org/es/3.10/library/socket.html#socket.socket.recv "socket.socket.recv") operations (and their counterparts) on the socket object as usual.

Este último ejemplo puede requerir privilegios especiales:

```
<span></span><span>import</span> <span>socket</span>
<span>import</span> <span>struct</span>

<span># CAN frame packing/unpacking (see 'struct can_frame' in &lt;linux/can.h&gt;)</span>

<span>can_frame_fmt</span> <span>=</span> <span>"=IB3x8s"</span>
<span>can_frame_size</span> <span>=</span> <span>struct</span><span>.</span><span>calcsize</span><span>(</span><span>can_frame_fmt</span><span>)</span>

<span>def</span> <span>build_can_frame</span><span>(</span><span>can_id</span><span>,</span> <span>data</span><span>):</span>
    <span>can_dlc</span> <span>=</span> <span>len</span><span>(</span><span>data</span><span>)</span>
    <span>data</span> <span>=</span> <span>data</span><span>.</span><span>ljust</span><span>(</span><span>8</span><span>,</span> <span>b</span><span>'</span><span>\x00</span><span>'</span><span>)</span>
    <span>return</span> <span>struct</span><span>.</span><span>pack</span><span>(</span><span>can_frame_fmt</span><span>,</span> <span>can_id</span><span>,</span> <span>can_dlc</span><span>,</span> <span>data</span><span>)</span>

<span>def</span> <span>dissect_can_frame</span><span>(</span><span>frame</span><span>):</span>
    <span>can_id</span><span>,</span> <span>can_dlc</span><span>,</span> <span>data</span> <span>=</span> <span>struct</span><span>.</span><span>unpack</span><span>(</span><span>can_frame_fmt</span><span>,</span> <span>frame</span><span>)</span>
    <span>return</span> <span>(</span><span>can_id</span><span>,</span> <span>can_dlc</span><span>,</span> <span>data</span><span>[:</span><span>can_dlc</span><span>])</span>

<span># create a raw socket and bind it to the 'vcan0' interface</span>
<span>s</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_CAN</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_RAW</span><span>,</span> <span>socket</span><span>.</span><span>CAN_RAW</span><span>)</span>
<span>s</span><span>.</span><span>bind</span><span>((</span><span>'vcan0'</span><span>,))</span>

<span>while</span> <span>True</span><span>:</span>
    <span>cf</span><span>,</span> <span>addr</span> <span>=</span> <span>s</span><span>.</span><span>recvfrom</span><span>(</span><span>can_frame_size</span><span>)</span>

    <span>print</span><span>(</span><span>'Received: can_id=</span><span>%x</span><span>, can_dlc=</span><span>%x</span><span>, data=</span><span>%s</span><span>'</span> <span>%</span> <span>dissect_can_frame</span><span>(</span><span>cf</span><span>))</span>

    <span>try</span><span>:</span>
        <span>s</span><span>.</span><span>send</span><span>(</span><span>cf</span><span>)</span>
    <span>except</span> <span>OSError</span><span>:</span>
        <span>print</span><span>(</span><span>'Error sending CAN frame'</span><span>)</span>

    <span>try</span><span>:</span>
        <span>s</span><span>.</span><span>send</span><span>(</span><span>build_can_frame</span><span>(</span><span>0x01</span><span>,</span> <span>b</span><span>'</span><span>\x01\x02\x03</span><span>'</span><span>))</span>
    <span>except</span> <span>OSError</span><span>:</span>
        <span>print</span><span>(</span><span>'Error sending CAN frame'</span><span>)</span>
```

Ejecutar un ejemplo varias veces con un retraso demasiado pequeño entre ejecuciones, podría dar lugar a este error:

```
<span></span><span>OSError</span><span>:</span> <span>[</span><span>Errno</span> <span>98</span><span>]</span> <span>Address</span> <span>already</span> <span>in</span> <span>use</span>
```

Esto se debe a que la ejecución anterior ha dejado el socket en un estado `TIME_WAIT` y no se puede reutilizar inmediatamente.

Este es una bandera [`socket`](https://docs.python.org/es/3.10/library/socket.html#module-socket "socket: Low-level networking interface.") para establecer, en orden para prevenir esto, `socket.SO_REUSEADDR`:

```
<span></span><span>s</span> <span>=</span> <span>socket</span><span>.</span><span>socket</span><span>(</span><span>socket</span><span>.</span><span>AF_INET</span><span>,</span> <span>socket</span><span>.</span><span>SOCK_STREAM</span><span>)</span>
<span>s</span><span>.</span><span>setsockopt</span><span>(</span><span>socket</span><span>.</span><span>SOL_SOCKET</span><span>,</span> <span>socket</span><span>.</span><span>SO_REUSEADDR</span><span>,</span> <span>1</span><span>)</span>
<span>s</span><span>.</span><span>bind</span><span>((</span><span>HOST</span><span>,</span> <span>PORT</span><span>))</span>
```

el indicador `SO_REUSEADDR` indica al kernel que reutilice un socket local en estado `TIME_WAIT`, sin esperar a que expire su tiempo de espera natural.

Ver también

Para obtener una introducción a la programación de sockets (en C), consulte los siguientes documentos:

- _An Introductory 4.3BSD Interprocess Communication Tutorial_, por Stuart Sechrest
- _An Advanced 4.3BSD Interprocess Communication Tutorial_, por Samuel J. Leffler et al,

ambos en el manual del programador de Unix, documentos suplementarios 1 ( secciones PS1:7 y PS1:8). La plataforma especifica material de referencia para las diversas llamadas al sistema también son una valiosa fuente de información en los detalles de la semántica del socket. Para Unix, referencia a las paginas del manual, para Windows, observa la especificación WinSock (o WinSock 2). Para APIS listas IPV6, los lectores pueden querer referirse al titulado Extensiones básicas de interfaz de socket para IPv6 [**RFC 3493**](https://datatracker.ietf.org/doc/html/rfc3493.html) .
