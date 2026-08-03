---
title: "Ingeneria Inversa"
date: 2025-02-11
tags:
  - ciberseguridad
---

##  IDA & Diaphora para comparar muestras de ensamblador


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

**IDA** (Interactive DisAssembler) es una de las herramientas más potentes en el ámbito de la ingeniería inversa. Permite desensamblar binarios de múltiples arquitecturas y explorar su estructura interna.

###  Diaphora: comparación de binarios

**Diaphora** es un complemento (plugin) para IDA Pro que permite **comparar funciones y estructuras entre dos binarios distintos**. Es especialmente útil para:

- Detectar cambios entre versiones de un mismo software,
    
- Identificar código compartido entre muestras de malware,
    
- Localizar secciones de código idénticas o similares.
    

El plugin genera hashes de funciones, analiza llamadas internas y estructuras, y ofrece un informe visual sobre las similitudes y diferencias.

---

###  Alternativas y extensiones

- **IDA Classroom Pro**  
    Versión académica/profesional de IDA pensada para enseñanza y laboratorios controlados. Integra funciones de desensamblado, análisis y scripting.
    
- **r2diaphora**  
    Plugin para **Radare2** que ofrece una funcionalidad similar a Diaphora dentro del entorno de Radare.  
    Permite comparar funciones entre binarios, útil si prefieres entornos libres y de línea de comandos.
    

---

##  Análisis de binarios en Rust (caso práctico con PEC 1)

Cuando se trabaja con proyectos en **Rust**, es importante tener en cuenta cómo se genera el binario final.

###  Enlazado estático por defecto

Rust tiende a **enlazar de forma estática** todas sus dependencias. Esto implica que:

- El binario generado contiene todo el código necesario para ejecutarse sin requerir bibliotecas externas en tiempo de ejecución.
    
- El tamaño del binario es mayor.
    
- Las firmas de funciones (hashes) cambian más fácilmente con cada compilación, dificultando la comparación binaria directa.
    

###  Implicación en reversing y comparación

- Las funciones externas quedan **embebidas** en el binario, lo que complica distinguir código propio del de las dependencias.
    
- Los binarios generados por Rust pueden ser **más difíciles de comparar** si no se controla el entorno de compilación (flags, optimizaciones, versiones de crates, etc.).
    

>  Recomendación: para comparar binarios Rust con Diaphora o r2diaphora, intenta compilar con las mismas versiones, desactiva optimizaciones, y utiliza `--remap-path-prefix` para reducir ruido entre versiones.


---

##  Llamadas a Funciones y Convenciones de Llamado

En bajo nivel, una **llamada a función** en ensamblador se realiza mediante instrucciones como `call` (en arquitecturas x86/x64). Esta instrucción **guarda la dirección de retorno en la pila** y transfiere el control al punto de entrada de la función.

###  Estructura del marco de pila (stack frame)

Cuando se ejecuta una función, se construye un **marco de pila** que contiene:

-  Dirección de retorno (`RET`): para volver al punto original tras ejecutar la función.
    
-  **Base pointer** (`BP` / `EBP` / `RBP`): apunta al inicio del marco de pila anterior. Se usa para facilitar el acceso a variables locales y argumentos.
    
-  Variables locales y argumentos pasados a la función.
    

Este marco permite mantener el orden y la integridad de las llamadas anidadas y facilita la depuración o análisis posterior.

---

##  Convenciones de llamada (Calling Conventions)

Las **convenciones de llamada** definen cómo se manejan los siguientes aspectos en una llamada a función:

- Cómo se pasan los argumentos (pila o registros),
    
- Qué registros deben preservarse (caller/callee-saved),
    
- Quién es responsable de limpiar la pila.
    

###  Convenciones más comunes

|Convención|Descripción|Limpieza de pila|Uso típico|
|---|---|---|---|
|`cdecl`|Argumentos por pila, el **caller limpia la pila**.|Llamador|Unix/Linux (x86)|
|`stdcall`|Argumentos por pila, la **función llamada limpia la pila**.|Callee|Windows API|
|`fastcall`|Argumentos pasados por **registros** (por ejemplo, ECX, EDX).|Varía|Windows, optimización|
|`sysv_amd64`|Registros como RDI, RSI, RDX para pasar los primeros 6 argumentos.|Caller|Linux x86_64|
|`ms_amd64`|Similar a SysV pero con registros RCX, RDX, R8, R9.|Caller|Windows x86_64|

>  _Callee_: función llamada.  
>  _Caller_: función que llama.

---

##  Relevancia en ingeniería inversa

Identificar la convención de llamada usada por un binario puede:

-  Ayudarte a deducir el **compilador** y el **sistema operativo** para el que fue construido.
    
-  Facilitar el **análisis de funciones** cuando no se dispone de símbolos.
    
-  Evitar errores de interpretación al reconstruir el comportamiento de funciones en desensamblado o descompilado.
    

Además, en algunos entornos (por ejemplo, en sistemas Linux con `gcc`), se puede **forzar una convención de llamada** mediante atributos específicos, como:

```c
__attribute__((cdecl))
__attribute__((stdcall))
```



---

##  Análisis de Binarios ELF

En sistemas **Linux y Unix-like**, los ejecutables utilizan el formato **ELF** (Executable and Linkable Format), que define cómo debe organizarse un binario para que pueda ser cargado y ejecutado por el sistema operativo.

