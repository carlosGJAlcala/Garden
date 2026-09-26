---
title: "Análisis sintáctico"
---


# Tema 4 — Análisis Sintáctico: Introducción, Gramáticas y Métodos

## Contenidos
- Objetivos y contexto
- Gramáticas
- Análisis Sintáctico Descendente - Recursivo
- Análisis Sintáctico Descendente - Predictivo
## Objetivos
Entender qué es el análisis sintáctico, la teoría de gramáticas y los métodos de análisis de las mismas, para conocer las responsabilidades y funciones del analizador sintáctico.
## Función del analizador sintáctico
- El analizador sintáctico ( parser) construye una representación del programa analizado.
- Para hacerlo, utiliza los tokens que recibe y, aplicando las producciones de la gramática, genera un árbol sintáctico ( o de análisis).
- Comprueba que el orden en que el analizador léxico le va entregando los tokens es válido:
 - Verifica que la cadena pueda ser generada por la gramática del lenguaje.
 - Informa acerca de los errores de sintaxis, recuperándose de los mismos ( si es posible) para continuar procesando la entrada.
La salida del analizador sintáctico es una representación en forma de árbol sintáctico de la cadena de componentes léxicos producida por el analizador léxico.
### Criterios a cumplir
- *Eficiencia**: en general, el tiempo de análisis debería ser proporcional al tamaño del archivo.
- La acción a realizar debe poder decidirse conociendo un número limitado de componentes léxicos de la entrada.
- Deben evitarse los retrocesos; las acciones a realizar se deben poder predecir con exactitud.
### Implementación
Como en el análisis léxico, encontramos dos opciones:
- Utilizando un lenguaje de programación: mayor control, pero no compensa su complejidad.
- Utilizando un generador de analizadores sintácticos como CUP, YACC, Bison, ANTLR. Mucho más sencillo, pero el código generado es más difícil de mantener y tenemos menos control sobre la eficiencia.
### Aproximaciones de los analizadores sintácticos
Hay dos formas de enfrentarse al análisis sintáctico:
- *Analizadores sintácticos descendentes ( Top-down)**
 - Construyen el árbol desde la raíz ( arriba) hasta las hojas ( abajo).
 - Parten del símbolo inicial de la gramática ( axioma) y van expandiendo producciones hasta llegar a la cadena de entrada.
- *Analizadores sintácticos ascendentes ( Bottom-up)**
 - Construyen el árbol desde las hojas.
 - Parten de los terminales de la entrada y, mediante reducciones, llegan hasta el símbolo inicial.
