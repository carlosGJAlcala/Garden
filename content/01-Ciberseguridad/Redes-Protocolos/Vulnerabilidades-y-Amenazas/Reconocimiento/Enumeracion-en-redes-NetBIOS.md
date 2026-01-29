---
title: "Enumeracion En Redes Netbios"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Enumeración en redes NetBIOS – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/ZEEK|ZEEK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]].

La **enumeración en redes NetBIOS** permite descubrir información detallada de una red Windows (o compatible) a través del **protocolo NetBIOS sobre TCP/IP (NBT)**. Este protocolo, aunque obsoleto en entornos modernos, **sigue activo en muchas redes internas**, especialmente en dominios Windows mal configurados.

---

###  ¿Qué es NetBIOS?

**NetBIOS (Network Basic Input/Output System)** es un servicio que permite la identificación de nombres y recursos compartidos en una red local. Usa **puertos 137 (UDP), 138 (UDP)** y **139 (TCP)**.

Se utiliza para:

- Resolución de nombres NetBIOS.
    
- Compartición de archivos e impresoras.
    
- Comunicación entre máquinas Windows en la misma red.
    

---

###  ¿Qué información permite obtener?

Mediante técnicas de enumeración NetBIOS, un atacante o auditor puede descubrir:

- **Nombres de máquina**
    
- **Usuarios conectados**
    
- **Recursos compartidos (carpetas, impresoras)**
    
- **Grupos de trabajo o dominios**
    
- **Direcciones IP y MAC**
    
- **Usuarios conectados y sesiones activas**
    
- **Versión del sistema operativo**
    

---

###  Comandos útiles en Windows para enumerar NetBIOS

#### 1. **Ver dominios en la red**

```cmd
net view /domain
```

#### 2. **Ver equipos en un dominio**

```cmd
net view /domain:NOMBRE_DEL_DOMINIO
```

#### 3. **Ver recursos compartidos de un equipo**

```cmd
net view \\NOMBRE_MAQUINA
```

#### 4. **Ver sesiones activas**

```cmd
net session
```

#### 5. **Conectarse a una carpeta compartida**

```cmd
net use Z: \\IP\recurso
```

---

###  Ejemplo práctico de enumeración

```cmd
C:\> net view \\192.168.1.10

Shared resources at \\192.168.1.10

Share name    Type    Used as  Comment
-------------------------------------------------
IPC$          IPC              Remote IPC
Users         Disk             Carpeta de usuarios
```

---

### ️ Herramientas de enumeración avanzadas

|Herramienta|Funcionalidad clave|
|---|---|
|**enum4linux**|Auditoría Linux de redes Windows (muy completo).|
|**nbtscan**|Escaneo de nodos NetBIOS en red.|
|**Nmap + scripts NSE**|Scripts como `smb-enum-shares`, `smb-os-discovery`, `smb-enum-users`.|
|**SMBMap**|Enumera y accede a recursos compartidos SMB.|
|**CrackMapExec**|Potente framework para enumeración, ataque y post-explotación SMB.|

---

###  Implicaciones de seguridad

#### ¿Por qué es peligrosa la enumeración NetBIOS?

- Permite descubrir **estructura interna de la red** sin autenticación.
    
- Expone nombres de usuarios y recursos sensibles.
    
- Puede ser usada para **acceder a carpetas compartidas sin permisos**.
    
- Es base para ataques de **fuerza bruta**, **relay SMB**, **pass-the-hash**, o **movimiento lateral** en redes Windows.
    

---

### ️ Medidas de defensa

1. **Deshabilitar NetBIOS sobre TCP/IP** si no es necesario.
    
    - Opcional en entornos modernos con DNS.
        
2. **Bloquear puertos 137, 138 y 139** desde redes externas o no confiables.
    
3. **Aplicar políticas de compartición restrictiva**:
    
    - Compartir solo carpetas necesarias.
        
    - Usar ACLs detalladas.
        
4. **Habilitar firewalls en cada host** para bloquear escaneo lateral.
    
5. **Monitorizar tráfico SMB/NetBIOS** con IDS (Snort, Zeek).
    
6. **Actualizar sistemas**: vulnerabilidades como **EternalBlue** (SMBv1) siguen explotándose hoy.
    

---

### Conclusión

La enumeración en redes NetBIOS es una técnica sencilla pero poderosa para **obtener visibilidad interna en entornos Windows**, especialmente si no se han aplicado buenas prácticas de seguridad. Aunque NetBIOS está en desuso, **su presencia en redes reales sigue siendo común**. Por eso, tanto su análisis como su mitigación son críticos en cualquier auditoría o ejercicio de hardening.

---

¿Quieres que prepare un ejemplo práctico con `enum4linux` o un escaneo con Nmap y scripts NSE específicos para NetBIOS/SMB?