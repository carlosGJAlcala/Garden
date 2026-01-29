---
title: "elimina su entrada con wzap o modifica con utmpdump"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Limpieza de logs – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Tripwire|Tripwire]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]].

La **limpieza de logs** es una técnica usada por atacantes **una vez han comprometido un sistema**, cuyo objetivo es **borrar o alterar las evidencias de su actividad** para evitar ser detectados. Es parte habitual de la fase final de un ataque, justo después de conseguir acceso y realizar acciones maliciosas o ilegítimas.

---

###  Objetivo de la limpieza de logs

- **Evitar la detección** por parte de administradores o sistemas de monitoreo.
    
- **Impedir la respuesta forense**, dificultando la reconstrucción del ataque.
    
- **Mantener persistencia** sin levantar alertas.
    
- **Eliminar trazabilidad** de comandos, archivos descargados o conexiones establecidas.
    

---

###  Tipos de logs que suelen limpiarse

|Tipo de log|Contenido|Ubicación común|
|---|---|---|
|**`auth.log` / `secure`**|Inicios de sesión, escaladas sudo|`/var/log/auth.log`, `/var/log/secure`|
|**`bash_history`**|Comandos usados en terminal|`~/.bash_history`|
|**`wtmp`, `utmp`, `lastlog`**|Historial de sesiones, usuarios|`/var/log/wtmp`, `/var/run/utmp`, `/var/log/lastlog`|
|**`messages`, `syslog`**|Registros generales del sistema|`/var/log/syslog`, `/var/log/messages`|
|**`cron`, `maillog`**|Tareas programadas, actividad de correo|`/var/log/cron`, `/var/log/maillog`|

---

### ️ Comandos típicos usados para limpieza

#### 1. **Borrar archivos directamente**

```bash
> ~/.bash_history
history -c
```

#### 2. **Eliminar líneas específicas con `sed` o `grep -v`**

```bash
grep -v '192.168.1.100' /var/log/auth.log > /tmp/cleaned
mv /tmp/cleaned /var/log/auth.log
```

#### 3. **Herramientas especializadas**

- `wzap`: borra entradas específicas de `wtmp`.
    
- `utmpdump`: permite editar registros binarios de sesiones.
    
- `logcleaner`, `zap`, `cleanlog`: herramientas históricas (algunas maliciosas).
    

---

###  Ejemplo práctico

1. El atacante se conecta por SSH.
    
2. Ejecuta comandos maliciosos (`nc`, `wget`, `chmod`...).
    
3. Para borrar huellas:
    

```bash
> ~/.bash_history
history -c
rm /var/log/auth.log
```

4. También modifica:
    

```bash
last -f /var/log/wtmp
# elimina su entrada con wzap o modifica con utmpdump
```

---

###  Contramedidas y defensa

####  Prevenir la modificación de logs

- **Enviar logs a servidores remotos** (SIEM, syslog central):
    
    - Si se borran localmente, los registros permanecen en el servidor externo.
        
- **Logs en sistemas inmutables**:
    
    - Montar `/var/log` como solo lectura o usar sistemas WORM (Write Once, Read Many).
        
- **Usar `auditd` + `ausearch`**:
    
    - Registra acciones incluso de root si se configura correctamente.
        
- **Activar `shell auditing`** (Linux):
    
    - `export PROMPT_COMMAND='history -a'`
        
    - `Snoopy logger`, `auditd`, o `tlog` para capturar comandos incluso si se borra el `.bash_history`.
        

####  Detectar la manipulación

- Gaps en los archivos de log (saltos de tiempo).
    
- Cambios en la integridad de archivos (`Tripwire`, `AIDE`).
    
- Logs incompletos o vacíos sospechosamente.
    
- Timestamps recientes de modificación en `/var/log`.
    

---

###  Recomendaciones forenses

- Si sospechas que han limpiado los logs:
    
    - Buscar **residuos en memoria** o en **disco no asignado**.
        
    - Usar herramientas como **Volatility**, **sleuthkit** o **log2timeline**.
        
    - Analizar shell history de root y otros usuarios (`~/.bash_history`, `~/.zsh_history`, `~/.lesshst`).
        
    - Revisar logs del **servidor remoto** si los hay.
        

---

### Conclusión

La **limpieza de logs es una técnica común y peligrosa** usada por atacantes para ocultar su presencia y dificultar la respuesta. Detectarla requiere **visibilidad externa, controles de integridad, y buenas prácticas de logging**. Para los defensores, es clave que los sistemas de registro **no dependan exclusivamente del host comprometido**.

---

¿Te gustaría que prepare un laboratorio en el que simulas un ataque con limpieza de logs y luego analizas los rastros que quedan para detección forense?