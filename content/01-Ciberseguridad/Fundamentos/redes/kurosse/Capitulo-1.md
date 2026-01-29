---
title: "Capitulo 1"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - redes
---

**Introducción a Redes de Computadoras: Un Enfoque de Arriba hacia Abajo, 5ª edición**  
Autores: Jim Kurose, Keith Ross  
Editorial: Addison-Wesley, Abril 2009  

#### Nota sobre el uso de estas diapositivas  

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Redes/Aplicaciones-P2P|Aplicaciones P2P]]. [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]].

Se ofrecen estas diapositivas de forma gratuita para su uso por profesores, estudiantes y lectores. Están en formato PowerPoint, permitiendo agregar, modificar o eliminar contenido según sea necesario. Sin embargo, solicitamos lo siguiente:  

1. Si las usa en su forma sustancialmente original (por ejemplo, en clases), mencione la fuente. Esto apoya la difusión del libro.  
2. Si publica estas diapositivas sin modificaciones importantes en un sitio web, indique que han sido adaptadas de nuestro material, mencionando los derechos de autor.  

**¡Gracias y disfruten!**  
*JFK/KWR*  
**Derechos de autor 1996-2009, J.F. Kurose y K.W. Ross. Todos los derechos reservados.**  

---

### Hoja de ruta del capítulo 1  
1.1 ¿Qué es Internet?  
1.2 El borde de la red  
   - Sistemas finales, redes de acceso, enlaces  
1.3 El núcleo de la red  
   - Conmutación por circuitos y paquetes, estructura de la red  
1.4 Retrasos, pérdida y rendimiento en redes de paquetes  
1.5 Capas de protocolo, modelos de servicio  
1.6 Redes bajo ataque: seguridad  

---

### Retrasos y pérdida en redes conmutadas por paquetes  
#### ¿Cómo ocurren los retrasos y pérdidas?  
- Los paquetes se encolan en los búferes de los routers.  
- Si la tasa de llegada de paquetes supera la capacidad del enlace, los paquetes se encolan o se pierden si no hay búfer disponible.  

**Fuentes de retraso en paquetes:**  
1. **Procesamiento nodal:**  
   - Verificación de errores.  
   - Determinación del enlace de salida.  
2. **Colas:**  
   - Tiempo de espera en el enlace de salida.  
   - Depende del nivel de congestión.  
3. **Retraso de transmisión:**  
   - Tiempo para enviar bits al enlace: \( t = \frac{L}{R} \) (donde \( L \) es la longitud del paquete en bits y \( R \) es el ancho de banda en bps).  
4. **Retraso de propagación:**  
   - Distancia \( d \) dividida por la velocidad de propagación \( s \).  

---

### Encapsulación y modelo en capas de protocolos  
**Modelo de capas:**  
1. **Aplicación:** Soporte para aplicaciones de red (HTTP, SMTP).  
2. **Transporte:** Transferencia de datos entre procesos (TCP, UDP).  
3. **Red:** Enrutamiento de datagramas (IP).  
4. **Enlace:** Transferencia entre elementos vecinos (Ethernet).  
5. **Física:** Bits en el medio físico.  

---

### Seguridad en redes  
El campo de la seguridad en redes aborda cómo proteger las redes frente a ataques. Algunos ejemplos incluyen:  
- Malware (virus, gusanos, troyanos).  
- Redes zombi utilizadas para ataques DDoS.  
- Sniffing de paquetes.  

**Denegación de servicio (DoS):**  
Los atacantes sobrecargan un recurso, como un servidor o ancho de banda, con tráfico falso.  

---

### Referencias en formato Markdown  
```markdown
### Referencias  
1. Kurose, J., & Ross, K. (2009). *Computer Networking: A Top-Down Approach (5th ed.)*. Addison-Wesley.  
2. "Retrasos en redes de paquetes." Adaptado de diapositivas de Kurose y Ross, 2009.  
3. "Seguridad en redes: amenazas y soluciones." Basado en el material de Kurose y Ross, 2009.  
```

### Capítulo 2  
**Capa de Aplicación**  
**Redes de Computadoras: Un Enfoque Descendente, 5ª edición**  
Autores: Jim Kurose, Keith Ross  
Editorial: Addison-Wesley, abril de 2009  