En ambos casos se examina la entrada de izquierda a derecha, analizando los tokens de entrada de uno en uno.
## Gramáticas
### Gramática Independiente del Contexto ( CFG)
La sintaxis de un lenguaje se especifica mediante CFGs. Principales ventajas:
- Describen de forma natural la estructura jerárquica de las construcciones de los lenguajes de programación.
- Facilitan la construcción de analizadores sintácticos eficientes.
- Si se diseña correctamente, imponen una estructura al lenguaje que resulta útil para la traducción posterior a código objeto y para detectar errores.
- Son fácilmente ampliables.
Es posible construir un analizador sintáctico para cualquier CFG.
### Descripción de una CFG
Componentes de una gramática: G = ( Vt, Vn, S, P)
- Símbolos terminales ( componentes léxicos), Vt.
- Símbolos no terminales, Vn.
- Producciones, formadas por terminales y no terminales, P.
- Símbolo inicial o axioma, S.
Una gramática se describe mostrando la lista de sus producciones, formadas por un símbolo no terminal ( izquierda), una flecha y una secuencia de símbolos terminales y no terminales ( parte derecha).
```
E : E + E
E : E − E
E : n
```
También existen otras notaciones, como la Backus-Naur Form ( BNF) o Extended BNF ( EBNF).
### Backus-Naur Form ( BNF)
Es una notación alternativa, con la siguiente representación:
- El símbolo `::=` significa "se define como".
- Una barra `|` representa el OR lógico.
- Los símbolos `< >` encierran a los no terminales.
- Los terminales se escriben directamente.
- Y más reglas.
Ejemplo:
```
<identificador> ::= <letra> | <identificador>[<letra>|<dígito>]
```
### Lenguaje definido por una gramática
Son el conjunto de cadenas de componentes léxicos derivadas del símbolo inicial de la gramática.
$$L ( G) = \{s \mid \text{exp} \to^* s\}$$
Ejemplos:
- `E : ( E) | a` : L ( G) = {a, ( a), (( a)), ((( a))), ...}
- `E : E + a | a` : L ( G) = {a, a+a, a+a+a, ...}
### Ejemplo general
Por ejemplo, para especificar la sintaxis de un bloque de lenguaje C mediante una CFG haríamos algo así:
```
Bloque : { Sentencias }
Sentencias : ListaSentencias | ε
ListaSentencias : ListaSentencias ; sentencia | sentencia
```
### Árbol gramatical
Un árbol gramatical de una derivación es un árbol etiquetado con elementos no terminales en su interior y elementos terminales en las hojas. Los hijos representan los pasos de derivación.
```
EXP : EXP OP EXP
EXP : DIG
OP : + | − | * | /
DIG : 0|1|2|3|4|5|6|7|8|9
```
### Derivaciones
Se denomina derivación a la sucesión de una o más producciones: A1 ⇒ A2 ⇒ A3 ⇒ ... ⇒ An, o también A1 ⇒* An.
Una cadena de componentes léxicos es considerada válida si existe una derivación en la gramática del lenguaje fuente que parta del símbolo inicial y que, tras aplicar las producciones a los no terminales, genere la frase a reconocer.
Con la gramática anterior:
- Válida: 3+4+5
- No válida: −1+2
Las derivaciones pueden ser por la izquierda o por la derecha ( canónicas). En la derivación por la izquierda, solo el no terminal de más a la izquierda de cualquier forma de frase se sustituye en cada paso:
```
EXP ⇒ EXP OP EXP ⇒ DIG OP EXP ⇒ 3 OP EXP ⇒ 3 + EXP ⇒ 3 + DIG ⇒ 3 + 4
```
### Recursividad
Nos permite expresar la iteración usando un número reducido de reglas de producción. Su estructura es:
- Una o más reglas no recursivas que forman el caso base.
- Una o más reglas recursivas que permiten crecer desde el caso base.
Ejemplo: un tren con un número indeterminado de vagones.
**Solución no recursiva:**
```
TREN : locomotora
TREN : locomotora vagon
TREN : locomotora vagon vagon
```
**Solución recursiva:**
- Regla base: `TREN : locomotora`
- Regla recursiva: `TREN : TREN vagon`
Nótese cómo la solución recursiva no pone límite al crecimiento.
Una gramática se dice que es recursiva si en una derivación de un símbolo no terminal aparece dicho símbolo en la parte derecha ( A ⇒* αAβ). Definimos tipos de recursividad:
- *Por la izquierda**: funciona bien para el análisis ascendente, pero es un problema para el descendente ( A ⇒* Aβ).
- *Por la derecha**: utilizada para el análisis descendente ( A ⇒* αA).
- *Por ambos lados**: no se usa porque produce gramáticas ambiguas.
### Ambigüedad
Una gramática se dice que es ambigua si el lenguaje que define contiene alguna cadena cuya representación en árbol sintáctico no es única.
La ambigüedad es indeseable para la mayoría de analizadores, puesto que:
- Es complicado generar representaciones intermedias consistentes.
- Se pierde eficiencia.
Afortunadamente, seguir ciertas reglas permite garantizar la no ambigüedad de una gramática.
Algunas reglas importantes:
**No permitir ciclos:**
```
S : A
S : a
A : S
```
**Suprimir reglas con caminos alternativos:**
```
S : A
S : B
A : B
```
**Evitar producciones recursivas en que las variables no recursivas puedan derivar a la cadena vacía:**
```
S : HRS
S : s
H : h | ε
R : r | ε
```
Resumiendo:
- Que una gramática sea ambigua implica que a una sentencia se le puedan asignar significados ( semánticas) diferentes.
- El algoritmo para crear el árbol sintáctico para una gramática ambigua necesita de prueba y retroceso.
- Si un lenguaje es ambiguo, existirán varios significados posibles para un mismo programa y, por lo tanto, el compilador podría generar varios códigos máquina distintos para un mismo código fuente.
- Un análisis sintáctico determinista es más eficiente.
En resumen, las gramáticas para los lenguajes de programación no deben ser ambiguas.
### Recordando los tipos de analizadores
Teníamos:
- Analizadores sintácticos descendentes ( Top-down o ASD).
- Analizadores sintácticos ascendentes ( Bottom-up o ASA).
Empezaremos por los ASD, pero es importante notar que:
- Los métodos descendentes son más fáciles de implementar sin generadores automáticos.
- Los métodos ascendentes pueden manejar una mayor variedad de gramáticas, por lo que suelen ser los métodos usados por los generadores automáticos.
- Para cualquier gramática existe al menos un analizador sintáctico general que la analiza en un tiempo O ( n³) para una cadena de n componentes léxicos. Para la mayoría de lenguajes de programación es posible hacerlo lineal O ( n).
## Análisis Sintáctico Descendente ( ASD)
Son métodos que parten del axioma y, mediante derivaciones por la izquierda, tratan de encontrar la entrada. Se pueden implementar de dos formas:
- *Análisis descendente recursivo**: es la manera más sencilla, implementándose con una función recursiva que aprovecha la propia recursividad de la gramática.
- *Análisis descendente predictivo**: para aumentar la eficiencia y evitar los retrocesos, se predice en cada momento cuál de las reglas sintácticas hay que aplicar para continuar el análisis.
En la práctica, el recursivo ( o con retroceso) apenas se usa debido a diversos inconvenientes.
### ASD Recursivo
Mediante un método de backtracking se van probando todas las opciones de expansión para cada no terminal de la gramática hasta encontrar la correcta.
- Cada retroceso en el árbol sintáctico tiene asociado un retroceso en la entrada: se deben eliminar todos los terminales y no terminales correspondientes a la producción que se "elimina" del árbol.
- Si el terminal obtenido como consecuencia de probar con una opción de las varias de una producción no coincide con el componente léxico leído en la entrada, hay que retroceder.
**Algoritmo**
1. Se colocan las reglas en orden, de forma que si la parte derecha de una producción es prefijo de otra, la última se sitúa detrás.
2. Se crea el nodo inicial con el axioma y se considera nodo activo.
3. Para cada nodo activo A:
 - Si A es un no terminal, se aplica la primera producción asociada.
 - El hijo izquierdo pasa a ser el nodo activo.
 - Cuando se terminan de tratar todos los descendientes, el siguiente hijo pasa a ser activo.
