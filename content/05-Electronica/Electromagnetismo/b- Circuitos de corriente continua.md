---
title: "b- Circuitos de corriente continua"
---

# B: Circuitos de corriente continua

Física ( 780000). Grado en Ingeniería de Computadores ( grupo 1ºA, lunes mañana). Curso 2020/2021 – Primer Cuatrimestre. R. Gómez Herrero. Departamento de Física y Matemáticas.

## Ley de Ohm en circuitos de corriente continua

La base para el estudio de circuitos de corriente continua es la ley de Ohm.
Si $V_A > V_B$, el campo eléctrico se dirige desde A hacia B y las cargas positivas se mueven en dicha dirección: $E = ( V_A - V_B)/L = V/L$ ( aquí $V$ denota diferencia de potencial; por brevedad no usamos la notación $\Delta V$).
Criterio de signos: $I$ sigue la dirección en que se moverían cargas positivas ( aunque los portadores sean electrones y se muevan realmente en dirección opuesta).
$$I = V/R \qquad V = R \cdot I$$
Materiales óhmicos: $R = \rho L / S = \text{constante}$.

## Potencia disipada en un conductor

Cuando cierta cantidad de carga $\Delta Q$ se desplaza en el conductor de un punto A a otro de potencial menor B, reduce su energía potencial electrostática:
$$\Delta U = \Delta Q \cdot ( V_B - V_A) = -\Delta Q \cdot V < 0$$
Por tanto la energía perdida por unidad de tiempo será:
$$\frac{\Delta U}{\Delta t} = \frac{\Delta Q}{\Delta t} \cdot V = V \cdot I$$
Esta energía perdida por unidad de tiempo se disipa en forma de calor generado por las colisiones microscópicas ( efecto Joule: aumento de la temperatura del material). La potencia disipada por tanto será:
$$P = V \cdot I = R \cdot I^2 = V^2/R$$
Un dato relevante es la potencia máxima que puede disipar un conductor ( valor de P por encima del cual el conductor puede sufrir daños). Para una R fija, esto limita el valor de ( V,I), que debe mantenerse siempre por debajo de la curva $V = P_{max}/I$.
- Ejercicio:** Calcular la máxima corriente segura que puede circular por una resistencia de 1,8 kΩ clasificada por el fabricante con 0,5 W de potencia máxima.
- Solución:* Dado que tenemos que hallar la intensidad máxima, partimos de la expresión de la potencia en función de la intensidad:
$$P_{max} = R I_{max}^2 \Rightarrow I_{max} = \sqrt{\frac{P_{max}}{R}} = \sqrt{\frac{0{,}5\ W}{1{,}8 \cdot 10^3\ \Omega}} = 0{,}016\ A = 1{,}6\ mA$$
( Nótese que W = J/s = V·A y que Ω = V/A.)
La máxima potencia es un parámetro importante a la hora de seleccionar componentes en el diseño de circuitos, puesto que si se supera el valor suministrado por el fabricante, tarde o temprano la resistencia sufrirá daños.

## Resistividad, resistencia y efecto Joule

Vídeos de referencia:
- https://www.youtube.com/watch?v=PFf8FcWyZco
- https://youtu.be/3dwNzK1fiJ8
- Aplicación del efecto Joule en fusibles de protección: https://www.youtube.com/watch?v=2MWwwrOQOUc y https://www.youtube.com/watch?v=4szbWvMmzKY ( en español)
- Corriente, voltaje y sus efectos en el cuerpo humano: https://www.youtube.com/watch?v=9iKD7vuq-rY

## Potencia disipada en un conductor: ejemplo

