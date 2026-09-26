---
title: "Magnetismo en el vacío"
---

# Tema 4: Magnetismo en el vacío

Física ( 780000). Grado en Ingeniería de Computadores ( grupo 1ºA, lunes mañana). Curso 2020/2021 – Primer Cuatrimestre. R. Gómez Herrero. Departamento de Física y Matemáticas.

## Magnetismo. Polos magnéticos

Las primeras nociones históricas sobre la existencia del magnetismo derivaron de las observaciones de los fenómenos de atracción y repulsión del hierro por ciertos minerales ( imanes permanentes, ya conocidos por los antiguos griegos en el siglo VI o VII a.C.). El nombre deriva de la región griega de Magnesia, donde se podía hallar minerales que contienen magnetita.
Igualmente se comprobó que una aguja magnetizada tiende a orientarse en dirección Norte-Sur, debido a la existencia de un campo magnético terrestre ( fundamento de la brújula). En el siglo XII ya hay evidencia del uso de brújulas en China, invento que posteriormente se generalizó entre los navegantes europeos.
Existen dos tipos de polos magnéticos. Polos iguales se repelen y polos diferentes se atraen, pero a diferencia de lo que ocurre con las cargas, no es posible aislarlos ( un imán partido por la mitad sigue constando de dos polos):
- Polo norte magnético: líneas de campo salientes.
- Polo sur magnético: líneas entrantes.
Desde el siglo XIX se comprobó que el magnetismo guarda estrecha relación con las cargas en movimiento, comprobándose que las corrientes generan campos magnéticos ( Oersted, 1820) y la existencia de fuerzas magnéticas entre corrientes.
( Visualización de las líneas de campo alrededor de un imán permanente usando limaduras de hierro esparcidas sobre un papel colocado sobre el imán.)
Actualmente el polo norte geográfico de la Tierra es un polo sur magnético ( el polo norte de una aguja imantada apunta aproximadamente al norte geográfico, que tiene polaridad magnética sur). Los polos magnéticos y geográficos no coinciden exactamente. A escala geológica se producen inversiones de la polaridad magnética terrestre.

## El campo B. Líneas de campo

Los campos magnéticos se suelen caracterizar por un campo vectorial $\vec{B}$, conocido también como vector inducción magnética o densidad de flujo magnético, que en muchas ocasiones es mencionado simplemente como "campo magnético".
Al igual que con el campo eléctrico, podemos trazar líneas del campo magnético. De forma semejante a lo que vimos para el campo $\vec{E}$, el vector $\vec{B}$ en todo punto es tangente a las líneas de campo. La densidad de líneas es proporcional al módulo de $\vec{B}$ ( líneas más separadas significan campo menos intenso y líneas más juntas significan campo más intenso).
Dado que no existen monopolos magnéticos, las líneas de campo magnético siempre forman bucles cerrados ( emergen del polo N y acaban en el polo S). Esto es una diferencia importante con respecto a las líneas del campo eléctrico.
( Líneas de campo magnético alrededor de un imán permanente. Nótese su carácter cerrado, en contraste con lo visto anteriormente para el campo eléctrico.)
Como veremos a continuación, los campos magnéticos ejercen fuerzas sobre cargas en movimiento. Otra diferencia importante con el campo eléctrico es que las líneas del campo $\vec{B}$ son perpendiculares a la fuerza magnética sobre una carga puntual ( en el caso del campo eléctrico, las líneas de campo eran paralelas a la fuerza).

## Cargas en movimiento: fuerza de Lorentz

La evidencia experimental muestra que una carga q moviéndose a una velocidad $\vec{v}$ en el seno de un campo magnético $\vec{B}$ experimenta una fuerza conocida como fuerza de Lorentz que cumple:
- Es directamente proporcional a q y a v.
- Está dirigida en perpendicular al plano que contiene a $\vec{v}$ y a $\vec{B}$.
- Desaparece cuando $\vec{v}$ y $\vec{B}$ son paralelos.
- Se hace máxima cuando $\vec{v}$ y $\vec{B}$ son perpendiculares.
- Se invierte si cambiamos el signo de la carga.
Las observaciones citadas se pueden resumir en la siguiente ecuación, que describe el módulo y dirección de la fuerza de Lorentz:
$$\vec{F} = q\vec{v} \times \vec{B}$$
Nótese que para q negativa, la fuerza sería hacia abajo ( siendo θ el ángulo entre $\vec{v}$ y $\vec{B}$).
Si la velocidad y el campo B forman un ángulo θ, el módulo de la fuerza de Lorentz será:
$$F = qvB\sin\theta$$
En caso de existir además un campo eléctrico E, tendríamos:
$$\vec{F} = q\vec{E} + q\vec{v}\times\vec{B} = q (\vec{E} + \vec{v}\times\vec{B})$$

