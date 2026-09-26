---
title: "Análisis léxico"
---

# Análisis Léxico
## Contenidos
- Objetivos y contexto
- Introducción a los Analizadores Léxicos
- Elementos del Analizador Léxico
- Especificación de Componentes Léxicos
- Expresiones Regulares
- Autómatas Finitos
- Construcción de un Analizador Léxico
- Lecturas recomendadas
## Objetivos
¿Qué vamos a ver en este tema?
- Describir un analizador léxico
- Entender su estructura, organización y funcionamiento general
- Formalismos de especificación léxica
- Expresiones regulares
- Autómatas finitos
- Errores léxicos
- Principios para la construcción de un analizador léxico
## Introducción a los Analizadores Léxicos
### ¿Qué es un analizador léxico?
Un analizador léxico ( también scanner) es un programa capaz de tomar el texto fuente y, a partir de correspondencias con patrones, generar una secuencia de tokens ( componentes léxicos) a los que asocia, si procede, una serie de atributos.
### Conceptos básicos
- *Token** ( o componente léxico): secuencia de caracteres con significado sintáctico propio.
- *Lexema**: secuencia de caracteres cuya estructura se corresponde con el patrón de un token.
- *Patrón**: regla que describe los lexemas correspondientes a un token.

| Componente Léxico | Ejemplo de Lexema | Descripción del patrón        | Observaciones     |
| ----------------- | ----------------- | ----------------------------- | ----------------- |
| Identificador     | x, y, aux, x2     | `<letra>(<letra>\|<dígito>)*` | Identificadores   |
| Cadena            | "cadena"          | Caracteres entre `"` y `"`    | Constantes cadena |
### Tareas del Analizador Léxico
- Reconocer los componentes léxicos del lenguaje.
- Eliminar espacios en blanco, tabulaciones, saltos de línea y de página y otros caracteres propios de la entrada.
- Eliminar comentarios.
- Reconocer los identificadores de variable, tipo, constante, etc. y, en general, almacenarlos en una tabla de símbolos.
- Gestionar los errores léxicos que se detecten, avisando de ellos y relacionando los errores con el lugar de aparición.
### Relación entre A. Léxico y A. Sintáctico
A menudo, el analizador léxico es una subrutina del analizador sintáctico. Hay varias razones para su independencia:
- Se simplifica el diseño del A. sintáctico.
- Se mejora la eficiencia del compilador, al contar con una entrada optimizada.
- Va en favor de la portabilidad, es decir, en ser independiente del alfabeto.
La comunicación entre ellos se hace a través del buffer intermedio y de la llamada a la subrutina.
## Elementos del Analizador Léxico
### Componentes Léxicos ( Tokens)
En la mayoría de los lenguajes de programación se consideran componentes léxicos ( o tokens):
- Palabras reservadas
- Operadores ( comparación, asignación, lógicos, aritméticos,..)
- Identificadores
- Constantes
- Signos de puntuación ( paréntesis, punto y coma,..)
- Marcas de comienzo y fin de bloque
Los delimitadores no se consideran, en general, tokens.
Cuando un patrón puede coincidir con más de un lexema es necesario conocer información adicional, que se almacena como atributo del token.
El análisis léxico es un análisis de los caracteres.
- Parte de éstos y, mediante patrones, reconoce los lexemas.
- Envía al A. sintáctico el componente léxico y sus atributos.
- Puede hacer tareas adicionales ( eliminar blancos, control de líneas).
- A veces lee caracteres adicionales para identificar un token.
### Atributos
Los identificadores tienen asociados como atributos el lugar de la tabla de símbolos en el que se encuentran: `<identificador, 32>`.
A veces, el analizador sintáctico es el único que trabaja con la tabla de símbolos; si ese es el caso, llevan asociado el propio lexema: `<identificador, x>`.
Los literales tienen asociados como atributos el propio lexema: `<literal-decimal, 3.4>`.
### Ejemplo de tokens con atributos
Para una sentencia como la siguiente: `IF x < 10 THEN x := x + y`
Se generaría una cadena de Tokens parecida a lo siguiente:
```
<if,-> <identificador, &ref1> <op-menor,-> <literal-entero, 10>
<then,-> <identificador, &ref1> <asignación,->
<identificador, &ref1> <op-suma,-> <identificador, &ref2>
```
Con ref1 y ref2 como referencias a la posición en la tabla de símbolos.
### Errores léxicos
El analizador léxico rechaza texto con caracteres ilegales ( no contemplados en el alfabeto) o combinaciones ilegales, como:
- "ñ", "ç", "é" ( caracteres que no pertenecen al alfabeto del lenguaje)
- "::", ";=" ( no coinciden con ningún patrón de los tokens posibles)
Es importante mostrar un mensaje de error claro y exacto:
- En vez de mostrar... "Error 124 / Falta declaración / Error en la línea 85 / Se ha producido un error"
- Sería mucho mejor... `int número1;` seguido de `^ERROR124: línea 85, columna 6, carácter no válido`
### Recuperación de errores léxicos
El analizador léxico puede tomar distintas acciones para detectar errores, recuperarse y continuar.
- Modo de pánico: eliminar caracteres hasta encontrar un carácter en el que se considera que podría empezar un lexema correcto.
- Distancia mínima de corrección de un error y recuperación "inteligente", llevando a cabo acciones como las siguientes:
 - Borrado de caracteres extraños
 - Insertado de caracteres faltantes
 - Reemplazo de caracteres incorrectos por otros correctos
 - Conmutación de posiciones de dos caracteres adyacentes