### Contenido del Capítulo 2: Capa de Aplicación  
1. **Principios de aplicaciones de red**  
2. **Web y HTTP**  
3. **FTP (Protocolo de Transferencia de Archivos)**  
4. **Correo electrónico** (SMTP, POP3, IMAP)  
5. **DNS (Sistema de Nombres de Dominio)**  
6. **Aplicaciones P2P (Peer-to-Peer)**  
7. **Programación de sockets con UDP**  
8. **Programación de sockets con TCP**  

---

### **Objetivos del capítulo:**  
- Entender aspectos conceptuales e implementaciones de los protocolos de aplicación.  
  - Modelos de servicio de capa de transporte.  
  - Paradigma cliente-servidor y P2P.  
- Analizar protocolos de aplicación populares como HTTP, FTP, SMTP, POP3, IMAP y DNS.  
- Aprender a programar aplicaciones de red usando APIs de sockets.  

---

### **Arquitecturas de aplicaciones de red:**  
1. **Cliente-servidor:**  
   - Un servidor está siempre activo, con una dirección IP permanente.  
   - Los clientes se conectan al servidor, pueden tener direcciones IP dinámicas y no interactúan entre sí directamente.  
2. **Peer-to-Peer (P2P):**  
   - No depende de servidores siempre activos.  
   - Los nodos actúan como clientes y servidores, comunicándose directamente entre ellos.  
   - Es altamente escalable pero más complejo de gestionar.  
3. **Híbrido (cliente-servidor + P2P):**  
   - Ejemplo: Skype utiliza servidores centrales para localizar pares y conexiones P2P directas para comunicación.  

---

### **Procesos y comunicación:**  
- **Proceso:** Programa en ejecución dentro de un host.  
- Los procesos en diferentes hosts se comunican intercambiando **mensajes**.  
  - **Proceso cliente:** Inicia la comunicación.  
  - **Proceso servidor:** Espera para ser contactado.  
- **Sockets:** Interfaz para enviar y recibir mensajes a través de la red.  

---

### **Protocolos de capa de aplicación**  
Un protocolo de aplicación define:  
- Los tipos de mensajes intercambiados (solicitudes, respuestas).  
- La sintaxis y semántica de los mensajes.  
- Las reglas para enviar y responder mensajes.  

---

### **Protocolos comunes y requisitos de transporte:**  
| Aplicación               | Pérdida de datos | Sensibilidad al tiempo | Ancho de banda necesario | Protocolo de transporte |  
|--------------------------|------------------|-------------------------|---------------------------|--------------------------|  
| Transferencia de archivos| No tolera        | No                     | Elástico                 | TCP                      |  
| Correo electrónico       | No tolera        | No                     | Elástico                 | TCP                      |  
| Streaming multimedia     | Tolerante        | Sí, algunos segundos   | 10 kbps - 5 Mbps         | TCP/UDP                  |  
| Juegos interactivos      | Tolerante        | Sí, cientos de ms      | Baja                     | UDP                      |  

---

### **HTTP (Protocolo de Transferencia de Hipertexto):**  
- Protocolo de capa de aplicación para la web.  
- **Modelo cliente-servidor:**  
  - **Cliente:** Navegador que solicita y muestra contenido web.  
  - **Servidor:** Entrega objetos web en respuesta a solicitudes.  

**Tipos de conexiones HTTP:**  
- **No persistentes:** Cada objeto requiere una nueva conexión TCP.  
- **Persistentes:** Todos los objetos pueden transferirse en una sola conexión TCP.  
## 2.3 FTP

**FTP: Protocolo de transferencia de archivos**

- Permite transferir archivos entre sistemas.
- Utiliza dos conexiones: una para comandos y otra para la transferencia de datos.

