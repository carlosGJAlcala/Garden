---
title: "Snmpbrute"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### SNMPBrute – Nota técnica expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

**SNMPBrute** es una herramienta de fuerza bruta diseñada para **descubrir cadenas de comunidad válidas en dispositivos que usan SNMP (Simple Network Management Protocol)**. SNMP es un protocolo de gestión de red que permite **consultar y modificar remotamente información de dispositivos** (routers, switches, servidores, etc.).

---

###  ¿Por qué atacar SNMP?

- SNMP se basa en **comunidades** (equivalentes a contraseñas).
    
- Las cadenas **“public”** (lectura) y **“private”** (escritura) son las más comunes.
    
- **SNMPv1 y v2c** son **inseguros por diseño**: no cifran la comunicación y confían en estas cadenas de texto plano.
    
- Si un atacante descubre una cadena válida:
    
    - Puede obtener **información sensible** del sistema.
        
    - Con la cadena de escritura (`private`), puede **reconfigurar el dispositivo**, apagarlo, o **redirigir tráfico (DoS o MITM)**.
        

---

### ️ ¿Qué hace SNMPBrute?

- Lanza una **fuerza bruta contra un host SNMP** usando una lista de cadenas de comunidad (como una lista de contraseñas).
    
- Verifica si el dispositivo responde con un `SNMP GET` válido.
    
- Opcionalmente, identifica información como:
    
    - Nombre del sistema (`sysName`)
        
    - Contacto (`sysContact`)
        
    - Uptime del dispositivo
        
    - Versión del software
        
    - Interfaces de red
        

---

###  Uso típico de SNMPBrute

#### 1. Instalar la herramienta

SNMPBrute no suele venir por defecto. Puedes encontrarla en:

- Algunos repositorios de GitHub:  
    Ejemplo: [https://github.com/hatlord/snmpbrute](https://github.com/hatlord/snmpbrute)
    
- En distros como Kali Linux puede venir preinstalada bajo otro nombre.
    

#### 2. Ejecutar un ataque de fuerza bruta

```bash
python snmpbrute.py -t 192.168.1.1 -w wordlist.txt
```

- `-t`: IP del objetivo.
    
- `-w`: diccionario de cadenas SNMP.
    

> Si encuentra una cadena válida, lo indicará en pantalla con el tipo (read/write) y la respuesta del dispositivo.

---

###  Ejemplo práctico

```text
Trying: public
️ Valid community string found: public (read-only)

Trying: private
️ Valid community string found: private (read-write)
```

Con esta información puedes ahora lanzar comandos SNMP válidos con herramientas como `snmpwalk`, `snmpset`, etc.

---

###  Riesgos si SNMP es vulnerable

- Exposición de datos de configuración, interfaces, usuarios.
    
- Modificación de parámetros: routing, firewall, DNS, interfaces.
    
- Apagado o reinicio del dispositivo.
    
- Montaje de ataques de **denegación de servicio** o **suplantación de tráfico**.
    

---

### ️ Contramedidas

1. **Deshabilitar SNMP si no se usa.**
    
2. **Usar SNMPv3**, que añade:
    
    - Autenticación con usuario/clave.
        
    - Cifrado de los datos (seguridad real).
        
3. **Cambiar las cadenas “public” y “private” por otras aleatorias y fuertes.**
    
4. **Restringir el acceso por IP o por ACL en el dispositivo.**
    
5. **Monitorizar peticiones SNMP anómalas o no autorizadas.**
    
6. **Bloquear el puerto UDP 161 en redes externas o segmentar SNMP solo para redes de gestión.**
    

---

### Herramientas complementarias a SNMPBrute

|Herramienta|Función|
|---|---|
|`snmpwalk`|Recorre la MIB y extrae info con una cadena válida|
|`snmpget`|Realiza consultas específicas SNMP|
|`snmpset`|Modifica parámetros si se tiene acceso de escritura|
|`onesixtyone`|Fuerza bruta SNMP en paralelo (más rápida que SNMPBrute)|
|`nmap --script snmp*`|Detecta y enumera SNMP desde Nmap|

---

### Conclusión

**SNMPBrute es una herramienta sencilla pero eficaz** para auditar la seguridad de servicios SNMP expuestos. En redes mal configuradas, puede revelar información crítica o permitir ataques remotos sin necesidad de exploits complejos. **SNMP debe ser tratado como un vector de riesgo serio si se expone sin protección**.

---

¿Quieres que prepare una demo o script con SNMPBrute + snmpwalk sobre una máquina virtual simulada?