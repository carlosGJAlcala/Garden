---
title: "Mensajería instantánea y seguridad"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

# Mensajería instantánea y seguridad


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

En el ecosistema actual de comunicaciones digitales, la mensajería instantánea es una de las formas de comunicación más utilizadas y, por tanto, uno de los objetivos prioritarios de ataques. Plataformas como WhatsApp, Messenger, Signal, Telegram, Matrix, Briar y Session ofrecen soluciones variadas con diferentes niveles de seguridad y privacidad, que es fundamental entender y comparar.

## Comparación de seguridad entre plataformas

- **WhatsApp y Signal** ofrecen cifrado extremo a extremo (E2EE) de forma predeterminada en todas sus conversaciones. Esto significa que únicamente el remitente y el destinatario pueden leer los mensajes, incluso el proveedor del servicio no puede acceder a su contenido. WhatsApp, de hecho, utiliza el mismo protocolo de Signal, garantizando estándares similares de seguridad.
    
- **Telegram** ofrece cifrado extremo a extremo únicamente en los denominados "chats secretos". Los chats normales están cifrados entre cliente y servidor, pero el servidor puede acceder a los mensajes, lo que representa un modelo de seguridad menos robusto frente a amenazas de acceso no autorizado o compromisos en los servidores de Telegram.
    
- **Matrix** es una plataforma orientada a entornos técnicos y comunidades especializadas, con un modelo descentralizado. Proporciona funcionalidades avanzadas de interoperabilidad y cifrado E2EE, pero su adopción masiva es más limitada y su nivel de seguridad depende mucho de la implementación concreta en cada servidor federado.
    
- **Briar y Session** están orientadas específicamente a ofrecer comunicaciones seguras en contextos de alto riesgo, con modelos descentralizados y foco explícito en privacidad y anonimato.
    
- **Messenger e Instagram**, en cambio, no ofrecen garantías robustas de seguridad por defecto en sus mensajes. Instagram, en particular, es insegura desde la perspectiva de confidencialidad porque no aplica cifrado de extremo a extremo, lo que expone los mensajes a potencial acceso por parte del proveedor o terceros que logren comprometer los sistemas.
    

## Fundamentos criptográficos: E3DH

El protocolo E3DH (Extended Triple Diffie-Hellman) constituye la base del cifrado extremo a extremo de Signal y, por extensión, de WhatsApp. Este protocolo se basa en el conocido intercambio de claves Diffie-Hellman, pero adaptado a contextos modernos y reforzado mediante el uso de criptografía de curva elíptica para maximizar la seguridad y eficiencia.

El funcionamiento se puede resumir en los siguientes puntos:

1. **Intercambio de claves públicas efímeras**:  
    Cada usuario genera pares de claves efímeras y públicas para una sesión determinada. Alice, por ejemplo, envía su clave pública `eaG` a Bob, mientras que Bob envía su clave pública `ebG` a Alice.
    
2. **Cálculo de clave secreta compartida**:  
    Ambos pueden, de manera independiente, calcular la misma clave secreta utilizando su propia clave privada y la clave pública recibida. Matemáticamente, se representa como `SK = DH(eaG, ebG) = eaebG`.
    
3. **Protección de confidencialidad y autenticidad**:  
    Este mecanismo asegura que únicamente quienes poseen las claves privadas correspondientes pueden derivar la clave secreta compartida, lo que protege la confidencialidad de las comunicaciones incluso si un atacante intercepta las claves públicas transmitidas.
    
4. **Uso de claves efímeras**:  
    Las claves generadas son temporales y no reutilizables. Esto garantiza el principio de forward secrecy (secreto hacia adelante): aunque una clave privada a largo plazo se vea comprometida en el futuro, las comunicaciones pasadas seguirán estando seguras.
    
5. **Capacidad offline**:  
    El protocolo permite establecer la clave compartida de forma asíncrona, incluso cuando una de las partes no está conectada en tiempo real. Esto es posible porque la clave pública puede ser almacenada en el servidor de mensajería y recuperada más tarde por la otra parte.
    

## Seguridad avanzada en Signal: Double Ratchet

