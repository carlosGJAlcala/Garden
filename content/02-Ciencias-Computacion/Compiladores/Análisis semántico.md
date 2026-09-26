---
title: "Análisis semántico"
---

# Análisis semántico

## Contenidos
- Introducción
- Gramáticas de atributos
- Gramáticas S-atribuidas
- Gramáticas L-atribuidas
- Grafos de dependencias
- Esquemas de traducción
- Evaluación
## Introducción
### Pequeño recordatorio
- Análisis léxico: detecta entradas con tokens no permitidos.
- Análisis sintáctico: detecta entradas que no pueden representarse con un árbol derivado de las reglas gramaticales.
- Análisis semántico: detecta el resto de posibles errores y define la semántica del lenguaje para su interpretación.
El análisis semántico es el punto final de la etapa de front-end.
### Funciones principales
La fase de Análisis Semántico no se realiza claramente diferenciada del resto de tareas del compilador.
1. Obtiene información necesaria para la compilación tras conocer la estructura sintáctica.
2. Completa las fases de análisis incorporando comprobaciones que van más allá del reconocimiento de cadenas y estructuras.
3. Identifica tipos de instrucción y componentes.
4. Completa la tabla de símbolos.
5. Realiza comprobaciones estáticas: se realizan durante la compilación del programa, como comprobación de tipos o etiquetas/identificadores.
6. Realiza comprobaciones dinámicas: se incorporan al programa traducido y hacen referencia a aspectos que solo pueden ser conocidos en tiempo de ejecución y que, por lo tanto, son dependientes del estado de la máquina en la ejecución.
7. Valida las declaraciones de identificadores.
### Categorías de comprobaciones
Las comprobaciones semánticas se pueden dividir en dos categorías:
- Análisis de la exactitud del programa: trata de garantizar una ejecución adecuada; si no se hace ahora, la máquina no lo hará ( por ejemplo, sumar un entero con un string es igual, a bajo nivel, donde todo son dígitos binarios).
 - Algunos lenguajes ( Lisp, Smalltalk) pueden no tener análisis estático.
 - Otros ( ADA, por ejemplo) imponen fuertes restricciones para que un programa sea ejecutable.
- Análisis para mejorar la eficiencia ( optimización del programa traducido).
 - Es ineficiente, por ejemplo, declarar una variable y no usarla.
 - Otras comprobaciones: condiciones que no siempre se evalúan a true ( o a false), sentencias insustanciales o sin efecto, etc.
### Especificación de la Semántica
No existe una notación estándar para especificar la semántica estática de un lenguaje; el análisis semántico varía mucho de unos lenguajes a otros.
Las especificaciones semánticas de un lenguaje pueden hacerse de manera informal o formal:
- Especificación Natural: basada en el lenguaje natural. Por ejemplo: "los identificadores deben definirse antes de utilizarse", "los operandos deben ser compatibles entre sí".
- Especificación Formal: definición más precisa. Lenguajes formales: Z, B, VDM, etc. Gramáticas de atributos ( Knuth, 1968).
## Gramáticas de atributos
Una Gramática de Atributos es una GLC...
- ... cuyos símbolos pueden tener asociados atributos.
- ... cuyas producciones pueden tener asociadas reglas de evaluación de atributos.
- En la creación de compiladores se utilizan ecuaciones de atributos o reglas semánticas como método para expresar la relación entre el cálculo de los atributos y las reglas del lenguaje.
- Cada producción ( regla sintáctica) tiene asociada una acción semántica que se aplica cuando se realiza una reducción en el análisis sintáctico ascendente.
No hay una notación estándar para especificar la semántica estática de un lenguaje: el análisis semántico varía mucho de unos lenguajes a otros.
La forma más sencilla de hacer que el compilador sepa interpretar cada posible código fuente es asociar a cada posible construcción gramatical ciertas reglas que permitan traducirla en términos computables, y solo es posible si se cumple el principio de Traducción Dirigida por la Sintaxis.
**Traducción dirigida por la sintaxis**: el significado de una construcción de un lenguaje está directamente relacionado con su estructura sintáctica según se representa en su árbol de análisis.
Ejemplos de traducción dirigida por la sintaxis:

| Tipo de declaración | Construcción sintáctica | Traducción semántica |
|---|---|---|
| Declaración de constantes | `CONST MAX = 100;` | Registrar 'MAX' como constante entera de valor 100 |
| Declaración de tipos | `TYPE TVector = ARRAY [1..MAX] OF INTEGER;` | Registrar 'Tvector' como tipo ARRAY de tamaño 100 y base INTEGER |
| Declaración de variables | `VAR v : TVector;` | Comprobar que 'Tvector' existe como un tipo y registrar 'v' como una variable de ese tipo |
| Declaración de procedimientos | `PROCEDURE Sort ( VAR v : TVector);` | Registrar 'Sort' como un procedimiento del ámbito en curso indicando la lista de tipos de los parámetros. Crear un nuevo ámbito y registrar en él 'v' como variable de tipo 'Tvector' |
### Atributos
**Atributo**: propiedad de una construcción de un lenguaje de programación.
- Pueden variar mucho en cuanto a información que contienen o tiempo que tardan en determinarse durante la traducción/ejecución.
- Cada símbolo ( terminal o no terminal) puede tener asociado un número finito de atributos.
- Ejemplos de atributos: tipo de una variable, valor de una expresión, ubicación en memoria, código objeto de un procedimiento, número de dígitos significativos en un número.
**Fijación de un atributo**: proceso de calcular el valor de un atributo y asociarlo con una construcción del lenguaje.
- Tipos de atributo por su fijación:
 - Estático: puede fijarse antes de la ejecución del programa ( por ejemplo, número de dígitos significativos).
 - Dinámico: solo puede fijarse durante la ejecución del programa ( por ejemplo, valor de una expresión no constante).
- Los valores de los atributos deben estar asociados con un dominio de valores.
Se denotan habitualmente mediante un nombre precedido por un punto y el nombre del símbolo al que están asociados: `NombreSimbolo.NombreAtributo`.
Ejemplo:
```
numero : numero digito
numero.valor = numero_0.valor * 10 + digito.valor
numero : digito
numero.valor = digito.valor
```
Otra notación referencia la posición del símbolo en la producción:
- `$$` representa el no-terminal en la parte izquierda de la producción.
- Los símbolos de la parte derecha de la producción se identifican consecutivamente: `$1, $2, $3... $n`.
Ejemplo:
```
numero : digito
$$.valor = $1.valor
numero : numero digito
$$.valor = $1.valor * 10 + $2.valor
```
### Ejemplo 1
```
Exp : Exp op_arit Exp {
 si ($1.tipo == $3.tipo) entonces
 $$.tipo = $1.tipo
 si no
 $$.tipo = ERROR
 Escribir ("error tipos incompatibles")
 fin si
}
```
### Ejemplo 2
```
<EXPRESION> ::= <EXPRESION> <OPERADOR> <EXPRESION> {
 <OPERADOR>.tipo = mayor_tipo (<EXPRESION>1.tipo, <EXPRESION>2.tipo)
 <EXPRESION>0.tipo = <OPERADOR>.tipo
 if (<OPERADOR>.tipo == 'F' && <EXPRESION>1.tipo == 'I') {
 <EXPRESION>1.tipo = 'F';
 <EXPRESION>1.valor = FLOAT (<EXPRESION>1.valor);
 }
 if (<OPERADOR>.tipo == 'F' && <EXPRESION>2.tipo == 'I') {
 <EXPRESION>2.tipo = 'F';
 <EXPRESION>2.valor = FLOAT (<EXPRESION>2.valor);
 }
 switch (<OPERADOR>.tipo) {
 case 'I': <EXPRESION>0.valor = op_entera (<OPERADOR>.clase, <EXPRESION>1.valor, <EXPRESION>2.valor); break;
 case 'F': <EXPRESION>0.valor = op_real (<OPERADOR>.clase, <EXPRESION>1.valor, <EXPRESION>2.valor); break;
 }
}
```
### Gramáticas de atributos - Tabla
Las gramáticas de atributos se escriben en forma de tabla:
| Regla gramatical | Regla semántica |
|---|---|
| L : E n | print ( E.val) |
| E : E + T | E₀.val = E₁.val + T.val |
| E : T | E.val = T.val |
| T : T * F | T₀.val = T₁.val * F.val |
| T : F | T.val = F.val |
| F : ( E) | F.val = E.val |
| F : digito | F.val = digito.valor_lexico |
### Definiciones dirigidas por la sintaxis
Generalización de una gramática en la que cada símbolo gramatical tiene asociado un conjunto de atributos. El valor de un atributo en un árbol sintáctico se calcula mediante una regla semántica asociada a la producción utilizada en el nodo.
Tipos de atributos:
- *Sintetizados**: su valor se calcula en función de atributos de nodos hijos en el árbol de análisis sintáctico.
 `A : aB { A.atributo = a.atributo + B.atributo }`
