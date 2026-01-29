---
title: "Rootkits"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Rootkits – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Tripwire|Tripwire]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Un **rootkit** es un conjunto de herramientas diseñadas para **mantener el acceso encubierto y persistente** a un sistema informático, **ocultando la presencia del atacante y sus actividades**. Se llaman así porque suelen otorgar al atacante acceso de **root o administrador**, y son una de las formas más avanzadas y peligrosas de malware.

---

###  ¿Qué hace un rootkit?

- **Oculta archivos, procesos, usuarios, conexiones de red, entradas del sistema de logs…**
    
- **Impide que herramientas de seguridad detecten su presencia.**
    
- **Carga su código dentro del kernel, librerías del sistema o procesos confiables.**
    
- **Puede instalar backdoors o keyloggers, controlar puertos, modificar configuraciones…**
    
- Su objetivo **no es dañar visiblemente**, sino **mantener el acceso y el control sin ser detectado**.
    

---

###  Objetivos principales

- Mantener **persistencia** en el sistema tras un ataque inicial.
    
- **Ocultar malware o shells remotas**.
    
- **Manipular la salida de herramientas forenses o de detección** (como `ps`, `netstat`, `ls`, `top`, `lsof`, etc.).
    
- **Interferir con actualizaciones o defensas** del sistema.
    

---

###  Tipos de rootkits

|Tipo|Descripción|
|---|---|
|**User-mode rootkits**|Se ejecutan como procesos de usuario. Modifican binarios o bibliotecas del sistema.|
|**Kernel-mode rootkits**|Se cargan en el núcleo del sistema operativo (`.ko` en Linux, drivers `.sys` en Windows). Muy difíciles de detectar.|
|**Firmware rootkits**|Se instalan en el firmware de dispositivos (BIOS, UEFI, routers, tarjetas de red). Persisten incluso tras formateos.|
|**Bootkits**|Se cargan en el MBR o UEFI y controlan el sistema desde el arranque.|
|**Hypervisor rootkits**|Se ejecutan por debajo del sistema operativo, como una máquina virtual. Son extremadamente complejos y sigilosos.|

---

### ️ Técnicas comunes usadas por rootkits

- **Hooking** de funciones del sistema (`syscalls`, `LD_PRELOAD` en Linux).
    
- **Reescritura de binarios** como `ps`, `netstat`, `ls` para ocultar procesos y conexiones.
    
- **Interposición de librerías** en tiempo de carga (`libc`, `libdl`).
    
- **Carga de módulos kernel maliciosos** (`insmod rootkit.ko`).
    
- **Modificación de estructuras internas del kernel** (listas de procesos, ficheros abiertos, etc.).
    
- **Manipulación de los registros del sistema (`/var/log`, `wtmp`, `lastlog`, etc.)**.
    

---

###  ¿Cómo se detecta un rootkit?

1. **Herramientas específicas**:
    
    -  **Chkrootkit** (Linux): analiza síntomas comunes de rootkits.
        
    -  **rkhunter (Rootkit Hunter)**: busca archivos, puertas traseras, firmas.
        
    -  **Tripwire**: compara hashes de archivos clave del sistema.
        
    - ️ **Volatility**: análisis forense de memoria (Windows/Linux).
        
    -  **Kmem, LiME, Rekall**: herramientas de análisis de kernel o RAM.
        
2. **Indicadores de compromiso**:
    
    - Diferencias entre lo que ves como usuario (`ls`) y lo que reporta un disco montado externo.
        
    - Archivos binarios del sistema modificados sin cambios de fecha.
        
    - Procesos que no aparecen en `ps` pero están en `/proc`.
        
    - Conexiones en `netstat` que no aparecen en `lsof`.
        
3. **Análisis desde un entorno seguro**:
    
    - Montar el disco del sistema infectado en un entorno limpio (live CD).
        
    - Leer la memoria con hardware forense o volcado externo (`LiME` + `Volatility`).
        

---

### ️ ¿Cómo se protege un sistema de rootkits?

- **Evitar la escalada a root**: un rootkit necesita privilegios para instalarse.
    
- **Bloquear la carga de módulos kernel** si no son estrictamente necesarios.
    
- **Habilitar Secure Boot y protección del firmware/UEFI.**
    
- **Usar SELinux, AppArmor o MACs avanzados.**
    
- **Segmentar accesos administrativos (su, sudo, roles).**
    
- **Mantener actualizado el kernel, drivers y firmwares.**
    
- **Registrar e integrar logs en sistemas remotos no modificables**.
    
- **Realizar auditorías periódicas de integridad de binarios.**
    

---

###  Ejemplo de rootkit Linux en laboratorio (educativo)

1. El atacante sube un módulo rootkit:
    

```bash
insmod suterus.ko
```

2. Se ocultan procesos:
    

```bash
ps aux  # no muestra el proceso malicioso
```

3. Se carga un backdoor en el puerto 31337:
    

```bash
nc 127.0.0.1 31337
```

4. El atacante tiene acceso root sin que ningún log lo refleje.
    

---

### Conclusión

Los **rootkits son herramientas altamente sofisticadas** diseñadas para esconderse y persistir. No solo permiten acceso encubierto, sino que **dificultan enormemente la detección forense**. Su uso está vinculado a ataques dirigidos, APTs y malware persistente avanzado. Para defenderse, es esencial **prevenir la ejecución privilegiada**, **monitorizar la integridad** y, si se sospecha de un rootkit, **analizar desde fuera del sistema operativo infectado**.

---

¿Te gustaría que prepare un laboratorio controlado para detectar un rootkit con `chkrootkit`, `rkhunter` o incluso con un volcado de memoria y `Volatility`?