### Pila de Protocolos TCP/IP – Nota Expandida

La pila de protocolos TCP/IP es el modelo de referencia fundamental sobre el que se basa Internet. Aunque se suele comparar con el modelo OSI de siete capas, el modelo TCP/IP tiene **cuatro capas**, cada una con funciones bien definidas y protocolos específicos. A continuación se explican las capas, sus funciones y su relación con la seguridad.

#### 1. **Capa de Aplicación**

Es la más cercana al usuario y contiene los protocolos que permiten la comunicación entre aplicaciones finales.

- **Protocolos típicos**:
    - **HTTP/HTTPS**: para la web.
    - **SMTP/IMAP/POP3**: correo electrónico.
    - **FTP/SFTP**: transferencia de archivos.
    - **DNS**: resolución de nombres de dominio.
- **Seguridad**:
    - La mayoría de los protocolos de aplicación no fueron diseñados inicialmente con seguridad, por lo que hoy se usan versiones cifradas como **HTTPS (con TLS)**, **SFTP**, y **DNSSEC**.
    - Son vulnerables al **sniffing**, **inyección de comandos**, y **ataques MITM** si no se protege la comunicación.

#### 2. **Capa de Transporte**

Esta capa asegura la comunicación de extremo a extremo entre dispositivos.

- **Protocolos principales**:
    - **TCP (Transmission Control Protocol)**: Orientado a conexión, garantiza entrega ordenada y fiable de datos.
    - **UDP (User Datagram Protocol)**: No orientado a conexión, más rápido pero sin garantías de entrega o orden.
- **Seguridad**:
    - TCP es vulnerable a ataques de **spoofing**, **secuestramiento de sesión** y **SYN flood**.
    - UDP es más vulnerable a **falsificación de origen**, **DDoS** y **reflejo/amplificación**.
    - La seguridad se refuerza con mecanismos como **TLS**, que se sitúan entre la capa de aplicación y transporte.

#### 3. **Capa de Red (Internet)**

Su función es el **encaminamiento** de paquetes a través de redes interconectadas.

- **Protocolo clave**:
    - **IP (Internet Protocol)**: Versiones IPv4 e IPv6.
    - **ICMP**: Para mensajes de control y diagnóstico (como `ping`).
    - **ARP**: Traduce IP a direcciones MAC (en redes locales).
- **Seguridad**:
    - **IP no ofrece autenticación ni cifrado** por defecto.
    - Facilita ataques como **IP spoofing**, **DoS**, y manipulación de rutas.
    - Extensiones como **IPsec** proporcionan confidencialidad, autenticación e integridad.

#### 4. **Capa de Enlace (Link Layer)**

Gestiona la comunicación directa entre nodos en la misma red física.

- **Protocolos comunes**:
    - **Ethernet**
    - **Wi-Fi (IEEE 802.11)**
    - **PPP (Point-to-Point Protocol)**
- **Funciones**:
    - Dirección física (MAC)
    - Detección de errores a nivel de tramas
    - Acceso al medio (por ejemplo, control de colisiones)
- **Seguridad**:
    - Expuesta a **ataques locales** como **[[ARP SPOOFING|ARP spoofing]]**, **MAC flooding** o **sniffing** si no hay cifrado (ej. redes Wi-Fi abiertas).
    - Se emplean soluciones como **WPA3**, **filtrado de MAC**, y **segmentación VLAN** para proteger esta capa.

### Encapsulamiento y Desencapsulamiento

Cuando se envían datos:

1. En la **aplicación**, los datos se generan (por ejemplo, una petición HTTP).
2. La **capa de transporte** los divide en segmentos (TCP) o datagramas (UDP).
3. La **capa de red** encapsula el segmento dentro de un paquete IP.
4. La **capa de enlace** encapsula ese paquete IP dentro de una trama Ethernet (u otro protocolo de enlace) y lo transmite.

Al llegar al destino, se invierte el proceso (desencapsulamiento), hasta que la aplicación final recibe los datos.

### Seguridad en la pila TCP/IP

La pila TCP/IP no fue diseñada con seguridad como prioridad. Muchos ataques explotan precisamente esta falta de diseño seguro. Algunos mecanismos para reforzarla son:

- **TLS (entre aplicación y transporte)**: protege datos en tránsito.
- **IPsec (capa de red)**: protege todo el tráfico IP.
- **VPNs**: crean canales cifrados a través de redes inseguras.
- **Firewalls y sistemas IDS/IPS**: controlan y monitorean el tráfico en diferentes capas.

### Resumen visual de la pila TCP/IP

|Capa|Protocolos Ejemplo|Función Principal|
|---|---|---|
|Aplicación|HTTP, SMTP, DNS, FTP|Comunicación entre aplicaciones|
|Transporte|TCP, UDP|Entrega de datos extremo a extremo|
|Red|IP, ICMP, ARP|Encaminamiento de paquetes|
|Enlace|Ethernet, Wi-Fi|Comunicación directa en la red local|