Signal no se limita a E3DH: sobre esta base añade el algoritmo **Double Ratchet**, que actualiza constantemente las claves criptográficas después de cada mensaje enviado o recibido. Esto proporciona propiedades adicionales de seguridad como el **secreto perfecto hacia adelante y secreto retrospectivo**: aunque un atacante consiga las claves actuales, no podría descifrar mensajes anteriores ni futuros porque cada mensaje tiene una clave diferente que se genera en cascada y se destruye después de su uso.

## Conclusión

La mensajería instantánea es hoy uno de los medios más utilizados pero también uno de los más atacados. Plataformas como Signal y WhatsApp ofrecen garantías robustas gracias a su implementación de E3DH y Double Ratchet, mientras que otras como Telegram y Messenger presentan limitaciones importantes, especialmente en sus configuraciones por defecto.

El cifrado extremo a extremo moderno, basado en Diffie-Hellman sobre curvas elípticas con claves efímeras, permite proteger las comunicaciones incluso en escenarios adversos como interceptaciones masivas o accesos indebidos a servidores. Además, la capacidad offline de estos protocolos garantiza que la seguridad no dependa de que ambas partes estén conectadas al mismo tiempo, una característica crítica en aplicaciones móviles y redes intermitentes.

La seguridad de estas aplicaciones no solo depende del protocolo, sino también de las implementaciones concretas, de su configuración y de la forma en que los usuarios las utilizan. Por ello, es importante conocer las diferencias entre plataformas y entender los mecanismos criptográficos que las sustentan.


---

##  ECDH y claves públicas: autenticación y confidencialidad

###  Escenario 1: Bob usa una clave **no efímera** (persistente)

![[Pasted image 20241129164147 1.png]]

En este caso, Bob (también llamado "Bono" en tu nota) **tiene una clave pública fija**, conocida por todos. No la genera en cada sesión, sino que:

- Está registrada, publicada y verificada (por ejemplo, por una autoridad de confianza).
    
- Alice puede usar esa clave para derivar el secreto ECDH sin que Bob envíe nada.
    

#### ️ Ventaja: autenticación

Como la clave pública de Bob **ya es conocida**, cualquier mensaje cifrado con un secreto derivado de esa clave implica que se está hablando con Bob. **No es necesario que Bob esté en línea ni envíe nada** en ese momento.

####  Desventaja: no hay forward secrecy

![[Pasted image 20241129165122 1.png]]

En este modelo, **si la clave privada de Alice o Bob se ve comprometida en el futuro**, cualquier sesión pasada que haya sido cifrada usando ECDH con esas claves puede ser **descifrada retroactivamente**.

Esto ocurre porque la clave derivada es la misma si se conoce la clave privada y la pública de la otra parte.

---

##  Escenario 2: Bob usa una clave **efímera**

![[Pasted image 20241129165614 1.png]]

En este modelo, Bob **genera una nueva clave para cada sesión** (una clave efímera). Por tanto:

- Bob tiene que estar presente (activo) en el momento del intercambio, ya que debe enviar su clave pública efímera a Alice.
    
- Nadie más conoce esa clave pública antes de la sesión.
    

### ️ Ventaja: **Forward Secrecy**

Como la clave efímera de Bob se destruye tras la sesión, incluso si se compromete su clave privada persistente **en el futuro**, los secretos pasados **no pueden ser recuperados**.

Esto protege la confidencialidad de sesiones anteriores frente a ataques diferidos.

###  Desventaja: requiere actividad y autenticación explícita

Bob **tiene que participar activamente** y, además, como la clave efímera no está verificada por nadie, se requiere algún mecanismo adicional para **autenticar** que esa clave efímera pertenece efectivamente a Bob (por ejemplo, una firma digital con su clave persistente).

---

##  Escenario híbrido: ambas partes usan claves efímeras **+ autenticación**

En muchos protocolos modernos (como **TLS 1.3**, **Signal**, **WireGuard**), se utiliza una combinación:

- Claves efímeras para obtener **forward secrecy**.
    
- Firmas digitales con claves persistentes para **autenticar la identidad** de las partes.
    

Así se logra lo mejor de ambos mundos: privacidad perfecta hacia el futuro **y autenticidad garantizada**.

---

