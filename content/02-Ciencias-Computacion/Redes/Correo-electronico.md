---
title: "Correo Electronico"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
### Correo electrónico – Funcionamiento en redes y protocolos


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

El **correo electrónico** (e-mail) es una de las aplicaciones más antiguas y fundamentales de Internet. Permite el **intercambio asincrónico de mensajes entre usuarios**, funcionando sobre una arquitectura de red cliente-servidor y empleando varios protocolos de aplicación.

---

##  Componentes del sistema de correo electrónico

Según el libro _Computer Networking_ (Kurose & Ross), el sistema se divide en tres funciones:

1. **User Agent (UA)**  
    Cliente de correo que permite redactar, leer y organizar emails.  
    Ejemplos: Outlook, Thunderbird, Apple Mail, Gmail (interfaz web).
    
2. **Mail Server**
    
    - Almacena los mensajes salientes en una cola.
        
    - Guarda los mensajes entrantes en un buzón.
        
    - Ejecuta un **Mail Transfer Agent (MTA)** como `sendmail`, `Postfix`, `Exim`.
        
3. **Mail Protocols**
    
    - **SMTP** (envío): para transferir mensajes entre servidores.
        
    - **POP3 / IMAP** (recepción): para recuperar mensajes del servidor por el cliente.
        

---

##  Flujo básico de un correo electrónico

1. El usuario redacta un mensaje con su cliente (UA).
    
2. El mensaje se envía al servidor de correo saliente usando **SMTP**.
    
3. El servidor usa SMTP para reenviar el mensaje al servidor del destinatario.
    
4. El destinatario recupera el mensaje desde su servidor usando **POP3** o **IMAP**.
    

---

##  Protocolo SMTP (Simple Mail Transfer Protocol)

- Estándar para el **envío de mensajes**.
    
- Utiliza **TCP puerto 25**.
    
- Es **push-based**: el emisor inicia la conexión.
    
- Texto plano, protocolo ASCII.
    

### Ejemplo de diálogo SMTP:

```text
C: HELO servidor.origen.com
S: 250 Hello
C: MAIL FROM:<alice@origen.com>
S: 250 OK
C: RCPT TO:<bob@destino.com>
S: 250 OK
C: DATA
S: 354 Start mail input
C: (contenido del mensaje)
C: .
S: 250 Message received
C: QUIT
S: 221 Bye
```

---

##  POP3 vs IMAP – para recuperación de mensajes

|Característica|POP3|IMAP|
|---|---|---|
|Modelo|Descargar y borrar|Sincronización con el servidor|
|Puerto|110 (TCP)|143 (TCP)|
|Estado|Sin estado|Con estado|
|Carpetas remotas|No|Sí|
|Uso típico|Clientes simples, baja conectividad|Webmail, múltiples dispositivos|

---

##  Arquitectura del correo electrónico

```text
UsuarioA     SMTP →   Servidor origen   SMTP →  Servidor destino   ← IMAP/POP3   UsuarioB
[UA]                        [MTA]                         [MTA]                           [UA]
```

---

##  Seguridad en correo electrónico

- **TLS** para cifrar conexiones SMTP/IMAP/POP3 (`STARTTLS`).
    
- **Autenticación SMTP (SMTP AUTH)** para evitar envío no autorizado.
    
- **SPF, DKIM, DMARC**: mecanismos para validar la legitimidad del remitente.
    
- **PGP, S/MIME**: cifrado de extremo a extremo del contenido del mensaje.
    

---

##  Problemas comunes

- Spam: correos no deseados automatizados.
    
- Spoofing: suplantación de identidad de remitente.
    
- Phishing: correos con engaños para robar credenciales.
    
- Relays abiertos: servidores mal configurados usados para enviar spam.
    

---

##  Conclusión

El **correo electrónico funciona sobre un conjunto de protocolos bien definidos**. SMTP gestiona el envío, mientras que POP3 o IMAP permiten la recuperación de mensajes. Aunque su estructura es robusta y ampliamente usada, **requiere medidas de seguridad activas** para evitar abusos como spam o suplantación.

---