## Movimiento de una carga en un campo magnético

A partir de la fuerza de Lorentz se puede comprobar que una carga q en un campo magnético en general describirá una trayectoria helicoidal. La carga cambia de dirección pero no gana energía ( los campos magnéticos no realizan trabajo sobre las cargas).
Velocidad de la carga: $\vec{v} = \vec{v}_\perp + \vec{v}_\parallel$
La componente paralela al campo, $v_\parallel$, no sufre fuerza de Lorentz. La componente perpendicular al campo, $v_\perp$, sufrirá una fuerza que provoca que la carga describa órbitas circulares de radio r ( radio de Larmor) tal que:
$$F = qv_\perp B = \frac{mv_\perp^2}{r} \Rightarrow r = \frac{mv_\perp}{qB} \quad \text{( crece con } v_\perp\text{)}$$
Periodo ciclotrón: $\displaystyle T = \frac{2\pi r}{v_\perp} = \frac{2\pi m}{qB}$
Frecuencia ciclotrón ( independiente de v): $\displaystyle f = \frac{1}{T} = \frac{qB}{2\pi m}$

## Unidades de B

La unidad de B en el sistema internacional es el Tesla ( T). Se define 1 T como un campo tal que una carga de 1 C moviéndose con v = 1 m/s experimente una fuerza de 1 N:
$$1\ T = 1\ N\cdot s\cdot C^{-1} m^{-1} = 1\ N\ A^{-1} m^{-1} = 1\ kg\ C^{-1} s^{-1}$$
Un campo de 1 T es bastante grande, por lo que habitualmente se emplean submúltiplos del tesla para medir campos cotidianos. Otra unidad muy habitual es el Gauss ( G), que es la unidad de B en el sistema cgs y se relaciona con el tesla por:
$$1\ G = 10^{-4}\ T$$
Por ejemplo, el campo magnético terrestre en España es del orden de 40 µT ( se puede medir de forma aproximada con un simple smartphone).

## Fuerza de Lorentz – Ejemplos