a) Vemos que el comportamiento más lineal (óhmico) corresponde a la lámpara de carbón de 48 W ( azul).
b) Para 10 V aplicamos la ley de Ohm en la forma $R = V/I$. Para 110 V realizamos una interpolación lineal entre las dos últimas filas:
- Lámpara 100 W: $R_{100W} = 40\ \Omega$ ( a 10V) — $126{,}4\ \Omega$ ( interpolado a 110V)
- Lámpara 40 W: $R_{40W} = 71{,}4\ \Omega$ — $305{,}6\ \Omega$
- Lámpara 48 W: $R_{48W} = 476{,}2\ \Omega$ — $255{,}8\ \Omega$
c) Coeficiente de temperatura: $\alpha = \dfrac{1}{\rho}\dfrac{d\rho}{dT}$, y de forma equivalente $\alpha = \dfrac{1}{R}\dfrac{dR}{dT}$.
Si la resistividad crece con la temperatura ($\alpha$ positivo): PTC ( conductor). Si la resistividad decrece con la temperatura ($\alpha$ negativo): NTC ( semiconductor).
En este caso vemos que las lámparas de 100 y 40 W presentan una mayor resistencia al crecer V ( y por tanto T), mientras que la lámpara de 48 W se comporta al contrario.
d) Potencia disipada a 110 V. Usando $P = VI$:
- $P_{100W} = 95{,}7\ W$
- $P_{40W} = 39{,}6\ W$
- $P_{48W} = 47{,}3\ W$
e) Hallamos la R equivalente ( suma) y aplicamos la ley de Ohm:
$$I = \frac{110\ V}{126{,}4 + 305{,}6\ \Omega} = 0{,}255\ A$$
$$V_{100W} = R_{100W} \cdot I = 32{,}2\ V; \qquad V_{40W} = R_{40W} \cdot I = 76{,}8\ V \qquad ( V_{100W} + V_{40W} = 110\ V)$$

## Elementos activos y pasivos en circuitos de C.C.

También es posible transformar ( parte de) esta energía en otras formas de energía además de calor, por ejemplo energía mecánica ( ejemplo: motores eléctricos).
Distinguimos dos tipos de elementos en un circuito eléctrico:
- Elementos pasivos:** consumen energía eléctrica y la transforman en otro tipo de energía. Ejemplo: resistencias.
- Elementos activos:** generan energía eléctrica a partir de otro tipo de energía. Ejemplos: pilas o baterías ( transforman energía química en eléctrica); dinamo ( genera energía mecánica en eléctrica).

## Algunos símbolos habituales en circuitos de C.C.

- Resistencia
- Resistencia variable
- Fuente o batería de corriente continua
- Voltímetro
- Amperímetro

## Fuentes reales: fuerza electromotriz

Definimos fuerza electromotriz $\varepsilon$ de un elemento activo ( batería, fuente) como el trabajo por unidad de carga que éste suministra. El resultado de este trabajo es elevar la energía potencial electrostática, es decir, crear una diferencia de potencial en virtud de la cual se pueda suministrar corriente a un circuito.
Una batería ideal mantendría entre sus bornes una diferencia de potencial igual a su fuerza electromotriz independientemente de los elementos conectados al circuito.
Las baterías reales tienen cierta resistencia interna $r_i$, y la propiedad anterior deja de cumplirse ya que existe una pequeña caída de potencial dentro de la propia fuente.
Fuente o batería real: $V_B - V_A = \varepsilon - r_i \cdot I < \varepsilon$
Fuente ideal: $r_i = 0 \Rightarrow V_B - V_A = \varepsilon$
Analogía energética con un flujo de agua. La pila actúa como "bombeador" de cargas ( aumenta su energía potencial), de forma que luego "caen" a menor potencial ( https://faraday.physics.utoronto.ca/IYearLab/Intros/DCI/Flash/WaterAnalogy.html).
- Teorema de máxima transferencia de potencia:** la máxima transmisión de potencia por parte de una fuente de CC se logrará cuando se conecte a ella una resistencia igual a su resistencia interna:
$$\varepsilon = ( R + r)I \Rightarrow I = \frac{\varepsilon}{R + r}$$
$$P = R I^2 = \frac{\varepsilon^2 R}{( R+r)^2}, \quad \text{cuando } R = r \Rightarrow P_{max} = \frac{\varepsilon^2}{4r}$$

## Asociaciones de resistencias

- Resistencia equivalente:** es la que sustituiría en el circuito al conjunto de resistencias originales, transportando la misma corriente I y estando sometida a la misma diferencia de potencial V.
- Resistencias en serie.** Comparten la misma I, por tanto:
$$V = IR_1 + IR_2 + \cdots + IR_N = I ( R_1 + R_2 + \cdots + R_N) = IR_{eq} \Rightarrow R_{eq} = R_1 + R_2 + \cdots + R_N$$
- Resistencias en paralelo.** Comparten la misma caída de potencial V. Teniendo además en cuenta que la intensidad total es la suma de las intensidades en cada rama:
$$I = I_1 + I_2 + \cdots + I_N = \frac{V}{R_1} + \frac{V}{R_2} + \cdots + \frac{V}{R_N} = \frac{V}{R_{eq}} \Rightarrow \frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \cdots + \frac{1}{R_N}$$
- Simulador virtual de circuitos de CC:**
- HTML5: https://phet.colorado.edu/es/simulation/circuit-construction-kit-dc-virtual-lab
- Java: https://phet.colorado.edu/es/simulation/legacy/circuit-construction-kit-dc

### Ejemplo ( problema de examen)

Sea el circuito de CC de la figura. Sabiendo que por la resistencia de 32 Ω circula una intensidad de 40 mA:
a) Hallar el valor de la resistencia R.
b) Determinar la potencia que suministra o absorbe cada fuente, así como la potencia disipada entre los puntos A y C.
- Solución abreviada:*
a) La resistencia equivalente del bloque comprendido entre los puntos A y C será ( usar expresiones serie y paralelo):
$$R_{AC} = \frac{20R + 1600\ \Omega}{R + 100\ \Omega}$$
De modo que la resistencia total del circuito será:
$$R_{total} = R_{AC} + 32\ \Omega = \frac{52R + 4800\ \Omega}{R + 100\ \Omega}$$
Resulta obvio que la corriente circulará en sentido horario y la batería de la derecha recibirá corriente por su polo positivo en vez de suministrarla. Aplicando la ley de las mallas:
$$40 \cdot 10^{-3}\ A \cdot \frac{52R + 4800\ \Omega}{R + 100\ \Omega} = 14V - 12V = 2V \Rightarrow R = 100\ \Omega$$
b) Las potencias serán:
$$P_{14V} = \varepsilon \cdot I = 14V \cdot 0{,}04A = 0{,}56\ W \text{ ( suministrada)}$$
$$P_{12V} = \varepsilon \cdot I = 12V \cdot 0{,}04A = 0{,}48\ W \text{ ( absorbida)}$$
$$P_{AC} = R_{AC} \cdot I^2 = 18\ \Omega \cdot ( 0{,}04\ A)^2 = 0{,}0288\ W$$
Comprobación de balance de potencias: $0{,}56 = 0{,}0288 + 32 \cdot 0{,}04^2 + 0{,}48$ ( aprox.)