### En la práctica
Hasta aquí todo claro, pero...
- ¿Cómo se organiza la operación?
- ¿En qué principios se basa?
- ¿Cómo lo programamos?
Empecemos por el principio: ¿qué es una palabra, de qué está compuesta y cómo identificamos si es correcta o no?
## Especificación de Componentes Léxicos
### Conceptos Básicos
**Alfabeto**: conjunto finito y no vacío de símbolos.
- Σ1 = {0,1}
- Σ2 = {a,b,c}
- Σ3 = {<,>,%}
Hay que notar el uso de meta-símbolos ( corchetes, comas,..) para formular los alfabetos. El contexto debe dejar claro si son símbolos del alfabeto o si se trata de meta-símbolos.
Un alfabeto no puede tener ni cero ni infinitos símbolos.
**Palabra o cadena**: una secuencia finita de símbolos de un alfabeto es una palabra sobre dicho alfabeto.
- Σ1 : 0, 1, 00, 101010, 11111
- Σ2 : a, b, c, aaa, abcabc, ccbb
- Σ3 : <<<, <><>, <%>, %><%
Algunos apuntes:
- La palabra vacía ( la que no contiene ningún símbolo) se anota como ε.
- ε no pertenece a ningún alfabeto.
- La longitud de una palabra es el número de símbolos que contiene.
- Podemos operar sobre cadenas: concatenación, exponenciación, etc.
**Lenguaje**: conjunto de palabras válidas sobre un alfabeto.
Operaciones con lenguajes:
- Unión
- Concatenación
- Cerradura de Kleene ( Cierre *)
- Cerradura positiva ( Cierre +)
### Primer reto
El primero de nuestros retos, modesto pero crucial, es ser capaces de identificar si una entrada de un fichero de datos está formada por palabras válidas o no.
La herramienta más sencilla ( pero potente a la vez) para tal fin son las Expresiones Regulares.
## Expresiones Regulares
### Concepto
Una Expresión Regular no es más que una secuencia de caracteres que conforma un patrón de texto.
Componentes básicos:
- ε representa la cadena vacía.
- Cualquier carácter como `a` se representa a sí mismo.
- Iteración:
 - 0 o más : `a*`
 - 1 o más : `aa* ≡ a+`
 - 0 o 1 : `ε|a ≡ a?`
- Agrupación de símbolos:
 - Por clases: `a|b|c ≡ [abc]`. También `a|b|c|...|z ≡ [a-z]`.
 - Por subexpresiones: `( a|b|c)*`
### Ejemplos de Expresiones Regulares
- `0 ( 0|1)0*`: 010, 000, 010000, ...
- `a ( ab)+b*`: aab, aababb, aabbbbbb, ...
- `[1-9]?0`: 0, 10, 20, ..., 90
- `[a-zA-Z]`
- `[0-9]+`
- `[a-zA-Z]([a-zA-Z]|[0-9])*`
### Ejercicios de Expresiones Regulares
Generar las expresiones regulares que permitan saber si una cadena cumple que:
- Pertenece a una de las siguientes palabras reservadas: if, else, then, for, while.
 - `if|else|then|for|while`
- Es un número entero par.
 - `[0-9]*( 0|2|4|6|8)` — o bien: `(( 0|2|4|6|8)|[1-9][0-9]*( 0|2|4|6|8))`
