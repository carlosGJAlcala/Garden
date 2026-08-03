---
title: "Aplicaciones P2P"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
### Aplicaciones P2P – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Las **aplicaciones Peer-to-Peer (P2P)** se basan en una arquitectura **descentralizada**, en la que **cada dispositivo actúa como cliente y como servidor a la vez**. A diferencia del modelo cliente-servidor tradicional, donde un servidor central proporciona los recursos o servicios, en una red P2P **los nodos (peers) comparten directamente recursos entre ellos**: archivos, ancho de banda, potencia de cómputo, etc.

---

##  Características clave del modelo P2P

- **Escalabilidad natural**: cuantas más máquinas se unen, más recursos hay.
    
- **Descentralización**: no depende de un único punto central.
    
- **Distribución de carga**: cada nodo contribuye con ancho de banda y almacenamiento.
    
- **Resiliencia**: si un nodo cae, los demás siguen operativos.
    
- **Autonomía**: los usuarios pueden controlar qué comparten y cuándo.
    

---

##  Aplicaciones populares P2P (históricas y actuales)

###  1. **Intercambio de archivos**

|Aplicación|Características|
|---|---|
|**Napster** (1999)|Modelo P2P híbrido con servidor central de indexado.|
|**Gnutella**|Red completamente descentralizada (por ejemplo, LimeWire, FrostWire).|
|**BitTorrent**|Divide los archivos en partes pequeñas, que se comparten entre pares. Muy eficiente.|
|**eDonkey / eMule**|Sistema basado en servidores y red Kademlia (P2P pura).|

###  2. **Streaming y VoIP**

|Aplicación|Características|
|---|---|
|**Skype (versiones iniciales)**|Usaba P2P para enrutar llamadas y transferencias.|
|**Zoom, Teams (componentes P2P)**|En algunas situaciones usan P2P entre usuarios en la misma red.|
|**PeerTube**|Plataforma descentralizada de vídeo basada en WebTorrent.|

###  3. **Mensajería descentralizada**

|Aplicación|Características|
|---|---|
|**Tox**|Protocolo cifrado y descentralizado de mensajería y videollamadas.|
|**Ricochet**|Usaba la red Tor como canal P2P para mensajería anónima.|

###  4. **Distribución de cómputo**

|Proyecto|Uso P2P|
|---|---|
|**SETI@Home**|Computación distribuida con millones de nodos analizando datos astronómicos.|
|**Folding@Home**|Investigación biomédica distribuida.|
|**BOINC**|Framework general para proyectos científicos con arquitectura P2P.|

###  5. **Redes blockchain y Web3**

|Proyecto|Tipo P2P|
|---|---|
|**Bitcoin, Ethereum**|Cada nodo mantiene una copia del libro contable y valida transacciones.|
|**IPFS (InterPlanetary File System)**|Sistema de archivos descentralizado, P2P puro.|
|**Bitmessage**|Protocolo de correo electrónico cifrado basado en P2P.|

---

##  Ejemplo práctico: cómo funciona BitTorrent

1. Un archivo grande se divide en bloques.
    
2. El _tracker_ (opcional) ayuda a encontrar otros pares.
    
3. Los usuarios (seeders y leechers) se conectan entre sí.
    
4. Cada parte del archivo se intercambia entre los peers.
    
5. Al final, cada peer tiene una copia completa y puede seguir compartiéndola.
    

> Ventaja: **descargas más rápidas y eficientes**, ya que no dependen de un único servidor.

---

##  Consideraciones de seguridad en P2P

- **Difícil control de contenido**: distribución de malware, material ilegal.
    
- **Anonimato relativo**: cada peer expone su IP a otros.
    
- **Dificultad para aplicar censura o moderación**.
    
- **Ataques de flooding o envenenamiento de recursos**.
    

---

##  Ventajas del modelo P2P

- Alta escalabilidad.
    
- Reducción de costes (sin servidores centrales).
    
- Mayor tolerancia a fallos.
    
- Ideal para redes comunitarias, proyectos open source, y contenido descentralizado.
    

---

##  Desventajas

- Difícil garantizar la calidad del servicio (QoS).
    
- Problemas legales si se usa para distribuir contenido protegido.
    
- Complejidad en el control y gestión de la red.
    
- Consumo de recursos en los dispositivos de los usuarios.
    

---

### Conclusión

Las aplicaciones P2P **cambian la lógica tradicional de cliente-servidor**, permitiendo a cada usuario participar como igual en la red. Desde el intercambio de archivos hasta la computación distribuida y las blockchains, el modelo P2P **sigue siendo esencial en la evolución de Internet**, especialmente en entornos donde **la descentralización y la resistencia a la censura son prioritarias**.

---