4. Si A es un terminal:
 - Si coincide con el símbolo de la entrada, se avanza el puntero de entrada y el nodo activo pasa a ser el siguiente "hermano" de A.
 - Si no, se retrocede en el árbol hasta el anterior no terminal ( y en la entrada) y se prueba la siguiente producción.
 - Si no hay más producciones a probar, se retrocede hasta el anterior no terminal y se prueba con la siguiente opción de este.
5. Si se acaban todas las opciones del nodo inicial, error sintáctico. Si, por lo contrario, se encuentra un árbol que encaja, éxito.
**Ejemplo ASD Recursivo**
Vamos a comprobar si `ccd` pertenece al lenguaje de la gramática:
```
S : cXd
X : ck | c
```

| Entrada | Pila | Regla a aplicar | Coincide pila con entrada | Queda en pila | Queda en entrada |
| ------- | ---- | --------------- | ------------------------- | ------------- | ---------------- |
| ccd     | S    | —               | —                         | —             | —                |
| ccd     | S    | S→cXd           | cXd                       | —             | —                |
| cd      | Xd   | S→cXd           | cXd, c                    | Xd            | cd               |
| cd      | Xd   | X→ck            | ckd, c                    | kd            | d                |
| d       | kd   | error           | deshacer todo             | deshacer todo | deshacer todo    |
| cd      | Xd   | X→c             | cd, c                     | d             | d                |
| d       | d    | —               | c, d                      | —             | —                |
`ccd` se reconoce con éxito tras retroceder de la opción `X→ck` a la opción `X→c`.
**Problemas del ASD recursivo**
- No puede tratar gramáticas con recursividad a izquierdas ( entra en bucle infinito).
- Acaba la ejecución al encontrar el primer error, con lo que es difícil proporcionar mensajes de error elaborados.
- Aunque sea simple de programar, usa muchos recursos debido a la necesidad de retroceso.
- Cuando el analizador sintáctico se usa para comprobar también la semántica y generar código, cada vez que se expande una regla se ejecutan acciones semánticas. Retroceder estas acciones es poco práctico y, a veces, incluso imposible.
**Eliminación de la recursividad por la izquierda**
Para eliminar la recursión inmediata, si la gramática recursiva tiene la forma siguiente:
```
A : Aα1 | Aα2 | ... | Aαn | β1 | β2 | ... | βm
```
donde A es el no terminal recursivo, αi son las partes derechas de las reglas recursivas del no terminal A, y βi son las partes derechas de las reglas no recursivas del no terminal A.
Entonces la gramática no recursiva equivalente será:
```
A : β1 A' | β2 A' | ... | βm A'
A' : α1 A' | α2 A' | ... | αn A' | ε
```
Para eliminar la recursión indirecta se debe encontrar el elemento conflictivo y sustituirlo por su definición. Ejemplo:
```
S : Aa | b
A : Ac | Sd | ε
```
( A : S es recursiva por S : Aa). Sustituimos:
```
S : Aa | b
A : Ac | Aad | bd | ε
```
Y eliminamos la recursión inmediata de A como antes:
```
S : Aa | b
A : bd A' | A'
A' : c A' | ad A' | ε
```
**Ejercicio ASD Recursivo**
Dada la gramática:
```
A : aBb
B : cd | c
```
Realizar el ASD recursivo para reconocer las expresiones:
- acdb
- abcd
- acb
## Análisis Sintáctico Descendente Predictivo
### ASD Predictivo
Intentan predecir la siguiente derivación a aplicar leyendo uno o más componentes léxicos por adelantado.
- "Saben" qué regla deben expandir para llegar a la entrada.
Este tipo de analizadores se denomina LL ( k):
- Leen la entrada de izquierda a derecha ( Left to right).
- Aplican derivaciones por la izquierda para cada entrada ( Left).
- Utilizan k componentes léxicos de la entrada para predecir la dirección del análisis.
En función de la entrada, de la tabla de análisis y de la pila, decide la función a realizar. Posibles acciones:
1. Aceptar la cadena.
2. Aplicar producción.
3. Pasar al siguiente símbolo de la entrada.
4. Notificar error.
### Tabla de análisis sintáctico
Se trata de una matriz M[Vn, Vt] donde se representan las producciones a expandir en función del estado actual de análisis y del símbolo de la entrada. En caso de entrada en blanco es equivalente a error.
Ejemplo de tabla:

|     | a     | b     | c     | d     | e     | $     |
| --- | ----- | ----- | ----- | ----- | ----- | ----- |
| S   | S→BA  | error | error | S→BA  | error | error |
| A   | error | A→bSC | error | error | A→ε   | A→ε   |
| B   | B→DC  | error | error | B→DC  | error | error |
| C   | error | C→ε   | C→cDC | error | C→ε   | C→ε   |
| D   | D→a   | error | error | D→dSe | error | error |
La regla a aplicar vendrá dada por la tabla de análisis sintáctico.
**Ejemplo**
Gramática:
```
A : aBc | xC | B
B : bA
C : c
```
Reconocimiento de `babxcc`:

| Símbolo entrada | Regla a aplicar | Pila | Derivación |
| --------------- | --------------- | ---- | ---------- |
| b               | A→B             | B    | B          |
| b               | B→bA            | bA   | bA         |
| a               | A→aBc           | aBc  | baBc       |
| b               | B→bA            | bAc  | babAc      |
| x               | A→xC            | xCc  | babxCc     |
| c               | C→c             | cc   | babxcc     |
| c               | —               | c    | babxcc     |
| —               | —               | —    | babxcc     |
### Analizador LL ( 1)
Una gramática es LL ( 1) si la tabla de análisis sintáctico asociada tiene, como máximo, una producción en cada entrada de la tabla.
- Es decir, que solo necesitamos mirar el primer token de la entrada para decidir qué regla aplicar.
El análisis descendiente más común es LL ( 1), pues con k>1 la tabla de análisis es más complicada.
- En la práctica no se usan LL ( 2), LL ( 3), etc.
Sin embargo, no todas las gramáticas se pueden analizar mediante métodos descendientes predictivos.
**Condiciones**
Para que a una gramática se le pueda aplicar el método LL ( 1) debe cumplir:
- No es recursiva por la izquierda. Si lo es, tenemos mecanismos para transformarla.
- Si existe un conjunto de reglas de la forma A : α1 | α2 | ... | αn debe ser posible decidir la opción a escoger mirando solamente un token de la entrada ( es decir, dos productores del mismo terminal no pueden dar lugar al mismo token inicial).
### Conjuntos de predicción
Para construir la tabla de análisis y probar si la gramática es LL ( 1) se construyen dos conjuntos:
- Conjunto Primero.
- Conjunto Siguiente.
Los conjuntos Primero se calculan para todos los símbolos de la gramática, terminales y no terminales. Los conjuntos Siguiente se definen solo para los no terminales.
**Conjunto Primero**
Dado un símbolo de la gramática A, su conjunto Primero es el conjunto de terminales por los que comienza cualquier frase que se genere a partir de A mediante derivaciones por la izquierda de las producciones ( A ⇒ αi). El conjunto Primero ( A) estará, pues, formado por la unión de todos los Primero (αi).
$$a \in \text{Primero}(\alpha_i) \text{ si } a \in ( V_t \cup \{\varepsilon\}) \mid \alpha_i \to^* a\beta$$
**Algoritmo de cálculo del conjunto Primero (α):**
1. Si α ≡ ε: añadir ε a Primero (α).
2. Si α ≡ a, con a Terminal: añadir a a Primero (α).
3. Si α ≡ A, con A no Terminal: añadir Primero ( A) a Primero (α).
4. Si α ≡ AB, con A y B no Terminales y Primero ( A) incluyendo ε: añadir Primero ( A) a Primero (α) sin incluir todavía ε. Puesto que A puede ser vacío, añadir también Primero ( B). Se incluye finalmente ε en Primero (α) sí y solo sí éste aparece en los conjuntos Primero de todos los no Terminales implicados.
**Ejemplo simple**
```
A : BC
B : ε | m
C : ε | s
```
Solución:
- Primero ( A) = {m, s, ε}
- Primero ( B) = {m, ε}
- Primero ( C) = {s, ε}
¿Y ahora, con `C : s` ( sin ε)?
```
A : BC
B : ε | m
C : s
```
**Ejemplo**
```
E : T E'
E' : + T E' | ε
T : F T'
T' : * F T' | ε
F : ( E) | id
```
Solución:
- Primero ( E) = Primero ( T E') = Primero ( T) = Primero ( F) = {(, id}
- Primero ( E') = {+, ε}
- Primero ( T') = {*, ε}
### Conjunto Siguiente
Dado un símbolo de la gramática A, su conjunto Siguiente es el conjunto de terminales que aparecen inmediatamente después de A en alguna sentencia por la que se pasa al realizar una derivación por la izquierda:
$$a \in \text{Siguiente}( A) \text{ si } a \in ( V_t \cup \{\$\}) \mid \exists S \Rightarrow^* ...Aa...$$
**Algoritmo de cálculo del conjunto Siguiente:**
1. Siguiente ( S) = {$}, siendo S el axioma. Los conjuntos Siguiente de todos los demás no terminales son inicialmente vacíos.
2. Para cada símbolo no terminal A de la gramática, añadir elementos siguiendo las siguientes dos reglas:
 - Si X : αAβ, añadir a Siguiente ( A) los elementos de Primero (β) con la excepción de ε ( este símbolo nunca se incluirá en los conjuntos Siguiente).
 - Si X : αA, o bien X : αAβ donde Primero (β) contiene ε, añadir a Siguiente ( A) los elementos de Siguiente ( X).
**Ejemplo simple**
```
S : aBCd
B : bb
C : cc
```
Solución:
- Primero ( A) = {a}, Primero ( B) = {b}, Primero ( C) = {c}
- Siguiente ( S) = {$}
- Siguiente ( B) = Primero ( C) = {c}
- Siguiente ( C) = {d}
**Ejemplo**
```
E : T E' Primero ( E) = {(, id}
E' : + T E' | ε Primero ( E') = {+, ε}
T : F T' Primero ( T) = {(, id}
T' : * F T' | ε Primero ( T') = {*, ε}
F : ( E) | id Primero ( F) = {(, id}
```
Solución:
- Siguiente ( E) = {$} — regla 1
- Siguiente ( E) = {$, )} — ( 2.1) en F : ( E)
- Siguiente ( E') = Siguiente ( E) — ( 2.2)
- Siguiente ( T) = Primero ( E') + Siguiente ( E') − ( 2.1 y 2.2) = {+, $, )}
- Siguiente ( T') = Siguiente ( T) — ( 2.2)
- Siguiente ( F) = Primero ( T') + Siguiente ( T) + Siguiente ( T') − ( 2.1 y 2.2) = {*, +, $, )}
### Condiciones LL ( 1) ( recordatorio)
Para que a una gramática se le pueda aplicar el método LL ( 1) debe cumplir:
- No es recursiva por la izquierda. Si lo es, tenemos mecanismos para transformarla.
- Si existe un conjunto de reglas de la forma A : α1 | α2 | ... | αn se cumple que Primero (αi) ∩ Primero (αj) = {}, para todo i ≠ j.
- Como máximo un αi puede derivar en la cadena vacía ε.
- Si un no terminal αi ⇒* ε, entonces no hay otro αj que comience por un elemento que esté en Siguiente ( A): Primero (αj) ∩ Siguiente ( A) = ∅.
### Modificar gramáticas para LL ( 1)
Cuando se da alguno de estos casos hay que intentar:
- Eliminar la recursión por la izquierda.
- Sacar factor común por la izquierda.
**Recursión:**
```
A : Aα | bB
```
se transforma en:
```
A : bB A'
A' : α A' | ε
```
**Factor común:**
```
B : bc | bb | b
```
se transforma en:
```
B : b B'
B' : c | b | ε
```
### Construcción de la tabla de análisis
Reglas a repetir para toda producción A : α de la gramática:
1. Para cada terminal a ∈ Primero (α): agregar A→α a la tabla M[A, a].
2. Si ε ∈ Primero (α): agregar A→α a la tabla M[A, b] para cada terminal b ∈ Siguiente ( A).
3. Si ε ∈ Primero (α) y $ ∈ Siguiente ( A): agregar A→α a la tabla M[A, $].
Recordad:
- Cada entrada en blanco es un error.
- Si alguna entrada tiene más de una producción es porque la gramática no es LL ( 1).
### Ejemplo completo
1. Compruébese si la siguiente gramática es LL ( 1) y constrúyase la tabla, calculando todos los conjuntos Primero y Siguiente.
```
S : cA
A : aB
B : b | ε
```
2. Reconocer la cadena `cab` con el analizador construido.
**Comprobación LL ( 1):**
3. No es recursiva a izquierdas. ✔
4. B : b | ε:
 - 2.1 Primero ( b) ∩ Primero (ε) = ∅ ✔
 - 2.2 ε ∈ Primero ( B), pero Primero ( b) ∩ Siguiente ( B) = ∅ ✔
Conjuntos primero: Primero ( S) = {c}, Primero ( A) = {a}, Primero ( B) = {b, ε}.
Conjuntos siguiente: Siguiente ( S) = {$}, Siguiente ( A) = Siguiente ( S) = {$}, Siguiente ( B) = Siguiente ( A) = {$}.
**Tabla:**

| | c | a | b | $ |
|---|---|---|---|---|
| S | S→cA | | | |
| A | | A→aB | | |
| B | | | B→b | B→ε |
**Reconocer la cadena `cab`:**
```
S : cA, A : aB, B : b | ε
```

| Pila | Entrada | Acción |
|---|---|---|
| $S | cab$ | — |
| $Ac | cab$ | Reconocimiento |
| $A | ab$ | A : aB |
| $Ba | ab$ | Reconocimiento |
| $B | b$ | B : b |
| $b | b$ | Reconocimiento |
| $ | $ | Éxito |
## Lecturas
- Compiladores: Principios, técnicas y herramientas, 2ª Ed., A.V. Aho, Monica S. Lam, Ravi Sethi, Jeffrey D. Ullman, Addison Wesley, 2008. Leer el capítulo 4: Análisis Sintáctico.
- K.C. Louden, Construcción de compiladores: principios y práctica. Ed. Thomson, 2004. Leer el capítulo 4 y 5.
## Ejercicio ( 1)
1. Compruébese si la siguiente gramática es LL ( 1) y constrúyase la tabla, calculando todos los conjuntos Primero y Siguiente.
```
A : a B b
B : c d | c
```
2. Reconocer las siguientes cadenas con el analizador construido:
- acdb
- abdc
- acb
## Ejercicio ( 2)
1. Compruébese si la siguiente gramática es LL ( 1) y constrúyase la tabla, calculando todos los conjuntos Primero y Siguiente.
```
A : B C
B : D E
C : ε | z B C
D : y A x | v
E : w D E | ε
```
2. Reconocer las siguientes cadenas con el analizador construido:
- ywx
- v
- yvxwvzvw
