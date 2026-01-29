---
title: "Automatas"
date: 2026-01-26
tags:
  - ciencias-computacion
  - compiladores
  - automatas
---
Aquí tienes el apartado **Autómatas** reescrito y ampliado usando tanto el contenido del Tema 2 como el Tema 3 que me pasaste para que quede más técnico, coherente y completo:

---

## **Autómatas en el análisis léxico**

En el contexto de los compiladores, un **autómata** es un modelo matemático que permite reconocer patrones de entrada, siendo la herramienta fundamental para implementar analizadores léxicos. Estos modelos procesan una secuencia de caracteres de entrada, cambiando de estado según reglas de transición predefinidas, hasta determinar si la cadena es aceptada o rechazada según el lenguaje que representan.

Los autómatas relevantes en esta etapa son los **Autómatas Finitos**, que pueden ser **deterministas (AFD)** o **no deterministas (AFND)**.

---

### **1. Autómata Finito Determinista (AFD)**

Un **AFD** se define como una 5-tupla:

AFD=(Σ,Q,f,q0,F)AFD = (\Sigma, Q, f, q_0, F)

donde:

- Σ\Sigma: Alfabeto de símbolos de entrada.
    
- QQ: Conjunto finito y no vacío de estados.
    
- ff: Función de transición f:Q×Σ→Qf: Q \times \Sigma \rightarrow Q.
    
- q0∈Qq_0 \in Q: Estado inicial.
    
- F⊆QF \subseteq Q: Conjunto de estados de aceptación (finales).
    

Un AFD acepta una cadena si, tras consumir todos los caracteres, termina en un estado final. En el análisis léxico, cada estado final está asociado a un token específico y, a menudo, a una acción semántica (por ejemplo, registrar un identificador en la tabla de símbolos).

**Características clave:**

- Cada estado tiene exactamente una transición definida para cada símbolo del alfabeto.
    
- Más simple de ejecutar en un ordenador que un AFND.
    
- Se puede obtener a partir de cualquier ER mediante conversión ER → AFND → AFD.
    

---

### **2. Autómata Finito No Determinista (AFND)**

Un **AFND** es similar a un AFD pero con dos diferencias clave:

- Un estado puede tener **varias transiciones** para un mismo símbolo.
    
- Puede incluir **transiciones ε** (epsilon), que no consumen entrada.
    

**Ventaja**: más simple de construir directamente a partir de una expresión regular usando el **algoritmo de McNaughton–Yamada–Thompson**.  
**Desventaja**: no se ejecuta de forma directa y eficiente, por lo que se transforma en un AFD antes de implementarlo.

---

### **3. Transformación ER → AFND → AFD**

#### **De ER a AFND**

El algoritmo de **Thompson** construye un AFND para cualquier ER aplicando reglas de composición:

- **Símbolo literal**: un autómata de dos estados con una transición etiquetada.
    
- **Concatenación**: se enlazan dos subautómatas en secuencia.
    
- **Alternativa (|)**: se añaden transiciones ε para bifurcar y unir caminos.
    
- **Cerradura (*)**: se rodea el autómata con transiciones ε que permiten repetirlo cero o más veces.
    

Ejemplo:  
ER: `ab|c*`

- Se construye un árbol sintáctico.
    
- Se generan subautómatas para `a`, `b` y `c*`.
    
- Se combinan usando las reglas anteriores para formar un AFND.
    

---

#### **De AFND a AFD**

El método de **construcción por subconjuntos** convierte un AFND en un AFD:

1. Calcular la **ε-cerradura** del estado inicial → primer estado del AFD.
    
2. Para cada símbolo del alfabeto, aplicar `mover(T, a)` seguido de otra **ε-cerradura** para generar nuevos estados.
    
3. Repetir el proceso para cada nuevo estado hasta que no aparezcan estados nuevos.
    
4. Marcar como finales todos los estados que contengan al menos un estado final del AFND.
    

---

### **4. Minimización del AFD**

El AFD resultante puede tener estados redundantes. Para optimizarlo:

- **Teorema de Myhill-Nerode**: dos estados son distinguibles si existe una cadena que lleva a uno a aceptación y al otro a rechazo.
    
- Procedimiento:
    
    - Marcar como distinguibles todos los pares (final, no final).
        
    - Iterar marcando nuevos pares según las transiciones.
        
    - Combinar los pares no marcados → estados equivalentes.
        

Esto genera un **AFD mínimo**, único para un lenguaje dado.

---

### **5. Uso en el análisis léxico**

En un compilador:

1. El programador especifica tokens con expresiones regulares.
    
2. El generador las transforma en un AFND → AFD → AFD mínimo.
    
3. Se implementa el AFD como:
    
    - Tabla de transiciones y bucle de lectura de caracteres.
        
    - Acciones asociadas a estados finales para emitir tokens.
        

---

Cuando en un lenguaje de alto nivel usas una **expresión regular** —por ejemplo en Python con `re.match()`, en Java con `Pattern/Matcher` o en JavaScript con `/regex/`—, internamente **no se compara carácter a carácter de forma “manual”**, sino que el motor de expresiones regulares traduce ese patrón a alguna forma de **autómata** y luego lo ejecuta sobre la cadena de entrada.

En términos formales, lo que ocurre es algo así:

1. **Compilación de la ER**
    
    - El motor toma la expresión regular y la transforma en una estructura interna.
        
    - Teóricamente, esto es equivalente a construir un **AFND** usando el algoritmo de **Thompson**.
        
2. **Conversión y optimización**
    
    - El AFND se convierte en un **AFD** mediante el algoritmo de **construcción por subconjuntos**.
        
    - Algunos motores lo minimizan para eliminar estados redundantes.
        
    - Otros, en lugar de convertirlo por completo a un AFD, mantienen un **backtracking** tipo AFND, lo que permite manejar patrones más complejos pero puede ser más lento.
        
3. **Ejecución sobre la entrada**
    
    - El autómata resultante lee carácter por carácter, cambiando de estado según las transiciones.
        
    - Si al final de la lectura se está en un **estado de aceptación**, la coincidencia es válida.
        

---

 **Dato curioso:**

- Motores como el de **grep** clásico o el de **lex/flex** implementan realmente un **AFD puro**, por lo que el tiempo de ejecución es lineal respecto a la longitud de la cadena.
    
- Motores más “ricos” como el de **PCRE** (Perl Compatible Regular Expressions) usan un **backtracking** que, aunque más flexible, puede tener un rendimiento peor en casos adversos.
    

---

Si quieres, puedo hacerte un **diagrama paso a paso** mostrando cómo una regex como

scss

CopiarEditar

`[a-zA-Z]([a-zA-Z]|[0-9])*`

se convierte en un AFND, luego en AFD y finalmente en el autómata que realmente se ejecuta cuando la llamas en un lenguaje de alto nivel