- Ejercicio:** Un protón se mueve perpendicularmente a un campo magnético de 4000 G describiendo una órbita circular de radio 21 cm. Determinar el periodo de la órbita y la velocidad del protón. Datos: $m_p = 1{,}67\cdot10^{-27}$ kg, $q_p = e = 1{,}6\cdot10^{-19}$ C.
- Solución:* Realizaremos todos los cálculos en SI, por tanto: R = 0,21 m, B = 4000·10⁻⁴ T = 0,4 T. Ahora empleamos las expresiones del radio de Larmor y el periodo:
$$T = \frac{2\pi m}{qB} = \frac{2\pi \cdot 1{,}67\cdot10^{-27}\ kg}{1{,}6\cdot10^{-19}\ C \cdot 0{,}4\ T} = 1{,}6\cdot10^{-7}\ s$$
$$r = \frac{mv_\perp}{qB} \Rightarrow v = \frac{rqB}{m} = \frac{0{,}21m \cdot 1{,}6\cdot10^{-19}C \cdot 0{,}4T}{1{,}67\cdot10^{-27}kg} = 8{,}05\cdot10^{6}\ m/s$$
Nótese que el radio de giro es directamente proporcional a la velocidad, pero el periodo solo depende de q, B y m, de modo que no variará aunque la carga se mueva a distinta velocidad.
Comprobación de unidades: $1\ T = 1\ kg\ C^{-1}s^{-1} \Rightarrow 1\ kg\ C^{-1}T^{-1} = 1\ kg\ C^{-1}\ kg^{-1}Cs = 1\ s$; y $1\ m\ C\ T\ kg^{-1} = 1\ m\ C\ kg\ C^{-1} s^{-1} kg^{-1} = 1\ m\ s^{-1}$.
Si además de un campo magnético hay uno eléctrico, habrá que tener en cuenta la fuerza de Coulomb:
$$\vec{F} = q\vec{v}\times\vec{B} + q\vec{E} = q (\vec{v}\times\vec{B} + \vec{E})$$
Simulaciones interactivas:
1) Solo campo magnético perpendicular: http://surendranath.org/GPA/Electricity/MCMF/MCMF.html
2) Campo eléctrico y magnético: http://surendranath.org/GPA/Electricity/MCEMF/MCEMF.html
- Ejercicio:** Un electrón pasa sin desviarse a través de la región comprendida entre dos placas plano-paralelas en la que existe un campo eléctrico de 3000 V/m y un campo magnético cruzado de 1,4 G. Si las placas tienen 4 cm de longitud y se sitúa una pantalla en vertical a 30 cm de ellas, calcular la desviación que sufre el electrón respecto a su eje de entrada en la pantalla al interrumpir el campo magnético. ( Masa del electrón: 9,11·10⁻³¹ kg.) Véase también el ejercicio 1 de la hoja de problemas.
Datos del montaje: tramo A, $d_A = 0{,}04$ m; tramo B, $d_B = 0{,}30$ m. Campo eléctrico $\vec{E} = -3000\ \vec{\jmath}$ V/m ( dirigido hacia abajo para q<0). Campo magnético $\vec{B} = -1{,}4\cdot10^{-4}\ \vec{k}$ T ( dirigido hacia arriba para q<0).
- Solución abreviada:*
1) Igualar la fuerza de Coulomb y la de Lorentz y despejar v, teniendo en cuenta que $\vec{v}\times\vec{B}$ tiene sentido $q\vec{E}$:
$$qE = -qvB \Rightarrow E = -vB \Rightarrow v = -\frac{E}{qB} = 2{,}14\cdot10^{7}\ m/s = 0{,}07c$$
2) Tramo A: movimiento rectilíneo uniforme en dirección X y uniformemente acelerado en dirección Y. Tramo B: rectilíneo uniforme en X e Y. $v_x$ = cte en todo el trayecto = $2{,}14\cdot10^7$ m/s.
$$t_A = \frac{d_A}{v_x} = 1{,}87\cdot10^{-9}\ s \qquad t_B = \frac{d_B}{v_x} = 1{,}4\cdot10^{-8}\ s$$
$$a_y = \frac{qE}{m_e} = 5{,}27\cdot10^{14}\ m/s^2 \qquad v_{yA} = a_y \cdot t_A = 1{,}87\cdot10^{5}\ m/s$$
$$\Delta y_A = \frac{1}{2} a_y t_A^2 = 9{,}2\cdot10^{-4}\ m$$
$$\Delta y_B = v_{yA} \cdot t_B = 0{,}014\ m$$
$$\Rightarrow \Delta y = \Delta y_A + \Delta y_B = 0{,}015\ m = 15\ mm$$

## Fuerza de Lorentz – Efecto Hall ( E. Hall, 1879)

