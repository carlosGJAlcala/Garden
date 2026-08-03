---
title: "Tipos De Analisis En Binarios Pe"
date: 2025-01-14
tags:
  - ciberseguridad
---

##  Ingeniería Inversa


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Herramientas/Rootkits-y-Hooking|Rootkits y Hooking]].

La **ingeniería inversa** consiste en analizar un programa o archivo binario para comprender su funcionamiento interno, su lógica y su comportamiento, sin tener acceso al código fuente original.

### Tipos de análisis en binarios PE (Portable Executable):

-  **Análisis dinámico**:  
    Se ejecuta el binario en un entorno controlado (sandbox) para observar su comportamiento (útil en análisis de malware).
    
-  **Análisis estático / Reversing**:  
    Se inspecciona el binario sin ejecutarlo, leyendo instrucciones en lenguaje ensamblador para reconstruir la lógica del programa.
    

---

## ️ Dependencia del ensamblador al procesador

El **lenguaje ensamblador** (assembly) está ligado a la **arquitectura del procesador**. No es lo mismo analizar binarios de:

- **Intel x86/x64** (arquitectura CISC, lectura de derecha a izquierda),
    
- que **ARM** (arquitectura RISC, lectura de izquierda a derecha).
    

Esto afecta tanto a la sintaxis como al orden de los operandos y la semántica de las instrucciones.

---

##  Android y su resistencia al reversing

El análisis en Android es especialmente complejo por varios factores:

- El código **se ofusca automáticamente** (por ejemplo con ProGuard o R8).
    
- Las aplicaciones pueden estar **empaquetadas** o incluso usar **descarga dinámica de código** (modularización por componentes).
    
- Se emplean técnicas anti-debugging y anti-reversing.
    

 Por estas razones, el **reversing de apps móviles** puede llegar a ser **más difícil que el análisis de malware clásico**.

---

##  Lenguaje ensamblador: conceptos clave

###  Descompilación vs Desensamblado

- **Desensamblar**: convertir el binario a instrucciones en ensamblador.  
    Herramientas: `objdump`, `IDA Free`, `radare2`, `Ghidra`.
    
- **Descompilar**: convertir el binario a un lenguaje de alto nivel (como C).  
    Herramientas: `Ghidra`, `Hex-Rays` (IDA Pro), `Snowman`.
    

> La descompilación es mucho más compleja que el desensamblado, ya que requiere reconstruir estructuras de control, tipos de datos y llamadas de funciones.

###  Instrucciones clave: `cmp` vs `test`

- `cmp A, B`  
    Calcula `A - B` y actualiza los flags (pero **no modifica los operandos**).
    
- `test A, B`  
    Realiza `A AND B` y actualiza los flags, también sin modificar los operandos.
    

> Son comúnmente usadas antes de instrucciones condicionales (`je`, `jne`, `jz`, etc.).

---

## ️ Herramientas destacadas

- **Ghidra**: descompilador de código abierto desarrollado por la NSA, muy potente y gratuito.
    
- **IDA Free / IDA Pro**: estándar de la industria para análisis estático.
    
- **radare2 / Cutter**: suite libre para reversing con interfaz CLI y gráfica.
    
- **x64dbg**: debugger útil para análisis dinámico de binarios Windows.
    

---