¿Quieres que añada ejemplos de cómo esto se implementa en TLS o Signal? También puedo ayudarte a comparar ECDH con otras variantes como ECDHE o X3DH.

![[Pasted image 20241129165947 1.png]]


---

# 3XDH (Triple Diffie-Hellman)

El protocolo **3XDH (Triple Diffie-Hellman)** es la base criptográfica del proceso de establecimiento de claves seguras en **Signal Protocol**, y está diseñado específicamente para escenarios de mensajería asíncrona con requisitos estrictos de seguridad.

Su objetivo es lograr:

1. Confidencialidad de los mensajes intercambiados.
    
2. Autenticación de Alice ante Bob.
    
3. Autenticación de Bob ante Alice.
    
4. Forward secrecy (secreto hacia adelante), para proteger mensajes pasados incluso si se comprometen claves futuras.
    
5. Funcionamiento offline, permitiendo que el destinatario no tenga que estar conectado en el momento en que el emisor inicia la comunicación.
    
6. Resistencia a ataques de replay, evitando que mensajes antiguos sean reutilizados maliciosamente.
    

---

## Flujo detallado de 3XDH

El establecimiento de sesión con 3XDH se desarrolla a través de varios intercambios de claves usando **claves de largo plazo, claves efímeras y pre-claves públicas**.

### Paso inicial: contacto con el servidor

Alice quiere iniciar comunicación con Bob. Alice consulta al servidor por Bob. El servidor tiene un "censo" donde mantiene las claves públicas necesarias para establecer la sesión con Bob.

Además del paquete de identidad de Bob (su clave de identidad pública), Bob publica **una pre-clave pública y una pre-clave firmada**, que permite garantizar que el servidor no puede falsificar pre-claves arbitrarias y mantiene la autenticidad del material criptográfico.

---

### Intercambios Diffie-Hellman involucrados

El protocolo realiza **tres intercambios Diffie-Hellman más uno adicional**, que permiten cumplir simultáneamente confidencialidad, autenticación mutua y forward secrecy.

Los detalles son:

1️⃣ **Diffie-Hellman entre la clave de identidad de Alice y la clave de sesión efímera de Bob**.  
Esto permite autenticar a Alice ante Bob, porque implica el uso de la clave privada de identidad de Alice.

2️⃣ **Diffie-Hellman entre la clave efímera de Alice y la clave de identidad de Bob**.  
Autentica a Bob ante Alice.

3️⃣ **Diffie-Hellman entre las claves efímeras de Alice y Bob**.  
Contribuye a la confidencialidad y forward secrecy.

4️⃣ **Diffie-Hellman adicional entre la clave de identidad de Alice y la clave de identidad de Bob** (en algunas versiones se incluye para fortalecer la autenticación mutua de largo plazo).

El resultado de estos cuatro intercambios es una colección de secretos compartidos que se concatenan y pasan a través de una función derivadora de claves (KDF), produciendo la clave maestra que servirá para iniciar la sesión de mensajería segura.

---

## Propiedades alcanzadas

Gracias a este diseño, **3XDH permite que Alice pueda iniciar una conversación con Bob aunque Bob no esté conectado en ese momento** (modo offline). Esto es posible porque Bob ha depositado sus pre-claves en el servidor y Alice puede usarlas para derivar una clave compartida de forma unilateral.

El mecanismo es también **resistente a ataques de replay** porque cada pre-clave solo puede ser usada una vez. Cuando Alice consume una pre-clave de Bob, el servidor la marca como utilizada y requiere que Bob publique nuevas pre-claves para futuras sesiones.

Además, el uso de claves efímeras garantiza forward secrecy: aunque las claves de largo plazo se vean comprometidas en el futuro, las sesiones anteriores permanecerán protegidas.

---

![[Pasted image 20241129171440 1.png]]
si porque hay que tener en cuenta el MIT

![[Pasted image 20241129171936 1.png]]

Gracias por toda la información y las imágenes. Estás describiendo conceptos avanzados del protocolo **Signal**, especialmente sobre cómo protege contra suplantaciones, ataques de replay, y cómo se logra **forward secrecy** y **asynchronous messaging** con el **Double Ratchet**.