- Es un número real.
 - `[0-9]+(.[0-9]+)?`
- Es una cadena de texto de un lenguaje de programación formada por letras y números.
 - `"[a-zA-Z0-9]+"`
- Secuencias binarias que no contienen dos ceros consecutivos.
 - `0?( 10|1)*`
- Es un teléfono móvil español.
 - `( 6|7)[0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]`
- Define un array como {1.1,3.33,2,9} con un número que puede ir desde cero hasta infinito en número de elementos.
 - `{([0−9]+(.[0−9]+)?(,[0−9]+(.[0−9]+)?)*)?}`
 - `{(([0−9]+(.[0−9]+)?,)*[0−9]+(.[0−9]+)?)?}`
 - `{real (.real)*|ε}`
### Definiciones Regulares
Por conveniencia, se puede etiquetar para construir estructuras más complejas:
```
Letra : [a-zA-Z]
Dígito : 0|1|2|3|4|5|6|7|8|9
Identificador : Letra ( Letra|Dígito)*
NúmeroReal : Dígito+(.Dígito+)?
Dígitos : Dígito+
Fracción : (.Dígitos)?
Exponente : ( E (+|-)? Dígitos)?
NúmeroReal : Dígitos Fracción Exponente
```
### Diagramas de transiciones
Las definiciones regulares permiten reutilización, composición y recursividad en su uso. Sin embargo, se complica la representación de las transiciones entre patrones; la alternativa son los Autómatas Finitos, que no son más que formalismos matemáticos para describir ciertos tipos de algoritmos y que, en análisis léxico, son útiles para mostrar lo que sucede a medida que se consumen caracteres de entrada.
## Autómatas Finitos
### Definición
Un Autómata Finito reconoce una cadena de entrada si, consumidos todos los caracteres de la misma, acaba en un estado final de aceptación. Puede ser determinista o no determinista.
En el caso de un Autómata Finito Determinista ( AFD), este es un conjunto AFD = ( T, Q, f, q, F) en el que:
- T es un alfabeto de símbolos terminales de entrada.
- Q es un conjunto de estados finito y no vacío.
- f: QxT : Q es una función de transición.
- q ∈ Q es un estado inicial.
- F ⊂ Q es un subconjunto de estados finales de aceptación.
Toda expresión regular puede reconocerse mediante un AFD y se emplean por la simplicidad relativa de su implementación.
### Representación gráfica
En general:
- Cada círculo representa un estado.
- Cada arista representa un carácter en la entrada.
- Doble círculo representa un estado de aceptación de un elemento léxico.
Ejemplo: autómata con estados q0 y q1, con transición 1 de q0 a q0, transición 0 de q0 a q1, transición 1 de q1 a q1 y transición 0 de q1 a q0.
¿Qué expresión regular acepta este autómata? Respuesta: secuencias binarias con un número par de ceros. O, si lo preferís, `( 1*) ( 0 ( 1*) 0 ( 1*))*`.
### Extensión de los AFD
Con el objetivo de simplificar, dentro de Teoría de Compiladores se utilizan las siguientes extensiones de la notación:
- No tiene estados de error ( se asume que si no existe la transición es un error).
- "Otro" significa cualquier carácter no asignado a una arista.
- Los estados finales paran el proceso y emiten token.
- Un asterisco representa un retroceso ( que se debe devolver un carácter).
- Se espera a reconocer el posible token del lexema más largo.
 - El estado final ya no es final.
 - Al llegar un carácter terminador se pasa a uno final.
 - Entonces se emite el token.
 - Si es necesario se puede marcar el estado final.
### Autómatas Finitos No Deterministas ( AFND)
La construcción sistemática de autómatas genera AFND. Un AFND es un Autómata Finito en el que cada estado:
- Posee al menos un estado q ∈ Q tal que, para un símbolo a ∈ Σ del alfabeto, existe más de una transición δ( q,a) posible.
- Puede tener varias transiciones con la misma etiqueta.
- Es decir, que en un AFND puede pasar:
 - Que existan transiciones del tipo δ( q,a)=q1 y δ( q,a)=q2 con q1≠q2.
 - Que existan transiciones del tipo δ( q,ε), siendo q un estado no final o bien un estado final con transiciones hacia otros estados.
