---
title: "2025 02 05 Diferentes Tipos De Tipados"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---
En programación, el **tipado** se refiere a cómo los lenguajes manejan y aplican los tipos de datos. Existen dos clasificaciones principales: **tipado estático vs. tipado dinámico** y **tipado fuerte vs. tipado débil**.

**Tipado estático vs. tipado dinámico:**

- **Tipado estático:** En este enfoque, el tipo de una variable se define en tiempo de compilación y no puede cambiar durante la ejecución. Esto permite que muchos errores se detecten antes de ejecutar el programa. Lenguajes como Java y C# utilizan tipado estático.
    
- **Tipado dinámico:** Aquí, el tipo de una variable se determina en tiempo de ejecución, lo que permite mayor flexibilidad, ya que una variable puede contener diferentes tipos de datos en distintos momentos. Lenguajes como Python y JavaScript emplean tipado dinámico.
    

**Tipado fuerte vs. tipado débil:**

- **Tipado fuerte:** Los lenguajes con tipado fuerte imponen reglas estrictas sobre cómo se pueden combinar y convertir los tipos de datos. No permiten operaciones entre tipos incompatibles sin una conversión explícita. Por ejemplo, en Python, intentar sumar un número y una cadena de texto sin una conversión explícita generará un error.
    
- **Tipado débil:** Estos lenguajes permiten conversiones implícitas entre tipos, a veces sin intervención del programador, lo que puede llevar a resultados inesperados si no se maneja con cuidado. JavaScript es un ejemplo de lenguaje con tipado débil, donde es posible sumar un número y una cadena, resultando en una concatenación en lugar de una operación aritmética.
    

**Clasificación de algunos lenguajes comunes:**

|Lenguaje|Tipado Estático/Dinámico|Tipado Fuerte/Débil|
|---|---|---|
|Java|Estático|Fuerte|
|C#|Estático|Fuerte|
|C|Estático|Débil|
|C++|Estático|Débil|
|Python|Dinámico|Fuerte|
|JavaScript|Dinámico|Débil|
|PHP|Dinámico|Débil|
|Go|Estático|Fuerte|
|Ruby|Dinámico|Fuerte|

Es importante destacar que estas clasificaciones pueden variar según las interpretaciones y características específicas de cada lenguaje. Algunos lenguajes ofrecen características que permiten comportamientos tanto de tipado fuerte como débil, o combinan tipado estático y dinámico en diferentes contextos


### Ejemplo en C:


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

```c
#include <stdio.h>

int main() {
    char c = 'A'; // 'A' tiene el valor ASCII 65
    int num = 5;
    int resultado = c + num; // Se convierte 'A' (65) en un entero y se suma

    printf("Resultado: %d\n", resultado); // Imprime 70
    return 0;
}
```

Aquí, el `char` `'A'` se convierte automáticamente en su valor ASCII (`65`), y se suma con `5`, resultando en `70`. Esto sucede sin necesidad de conversión explícita.

### ¿Por qué se considera débil?

- **Conversiones implícitas:** C permite la conversión automática entre diferentes tipos de datos, como `char`, `int`, `float`, `double`, etc.
- **Poca verificación de tipos:** Puedes hacer operaciones entre tipos incompatibles sin errores en tiempo de compilación.
- **Punteros y casting explícito:** Es posible reinterpretar bloques de memoria con `void *`, lo que da aún más flexibilidad al programador, pero puede causar errores difíciles de depurar.

Por estas razones, C es considerado **tipado débil**, aunque su tipado sigue siendo **estático**, ya que los tipos de variables se establecen en tiempo de compilación.