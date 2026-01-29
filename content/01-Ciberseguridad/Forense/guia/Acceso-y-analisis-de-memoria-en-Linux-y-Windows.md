---
title: "Objetivo"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---

# Objetivo


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/STUB|STUB]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Heaps|Heaps]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]].

Comprender cómo la MMU, las tablas de páginas y el kernel median el acceso a memoria; practicar lectura/escritura de memoria **propia** y de **otros procesos** usando APIs/documentación soportada; extraer y analizar memoria del sistema con herramientas forenses; observar llamadas y eventos del kernel sin escribir código en ring 0.

# Entorno de laboratorio

Trabaja siempre en máquinas virtuales con snapshots. Una VM Linux (Ubuntu o Debian) y una VM Windows te permiten romper cosas sin miedo. Activa símbolos de depuración y ten un disco aparte para volcados de memoria. No uses tu equipo principal.

# Conceptos base (qué debes dominar primero)

Empieza por la traducción de direcciones y la MMU: espacios de direcciones por proceso, páginas, TLB y permisos RWX. Revisa cómo el kernel configura CR3 y las tablas de páginas en x86_64, qué es KASLR y por qué dificulta localizar estructuras; por qué SMEP/SMAP bloquean accesos peligrosos desde kernel a userland; cómo se pasa de ring 3 a ring 0 mediante syscalls y trampolines (syscall/sysenter, stubs, tablas de servicios). Entiende la diferencia entre **copias controladas** (`copy_to_user`/`copy_from_user` en Linux, `ProbeForRead/Write` en Windows) y accesos arbitrarios. Así verás por qué un driver puede leer “todo”, pero el camino correcto en usuario son APIs del SO.

# Ruta segura en Linux (usuario y observabilidad)

Compila un programa C que lea y escriba **su propia memoria** con punteros y verifica con `gdb` qué regiones están mapeadas (`info proc mappings`). Practica inspección de otro proceso con permisos usando herramientas existentes: `gdb -p <pid>` para leer variables; `/proc/<pid>/maps` para ver mapeos; `dd` sobre `/proc/<pid>/mem` solo cuando el kernel lo permite y con el proceso detenido (aprende por qué suele estar restringido). Complementa con `strace` para observar syscalls de E/S y memoria. Da el salto a **eBPF** con herramientas tipo `bcc`/`bpftrace`: observa eventos como `sys_enter_read`, fallos de página y life‑cycle de procesos; es una forma moderna de “asomarte” al kernel sin escribir módulos.

# Ruta segura en Windows (usuario, depuración y minidumps)

Aprende a abrir otro proceso con `OpenProcess` y, si tienes privilegios, a leer su memoria con `ReadProcessMemory` y escribir con `WriteProcessMemory` en escenarios controlados (por ejemplo, dos programas tuyos: uno “target” y otro “inspector”). Genera **volcados** con `MiniDumpWriteDump` y estúdialos en **WinDbg** (o Visual Studio) para entender pilas, heaps y módulos. Juega con permisos y ASLR para ver cuándo fallan los accesos. Úsalo siempre en tu VM y con procesos de prueba.

# Forense de memoria de sistema completo

Practica adquisición en caliente y análisis fuera de línea. En Linux, utiliza **LiME** o **AVML** para un volcado completo en tu VM; en Windows, **WinPMEM**. Analiza con **Volatility/Volatility3**: enumera procesos, módulos, regiones mapeadas y cadenas, y entiende por qué los IOCs “de memoria” (mutex/handles, secciones, pipes) son tan potentes. Este flujo te enseña exactamente qué “vería” un driver sin tener que escribirlo.

# Lectura y escritura coordinada entre procesos (sin kernel)

Simula casos reales de competencia por recursos. En Linux, usa bloqueos de archivo con `fcntl` y en Java `FileChannel.lock()` para ver interoperabilidad real. En Windows, prueba `LockFileEx` desde C y el `FileLock` de NIO. Observa con `strace`/ProcMon cómo el SO arbitra el acceso. Esto te da intuición de sincronización, que es la base para entender por qué un mutex nombrado se convierte en IOC en memoria.

# Mitigaciones y su impacto

Explora cómo KASLR cambia direcciones base; cómo SMEP/SMAP cortan accesos kernel→user peligrosos; cómo la firma obligatoria de controladores y Secure Boot elevan la barrera para ring 0; por qué PatchGuard (KPP) en Windows vigila integridad del kernel. Comprender estas barreras es crucial para interpretar tanto límites de depuración como de adquisición forense.

# Plan de prácticas propuesto

Primero ejecuta programas propios: uno “target” que aloja un buffer y otro “inspector” que lo lee por API soportada. Luego detén el target con un depurador, examina regiones de memoria y confirma offsets. Extrae un **minidump** y valida en WinDbg que los datos coinciden. Repite en Linux con `gdb` adjunto y volcados parciales del heap. Finalmente, saca un **volcado completo** de la VM, ábrelo con Volatility y localiza las mismas estructuras, relacionando lo que viste en vivo con lo que ves offline. Cierra con ejercicios de eBPF observando syscalls relacionadas con memoria y E/S.

# Qué no hacer (y por qué)

No intentes “leer todo” desde ring 0 ni escribir módulos del kernel por tu cuenta: es un atajo a técnicas de rootkit. Las mismas habilidades se aprenden más seguro con depuración, dumps y eBPF, y son válidas para DFIR, pentest defensivo y auditoría.

# Resultado esperado

Al terminar deberías poder explicar con claridad cómo se traduce una dirección virtual hasta la física, qué partes del kernel participan en un acceso entre procesos, cuándo y cómo puedes leer/escribir memoria de otro proceso **solo** por vías legítimas, y cómo adquirir y analizar memoria de un sistema de forma pericial.

Si quieres, adapto esto a un itinerario de 2–3 semanas con hitos diarios en tus VMs (Linux y Windows) y con comandos concretos para cada sesión de práctica. ¿Lo preparo así de estructurado?