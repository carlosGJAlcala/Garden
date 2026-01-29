---
title: "Expresion Regular"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - analizadores-lexicos
---

Una **expresión regular** (ER) es una notación formal utilizada para describir patrones de texto, es decir, conjuntos de cadenas que cumplen unas determinadas reglas. Su origen se remonta a la teoría de lenguajes formales y autómatas, y su uso es fundamental en el **análisis léxico** de compiladores, ya que permite especificar de forma compacta y precisa los **patrones** que definen los **tokens** del lenguaje de programación.

En términos formales, una expresión regular describe un **lenguaje regular**, es decir, un conjunto de palabras sobre un alfabeto finito que puede ser reconocido por un **autómata finito** determinista (AFD) o no determinista (AFND).

---

### **Componentes básicos de una expresión regular**

1. **Símbolos literales**  
    Cualquier carácter del alfabeto se representa a sí mismo.  
    Ejemplo:
    
    - La ER `a` representa la cadena `"a"`.
        
    - La ER `0` representa la cadena `"0"`.
        
2. **Cadena vacía (ε)**  
    Representa la palabra vacía, es decir, una cadena de longitud cero.  
    Ejemplo: La ER `ε` acepta solo la cadena vacía.
    
3. **Operadores fundamentales**
    
    - **Concatenación**: Si `R1` y `R2` son expresiones regulares, `R1R2` representa todas las cadenas que son el resultado de concatenar una cadena de `R1` seguida de una cadena de `R2`.  
        Ejemplo: `ab` acepta `"ab"`.
        
    - **Alternativa (|)**: Si `R1` y `R2` son expresiones regulares, `R1|R2` acepta cualquier cadena aceptada por `R1` o por `R2`.  
        Ejemplo: `a|b` acepta `"a"` o `"b"`.
        
    - **Cerradura de Kleene (*)**: `R*` acepta cero o más repeticiones de cadenas aceptadas por `R`.  
        Ejemplo: `(ab)*` acepta `""`, `"ab"`, `"abab"`, etc.
        
    - **Cerradura positiva (+)**: `R+` acepta una o más repeticiones de cadenas aceptadas por `R`.  
        Ejemplo: `(ab)+` acepta `"ab"`, `"abab"`, pero no `""`.
        
    - **Opción (?)**: `R?` acepta la cadena vacía o una cadena aceptada por `R`.  
        Ejemplo: `a?` acepta `""` o `"a"`.
        
4. **Agrupaciones**
    
    - **Clases de caracteres**: `[abc]` equivale a `a|b|c`. Los rangos también están permitidos: `[a-z]`, `[0-9]`.
        
    - **Subexpresiones**: Paréntesis `( )` para agrupar y aplicar operadores a conjuntos más complejos.  
        Ejemplo: `(a|b)*c` acepta cualquier cadena formada por `a` y `b` y terminada en `c`.
        

---

### **Ejemplos prácticos de ER aplicadas al análisis léxico**

- **Palabras reservadas**:
    
    ```
    if|else|then|for|while
    ```
    
    Esta ER detecta cualquiera de esas cinco palabras exactas.
    
- **Número entero par**:
    
    ```
    [0-9]*(0|2|4|6|8)
    ```
    
    Acepta secuencias de dígitos cuyo último sea par.
    
- **Número real**:
    
    ```
    [0-9]+(\.[0-9]+)?
    ```
    
    Acepta números enteros o reales con parte decimal opcional.
    
- **Identificador** (letras y dígitos, comenzando por letra):
    
    ```
    [a-zA-Z]([a-zA-Z]|[0-9])*
    ```
    
- **Secuencias binarias sin dos ceros consecutivos**:
    
    ```
    0?(10|1)*
    ```
    
- **Teléfono móvil español**:
    
    ```
    (6|7)[0-9]{8}
    ```
    
- **Definición de array como `{1.1, 3.33, 2, 9}`**:
    
    ```
    \{([0-9]+(\.[0-9]+)?(, [0-9]+(\.[0-9]+)?)*)?\}
    ```
    

---

### **Definiciones regulares para reutilización**

Para facilitar la construcción de patrones complejos, es habitual definir subcomponentes reutilizables:

```
Letra       → [a-zA-Z]
Dígito      → [0-9]
Identificador → Letra(Letra|Dígito)*
NúmeroReal  → Dígito+(\.Dígito+)?
Fracción    → (\.Dígito+)?
Exponente   → (E(\+|-)?Dígito+)?
NúmeroReal  → Dígito+ Fracción Exponente
```

Esto mejora la legibilidad y facilita el mantenimiento del código del analizador léxico.

---

### **Relación con autómatas finitos**

Cada expresión regular puede transformarse en un **autómata finito no determinista (AFND)** equivalente, que a su vez puede convertirse en un **autómata finito determinista (AFD)**. Esta equivalencia es la base de los generadores automáticos de analizadores léxicos como **Lex** o **JFlex**:

1. El programador define tokens mediante ER.
    
2. El generador traduce las ER a AFND.
    
3. El AFND se convierte en un AFD.
    
4. El AFD se implementa como código ejecutable.
    
