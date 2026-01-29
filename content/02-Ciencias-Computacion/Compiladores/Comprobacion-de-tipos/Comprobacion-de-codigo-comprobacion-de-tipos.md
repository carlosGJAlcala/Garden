---
title: "Comprobación de código (comprobación de tipos)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - comprobacion-de-tipos
---
¿Te refieres a la **comprobación de código** dentro del compilador (lo que típicamente llamamos **comprobación de tipos**)? Te dejo un resumen ampliado y práctico de cómo se hace, con qué reglas, y cómo se implementa, enlazándolo con la tabla de símbolos y el análisis semántico.

---

# Comprobación de código (comprobación de tipos)


> **Relacionado**: [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

## Qué es y por qué importa

La **comprobación de tipos** es el conjunto de reglas y mecanismos que verifican que cada parte del programa “tiene sentido” según el **sistema de tipos** del lenguaje. Es parte del **análisis semántico** y se apoya en la **tabla de símbolos**. Su objetivo: detectar incoherencias antes (estático) o durante (dinámico) la ejecución.

### Estático vs. dinámico

- **Estática (en compilación):** evita muchos errores y no sobrecarga el binario con comprobaciones en tiempo de ejecución (ej.: C, Java, Pascal).
    
- **Dinámica (en ejecución):** más flexible para prototipos (ej.: Python), a costa de introducir checks en runtime. En la práctica, muchos lenguajes combinan ambos enfoques.
    

---

## Piezas que intervienen

- **Sistema de tipos:** define tipos base, constructores (arrays, registros, funciones, punteros…), y reglas de compatibilidad.
    
- **Expresiones de tipos:** representación interna (a menudo con **grafos acíclicos dirigidos**) para comparar y reutilizar estructuras de tipos eficientemente.
    
- **Tabla de símbolos:** guarda para cada identificador su tipo, clase (var, const, función…), ámbito, etc.; el verificador consulta aquí cada vez que aparece un nombre.
    
- **Árbol sintáctico + atributos:** las reglas semánticas decoran el árbol con tipos (síntesis/herencia) y disparan errores cuando no cuadran.
    

---

## Qué se comprueba (core)

1. **Uso de identificadores**  
    Declaración previa, clase correcta, y visibilidad según el ámbito.
    
2. **Asignaciones**  
    El tipo RHS debe ser **compatible** con el LHS (conversión permitida o coerción definida).
    
3. **Operaciones**  
    Operandos compatibles con el operador; resultado con tipo bien definido (promociones `int→float`, etc.).
    
4. **Llamadas a funciones**  
    Número/orden/tipos de argumentos vs. firma; tipo de retorno usado coherentemente.
    
5. **Estructuras compuestas**  
    Índices de arrays del tipo esperado; campos de `struct/record` existentes y con el tipo correcto. (El rango del índice es análisis adicional, no estricto “tipo” en sí).
    
6. **Conversión de tipos**
    
    - **Explícita (cast):** el programador la solicita.
        
    - **Implícita (coerción):** la hace el compilador si el lenguaje lo permite.
        
7. **Equivalencia/compatibilidad de tipos**
    
    - **Estructural:** misma forma (ej.: dos `array(0..5, real)` son equivalentes).
        
    - **Nominal:** los alias de tipo cuentan como tipos básicos distintos.
        
    - **Funcional:** pueden usarse indistintamente en un contexto sin transformar el valor.
        
8. **Sobrecarga y polimorfismo**  
    Resolver qué versión aplica según los tipos; mantener conjuntos de tipos por identificador.
    

---

## Algoritmo práctico (esqueleto)

1. **Decoración de expresiones**
    

- Para un literal/identificador: `tipo(node) ← tipo_en_tabla_simbolos(name)`.
    
- Para `E1 op E2`:
    
    - `t1 ← tipo(E1)`, `t2 ← tipo(E2)`
        
    - si `compatible(op, t1, t2)` entonces `tipo(node) ← tipo_resultante(op, t1, t2)`; si se requiere, inserta coerciones en el IR.
        
    - si no, **error de tipos**.
        

2. **Asignaciones**
    

- `tL ← tipo(LHS)`, `tR ← tipo(RHS)`
    
- si `tR` convertible/compatible con `tL`, ok (añadir conversión si procede); si no, error.
    

3. **Llamadas**
    

- Busca firma en tabla; compara lista de argumentos (longitud y tipos). Error si no coincide; el tipo del nodo es el tipo de retorno.
    

Este esquema se implementa con **gramáticas de atributos** (S-atribuidas para análisis ascendente; L-atribuidas para pasar contexto), evaluando reglas cuando el parser reduce o expande.

---

## Ejemplos rápidos

- **Asignación con promoción:**
    
    ```
    int x; float y;
    x = y + 3.14; // y+3.14 : float ⇒ requiere conversión a int o error según lenguaje
    ```
    
    (promociones/reglas definidas en el sistema de tipos).
    
- **Array index:**
    
    ```
    real a[1..10];
    a[i] = 2.0; // tipo(i)==integer; a[i]: real
    ```
    
    (rango es verificación adicional; el tipo de `a[i]` es `real`).
    
- **Equivalencia estructural vs. nominal:**  
    Dos `array(0..5, array(0..5, real))` pueden ser equivalentes **estructuralmente**; nominalmente no, si el lenguaje trata los alias como tipos básicos distintos.
    

---

## Relación con la tabla de símbolos y el AST

- La **tabla de símbolos** se actualiza en declaraciones (tipos, parámetros, forma de paso, etc.) y se consulta en usos; maneja **ámbitos anidados** para aplicar “anidación más próxima”.
    
- El **árbol** se **anota** con atributos (`.tipo`, `.val`, etc.) y se usa un **grafo de dependencias** para respetar el orden de cálculo.
    

---

## Qué errores “de código” te pilla aquí

- Usar una variable no declarada / fuera de ámbito.
    
- Operar `string + int` (si el lenguaje no lo define).
    
- Llamar `f(int, float)` como `f(3, "hola")`.
    
- Escribir en una constante o asignar a un valor de tipo incompatible.
    

---

Si quieres, te preparo un **mini-ejemplo de lenguaje** (declaraciones, expresiones y funciones) y te muestro:

1. Cómo se llena la **tabla de símbolos**,
    
2. Cómo se **anota** el árbol con tipos, y
    
3. Dónde saltan exactamente los **errores de tipos** según tus reglas (estático vs. dinámico).