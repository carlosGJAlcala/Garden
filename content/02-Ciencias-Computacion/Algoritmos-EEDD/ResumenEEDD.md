---
title: "Resumeneedd"
date: 2026-01-26
tags:
  - ciencias-computacion
  - algoritmos-eedd
---

> **Relacionado**: [[00-Inicio/HOME|HOME]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

Negación: es lo contrario
!
![](media/image1.png){width="1.1354166666666667in"
height="1.1354166666666667in"}

[Conjunción:]{.underline} tiene que ser ambas verdad (y)

![](media/image2.png){width="1.8125in" height="1.84375in"}

[Disyunción:]{.underline} tiene que ser al menos una verdad (o)

![](media/image3.png){width="1.8020833333333333in"
height="1.8541666666666667in"}

[Implicación:]{.underline} no puede, cumplirse lo primero y no cumplirse
lo segundo (entonces)

![](media/image4.png){width="1.805715223097113in"
height="1.7280500874890639in"}Eq:
$\neg(p \land \neg q) \equiv \neg p \vee q$

[Bicondicional o doble implicación:]{.underline} tiene que ser ambas
iguales (sí y solo sí)

![](media/image5.png){width="1.9270833333333333in"
height="1.8645833333333333in"}Eq:
$(p \rightarrow q) \land (q \rightarrow p)$

[Disyunción excluyente:]{.underline} o una cosa o la otra, pero no ambas
(XOR)

![](media/image6.png){width="1.8541666666666667in"
height="1.8645833333333333in"}Eq: $\neg(p \leftrightarrow q)$

![](media/image7.jpeg){width="4.0in" height="8.229054024496937in"}

![](media/image8.png){width="3.928472222222222in" height="3.24375in"}

Nunca puede hacer una disyunción y una conjunción en el mismo nivel.
Nunca escribir $p \vee q \land r$. Hay que poner paréntesis.

Si en una expresión tenemos el mismo conector y están en el mismo nivel,
podemos eliminar los paréntesis, quedando $p \vee q \vee r$.

Una **tautología** es una expresión que siempre va a ser cierta (1) con
cualquier valor de las proposiciones. Lo contrario es una
**contradicción**.

Si una doble implicación $(p \leftrightarrow q)$ es una tautología
entonces p y q son **lógicamente equivalentes** (tienen los mismos
valores haciendo la tabla de verdad).

*p solo si q*: $p \rightarrow q$

*p si es q*: $q \rightarrow p$

Si por reglas de inferencia no llegamos a una conclusión, hay que
demostrarlo tomando las premisas como valor 1 y la conclusión como 0.

El **método de refutación por resolución** consiste en pasar todo a FNC
y añadir la conclusión negada como tesis, si se llega clausula vacía (0)
entonces es una tautología (las tesis anteriores son ciertas).

Estudiar la **satisfactibilidad** consiste en encontrar la combinación
de valores para que la fórmula total sea cierta (o no).

En las matrices de adyacencia si la diagonal principal es 0, significa
que **no hay bucles** (es un grafo simple).

En las matrices de adyacencia **simétricas** significan que es un grafo
no dirigido.

![](media/image9.png){width="1.4034722222222222in"
height="0.6666666666666666in"}Es un **grafo completo** si contiene una
arista para cada vértice. Siendo *E* el número de aristas y *n* el
número de vértices: $|E| = \frac{n(n - 1)}{2}$

![](media/image10.png){width="0.9166666666666666in"
height="0.46944444444444444in"}**Grafo bipartido completo**

Dos **grafos son isomorfos** son dos grafos iguales, pero de distinta
forma. Tienen que tener el mismo número de vértices y aristas. Se
comprueba etiquetando los vértices y comparándolos con el número de
grado.

![](media/image11.png){width="2.3229166666666665in"
height="1.1145833333333333in"}

Un **grafo es conexo** si se puede crear un árbol generador a partir de
éste. Aplicar Dijkstra con peso 1.

Los grafos tienen $|E| = 2|V|$

Los árboles tienen $|E| = |V| - 1$

**Búsqueda en profundidad (BEP).**

![](media/image12.png){width="3.3881944444444443in" height="1.13125in"}

**Búsqueda en anchura (BEA).**

![](media/image13.png){width="3.3881944444444443in"
height="1.1368055555555556in"}

El algoritmo de **PRIM** genera un grafo mínimo. Se elige la arista de
menor peso y después se van añadiendo las aristas de menor peso
incidentes a las que ya tenía sin formar bucles. **Kruscal** no necesita
que sea incidentes a las que ya tenía.

![](media/image14.png){width="3.3881944444444443in"
height="1.1465277777777778in"}

Un **grafo es plano** si se puede representar sin que haya aristas que
se crucen. $|V| - |E| + |R| = 2$

Si es simple y convexo y no cumple $e \leq 3v - 6$ y $2e \geq 3r$
entonces ya sabemos que no es plano. Y si además no tiene ciclos de
longitud 3 y no cumple $e \leq 2v - 4$ entonces sabemos que no es plano.
Si se cumpliese las propiedades no verificarían que fuese un grafo
plano.

**Teorema de Kuratowski** afirma que un grafo es plano si, y solo si, no
contiene ningún grafo homeomorfo K5, K3,3.

La **coloración de grafos** se realiza empezando a colorear por el nodo
de mayor grado. El algoritmo no garantiza que el valor sea mínimo, para
ver si es mínimo basta con comprobar si hay un ciclo de ese valor. Si el
número cromático es 2, entonces es un grafo bipartido.

Una aplicación es **inyectiva** si dos elementos distintos del dominio
no tienen la misma imagen. Cada imagen no puede tener más de un dominio.

Una aplicación es **sobreyectiva** si no quedan elementos de la imagen
sin asociarse. Cada imagen tiene un dominio.

Una aplicación es **biyectiva** si es inyectiva y sobreyectiva. Relación
perfecta.

Contar es establecer una aplicación biyectiva.

Reordenar *x* de un conjunto *y.* Hacer una inyección del conjunto *x*
con el conjunto *y*:

> $\frac{y!}{(y - x)!}$

Reordenar un conjunto *x.* Hacer una biyección entre un conjunto *x* y
otro *y*:

> $x!$

Si *x* elementos tienen que ir juntos, basta con reordenar dicho
conjunto de elementos, y tratar dicho conjunto como un único elemento.
Ej: Si en principio hay 30 elementos, y dos tienen que ir juntos, sólo
se va a tener 28 elementos restantes.

Escoger un conjunto *x* de un conjunto *y:*

$\frac{y!}{x!\ (y - x)!} = binomial(y,\ x)$

Reordenar un conjunto *x* que puede repetirse en otro conjunto *y.*
Aplicación sobreyectiva: $x^{y}$

Cuantas soluciones tiene la ecuación:

$x_{1} + x_{2} + x_{3} = 11$ $binomial(11 + 3 - 1,\ \ 11)$

Reordenar las letras de PATATA:

$$binomial(6,\ 3)*binomial(3,\ 2)*binomial(1,\ 1)$$

Hay 6 N y 7 C. No puede haber dos N juntas:

\_ N \_ N \_ N \_ N \_ N \_ N \_

$$(binomial(7,\ 2) + binomial(7,\ 1))*7!*6!$$

Hay 10 mujeres y 5 hombres. No puede haber dos hombres juntos:

$$binomial(11,\ 5)*10!*5!$$

Hay 3 conferenciantes y 3 presentadores. No se pueden sentar juntos ni
conferenciantes ni presentadores:

$$2*3!*3!$$

Formas de distribuir seis juguetes entre tres niños, de tal forma que
cada niño reciba al menos un juguete.

![](media/image15.png){width="3.3881944444444443in"
height="0.7541666666666667in"}