Relacionado: [Criterios para elegir servicios de transporte](#2.6-aplicaciones-p2p).

---

## 2.4 Correo electrónico

Protocolos:

- **SMTP (Simple Mail Transfer Protocol)**: Envío de correos.
- **POP3** y **IMAP**: Recuperación de correos.

Consulta también la sección sobre [protocolos populares](#2.6-aplicaciones-p2p).

---

## 2.5 DNS

**DNS: Sistema de nombres de dominio**

- Traduce nombres de dominio (por ejemplo, `www.google.com`) a direcciones IP.
- Funciona en un modelo cliente-servidor.

Más sobre DNS en [Protocolos populares](#2.6-aplicaciones-p2p).

---

## 2.6 Aplicaciones P2P

**Arquitecturas P2P (peer-to-peer)**

- No existe un servidor permanente.
- Comunicación directa entre sistemas finales.
- Ejemplo: Skype.

Consulta más en [Principios de aplicaciones de red](#2.1-principios-de-las-aplicaciones-de-red).

---

## 2.7 Programación de sockets con UDP

- **UDP**: Protocolo simple y sin conexión.
- Ejemplo: Aplicaciones multimedia como transmisión de video.

Relacionado: [Programación de sockets](#2.8-programaci%C3%B3n-de-sockets-con-tcp).

---

## 2.8 Programación de sockets con TCP

- **TCP**: Protocolo orientado a conexión.
- Características:
    - Control de flujo.
    - Retransmisión confiable.
    - Uso en aplicaciones como HTTP, FTP y SMTP.

Para más detalles sobre TCP, consulta la [Capa de Transporte](#cap%C3%ADtulo-3-capa-de-transporte).

Voy a continuar con el **Capítulo 3: Capa de Transporte**, basado en el documento proporcionado. El texto estará traducido, formateado en Markdown, y con enlaces cruzados a otras secciones cuando corresponda.  

---

## Capítulo 3: Capa de Transporte  

**Fuente:**  
*Computer Networking: A Top-Down Approach, 5ª edición*  
Autores: Jim Kurose, Keith Ross.  
Editorial: Addison-Wesley, abril de 2009.

---

### Contenidos principales  

- **3.1 Introducción a la capa de transporte**  
  La capa de transporte proporciona servicios de comunicación lógica entre procesos de aplicación que se ejecutan en diferentes sistemas finales.  
  - Servicios clave:  
    - **Multiplexación y demultiplexación.**  
    - **Transferencia confiable de datos.**  
    - **Control de flujo.**  
    - **Control de congestión.**  

---

### **3.2 Protocolo UDP (User Datagram Protocol)**  

- **Características principales:**  
  - Protocolo sin conexión y no confiable.  
  - No garantiza entrega, orden o corrección de datos.  
  - Se usa en aplicaciones sensibles a la latencia como transmisión de video y voz en tiempo real.  
- **Ventajas:**  
  - Baja sobrecarga de red.  
  - Mayor velocidad en comparación con TCP.  

#### Ejemplos de uso:  
- DNS (Sistema de Nombres de Dominio).  
- Streaming de video.  
- Juegos en línea.  

Consulta la sección sobre [programación de sockets con UDP](#2.7-programación-de-sockets-con-udp) en la Capa de Aplicación.  

---

### **3.3 Protocolo TCP (Transmission Control Protocol)**  

- **Características principales:**  
  - Orientado a conexión.  
  - Garantiza la entrega de datos y mantiene el orden.  
  - Implementa control de flujo y congestión.  
- **Ventajas:**  
  - Fiabilidad en la transmisión.  
  - Adecuado para aplicaciones que requieren precisión, como transferencia de archivos y correo electrónico.  

#### Ejemplos de uso:  
- HTTP (Protocolo de Transferencia de Hipertexto).  
- FTP (Protocolo de Transferencia de Archivos).  
- SMTP (Protocolo Simple de Transferencia de Correo).  

---

### **3.4 Multiplexación y demultiplexación**  

- **Multiplexación:** Permite que múltiples aplicaciones compartan el mismo enlace físico de red.  
- **Demultiplexación:** Entrega los datos al proceso de aplicación correcto en el sistema final de destino.  

**Identificadores clave:**  
- Dirección IP del host.  
- Número de puerto de la aplicación (ejemplo: puerto 80 para HTTP).  

Para más detalles, consulta el apartado sobre [encapsulación de mensajes](#capítulo-4-capa-de-red).

---

### **3.5 Control de flujo y congestión**  

- **Control de flujo:** Asegura que el receptor no sea abrumado por datos del emisor.  
- **Control de congestión:** Reduce la velocidad de transmisión cuando la red está sobrecargada.  

#### Algoritmos de control de congestión en TCP:  
- **Ventana deslizante (Sliding Window):** Regula la cantidad de datos enviados antes de esperar confirmación.  
- **Slow Start:** Incrementa la velocidad de transmisión progresivamente hasta detectar congestión.  

---

### **Referencias cruzadas**  

- [Capítulo 1: Introducción](#capítulo-1-introducción).  
- [Capítulo 2: Capa de Aplicación](#capítulo-2-capa-de-aplicación).  
- [Capítulo 4: Capa de Red](#capítulo-4-capa-de-red).  

---
### **Capítulo 4: Capa de Red**  

**Fuente:**  
*Computer Networking: A Top-Down Approach, 5ª edición*  
Autores: Jim Kurose, Keith Ross.  
Editorial: Addison-Wesley, abril de 2009.

---

### Contenidos principales  

- **4.1 Introducción a la capa de red**  
  - Proporciona servicios de comunicación lógica entre **hosts** (no procesos individuales).  
  - Funciones clave:  
    - **Enrutamiento:** Determina la trayectoria para los paquetes desde el origen hasta el destino.  
    - **Conmutación:** Mueve los paquetes a través de los routers hacia su destino.  

- **4.2 Modelos de servicios de la capa de red**  
  - **Servicios orientados a conexión:** Garantizan entrega confiable y ordenada.  
  - **Servicios sin conexión:** No garantizan fiabilidad ni orden, pero ofrecen menor sobrecarga.  

Consulta la [Capa de Transporte](#capítulo-3-capa-de-transporte) para más detalles sobre los servicios orientados a conexión.

---

### **4.3 Conmutación en la capa de red**  

- **Conmutación por circuitos:**  
  - Reservan recursos específicos para una conexión.  
  - Ofrecen garantías de ancho de banda, pero son menos flexibles.  

- **Conmutación por paquetes:**  
  - Los datos se dividen en paquetes independientes que pueden tomar rutas diferentes.  
  - Más eficiente en redes compartidas.  

Relacionado: Más información sobre la [estructura del núcleo de la red](#1.2-el-núcleo-de-la-red).

---

### **4.4 Algoritmos de enrutamiento**  

Los algoritmos de enrutamiento determinan las trayectorias de los paquetes:  
- **Estáticos:** Las rutas se configuran manualmente y cambian poco.  
- **Dinámicos:** Las rutas se actualizan automáticamente en función del estado de la red.  

#### Ejemplos de algoritmos:  
1. **Enrutamiento por vector de distancia:**  
   - Cada nodo comparte información sobre las distancias a los destinos.  
   - Ejemplo: RIP (Routing Information Protocol).  
2. **Enrutamiento por estado de enlace:**  
   - Cada nodo construye un mapa completo de la red y calcula las mejores rutas.  
   - Ejemplo: OSPF (Open Shortest Path First).  

---

### **4.5 Protocolo IP y direcciones**  

- **Protocolo IP:** Base de la capa de red en Internet.  
  - Define el formato de los paquetes (datagramas IP).  
  - Es un protocolo **sin conexión** y **no confiable**.  

#### Direccionamiento IP:  
- Direcciones IP son únicas para cada host.  
- **IPv4:** 32 bits, formato decimal (ejemplo: 192.168.1.1).  
- **IPv6:** 128 bits, diseñado para resolver la escasez de direcciones en IPv4.  

Más detalles sobre el [DNS](#2.5-dns) para traducir nombres de dominio a direcciones IP.

---

### **4.6 NAT (Traducción de direcciones de red)**  

- Permite que múltiples dispositivos compartan una sola dirección IP pública.  
- Traduce las direcciones privadas a direcciones públicas en el router.  
- Problemas: rompe la transparencia extremo a extremo en redes.  

---

### **4.7 ICMP (Protocolo de mensajes de control de Internet)**  

- **ICMP** se utiliza para enviar mensajes de diagnóstico y error entre hosts y routers.  
- Ejemplo:  
  - Mensajes de *ping* para verificar la conectividad entre dispositivos.  

---

### **4.8 Protocolos de enrutamiento intra e interdominio**  

- **Enrutamiento intradominio:**  
  - Algoritmos utilizados dentro de una red autónoma (ejemplo: RIP, OSPF).  

- **Enrutamiento interdominio:**  
  - Coordina el tráfico entre diferentes redes autónomas (ejemplo: BGP).  

Relacionado: Más sobre [control de congestión](#3.5-control-de-flujo-y-congestión) en la capa de transporte.

---

### Referencias cruzadas  

- [Capítulo 1: Introducción](#capítulo-1-introducción).  
- [Capítulo 3: Capa de Transporte](#capítulo-3-capa-de-transporte).  
- [Capítulo 5: Capa de Enlace de Datos y Redes Locales](#capítulo-5-capa-de-enlace-de-datos-y-redes-locales).  

---

### **Capítulo 5: Capa de Enlace de Datos y Redes Locales**  

**Fuente:**  
*Computer Networking: A Top-Down Approach, 5ª edición*  
Autores: Jim Kurose, Keith Ross.  
Editorial: Addison-Wesley, abril de 2009.  

---

### Contenidos principales  

- **5.1 Introducción a la capa de enlace de datos**  
  - Proporciona comunicación confiable entre nodos directamente conectados.  
  - Encapsula paquetes de la capa de red en **tramas (frames)**.  
  - Detecta y corrige errores de transmisión.  

Consulta la sección sobre [encapsulación en la capa de red](#4.5-protocolo-ip-y-direcciones) para entender el flujo completo de los datos.  

---

### **5.2 Servicios de la capa de enlace de datos**  

- **Detección de errores:**  
  - Identifica errores en los datos transmitidos mediante sumas de comprobación (*checksums*).  
- **Corrección de errores:**  
  - Permite recuperar datos dañados mediante algoritmos como códigos de redundancia cíclica (CRC).  
- **Control de flujo:**  
  - Garantiza que el transmisor no abrume al receptor.  

Relacionado: Más información en [control de flujo en la capa de transporte](#3.5-control-de-flujo-y-congestión).

---

### **5.3 Protocolos de acceso al medio (MAC)**  

- En redes donde varios nodos comparten el mismo medio físico, los protocolos MAC controlan el acceso.  
- **Tipos de protocolos MAC:**  
  1. **Acceso aleatorio:**  
     - Ejemplo: CSMA/CD (Carrier Sense Multiple Access with Collision Detection) en Ethernet.  
  2. **Acceso controlado:**  
     - Los nodos acceden al medio siguiendo un orden predeterminado (ejemplo: paso de testigo en redes token).  
  3. **División del canal:**  
     - Divide el medio en múltiples canales físicos o lógicos.  

---

### **5.4 Ethernet**  

- **Ethernet** es el estándar más utilizado en redes locales (LAN).  
- Características principales:  
  - Tecnología de difusión.  
  - Utiliza **CSMA/CD** para acceso al medio.  
  - Ofrece velocidades desde 10 Mbps hasta 400 Gbps.  

---

### **5.5 Redes inalámbricas y Wi-Fi**  

- **802.11 (Wi-Fi):** Protocolo estándar para redes locales inalámbricas (WLAN).  
  - Utiliza puntos de acceso (*access points*) para conectar dispositivos.  
- **Problemas únicos de redes inalámbricas:**  
  - **Colisiones ocultas:** Los nodos no siempre pueden detectar otros transmisores en la red.  
  - **Desvanecimiento de señales:** La calidad de la señal puede variar debido a interferencias.  

---

### **5.6 Conmutadores de capa de enlace**  

- **Switches:** Dispositivos que conectan múltiples dispositivos en una red local.  
  - Usan **tablas de conmutación** para determinar el puerto al que deben reenviar las tramas.  
- Beneficios:  
  - Mejoran el rendimiento al reducir colisiones.  
  - Permiten redes más grandes al dividir dominios de colisión.  

---

### **5.7 Redes locales virtuales (VLANs)**  

- Las **VLANs** permiten dividir una red física en varias subredes lógicas.  
  - Ventajas:  
    - Mejora la seguridad al aislar grupos de dispositivos.  
    - Reduce la congestión al segmentar el tráfico.  
  - Implementación común en conmutadores y routers de nivel empresarial.  

Consulta la sección sobre [enrutamiento en redes](#4.4-algoritmos-de-enrutamiento) para entender cómo las VLANs interactúan con las capas superiores.

---

### Referencias cruzadas  

- [Capítulo 3: Capa de Transporte](#capítulo-3-capa-de-transporte).  
- [Capítulo 4: Capa de Red](#capítulo-4-capa-de-red).  
- [Capítulo 6: Seguridad en Redes](#capítulo-6-seguridad-en-redes).  

---

¿Continuamos con el **Capítulo 6: Seguridad en Redes**? 