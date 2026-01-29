---
title: "Ruta Segura En Linux"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---
Te amplío esa sección con más detalle, ejemplos y contexto para que quede como una guía paso a paso de prácticas seguras en Linux para observación y manipulación de memoria en modo usuario.

---

## **Ruta segura en Linux (usuario y observabilidad)**


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

El objetivo de esta ruta es **comprender cómo funciona el acceso a memoria y a recursos del sistema en Linux** sin escribir código de kernel (ring 0), aprovechando únicamente herramientas y APIs legítimas en modo usuario. Esto te permite practicar de forma segura y reproducible en un laboratorio o máquina virtual.

---

### **1. Compilar un programa C que lea y escriba su propia memoria**

Crea un programa que:

- Declare una variable en memoria.
    
- Lea y escriba en ella usando punteros.
    
- Muestre su dirección con `printf` para poder inspeccionarla desde fuera.
    

Ejemplo mínimo:

```c
#include <stdio.h>

int main() {
    int valor = 42;
    printf("Valor inicial: %d\n", valor);
    printf("Dirección de valor: %p\n", (void*)&valor);
    valor = 99;
    printf("Valor modificado: %d\n", valor);
    while (1); // bucle para dejarlo vivo y poder inspeccionarlo
}
```

Compilación:

```bash
gcc -o memtest memtest.c
./memtest
```

---

### **2. Ver regiones de memoria con GDB**

- Abre otro terminal y adjunta `gdb` al proceso:
    
    ```bash
    gdb -p <pid>
    ```
    
- Lista regiones de memoria mapeadas:
    
    ```gdb
    info proc mappings
    ```
    
- Observa dónde están el binario, la pila, el heap, bibliotecas y áreas de memoria compartida.
    

---

### **3. Inspeccionar y modificar variables en vivo**

- En GDB, muestra el contenido de la dirección:
    
    ```gdb
    p *(int*)0xDIRECCION
    ```
    
- Modifica su valor:
    
    ```gdb
    set *(int*)0xDIRECCION = 1234
    ```
    

Esto simula lectura/escritura de memoria “externa”, pero solo dentro de tu propio proceso.

---

### **4. Observar otro proceso con permisos**

En un escenario controlado, puedes inspeccionar otro proceso que también sea tuyo:

- Listar mapeos:
    
    ```bash
    cat /proc/<pid>/maps
    ```
    
- Leer memoria (si está permitido y el proceso está detenido):
    
    ```bash
    sudo dd if=/proc/<pid>/mem bs=1 skip=OFFSET count=BYTES status=none
    ```
    

 Esto suele estar restringido por razones de seguridad; en muchas distribuciones modernas `/proc/<pid>/mem` es inaccesible salvo para depuradores con permisos.

---

### **5. Rastrear llamadas al sistema con `strace`**

Usa `strace` para ver qué syscalls de E/S y memoria ejecuta un proceso:

```bash
strace -p <pid> -e trace=read,write,mmap,munmap
```

Esto te muestra:

- Aperturas y cierres de archivos.
    
- Mapas y desmapas de regiones de memoria.
    
- Lecturas y escrituras.
    

---

### **6. Observabilidad avanzada con eBPF**

**eBPF** (_extended Berkeley Packet Filter_) permite inyectar programas seguros en el kernel para observar eventos en vivo sin escribir módulos.

Con **bcc**:

```bash
sudo apt install bpfcc-tools
sudo execsnoop-bpfcc
```

- Muestra qué procesos se están ejecutando.
    

Con **bpftrace**:

```bash
sudo bpftrace -e 'tracepoint:syscalls:sys_enter_read { printf("%s leyendo\n", comm); }'
```

- Informa cada vez que un proceso hace una syscall `read`.
    

Otros ejemplos útiles:

- Observar fallos de página:
    
    ```bash
    sudo bpftrace -e 'tracepoint:mm_vmscan_kswapd_wake { printf("Kswapd wakeup: %s\n", comm); }'
    ```
    
- Monitorizar ciclo de vida de procesos:
    
    ```bash
    sudo bpftrace -e 'tracepoint:sched:sched_process_exit { printf("Proceso %s terminó\n", comm); }'
    ```
    

---

 **Ventaja de este enfoque**:  
Todo lo haces desde **ring 3** usando APIs y herramientas oficiales. No comprometes la seguridad del sistema, pero aprendes a:

- Identificar regiones de memoria.
    
- Manipular datos en vivo.
    
- Observar interacción de procesos con memoria y kernel.
    

---

Si quieres, puedo ampliarte esta parte con **un diagrama del flujo de memoria en Linux** que muestre cómo se ven las regiones de código, heap, pila y bibliotecas en `/proc/<pid>/maps`, y cómo encajan con las direcciones que inspeccionas en GDB.  
¿Quieres que lo haga?