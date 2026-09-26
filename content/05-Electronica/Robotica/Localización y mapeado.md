---
title: "Localización y mapeado"
tags: [universidad, 4anyo, robots]
date: 2026-08-12
lang: es
---
# T1.LocalizacionMapeado 19 20

Grado en Ingeniería Informática
Grado en Ingeniería de Computadores
Grado en Ingeniería en Sistemas de la Información
Grado en Sistemas de la Información
Sistemas de Control para Robots
Tema 1. Localización y mapeado
Elena López Guillén
Manuel Ocaña Miguel
Rafael Barea Navarro
Índice del Tema

## 1. mapeado: representaciones métricas y topológicas

1. Mapeado: representaciones métricas y topológicas

## 2. sistemas de localización: local y global

2. Sistemas de localización: local y global

## 3. introducción al problema del slam ( localización y mapead

3. Introducción al problema del SLAM ( localización y mapeado simultáneos)

## 4. localización y mapeado mediante estimación bayesiana

4. Localización y mapeado mediante estimación bayesiana

## 1. generalidades

1. Generalidades

## 2. estimación de estados probabilística ( bayesiana)

2. Estimación de estados probabilística ( bayesiana)

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Práctica 1:
 Mapeado
 Localización
Sistemas de Control para Robots 2

## 1. mapeado: representaciones

1. Mapeado: representaciones
métricas y topológicas
Elección del método de representación
Elección del método de representación, depende de:

 La aplicación en cada caso
 Las características observables
 La carga computacional
Tipos de representaciones:

 Continuas: precisión, gran carga computacional
 Discretas: simplificación
Sistemas de Control para Robots 4
Representación continua
 MAPAS GEOMÉTRICOS basados en la arquitectura del
edificio
 Representación con un conjunto de líneas infinitas
 Requieren una carga computacional elevada
Grado en Ingeniería Sdies tCeommaps udtea dCoornetsr o–l Spiasrtae mRoabs odtes Control para Robots 5
Representaciones discretas ( I)
Descomposición en CELDAS EXACTAS
1.
 Busca cubrir el espacio no ocupado mediante teselas o
polígonos
 No es importante la posición que ocupa el robot en el área
libre sino la capacidad para pasar de una a otra
 Se almacenan las relaciones entre las diferentes áreas
( diagramas de conectividad)
Sistemas de Control para Robots 6
Representaciones discretas ( II)
Descomposición en CELDAS FIJAS
2.
 Descompone en celdas fijas con dos posibles valores:
ocupada (“1”) y libre (“0”)
 También es posible añadir valor desconocido
 Problema: desaparecen los pasos estrechos
Sistemas de Control para Robots 7
Representaciones discretas ( III)
Descomposición ADAPTATIVA en celdas de tamaño
3.
variable
 Resuelve el problema de los pasos estrechos
 Se parte de un tamaño fijo que se mantiene en zonas libres
 Si queda una zona
ocupada en la
celda se divide en
cuatro y así sucesi-
vamente hasta una
resolución máxima
determinada
Sistemas de Control para Robots 8
Representaciones discretas ( IV)
REJILLAS DE OCUPACIÓN utilizando celdas de un
4.
tamaño mínimo
 A cada celda se le asigna un contador. El contador se incrementa con
cada impacto de los sensores de distancia y se decrementa con un
impacto en una celda que quedaba oculta tras ella.
 Se utilizan normalmente con sensores de distancia láser
 Problema: los mapas crecen a medida que lo hace el entorno
Courtesy of S. Thrun
Sistemas de Control para Robots 9
Representaciones discretas ( V)

## representación topológica

REPRESENTACIÓN TOPOLÓGICA
5.
 Evitan las medidas geométricas del entorno.
 Se concentran en características relevantes del entorno
que son útiles para los objetivos del robot móvil.
~ 400 m
~ 1 km
~ 200 m
~ 50 m
~ 10 m
Sistemas de Control para Robots 10
Representaciones discretas ( VII)
 Elementos de la
representación topológica:
 Nodos y Arcos
nodo
 Nodos: se utilizan para denotar
áreas de interés
 Arcos: se utilizan para indicar la
adyacencia de dos nodos.
 Cuando un arco conecta dos
arco
nodos, indica que se puede
( conexión)
pasar de un nodo a otro sin
necesidad de atravesar otro
nodo
 En la representación topológica
los nodos no tienen por qué
estar separados un tamaño fijo
como en la discretización
basada en celdas
Sistemas de Control para Robots 11
Representaciones discretas ( VI)
 Ejemplo de representación topológica
Sistemas de Control para Robots 12
Construcción de los mapas
 ¿Quién construye los mapas?

## 1. a mano 2. automáticamente:

1. A mano 2. Automáticamente:
El robot aprende su entorno ( mapeado)
Motivación:
 A mano: duro y costoso
123.5
 El entorno cambia dinámicamente
Sistemas de Control para Robots 13
Construcción de los mapas
 Retos

## 2. representación y reducción de la

2. Representación y Reducción de la

## 1. mantenimiento del mapa: mantener

1. Mantenimiento del Mapa: mantener
Incertidumbre
la consistencia del mapa ante
cambios
posición del robot -> posición del muro
p.e. desaparición
de columna
?
posición del muro-> posición del robot
 Densidad de probabilidad sobre las
posiciones de las características
- p.e. medida de creencia de cada una de  Estrategias de exploración adicionales
las características del entorno
Sistemas de Control para Robots 14

## 2. sistemas de localización: local y

2. Sistemas de localización: local y
global
Localización local y global ( I)
Localización: proceso por el cual el robot obtiene su

posición dentro del entorno en el que se mueve. Se
clasifica como:
 Local: se proporciona al robot la posición inicial de la que
parte ( p.e. odometría)
 Global: no es necesario proporcionar información sobre su
posición en el comienzo de la navegación ( p.e. GPS, WiFi)
Clasificación (¿quién realiza la localización?):

 Entorno inteligente: es el entorno el que realiza la
localización
?
 Propio robot realiza la localización
Sistemas de Control para Robots 16
Localización local y global ( II)
El proceso de la localización es iterativo:

position
Position Update
( Estimation?)
Prediction of
Encoder matched
Position
observations
( e.g. odometry)
YES
predicted position
Map
Matching
data base
raw sensor data or
extracted features
n
no
ot i
ip Observation
t
pe
ec
cr
re
eP
P
Sistemas de Control para Robots 17
Localización local y global ( III)
La localización se puede llevar a cabo mediante

diversas técnicas que se clasifican como:
 Determinísticas: basadas en marcas, balizas, camino,
( odometría, dead-reckoning)
 Probabilísticas: filtros de Kalman, procesos de Markov
?
Sistemas de Control para Robots 18
Localización basada en marcas ( I)
Se utilizan marcas ( artificiales o naturales) en el

entorno:
 Entre marca y marca sólo se utiliza la fase de predicción
 Cuando se detecta una marca, se utilizan sus propiedades
geométricas para corregir la posición
Sistemas de Control para Robots 19
Localización basada en marcas ( II)
Ejemplo: MDARS

Sistemas de Control para Robots 20
Localización basada en balizas ( I)
Se utilizan las posiciones

conocidas de diferentes
balizas en el entorno
para obtener la posición
mediante, por ejemplo,
el algoritmo de
triangulación o
trilateración
Sistemas de Control para Robots 21
Localización basada en el camino
| Algunos | | | sistemas | | | | utilizan | | | estrategias | | | | de | localización | | |
| ------- | --- | --- | -------- | --- | --- | --- | -------- | --- | --- | ----------- | --- | --- | --- | --- | ------------ | --- | --- |

| basadas | | | en | el | camino | | | que | | debe | | seguir | | el | robot. | | |
| ------- | -------------- | ------ | ---- | ---------- | -------------- | ------- | ------------ | -------- | ----- | ------- | ------ | ------- | ------------ | --- | ---------- | -------- | ---- |
|  | En | | este | | caso | | la | ruta | | a | seguir | | por | | el | robot | está |
| | explícitamente | | | | | marcada | | | sobre | | el | entorno | | | | | |
|  | El | robot | | obtiene | | | su | posición | | | global | | sobre | | el entorno | | por |
| | medio | | de | conocer | | | su | posición | | | sobre | | la ruta | | | | |
|  | Existen | | | diferentes | | | estrategias: | | | | | | | | | | |
| |  -  | Marcar | | el camino | | | completo | | | | | | | | | | |
| |  -  | Marcar | | las | intersecciones | | | | | | | | | | | | |
|  | Normalmente | | | | | se | emplea | | | pintura | | | ultravioleta | | | o marcas | |
| | magnéticas | | | | sobre | | el | entorno. | | | | | | | | | |
Sistemas de Control para Robots
22