###  Características clave del formato ELF

- Es el formato estándar para **ejecutables, bibliotecas compartidas (.so)** y **núcleos (kernel modules)**.
    
- Tiene una estructura bien definida que permite su análisis con herramientas como **IDA**, **radare2**, **Ghidra** o **objdump**.
    

>  Si puedes ejecutar un archivo directamente desde la terminal (`./programa`) y no es un script, **casi con seguridad es un binario ELF**.

---

##  Análisis en IDA: enfoque sobre `.text`

Al abrir un binario ELF en **IDA**, la herramienta examina principalmente la sección `.text`, que contiene el **código ejecutable**. Esta sección es donde reside la lógica del programa (funciones, rutinas, instrucciones de control, etc.).

###  Información útil para el análisis

La facilidad del análisis dependerá de si el binario incluye **símbolos de depuración**:

- Nombres reales de funciones (`main`, `do_login`, etc.),
    
- Nombres de variables globales o locales,
    
- Comentarios de compilación o referencias cruzadas.
    

En binarios que han sido tratados con `strip` o compilados en modo release, toda esta información puede estar ausente, lo que dificulta el trabajo de ingeniería inversa.

---

## ️ Enlazado en binarios Linux

En Linux, muchos binarios pueden estar:

- **Estáticamente enlazados**: todo el código necesario está dentro del binario, incluyendo bibliotecas estándar.
    
    -  Independencia del entorno.
        
    -  Binarios más grandes y difíciles de actualizar.
        
- **Dinámicamente enlazados**: el binario hace referencia a bibliotecas externas (`libc.so`, `libm.so`, etc.).
    
    -  Binarios más pequeños.
        
    -  Ahorro de memoria si múltiples procesos usan las mismas bibliotecas.
        
    -  Dependencias externas.
        

> ️ A diferencia de Windows, donde las dependencias suelen estar en **DLLs**, en Linux se usan **archivos `.so`** (Shared Object).

---

##  Corkami: visualizaciones de estructuras binarios

**Corkami** es un proyecto colaborativo que ofrece:

- Diagramas detallados de estructuras internas de binarios (PE, ELF, Mach-O).
    
- Visualizaciones educativas sobre ensamblador, representación de funciones, flujo de llamadas, formatos de archivo y más.
    

 GitHub del proyecto: [https://github.com/corkami](https://github.com/corkami)

###  ¿Por qué es útil Corkami?

- Ayuda a **visualizar el formato ELF y sus secciones**.
    
- Es excelente para aprender sobre el diseño de binarios y estructuras internas.
    
- Útil como referencia rápida en prácticas de reversing o análisis forense.
    


---

## ️ Parches en Ensamblador

Los **parches en ensamblador** (o _assembly patching_) permiten **modificar el comportamiento de un binario** alterando directamente sus instrucciones en lenguaje máquina.

Esta técnica es fundamental en:

-  **Análisis de seguridad** (por ejemplo, desactivar una comprobación de licencia),
    
-  **Ingeniería inversa** (modificar el flujo de un programa),
    
-  **Desarrollo de exploits o pruebas de concepto** (PoC),
    
- ️ **Hardening de binarios** (eliminar funciones peligrosas o vulnerables).
    

---

### ️ ¿Qué implica un parche?

Parchear consiste en:

1. **Localizar la instrucción o secuencia de instrucciones** que deseas modificar (por ejemplo, un `cmp` que activa una validación).
    
2. **Reemplazarla por otra** instrucción que altere el comportamiento deseado, como:
    
    - Cambiar un `jne` por `je` para invertir una condición,
        
    - Insertar un `nop` para anular instrucciones,
        
    - Saltar instrucciones críticas con un `jmp`.
        
3. **Guardar el binario modificado**, asegurándose de no romper la estructura general del ejecutable.
    

---

###  Herramientas comunes para parcheo

- **IDA Pro / IDA Free**  
    Permite editar instrucciones directamente desde la vista de ensamblador (`Edit → Patch program`).
    
- **Ghidra**  
    Incluye un _patching tool_ que permite modificar instrucciones desde el editor.
    
- **Radare2 / Cutter**  
    Permiten parches rápidos desde consola (`wa jmp`, `wx 90`, etc.) o desde su interfaz gráfica.
    
- **Hiew**, **Binary Ninja**, **x64dbg**  
    También ofrecen soporte para parcheo y visualización hexadecimal.
    

---

###  Ejemplo práctico

Supongamos que una función verifica si un usuario tiene licencia mediante:

```asm
cmp eax, 1
jne fail
```

Podemos **parchear el salto condicional `jne` por `jmp`**, lo que forzará siempre la ejecución como si la comprobación fuera positiva:

```asm
cmp eax, 1
jmp success
```

O simplemente **anular la instrucción** con `NOPs` (`0x90` en x86):

```asm
nop
nop
```

> ️ Siempre revisa el **tamaño del parche**. Si la nueva instrucción ocupa menos bytes que la original, deberás rellenar con NOPs. Si ocupa más, necesitarás espacio adicional o redireccionamiento.

---

###  Riesgos del parcheo

- Puede **romper el binario** si se alteran offsets críticos o estructuras internas.
    
- Puede invalidar **firmas digitales** o protecciones anti-tamper.
    
- En análisis forense, los parches deben ser **documentados** con precisión para replicabilidad y auditoría.
    

---