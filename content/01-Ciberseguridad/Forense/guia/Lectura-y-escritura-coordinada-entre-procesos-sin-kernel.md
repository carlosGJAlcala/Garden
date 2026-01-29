---
title: "Lectura Y Escritura Coordinada Entre Procesos Sin Kernel"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---
Te amplío esa sección para que quede como una práctica guiada y con contexto, conectando la **sincronización de recursos entre procesos** con la **detección forense de mutex nombrados como IOC**.

---

## **Lectura y escritura coordinada entre procesos (sin kernel)**


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Forense/guia/Acceso-y-analisis-de-memoria-en-Linux-y-Windows|Acceso y analisis de memoria en Linux y Windows]]. [[03-Desarrollo-Software/Paradigmas/Paradigmas-de-Objectivos/Paradigma-Concurrente-Memoria-Comun|Paradigma Concurrente Memoria Comun]].

El objetivo es reproducir, en un entorno seguro, **condiciones reales de competencia por recursos** (race conditions) y cómo el sistema operativo las resuelve usando mecanismos de sincronización a nivel de usuario. Esta práctica te ayuda a comprender por qué un **mutex nombrado** o un **lock de archivo** puede dejar rastro en memoria y convertirse en un **indicador de compromiso (IOC)**.

---

### **1. Contexto**

- En sistemas multiusuario/multitarea, varios procesos pueden intentar acceder simultáneamente a un recurso compartido (archivo, socket, región de memoria mapeada).
    
- El sistema operativo provee **bloqueos coordinados** que evitan corrupción de datos o condiciones de carrera.
    
- Estos bloqueos pueden ser:
    
    - **En disco/archivo** (persisten mientras el descriptor esté abierto).
        
    - **En memoria/nombrados** (persisten en la tabla de objetos del sistema operativo).
        

Cuando un malware crea un **mutex nombrado** global, ese objeto queda **visible en memoria** y puede ser listado con herramientas forenses o de depuración, convirtiéndose en un IOC.

---

### **2. En Linux**

**Bloqueo con `fcntl`** (bloqueo de archivo por proceso):

```c
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int fd = open("datos.txt", O_WRONLY | O_CREAT, 0644);

    struct flock fl = {0};
    fl.l_type = F_WRLCK; // Bloqueo de escritura
    fcntl(fd, F_SETLKW, &fl);

    printf("Bloqueo activo, presiona Enter para liberar...\n");
    getchar();

    fl.l_type = F_UNLCK; // Liberar
    fcntl(fd, F_SETLK, &fl);
    close(fd);
}
```

En Java, equivalente interoperable:

```java
try (FileChannel ch = FileChannel.open(Paths.get("datos.txt"), StandardOpenOption.WRITE)) {
    FileLock lock = ch.lock();
    System.out.println("Bloqueo activo");
    System.in.read();
    lock.release();
}
```

 Si ejecutas ambos programas a la vez, verás que uno se queda esperando hasta que el otro libere el lock.

---

### **3. En Windows**

**C con `LockFileEx`**:

```c
#include <windows.h>
#include <stdio.h>

int main() {
    HANDLE hFile = CreateFile("datos.txt", GENERIC_WRITE, 0, NULL, OPEN_ALWAYS, 0, NULL);
    OVERLAPPED ov = {0};
    LockFileEx(hFile, LOCKFILE_EXCLUSIVE_LOCK, 0, MAXDWORD, MAXDWORD, &ov);
    printf("Bloqueo activo, presiona Enter para liberar...\n");
    getchar();
    UnlockFileEx(hFile, 0, MAXDWORD, MAXDWORD, &ov);
    CloseHandle(hFile);
}
```

En Java (NIO):

```java
try (FileChannel ch = FileChannel.open(Paths.get("datos.txt"), StandardOpenOption.WRITE)) {
    FileLock lock = ch.lock();
    System.out.println("Bloqueo activo");
    System.in.read();
    lock.release();
}
```

---

### **4. Observación del arbitraje**

- **En Linux**: ejecuta `strace -p <PID>` para ver las syscalls `fcntl` bloqueando/desbloqueando.
    
- **En Windows**: usa **Process Monitor** (ProcMon) para ver llamadas a `LockFileEx` y `UnlockFileEx`.
    

Esto demuestra cómo el SO gestiona y coordina accesos entre procesos sin que tengamos que entrar en ring 0.

---

### **5. Conexión con los mutex como IOC**

- Un **mutex nombrado** en Windows (o un objeto de sincronización equivalente en Linux) deja una **huella persistente en memoria** mientras esté vivo.
    
- Herramientas como Volatility (`windows.handles`) o Sysinternals (`Handle.exe`) pueden listar estos objetos.
    
- Malware aprovecha mutex nombrados para evitar que se ejecute otra copia de sí mismo.
    
- Analistas forenses los usan como IOC porque:
    
    - Suelen tener nombres únicos o identificativos.
        
    - Persisten en memoria aunque el malware intente ocultar otros rastros.
        

---

 **Ejercicio extra**:  
Crea un mutex nombrado en Windows con `CreateMutex` o en .NET con `Mutex("NombreGlobal", ...)`. Luego, con Sysinternals:

```cmd
handle.exe | findstr NombreGlobal
```

Verás cómo puedes detectar su existencia, igual que harías en una investigación forense.

---

Si quieres, puedo unir esto con un **laboratorio forense** donde se cree un mutex nombrado, se observe en ejecución, y luego se detecte con Volatility a partir de un volcado de memoria. ¿Quieres que lo prepare?