## 3. introducción al problema del slam

3. Introducción al problema del SLAM
( localización y mapeado simultáneos)
El Problema del SLAM
|  Comenzando | | en | un punto | cualquiera | | del | entorno | | el |
| ------------ | ------- | ---------- | -------- | ----------- | ----------- | ------------- | --------- | --- | --- |
| robot | debería | ser | capaz | de explorar | | autónomamente | | | |
| el entorno | | utilizando | | sus | sensores | | y debería | | |
| construir | el mapa | | a la vez | que | se localiza | | sobre | él. | |
SLAM
“Simultaneous Localization And Mapping”
Sistemas de Control para Robots
24
El Problema del SLAM
| El error cometido | | en | la localización | se traslada | | al mapa… |
| ----------------- | -------- | --- | --------------- | ----------- | ---------------- | -------- |
| Y los errores | del mapa | | producen | errores | de localización… | |
Sistemas de Control para Robots
25
El Problema del SLAM
Cierre de lazos:

 Pequeños errores se acumulan produciendo graves errores
globales, sobre todo en los cierres de lazos
 Normalmente no suele dar problemas en la navegación
local, pero si a la hora de construir el mapa
Sistemas de Control para Robots 26
El Problema del SLAM
Sistemas de Control para Robots 27
El Problema del SLAM
Sistemas de Control para Robots 28

## 4. localización y mapeado

4. Localización y mapeado
mediante estimación bayesiana
Índice

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.1. Incertidumbres asociadas a los sistemas robóticos
1.2. ¿Qué son los métodos probabilísticos?
1.3. Fundamentos: teoría de la probabilidad

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Sistemas de Control para Robots 30

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.1 Incertidumbres asociadas a los sistemas robóticos
| Cuatro fuentes | principales | de incertidumbre: | |
| -------------- | ----------- | ----------------- | --- |
- El entorno
Entornos parcial o totalmente desconocidos, dinámicos e impredecibles (¿personas?)
- El robot
| Sistemas | de actuación | imprecisos | |
| -------- | ------------ | ---------- | --- |
- Los sensores
| Sensores | con información | limitada | y ruidosa |
| -------- | --------------- | -------- | --------- |
- Los modelos
| Modelos | inexactos | | |
| ------- | --------- | --- | --- |
¿Cómo conseguir sistemas robóticos robustos?
Sistemas de Control para Robots 31

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.2 ¿Qué son los métodos probabilísticos?
MÉTODOS PROBABILÍSTICOS: Introducen información sobre las ambigüedades debidas a los
modelos y a los sensores, trabajando con distribuciones de probabilidad, en lugar de con datos
exactos.
Aplicación en la resolución de problemas clásicos de robótica:

## 1. percepción - estimación de estados ( localización y mapea

1. PERCEPCIÓN - estimación de estados ( LOCALIZACIÓN Y MAPEADO)

## 2. toma de decisiones – optimización de las acciones ( contr

2. TOMA DE DECISIONES – optimización de las acciones ( CONTROL Y PLANIFICACIÓN)
Ventajas: Inconvenientes:
- No requieren modelos exactos ni precisión en  -  Complejidad desde el punto de vista
los sensores. computacional.
- Mayor robustez ante ruidos y errores de medida  -  Necesidad de realizar diferentes tipos de
( aplicaciones reales). aproximaciones
- Posibilidad de recuperación ante fallos  -  Necesidad de discretizar el estado del robot y
del entorno.
Sistemas de Control para Robots 32

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.3 Fundamentos: teoría de la probabilidad
1.3.1. Axiomas básicos de probabilidad
p ( a) representa la probabilidad de que el suceso a sea cierto:
|  -  | Si p ( a)=1, entonces a es “verdadero” | | | | 0 |  p ( a) | 1 |
| ----- | ------------------------------------ | --- | ------ | ------------ | ---- | ----------- | --- |
|  -  | Si p ( a)=0, entonces a es “falso” | | | | | | |
| UNIÓN | DE SUCESOS: | | p ( ab) | probabilidad | de a | o b ciertos | |
INTERSECCIÓN DE SUCESOS: p ( a,b) probabilidad de a y b ciertos
| Axioma: | p ( ab)=p ( a)+p ( b)-p ( a,b) | | | | | | |
| ------- | ----------------------- | --------------- | ---------------- | --- | --- | --- | --- |
| Axioma: | Si a y b son | independientes, | p ( a,b)=p ( a)p ( b) | | | | |
Sistemas de Control para Robots
33

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.3.2. Variables aleatorias continuas y discretas
VARIABLE ALEATORIA DISCRETA X: sólo toma conjunto finito de valores {x , x , …, x }
| | | | 1 | 2 n | | |
| ------- | ------------------------------------- | --------------- | --- | --- | --- | --- |
|  -  P ( X=x | ) o p ( x ) es la probabilidad de que X | tome el valor x | | | | |
1 1 1
- Distribución de probabilidad:
p ( xi)
| | | | p ( xi) |  1 | | |
| --- | --- | --- | ------ | --- | --- | --- |
xi
x1 x2 x3 …. xn xi
VARIABLE ALEATORIA CONTINUA X: toma cualquier valor x dentro de un rango continuo
- P ( X=x) o p ( x) siempre tiende a cero
b
 
- Función densidad de probabilidad:
| | | | p ( x |  a,b ) |  p ( x) |  dx |
| --- | --- | --- | --- | ------- | ------- | ---- |
a
p ( x)

| | | | p ( x) |  dx  | p ( x)  | dx  1 |
| --- | --- | --- | ----- | ------ | ------- | ------ |
a b x
| | | |  | | x | |
| --- | --- | --- | --- | --- | --- | --- |
Sistemas de Control para Robots
34

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.3.3. Probabilidad condicional
- p ( a|b)  probabilidad de que suceda “a” habiendo sucedido “b”
- p ( a|b,c)  probabilidad de que suceda “a” habiendo sucedido “b” y “c”
1.3.4. Teorema de la probabilidad total
Supóngase que el suceso a puede ocurrir en condiciones de aparición de uno de los sucesos
mutuamente excluyentes b , b ,..., b , que forman un grupo completo:
1 2 n
n
p ( a) p ( b ) p ( a|b ) p ( b ) p ( a|b )... p ( b ) p ( a|b )  p ( b ) p ( a|b )
1 1 2 2 n n i i
i1
( versión discreta)
p ( a)  p ( b) p ( a|b)db ( versión continua)
b
Sistemas de Control para Robots 35

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
| 1.3.5. Teorema de Bayes | | ( probabilidad a posteriori) | | | | |
| ----------------------- | --- | --------------------------- | --- | --- | --- | --- |
Supóngase que el suceso a puede ocurrir en condiciones de aparición de uno de los sucesos
| mutuamente | excluyentes | b , b | ,... b : HIPÓTESIS. | | | |
| ---------- | ----------- | ----- | ------------------- | --- | --- | --- |
| | | 1 2 | n | | | |
Teorema de Bayes: permite estimar las probabilidades de las hipótesis después de conocer el
resultado de la experimentación, debido a la cual ocurrió el suceso a:
| | | | | p ( a |b | ) p ( b | ) |
| --- | --- | --- | ------- | ------- | ------ | --- |
| | | | | | i | i |
| | | p ( b | | a )  | | | |
i
p ( a )
 p ( bi|a)  probabilidad a posteriori de la hipótesis b, habiendo sucedido a.
i
 p ( a|bi)  verosimilitud ( probabilidad condicional) del suceso a bajo la hipótesis b.
