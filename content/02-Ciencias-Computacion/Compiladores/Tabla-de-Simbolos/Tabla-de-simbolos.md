---
title: "Tabla De Simbolos"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - tabla-de-simbolos
---
La **tabla de símbolos** es una estructura de datos central en la fase de _front-end_ del compilador. Sirve como un “diccionario” donde el compilador guarda y consulta toda la información relevante sobre **identificadores** (variables, funciones, constantes, tipos, etc.) que aparecen en el código fuente.

Piensa en ella como una **agenda del compilador**: cada vez que el analizador léxico, sintáctico o semántico detecta un nuevo símbolo, lo “anota” con todos sus datos.

---

## **1. Funciones principales**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

- **Insertar** un símbolo cuando se declara por primera vez.
    
- **Buscar** un símbolo cuando aparece en el código para obtener su información.
    
- **Actualizar** datos de un símbolo (por ejemplo, añadir su dirección de memoria).
    
- **Eliminar** símbolos cuando salen de su ámbito (por ejemplo, al salir de una función).
    

---

## **2. Qué información guarda**

Depende del tipo de símbolo:

- **Variable:**
    
    - Tipo (`int`, `float`, `struct`…)
        
    - Dirección en memoria (offset o registro)
        
    - Alcance (_scope_)
        
    - Valor inicial (si lo tiene)
        
- **Constante:**
    
    - Tipo y valor literal
        
- **Función / Procedimiento:**
    
    - Lista y tipo de parámetros
        
    - Tipo de retorno
        
    - Forma de paso de parámetros (por valor, por referencia)
        
    - Dirección de inicio de código
        
- **Tipos definidos por el usuario:**
    
    - Campos de un `struct` o `class`
        
    - Límites de arrays
        

---

## **3. Uso dentro del compilador**

- **Análisis léxico:** puede crear entradas iniciales (palabras reservadas, símbolos predefinidos).
    
- **Análisis sintáctico:** al reconocer declaraciones, pide insertar entradas nuevas.
    
- **Análisis semántico:** valida que un identificador esté declarado antes de usarlo, y que el tipo concuerde con su uso.
    
- **Generación de código:** usa la dirección, tamaño y tipo para emitir instrucciones correctas.
    

---

## **4. Implementaciones comunes**

- **Lista lineal:** fácil de implementar, pero lenta para muchos símbolos.
    
- **Tabla hash:** la más habitual; acceso rápido promedio O(1).
    
- **Árboles de búsqueda (AVL, B-tree):** útiles si hay ordenamientos o búsquedas por rango, aunque menos comunes para compiladores.
    

---

## **5. Ámbitos y reglas de alcance**

La tabla de símbolos debe manejar **estructuras de bloques** (scopes) y **ocultamiento** de nombres:

- **Ámbito local:** válido solo dentro de una función o bloque.
    
- **Ámbito global:** válido en todo el programa.
    
- **Regla de anidación más próxima:** si un nombre existe en varios ámbitos, se usa el más cercano al punto de uso.
    

**Ejemplo en C:**

```c
int x; // Global

void f() {
    int x; // Local, oculta la global
    x = 5; // Se refiere al x local
}
```

---

## **6. Ejemplo de entrada en tabla de símbolos**

|Nombre|Tipo|Categoría|Alcance|Dirección|Otros atributos|
|---|---|---|---|---|---|
|`PI`|double|Constante|Global|ConstSeg|Valor=3.1415|
|`x`|int|Variable|Local f()|FP-4|Inicializada=false|
|`f`|func|Procedim.|Global|CódigoSeg|Params=(int,float)|

---

Si quieres, puedo prepararte un **ejemplo visual** donde, al compilar un pequeño programa en C o Pascal, veas cómo la tabla de símbolos se va llenando paso a paso conforme actúan el léxico, el sintáctico y el semántico.  
¿Quieres que lo haga?