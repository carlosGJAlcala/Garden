---
title: "Ruta Segura En Windows Usuario Depuracion Y Minidumps"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---
Te desarrollo esa sección como hicimos con la de Linux, pero enfocada en **Windows** y siempre desde un enfoque seguro (modo usuario y herramientas soportadas por Microsoft).

---

## **Ruta segura en Windows (usuario, depuración y minidumps)**


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

El objetivo aquí es **comprender cómo inspeccionar y modificar memoria de procesos en Windows** usando solo APIs documentadas, depuradores y volcados (_dumps_) de memoria. Así puedes aprender los mismos conceptos que usaría un programa de ring 0, pero respetando el modelo de seguridad del sistema.

---

### **1. Leer y escribir memoria propia**

Crea un programa simple en C/C++ que:

- Declare una variable.
    
- Imprima su dirección.
    
- Espere entrada para mantenerse vivo.
    

Ejemplo:

```c
#include <windows.h>
#include <stdio.h>

int main() {
    int valor = 42;
    printf("PID: %lu\n", GetCurrentProcessId());
    printf("Dirección de valor: %p\n", &valor);
    getchar(); // Esperar para que puedas adjuntar el depurador
    return 0;
}
```

Compílalo en Visual Studio o con `cl.exe`.

---

### **2. Inspeccionar y modificar con WinDbg**

- Abre **WinDbg** (puedes instalarlo con el Windows SDK).
    
- Adjunta al proceso:  
    **File → Attach to a Process** → selecciona el PID mostrado.
    
- Mostrar el contenido de la dirección:
    
    ```
    dd DIRECCION L1
    ```
    
    (`dd` = dump DWORDs, `L1` = longitud 1 DWORD).
    
- Modificar el valor:
    
    ```
    ed DIRECCION NUEVO_VALOR
    ```
    
- Reanuda el proceso (`g`).
    

Esto es el equivalente a leer/escribir memoria desde un depurador en Linux.

---

### **3. Usar APIs documentadas para leer/escribir otro proceso**

Windows ofrece funciones seguras para esto:

- **OpenProcess**: obtiene un handle al proceso con permisos adecuados.
    
- **ReadProcessMemory**: copia memoria del proceso objetivo a tu buffer.
    
- **WriteProcessMemory**: escribe datos en el proceso objetivo.
    

Ejemplo (simplificado):

```c
HANDLE h = OpenProcess(PROCESS_VM_READ | PROCESS_VM_WRITE | PROCESS_VM_OPERATION, FALSE, pid);
ReadProcessMemory(h, (LPCVOID)direccion, &buffer, sizeof(buffer), NULL);
WriteProcessMemory(h, (LPVOID)direccion, &nuevoValor, sizeof(nuevoValor), NULL);
CloseHandle(h);
```

 Solo funciona si tienes permisos para ese proceso (p. ej., ejecutando como administrador para procesos de sistema).

---

### **4. Volcados de memoria (Minidumps)**

Puedes capturar el estado completo o parcial de un proceso usando:

- **Task Manager** → clic derecho en el proceso → _Create dump file_.
    
- **ProcDump** (Sysinternals):
    
    ```cmd
    procdump -ma PID archivo.dmp
    ```
    
- **MiniDumpWriteDump** (API): permite crear minidumps programáticamente para análisis posterior.
    

---

### **5. Analizar el dump**

Abre el `.dmp` con:

- **WinDbg**:
    
    ```
    .examine
    dps DIRECCION
    ```
    
- **Visual Studio**: permite examinar variables y memoria como si el proceso estuviera en pausa.
    

---

### **6. Observar llamadas al sistema**

Puedes usar **Process Monitor (Procmon)** de Sysinternals para:

- Ver lecturas/escrituras de archivos.
    
- Mapas de memoria (operaciones `VirtualAlloc`, `VirtualFree`).
    
- Operaciones de red y registro.
    

Esto es similar a `strace` en Linux.

---

 **Ventaja del enfoque seguro**:

- No tocas ring 0.
    
- Usas herramientas oficiales y soportadas.
    
- Entiendes cómo interactúan procesos y memoria en Windows.
    
- Puedes practicar inyección de memoria controlada en tus propios procesos para comprender cómo se haría a nivel técnico, pero de forma ética.
    

---

Si quieres, puedo ahora añadir un **mini-laboratorio Windows paso a paso** donde:

1. Compilas dos programas (uno “target” y uno “inspector”).
    
2. El inspector lee y escribe memoria del target usando `ReadProcessMemory` y `WriteProcessMemory`.
    
3. Capturas un minidump del target y analizas la variable modificada con WinDbg.
    

¿Quieres que lo prepare así?