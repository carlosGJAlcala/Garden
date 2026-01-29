---
title: "The Linux Development Environment"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---


## Contenido


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

- [El Editor Vim](#el-editor-vim)
- [Opciones de Configuración](#opciones-de-configuraci%C3%B3n)
- [Referencia Rápida](#referencia-r%C3%A1pida)
- [Ayuda Integrada](#ayuda-integrada)
- [Ciclo de Creación de Programas](#ciclo-de-creaci%C3%B3n-de-programas)
- [Generación de Ejecutables](#generaci%C3%B3n-de-ejecutables)
- [Depuración](#depuraci%C3%B3n)
- [La Herramienta Make](#la-herramienta-make)
- [Ejemplo de un Makefile](#ejemplo-de-un-makefile)

---

## El Editor Vim

**Descripción general:**

- Vim (Vi iMproved) es un editor de archivos de código abierto para Linux.
- Desarrollado por Bram Moolenaar en 1991, escrito en C y Vimscript.
- Extensible mediante plugins.

**Modos de trabajo:**

1. **Modo Normal**: Navegación, copiar/pegar, y eliminación de texto.
2. **Modo de Inserción**: Edición de texto.
3. **Modo de Línea de Comando**: Acepta comandos en lenguaje Vimscript.
4. **Modo Visual**: Selección de texto.

## Opciones de Configuración

Editar el archivo `~/.vim/vimrc` para modificar las opciones de configuración. Ejemplos:

vim

Copiar código

`syntax on            " Activa el resaltado de sintaxis set tabstop=4        " Tabulación de 4 espacios set shiftwidth=4     " Indentación de 4 espacios set expandtab        " Usa espacios en lugar de TAB autocmd FileType make setlocal noexpandtab`

## Referencia Rápida

**Movimiento de cursor:**

- `k`: arriba, `j`: abajo, `h`: izquierda, `l`: derecha
- `Ctrl+b`: página atrás, `Ctrl+f`: página adelante

**Modos de inserción:**

- `i`: en el cursor, `a`: después del cursor, `o`: nueva línea abajo

**Borrar/cortar:**

- `x`: borrar carácter en el cursor, `dd`: borrar línea actual

**Guardar y salir:**

- `:w`: guardar archivo, `:q`: salir, `:wq`: guardar y salir

## Ayuda Integrada

- Para acceder a la documentación: `:help y` o `:h movement`.
- Tutorial complementario: `vimtutor`.

## Ciclo de Creación de Programas

**Etapas de desarrollo:**

1. Edición de código
2. Generación de ejecutables
3. Depuración

## Generación de Ejecutables

Ejemplo de programa en varios módulos (archivos `.c` y `.h`):

1. **Compilación**:
    
    bash
    
    
    `gcc -g -Wall -c main.c -o main.o` 
    `gcc -g -Wall -c add.c -o add.o`
    
2. **Enlace**:
    
    bash
    
    
    `gcc -g -Wall main.o add.o -o program`
    

Para ver contenido de archivos objeto: `objdump -D main.o | less`.

## Depuración

Comandos básicos en GDB:

- `run`: iniciar ejecución
- `break <posicion>`: establecer punto de interrupción
- `step`: ejecutar la siguiente instrucción (entra en funciones)
- `next`: siguiente instrucción (sin entrar en funciones)
- `print <variable>`: inspeccionar valor de una variable

## La Herramienta Make

**Descripción general:**

- Automática el proceso de generación de programas en múltiples módulos.
- Usa un archivo llamado `makefile` o `Makefile` para definir las reglas de compilación.

## Ejemplo de un Makefile

makefile

Copiar código

`.PHONY: clean  CC=gcc CFLAGS=-g -Wall  program: main.o add.o     $(CC) $(CFLAGS) main.o add.o -o program  main.o: main.c add.h     $(CC) $(CFLAGS) -c main.c -o main.o  add.o: add.c add.h     $(CC) $(CFLAGS) -c add.c -o add.o  clean:     rm -rf *.o program`

Comandos:

- Generar ejecutable: `$ make`
- Limpiar archivos intermedios: `$ make clean`

---

## Bibliografía

- Neil, D. _Practical Vim_. The Pragmatic Programmers, 2da Ed., 2015.
- [GNU Make Reference Manual](https://www.gnu.org/software/make/manual/make.html)