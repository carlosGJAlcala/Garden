---
title: "Immunity Debugger Y Ghidra"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---




### **Immunity Debugger y Ghidra: Análisis y Modificación de Binarios**

Immunity Debugger y Ghidra son herramientas poderosas para escribir exploits, analizar malware y aplicar ingeniería inversa a archivos binarios. En este caso, las utilizaremos para analizar cómo se valida una clave en un programa y modificar su comportamiento.

> **Relacionado**: Ver [[01-Ciberseguridad/Malware/2025-02-24-Formatos-ejecutables-PE-y-ELF|Formatos PE y ELF]] para entender la estructura de binarios. [[01-Ciberseguridad/Ingenieria-Inversa/2025-03-11-Radare2|Radare2]] como alternativa. [[01-Ciberseguridad/Ingenieria-Inversa/2025-03-25-exploit|Desarrollo de exploits]] para técnicas avanzadas.

### **Análisis de un Sistema de Validación de Claves**

Supongamos que tenemos un programa en Windows 10 que, al ejecutarse, solicita una clave de activación. Si ingresamos una clave incorrecta, el programa nos devuelve un mensaje de error como _"Invalid key"_. Nuestro objetivo será encontrar en el binario la sección donde se compara la clave ingresada con la clave correcta y modificar el flujo del programa a nuestro favor.

#### **Ejecutando el Programa en Immunity Debugger**

1. Abrimos el programa en **Immunity Debugger** y lo ejecutamos.
2. Cuando el programa solicite la clave, ingresamos una incorrecta y observamos en qué parte del código se detiene la ejecución.
3. Si presionamos **F9**, podemos continuar con la ejecución y observar el comportamiento del programa.
4. Es probable que, si introducimos una clave incorrecta, el flujo de ejecución pase por una sección donde se genera el mensaje de _"Invalid key"_.

#### **Identificando y Modificando la Comparación de la Clave**

El primer paso es identificar dónde el programa inserta la clave que ingresamos en memoria y dónde la compara con la clave válida almacenada en el binario. Esto se puede hacer buscando instrucciones de comparación como `CMP`, `TEST` o `JE/JNE`.

Una técnica común para evitar la validación de claves es modificar la ejecución del código en ensamblador. Para ello, podemos utilizar **NOPs (No Operation)** en la instrucción de comparación o alterar las instrucciones de salto condicional.

Por ejemplo, si el programa contiene un código como este en ensamblador:

```assembly
CMP EAX, [VALID_KEY]  ; Compara la clave ingresada con la clave válida
JNE INVALID_KEY_MSG   ; Si no son iguales, muestra "Invalid key"
```

Podemos modificar la instrucción de salto `JNE` (Jump if Not Equal) para que en su lugar siempre se dirija a la parte del código donde se concede acceso, sin importar la clave ingresada.

#### **Modificación del Binario y Creación de un Nuevo Ejecutable**

Una forma de aplicar el cambio de manera permanente es guardar los ajustes en el binario y generar un nuevo ejecutable con las modificaciones aplicadas. Esto se puede hacer con herramientas como Ghidra o un editor hexadecimal.

Alternativamente, en lugar de modificar el binario original, algunos atacantes escriben un programa en **C** que llama al binario original y altera su comportamiento en tiempo de ejecución, inyectando código o manipulando memoria.

### **Conclusión**

Con herramientas como Immunity Debugger y Ghidra, podemos desensamblar un ejecutable, analizar su lógica interna y modificar su comportamiento para alterar su funcionalidad. En este caso, logramos omitir la validación de una clave manipulando la lógica de comparación del programa.