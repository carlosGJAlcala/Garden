---
title: "2025 02 18 Ingenieria Inversas"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---

Siempre hay un `push ebp`, seguido de `mov ebp, esp`. Esto configura el `ebp` como el nuevo marco de pila, permitiendo un acceso ordenado a los parámetros y variables locales.

El `push ecx` mueve el puntero de pila (`esp`) 4 bytes hacia abajo.

## Convenciones de llamadas


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

### Cdecl

En la convención **cdecl**, el **llamador** es el responsable de limpiar la pila. Para ello, realiza un `add esp, <bytes>` después de usar los argumentos.

### Stdcall

En **stdcall**, el **llamado** es quien limpia la pila, lo que significa que la función se encarga de ajustar `esp` antes de retornar. El resultado se almacena en `EAX`. En **Ghidra**, cuando una función está marcada como `stdcall`, se puede observar que realiza un `pop` antes de retornar.

### Fastcall

En **fastcall**, se utilizan registros en lugar de la pila para pasar algunos parámetros, lo que mejora el rendimiento. La restauración de la pila se hace dentro de la función, y la optimización del compilador juega un papel importante en este esquema.

## Ghidra y Reversing

Para hacer **reversing** en Ghidra y localizar la función `main`, se debe buscar una firma típica como:

```c
int WINAPI wWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
```

Esta función es el punto de entrada en aplicaciones Windows que usan la API de Win32.

### KillSwitch y WannaCry

Un **KillSwitch** es un mecanismo diseñado para detener la ejecución de un malware bajo ciertas condiciones. En el caso de **WannaCry**, se utilizó un **dominio no registrado** como killswitch. Cuando el malware intentaba conectarse a este dominio y recibía una respuesta válida, se desactivaba.

El malware suele dividirse en **stages** o fases, lo que dificulta su análisis. WannaCry, por ejemplo, tenía una fase en la que se instalaba y otra en la que ejecutaba su carga maliciosa.

Algunos **IOC (Indicators of Compromise)** de WannaCry incluyen archivos como `tasksche.exe`, utilizados para persistencia.

Los malwares pueden utilizar **Tor** para comunicarse con su C2 (Command & Control) de forma anónima.

## Herramientas útiles para análisis de malware

- **icoutils**: Permite extraer el icono embebido en archivos ejecutables.
- **wrestool**: Examina qué recursos están incrustados en un ejecutable.
- **strncpy**: Es una versión segura de `strcpy`, utilizada para copiar cadenas con una longitud máxima especificada. En ensamblador, se puede ver como un loop (`for`) que copia en bloques de 4 bytes.
- **InternetOpenUrlA**: Función de la API de WinInet utilizada por los malwares para establecer conexiones HTTP.