i
|  p ( bi) |  probabilidad | a priori | del suceso | b. | | |
| ------- | -------------- | -------- | ---------- | --- | --- | --- |
i
|  p ( a) |  probabilidad | total | ( o evidencia) | de que | suceda | a |
| ------ | -------------- | ----- | ------------- | ------ | ------ | --- |
Sistemas de Control para Robots
36

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica
1.3.6. Condicionalidad en los teoremas de probabilidad total y de Bayes
Sean a, b y c tres sucesos dependientes.
- Teorema de la probabilidad total. Se desea calcular la probabilidad total de que suceda a,
habiendo sucedido b, y sabiendo que ello puede ocurrir en condiciones de aparición de uno de
| los sucesos mutuamente excluyentes c | | , c , c , … , c | . |
| ------------------------------------ | --- | --------------- | --- |
| | | 1 2 3 | n |
n
| | p ( a|b) |  p ( ci|b) | p ( a|b,ci) |
| --- | ------ | ---------- | ---------- |
Versión discreta:
i1
Versión continua:
| | p ( a|b) |  p ( c|b)p ( a|b,c)dc | |
| --- | ------ | --------------------- | --- |
- Teorema de Bayes. Se desea calcular la probabilidad a posteriori de c, habiendo sucedido b y a.
p ( b |c,a) p ( c |a)
| | p ( a |c,b) | p ( c |b) | o |
| --- | ---------- | ------- | --- |
p ( c |b,a) 
p ( c |b,a) 
p ( b |a)
| | p ( a | |b) | |
| --- | --- | --- | --- |
Sistemas de Control para Robots
37
Índice del Bloque

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.1. Planteamiento de estimación de estados: ejemplo práctico
2.2. Filtros bayesianos
2.3. Ejemplo de aplicación de un filtro de Bayes a la localización de un robot

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Sistemas de Control para Robots 38

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.1 Planteamiento de estimación de estados: ejemplo práctico
Supóngase un robot capaz de obtener una medida O que puede
| tomar valores de un conjunto definido {o | , o ,…,o | } | |
| ---------------------------------------- | -------- | --- | --- |
| | 1 2 | n | |
OBJETIVO: estimar el estado S={abierta, cerrada} de una puerta.
2.1.1. Planteamiento del problema de estimación del estado de la puerta
- p ( abierta|o ) es el OBJETIVO DE ESTIMACIÓN ( diagnóstico), difícil de obtener
1
- p ( o |abierta) es una verosimilitud ( probabilidad causal), fácil de obtener
1
- p ( abierta) es una probabilidad a priori, que se conoce de antemano
p ( o | abierta) p ( abierta)
| | p ( abierta|o | )  | 1 |
| -------------------------- | ----------- | --- | --- |
| SOLUCIÓN: Teorema de Bayes | | 1 | |
p ( o )
1
Sistemas de Control para Robots 39

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
Ejemplo 1: Estimación tras la realización de una primera medida
| Se realiza una primera medida de valor O=o | | | . | |
| ------------------------------------------ | --- | --- | --- | --- |
1
DATOS: Verosimilitudes: p ( o |abierta)=0.6 p ( o |cerrada)=0.3
| | | 1 | | 1 |
| --- | --- | --- | --- | --- |
Probabilidades a priori: p ( abierta)=p ( cerrada)=0.5
ESTIMACIÓN ( PROBABILIDAD A POSTERIORI) del estado de la puerta:

## p ( s)

P ( S)
| | p ( o |abierta)p ( abierta) | | 0.60.5 | |
| ----------- | ----------------------- | --- | ------- | ------ |
| p ( abierta|o | )  1 | |  |  0.67 |
1 0.67
| | | p ( o ) | 0.60.50.30.5 | |
| --- | --- | ----- | --------------- | --- |
1
0.5
0.33
| | p ( o |cerrada)p ( cerrada) | | 0.30.5 | |
| ----------- | ----------------------- | ----- | --------------- | ------ |
| p ( cerrada|o | )  1 | |  |  0.33 |
| | 1 | p ( o ) | 0.60.50.30.5 | |
1 abierta cerrada S
La primera medida ha INCREMENTADO la probabilidad de que la puerta esté abierta
Sistemas de Control para Robots 40

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
Ejemplo 2: Estimación tras la realización de una segunda medida
| Se realiza una segunda medida de valor O=o | | | | . | | |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- |
2
DATOS: Verosimilitudes: p ( o |abierta)=0.4 p ( o |cerrada)=0.6
| | | | 2 | 2 | | |
| --- | --- | --- | --- | --- | --- | --- |
Probabilidades a priori: p ( abierta|o )=0.67 p ( cerrada|o )=0.33
1 1
ESTIMACIÓN ( PROBABILIDAD A POSTERIORI) del estado de la puerta:

## p ( s)

P ( S)
| | p ( o |abierta)p ( abierta|o | | ) | | | |
| ------------- | ------------------------- | -------- | --- | --- | --- | ----- |
| p ( abierta|o,o | ) 2 | | 1  | | | 0.575 |
| | 1 2 | p ( o |o ) | | | | |
2 1
0.5
| | p ( o |abierta)p ( abierta|o | | ) | 0.40.67 | | 0424 |
| ------------------------- | ------------------------- | ---------------------------- | --- | ------------------- | ------ | ---- |
|  | 2 | | 1 |  | 0.575 | |
| p ( o |abierta)p ( abierta|o | | ) p ( o |cerrada)p ( cerrada|o | | ) 0.40.670.60.33 | | |
| 2 | | 1 2 | | 1 | | |
abierta cerrada S
La segunda medida ha REDUCIDO la probabilidad de que la puerta esté abierta
Sistemas de Control para Robots
41

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
| 2.1.2. Estimación tras la obtención de la n-ésima | | | | | | medida | | | | | |
| ------------------------------------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- |
Se realizan sucesivamente medidas para mejorar la estimación. ¿Cómo se integra la n-ésima medida
O=o ?
n

## actualización recursiva de la fórmula de bayes:

ACTUALIZACIÓN RECURSIVA DE LA FÓRMULA DE BAYES:
| | | | | p ( o | |abierta,o | ,o ,...o | ) p ( abierta|o | | ,o ,...o | ) | |
| --- | ----------- | --- | ------- | --- | ---------- | -------- | -------------- | --- | -------- | --- | --- |
| | p ( abierta|o | ,o | ,...o ) |  n | | 1 2 | n1 | | 1 2 | n1 | |
| | | 1 2 | n | | | | | | | | |
| | | | | | | p ( o | |o ,o ,...o | ) | | | |
| | | | | | | | n 1 2 | n1 | | | |

## propiedad de markov:

PROPIEDAD DE MARKOV:
Según esta condición, o no depende de las medidas previas SI SE CONOCE el estado, es decir:
n
| p ( o |abierta,o | ,o ,…,o | )=p ( o | |abierta) | | | | | | | | |
| ------------------- | --------- | ----- | ----------- | --- | -------- | --- | ---------- | ----------- | --- | -------- | --- |
| n | 1 2 | n-1 | n | | | | | | | | |
| | | | | | | p ( o | |abierta) | p ( abierta|o | | ,o ,...o | ) |
| | | | p ( abierta|o | | ,o ,...o | )  | n | | | 1 2 | n1 |
| Y la regla de Bayes | queda: | | | | | | | | | | |
| | | | | | 1 2 | n | | | | | |
| | | | | | | | | p ( o | ) | | |
n
Sistemas de Control para Robots 42

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.1.3. Aspectos prácticos: NORMALIZACIÓN DEL ESTADO
Tras cualquier actualización del estado, las nuevas probabilidades de la distribución de estado deben
sumar siempre 1  SE SUSTITUYE EL DENOMINADOR DE LA FÓRMULA DE BAYES POR UN FACTOR DE

## normalización:

NORMALIZACIÓN:
p ( abierta|o ,...,o )  p ( o | abierta) p ( abierta|o ,....,o )
1 n n 1 n1
p ( cerrada|o ,...,o )  p ( o | cerrada) p ( cerrada|o ,....,o )
1 n n 1 n1
Sistemas de Control para Robots 43

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.1.4. Conclusiones
 La regla de Bayes permite calcular probabilidades que de otro modo son difíciles
de obtener.
 Bajo el supuesto de Markov, la actualización recursiva de la fórmula de Bayes
permite integrar eficientemente múltiples condiciones para la estimación del estado.
Sistemas de Control para Robots 44

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.2 Filtros bayesianos
2.2.1. Planteamiento del problema
Supóngase un sistema para el cual se definen:
- Un conjunto de estados sS que el sistema puede adoptar
- Un conjunto de acciones aA que hacen pasar al sistema de unos estados a otros
- Un conjunto de observaciones oO que es posible obtener en los diferentes estados del
sistema
Se conocen además dos modelos probabilísticos del sistema:
- p ( s’|s,a) es el modelo de actuación que caracteriza las incertidumbres de las acciones
- p ( o|s) es el modelo de percepción que caracteriza las incertidumbres de las observaciones
Sistemas de Control para Robots 45

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
Se supone también que el sistema es dinámico, de tal manera que a lo largo del tiempo se van
sucediendo las acciones y observaciones.
| | | | o | o | o |
| ----- | -------------- | --------- | ----- | ----- | --- |
| | | | t-2 | t-1 | t |
| d ={o | ,a ,o ,a ,….,o | ,a ,o } | | | |
| t 1 | 1 2 2 | t-1 t-1 t | | | |
| | | | a | a | a |
| | | | s t-2 | s t-1 | s t |
| | | | t-2 | t-1 | t |
2.2.2. Objetivo de un Filtro Bayesiano. Concepto de Distribución de Creencia
OBJETIVO: estimar el estado del sistema en cada instante de tiempo t, manteniendo para ello una
distribución de probabilidad sobre la variable S.
Esta distribución se conoce como DISTRIBUCIÓN DE CREENCIA ( o creencia) Bel ( S) y caracteriza,
t
para cada valor particular del estado s, su probabilidad de ser el estado real del sistema.

