---
title: "Conceptos Base"
date: 2026-01-26
tags:
  - ciberseguridad
  - forense
  - guia
---

# Conceptos base (qué debes dominar primero)


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

Antes de tocar cualquier herramienta o volcado, es clave entender cómo se organiza y protege la memoria en un sistema operativo moderno, porque esto explica tanto **por qué un proceso normal no puede ver la memoria de otro** como **por qué un código en ring 0 sí puede hacerlo**.


---

### **1. Traducción de direcciones y la MMU**

En un sistema operativo moderno, **cada proceso en modo usuario (ring 3)** trabaja en lo que parece ser **su propia memoria completa y aislada**. Esa visión es una **abstracción**: en realidad, la memoria que ve el proceso es **memoria virtual**, no la memoria física real.  
La tarea de **traducir direcciones virtuales a direcciones físicas** la realiza un componente de hardware especializado: la **MMU** (_Memory Management Unit_).

Esta traducción ocurre **en cada acceso a memoria** y sigue reglas definidas por el sistema operativo a través de las **tablas de páginas**.  
La separación entre memoria virtual y física tiene varias ventajas:

- **Aislamiento** entre procesos (seguridad).
    
- **Protección** contra corrupción accidental de memoria.
    
- **Flexibilidad** para asignar o mover páginas sin que el proceso lo note.
    
- **Soporte de swapping** y asignación perezosa (_lazy allocation_).
    

---

#### **Registro CR3 y tablas de páginas**

En arquitecturas **x86/x86_64**, la MMU obtiene la dirección base de la tabla de páginas desde el **registro CR3**.

- El **kernel** es quien configura CR3 cuando crea o cambia el contexto de un proceso.
    
- Cada proceso tiene su propia tabla de páginas; al hacer un _context switch_, el kernel actualiza CR3 para apuntar a la tabla del proceso que pasa a ejecutarse.
    
- Esto garantiza que un proceso solo tenga acceso a las páginas que le pertenecen (y al espacio compartido del kernel).
    

---

#### **Organización en páginas**

La memoria virtual está dividida en **páginas**:

- Lo habitual es usar páginas pequeñas de **4 KB**.
    
- Para mejorar rendimiento en aplicaciones que manejan grandes bloques de datos, las CPUs modernas soportan **páginas grandes** de **2 MB** (huge pages) o incluso **1 GB** (giant pages), lo que reduce el coste de traducción.
    
- Cada página se asocia a un **marco de página** (_page frame_) en memoria física, o bien puede estar almacenada en disco si ha sido _swappeada_.
    

---

#### **El TLB (Translation Lookaside Buffer)**

Acceder a las tablas de páginas en cada operación sería muy costoso. Por eso, la CPU cuenta con una caché interna especializada llamada **TLB** (_Translation Lookaside Buffer_):

- El TLB guarda traducciones recientes de direcciones virtuales a físicas.
    
- Si la dirección solicitada está en el TLB (**TLB hit**), el acceso es inmediato.
    
- Si no está (**TLB miss**), la CPU consulta las tablas de páginas en memoria, lo que implica más ciclos de CPU y posibles fallos de página (_page faults_).
    

El **rendimiento** del sistema depende mucho de la tasa de aciertos en el TLB.

---

#### **Permisos RWX y bit de usuario/kernel**

Cada entrada en la tabla de páginas (_Page Table Entry_, PTE) tiene **bits de control** que definen:

- **R/W/X** (Read, Write, Execute): si la página se puede leer, escribir o ejecutar.
    
- **U/S** (User/Supervisor): si la página es accesible desde modo usuario (ring 3) o solo desde el kernel (ring 0).
    
- Bits adicionales para caché, presencia en memoria, uso reciente, etc.
    

Estos permisos permiten que:

- El kernel proteja su espacio de memoria para que no pueda ser tocado por procesos en ring 3.
    
- Se bloquee la ejecución de código en regiones que solo deben contener datos (_Data Execution Prevention_ / NX bit).
    

---


---

### **2. KASLR (Kernel Address Space Layout Randomization)**

