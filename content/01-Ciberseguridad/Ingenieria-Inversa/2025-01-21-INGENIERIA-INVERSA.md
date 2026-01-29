---
title: "Ingenieria Inversa"
date: 2025-01-21
tags:
  - ciberseguridad
---

## ️ Llamadas a funciones y marcos de pila


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Cuando un programa ejecuta una instrucción `call`, se produce una **llamada a función** que provoca la creación de un **nuevo marco de pila (stack frame)**. Este marco contiene:

- La dirección de retorno (para saber dónde continuar),
    
- Los argumentos pasados a la función,
    
- Variables locales.
    

> ️ Si se crean demasiados marcos (por ejemplo, en una recursión infinita), se puede agotar la pila y el sistema operativo detona un **`segmentation fault`**, como mecanismo de defensa.

---

##  Enlazado en C: estático vs dinámico

El **lenguaje de programación** influye significativamente en el comportamiento del binario resultante.

En C, existen dos formas principales de enlazar bibliotecas:

- **Enlazado estático**:  
    El código de las bibliotecas se **incluye dentro del binario**.  
     Binario independiente.  
     Aumenta su tamaño.
    
- **Enlazado dinámico**:  
    El binario contiene **referencias** a bibliotecas externas (DLL o `.so`) que se resuelven en tiempo de ejecución.  
     Binario más pequeño.  
     Depende del entorno para ejecutarse.
    

---

##  Compilación en diferentes lenguajes

- **Swift**: se compila directamente a lenguaje máquina (nativo). Las apps se **firman digitalmente**, lo que protege su integridad y permite distribuirlas de forma segura en entornos como iOS/macOS.
    
- **Android (Java/Kotlin)**:  
    El código se compila a **bytecode**, que se ejecuta sobre la máquina virtual Dalvik/ART.  
     Ventaja: portabilidad (funciona en cualquier dispositivo con la JVM/ART).  
     Desventaja: más fácil de descompilar que código nativo.
    

---

##  DLL y bibliotecas en C++

Las **DLL (Dynamic Link Libraries)** en Windows, especialmente dentro del ecosistema .NET, son funcionalmente similares a las bibliotecas dinámicas en C/C++ (`.so` en Linux, `.dylib` en macOS).

> En entornos .NET, las DLL pueden contener ensamblados, recursos, metadatos y código CIL que se interpreta por el CLR (Common Language Runtime).

---

##  Herramientas de análisis: IDA

**IDA (Interactive DisAssembler)** es una de las herramientas más potentes para ingeniería inversa de binarios. Sus funciones incluyen:

- Desensamblado estático,
    
- Reconstrucción de funciones y flujo de control,
    
- Soporte para múltiples arquitecturas.
    

Existen dos versiones: **IDA Free** (gratuita) y **IDA Pro** (comercial).

---

## ️ Argumentos de entrada en C

En programas escritos en C, el primer argumento que recibe la función `main` (si se usa `int main(int argc, char *argv[])`) es:

```c
argv[0]
```

Este contiene el **path del programa ejecutado**, y no un argumento real pasado por el usuario. Los argumentos reales comienzan desde `argv[1]`.

---

## ️ `strip`: limpieza de símbolos

La utilidad `strip` se usa para **eliminar la tabla de símbolos** de un binario. Esto tiene varias consecuencias:

- Oculta los nombres de funciones y variables,
    
- Reduce el tamaño del archivo,
    
- Dificulta el análisis (muy usado en malware y binarios de producción).
    

Cuando no se dispone de la tabla de símbolos, una estrategia típica es **buscar funciones que devuelvan un entero y reciban como argumentos un entero y un puntero a `char`**, ya que suelen corresponder a funciones estándar como `strcmp`, `write`, etc.

---

##  Referencias

Consulta la **bibliografía del Tema 2** del curso para profundizar en:

- Formatos PE/ELF,
    
- Linkers y loaders,
    
- Herramientas de análisis estático y dinámico,
    
- Casos prácticos de reversing.
    

---

¿Quieres que te prepare una plantilla con funciones comunes y su patrón en ensamblador o ejemplos en Ghidra o radare2? Puedo ayudarte a practicar casos reales.

---

**Reversing Tools**

### Disassemblers

Convierte los ceros y unos a mnemónicos de ensamblador.

Uno de los más conocidos es IDA, sobre todo la versión de pago, que es la más popular. Tiene plugins porque un paquete contiene varios módulos que permiten ver diferentes parches, por ejemplo, en iOS.

Ghidra está hecho en Java y tiene un rendimiento inferior.

### Decompilers

Intenta convertir el binario en C, ya que C es un lenguaje estándar para este tipo de tareas.

### Radare2

Es parecido a IDA y está hecho en España.

### GDB con PEDA

Se utiliza para analizar exploits.

No usar OllyDbg, aunque hay muchos tutoriales, ya que su momento ha pasado. Para ello, es mejor usar Immunity Debugger. El que vemos aquí es `x64dbg`.

---