### Ejercicio

Un conductor A está formado uniendo extremo contra extremo dos barras prismáticas de 0,5 m de longitud, una de hierro y otra de cobre, ambas de sección cuadrada de 0,8 cm de lado. Otro conductor B consiste en dos barras unidas lateralmente, una de cobre y otra de hierro, ambas de 1 m de longitud y sección 0,4×0,8 cm:
a) Hallar la resistencia de los conductores A y B.
b) ¿En cuál de los dos conductores componentes se disipará mayor potencia si sometemos al conductor A a una diferencia de potencial ∆V?
c) ¿Y si lo hacemos con el conductor B?
Datos: resistividades a temperatura ambiente: $\rho_{Fe} = 10{,}0 \cdot 10^{-6}\ \Omega\text{cm}$, $\rho_{Cu} = 1{,}77 \cdot 10^{-6}\ \Omega\text{cm}$.
- Solución abreviada:*
a) Aplicando directamente la definición de resistencia a cada componente, pasando todas las unidades al SI, y teniendo en cuenta que el montaje A es en serie y el B en paralelo:
- Conductor A ( serie):**
$$R_{Fe} = \frac{\rho_{Fe} L}{S} = \frac{10 \cdot 10^{-8}\ \Omega m \cdot 0{,}5\ m}{0{,}008^2\ m^2} = 0{,}78 \cdot 10^{-3}\ \Omega$$
$$R_{Cu} = \frac{\rho_{Cu} L}{S} = \frac{1{,}77 \cdot 10^{-8}\ \Omega m \cdot 0{,}5\ m}{0{,}008^2\ m^2} = 0{,}14 \cdot 10^{-3}\ \Omega$$
$$\Rightarrow R_{AC} = R_{Fe} + R_{Cu} = 9{,}2 \cdot 10^{-4}\ \Omega$$
- Conductor B ( paralelo):**
$$R_{Fe} = \frac{\rho_{Fe} L}{S} = \frac{10 \cdot 10^{-8}\ \Omega m \cdot 1\ m}{0{,}004 \cdot 0{,}008\ m^2} = 3{,}125 \cdot 10^{-3}\ \Omega$$
$$R_{Cu} = \frac{\rho_{Cu} L}{S} = \frac{1{,}77 \cdot 10^{-8}\ \Omega m \cdot 1\ m}{0{,}004 \cdot 0{,}008\ m^2} = 5{,}53 \cdot 10^{-4}\ \Omega$$
$$\Rightarrow R_B = \frac{R_{Fe} \cdot R_{Cu}}{R_{Fe} + R_{Cu}} = 4{,}7 \cdot 10^{-4}\ \Omega$$
Nótese cómo $R_B$ es menor que las resistencias componentes.
b) Montaje serie. Circula la misma I por ambos conductores. Expresamos P en función de I:
$$P = VI = RI^2 \Rightarrow P_{Fe} = R_{Fe}I^2; \quad P_{Cu} = R_{Cu}I^2$$
Como $R_{Fe} > R_{Cu} \Rightarrow P_{Fe} > P_{Cu}$: a una I dada, el Fe disipa más calor porque conduce peor la electricidad.
c) Montaje paralelo. Ambos conductores están sometidos a la misma V. Expresamos P en función de V:
$$P = VI = \frac{V^2}{R} \Rightarrow P_{Fe} = \frac{V^2}{R_{Fe}}; \quad P_{Cu} = \frac{V^2}{R_{Cu}}$$
Como $R_{Fe} > R_{Cu} \Rightarrow P_{Fe} < P_{Cu}$: a una V dada, el Fe disipa menos calor porque conduce peor la electricidad y esto supone menos paso de corriente.