KASLR es una técnica de **seguridad por ocultación** introducida en Linux a partir de la versión 3.14 y en Windows desde Windows 8.1/Server 2012 R2. Su objetivo es **dificultar la explotación de vulnerabilidades en el kernel** y proteger contra ataques de tipo _ROP_ (Return-Oriented Programming) o de lectura arbitraria de memoria.

**Cómo funciona**:

- En cada arranque, el kernel **elige una posición aleatoria** en memoria virtual para cargar su código y estructuras de datos clave.
    
- La aleatorización afecta no solo a la base del kernel, sino también a:
    
    - Módulos cargables.
        
    - Pilas del kernel.
        
    - Estructuras de datos estáticas importantes.
        
- Esto rompe la suposición de direcciones fijas que un atacante podría usar para saltar directamente a funciones críticas.
    

**Implicaciones para análisis forense**:

- **Sin símbolos** (archivos PDB en Windows, System.map en Linux) no puedes asumir direcciones constantes entre sesiones.
    
- Las herramientas forenses deben localizar patrones conocidos o usar _signatures_ para encontrar estructuras en la memoria dump.
    
- La aleatorización se reinicia **cada vez que el sistema arranca**, por lo que incluso en la misma máquina las direcciones cambian.
    

 **Ejemplo**: si antes de KASLR el kernel siempre arrancaba en `0xffffffff81000000`, con KASLR podría arrancar en algo como `0xffffffff82430000` en un arranque y `0xffffffff81f00000` en el siguiente.

---

### **3. SMEP y SMAP**

En arquitecturas x86_64 modernas, Intel introdujo dos extensiones importantes para endurecer la separación entre memoria de usuario y kernel:

#### **SMEP – Supervisor Mode Execution Prevention**

- **Función**: impide que el código en modo supervisor (ring 0) **ejecute instrucciones** que se encuentren en páginas marcadas como _user-space_.
    
- **Objetivo**: prevenir ataques que inyecten código malicioso en memoria de usuario y luego provoquen que el kernel lo ejecute, por ejemplo, mediante explotación de punteros de función.
    
- **Mecánica**: si SMEP está activado y el kernel intenta ejecutar desde una dirección marcada como de usuario, la CPU genera una excepción de protección.
    

#### **SMAP – Supervisor Mode Access Prevention**

- **Función**: impide que el kernel **lea o escriba datos** de páginas de usuario mientras está en modo supervisor, salvo que temporalmente desactive la protección.
    
- **Objetivo**: evitar que errores de validación o desbordamientos permitan que el kernel manipule datos de usuario sin control.
    
- **Mecánica**: para acceder legalmente a memoria de usuario, el kernel debe usar instrucciones especiales:
    
    - `stac` (_Set AC flag_): habilita temporalmente el acceso.
        
    - `clac` (_Clear AC flag_): lo deshabilita de nuevo.
        
- **Ventaja**: incluso si un driver o módulo en ring 0 es comprometido, estas protecciones reducen el impacto al bloquear accesos accidentales o no autorizados.
    

 **Relación con seguridad**: SMEP y SMAP no impiden que el kernel mapee memoria arbitraria, pero añaden un paso extra y validaciones para acceder a datos o código fuera de su espacio seguro.

---
---

### **4. Transición de ring 3 a ring 0 (explicado en detalle)**

En un sistema moderno, **ring 3** es el modo usuario: el código se ejecuta con privilegios limitados y no puede acceder directamente al hardware o a memoria de otros procesos.  
**Ring 0** es el modo kernel: aquí se ejecuta el núcleo del SO y tiene control total de la máquina.

Cuando un proceso de usuario necesita que el sistema operativo haga algo privilegiado —por ejemplo, escribir en disco, abrir un socket o asignar memoria— **no puede hacerlo directamente**. En su lugar, hace una **llamada al sistema** (_syscall_).

#### Pasos internos:

1. El proceso de usuario ejecuta una instrucción especial (`syscall` o `sysenter` en x86_64, `svc` en ARM) para **cambiar al modo kernel**.
    
2. La CPU salta a un **trampoline** del kernel, cuya dirección y contexto están configurados en registros especiales (como `MSR_LSTAR` en x86_64 para `syscall`).
    
3. El kernel:
    
    - Guarda el estado del proceso (registros, flags, pila).
        
    - Valida los parámetros (para evitar accesos ilegales).
        
    - Busca el número de syscall en la **tabla de servicios** (`sys_call_table` en Linux) para saber qué función ejecutar.
        