Distribución uniforme si el estado inicial es desconocido
Inicialización de Bel ( S)
1
 Distribución delta si el estado inicial es conocido
Sistemas de Control para Robots
46

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.2.3. Propiedad de Markov
Para que sea posible aplicar un filtro de Bayes, debe cumplirse la propiedad de Markov:
p ( s |s ,d )=p ( s |s ,a )
t+1 t t t+1 t t
Esta propiedad equivale a decir que “conocer el estado actual ( presente), hace que el futuro sea
independiente del pasado”.
O lo que es lo mismo, “toda la historia pasada del sistema queda resumida en el estado actual
que, junto con la acción actual realizada, son suficientes para estimar el siguiente estado”.
Sistemas de Control para Robots 47

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.2.4. Formulación de un filtro de Bayes
| | Bel ( s | ) |  p ( s | | d | )  p ( s | | | o ,a | ,o | ,...,a | ,o | )  | | | |
| --- | ------- | --- | ----- | ----- | ------- | ----- | ---- | --- | --------- | --- | --- | --- | --- | --- |
| | | t | | t t | | t | 1 | 1 | 2 | t1 | t | | | |
| |  p ( o | | | s | ,o ,a | ,...,a | )p ( s | | | o | ,a ,...,a | | ) |  | | |
R. Bayes
| | | | t t | 1 | 1 | t1 | | t | 1 1 | | t1 | | | |
| --------- | ------- | --- | --- | ----- | --- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
| P. Markov |  p ( o | | | s | )p ( s | | o | ,a | ,...,a | ) |  | | | | | |
| | | | t t | | t | 1 1 | | t1 | | | | | | |
T. Prob. Total.  p ( o | s )p ( s | o ,a ,...a ,s )p ( s | o ,a ,...,a )ds 
| | | | t t | | t | 1 1 | t1 | | t1 | t1 | 1 | 1 | t1 | t1 |
| --- | ------- | --- | --- | ----- | --- | --- | ----- | --- | --- | --------- | --- | ---- | --- | --- |
| |  p ( o | | | s | )p ( s | | s | ,a | )p ( s | | | o | ,a ,...,a | | )ds |  | |
P. Markov
| | | | t t | | t | t1 | t1 | | t1 | 1 1 | | t1 | t1 | |
| --- | --- | ----- | --- | ------- | --- | ---- | ------- | --- | --- | ---- | --- | --- | --- | --- |
| |  | p ( o | | | s )p ( s | | | s ,a | )Bel ( s | | | )ds | | | | |
| | | | t | t | t | t1 | t1 | | t1 | | t1 | | | |
Esta es la fórmula compacta de
Modelo de percepción Modelo de actuación
un filtro de Bayes
p ( o|s) p ( s’|s,a)
Sistemas de Control para Robots
48

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
Un filtro de Bayes también puede aplicarse en dos etapas:

## 1. etapa de predicción, tras la ejecución de una acción a en

1. Etapa de predicción, tras la ejecución de una acción a en el tiempo t-1:
| Bel | ( s')   p ( s' | | s,a)Bel | ( s) |
| --- | ------------- | ---------- | --- |
| t | | | t1 |
S
Modelo de actuación

## 2. etapa de estimación, tras la obtención de una observación

2. Etapa de estimación, tras la obtención de una observación o en el nuevo estado
| Bel | ( s)  p ( o| | s)Bel | ( s) |
| --------- | ------------ | ------ | -------- |
| posterior | | | anterior |
Modelo de percepción
Sistemas de Control para Robots
49

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.2.5. Programación de un filtro de Bayes
S a
o S
| s | s | s s a | s s |
| --- | --- | ----- | --- |
s
| | | s o s | s |
| --- | --- | ----- | --- |
s
| s | s | s | |
| --- | --- | --- | --- |
Sistemas de Control para Robots
50

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos
2.3 Ejemplo de aplicación de un filtro de Bayes a la localización de un robot
Sistemas de Control para Robots 51
Índice del Bloque

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles
3.1. Introducción
3.2. Generalidades sobre localización bayesiana
3.3. Filtros de Kalman
3.4. Seguimiento de múltiples hipótesis ( MHT)
3.5. Rejillas de probabilidad. Localización de Markov
3.6. Filtros de partículas. Localización de MonteCarlo
3.7. Localización topológica
3.8. Comparativa de los métodos de localización bayesianos
3.9. Evaluación de la incertidumbre

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Sistemas de Control para Robots 52

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.1 Introducción
3.1.1. Localización del robot
Consiste en estimar la posición del robot dentro del mapa de entorno, a partir de:
* Referencias en el mapa de entorno ( marcas, distancias a elementos, etc.)
* Medidas ( observaciones) realizadas por los sensores
* Conocimiento de los movimientos realizados ( odometría)
3.1.2. Problema: naturaleza de los datos sensoriales
Odometría Sensores de distancia
( sonar, láser)
Sistemas de Control para Robots 53

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.1.3. Problemas de localización
De menor a mayor complejidad:
- Localización local  conocida la posición inicial del robot ( al menos de forma aproximada),
consiste en realizar un seguimiento de dicha posición que compense los errores de odometría
| mediante | el uso de | observaciones | | del entorno |
| -------- | --------- | ------------- | --- | ----------- |
- Localización global  consiste en localizar globalmente el robot dentro del entorno, siendo
| su posición | inicial | desconocida | | |
| ----------- | ------- | ----------- | --- | --- |
- Recuperación ante fallos de localización ( problema del Kidnapping)  consiste en localizar
globalmente un robot que, conociendo su posición, es transportado instantáneamente ( sin
| información) | a otra | posición | alejada | del entorno |
| ------------ | ------ | -------- | ------- | ----------- |
Sistemas de Control para Robots
54

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.2 Generalidades sobre localización bayesiana
3.2.1. Los ELEMENTOS del filtro ( mapa, estados, acciones y observaciones)
Acciones aA
Mapa de entorno m
-Cambian el estado ( posición) del
robot pues generan movimiento.
- Puede ser cualquier tipo de
mapa ( rejilla, geométrico o
- Pueden ser de muchos tipos.
topológico).
Comandos de traslación, de
rotación, de velocidad de las
- Puede haber sido obtenido
ruedas, etc.
experimentalmente.
- Suelen medirse por odometría.
Estados del robot sS
( posibles posiciones)
Observaciones oO
- Es la variable a estimarpor
el filtro.  -  Sonmedidas tomadas por los
sensores ( cualquier sensor, o
- Puede definirse de muchas
varios sensores).
formas. Sobre mapas
métricos, la más típica es  -  Pueden ser de cualquier tipo.
s=( x,y,). Distancia a marcas, scan de sonar
o láser, etc.
- El estado puede ser
continuo o discreto.
Sistemas de Control para Robots 55

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.2.2. Los MODELOS PROBABILÍSTICOS: modelo de actuación y modelo de percepción
a) Modelo de actuación o movimiento p ( s’|s,a) Probabilidad de pasar al estado s’ si inicialmente
se encuentra en el estado s y ejecuta la acción a. ACCIONES INCIERTAS.
Modelo error de odometría
EJEMPLO: p ( s’ | s , a )
Rotación medida a
rot
Movimiento medido a o
traslación medida a
tras
| | | | | , | ) |
| --- | --- | --- | --- | ---- | --------------------- |
| | | | | a=( a | a |
| | | | | rot | tras p ( d|a)=p ( s’|s,a) |

## odometría

ODOMETRÍA

## ecuaciones cinemática

ECUACIONES CINEMÁTICA
Rotación necesaria d o traslación necesaria d
rot tras
| | |  |  | | |
| ------ | ---------- | ----- | --- | ---------------------- | --- |
| x' | x  d cos | θ  d |  | | |
| | tras | rot | | Movimiento necesario d | |
|   |  | |  | | |
| | |  |  | | |
| y'  | y  d sen | θ  d | | | |
| | tras | rot |  | | |
, )
|   |  | |  | d=( d | d |
| --- | --- | --- | --- | ---- | -------- |
| θ' |  | d | | | rot tras |
|   |  | |  | | |
rot
Sistemas de Control para Robots
56

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
b) Modelo de observación o percepción p ( o|s) Probabilidad de realizar la observación o en el
estado s. SOLAPAMIENTO PERCEPTUAL Y RUIDO EN LOS SENSORES.
Modelo ruido de sensores
EJEMPLO: p ( o | s , m ) = p ( o|s)
Distancias medidas p ( o |s)
n
o ... o
o n

## ultrasonidos

ULTRASONIDOS

## mapa métrico entorno

