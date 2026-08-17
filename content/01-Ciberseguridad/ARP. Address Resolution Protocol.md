### ARP (Address Resolution Protocol) – Nota expandida

El **ARP** es uno de los protocolos más importantes dentro de una red local (LAN) y actúa como puente entre la **capa de red (IP)** y la **capa de enlace (Ethernet)** del modelo TCP/IP. Aunque es esencial para el funcionamiento de la red, su diseño inicial carece de mecanismos de seguridad, lo que lo convierte en un blanco frecuente de ataques.

### ¿Qué es ARP y para qué sirve?

ARP traduce direcciones **IP** (por ejemplo, `192.168.1.1`) en direcciones **MAC** (por ejemplo, `00:1A:2B:3C:4D:5E`), necesarias para enviar paquetes dentro de una red local.

- Un host puede conocer la IP de destino, pero no su dirección MAC.
- ARP responde a esta necesidad mediante un mecanismo de consulta-respuesta.

### Funcionamiento básico del protocolo ARP

1. Un equipo (A) quiere enviar un paquete IP a otro equipo (B) en la misma red local.
2. A consulta su **tabla ARP**. Si no tiene la MAC asociada a la IP de B:
    - A emite un **ARP Request** en broadcast (`FF:FF:FF:FF:FF:FF`) a toda la LAN, preguntando: “¿Quién tiene la IP X.X.X.X?”.
3. B responde con un **ARP Reply**, informando de su dirección MAC.
4. A guarda esa información en su tabla ARP por un tiempo limitado (TTL típico: 20 minutos).

> Es un protocolo **“plug-and-play”**, es decir, no requiere configuración manual.

### Estructura de la tabla ARP

Las tablas ARP de cada dispositivo almacenan pares clave-valor:

|Dirección IP|Dirección MAC|Tiempo de vida|
|---|---|---|
|192.168.1.100|00:1A:2B:3C:4D:5E|20 min|

### Vulnerabilidades: ARP Spoofing o ARP Poisoning

**ARP no autentica las respuestas**, por lo que cualquier dispositivo puede responder a una petición ARP. Esto abre la puerta a ataques de suplantación:

- Un atacante responde a una solicitud ARP antes que el equipo legítimo, diciendo “yo tengo esa IP”.
- El atacante hace que su MAC aparezca como asociada a la IP del router o de otro equipo.
- De esta forma, el tráfico legítimo se desvía hacia el atacante (ataque **Man-in-the-Middle**, o **DoS** si el atacante simplemente descarta los paquetes).

### Medidas de defensa contra ARP Spoofing

1. **Tablas ARP estáticas**:
    - Se fija manualmente la asociación IP-MAC en cada equipo.
    - **Desventaja**: Poco práctico en redes grandes o dinámicas.
2. **Inspección [[DHCP]] (DHCP Snooping)**:
    - Switches avanzados (como los de Cisco) registran qué dirección MAC está en cada puerto.
    - Detectan inconsistencias entre ARP y DHCP.
3. **Herramientas de detección**:
    - **ARPWatch**: monitoriza cambios en las tablas ARP y alerta ante nuevas asociaciones.
    - **XArp**, **Ettercap** o **Wireshark** también permiten detectar ataques.
4. **Verificación de MAC duplicadas**:
    - Si una misma MAC responde a múltiples IPs (o viceversa), puede ser una señal de ataque.
5. **RARP (Reverse ARP)**:
    - Pregunta: “¿Cuál es la IP asociada a esta MAC?”
    - Si devuelve múltiples IPs, la MAC está clonada.

### ARP en contextos modernos

Aunque sigue siendo esencial, ARP está siendo reemplazado o reforzado por alternativas más seguras en algunos entornos:

- **NDP (Neighbor Discovery Protocol)** en IPv6, con autenticación opcional mediante **IPsec**.
- **ARP dinámico autenticado** en redes seguras mediante extensiones propietarias.
- En redes inalámbricas o virtualizadas, la **segmentación de red (VLANs)** y el uso de **VPNs** también limita los efectos del spoofing.

### Ejemplo de ataque ARP Spoofing

```plaintext
1. Víctima envía ARP Request: "¿Quién tiene 192.168.1.1?"
2. Atacante responde antes que el router: "192.168.1.1 soy yo – MAC 00:AA:BB:CC:DD:EE"
3. La víctima guarda esta falsa entrada en su tabla ARP.
4. Todo su tráfico hacia el router va ahora al atacante.
```

### Conclusión

El protocolo ARP es un componente fundamental pero inseguro en las redes modernas. Entender su funcionamiento y sus debilidades permite aplicar contramedidas efectivas y prevenir ataques de red locales. Las organizaciones deben monitorizar y segmentar correctamente sus redes para minimizar su exposición a estas amenazas.