Por ejemplo, este AFND reconoce la expresión regular `( a|b)*b+`: estados q0 y q1, con transiciones a,b desde q0 a q0, transición b de q0 a q1 y transición b de q1 a q1.
### Tabla de transiciones
Ejemplo de reconocimiento de números enteros:

| Estado | 0-9 | otro | Token | Retroceso |
|---|---|---|---|---|
| q0 | q1 | error | - | - |
| q1 | q1 | q2 | | |
| q2 ( final) | - | - | NumEntero | q1 |
## Construcción de un Analizador Léxico
### Tratamiento de palabras reservadas
Las palabras reservadas son aquellas que los lenguajes de programación reservan para usos particulares. El problema en su tratamiento es que:
- Pueden confundirse con identificadores
- Y comparten patrones
### Diferenciación
Las palabras reservadas se pueden diferenciar de los identificadores con dos aproximaciones:
- *Resolución explícita**: se indican todas las expresiones regulares de todas las palabras reservadas y se integran los diagramas de transiciones resultantes de sus especificaciones léxicas en la máquina reconocedora.
- *Resolución implícita**: se reconocen todas como identificadores, pero existe una tabla adicional de palabras reservadas que se consulta para comprobar si el lexema reconocido es un identificador o una palabra reservada.
#### Resolución explícita
Palabras clave como expresiones regulares: `[fF][oO][rR] : return ( TK_FOR)`
- Código más largo y complicado de leer.
- El autómata generado tiene muchos más estados.
- La ejecución es más lenta.
#### Resolución implícita
Las palabras clave se incluyen en una tabla y se verifica si el identificador encontrado es palabra clave.
```
if is_keyword ( text, kw) then
 return ( kw);
else
 return ( IDENTIFIER);
```
Serían, por lo tanto, casos particulares de identificador. Cuando se detecta uno:
- Se comprueba si es palabra clave.
- Si no, se trata de un identificador y hay que comprobar si ya está en la TS.
- Si no lo está, hay que darle de alta y retornar un token identificador.
### Construcción de un Analizador Léxico
Varias posibilidades:
- Usar generadores de analizadores léxicos. Es la forma más sencilla, pero también puede resultar poco eficiente.
- Escribir el analizador léxico en un lenguaje de alto nivel. Supone un mayor esfuerzo y es más propenso a errores, pero a cambio es más eficiente y sencillo de mantener.
- Escribir el analizador léxico en ensamblador. Solo en casos muy concretos por su alto coste y baja portabilidad.
### Proceso de implementación
- Definir las expresiones regulares del analizador léxico
- Identificar los tokens ( códigos y atributos)
- Construir los diagramas de transiciones ( AFD)
- Completar los autómatas con acciones semánticas
- Definir todos los posibles errores
- Implementar el AFD y las acciones semánticas usando switch o tablas de transiciones
### Generadores automáticos ( LEX)
- Reciben las especificaciones de las expresiones regulares de los patrones que representan los tokens del lenguaje y las acciones a tomar cuando los detecten.
- Generan los diagramas de transición de estados generalmente en código C, C++ o Java.
- Como ventaja, hacen más cómodo el desarrollo.
- Como desventaja, complican el mantenimiento del código y la eficiencia depende del generador.
En resumen, la tarea de un generador automático consiste en transformar las expresiones regulares y tokens definidos por el programador en un autómata finito, para luego implementarlo en un lenguaje de alto nivel.
### Generadores automáticos ( ejemplo JFLEX)
```
nl = [\n\r]+
ws = [ \t\b\015]+
number = [0-9]+
name = [a-zA-Z]+
dash = "-"
colon = ":"
%%
{nl} { /* do nothing */ }
{ws} { /* happy meal */ }
{name} { value = yytext (); return MiniParser.NAME; }
{dash} { return MiniParser.DASH; }
{colon} { return MiniParser.COLON; }
{number} {
 try {
 value = Integer.valueOf ( Integer.parseInt ( yytext ()));
 } catch ( NumberFormatException nfe) {
 // shouldn't happen
 throw new Error ();
 }
 return MiniParser.NUMBER;
}
```
## Lecturas recomendadas
- Compiladores: Principios, técnicas y herramientas, 2ª Ed., A.V. Aho, Monica S. Lam, Ravi Sethi, Jeffrey D. Ullman, Addison Wesley, 2008. Leer el capítulo 3: Análisis Léxico.
- K.C. Louden, Construcción de compiladores: principios y práctica. Ed. Thomson, 2004. Leer el capítulo 2: Rastreo o análisis léxico.