MAPA MÉTRICO ENTORNO
Distancias esperadas en s p ( o|s)
d ... d producto de
o n
todos los
sensores
Sistemas de Control para Robots 57

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.2.3. Estimación de la localización: CREENCIA
El resultado de la estimación no es una posición exacta, sino una densidad de probabilidad sobre los
estados
Si el estado es continuo -> densidad de Creencia
Bel ( s)ds 1
CREENCIA Bel ( S)
S
Si el estado es discreto -> distribución de Creencia
Bel ( s) 1
sS

## ejemplo:

EJEMPLO:
INICIALIZACIÓN DE Bel ( S):
- Si posición inicial CONOCIDA:
función delta en dicha posición
- Si posición inicial DESCONOCIDA:
distribución uniforme
- Cualquier otra distribución según
el conocimiento inicial
Sistemas de Control para Robots 58

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.2.4. Aplicación del filtro bayesiano
- Desde su posición anterior ( caracterizada por Bel ( S))…
- …el robot ejecuta una acción a ( desplazamiento)…
- …y obtiene una observación o ( medida sensores)
- ACTUALIZACIÓN DE Bel ( S)
Bel ( s')  p ( o| s')  p ( s'| s,a) Bel ( s)  ds
PREDICCIÓN usando el modelo de actuación
CORRECCIÓN o ESTIMACIÓN usando el modelo de observación

## normalización

NORMALIZACIÓN
Sistemas de Control para Robots 59

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.2.5. Diferentes representaciones de la localización bayesiana
Si el estado S es continuo y no se impone ninguna restricción
Bel ( s')  p ( o|s')p ( s'|s,a)Bel ( s)ds
adicional, un filtro de Bayes es intratable computacionalmente

## soluciones propuestas:

SOLUCIONES PROPUESTAS:
Métodos basados en discretización ( 95) Filtros de Kalman ( finales 80)
 Con representación topológica ( 95)  Gaussianas
o Planificación con POMDPs  Modelos lineales
 Sólo localización local ( tracking)
o Localización global y recuperación
 Con representación métrica ( rejillas) ( 96)
o Localización global y recuperación
Multi-hipótesis ( 00)
 Varios filtros de Kalman
Filtros de Partículas ( 99)  Localización global y
 Representación basada en muestras recuperación ante fallos
 Localización global y recuperación
Uso de funciones continuas
Discretización del estado y/o creencia parametrizadas
Sistemas de Control para Robots 60

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.3 Filtros de Kalman
3.3.1. Restricciones del filtro de Kalman respecto al filtro de Bayes
Aunque el estado S es continuo, recurre al uso de funciones parametrizadas :
- Modelos de actuación y percepción lineales, contaminados con ruido independiente, blanco,
gaussiano y de media cero.
- La Creencia se modela también como una función de probabilidad gaussiana.

## modelos gaussianos:

MODELOS GAUSSIANOS:
Se caracterizan por su media  y varianza 2:
p ( x)=N (,2)
Si x es multivariable… p ( x)=N (,)
La Creencia se modela mediante una función de este tipo
Y los ruidos de los modelos de actuación y percepción también. Nomenclatura:
Ruido en el modelo de actuación ( o del sistema): w=N ( 0,Q)
Ruido en el modelo de percepción ( o de medida): v=N ( 0,R)
Sistemas de Control para Robots 61

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.3.2. Planteamiento de un filtro de Kalman como estimador de estados ( posición)
Los modelos que intervienen son:

## 1. modelo del sistema ( lineal y con ruido gaussiano)

1. MODELO DEL SISTEMA ( lineal y con ruido gaussiano)
Equivale al MODELO DE ACTUACIÓN de un f. Bayes
| s |  A | s |  B | a |  | w | p ( s |s | | ,a ) |  N ( A | s B | a ,Q ) |
| --- | --- | --- | --- | --- | --- | --- | ------ | --- | ---- | ----- | ----- | ------- |
| t | | t1 | | t1 | | t1 | t | t1 | t1 | | t1 | t1 t |

## 2. modelo de medida ( lineal y con ruido gaussiano)

2. MODELO DE MEDIDA ( lineal y con ruido gaussiano)
Equivale al MODELO DE PERCEPCIÓN de un f. Bayes
| | o | Hs | | v | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---- | --- |
| | |  |  | | | | | p ( o | |s | )  N ( Hs | ,R ) | |
| | t | | t | t | | | | | t t | | t t | |

## 3. función densidad de creencia gaussiana

3. FUNCIÓN DENSIDAD DE CREENCIA GAUSSIANA
- sˆ es la media ( valor estimado del estado)
t
- P es la covarianza del error de estimación
| | Bel ( s | | )  N (ˆs | ,P | ) | | | | | | | |
| --- | ----- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
t
| | | | t | t | t | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
- El error de estimación es la desviación entre el estado
ˆs
| | | | | | | real y el estimado | | | | e  s | | |
| --- | --- | --- | --- | --- | --- | --------------------- | --- | --- | --- | ----- | --- | --- |
| | | | | | | | | | | t t | t | |
Sistemas de Control para Robots
62

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.3.3. Ecuaciones del filtro de Kalman

## 1. inicialización de la creencia

1. INICIALIZACIÓN DE LA CREENCIA
| | | | | | | | | | Bel ( s | ) N (ˆs | ,P | ) | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | ------- | --- | --- | --- | --- | --- | --- |
| | | | | | | | | | | 0 | 0 | 0 | | | | |

## 2. etapa de predicción

2. ETAPA DE PREDICCIÓN
Nueva Creencia
| ˆs |  Aˆs | Ba | | | | | | | | | | | | | | |
| --- | ------ | ---- | --- | --- | --- | ----- | --- | ------- | --- | ---- | ---- | --- | ----- | --- | --- | --- |
| t | | t1 | t1 | | | | | | | | | | | | | |
| | | | | | | | | N ( Aˆs | | | | | T | | | |
| | | | T | | | Bel ( s | ) | | | Ba | ,AP | | A Q | ) | | |
| P |  AP | A |  Q | | | | t | | t1 | | t1 | t1 | | t1 | | |
| t | t1 | | t1 | | | | | | | | | | | | | |

## 3. etapa de corrección

3. ETAPA DE CORRECCIÓN
| ˆs |  ˆs | K | ( o Hˆs | | ) | | | | | | | | | | | |
| ---------- | ------ | --- | -------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| tposterior | tprior | | t t | tprior | | | | | | | | | | | | |
Nueva Creencia
| | | |  | | 1 | | | | | | | | | | | |
| --- | --- | ---- | ------ | --- | --- | --- | ----- | --- | --- | ----- | --- | --- | ----- | ------ | ----- | --- |

## | | | | t | t | | | | | | | | | | | | |

| | | | T | T | | | | | | | | | | | | |
| con | K  | P H | HP H | R | | | | | | | | | | | | |
| | t | t | t | | t | | | | | | | | | | | |
| | | | | | | | Bel ( s | | ) | N (ˆs | K | ( o | Hˆs | ),( IK | H)P | ) |
Ganancia de Kalman
| | | | | | | | | tposterior | | tprior | | t | t tprior | | t tprior | |
| --- | --- | ----- | ----- | ------ | --- | --- | --- | ---------- | --- | ------ | --- | --- | -------- | --- | -------- | --- |

## | p |  | ( i k | h)p | | | | | | | | | | | | | |

| P |  | ( I K | H)P | | | | | | | | | | | | | |
| | | | t | tprior | | | | | | | | | | | | |
tposterior
Sistemas de Control para Robots
63

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.3.4. Aplicación a la localización
- La posición inicial debe ser conocida
( aproximadamente), para modelarla como
una gaussiana
- Sólo es capaz de seguir una hipótesis
( localización local). No resuelve la localización
global y el kidnapping.
- La dinámica del movimiento del robot
debe ser lineal, y todos los ruidos gaussianos.
Si no lineal -> EKF
- Las “marcas” utilizadas para el
posicionamiento deben ser distinguibles para
que el modelo de medida sea gaussiano
Sistemas de Control para Robots 64

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.4 Seguimiento de Múltiples Hipótesis ( MHT)
3.4.1. ¿En qué consiste?
Es una GENERALIZACIÓN del filtro de Kalman que permite el seguimiento de varias hipótesis para
resolver el problema de LOCALIZACIÓN GLOBAL.
- El estado S sigue siendo continuo
- La creencia admite varias hipótesis ( multi-modal), todas ellas gaussianas
- Cada hipótesis es actualizada mediante un filtro de Kalman

## problemática adicional:

PROBLEMÁTICA ADICIONAL:
- Asociación de datos: ¿qué medida u observación corresponde a cada hipótesis?
- Gestión de las hipótesis: ¿cuándo añadir una nueva hipótesis o eliminar alguna existente?
Sistemas de Control para Robots 65

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.4.2. Localización mediante MHT
- La posición inicial puede ser
desconocida
- Es capaz de seguir varias hipótesis por
lo que resuelve el problema de
localización global.
- La dinámica del movimiento del robot
debe ser lineal, y todos los ruidos
gaussianos.
Si no lineal -> EKF
- Las “marcas” utilizadas para el
posicionamiento pueden ser
indistinguibles ( pero debe establecerse
un sistema para gestionar las hipótesis)
Sistemas de Control para Robots 66

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.5 Rejillas de probabilidad. Localización de Markov
3.5.1. Discretización del estado mediante rejillas de probabilidad
La localización de Markov consiste en aplicar un filtro bayesiano sobre un espacio de estados
( número finito de estados sS). Así, la integral se convierte en sumatorio:
discreto
p ( s'|s,a)Bel ( s)
| | | Bel ( s') |  p ( o|s') | | s'S |
| --- | --- | ------- | ------------ | --- | ----- |
sS
| Discretización | típica: REJILLAS de tamaño fijo | | | | |
| -------------- | -------------------------------- | --- | --- | --- | --- |
Por ejemplo, si el estado es la posición s=( x,y,)
| VENTAJAS | respecto a filtros de Kalman | | | y MHT: | |
| -------- | ---------------------------- | --- | --- | ------ | --- |
- Los modelos no tienen que ser lineales, ni los ruidos gaussianos ( no restricciones)
- La creencia no es una función parametrizada, sino una distribución de cualquier tipo
Sistemas de Control para Robots 67

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.5.2.Localización de Markov
- La posición inicial puede ser desconocida
- Es capaz de seguir varias hipótesis por lo que
resuelve el problema de localización global.
- La dinámica del movimiento del robot no
tiene que ser lineal, y los modelos de ruido en
medida o actuación no tienen que ser
gaussianos.
- Las “marcas” utilizadas para el
posicionamiento pueden ser indistinguibles sin
que ello conlleve complejidad adicional
ninguna, como sucedía con el MHT.
Sistemas de Control para Robots 68

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6 Filtros de partículas. Localización de Monte Carlo
3.6.1. Generalidades
PROBLEMAS de la Localización de Markov:
- Cuando la creencia se centra en una zona, no tiene interés mantener una rejilla de tamaño fijo en
todo el entorno.
- Poca eficiencia computacional si se desea tener una buena resolución en entornos amplios ( aumenta
el número de estados)

## localización de monte carlo ( mcl):

LOCALIZACIÓN DE MONTE CARLO ( MCL):
- El estado S es continuo ( los estados s pueden tomar cualquier valor)
- La creencia se discretiza en partículas ( muestras de Bel ( S) que adquirirán mayor concentración
en las zonas del entorno con más probabilidad de ser la posición del robot).
Bel ( S)
S
Sistemas de Control para Robots 69

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.2. Discretización de la creencia mediante partículas
El estado S es continuo
La creencia se discretiza mediante un conjunto de N partículas:
P={pi|i=1,…,N}
Cada PARTÍCULA tiene la forma p={s,w} donde:
- s  posición de la partícula en el entorno ( normalmente s=( x,y,))
- w  peso de la partícula ( “importancia” de la misma). Se conoce como factor de importancia.
Cuanto mayor es el factor de importancia, mayor probabilidad tiene la partícula de ser la posición
real del robot. Normalmente se normaliza el conjunto de todas las partículas de manera que la
suma de sus factores de importancia sea 1.
Sistemas de Control para Robots 70

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.3. Localización de Monte Carlo ( MCL)

## 1. conjunto inicial de patículas p según conocimiento inicia

1. CONJUNTO INICIAL DE PATÍCULAS P según conocimiento inicial de la posición:
0
- Posición inicial desconocida  muestras aleatorias con wi=N-1
| | |  | | wi=N-1 |
| ----------------------------- | --- | ----------------------- | --- | ------ |
|  -  Posición inicial conocida s | | todas las muestras en s | | con |
| | 0 | | | 0 |

## 2. etapa de predicción ( movimiento del robot tras ejecutar

2. ETAPA DE PREDICCIÓN ( movimiento del robot tras ejecutar la acción a )
t-1
Se genera un nuevo conjunto de partículas P ={p i}={s i,w i}, a partir del anterior
| | | | t t | t t |
| --- | --- | --- | --- | --- |
P ={p i}={s i,w i}. Cada nueva partícula p i se genera en dos pasos:
t-1 t-1 t-1 t-1 t
i
a. Seleccionando aleatoriamente una partícula p del conjunto anterior, con probabilidad
t-1
determinada por el factor de importancia de dichas partículas ( resampling).
b. Propagando dicha partícula a su nueva posición, utilizando el modelo de movimiento
p ( s’|s,a). Para ello, se toma s i como posición original, y se escoge aleatoriamente una
t-1
| muestra de la distribución p ( s | | i|s i,a | ) | |
| ------------------------------ | --- | ------- | --- | --- |
| | | t t-1 | t-1 | |
i=N-1
El factor de importancia de la nueva partícula es w
t-1
71
Sistemas de Control para Robots

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
Ejemplo de predicción:
Sistemas de Control para Robots 72

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots

## 3. etapa de estimación ( obtención de una medida o con los s

3. ETAPA DE ESTIMACIÓN ( obtención de una medida o con los sensores)
t
La obtención de una medida o se incorpora al filtro de partículas recalculando los factores de
t
importancia de cada una de ellas del siguiente modo:
w i=p ( o |s i) con  factor de normalización
t t t
Ejemplo de estimación:
Sistemas de Control para Robots 73

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
Ejemplo con varias iteraciones…
a) Inicialización. Muestras
aleatorias con el mismo
factor de importancia
b) Observación de una
puerta. Reponderación de
los factores de
importancia
c) Movimiento.
Remuestreo del conjunto
de partículas y
propagación de las
mismas
d) Observación de una
puerta. Reponderación de
los factores de
importancia
e) Movimiento.
Remuestreo del conjunto
de partículas y
propagación de las
mismas
Sistemas de Control para Robots 74

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.4. Algoritmo MCL
Cada iteración del MCL…
| Si st e m | a s d e C on t ro | l p a ra R ob o t s |
| --------- | ------------------- | --------------------- |
DEPARTAMENT O D E E L E C T R Ó N I C A – U n iv e rsidad de Alcalá 75

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.5. Ventajas e inconvenientes del MCL

