---
title: "Ingenieria Inversa"
date: 2025-01-28
tags:
  - ciberseguridad
---

Los malwares suelen estar comprimidos en archivos ZIP protegidos con contraseña para dificultar su análisis. Por ello, al analizar estos archivos, se hace una clasificación binaria: **"clean" (limpio)** o **"infected" (infectado)**, dependiendo de si contienen código malicioso o no.

**Para la clase de hoy utilizaremos IDA Pro** para analizar un binario. Este software es ampliamente usado para desensamblar y depurar código. Un aspecto interesante de algunos binarios maliciosos es que han sido manipulados con herramientas específicas para ocultar su funcionalidad real.

### Conceptos clave:


> **Relacionado**: [[03-Desarrollo-Software/Distribuido/SAP_PI/STUB|STUB]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

1. **Strip (tabla de símbolos eliminada):**  
    Muchos binarios maliciosos están "striped", lo que significa que han eliminado la tabla de símbolos, dificultando la identificación de funciones y variables. Esto se hace para entorpecer el análisis.
    
2. **Crypters y stubs:**  
    Un **crypter** es una herramienta utilizada para cifrar o modificar un archivo binario con el objetivo de evadir la detección por software antivirus. Su estructura básica incluye dos partes principales: el **stub** y el payload cifrado.
    
    - El **stub** es el código que se ejecuta primero y se encarga de descifrar el payload cifrado. Escrito generalmente en ensamblador, este fragmento de código es esencial para recuperar el malware en su forma operativa.
    - El propósito del crypter es asegurarse de que el binario descifrado solo sea visible en memoria durante la ejecución, lo que lo hace difícil de analizar con herramientas estáticas.
3. **UPX (Ultimate Packer for Executables):**  
    Es un empaquetador que comprime ejecutables para reducir su tamaño. Algunos malwares utilizan UPX modificado como una capa adicional de protección, aunque es posible descomprimirlo usando herramientas específicas.
    
4. **Ejecución forzada:**  
    Para analizar un binario protegido, muchas veces es necesario ejecutarlo en un entorno controlado para que se descifre y se pueda analizar su comportamiento en tiempo real. Esto requiere un sandbox o un entorno virtual seguro.
    
5. **Cambios dinámicos de clave:**  
    Algunos crypters generan claves dinámicamente, cambiándolas en cada ejecución. Esto asegura que los patrones del malware no puedan ser identificados fácilmente con herramientas de análisis estático.
    
6. **Comando `strings`:**  
    Este comando extrae cadenas de texto de un archivo binario. Sin embargo, los crypters suelen ofuscar las cadenas para que no sean legibles con este comando, dificultando aún más la tarea de análisis.
    

---

### Herramientas adicionales:

- **GDB y su extensión "Peda":**  
    La extensión **Peda** para GDB facilita el análisis dinámico al incluir funciones para examinar memoria, identificar saltos condicionales y detectar cadenas relevantes.
    
- **IDA y referencias cruzadas (Xrefs):**  
    En IDA, al analizar un binario, puedes identificar dónde se utilizan cadenas específicas gracias a las referencias cruzadas (**Xrefs**). Esto se logra haciendo doble clic en una cadena dentro de la vista de desensamblado, lo que te llevará a las partes del código que hacen uso de ella. Los comentarios en la columna derecha de IDA proporcionan pistas adicionales para comprender el flujo del programa.
    

---

### Otros conceptos útiles:

1. **Conversión de tipos (`atoi`):**  
    La función `atoi` convierte cadenas de texto en enteros. Este tipo de funciones son comunes en binarios maliciosos que necesitan interpretar datos de configuración codificados como texto.
    
2. **Ofuscación de contraseñas con ROT13:**  
    Históricamente, las contraseñas se ofuscaban con métodos simples como ROT13, un cifrado de sustitución que rota cada letra del alfabeto 13 posiciones. Aunque obsoleto, sigue siendo un ejemplo clásico de ofuscación básica.
    
3. **Cadena terminadora (`\0` o NULL):**  
    Las cadenas en C terminan con un carácter NULL (`\0`), lo que marca su final. Este detalle es crucial en la manipulación de cadenas dentro del análisis estático de binarios.
    

---
La función **`IsDebuggerPresent`** es una API de Windows que permite a un programa determinar si está siendo depurado. Esta función es muy utilizada por malwares para dificultar el análisis dinámico al identificar si están siendo ejecutados en un entorno controlado o bajo un depurador. Si el malware detecta un depurador, puede alterar su comportamiento o simplemente no ejecutarse, complicando así la labor del analista.

### Cómo funciona `IsDebuggerPresent`

`IsDebuggerPresent` consulta un valor del **PEB (Process Environment Block)**, específicamente el campo **BeingDebugged**. Este campo indica si el proceso actual está siendo depurado. Si el valor es `1`, significa que hay un depurador presente; si es `0`, no lo hay.

#### Implementación básica:

El código para utilizar esta función sería algo como:

```c
#include <windows.h>
#include <stdio.h>

int main() {
    if (IsDebuggerPresent()) {
        printf("Debugger detectado. Terminando ejecución.\n");
        return 1;
    }
    printf("No hay debugger. Continuando ejecución.\n");
    return 0;
}
```

#### Comportamiento en el malware:

Cuando un malware detecta un depurador:

1. Puede terminar abruptamente para evitar el análisis.
2. Alterar su código o comportamiento, mostrando un funcionamiento inofensivo.
3. Generar datos falsos o inútiles que confundan al analista.

---

### Métodos avanzados para evadir análisis dinámico:

Además de `IsDebuggerPresent`, los malwares suelen emplear otros mecanismos:

1. **`CheckRemoteDebuggerPresent`:** Permite verificar si otro proceso está depurando el programa actual.
2. **`NtQueryInformationProcess`:** Se puede usar para consultar directamente información más detallada del proceso, incluido si está siendo depurado.
3. **Anti-debugging por tiempo:** El malware mide el tiempo entre instrucciones clave (usando `QueryPerformanceCounter` o funciones similares). Si el tiempo es anormalmente alto, supone que se está ejecutando bajo un depurador que ralentiza el flujo.
4. **Modificación del PEB:** Algunos malwares directamente escriben en el campo **BeingDebugged** del PEB para evitar que los depuradores detecten el estado real.

---

### Cómo contrarrestar `IsDebuggerPresent`

1. **Modificar el valor del PEB manualmente:** Puedes usar un depurador como **x64dbg** o **OllyDbg** para cambiar el valor de **BeingDebugged** a `0` durante el análisis.
2. **Usar entornos de análisis avanzados:** Sandboxes y herramientas como **Cuckoo** ya suelen contrarrestar estos métodos.
3. **Interceptar las llamadas a `IsDebuggerPresent`:** Con herramientas como **Frida** puedes sobrescribir la funcionalidad de esta API y devolver un valor falso (`0`) al malware.

---

### Ejemplo de manipulación del PEB:

```c
#include <windows.h>
#include <stdio.h>

void DisableDebuggerCheck() {
    // Obtener el puntero al PEB
    __asm {
        mov eax, fs:[0x30]  ; Obtener el puntero al PEB
        mov byte ptr [eax+2], 0 ; Establecer BeingDebugged a 0
    }
}

int main() {
    printf("Desactivando chequeo de depurador...\n");
    DisableDebuggerCheck();

    if (IsDebuggerPresent()) {
        printf("Debugger detectado (falla al parchear PEB).\n");
    } else {
        printf("Debugger NO detectado (PEB modificado).\n");
    }
    return 0;
}
```

Este tipo de técnicas de evasión son solo una pequeña parte del arsenal que utilizan los malwares para resistir el análisis. Si necesitas ejemplos más avanzados o formas de contrarrestarlos, puedo incluirlos.