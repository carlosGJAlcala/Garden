---
title: "Shellcode - Creación y uso en explotación"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
# Shellcode - Creación y uso en explotación

> **Relacionado**: Ver [[02-Ciencias-Computacion/Lenguajes-Programacion/C/Ejemplos/Buffer-OverFlow-y-Condiciiones-de-Carrera|Buffer Overflow]] para vulnerabilidades de memoria. [[01-Ciberseguridad/Ingenieria-Inversa/2025-03-25-exploit|Desarrollo de exploits]]. [[01-Ciberseguridad/Ingenieria-Inversa/Immunity-debugger-y-Ghidra|Ghidra/Immunity Debugger]] para análisis. [[01-Ciberseguridad/Fundamentos/malware-oculto|Técnicas de ocultación]].

Sí, para crear **shellcode**, modificar el código fuente no es estrictamente necesario, pero sí puede facilitar el proceso dependiendo del enfoque que uses. Te explico los aspectos clave:

### **¿Qué es un Shellcode?**

Un **shellcode** es un fragmento de código en lenguaje ensamblador diseñado para ser inyectado y ejecutado en la memoria de un proceso. Se usa en exploits para ejecutar comandos arbitrarios, obtener una shell o realizar otras acciones maliciosas o de prueba de seguridad.

### **¿Se necesita modificar el código fuente?**

Depende del caso:

1. **Si tienes acceso al código fuente**
    
    - Puedes modificarlo para incluir una vulnerabilidad controlada (como un buffer overflow).
    - Puedes insertar un payload directamente en el código en C o ensamblador antes de compilarlo.
    - Puedes desactivar protecciones como **DEP (Data Execution Prevention)** y **ASLR (Address Space Layout Randomization)** si estás trabajando en un entorno de pruebas.
2. **Si no tienes acceso al código fuente**
    
    - Debes trabajar con binarios ya compilados, usando técnicas de inyección de código, explotación de vulnerabilidades de memoria, o modificación con herramientas como Ghidra, Radare2 o Immunity Debugger.
    - Puedes buscar gadgets útiles con **ROP (Return Oriented Programming)** si el entorno tiene restricciones como **NX (No eXecute)**.

### **Proceso Básico de Creación de un Shellcode**

1. **Escribir el shellcode en ensamblador**  
    Se usa ensamblador para escribir instrucciones pequeñas y eficientes. Un ejemplo de shellcode simple en Linux para ejecutar `/bin/sh`:
    
    ```assembly
    section .text
    global _start
    
    _start:
        xor rax, rax
        push rax
        mov rdi, 0x68732f6e69622f
        push rdi
        mov rdi, rsp
        xor rsi, rsi
        xor rdx, rdx
        mov al, 59
        syscall
    ```
    
2. **Compilar a binario**  
    Se ensambla y enlaza con `nasm` y `ld`:
    
    ```bash
    nasm -f elf64 shellcode.asm -o shellcode.o
    ld shellcode.o -o shellcode
    ```
    
3. **Extraer los opcodes**  
    Usamos `objdump` para obtener los bytes que se usarán como shellcode:
    
    ```bash
    objdump -d shellcode | grep '[0-9a-f]:' | cut -f2 -d':' | tr -s ' ' | cut -d' ' -f2- | tr -d '\n' | sed 's/ /\\x/g'
    ```
    
    Esto generará algo como:
    
    ```c
    "\x48\x31\xc0\x50\x48\xbb\x2f\x62\x69\x6e\x2f\x73\x68\x50\x48\x89\xe7\x48\x31\xf6\x48\x31\xd2\xb0\x3b\x0f\x05"
    ```
    
4. **Inyectarlo en otro programa**  
    En C podríamos ejecutarlo así:
    
    ```c
    #include <stdio.h>
    #include <string.h>
    
    int main() {
        unsigned char shellcode[] = "\x48\x31\xc0\x50\x48\xbb\x2f\x62\x69\x6e\x2f\x73\x68\x50\x48\x89\xe7\x48\x31\xf6\x48\x31\xd2\xb0\x3b\x0f\x05";
        void (*exec)() = (void (*)())shellcode;
        exec();
    }
    ```
    
    Se compila con:
    
    ```bash
    gcc -z execstack shellcode.c -o shellcode_exec
    ```
    

### **Conclusión**

No es obligatorio modificar el código fuente para hacer shellcode, pero si tienes acceso al código, puedes insertar exploits de manera más controlada. Si trabajas con binarios ya compilados, necesitarás técnicas de ingeniería inversa y explotación de memoria.