## ventajas:

VENTAJAS:
- Resuelve los problemas de localización local y localización global.
- Cualquier tipo de modelo del sensor, dinámica de movimiento y distribución de ruido.
- Centra los recursos computacionales en las áreas del entorno en que hay más probabilidad de que se
encuentre el robot ( mayor concentración de partículas)
- Precisión: no discretizan el estado.
- Controlando y adaptando el número de partículas, los filtros de partículas se adaptan fácilmente a los
recursos computacionales disponibles
- Fáciles de implementar desde el punto de vista computacional.

## inconvenientes:

INCONVENIENTES:
- Si el conjunto de partículas es pequeño, un robot bien localizado puede llegar a perderderse debido a
que el proceso de “remuestreo” aleatorio no genere ninguna muestra en la localización correcta.
- Para resolver también el problema de la recuperación ante fallos ( kidnapping) es necesario alterar el
algoritmo estándar, manteniendo siempre un número reducido de partículas aleatoriamente
distribuidas por el entorno.
76
Sistemas de Control para Robots

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.6. Ejemplos prácticos
Ejemplo de localización global utilizando ultrasonidos ( anillo de 24 sensores).
Sistemas de Control para Robots 77

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.6.6. Ejemplos prácticos
Ejemplo de localización global utilizando ultrasonidos ( anillo de 24 sensores).
Sistemas de Control para Robots 78

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
Ejemplo de localización global utilizando ultrasonidoscon número de partículas adaptativo
Sistemas de Control para Robots 79

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
Ejemplo de localización global utilizando lásercon número de partículas adaptativo
Sistemas de Control para Robots 80

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
Ejemplo de localización global utilizando visión ( Condensation algorithm)
Sistemas de Control para Robots 81

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.7 Localización topológica
3.7.1. Generalidades
- Todos los métodos anteriores utilizan como estado la posición métrica s=( x,y,) del robot dentro
del entorno
- Cuando se trabaja con una discretización más gruesa ( TOPOLÓGICA) los estados pueden ser los
nodos de un grafo.
Tipo: pasillo
Distancia: 2 m con prob. 0.3
Tipo: nodo topológico
3 m con prob. 0.5
Norte: abierto
4 m con prob. 0.2
Oeste: abierto
Bel ( s')  p ( o|s') p ( s'|s,a)Bel ( s) s'S Sur: abierto
Este: pared
sS
Nodo Nodo
- Este tipo de modelos bayesianos se formulan matemáticamente como Procesos de Decisión de
Markov Parcialmente Observables ( POMDPs) ( se verán en el tema de planificación).
o La localización corresponde al estimador de estados del POMDP
o La planificación corresponde a las políticas de decisión del POMDP
Sistemas de Control para Robots 82

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.7.2. Modelos de transición y observación

## 1. modelo de transición p ( s’|s,a)

1. MODELO DE TRANSICIÓN p ( s’|s,a)
- Las acciones no son movimientos métricos, sino comportamientos abstractos del tipo “girar 90º
a la izquierda”, “seguir pasillo”, “cruzar puerta”, etc.
- El modelo de transición se almacena en matrices de transición ( una por cada posible acción).

## ejemplo:

EJEMPLO:
| | ao=Salir de habitación | | | aE=Entrar en habitación | | | | aF=Seguir pasillo | | |
| --- | ---------------------- | --------- | ---------- | ----------------------- | ------- | ----- | ------ | ---------------------- | -------------- | ------- |
| s’ | | | s’ | | | | s’ | | | |
| s | 0 1 | 2 3 4 5 6 | 7 8 ... s | 0 1 | 2 3 4 5 | 6 7 8 | ... s | ... 22 23 | 24 25 26 27 28 | 29 ... |
| 0 | 5 0 | 0 0 0 0 0 | 0 0 ... | | ... | | ... | | ... | |
| 1 | 0 5 | 0 0 0 0 0 | 0 0 16 | 90 0 | 0 0 0 0 | 0 0 0 | 22 | 10 | 0 0 0 70 0 | 0 0 |
| 2 | 0 0 | 5 0 0 0 0 | 0 0 17 | 0 0 | 0 0 0 0 | 0 0 0 | 23 | 0 | 0 0 0 0 0 | 0 0 |
| 3 | 0 0 | 0 5 0 0 0 | 0 0 18 | 0 0 | 0 0 0 0 | 0 0 0 | 24 | 0 | 0 10 0 0 0 | 0 0 |
| 4 | 0 0 | 0 0 5 0 0 | 0 0 ... 19 | 0 90 | 0 0 0 0 | 0 0 0 | ... 25 | ... 0 | 0 0 0 0 0 | 0 0 ... |
Modelo con 5 acciones… 5 0 0 0 0 0 5 0 0 0 20 0 0 0 0 0 0 0 0 0 26 0 0 0 0 10 0 0 0
| 6 | 0 0 | 0 0 0 0 5 | 0 0 21 | 0 0 | 0 0 0 0 | 0 0 0 | 27 | 0 | 0 0 0 0 0 | 0 0 |
| --- | --- | ----------------------- | ----------- | ----- | ------- | --------------------- | -------- | -------- | ---------- | ---- |
| 7 | 0 0 | 0 0 0 0 0 | 5 0 22 | 0 0 | 0 0 0 0 | 0 0 0 | 28 | 0 | 0 70 0 0 0 | 10 0 |
| 8 | 0 0 | 0 0 0 0 0 | 0 5 23 | 0 0 | 0 0 0 0 | 0 0 0 | 29 | 0 | 0 0 0 0 0 | 0 0 |
| ... | | ... | ... | | ... | | ... | | ... | |
| | | aL=Girar a la izquierda | | | | aR=Girar a la derecha | | | | |
| | | s’ | | | s’ | | | | | |
| | | s ... 14 15 | 16 17 18 19 | 20 21 | ... s | ... 14 15 | 16 17 18 | 19 20 21 | ... | |
| | | ... | ... | | ... | | ... | | | |
| | | 14 5 | 90 5 0 0 0 | 0 0 | 14 | 5 0 | 5 90 0 | 0 0 0 | | |
| | | 15 0 | 5 90 5 0 0 | 0 0 | 15 | 90 5 | 0 5 0 | 0 0 0 | | |
| | | 16 5 | 0 5 90 0 0 | 0 0 | 16 | 5 90 | 5 0 0 | 0 0 0 | | |
| | | 17 ... 90 | 5 0 5 0 0 | 0 0 | ... 17 | ... 0 5 | 90 5 0 | 0 0 0 | ... | |
| | | 18 0 | 0 0 0 5 90 | 5 0 | 18 | 0 0 | 0 0 5 | 0 5 90 | | |
| | | 19 0 | 0 0 0 0 5 | 90 5 | 19 | 0 0 | 0 0 90 | 5 0 5 | | |
| | | 20 0 | 0 0 0 5 0 | 5 90 | 20 | 0 0 | 0 0 5 | 90 5 0 | | |
| | | 21 0 | 0 0 0 90 5 | 0 5 | 21 | 0 0 | 0 0 0 | 5 90 5 | | |
| | | ... | ... | | ... | | ... | | | |
Sistemas de Control para Robots
83

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots

## 2. modelo de observación p ( o|s)

2. MODELO DE OBSERVACIÓN p ( o|s)
- Las observaciones también suelen ser medidas abstractas del tipo “número de marcas del tipo
A visualizadas”, “detección de puerta”, “detección de pasillo”, etc
- El modelo de observación se almacena en matrices de observación ( una por cada posible
observación).

## ejemplo:

EJEMPLO:
| | | p ( o OAU |s) | | | p ( o OVM | |s) | p ( o | OVP |s) |
| --------------------------- | --- | ---------------- | ------- | ----- | ------- | ---------- | ------ | -------- |
| Modelo con 3 observaciones… | OAU | | | OVM | | | OVP | |
| | s | 0 1 2 3 4 | 5 6 7 | s | 0 1 2 | 3 4 5 6 | s 0 | 1 2 3 |
| | ... | ... | | ... | | ... | ... | |
| | 14 | 0 4 0 0 4 | 83 0 9 | 14 | 0 10 10 | 60 10 10 0 | 14 10 | 10 10 70 |
| | 15 | 2 0 42 4 2 | 0 46 4 | 15 60 | 20 20 | 0 0 0 0 | 15 70 | 10 10 10 |
| | 16 | 0 2 0 2 2 | 43 2 49 | 16 20 | 60 10 | 10 0 0 0 | | |
| | | | | | | | 16 70 | 10 10 10 |
| | 17 | 2 2 42 46 0 | 0 4 4 | 17 60 | 20 20 | 0 0 0 0 | 17 70 | 10 10 10 |
| | 18 | 2 42 0 4 2 | 46 0 4 | 18 | 0 10 10 | 60 10 10 0 | | |
| | | | | | | | 18 10 | 10 10 70 |
| | 19 | 40 4 44 4 4 | 0 4 0 | 19 20 | 60 10 | 10 0 0 0 | 19 70 | 10 10 10 |
| | 20 | 2 2 0 0 42 | 46 4 4 | 20 20 | 60 10 | 10 0 0 0 | | |
| | | | | | | | 20 70 | 10 10 10 |
| | 21 | 4 0 78 9 0 | 0 9 0 | 21 60 | 20 20 | 0 0 0 0 | 21 70 | 10 10 10 |
| | ... | ... | | ... | | ... | ... | |
Sistemas de Control para Robots
84

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.7.3. Ventajas e inconvenientes de la localización topológica

## ventajas:

VENTAJAS:
- Es posible modelar entornos mucho más amplios mediante un número más reducido de estados
- No es necesario mantener la consistencia métrica global en el entorno
- Mayor eficiencia computacional: tiempos de cálculo reducidos y necesidad de menos recursos de
memoria
- Los modelos de transición y observación no deben calcularse “on-line” como en los enfoques métricos,
sino que se almacenan “off-line” en tablas, a las que se accede mucho más rápido en tiempo de
ejecución
- No existen restricciones en cuanto a los modelos, que pueden ser no lineales y multimodales
- Resuelve la localización local, global y el kidnapping ( evitando la anulación completa de la probabilidad
de un estado)

## inconvenientes:

INCONVENIENTES:
- Menor resolución en el posicionamiento
- Acciones y observaciones más complejas
Sistemas de Control para Robots 85

## 3. aplicación a la localización de robots

3. Aplicación a la localización de robots
3.8 Comparativa de los métodos de localización bayesianos
Sistemas de Control para Robots 86

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
3.9 Evaluación de la incertidumbre
La localización bayesiana genera como resultado una función densidad de probabilidad o una
distribución de probabilidad en lugar de un dato único ( CREENCIA)
Puede ser necesario evaluar el grado de incertidumbre de la creencia. Para ello:
- Métodos basados en filtros de Kalman  varianzas de las gaussianas
- Métodos que discretizan el estado o la creencia  entropía:
Entropía de la creencia: H ( B e l)    B e l ( s )  log ( Bel ( s)) A mayor valor, más incertidumbre
Bel ( s)0
Entropía normalizada: 1  1   1  ( 0= delta; 1= uniforme)
H ( Bel)   log   log  log ( m)
max
m m m
sS

## clasificación del resultado:

CLASIFICACIÓN DEL RESULTADO:
- Etapa de localización global  la varianza o entropía ( incertidumbre) es elevada
- Etapa de localización local  la varianza o entropía ( incertidumbre) es reducida. El robot está
globalmente localizado
Sistemas de Control para Robots 87
Índice del Bloque

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
4.1. Introducción
4.2. Rejillas de ocupación

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Sistemas de Control para Robots 88

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
4.1 Introducción
- En el apartado anterior, el robot se localiza a partir de un mapa conocido a
priori ( problema de estimación de bajas dimensiones ( x,y,)).
- Sin embargo, en muchas aplicaciones el mapa no está disponible, y el robot
debe obtenerlo a partir de sus sensores ( problema de estimación de
dimensión mucho más elevada).
- Se aborda en este apartado el problema de mapeado suponiendo que la
posición del robot es conocida sin errores.
Sistemas de Control para Robots 89

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
Factores que influyen en la dificultad del mapeado:
- Tamaño del mapa respecto a el rango de percepción sensorial del robot
- Ruido en la percepción y la actuación
- Solapamiento perceptual ( lugares distintos que se “ven” igual por los
sensores del robot – dificultad para establecer correspondencias)
- Lazos ( regresar al mismo punto por un camino diferente – dificultad en su
detección)
Sistemas de Control para Robots 90

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
4.2 Rejillas de ocupación
|  -  Método | introducido | | por Moravec | y Elfes | in 1985 |
| -------- | ----------- | --- | ----------- | ------- | ------- |
-
| Representa | el entorno | | mediante | una rejilla. | |
| ---------- | ---------- | --- | -------- | ------------ | --- |
- Estima la probabilidad de que cada celda esté ocupada por un obstáculo.
|  -  Suposiciones | | principales: | | | |
| -------------- | --- | ------------ | --------- | --- | --- |
| o La posición | | del robot es | conocida. | | |
o
La ocupación de cada celda ( m[xy]) es independiente de las demás.
| | | | x | x | |
| --- | --- | --- | --- | --- | --- |
Sistemas de Control para Robots
91

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
- Idea principal: actualizar cada celda utilizando un filtro de Bayes binario
x
- Suposición adicional: el mapa es estático
- El mapa se actualiza utilizando un modelo inverso del sensor.
Sistemas de Control para Robots 92

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas
Ejemplo de obtención incremental de un mapa de rejilla de ocupación:
Sistemas de Control para Robots 93
Índice del Bloque

## 1. introducción: los métodos probabilísticos en robótica

1. Introducción: los métodos probabilísticos en robótica

## 2. estimación de estados mediante filtros bayesianos

2. Estimación de estados mediante filtros bayesianos

## 3. aplicación a la localización de robots móviles

3. Aplicación a la localización de robots móviles

## 4. aplicación a la obtención de mapas

4. Aplicación a la obtención de mapas

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
5.1. Introducción
5.2. Estructura del problema del SLAM
5.3. Tipos de problemas de SLAM
5.4. Técnicas de SLAM
Sistemas de Control para Robots 94

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
5.1 Introducción
- En la práctica, el robot no conoce su posición exacta mientras va obteniendo
el mapa.
- Problema de tipo “chicken and egg”: para obtener el mapa se requiere la
posición, y para obtener la posición se requiere el mapa.
-
| SLAM: Simultaneous | | Localization | | | and Mapping | | |
| ------------------- | --- | ------------ | --- | --- | ----------- | --- | --- |
o
Dadas:
|  Las acciones | realizadas | | por | el robot | | | |
| ------------------- | ---------- | ---------- | --- | ----------- | --- | ------- | --------- |
|  Las observaciones | | realizadas | | del entorno | | ( marcas | cercanas) |
o Estimar:
|  La posición | de las | marcas | del mapa | | | | |
| ------------- | ------- | ------ | --------------- | --- | -------- | --- | --- |
|  El camino | seguido | por | el robot dentro | | del mapa | | |
Sistemas de Control para Robots
95

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
5.2 Estructura del problema del SLAM
SLAM: el camino seguido por el robot y el mapa son ambos desconocidos
El error cometido en la localización está correlado con el error del mapa
Sistemas de Control para Robots 96

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
Incertidumbre
en la posición
del robot
 En una aplicación real, la correspondencia entre las marcas y las
observaciones no se conoce
 Hacer asociaciones incorrectas produce grandes errores en el mapa
 El error de posición está correlado con las asociaciones de datos
Sistemas de Control para Robots 97

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
5.3 Tipos de problemas de SLAM
Full SLAM: estima el mapa y la trayectoria completa del robot

| p ( x | , m | z | ,u ) |
| --- | ------- | ------- |
| | 1:t | 1:t 1:t |
Sistemas de Control para Robots
98

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
 Online SLAM: estima el mapa y la posición actual del robot
| p ( x ,m | | z ,u | )    | p ( x ,m | | z ,u | ) dx dx | ...dx |
| ------ | ------ | --------- | ------ | ------ | ------- | ----- |
| t | 1:t | 1:t | 1:t | 1:t | 1:t 1 | 2 t1 |
Sistemas de Control para Robots
99

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
5.4 Técnicas de SLAM
-
Scan matching
-

## ekf slam

EKF SLAM
-
Fast-SLAM
-
Graph-SLAM
-
SEIFs
-
iSAM, etc.
Sistemas de Control para Robots 100

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM

## ekf slam

EKF SLAM
Se añaden las marcas al vector de estados:

| | | |  | 2 | | | | | | |  |
| --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
| | |  x  | | |  |  |  |  |  |  | |
| | | |  | x | xy | x | xl | xl | | | xl  |

## | | |   | | | | | 1 | 2 | | | n |

| | |   | | | | | 1 | 2 | | | N |
| | | y |  | | 2 |  |  |  |  |  |  |
 
| | | | | xy | y | y | yl | yl | | | yl |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

## | | | | | | | | 1 | 2 | | | n |

| | | | | | | | 1 | 2 | | | N |
| | |   |  | | | | | | | |  |
2
| | |  |  | |  | |  |  |  |  | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | |  | x | y |  | l | l | | l |  |
 

## | | | | | | | | 1 | 2 | | | n |

| | | | | | | | 1 | 2 | | | N |
| ----- | ------ | ------ | --- | --- | --- | --- | --- | --- | --- | --- | ----- |
| | | |  | | | | 2 | | | |  |
| Bel ( x | ,m )  |  l , | | |  |  | |  |  |  | |
| | t t | 1 | | xl | yl | l | l | ll | | | ll |

## | | | |  | 1 | 1 | 1 | 1 | 12 | | | 1 n  |

| | | |  | 1 | 1 | 1 | 1 | 12 | | | 1 N  |
 
| | | l |  | |  |  |  | 2 |  |  | |
| --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | |   |  | | | | | | | |  |
| | | 2 | | xl | yl | l | ll | l | | | l l |

## | | | | | 2 | 2 | 2 | 12 | 2 | | | 2 n |

| | | | | 2 | 2 | 2 | 12 | 2 | | | 2 N |
| | | |  | | | | | | | |  |
| | |    | |  |  |  |  |  |  | |  |
| | | |  | | | | | | | |  |
 
| | | |  | | | | | | | 2 |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | l |  | |  |  |  |  |  | | |
| | |   |  | | | | | | | |  |
| | | N | | xl | yl | l | ll | l l | | | l |

## | | | | | n | n | n | 1 n | 2 n | | | n |

| | | | | N | N | N | 1 N | 2 N | | | N |
Sólo puede manejar el orden de pocos cientos de marcas

Sistemas de Control para Robots
101

## 5. aplicación al problema del slam

5. Aplicación al problema del SLAM
| Ejemplo | de evolución | del EKF SLAM: | | | | |
| ------- | ------------ | ------------- | --- | --- | --- | --- |
Mapa Matriz de covarianza
Mapa Matriz de covarianza

## resumen:

RESUMEN:
| | | | Cuadrático | en función | del número | de |
| --- | --- | --- | ---------- | ---------- | ---------- | --- |

marcas: O ( n2)
| | | | Dificultad | para converger | en caso | de que |
| --- | --- | --- | ---------- | -------------- | ------- | ------ |

| | | | haya fuertes | no linealidades. | | |
| --- | --- | --- | ------------ | ---------------- | -------- | --- |
| | | | Diferentes | aproximaciones | permiten | |

| | | | implementarlo | en tiempo | real. | |
| --- | --- | --- | ------------- | --------- | ----- | --- |
Mapa Matriz de covarianza
Sistemas de Control para Robots
102