Si un conductor transportando corriente es sumergido en un campo magnético, los portadores experimentarán la fuerza de Lorentz. Dicha fuerza provocará una concentración de cargas opuestas en caras opuestas del conductor, y por tanto una diferencia de potencial medible.
Ejemplo: campo B hacia fuera del papel, intensidad hacia la derecha.
- Si los portadores son positivos: v hacia la derecha, F hacia abajo, la carga positiva se concentra abajo.
- Portadores negativos: v hacia la izquierda, F hacia abajo, la carga negativa se concentraría abajo.
En ambos casos aparece una diferencia de potencial, pero los signos son opuestos. ( Fuente: https://youtu.be/Scpi91e1JKc — azul: portadores negativos.)
El diferente comportamiento para portadores positivos y negativos puede usarse para probar experimentalmente la naturaleza de los portadores en metales y en semiconductores. Posee muchas aplicaciones tecnológicas, por ejemplo en la construcción de sensores de campo magnético para smartphones ( brújula electrónica), sensores que detectan el cierre de cubiertas de smartphones portátiles, o mandos rotatorios sin contacto físico.

## Fuerza magnética sobre un hilo de corriente

Una corriente I está constituida por cargas en movimiento. Si la sumergimos en un campo magnético, cada una de ellas experimentará la fuerza de Lorentz, de forma que habrá una fuerza neta sobre el conductor.
Sea un hilo recto de longitud L por el que circula una intensidad I. Si la sección del hilo es S y hay n portadores de carga por unidad de volumen, cada uno con velocidad v y carga q, la fuerza neta sobre el hilo será:
$$\vec{F} = q_{total}\vec{v}\times\vec{B} = q \cdot n \cdot S \cdot L\ (\vec{v}\times\vec{B})$$
Como vimos en el tema anterior, la corriente que circula por el hilo viene dada por $I = n\cdot q\cdot S\cdot v$, de modo que si expresamos L como un vector según la dirección de v podemos reescribir:
$$\vec{F} = I (\vec{L}\times\vec{B})$$
En términos generales, por ejemplo si el hilo no es recto o B varía, solo podemos escribir la ecuación anterior para tramos infinitesimales del cable, con longitud dl, los cuales experimentan una fuerza dF dada por ( elemento de corriente $I d\vec{l}$):
$$d\vec{F} = I\,d\vec{l}\times\vec{B}$$

## Fuerza magnética sobre una espira de corriente

Consideremos ahora una espira rectangular. Podemos tratar por separado los 4 lados como hilos de corriente para hallar la fuerza neta al sumergirla en un campo B que forma un ángulo φ con la normal a la espira ( ver figura).
Las fuerzas sobre los lados 1 y 3 son iguales y de sentido opuesto. Se cancelan y además no ejercen momento sobre la espira.
Las fuerzas sobre los lados 2 y 4 son iguales y de sentido opuesto. También se cancelan pero ejercen un par sobre la espira que provocará su giro:
$$F_2 = F_4 = IaB$$
$$M = M_2 + M_4 = IaB\frac{b}{2}\sin\phi + IaB\frac{b}{2}\sin\phi = IabB\sin\phi = ISB\sin\phi$$
Siendo S = a·b el área de la espira. Supongamos ahora que en vez de una sola espira tenemos N espiras superpuestas ( espira con N vueltas). El módulo del momento total será:
$$M = NISB\sin\phi$$
- Regla de la mano izquierda ( ejemplo 1):** apuntar dedo medio ( I) hacia adentro, dedo índice ( B) hacia arriba, dedo pulgar ( F) hacia la derecha.
- Regla de la mano izquierda ( ejemplo 2):** apuntar dedo medio ( I) hacia uno mismo, dedo índice ( B) hacia arriba, dedo pulgar ( F) hacia la izquierda.

## Momento magnético

Basándonos en el resultado anterior, podemos definir un nuevo vector llamado momento magnético $\vec{\mu}$, dado por:
$$\vec{\mu} = NIS\,\hat{n}$$
siendo $\hat{n}$ un vector unitario normal a la superficie de la espira ( sentido dado por la regla del tornillo aplicada a la intensidad). Las unidades de µ son A·m².
De este modo, el momento de las fuerzas sobre la espira se puede expresar como:
$$\vec{M} = \vec{\mu}\times\vec{B}$$
( Notaciones habituales alternativas: $\vec{\mu} \to \vec{m}$, $\vec{M} \to \vec{\tau}$.)
El resultado obtenido para la espira rectangular se puede generalizar a cualquier otra forma geométrica: una espira de corriente sumergida en un campo magnético sufre un momento que trata de reorientarla, haciendo que ésta gire. El momento solo se anula si el campo B y el momento magnético de la espira son paralelos ( es decir, si el campo B es perpendicular a la espira).
- ( Nótese la analogía con el comportamiento de un dipolo eléctrico sumergido en un campo eléctrico E: el momento dipolar tiende a alinearse con el campo.)*
Recordatorio del significado del momento $\vec{\tau}$ ( M en la figura) de una fuerza F aplicada en $\vec{r}$ y su relación con el movimiento de rotación del sistema:
$$\frac{d\vec{L}}{dt} = \vec{r}\times\frac{d\vec{p}}{dt} = \vec{r}\times\vec{F} = \vec{\tau}$$
( Referencia: http://hyperphysics.phy-astr.gsu.edu/hbasees/tord.html)
Obsérvese cómo el momento $M = \vec{\mu}\times\vec{B}$ ($\vec{\tau}$ en la animación) solo se anula cuando $\vec{\mu}$ está alineado con $\vec{B}$, y se hace máximo cuando son perpendiculares. ( Nota: la animación muestra los vectores para distintas orientaciones posibles de la espira, no el movimiento que adquiere la espira a partir de la situación inicial. https://www.youtube.com/user/mrg3/videos)
- Analogía del dipolo magnético en un campo B con el dipolo eléctrico en un campo E:** una espira ( dipolo magnético con momento magnético $\vec{\mu}$) puede hacerse equivaler a un imán permanente, que a su vez guarda importantes analogías con el dipolo eléctrico visto en el tema de electrostática ( importante para el estudio de medios materiales).
- Dipolo eléctrico: momento $\vec{p}$, campo $E$ entrante, dipolo gira en sentido horario para orientarse a favor de E aplicado: $M = \vec{p}\times\vec{E}$
- Dipolo magnético: momento $\vec{\mu}$, campo $B$ entrante, dipolo gira en sentido horario para orientarse a favor de B aplicado: $M = \vec{\mu}\times\vec{B}$
El caso del giro del dipolo eléctrico es más sencillo de visualizar en términos de fuerza de Coulomb sobre las cargas componentes. En el caso del dipolo magnético habría que visualizar las fuerzas magnéticas sobre, por ejemplo, los lados de una espira cuadrada.
- Ejercicio:** Una espira rectangular de 5,40 × 8,50 cm está formada por 25 vueltas de cable. La espira transporta una corriente de 15 mA. Calcular el par de fuerzas que se ejerce sobre la espira cuando se le aplica un campo magnético uniforme de valor 0,350 T paralelo al plano de la espira. Determinar el momento magnético de la espira.
- Solución abreviada:*
Área de la espira: $S = 8{,}50\cdot10^{-2}\cdot 5{,}40\cdot10^{-2}\ m^2 = 4{,}59\cdot10^{-3}\ m^2$
Por definición de momento magnético, éste será perpendicular a la espira y con módulo:
$$\mu = NSI = 25 \cdot 0{,}015 \cdot 4{,}59\cdot10^{-3}\ Am^2 = 1{,}72\cdot10^{-3}\ A\,m^2$$
El momento de las fuerzas magnéticas sobre la espira tendrá módulo:
$$M = \mu B = 1{,}72\cdot10^{-3}\cdot0{,}350\ Am^2 T = 6{,}02\cdot10^{-4}\ Nm$$
El vector $\vec{\mu}$ será perpendicular a la espira dirigido hacia fuera. El vector $\vec{M}$ estará dirigido hacia arriba, de modo que la espira tenderá a girar hundiendo su parte derecha y levantando la izquierda. El movimiento se puede visualizar también usando simplemente la fuerza de Lorentz. Nótese que no hemos necesitado conocer cuál es cada uno de los lados de la espira, pues solo importa el área.

## Ejemplos de fuerzas sobre espiras

- Motor eléctrico CC: https://youtu.be/aMH7pdn-qr4
- Motor homopolar: https://www.youtube.com/watch?v=yUToL9WAK8I y https://www.youtube.com/watch?v=LcyqJWvZioM

## Campo creado por cargas en movimiento

Las cargas en movimiento no solo sufren el efecto de los campos magnéticos ( fuerza de Lorentz) sino que además ellas mismas son fuentes de campo magnético.
El campo B creado por una carga q que se mueve con velocidad $\vec{v}$, evaluado en una posición $\vec{r}$, viene dado por:
$$\vec{B} = \frac{\mu_0}{4\pi}\frac{q\vec{v}\times\hat{u}_r}{r^2} = \frac{\mu_0}{4\pi}\frac{q\vec{v}\times\vec{r}}{r^3}$$
siendo $\mu_0$ una constante llamada permeabilidad magnética del vacío, cuyo valor numérico es:
$$\mu_0 = 4\pi\cdot10^{-7}\ T\,m\,A^{-1} = 4\pi\cdot10^{-7}\ N\,A^{-2}$$
Para un elemento de corriente, dado que $q_{portador}\cdot\vec{v} = n\cdot q\cdot S\cdot d\vec{l} = I\,d\vec{l}$, tendríamos que el campo creado es ( Ley de Biot-Savart):
$$d\vec{B} = \frac{\mu_0}{4\pi}\frac{I\,d\vec{l}\times\vec{r}}{r^3}$$

## Ley de Biot-Savart

Para calcular el campo B creado por un conductor completo, podemos integrar a toda la trayectoria a lo largo del conductor.
- Caso particular 1:** campo B creado por una espira circular C de radio R, para un punto situado en su centro:
$$dB = \frac{\mu_0 I \cdot dl \cdot \sin (\pi/2)}{4\pi R^2}$$
$$\Rightarrow B = \frac{\mu_0}{4\pi}\int_C \frac{I\,dl}{R^2} = \frac{\mu_0 I}{4\pi R^2}\int_C dl = \frac{\mu_0 I \cdot 2\pi R}{4\pi R^2}$$
$$B = \frac{\mu_0 I}{2R}$$
El vector B estará dirigido a lo largo del eje, con sentido dado por la regla del tornillo aplicada a $d\vec{l}\times\vec{r}$ ( en el caso del dibujo: hacia fuera).
- Caso particular 2:** campo B creado por un hilo recto infinito, para un punto situado a cierta distancia d del hilo:
Con $d = r\cos\alpha \Rightarrow r = d/\cos\alpha$, y $h = r\sin\alpha = d\tan\alpha \Rightarrow dl = dh = d\,d\alpha/\cos^2\alpha$:
$$dB = \frac{\mu_0}{4\pi}\frac{I\,dl\cdot r\sin (\alpha+\pi/2)}{r^3} = \frac{\mu_0}{4\pi}\frac{I\cos\alpha\,dl}{r^2} = \frac{\mu_0}{4\pi}\frac{\cos\alpha\,Id\,d\alpha}{d^2}$$
$$B = \frac{\mu_0 I}{4\pi d}\int_{-\pi/2}^{+\pi/2}\cos\alpha\,d\alpha = \frac{\mu_0 I}{4\pi d}\cdot 2$$
$$B = \frac{\mu_0 I}{2\pi d}$$
El vector B según la regla del tornillo aplicada a $d\vec{l}\times\vec{r}$ ( hacia dentro).
- Aplicación tecnológica:** amperímetros sin contacto ( pinza amperimétrica). Para corriente alterna pueden basarse en inducción en vez de en efecto Hall.
- Ejercicio:** Considere una espira circular de cable, de radio R, situada en el plano XY, por la que circula una corriente estacionaria I. Determinar el campo magnético en un punto P situado en el eje de la espira ( Z) a una distancia z cualquiera del centro de la espira.
Las componentes en el plano perpendicular a z se cancelan, puesto que cada elemento de longitud tiene una contrapartida en sentido contrario ( ver $dB_x$ en el caso de la figura). Las $dB_z$ se suman. Integrando a toda la espira ( R y z son constantes):
$$B_z = \frac{\mu_0 I\cdot 2\pi R\cdot R}{4\pi ( z^2+R^2)^{3/2}} = \frac{\mu_0 I R^2}{2 ( z^2+R^2)^{3/2}}$$
Si estamos muy lejos de la espira, $z \gg R \Rightarrow$:
$$B_z = \frac{\mu_0 I R^2}{2z^3} = \frac{\mu_0 m}{2\pi z^3}$$
siendo m el momento magnético de la espira: $m = \pi R^2 \cdot I$ ( analogía con expresión dipolo eléctrico).
Fuente: http://hyperphysics.phy-astr.gsu.edu/hbase/magnetic/curloo.html. Ver también simulación interactiva en http://surendranath.org/GPA/Electricity/MFACC/MFACC.html y bobinas de Helmholtz en http://surendranath.org/GPA/Electricity/MFACC/Helmholtz.html.

## Fuerza entre dos elementos de corriente

Si colocamos uno frente a otro dos elementos de corriente $I_1 d\vec{l}_1$ e $I_2 d\vec{l}_2$, las cargas en movimiento del segundo sufrirán el efecto del campo B creado por las cargas en movimiento del primero, y viceversa.
Recordando la fuerza sobre un elemento de corriente y sustituyendo el campo B por su expresión según la ley de Biot-Savart:
$$d\vec{F}_2 = I_2\,d\vec{l}_2\times\vec{B}_{12}, \qquad \vec{B}_{12} = \frac{\mu_0}{4\pi}\frac{I_1\,d\vec{l}_1\times\vec{r}_{12}}{r_{12}^3}$$
$$d^2\vec{F}_2 = \frac{\mu_0}{4\pi}I_1I_2\,d\vec{l}_2\times\frac{d\vec{l}_1\times\hat{u}_{12}}{r_{12}^2}$$

### Ejemplo: fuerza por unidad de longitud entre dos hilos paralelos e infinitos

Recorridos por intensidades $I_1$ e $I_2$ y separados por una distancia d. El segundo hilo verá el campo B creado por el primero. Como vimos anteriormente:
$$d\vec{F}_2 = I_2\,d\vec{l}_2\times\vec{B}_1$$
Sustituyendo y teniendo en cuenta que $B_1$ es perpendicular al hilo 2 en todos sus puntos: $B_1 = \dfrac{\mu_0 I_1}{2\pi d}$.
La fuerza por unidad de longitud sobre el hilo 2 será:
$$dF_2 = \frac{\mu_0 I_1 I_2}{2\pi d}\,dl_2 \quad\Rightarrow\quad \frac{dF_2}{dl_2} = \frac{\mu_0 I_1 I_2}{2\pi d}$$
La fuerza es atractiva si las intensidades van en la misma dirección y repulsiva si van en dirección opuesta.
Demostración experimental: https://youtu.be/43AeuDvWc0k

## Definición de amperio ( A)

El resultado del ejemplo anterior se puede utilizar para dar una definición experimental del amperio ( unidad de corriente S.I.):
$$\frac{dF_2}{dl_2} = \frac{\mu_0 I_1 I_2}{2\pi d}$$
Podemos definir 1 A como aquella corriente tal que la fuerza por unidad de longitud entre dos hilos paralelos de corriente separados por una distancia de 1 m vale $2\cdot10^{-7}$ N/m:
$$\frac{dF_2}{dl_2} = \frac{4\pi\cdot10^{-7}\ T\,m\,A^{-1}\cdot 1\cdot 1\,A^2}{2\pi\cdot 1} = 2\cdot10^{-7}\ N/m$$

## Flujo del campo magnético

Las líneas del campo magnético son siempre trayectorias cerradas, por tanto el flujo del campo magnético B a través de cualquier superficie cerrada Σ es nulo, ya que todas las líneas salientes vuelven a cruzar la superficie como líneas entrantes:
$$\phi = \oint_\Sigma \vec{B}\cdot d\vec{s} = 0 \qquad \text{( Ley de Gauss para el magnetismo)}$$
El flujo magnético en el S.I. se mide en weber: $1\ Wb = 1\ T\cdot m^2 = 1\ V\cdot s$ ( recordar que $1\ T = 1\ kg\,s^{-2}A^{-1} = 1\ V\cdot s\cdot m^{-2}$).

## Circulación de B: Ley de Ampère

La segunda ley básica del magnetismo se refiere al valor de la circulación del campo B. Para cualquier curva cerrada C que consideremos, la circulación de B es igual al producto de $\mu_0$ por la corriente I encerrada por dicho trayecto ( Ley de Ampère):
$$\oint_C \vec{B}\cdot d\vec{l} = \mu_0 I_{encerrada}$$
La ley de Ampère se emplea en magnetismo de forma análoga a la ley de Gauss en electrostática, ya que permite calcular de forma simple el campo B para distribuciones de corriente que presentan suficiente simetría.
- Aplicación a un hilo infinito de corriente.** Tomando un trayecto circular alrededor del hilo, la circulación será:
$$\oint_C \vec{B}\cdot d\vec{l} = \mu_0 I$$
Por simetría, el campo es tangencial y tiene el mismo módulo B en todos los puntos del trayecto, pudiendo entonces sacarse de la integral. Por tanto el campo en todos los puntos de la circunferencia vale:
$$B\cdot 2\pi d = \mu_0 I \Rightarrow B = \frac{\mu_0 I}{2\pi d}$$
Que coincide con lo deducido anteriormente mediante integración.
- Ejercicio:** Utilizar la ley de Ampère para hallar el campo magnético en el interior de un solenoide cilíndrico de longitud $l$ que consta de N espiras circulares recorridas por una intensidad I. Asumir que el campo exterior del solenoide es pequeño y casi paralelo al eje y que el campo en su interior es uniforme y axial.
- Solución abreviada:* Trayecto de integración con: trayecto superior ( CD), B casi nulo; trayectos laterales ( BC, DA), B casi perpendicular al trayecto; trayecto inferior ( AB), B paralelo al trayecto.
$$\oint_C \vec{B}\cdot d\vec{l} = \mu_0 I_{encerrada}$$
$$B\cdot L + 0 + 0 + 0 = \mu_0 I\cdot N \Rightarrow B = \frac{\mu_0 N I}{L} = \mu_0 n I$$
siendo N el número de espiras y $n = N/L$ el número de espiras por unidad de longitud.
- Ejercicio:** Hallar el campo B en el interior de un solenoide toroidal de radio medio R usando la ley de Ampère.
- Solución:* El proceso es análogo al anterior. Tomando el trayecto de Ampère azul de la figura:
$$B\cdot 2\pi r = \mu_0 N I \Rightarrow B = \frac{\mu_0 N I}{2\pi r}$$
De hecho el resultado es esencialmente el mismo que si consideramos el toroide como resultado de enrollar sobre sí mismo un solenoide cilíndrico de longitud $2\pi r$.
- Ejercicio:** Analizar la distribución del campo B alrededor de un cable cilíndrico coaxial con corrientes iguales pero opuestas en el conductor interior y exterior.
- Solución abreviada:* Aplicar la ley de Ampère a trayectos circulares concéntricos por separado en cuatro regiones:
- I) Dentro del hilo interior ($r < R_1$): $B ( r) = \dfrac{\mu_0 I r}{2\pi R_1^2}\,\hat{u}_\phi$
- II) Entre ambos conductores ($R_1 < r < R_2$): $B ( r) = \dfrac{\mu_0 I}{2\pi r}\,\hat{u}_\phi$
- III) Dentro del conductor exterior ($R_2 < r < R_3$): $B ( r) = \dfrac{\mu_0 I}{2\pi r}\dfrac{R_3^2 - r^2}{R_3^2 - R_2^2}\,\hat{u}_\phi$
- IV) En el exterior del cable coaxial ($r > R_3$): $B ( r) = 0$ ( el exterior queda apantallado).
Gráfico cualitativo de B frente a r, con los tramos delimitados por $R_1$, $R_2$ y $R_3$.

