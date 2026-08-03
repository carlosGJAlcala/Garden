---
title: "Plan De Practicas Propuesto"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---

## **Plan de prácticas propuesto**


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Forense/guia/Acceso-y-analisis-de-memoria-en-Linux-y-Windows|Acceso y analisis de memoria en Linux y Windows]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[03-Desarrollo-Software/Paradigmas/Paradigmas-de-Objectivos/Paradigma-Concurrente-Memoria-Comun|Paradigma Concurrente Memoria Comun]].

El objetivo es progresar desde interacciones controladas en modo usuario, pasando por depuración en vivo, hasta análisis forense offline y observabilidad con eBPF. Esto te permitirá **reconocer un mismo artefacto** (variable, buffer, mutex, etc.) en distintos niveles de acceso y con distintas herramientas.

---

### **Fase 1 – Acceso coordinado vía API**

**Objetivo:** entender cómo leer/escribir memoria de otro proceso usando únicamente APIs documentadas.

1. Crea un programa **target** que contenga un buffer conocido (ej. un array con texto o números) y se mantenga en ejecución imprimiendo su PID.
    
2. Crea un programa **inspector** que:
    
    - Obtenga un `HANDLE` (Windows) o `fd`/`pid` (Linux).
        
    - Lea la memoria del target con `ReadProcessMemory` (Windows) o `/proc/<pid>/mem` (Linux, con permisos).
        
3. Verifica que el valor leído desde el inspector coincide con el que imprime el target.
    

---

### **Fase 2 – Depuración en vivo**

**Objetivo:** inspeccionar y modificar memoria en tiempo real.

1. Abre el target en un depurador (`WinDbg` o `gdb`).
    
2. Detén la ejecución y localiza la variable/buffer (puedes usar el símbolo o dirección impresa).
    
3. Muestra el contenido (`dps` en WinDbg, `x/` en gdb).
    
4. Modifica el valor desde el depurador y continúa la ejecución.
    
5. Observa que el cambio se refleja en el programa en ejecución.
    

---

### **Fase 3 – Análisis de minidump**

**Objetivo:** confirmar que la información es consistente en un volcado parcial.

1. Genera un **minidump** del target:
    
    - Windows: `MiniDumpWriteDump` o _Create Dump File_ en Task Manager.
        
    - Linux: usa `gcore` para crear un core dump.
        
2. Ábrelo en WinDbg (Windows) o `gdb` (Linux).
    
3. Localiza la variable/buffer y verifica que su contenido coincide con el estado observado en vivo.
    
4. Documenta offsets y direcciones relativas para uso posterior.
    

---

### **Fase 4 – Análisis forense offline**

**Objetivo:** localizar estructuras conocidas en un volcado completo.

1. Genera un volcado de **toda la RAM de la VM**:
    
    - Linux: `avml` o LiME.
        
    - Windows: WinPMEM.
        
2. Abre el volcado en Volatility/Volatility3.
    
3. Localiza el proceso target (`pslist` / `linux.pslist`).
    
4. Examina regiones de memoria asignadas (`vadinfo` en Windows, `linux_proc_maps` en Linux).
    
5. Busca el contenido del buffer/variable con `strings` o `yarascan`.
    
6. Confirma que coincide con lo visto en fases anteriores.
    

---

### **Fase 5 – Observabilidad con eBPF**

**Objetivo:** ver la actividad de memoria y E/S en vivo desde el kernel sin escribir drivers.

1. Instala `bcc` o `bpftrace` en la VM Linux.
    
2. Usa scripts predefinidos:
    
    - `execsnoop` → para ver ejecuciones de procesos.
        
    - `opensnoop` → para ver apertura de archivos.
        
    - `sys_enter_read` y `sys_exit_read` → para interceptar lecturas de memoria/E/S.
        
3. Ejecuta el target y el inspector.
    
4. Observa las llamadas al sistema que se generan y mapea esas syscalls con las operaciones vistas en vivo y en los volcados.
    

---

### **Resultado esperado**

Al final de este plan:

- Podrás **seguir un mismo artefacto** desde que se crea en un programa hasta que lo ves en un volcado forense.
    
- Entenderás cómo **API, depurador, minidump, volcado completo y eBPF** se complementan para dar distintas perspectivas de la misma información.
    
- Tendrás claro qué limitaciones y protecciones pueden alterar los resultados (ASLR, permisos, etc.).
    

---

