---
title: "2024 12 19 Redes Wifi"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

A continuación, el texto reformulado incluye las referencias a las imágenes en formato Markdown:

---

**Wi-Fi y Redes Inalámbricas**

Las redes Wi-Fi son sistemas de comunicación inalámbrica que permiten la conexión entre dispositivos sin la necesidad de cables físicos. Estas redes pueden operar principalmente en dos modos:

1. **Redes Ad-Hoc (punto a punto):**  
    En este modo, los dispositivos (clientes) se comunican directamente entre sí, sin la necesidad de un punto de acceso central. Resulta útil en situaciones donde no se dispone de una infraestructura preestablecida, ya que cada equipo actúa como emisor y receptor.
    
2. **Redes con Infraestructura:**  
    En este modo, los dispositivos clientes se conectan de forma inalámbrica a un punto de acceso (AP, por sus siglas en inglés). El punto de acceso, a su vez, conecta a los clientes entre sí y con la red cableada o el router principal que da salida a Internet. Este es el modo más utilizado en entornos domésticos, empresariales y públicos, ya que centraliza el control y facilita la gestión de la red.
    

---

**Multiplexación en Frecuencia y Canales Wi-Fi**

La tecnología Wi-Fi se basa en la utilización de bandas de frecuencia estandarizadas, principalmente 2,4 GHz y 5 GHz.

- **Banda de 2,4 GHz:**  
    Esta banda se divide en canales que normalmente van del 1 al 13, aunque en algunos países, como Japón, se permite el canal 14. A pesar de esta numeración, en muchos lugares solo se utilizan los canales del 1 al 11. Debido a que las señales en 2,4 GHz se superponen, es recomendable usar canales que no se solapen, como el 1, 6 y 11, para minimizar interferencias.
    
- **Banda de 5 GHz:**  
    Esta banda ofrece más canales (por ejemplo, el canal 36 y muchos otros en rangos superiores) y menor interferencia, lo que se traduce en un mejor rendimiento y más estabilidad en entornos congestionados.
    

**Terminología:**

- **Cliente = STA (Station):** Dispositivo final que se conecta a la red Wi-Fi (ej. un teléfono, una laptop).
- **Punto de Acceso = AP (Access Point):** Dispositivo que proporciona el acceso inalámbrico a la red.
- **ESSID (Extended Service Set Identifier):** Nombre de la red Wi-Fi que se muestra a los usuarios para su selección.
- **BSSID (Basic Service Set Identifier):** Dirección MAC del punto de acceso que identifica de forma única cada AP en la red.

El BSSID se utiliza para identificar el punto de acceso en el enlace inalámbrico. La dirección MAC del AP es su identidad en la red, y a veces puede “enmascararse” o suplementarse para mejorar la seguridad.

---

**Seguridad en Wi-Fi: Evolución de Protocolos**

A lo largo del tiempo, la seguridad en las redes inalámbricas ha ido evolucionando:

- **WEP (Wired Equivalent Privacy):**  
    Fue uno de los primeros protocolos de seguridad Wi-Fi. Resultó ser sumamente inseguro debido a vulnerabilidades que permiten descifrar la clave en pocos minutos.
    
- **WPA y WPA2 (Wi-Fi Protected Access):**  
    WPA mejoró respecto a WEP, y WPA2 fue durante mucho tiempo considerado un estándar seguro. Sin embargo, con el tiempo y el incremento de la potencia computacional, se han encontrado vulnerabilidades en WPA2.
    
    - **WPA2 Personal (PSK - Pre-Shared Key):**  
        Utiliza una clave previamente compartida (una contraseña) para autenticación. Es el tipo más común en entornos domésticos, pero es susceptible a ataques de diccionario contra la clave.
    - **WPA2 Enterprise:**  
        Emplea autenticación basada en certificados y un servidor RADIUS, lo que reduce la superficie de ataque, ya que no depende de una única contraseña compartida, sino de credenciales individuales o certificados digitales. Es más seguro para entornos empresariales.
- **WPA3:**  
    Es la versión más reciente, que incorpora mecanismos más robustos, como la autenticación basada en SAE (Simultaneous Authentication of Equals, una variante de Diffie-Hellman autenticado). Esto dificulta los ataques de fuerza bruta y de diccionario, ya que no se revela información crítica como la que se filtraba en WPA2. Aun así, su adopción es lenta.
    