A continuación te presento el contenido reescrito, corregido y expandido en **Markdown**, con todas las imágenes **mantenidas tal cual las has referenciado** (`![[]]`), y con explicaciones técnicas claras y estructuradas.

---

##  Verificación con código QR: autenticidad de claves

En el protocolo **Signal**, la autenticación del interlocutor **no se basa solo en firmas digitales**. Esto se debe a que el servidor podría **falsificar claves públicas** (por ejemplo, IKA o PKA) si actuara de forma maliciosa o estuviera comprometido.

![[Pasted image 20241129172318 1.png]]

###  ¿Por qué el código QR es importante?

El **escaneo del código QR** entre los dispositivos permite verificar de forma manual (fuera del servidor) que las claves públicas realmente pertenecen al interlocutor. Esto:

- Impide **ataques man-in-the-middle** (MITM) realizados por el servidor.
    
- Asegura que el canal de comunicación está cifrado entre las dos partes reales.
    

---

##  Garantías de los intercambios de clave

![[Pasted image 20241129172516 1.png]]  
![[Pasted image 20241129172657 1.png]]  
![[Pasted image 20241129172935 1.png]]

En la arquitectura de Signal, el intercambio de claves se basa en varios elementos:

- **IK (Identity Key):** Clave pública persistente de la identidad.
    
- **SPK (Signed PreKey):** Clave efímera firmada por la IK.
    
- **OPKs (One-Time PreKeys):** Claves efímeras de un solo uso, almacenadas en el servidor para permitir mensajes asíncronos.
    

###  Garantías clave:

1. El **paso 3 garantiza el secreto compartido**: Es donde se combinan las claves efímeras y persistentes para generar el secreto inicial.
    
2. El **paso 4 evita ataques de replay**: Al consumir y eliminar las OPKs después de su uso, evita que se reutilicen claves para sesiones futuras.
    

> ️ Cualquier material criptográfico que **no se elimine** (como una clave efímera no borrada) puede comprometer la **forward secrecy**.

---

##  SPK y OPKs en Signal

- **SPK (Signed PreKey):** Es una clave efímera que se cambia periódicamente. Está firmada con la IK y sirve como parte del cálculo del secreto inicial.
    
- **OPKs:** Se eliminan tras un solo uso para evitar su reutilización. Su rol es garantizar el secreto hacia adelante cuando el receptor no está disponible.
    

---

##  Doble Ratchet: el sistema de doble carril

Signal utiliza el sistema llamado **Double Ratchet Algorithm**, que combina:

1. Un **ratchet de Diffie-Hellman**: cambia las claves cada vez que llega un mensaje con una nueva clave pública.
    
2. Un **ratchet simétrico (KDF-chain)**: avanza con cada mensaje enviado o recibido, incluso si no hay nuevas claves.
    

![[Pasted image 20241129175744 1.png]]

###  Beneficios del Double Ratchet

- **Forward Secrecy**: Cada mensaje tiene su propia clave derivada, y las claves anteriores no pueden recuperarse aunque se comprometa la clave actual.
    
- **Future Secrecy / Post-Compromise Security**: Si un atacante roba una clave, solo puede acceder a un mensaje — no a los anteriores ni a los futuros.
    
- **Sincronización independiente**: Cada parte puede avanzar su ratchet simétrico por separado, lo que permite **mensajería asincrónica**.
    

### ️ “Recuperación en vivo” no se cumple

La propiedad de **live recovery** (recuperar mensajes sin acceso físico) **no se cumple**: si se pierde el estado del ratchet, se pierden los mensajes cifrados con claves avanzadas. Esto es un **precio intencionado** que se paga para preservar la confidencialidad y la no recuperación por parte de terceros.

---

##  Metáfora de las “carretas”

En tus apuntes usas “carretas” para referirte a los dos caminos que avanzan (uno simétrico, otro asimétrico). Esto es correcto:

- Las **dos carretas se sincronizan** cuando ambas partes envían mensajes.
    
- Mientras no se rompan (es decir, no haya pérdida de estado ni compromiso de claves), el canal se mantiene seguro y progresivo.
    

---

¿Quieres que te prepare un esquema visual con todo esto o una presentación de resumen para clase o exposición? También puedo explicarte cómo Signal usa esto dentro del protocolo X3DH.