## Tema 4 ( Apéndices): resumen de algunos casos prácticos frecuentes

Física ( 780000). Grado en Ingeniería de Computadores ( grupo 1ºA, lunes mañana). Curso 2019/2020 – Primer Cuatrimestre. R. Gómez Herrero. Departamento de Física y Matemáticas.

### Recordatorio de reglas mnemotécnicas

- Regla de la mano izquierda ( Fleming).** Nos permite obtener la dirección y sentido del resultado de un producto vectorial. Por ejemplo, de la fuerza sobre un conductor conocidas las direcciones y sentidos de la intensidad y el vector campo magnético, o la fuerza de Lorentz conocida la velocidad y el campo magnético. Nótese que si se usa la mano derecha el orden sería al contrario ( dedo índice para el primer vector del producto vectorial).
- Regla del tornillo ( mano derecha).** Nos permite obtener la dirección de un vector resultante de un producto vectorial. El giro se debe realizar del primer al segundo vector del producto, y el pulgar indicará el sentido del resultado. También permite obtener la dirección del vector campo magnético conocida la intensidad circulante en un hilo, o la dirección del campo conocido el sentido de giro de la intensidad en un solenoide o espira.
- Norte magnético: líneas de B salientes.
- Sur magnético: líneas de B entrantes.
Nota: el polo norte geográfico de la Tierra actualmente tiene polaridad magnética sur, por ello el polo norte de una aguja magnética se orienta hacia el norte.

