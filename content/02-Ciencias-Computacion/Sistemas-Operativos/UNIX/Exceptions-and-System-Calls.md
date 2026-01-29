---
title: "Exceptions And System Calls"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
## Contenido


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

- [Modos de Operación de la CPU](#modos-de-operaci%C3%B3n-de-la-cpu)
- [Unidad de Protección de Memoria (MPU)](#unidad-de-protecci%C3%B3n-de-memoria-mpu)
- [Excepciones](#excepciones)
- [Programación de Llamadas al Sistema](#programaci%C3%B3n-de-llamadas-al-sistema)
- [Ejercicios](#ejercicios)

---

## Modos de Operación de la CPU

- **Modos de operación**:
    - **Supervisor**: permite ejecutar todas las instrucciones.
    - **Usuario**: restringido a instrucciones de usuario, sin acceso a instrucciones privilegiadas (`STI`, `CLI`, `IN`, `OUT`, etc.).
- Al iniciar, la CPU siempre está en modo supervisor.
- Cambio de modo:
    - **SVC**: cambia de usuario a supervisor, almacenando el estado en la pila de supervisor y ajustando la IP a un valor fijo (`0x0006`).
    - **SRET**: cambia de supervisor a usuario, restaurando el SP, IP y registro de estado.

## Unidad de Protección de Memoria (MPU)

- La MPU bloquea el acceso a regiones de memoria, configurado con los registros `MEMPTSTART` y `MEMPTEND`.
- **Registro MEMPTSTART**:
    - **Protección activada**: `1` para habilitar, `0` para deshabilitar.
    - **Modo de escritura**: `1` para permitir escritura en modo usuario/supervisor.
    - Dirección de inicio calculada como `START_ADDRESS * 16`.
- **Registro MEMPTEND** define el final de la región de memoria protegida.

## Excepciones

- Las excepciones ocurren al ejecutar una instrucción y se manejan solo en modo usuario.
- **Tipos de excepciones**:
    1. `DIVIDE_BY_ZERO`: divisor en una instrucción `div` es cero.
    2. `INSTRUCTION_FETCH_ERROR`: error al buscar la siguiente instrucción.
    3. `MEMORY_ACCESS_ERROR`: acceso a posición de memoria prohibida.
    4. `UNKNOWN_OPCODE`: código de operación desconocido.
    5. `ILLEGAL_INSTRUCTION`: instrucción privilegiada en modo usuario.
    6. `STACK_ACCESS_ERROR`: error de acceso a la pila.
- **Frame de excepción**:
    - Almacena información sobre la excepción: tipo, posición de memoria, SP y registro de estado al momento de la excepción.

## Programación de Llamadas al Sistema

- En sistemas convencionales, las aplicaciones corren en modo usuario y el kernel en modo supervisor.
- Las aplicaciones solicitan servicios mediante instrucciones de sistema (como `TRAP` en simuladores).
- **Rutina de manejo de llamadas al sistema**:
    - Cada llamada puede manejar múltiples servicios con parámetros variables.
    - Los parámetros se pasan por registros, pila o ubicaciones de memoria fijas.
- Ejemplo: añadir una llamada al sistema `print_pixel` para colorear un píxel específico.
    - **Parámetros**:
        - `A`: número de llamada (2)
        - `BH`: coordenada X
        - `BL`: coordenada Y
        - `CL`: color

## Ejercicios

1. Añadir la llamada al sistema `print_pixel` al programa de ejemplo.
2. Implementar el código del sistema y el envoltorio de usuario para `print_pixel`.