- *Heredados**: para un hijo se calculan a partir de los atributos del padre y hermanos en el árbol de análisis.
 `A : aB { B.atributo = a.atributo − A.atributo }`
Tienen la siguiente forma:
1. Cada producción A : α tiene una o más reglas semánticas asociadas.
2. Cada regla tiene la forma `b = f ( c1, c2, ..., cn)`.
3. `b`, que depende de `c1, c2, ..., cn`, puede ser:
 4. Un atributo sintetizado de A.
 5. Un atributo heredado de uno de los símbolos del lado derecho de la producción.
6. Las funciones f de las reglas se escriben como expresiones.
- Las reglas semánticas establecen las dependencias entre los atributos, que se pueden representar en un grafo.
- Del grafo de dependencias se obtiene el orden de evaluación de las reglas semánticas.
**Árbol sintáctico con anotaciones**: árbol sintáctico que muestra información en cada nodo sobre los atributos.
## Gramáticas S-atribuidas
**Gramática S-atribuida**: todos los atributos asociados con los símbolos gramaticales son sintetizados.
**Evaluación**: las reglas de evaluación de los atributos sintetizados se realizan cuando se aplican reducciones en el análisis sintáctico.
Requisitos para la evaluación:
- Las reglas de evaluación de los atributos deben definirse en función de los atributos asociados con los símbolos gramaticales a su derecha.
- Se realiza un análisis ascendente.
### Gramáticas S-atribuidas - Ejemplo
Calculadora aritmética sencilla, donde se desea evaluar expresiones a la vez que las analizamos.
```
L : E n { print ( E.val) } (* n = salto de línea *)
E : E + T { E0.val = E1.val + T.val }
E : T { E.val = T.val }
T : T * F { T0.val = T1.val * F.val }
T : F { T.val = F.val }
F : ( E) { F.val = E.val }
F : digito { F.val = digito }
```
Evaluación de la expresión `2 * 3 + 4`. Resultado: se imprime el resultado de la expresión ( 10).
## Gramáticas L-atribuidas
**Gramática L-atribuida**: los atributos asociados son sintetizados o heredados; su evaluación depende de los atributos asociados con los símbolos precedentes en la derivación.
- Heredan del nodo "padre": `A : XYZ { Y.valor = A.valor }`
- Heredan de hermanos a su "izquierda": `A : XYZ { Y.valor = X.valor }`
- Heredan de otros atributos del mismo símbolo: `A : XYZ { Y.valor = float ( Y.intvalue) * 2 }`
Los atributos Heredados permiten expresar la dependencia de una construcción del lenguaje con respecto al contexto en que aparece. Ejemplos:
- Saber si un identificador está en la parte izquierda ( dirección) o derecha ( valor) de una expresión.
- Conocer la posición de un argumento de función `f ( x,y,z)`: "¿qué posición ocupa dentro de la lista de argumentos el argumento y?".
Requisitos para la evaluación: el análisis óptimo es el descendente.
### Gramáticas L-atribuidas - Ejemplo
```
D -> T L { L.her = T.tipo; }
T -> int { T.tipo = entero; }
T -> real { T.tipo = real; }
L -> L, id { L1.her = L0.her; anadetipo ( id, L0.her); }
L -> id { anadetipo ( id, L.her); }
```
Evaluar la expresión `real id1, id2, id3`.
## Grafo de dependencias
El grafo de dependencias es un grafo dirigido acíclico con:
- Un nodo para cada atributo.
- Un arco b : c si el atributo c depende del atributo b.
Se construye de la siguiente forma:
- Para cada nodo n del árbol sintáctico, hacer:
 - Para cada atributo a asociado al símbolo gramatical del nodo n, construir un nodo etiquetado con a en el grafo de dependencias.
 - Para cada regla semántica `b = f ( c1, c2, ..., cn)` asociada con la producción del nodo n, trazar arcos desde cada ci hasta b.