## Elementos de un circuito

- Elemento:** componente con dos ( o más) bornes ( terminales) que forma parte del circuito. Por ejemplo, una resistencia.
- Conductor:** hilo que une los componentes en un circuito y que se considera de resistencia despreciable.
- Rama:** unión de elementos de un circuito formando un conjunto con solo dos terminales.
- Malla:** trayectoria cerrada por la unión de varias ramas.
- Nudo ( o nodo):** es el punto de conexión entre dos o más ramas ( donde concurren 3 o más conductores). Se representa normalmente mediante un punto.

## Reglas de Kirchhoff

Permiten abordar la resolución de circuitos complejos compuestos por varias mallas. La primera ley se refiere a intensidades y la segunda a voltajes.
- Ley de los nudos:** la suma de las intensidades que concurren en un nudo es igual a cero. Básicamente es una consecuencia de la conservación de la carga: si la carga no se destruye ni se crea en el nudo, el balance total de corriente entrante debe ser igual al de corriente saliente.
- Ley de las mallas:** la suma algebraica de fuerzas electromotrices en un bucle cerrado ( malla) es equivalente a la suma algebraica de caídas de potencial en dicha malla. Es una consecuencia de la conservación de la energía.
Formulación matemática:
Ley de los nudos: $\displaystyle\sum_{i=1}^{N} I_i = I_1 + I_2 + \cdots + I_n = 0$, siendo N el número de hilos que concurren en el nudo. Ejemplo: $-I_1 + I_2 + I_3 = 0$
Ley de las mallas: $\displaystyle\sum_{i=1}^{N} V_i = \sum_{i=1}^{N} \varepsilon_i \Rightarrow \sum_{i=1}^{N} R_i \cdot I_i = \sum_{i=1}^{N} \varepsilon_i$. Ejemplo: $R_2 I_2 + R_3 I_3 = \varepsilon_2$

## Resolución práctica de circuitos de C.C.

1) Identificar cada rama "i" y asignar un sentido arbitrario a las intensidades "$I_i$" que circulan por cada una de ellas.
2) Identificar los nudos y plantear la primera regla de Kirchhoff asignando signo negativo a intensidades salientes y signo positivo a intensidades entrantes. Nótese que no hace falta plantear todos los nudos puesto que una de las ecuaciones será redundante.
3) Identificar las mallas. Definir un sentido arbitrario para la intensidad circulante en cada malla. Formular la segunda regla de Kirchhoff para cada malla, teniendo en cuenta el siguiente criterio de signos para las caídas de potencial "$R_i \cdot I_i$" y las f.e.m. "$\varepsilon_i$":
- $\varepsilon_i$ es positiva si la intensidad es entrante en la parte negativa de la fuente y saliente en la parte positiva. En caso contrario es negativa.
- $R_i \cdot I_i$ es positiva si $I_i$ sigue el sentido arbitrario definido al marcar la malla y negativa en caso contrario.
4) Resolver el sistema de ecuaciones resultantes. Nótese que si se formulan todas las mallas posibles, habrá ecuaciones redundantes. Las mallas que son la composición de otras no aportan información nueva.
Recordar que la elección del sentido de la intensidad en cada rama y el sentido de circulación considerado positivo en cada malla son una elección arbitraria PERO una vez seleccionados hay que marcar los signos de forma consecuente en las ecuaciones de nodos y mallas.
- Ejemplos de signos para las ecuaciones de las mallas:** $I_1$ e $I_5$ serían negativas por ir dirigidas contra el sentido considerado positivo en la malla ( flecha circular roja); $I_3$ sería positiva al ir a favor; $I_0$, $I_3$ e $I_4$ serían negativas al ir contra el sentido considerado positivo ( flecha roja). La fem $\varepsilon$ se escribiría en el miembro derecho de la ecuación con signo positivo, ya que el sentido de la circulación definido por la flecha roja sale del polo positivo y entra en el negativo.