### Campo creado por un hilo infinito de corriente

Campo magnético creado por un hilo infinito de corriente, evaluado en un punto a cierta distancia d:
$$B = \frac{\mu_0 I}{2\pi d}\,\hat{u}_\varphi$$
Las líneas de campo son círculos alrededor del hilo. $r$ = distancia al hilo; $I$ = intensidad que circula por el hilo. El sentido del campo viene dado por la regla de la mano derecha vista desde arriba.

### Campo sobre el eje de una espira circular

Campo magnético creado por una espira de radio R, evaluado en un punto P situado a cierta distancia z de su centro y situado sobre su eje:
$$B_z = \frac{\mu_0 I R^2}{2 ( z^2+R^2)^{3/2}}\,\hat{u}_z$$
En el centro de la espira ( z = 0): $B = \dfrac{\mu_0 I}{2R}\,\hat{u}_z$
Muy lejos ( z ≫ R): $B \approx \dfrac{\mu_0 I R^2}{2z^3}\,\hat{u}_z$
La expresión es válida tomando +Z según la regla de la mano derecha aplicada a la intensidad circulante. Si la espira tuviera N vueltas en vez de solo una, basta multiplicar por N.

### Campo en el eje de un solenoide cilíndrico

Campo magnético en el interior de un solenoide cilíndrico de longitud $l$ con N espiras circulares por las que circula una intensidad I:
$$B = \mu_0 n I\,\hat{u}_z; \qquad n = N/l$$
El eje +Z está dirigido según el eje del solenoide, según la regla de la mano derecha aplicada a la intensidad circulante.

### Campo en el eje de un solenoide toroidal

Campo magnético en el interior de un solenoide toroidal de radio medio r con N espiras circulares por las que circula una intensidad I:
$$B = \frac{\mu_0 N I}{2\pi r}\,\hat{u}_\varphi$$
El vector unitario $\hat{u}_\varphi$ es tangente al círculo de radio r y está dirigido según la regla de la mano derecha aplicada a la intensidad circulante ( válido para el interior del toroide).

### Fuerza entre dos hilos de corriente

Fuerza por unidad de longitud entre dos hilos de corriente separados por una distancia d:
$$f = \frac{\mu_0 I_1 I_2}{2\pi d}$$
Si el sentido de las dos corrientes es el mismo, la fuerza es atractiva; si el sentido es opuesto, la fuerza es repulsiva.
