---
title: "Desreferenciar Un Puntero Nulo"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
**Desreferenciar un puntero nulo** puede ser un vector de ataque en algunos contextos, especialmente cuando el **comportamiento indefinido** o **errores de segmentación** derivados de esta operación no son correctamente manejados. Un **atacante** puede aprovechar errores relacionados con la desreferenciación de punteros nulos para **explotar vulnerabilidades** en un programa y tomar control de un sistema.

A continuación, te explico cómo un atacante podría **emplear una desreferenciación de puntero nulo** para llevar a cabo un **ataque**.

###  **¿Cómo un atacante podría aprovechar la desreferenciación de un puntero nulo?**


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

1. **Desbordamiento de búfer o corrupción de memoria:**
    
    - Si un puntero nulo es **incorrectamente desreferenciado**, podría causar un **desbordamiento de búfer** o **corrupción de memoria**. Este tipo de vulnerabilidad permite que un atacante **sobreescriba áreas de memoria** del programa, lo que potencialmente podría alterar el flujo de ejecución del programa, permitiendo que el atacante **ejecute código arbitrario**.
        
2. **Manipulación del flujo de ejecución del programa:**
    
    - En algunos casos, los errores derivados de desreferenciar punteros nulos pueden corromper las estructuras de control del programa, como las **pilas de llamadas** o las **tablas de punteros de función**. Un atacante podría aprovechar estos errores para **modificar el flujo de ejecución** de un programa, llevándolo a ejecutar código malicioso en lugar de seguir el flujo legítimo.
        
3. **Denegación de servicio (DoS):**
    
    - Un atacante podría utilizar la desreferenciación de un puntero nulo para **provocar un fallo de segmentación (segfault)**. Esto **bloquea** el programa y lo hace **inestable**, lo que puede resultar en un **denegación de servicio**. Un **denegación de servicio (DoS)** simplemente hace que un servicio se caiga y no sea accesible para los usuarios legítimos.
        
4. **Control total sobre el sistema:**
    
    - En un escenario más grave, **si el puntero nulo se encuentra en una estructura de datos crítica** (por ejemplo, en las funciones que gestionan la memoria dinámica o las tablas de direcciones de funciones), un atacante podría desreferenciar el puntero de manera que **redirija la ejecución del programa** a código malicioso que el atacante ha inyectado.
        
5. **Explotación de errores de programación**:
    
    - En sistemas o aplicaciones donde los errores no se manejan adecuadamente, desreferenciar un puntero nulo puede dejar al programa en un **estado inseguro**. Si este tipo de errores no se gestionan correctamente (por ejemplo, **sin validaciones adecuadas**), el atacante podría aprovechar esta vulnerabilidad para lanzar un ataque más sofisticado.
        

###  **Ejemplo práctico de ataque (Desbordamiento de búfer mediante desreferenciación de puntero nulo)**

1. **El atacante controla el puntero nulo**:
    
    - Supongamos que hay un puntero que debe contener una dirección válida, pero no está inicializado correctamente o se establece a `NULL` (nulo). El atacante puede manipular la dirección del puntero a través de un **desbordamiento de búfer**, forzando el puntero a apuntar a una **zona de memoria controlada por el atacante**.
        
2. **Desreferencia el puntero nulo**:
    
    - Cuando el código intenta **desreferenciar el puntero**, se intenta acceder a una **dirección de memoria no válida**, lo que puede causar que el sistema o aplicación se bloquee (falla de segmentación).
        
3. **Acceso no autorizado a la memoria**:
    
    - Si el atacante logra controlar el puntero y hace que apunte a una **zona de memoria ejecutable** (como el stack o el heap), puede escribir **código malicioso** en esa zona. En el siguiente paso, puede lograr que el programa ejecute su propio código, **obteniendo control total sobre el sistema**.
        

---

###  **Cómo explotan los atacantes las vulnerabilidades de puntero nulo:**

1. **Inyección de código malicioso**:
    
    - Si la desreferenciación de punteros nulos permite la corrupción de la memoria, el atacante puede sobrescribir áreas sensibles de la memoria (por ejemplo, **registros de retorno**, **punteros de función** o **direcciones de salto**).
        
    - Esto podría permitir que el atacante **inyecte su propio código** en la memoria y haga que se ejecute en lugar del código legítimo de la aplicación.
        
2. **Redirigir el flujo de ejecución**:
    
    - Un atacante puede manipular el flujo de ejecución al hacer que un puntero nulo apunte a una dirección de memoria controlada por el atacante. Esto podría provocar que el programa **salte a una sección de código malicioso**.
        
3. **Explotación de errores de desbordamiento**:
    
    - En sistemas vulnerables que permiten **desbordamientos de búfer**, un atacante podría enviar datos diseñados específicamente para sobrescribir un puntero, haciéndolo apuntar a una **dirección de memoria** que contiene código malicioso. Luego, cuando el programa intente desreferenciar el puntero, ejecutará el **código malicioso** del atacante.
        
4. **Desbordamiento de pila**:
    
    - Si el puntero nulo se encuentra en una estructura de datos crucial, como una **pila de llamadas**, un atacante podría aprovechar la desreferenciación para **sobreescribir el puntero de retorno** en la pila. Esto podría permitir que el atacante **tome el control** del flujo de ejecución y ejecute código arbitrario.
        

---

###  **Medidas de prevención**:

1. **Comprobación de punteros nulos**:
    
    - Siempre verifica que un puntero no sea nulo antes de desreferenciarlo. Esto es una de las formas más efectivas de prevenir que el sistema intente acceder a memoria no válida.
        
    
    ```c
    if (ptr != NULL) {
        // Desreferenciar el puntero de forma segura
        printf("%d\n", *ptr);
    } else {
        printf("El puntero es nulo\n");
    }
    ```
    
2. **Inicialización de punteros**:
    
    - Siempre **inicializa los punteros** adecuadamente. Si no se necesita que apunten a una dirección válida, asigna un valor `NULL` explícito o asegúrate de que no apunten a memoria sin usar.
        
3. **Uso de punteros inteligentes** (en C++):
    
    - Utiliza **punteros inteligentes** (como `std::unique_ptr` o `std::shared_ptr` en C++) para gestionar automáticamente la memoria y reducir los riesgos de manipulación de punteros nulos.
        
4. **Herramientas de análisis estático**:
    
    - Usa herramientas de **análisis estático de código** para detectar posibles desreferencias de punteros nulos antes de que lleguen a producción. Herramientas como **Clang**, **Coverity** o **SonarQube** pueden ayudarte a encontrar estos errores en el código.
        
5. **Protección mediante seguridad de memoria**:
    
    - Implementa **protecciones de seguridad de memoria** como **Address Space Layout Randomization (ASLR)** y **Stack Canaries** para hacer más difícil la explotación de vulnerabilidades relacionadas con la memoria.
        

---

###  **Resumen**:

La desreferenciación de un puntero nulo puede ser una vulnerabilidad de **seguridad crítica** que un atacante puede explotar para **tomar control del sistema** mediante **inyección de código**, **desbordamiento de búfer** o **corrupción de memoria**. Es fundamental prevenir este tipo de errores mediante la **comprobación adecuada de punteros**, la **inicialización de variables** y el uso de **herramientas de análisis** para identificar posibles riesgos de seguridad.