4. Se ejecuta la función del kernel asociada.
    
5. El kernel devuelve el control a modo usuario con `sysret` o `sysexit`, restaurando el estado original.
    

---

### **Ejemplo seguro en C (Linux, llamada a write)**

Este ejemplo hace una llamada al sistema `write` directamente, usando la convención de Linux x86_64. No escala privilegios, simplemente imprime un mensaje por salida estándar sin pasar por la libc.

```c
#include <unistd.h>
#include <sys/syscall.h>

int main() {
    const char *msg = "Hola desde syscall\n";
    // syscall(SYS_write, fd=1, buffer, length)
    syscall(SYS_write, 1, msg, 20);
    return 0;
}
```

**Qué ocurre internamente**:

- `syscall()` es un wrapper de la libc que coloca el número de syscall (`SYS_write`) en el registro `rax`, los parámetros en `rdi`, `rsi`, `rdx`, y luego ejecuta la instrucción `syscall`.
    
- La CPU cambia a ring 0, salta al trampoline del kernel y ejecuta `sys_write` de la tabla `sys_call_table`.
    
- El kernel escribe en el descriptor de archivo 1 (stdout) y devuelve el control a ring 3.
    

---

 Si quieres ver este mecanismo _a bajo nivel_, puedes compilarlo con:

```bash
gcc -nostdlib -static -o test test.c
objdump -d test
```

y observarás la instrucción `syscall` generada en ensamblador.

### **5. Copias controladas vs accesos arbitrarios**

Cuando el kernel necesita interactuar con memoria que **no le pertenece directamente** —por ejemplo, datos que un proceso de usuario pasa a través de una llamada al sistema (_syscall_)— **no realiza un acceso directo a esa dirección virtual**. Esto no es por limitación técnica, sino por **seguridad y estabilidad**:

- Una dirección pasada por el proceso puede ser inválida.
    
- Puede estar mapeada pero no tener permisos de lectura/escritura.
    
- Puede provocar un fallo de página (_page fault_) que, si no se gestiona, derribe todo el sistema.
    

---

#### **En Linux**

El kernel utiliza funciones especiales para manejar estos casos:

- **`copy_from_user(void *to, const void __user *from, unsigned long n)`**  
    Copia datos desde el espacio de usuario a memoria del kernel.
    
- **`copy_to_user(void __user *to, const void *from, unsigned long n)`**  
    Copia datos desde memoria del kernel al espacio de usuario.
    

Estas funciones:

1. **Validan** que la dirección de usuario es accesible para la operación solicitada.
    
2. **Atrapan** excepciones de acceso inválido.
    
3. **Devuelven** la cantidad de bytes que no se copiaron (0 si la copia fue exitosa).
    

Para validaciones más específicas, el kernel también expone:

- `access_ok()` → comprueba que un puntero de usuario está en un rango permitido.
    
- `get_user()` / `put_user()` → copian valores simples (por ejemplo, enteros) de forma segura.
    

---

#### **En Windows**

El kernel ofrece mecanismos equivalentes:

- **`ProbeForRead(PVOID Address, SIZE_T Length, ULONG Alignment)`**  
    Comprueba que una región de memoria de usuario es legible y está alineada correctamente.
    
- **`ProbeForWrite(PVOID Address, SIZE_T Length, ULONG Alignment)`**  
    Comprueba que una región de memoria de usuario es escribible.
    

Estos métodos:

1. Validan que la página pertenece al espacio de usuario.
    
2. Garantizan que el acceso cumple las reglas de alineación y permisos.
    
3. Si la comprobación falla, lanzan una excepción que el driver puede manejar.
    

---

#### **Por qué se usan**

- **Evitan que un fallo en un puntero de usuario corrompa memoria del kernel**.
    
- **Protegen la estabilidad del sistema**: un fallo de acceso se convierte en un error controlado, no en un cuelgue.
    
- **Proporcionan trazabilidad**: si la validación falla, el kernel puede registrar el error o abortar la operación de forma segura.
    

---

#### **Acceso arbitrario**

Un driver malicioso o mal programado puede omitir estos pasos y:

- Acceder directamente a direcciones de usuario usando un _cast_ y desreferenciación (`*ptr`).
    
- Manipular tablas de páginas para mapear memoria física arbitraria y leer/escribir sin validación.
    

Esto le permite:

- **Leer cualquier dirección física**.
    
- **Escribir en memoria crítica del kernel o de otros procesos**.
    
- **Eludir protecciones como SMEP/SMAP** si ya corre en ring 0.
    

Pero este comportamiento:

- **Rompe el modelo de seguridad del SO**.
    
- **Es inestable**: un puntero incorrecto puede provocar un _kernel panic_ o _BSOD_.
    
- En entornos reales, se considera una **técnica de rootkit**.
    

---

 **Resumen práctico**:  
En código legítimo de ring 0, **todas las interacciones con memoria de usuario** deben pasar por las funciones de copia y validación que ofrece el sistema. El acceso arbitrario solo se ve en malware, PoCs de explotación o errores graves de programación.

---



---

### **6. Implicación práctica**

Cuando conectas todos los conceptos previos —MMU, tablas de páginas, CR3, KASLR, SMEP/SMAP, y funciones de copia segura— obtienes una imagen completa de cómo el sistema operativo y el hardware gestionan la memoria. Esto tiene consecuencias claras tanto para la seguridad como para el análisis forense.

---

#### **1. Por qué el kernel ve toda la RAM**

El kernel, al ejecutarse en **ring 0**, tiene privilegios para:

- Acceder a cualquier dirección física.
    
- Cambiar los mapeos de direcciones virtuales a físicas en las tablas de páginas.
    
- Insertar o quitar mapeos de cualquier proceso.  
    Esto significa que **puede inspeccionar y modificar la memoria de cualquier proceso**, o incluso reservar y usar partes de la RAM para sí mismo.  
    Ejemplo legítimo: un _dump_ completo de memoria del sistema para análisis forense se hace mapeando toda la RAM desde el kernel.
    

---

#### **2. Por qué en modo usuario dependes de las APIs**

En **ring 3**, no tienes acceso a las estructuras internas del kernel ni a la MMU:

- Tus accesos a memoria son validados por la CPU usando las tablas de páginas asignadas a tu proceso.
    
- Si intentas leer fuera de tu espacio de direcciones, recibes una **violación de segmento** (Linux) o un **Access Violation** (Windows).
    
- La única forma de leer o escribir memoria de otro proceso es pedir al kernel que lo haga por ti, usando APIs como `ReadProcessMemory` (Windows) o `ptrace` (Linux).  
    Esto no es una limitación de programación, sino una **política de seguridad** respaldada por hardware.
    

---

#### **3. Cómo KASLR, SMEP y SMAP añaden barreras**

- **KASLR** → impide que un atacante o analista sin símbolos fijos ubique fácilmente funciones o estructuras del kernel, ya que sus direcciones cambian en cada arranque.
    
- **SMEP** → evita que el kernel ejecute código que esté mapeado en memoria de usuario, incluso si el atacante logra manipular punteros de función.
    
- **SMAP** → evita que el kernel lea/escriba memoria de usuario de forma accidental o maliciosa, salvo que temporalmente levante la restricción de forma explícita.  
    Estas tecnologías no hacen imposible el acceso, pero sí elevan el nivel de dificultad para explotar vulnerabilidades o para realizar un análisis directo de memoria en vivo desde ring 0.
    

---

#### **Impacto para el análisis y la seguridad**

- **En ciberseguridad ofensiva**: obliga a conocer y sortear protecciones de hardware/OS para acceder a memoria arbitraria.
    
- **En análisis forense**: exige usar técnicas que respeten estas protecciones (por ejemplo, volcados de memoria a través de controladores legítimos o APIs documentadas).
    
- **En desarrollo de software de bajo nivel**: fuerza a programar drivers y módulos usando funciones seguras (`copy_from_user`, `ProbeForRead`) para no romper estabilidad ni seguridad.
    

---

 **En resumen**: entender este modelo te permite interpretar por qué ciertas operaciones son imposibles desde modo usuario, por qué el kernel es tan poderoso, y cómo las protecciones modernas limitan ese poder para evitar abusos.

---
