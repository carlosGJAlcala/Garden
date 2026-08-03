---
title: "Analizador Sintactico"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - analisis-sintactico
---

## **Analizador Sintáctico**


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

El **analizador sintáctico** (_parser_) es el componente del compilador encargado de procesar la secuencia de **tokens** producida por el analizador léxico y verificar que su disposición respeta las reglas sintácticas del lenguaje, normalmente definidas mediante una **Gramática Libre de Contexto (CFG)**.  
Su función no es solo validar la estructura del código, sino también **construir una representación estructurada** —habitualmente un **árbol sintáctico**— que servirá de base para las fases posteriores del compilador, como el análisis semántico o la generación de código.

---

### **Objetivos principales**

- **Verificar la sintaxis**: comprobar que la cadena de tokens puede ser generada por la gramática del lenguaje.
- **Construir la estructura jerárquica** del código fuente mediante árboles sintácticos.
- **Detectar y manejar errores sintácticos**, recuperando la ejecución si es posible para seguir procesando el resto del código.
- **Preparar la información estructural** para etapas posteriores del compilador.

---

### **Tipos de análisis sintáctico**

El análisis sintáctico se puede abordar desde dos estrategias principales:

1. **Descendente (Top-down)**  
   - Construye el árbol desde la **raíz (axioma)** hacia las **hojas**.  
   - Parte del símbolo inicial y aplica derivaciones para llegar a la cadena de entrada.  
   - Ejemplos:  
     - Análisis descendente recursivo (con retroceso).  
     - Análisis predictivo \( LL(k) \) (sin retroceso o con retroceso controlado).

2. **Ascendente (Bottom-up)**  
   - Construye el árbol **desde las hojas** hacia la raíz.  
   - Parte de la entrada y aplica **reducciones** hasta alcanzar el símbolo inicial.  
   - Ejemplos:  
     - _Shift-Reduce parsing_.  
     - Analizadores LR, SLR, LALR.  
   - Generalmente más potentes y utilizados por generadores como YACC o Bison.

En ambos casos, la entrada se procesa de izquierda a derecha, analizando un token por vez.

---

### **Gramática Libre de Contexto (CFG)**

Una CFG \( G = (V_t, V_n, S, P) \) está compuesta por:

- \( V_t \): símbolos terminales (tokens).  
- \( V_n \): símbolos no terminales.  
- \( S \): símbolo inicial.  
- \( P \): conjunto de producciones \( A \rightarrow \alpha \), donde \( A \in V_n \) y \( \alpha \) es una secuencia de terminales y no terminales.

**Ejemplo de producciones**:



E → E + E  
E → E - E  
E → n



También se puede usar notación **BNF** o **EBNF** para representar reglas de forma más compacta.

---

### **Árbol sintáctico**

El árbol sintáctico (o de derivación) es una estructura jerárquica:

- **Nodos internos**: no terminales.  
- **Hojas**: terminales.  
- Los hijos representan los pasos de derivación aplicados.

**Ejemplo** (expresión `3 + 4` con la gramática anterior):




 E


/ |  
E + E  
| |  
3 4



---

### **Recursividad y ambigüedad**

- **Recursividad**: permite describir estructuras repetitivas.  
  - Por la **izquierda**: útil para análisis ascendente, pero problemática para el descendente.  
  - Por la **derecha**: más adecuada para análisis descendente.  

- **Ambigüedad**: una gramática es ambigua si una misma cadena puede derivar en más de un árbol sintáctico.  
  - Indeseable para compiladores porque genera interpretaciones múltiples y dificulta la generación de código.  
  - Se resuelve eliminando reglas ambiguas o reescribiendo la gramática.



### **Análisis descendente recursivo**

- Implementa derivaciones por la izquierda probando opciones y retrocediendo si falla (_backtracking_).  
- Problemas:  
  - No maneja bien recursividad por la izquierda.  
  - Alto coste por retrocesos.  
  - Difícil generar mensajes de error detallados.  

- Para eliminar la recursividad inmediata:



A → Aα₁ | Aα₂ | β₁ | β₂


se convierte en:


A → β₁A' | β₂A'  
A' → α₁A' | α₂A' | ε



---

### **Análisis descendente predictivo y LL(1)**

- Evita retrocesos prediciendo la producción a aplicar con base en el siguiente token de entrada.  
- **LL(1)**:  
  - Lee la entrada de izquierda a derecha.  
  - Aplica derivaciones por la izquierda.  
  - Usa 1 token de _lookahead_ para decidir la producción.

- Construcción:  
  1. Calcular conjuntos **Primero** y **Siguiente** para cada no terminal.  
  2. Crear tabla de análisis \( M[V_n, V_t] \) según reglas:  
     - Para cada \( a \in Primero(\alpha) \), insertar \( A \rightarrow \alpha \) en \( M[A, a] \).  
     - Si \( \varepsilon \in Primero(\alpha) \), insertar para todos \( b \in Siguiente(A) \).

---

### **Implementación**

El analizador sintáctico puede:

- **Escribirse manualmente** (más control, más complejidad).  
- **Generarse automáticamente** con herramientas como:  
  - CUP, YACC, Bison, ANTLR (descendentes y ascendentes).

**Criterios de eficiencia**:

- Tiempo de análisis proporcional al tamaño del código.  
- Decisión de la acción a realizar usando un número limitado de tokens.  
- Evitar retrocesos siempre que sea posible.

---