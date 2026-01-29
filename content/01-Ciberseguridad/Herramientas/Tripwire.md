---
title: "Tripwire"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### Tripwire – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/GanarAcceso/Rootkits|Rootkits]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]].

**Tripwire** es una herramienta de **control de integridad de sistemas**. Su función principal es **detectar cambios no autorizados en archivos críticos del sistema**, lo cual permite **identificar manipulaciones, infecciones por malware, rootkits o actividades maliciosas**. Es ampliamente utilizada en **auditorías, entornos de alta seguridad y sistemas Linux/UNIX**.

---

###  ¿Qué hace Tripwire?

Tripwire **toma una “instantánea” (baseline)** de archivos y directorios seleccionados: guarda **sumas de comprobación (hashes), permisos, propietarios, tamaños y fechas**. Luego, de forma periódica o manual:

- Vuelve a escanear esos archivos.
    
- **Detecta cualquier diferencia** (incluso de 1 bit).
    
- Reporta los cambios.
    

Esto permite saber si un **binario del sistema fue alterado**, si se insertó una **backdoor, rootkit, shell maliciosa o keylogger**, etc.

---

###  ¿Qué protege Tripwire?

Archivos y directorios como:

- `/bin`, `/sbin`, `/usr/bin`, `/lib` → binarios del sistema.
    
- `/etc/passwd`, `/etc/shadow` → credenciales.
    
- `/boot` → kernel y archivos de arranque.
    
- `/var/log` → logs del sistema (detectar manipulaciones).
    
- Cualquier otro que definas como crítico (scripts, servicios…).
    

---

###  Funcionamiento resumido

#### 1. **Inicialización (baseline)**

```bash
tripwire --init
```

 Se genera una **base de datos de estado actual** (`tw.db`) con hashes de todos los archivos monitorizados.

#### 2. **Verificación**

```bash
tripwire --check
```

 Compara los archivos actuales con la base de datos y **reporta todos los cambios detectados**.

#### 3. **Actualización del estado**

Si modificaste archivos legítimamente (ej. actualizaciones del sistema), puedes actualizar la base:

```bash
tripwire --update --twrfile reporte.twr
```

---

###  ¿Qué detecta Tripwire?

|Tipo de cambio|Implicación|
|---|---|
|Cambios en binarios (`/bin/ls`, `/usr/sbin/sshd`)|Posible infección o rootkit|
|Archivos eliminados o añadidos|Shells ocultas, limpieza de logs|
|Cambios en `/etc/shadow`, `/etc/sudoers`|Escalada de privilegios, cuentas ocultas|
|Logs alterados|Intento de borrar huellas|

---

### ️ Beneficios en seguridad

- **Detecta intrusiones incluso si no hay logs**.
    
- **Detecta rootkits** que modifican utilidades del sistema.
    
- **Complementa antivirus/antimalware** con detección basada en integridad.
    
- **Imprescindible en entornos regulados** (PCI-DSS, ISO 27001, HIPAA, etc.).
    

---

### ️ Limitaciones

- Si el atacante **modifica la base de datos o clave de Tripwire**, puede eludir la detección.
    
- Si el sistema está comprometido, **Tripwire también podría estar manipulado**.
    
- Por eso, se recomienda:
    
    - **Almacenar la base de datos y clave en una partición protegida o sistema externo**.
        
    - Usar **servidores de monitorización externos**.
        

---

### ️ Instalación en Linux (Debian/Ubuntu)

```bash
sudo apt install tripwire
sudo tripwire-setup-keyfiles
sudo tripwire --init
```

Revisar y editar `/etc/tripwire/twpol.txt` para personalizar qué archivos se auditan.

---

###  Informe típico de verificación

```text
Modified: /usr/bin/passwd
Removed:  /usr/bin/ftp
Added:    /tmp/shell
```

→ Esto podría indicar que se ha instalado una shell backdoor en `/tmp`, eliminado el binario de FTP y modificado el binario de contraseñas.

---

###  Alternativas modernas a Tripwire

|Herramienta|Característica destacada|
|---|---|
|**AIDE**|Muy ligero, reemplazo directo.|
|**Samhain**|Control de integridad + detección de intrusos.|
|**OSSEC**|HIDS completo con control de integridad, alertas, log analysis.|
|**Wazuh**|Versión mejorada de OSSEC, con dashboard.|

---

### Conclusión

**Tripwire es una herramienta potente y confiable** para detectar manipulaciones de archivos en sistemas críticos. Aunque antigua, sigue siendo muy útil cuando se configura y protege correctamente. Es una defensa pasiva clave contra rootkits, shells maliciosas, limpieza de logs y cambios sigilosos que no generan alertas tradicionales.

---

¿Te gustaría que te prepare una guía paso a paso para instalar y usar Tripwire en un entorno Linux y detectar un cambio malicioso simulado?