### Ejemplo

En el circuito de la figura la f.e.m. de la pila es de 6 V y su resistencia interna de 10 Ohmios. Las resistencias $R_1$, $R_2$, $R_3$, $R_4$ y $R_5$ valen respectivamente 100, 200, 300, 400 y 500 Ohmios. Hallar la potencia disipada en la red y su resistencia equivalente.
- Nodos.** Hasta 4 ecuaciones, una de ellas redundante. Formularemos solo 3 de ellas:
$$I_1 + I_2 - I_5 = 0$$
$$-I_0 - I_2 + I_4 = 0$$
$$I_3 - I_4 + I_5 = 0$$
- Mallas.** Hasta 7 ecuaciones, solo necesitamos 3 ( las mallas compuestas proporcionan ecuaciones redundantes). Nótese que esta fem aparecería como positiva al formular la segunda regla de Kirchhoff ( la flecha circular roja "sale" del positivo y entra en el negativo):
$$200 I_2 + 400 I_4 + 500 I_5 = 0$$
$$-100 I_1 + 300 I_3 - 500 I_5 = 0$$
$$-10 I_0 - 300 I_3 - 400 I_4 = 6$$
Combinando nudos y mallas obtenemos un sistema de 6 ecuaciones con 6 incógnitas:
$$I_1 + I_2 - I_5 = 0$$
$$-I_0 - I_2 + I_4 = 0$$
$$I_3 - I_4 + I_5 = 0$$
$$200 I_2 + 400 I_4 + 500 I_5 = 0$$
$$-100 I_1 + 300 I_3 - 500 I_5 = 0$$
$$-10 I_0 - 300 I_3 - 400 I_4 = 6$$
- Solución:* El sentido real de las corrientes será:
- $I_0 = -27{,}3\ mA$
- $I_1 = -19{,}6\ mA$
- $I_2 = +18{,}8\ mA$
- $I_3 = -7{,}8\ mA$
- $I_4 = -8{,}5\ mA$
- $I_5 = -0{,}74\ mA$
- Resistencia equivalente:** $\varepsilon = ( R_{eq} + r) I_0 \Rightarrow R_{eq} = 208{,}4\ \Omega$
- Potencia disipada:** $P = \varepsilon \cdot I_0 = 0{,}165\ W$
Además se puede comprobar que P también es igual a la suma de potencias disipadas en cada rama ( suma de los productos $R_i \cdot I_i^2$).

## Apéndice: solución de un sistema de ecuaciones usando MS Excel

`=MINVERSA ( B18:G23)`
`=TRANSPONER ( MMULT ( J18:O23;H18:H23))`

## Apéndice: otros elementos de análisis de circuitos

- Principio de superposición:** Si en una red lineal existen dos o más fuentes, la intensidad que circula por el circuito será la suma de las intensidades que produciría cada una de ellas si sólo existiera ella en el circuito.
Procedimiento práctico:
- Resolver ambos circuitos por separado, hallando las intensidades en cada rama en cada uno de ellos.
- Sumar las intensidades de ambos circuitos ( con su signo) para hallar la intensidad resultante en el circuito combinado.
- Resistencia de entrada de una red.** Es la resistencia equivalente que "vería" una fuente de f.e.m. conocida ε conectada a los bornes de dicha red. Si no conocemos los componentes de la red, se puede calcular midiendo la intensidad I y usando la ley de Ohm: $R = \varepsilon / I$.
- Teorema de Thévenin:** Una parte de un circuito activo entre dos terminales se comporta como un circuito equivalente compuesto únicamente por una fuente y cierta resistencia en serie llamada resistencia de salida.
- Teorema de Norton:** Similar al teorema de Thévenin, pero el circuito equivalente consta de una fuente y una resistencia en paralelo con ella.
