---
title: "Analizador Semantico"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - analisis-semantico
---
El **analizador semántico** es la tercera gran etapa del _front-end_ de un compilador, después del **léxico** y el **sintáctico**, y su papel es **dar significado y coherencia al código** más allá de la estructura.

En pocas palabras:

- El **léxico** pregunta: “¿Esto es un token válido?”
    
- El **sintáctico** pregunta: “¿Estos tokens están en un orden gramatical correcto?”
    
- El **semántico** pregunta: “¿Esto tiene sentido en el contexto del lenguaje?”
    

---

## **1. Función del analizador semántico**


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

El analizador semántico trabaja **sobre el árbol sintáctico** generado por el parser y, usando información de la **tabla de símbolos**, realiza:

1. **Comprobaciones estáticas** (en tiempo de compilación):
    
    - Tipos compatibles en operaciones (`int + float`, `string + int`, etc.).
        
    - Que las variables y funciones estén **declaradas antes de usarse**.
        
    - Que el número y tipo de parámetros en llamadas a funciones coincidan con su definición.
        
    - Que los identificadores no estén duplicados en el mismo ámbito.
        
    - Que las constantes no se modifiquen.
        
2. **Comprobaciones dinámicas** (insertando código que se verificará en ejecución):
    
    - Acceso a índices de arrays dentro de rango.
        
    - División entre cero.
        
    - Comprobaciones de punteros nulos.
        
3. **Decoración del árbol sintáctico**:
    
    - Añadir atributos a cada nodo: tipo, valor, ubicación en memoria, etc.
        
    - Ejemplo: el nodo `a + b` recibe como atributo el tipo resultante tras aplicar las reglas de promoción de tipos.
        

---

## **2. Herramientas y mecanismos**

- **Gramáticas de atributos**:  
    Extienden la gramática sintáctica añadiendo **reglas semánticas** para calcular propiedades.
    
    - **Atributos sintetizados**: calculados desde los hijos hacia el padre.
        
    - **Atributos heredados**: calculados desde el padre o hermanos hacia un nodo.
        
- **Traducción dirigida por la sintaxis**:  
    El significado se asocia directamente con la forma del árbol sintáctico.
    
- **Grafos de dependencias**:  
    Representan qué atributos dependen de cuáles para calcularlos en orden correcto.
    

---

## **3. Ejemplos de comprobaciones semánticas**

**Ejemplo 1 — Tipos compatibles:**

```pascal
VAR x : INTEGER;
    y : REAL;
BEGIN
    x := y + 3.14;
END;
```

El semántico detecta que `y + 3.14` es `REAL` y exige conversión antes de asignar a `x`.

**Ejemplo 2 — Variable no declarada:**

```c
int main() {
    z = 10; // Error: 'z' no ha sido declarada
}
```

**Ejemplo 3 — Parámetros correctos:**

```c
void f(int a, float b);
...
f(3, "hola"); // Error: el segundo argumento debería ser float
```

---

## **4. Relación con las otras fases**

1. **Léxico** → reconoce que `if`, `x`, `<`, `10` son tokens válidos.
    
2. **Sintáctico** → verifica que `if (x < 10) { y = y + 1; }` sigue la gramática del lenguaje.
    
3. **Semántico** → confirma que `x` y `y` están declaradas, que `<` es válido para sus tipos, que `y+1` puede asignarse a `y`.
    

---

Si quieres, puedo montarte **un ejemplo completo** donde tomemos un fragmento de código, lo pasemos por léxico, sintáctico y semántico, para que veas **qué detecta cada uno** y dónde el sintáctico no basta pero el semántico sí detecta el error.  
¿Quieres que lo haga?