- Los atributos sintetizados se representan marcando el nodo con un punto gordo.
- El árbol sintáctico se representa en paralelo mediante líneas punteadas.
Para calcular el valor de un atributo es necesario calcular en primer lugar los valores de los atributos de los que depende, estableciendo una dependencia entre atributos. Cuando aparecen definidos atributos sintetizados y heredados, es necesario establecer un orden de evaluación: para cualquier acción semántica de la forma `X.atr = f ( Y1.atr, ..., Yn.atr)`, los valores de los atributos `Y1.atr, ..., Yn.atr` deben estar disponibles antes de ejecutarla.
Ejemplos:
```
E : E + E { E0.val = E1.val + E2.val }
```
```
D -> T L { L.her = T.tipo; }
T -> int { T.tipo = entero; }
T -> real { T.tipo = real; }
L -> L, id { L1.her = L0.her; anadetipo ( id, L0.her); }
L -> id { anadetipo ( id, L.her); }
```
Evaluar la expresión `real id1, id2, id3`.
## Esquemas de traducción
Gramática con atributos cuyas acciones semánticas se expresan entre llaves. Estas acciones se encuentran bien intercaladas entre los símbolos de la parte derecha de las producciones, o bien al final de las mismas.
```
S ::= B1 B2 { B1.atr = 1; B2.atr = 2; }
B ::= x { print ( B.atr); }
Proced ::= procedure { CrearAmbito (); } id Args Decl Sentencias;
```
## Evaluación
### Evaluación ascendente
- Los principales métodos de análisis sintáctico procesan la entrada de izquierda a derecha, lo que implica que los atributos no pueden tener dependencias "hacia atrás" ( este problema se plantearía solo para atributos heredados).
- Los analizadores ascendentes ( LR) son más adecuados para manejar atributos sintetizados ( reducen cuando se conoce toda la parte derecha de una producción).
- Es posible implementar traductores ascendentes para atributos heredados utilizando técnicas avanzadas.
- El cálculo de los atributos depende de la estructura de la gramática.
- Es posible simplificar el cálculo mediante una modificación de las reglas gramaticales.
**Teorema de Knuth**: dada una gramática con atributos, todos los atributos heredados se pueden convertir en sintetizados modificando adecuadamente la gramática, sin cambiar el lenguaje. En la práctica no se utiliza demasiado, pues puede generar gramáticas y reglas semánticas más complejas que las originales.
¿Qué cambia en el análisis visto hasta ahora?
- La estructura de la pila se adecua para que cada símbolo de la gramática disponga de sus atributos asociados.
- La evaluación de los atributos se realiza justo antes de cada reducción.
- El analizador LR contiene una pila de valores adicional para almacenar los valores de los atributos sintetizados ( si hay más de un atributo para un símbolo, se almacenan como estructuras).
- El analizador es similar, pero ahora utiliza producciones compuestas por símbolos más acciones semánticas: al aplicar una reducción se realizan los cálculos indicados en las acciones semánticas, utilizando generalmente los elementos de la pila de valores.
- Un desplazamiento consiste en la inserción de valores de token tanto en la pila de valores como en la pila de análisis sintáctico.
### Ejemplo - Contar en binario
Supongamos que tenemos la siguiente gramática, que genera cadenas binarias. ¿Cómo contaríamos el número de unos de la cadena mediante acciones semánticas?
```
N : L { N.c = L.c }
L : L B { L0.c = L1.c + B.c }
L : B { L.c = B.c }
B : 0 { B.c = 0 }
B : 1 { B.c = 1 }
```
### Ejemplo - Valor en binario
Supongamos que tenemos la siguiente gramática, que genera cadenas binarias. ¿Cómo obtendríamos el número decimal que representa la cadena mediante acciones semánticas?
```
N : L { N.val = L.val }
L : L B { L0.val = L1.val*2 + B.val }
L : B { L.val = B.val }
B : 0 { B.val = 0 }
B : 1 { B.val = 1 }
```
### Ejemplo completo
Supongamos que tenemos la siguiente gramática, que genera cadenas de x, y, z, junto a sus acciones semánticas:
```
S : x x W { printf ( 1); }
S : y { printf ( 2); }
W : S z { printf ( 3); }
```
¿Qué resultado obtendremos por pantalla si reconocemos con un ASA del tipo LALR ( 1) la cadena `xxxxyzz`?
**Paso 1**: gramática y cadena de entrada `xxxxyzz` a reconocer.
**Paso 2**: tabla de análisis LALR ( 1) construida a partir de la gramática.

