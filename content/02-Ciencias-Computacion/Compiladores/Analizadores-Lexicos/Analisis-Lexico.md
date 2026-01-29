---
title: "Analisis Lexico"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - analizadores-lexicos
---

El **análisis léxico**, también conocido como _lexical analysis_ o _scanning_, constituye la primera fase del proceso de compilación de un programa. Su propósito principal es transformar la secuencia bruta de caracteres del código fuente en una secuencia estructurada de **tokens** (componentes léxicos), cada uno de los cuales posee un significado sintáctico específico y, opcionalmente, un conjunto de **atributos** que enriquecen su descripción.

Esta etapa actúa como un filtro entre el **editor de texto** donde se escribe el código y el **analizador sintáctico** (_parser_), asegurando que la información que llega a este último sea más compacta, libre de elementos irrelevantes (como espacios o comentarios) y coherente con las reglas léxicas del lenguaje.

---

### **Conceptos fundamentales**


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Reconocimiento/Scanning|Scanning]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

1. **Token (componente léxico)**:  
    Es una unidad atómica de información sintáctica. Por ejemplo, en el lenguaje C, `if`, `x`, `+` o `3.14` son tokens distintos.  
    Cada token se define mediante un **patrón** formal (a menudo una expresión regular) que describe todas las posibles secuencias de caracteres (_lexemas_) que lo representan.
    
2. **Lexema**:  
    Secuencia concreta de caracteres que encaja con el patrón definido para un token.  
    Ejemplo:
    
    - Token: `IDENTIFICADOR`
        
    - Patrón: `<letra>(<letra>|<dígito>)*`
        
    - Lexema válido: `contador`, `x2`.
        
3. **Patrón**:  
    Regla o expresión regular que describe todos los lexemas válidos para un token.  
    Ejemplo: el patrón para un **número entero par** podría expresarse como:
    
    ```
    [0-9]*(0|2|4|6|8)
    ```
    

---

### **Funciones principales del analizador léxico**

- **Reconocimiento de componentes léxicos**: identifica en la secuencia de caracteres los distintos tokens que componen el programa.
    
- **Eliminación de elementos irrelevantes**: descarta espacios en blanco, tabulaciones, saltos de línea, saltos de página y comentarios.
    
- **Gestión de la tabla de símbolos**: registra identificadores, constantes y, en general, cualquier nombre definido por el usuario, asociándolos con atributos como su posición en memoria o su tipo.
    
- **Detección y reporte de errores léxicos**: identifica caracteres no válidos o combinaciones ilegales, indicando con precisión la ubicación y naturaleza del error.
    
- **Optimización para el parser**: entrega al analizador sintáctico una secuencia optimizada de tokens para facilitar y acelerar el análisis gramatical.
    

---

### **Relación con el análisis sintáctico**

En la mayoría de compiladores, el analizador léxico se implementa como una **subrutina** del analizador sintáctico, lo que permite:

- Simplificar el diseño del parser, delegando la gestión de caracteres y patrones al scanner.
    
- Mejorar la eficiencia del compilador al trabajar sobre tokens ya procesados.
    
- Favorecer la portabilidad, haciendo que el sistema sea independiente del alfabeto y las peculiaridades del lenguaje.
    

La comunicación entre ambos módulos suele realizarse a través de un **búfer intermedio**, donde el analizador léxico deposita los tokens para que el sintáctico los consuma.

---

### **Tratamiento de errores léxicos**

Un error léxico ocurre cuando una secuencia de caracteres no encaja en ningún patrón válido del lenguaje. Ejemplos típicos:

- Uso de caracteres no admitidos (`ñ`, `ç`, acentos, etc., en un lenguaje que no los contemple).
    
- Operadores ilegales (`::`, `;=`) que no figuren en la gramática léxica.
    

Estrategias de recuperación:

- **Modo pánico**: se descartan caracteres hasta encontrar uno que pueda iniciar un lexema válido.
    
- **Corrección mínima**: inserción, borrado o sustitución de caracteres para reconstruir un token válido.
    
- **Transposición**: intercambio de dos caracteres adyacentes para corregir errores comunes de escritura.
    

Ejemplo de buen mensaje de error:

```
int número 1;
       ^
ERROR 124: línea 85, columna 6, carácter no válido
```

Esto es preferible a un simple “Error en la línea 85”.

---

### **Implementación**

Un analizador léxico puede construirse de distintas formas:

- **Manualmente** en un lenguaje de alto nivel (más esfuerzo, mayor control y eficiencia).
    
- **Mediante generadores automáticos** como _Lex_ o _JFlex_, que traducen las expresiones regulares y acciones definidas por el programador en un autómata finito implementado en C, C++ o Java.
    
- **En ensamblador**, en casos muy específicos donde el rendimiento extremo sea crucial.
    

En todos los casos, la base técnica descansa sobre **expresiones regulares** y su traducción a **autómatas finitos deterministas o no deterministas**, que modelan el reconocimiento de patrones sobre la entrada.

---

Si quieres, puedo ahora ampliar este mismo apartado incluyendo **ejemplos visuales con autómatas** y **diagramas de transición** que aparecen en el documento para que quede como una sección más didáctica y visual. ¿Quieres que lo haga?