---

**Tramas de Gestión (Management Frames)**

En las redes Wi-Fi, además de las tramas de datos, existen las tramas de gestión, que se transmiten en texto claro a nivel físico, facilitando ciertas operaciones y estados de la red. Estas tramas cumplen funciones como anunciar la red, iniciar y finalizar conexiones, e intercambiar información de autenticación y asociación. Algunas de las tramas de gestión más comunes son:

- **Beacon Frame (Baliza):**  
    El AP las envía periódicamente anunciando su presencia, ESSID, parámetros de la red, etc.
    
- **Probe Request / Probe Response (Sonda):**  
    Permiten a un cliente buscar redes disponibles. Un Probe Request puede ser dirigido (buscando una red específica) o en broadcast (buscando cualquier red).
    
- **Authentication Request/Response:**  
    Gestionan el proceso inicial de autenticación entre el cliente y el AP.
    
- **Association Request/Response:**  
    Una vez autenticado, el cliente solicita asociarse a la red, y el AP responde otorgándole la conexión.
    
- **Deauthentication y Disassociation:**  
    Tramas que indican el fin de la autenticación o de la asociación entre un cliente y el AP.
    

Estas tramas, cuando no están protegidas, pueden ser utilizadas por atacantes para recopilar información (por ejemplo, ubicaciones potenciales, ESSIDs) o para enviar solicitudes maliciosas (como deauth attacks, que expulsan dispositivos de la red).

Para mitigar estos problemas se introdujo el estándar 802.11w (Protected Management Frames), que cifra y protege determinadas tramas de gestión evitando la desconexión forzada de clientes.

![[Pasted image 20241219164248.png]]  
![[Captura desde 2024-12-19 16-44-13.png]]  
![[Pasted image 20241219165419.png]]

---

**Handshake en WPA2 Personal**

En WPA2 Personal, se realiza un handshake (intercambio de claves) de cuatro pasos para generar las claves temporales que cifran la comunicación. A partir de la contraseña (PSK) y el ESSID, se deriva la PMK (Pairwise Master Key) usando funciones hash (por ejemplo, PBKDF2-HMAC-SHA1 con 4096 iteraciones). Luego, la PMK se combina con nonces (valores aleatorios ANonce y SNonce) y las direcciones MAC del AP y del cliente para crear la PTK (Pairwise Temporal Key), que finalmente se utiliza para cifrar el tráfico real.

La PMK garantiza una clave maestra, pero la PTK (clave temporal) es la que protege los datos en el día a día. El problema principal es que si un atacante captura el handshake, puede intentar una búsqueda por diccionario sobre la contraseña. Si la clave es débil, resultará relativamente sencillo romperla.

---

**Ataques y Contramedidas**

- **Ataque de Diccionario al Handshake:**  
    Capturando las tramas del handshake, el atacante conoce todos los datos necesarios excepto la contraseña. Con ello puede probar múltiples contraseñas hasta encontrar la correcta, si esta es débil o común.
    
- **Evil Twins:**  
    Un atacante puede crear un punto de acceso falso (un "gemelo malvado") con el mismo ESSID que la red legítima, para engañar a los usuarios a conectarse a este AP falso y así robar datos o credenciales.
    
- **WPA3 y Autenticación Basada en SAE (Simultaneous Authentication of Equals):**  
    La autenticación con SAE en WPA3 soluciona muchos problemas introducidos en WPA2, al no compartir información que facilite los ataques de diccionario. Sin embargo, al ser más reciente, su adopción aún es limitada y, con el tiempo, pueden surgir nuevos ataques que requieran nuevas contramedidas.
    

![[ciberseguridad/5COMUNICACIONES-SEGURAS/imagenes/WIFI/Pasted image 20241219170500.png]]  
![[Pasted image 20241219170651.png]]  
![[Pasted image 20241219171005.png]]  
![[Pasted image 20241219171358.png]]  
![[Pasted image 20241219171741.png]]

---

En conclusión, las redes Wi-Fi son una tecnología compleja que evoluciona continuamente en cuanto a seguridad, modos de operación, y manejo de tramas de gestión. Conocer sus fundamentos, modos, canales, encriptaciones y protocolos de seguridad es esencial para el diseño y mantenimiento de redes inalámbricas seguras y eficientes.

Use iw or airodump-ng

Got it!