| Estado | x   | y   | z   | $   | GoTo S | GoTo W |
| ------ | --- | --- | --- | --- | ------ | ------ |
| I0     | S2  | S3  |     |     | 1      |        |
| I1     |     |     |     | ✓   |        |        |
| I2     | S2  | S3  |     |     |        |        |
| I3     |     |     | r2  | r2  |        |        |
| I4     | S2  | S3  |     |     | 6      | 5      |
| I5     |     |     |     | r1  |        |        |
| I6     |     |     | S7  |     |        |        |
| I7     |     |     |     | r3  |        |        |
**Paso 3**: rastro del análisis de `xxxxyzz`.

| Paso | Pila sintáctica | Entrada | Acción | Pila valores | Acción semántica |
|---|---|---|---|---|---|
| 1 | 0 | xxxxyzz$ | s2 | $ | |
| 2 | 0x2 | xxxyzz$ | s4 | $ | |
| 3 | 0x2x4 | xxyzz$ | s2 | $ | |
| 4 | 0x2x4x2 | xyzz$ | s4 | $ | |
| 5 | 0x2x4x2x4 | yzz$ | s3 | $ | |
| 6 | 0x2x4x2x4y3 | zz$ | r2 | $2 | printf ( 2); |
| 7 | 0x2x4x2x4S | zz$ | 6 | $2 | |
| 8 | 0x2x4x2x4S6 | zz$ | s7 | $2 | |
| 9 | 0x2x4x2x4S6z7 | z$ | r3 | $23 | printf ( 3); |
| 10 | 0x2x4x2x4W | z$ | 5 | $23 | |
| 11 | 0x2x4x2x4W5 | z$ | r1 | $231 | printf ( 1); |
| 12 | 0x2x4S | z$ | 6 | $231 | |
| 13 | 0x2x4S6 | z$ | s7 | $231 | |
| 14 | 0x2x4S6z7 | $ | r3 | $2313 | printf ( 3); |
| 15 | 0x2x4W | $ | 5 | $2313 | |
| 16 | 0x2x4W5 | $ | r1 | $23131 | printf ( 1); |
| 17 | 0S | $ | 1 | $23131 | |
| 18 | 0S1 | $ | acc | $23131 | |
## Lecturas
- Compiladores: Principios, técnicas y herramientas, 2ª Ed., A.V. Aho, Monica S. Lam, Ravi Sethi, Jeffrey D. Ullman, Addison Wesley, 2008. Leer el capítulo 5 y 6.
- K.C. Louden, Construcción de compiladores: principios y práctica. Ed. Thomson, 2004. Leer el capítulo 6.
