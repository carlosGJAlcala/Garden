---
title: "Electrostática en el vacío"
---

# Tema 1 — Electrostática en el vacío

Física ( 780000) — Grado en Ingeniería de Computadores ( grupo 1ºA, lunes mañana)
Curso 2020/2021 – Primer Cuatrimestre
R. Gómez Herrero — Departamento de Física y Matemáticas

## Carga eléctrica - triboelectricidad

Ya en la antigua Grecia, Tales de Mileto ( s. VI a.C.) observó que frotando un fragmento de ámbar (élektron en griego), éste era capaz de atraer ciertos objetos ligeros como fragmentos de plumas. Otros materiales como la lana presentan este mismo comportamiento. Esta capacidad de electrificación por contacto o fricción se denomina triboelectricidad.
Experimentos sencillos:
- Un globo o una varilla de plástico que hayan sido frotados atraen pequeños trozos de papel.
- Dos varillas de plástico que han sido frotadas y suspendidas de un hilo se repelen.
- Todos hemos sentido pequeñas descargas de electricidad estática en la vida cotidiana.
En el siglo XVI, Girolamo Cardano y William Gilbert identificaron la electrostática como un fenómeno diferente al magnetismo. Gilbert especuló que la frotación del material conducía a la pérdida de algún tipo de fluido.
En el siglo XVIII, B. Franklin, apoyándose en trabajos previos, propuso la existencia de dos tipos de carga y sugirió que sólo uno de ellos se comportaba como un fluido capaz de transferirse de un cuerpo a otro. La ley de Coulomb, enunciada por este en 1785, puso las bases de la electrostática actual, permitiendo su completo desarrollo durante el siglo XIX.
Hoy sabemos que estos fenómenos son debidos a la transferencia de cargas eléctricas ( electrones) entre objetos. Dependiendo de si se adquieren o ceden electrones, un objeto inicialmente neutro quedará cargado negativa o positivamente. La existencia de dos tipos de carga explica que pueda existir repulsión ( cargas del mismo signo) o atracción ( cargas opuestas).
La carga eléctrica está cuantizada. En el mundo macroscópico todas las cargas observadas son múltiplos enteros Q = N·e de la carga del electrón e, a la que podemos considerar unidad fundamental de carga ( los quarks tienen carga fraccionaria, q = ⅓e, pero no se observan libres).
Vídeos de referencia: youtube.com/watch?v=yc2-363MIQs, youtube.com/watch?v=ViZNgU-Yt-Y, youtube.com/watch?v=4S0EBxT60pw.
El electroscopio permite detectar la carga, y la serie triboeléctrica clasifica los materiales según su tendencia a ceder o tomar electrones al frotarse: vidrio (+), cabello humano, nylon, lana, seda, goma natural, poliestireno, PVC, teflón (−) ( simulación en phys23p.sl.psu.edu).

## Carga eléctrica — unidad fundamental

La conservación de la carga es una de las leyes fundamentales de la naturaleza. El valor de e es extremadamente pequeño comparado con las cargas típicamente presentes en objetos macroscópicos.
- Carga del electrón: e = 1,6·10⁻¹⁹ C.
- Unidad de carga en el S.I.: culombio ( C), en honor a Charles-Augustin de Coulomb.
- Nótese que e denota el valor absoluto ( sin signo).
- Ejercicio**: calcular la carga total de todos los electrones contenidos en una moneda de cobre de 3 gramos ( datos: Z = 29, A = 63,5 g/mol, Nₐ = 6,023·10²³ mol⁻¹, e = 1,6·10⁻¹⁹ C).
Solución abreviada: nº moles n = m/A = 0,047; nº átomos N = n·Nₐ = 2,85·10²²; carga total Q = N·29·(−e) = −1,32·10⁵ C.

## Distribuciones continuas de carga

Aunque la carga está cuantizada, en ocasiones a nivel macroscópico las cargas son tan numerosas y están tan juntas que pueden tratarse como una distribución continua. Por el contrario, cuando el número de cargas es bajo, estas se tratan individualmente como cargas puntuales ( distribución discreta de carga). Las distribuciones continuas pueden ser de distinto tipo: lineales, superficiales o volumétricas.
Las distribuciones continuas a lo largo de una línea se caracterizan por una densidad lineal de carga λ ( C/m):
$$\lambda = \lim_{\Delta l \to 0} \frac{\Delta q}{\Delta l} = \frac{dq}{dl}$$
Las distribuciones sobre una superficie se caracterizan por una densidad superficial de carga σ ( C/m²):
$$\sigma = \lim_{\Delta S \to 0} \frac{\Delta q}{\Delta S} = \frac{dq}{dS}$$
Las distribuciones dentro de un volumen se caracterizan por una densidad de carga volumétrica ρ ( C/m³):
$$\rho = \lim_{\Delta \tau \to 0} \frac{\Delta q}{\Delta \tau} = \frac{dq}{d\tau}$$
Nótese que estas densidades no tienen por qué ser constantes, sino que en general dependen de la posición. La integral sobre toda la región ( línea, área o volumen) es igual a la carga total contenida en dicha región:
$$Q = \int_L \lambda\, dl \qquad Q = \int_S \sigma\, ds \qquad Q = \int_V \rho\, d\tau$$
- Ejercicio**: el radio medio del núcleo de azufre ( Z = 16) es aproximadamente 1,37×10⁻¹³ cm. Suponiendo que la carga eléctrica esté uniformemente distribuida en el núcleo, calcular la densidad de carga en C/m³.
Solución abreviada:
$$Q = \int_V \rho\, d\tau = \rho\int_V d\tau = \rho\cdot V \Rightarrow \rho = \frac{Q}{V}$$
Z = 16 ⇒ Q = 16e = 16·1,6·10⁻¹⁹ C = 2,56·10⁻¹⁸ C.
V = ( 4/3)πR³ = ( 4/3)π( 1,37·10⁻¹⁵ m)³ = 1,08·10⁻⁴⁴ m³.
⇒ ρ = Q/V = 2,4·10²⁶ C·m⁻³.
- Ejercicio**: la densidad de carga de una nube electrónica en el estado fundamental del átomo de hidrógeno viene dada por la función ρ( r) = −e·e^(−2r/a₀)/(πa₀³), siendo e la carga del electrón y a₀ el radio de la primera órbita de Bohr. Calcular la carga total.
Solución abreviada: en este caso ρ depende de la posición y por tanto no se puede sacar de la integral. Además, sólo se anula cuando r tiende a infinito, por lo que la integral se extiende a todo el espacio:
$$Q = \int_V \rho\, d\tau = \int_0^\infty \rho ( r)\,4\pi r^2\, dr = -\frac{4e}{a_0^3}\int_0^\infty r^2\, e^{-2r/a_0}\, dr$$
Aplicando dos integraciones por partes consecutivas se llega a Q = −4e·a₀³/( a₀³·4) = −e ( véase también el cálculo con Wolfram Alpha).

## Ley de Coulomb

Determinada experimentalmente por Coulomb a finales del siglo XVIII mediante una balanza de torsión. La fuerza que ejerce una carga puntual q₁ sobre otra q₂:
- Está dirigida según la línea que une las cargas.
- Su módulo es proporcional al valor de ambas cargas.
- Si ambas cargas son del mismo signo, es repulsiva.
- Si ambas cargas son de signos opuestos, es atractiva.
- Decrece con el cuadrado de la distancia entre ambas cargas.
- La fuerza ejercida sobre la carga 2 por efecto de la carga 1 ( F₁₂) es de igual módulo pero de sentido contrario a la fuerza ejercida sobre la carga 1 por efecto de la carga 2 ( F₂₁).
Vídeo sobre la balanza de torsión y el experimento de Coulomb: youtube.com/watch?v=FYSTGX-F1GM.
Matemáticamente se pueden condensar todos estos enunciados en la siguiente expresión:
$$\vec{F}_{12} = K_e\,\frac{q_1 q_2}{d_{12}^2}\,\vec{u}_{12}$$
Siendo u₁₂ el vector unitario que empieza en 1 y va dirigido hacia 2, y F₁₂ la fuerza ejercida por 1 sobre 2 ( la notación opuesta también es frecuente). K_e es una constante cuyo valor en el Sistema Internacional de unidades es K_e = 8,99·10⁹ N·m²/C² ( simulación interactiva disponible).
Cuando existen más de dos cargas, se aplica el principio de superposición: la fuerza resultante es la suma de las fuerzas individuales ejercidas por cada carga:
$$\vec{F}_j = \sum_{i=1,i\neq j}^{n} \vec{F}_{ij} = K_e \sum_{i=1,i\neq j}^{n} \frac{q_i q_j}{d_{ij}^2}\,\vec{u}_{ij}$$
- Ejercicio ( cuestión de examen)**: dos cargas puntuales positivas Q y 3Q se mantienen separadas por una distancia d, de forma que la fuerza sobre la carga Q tiene un valor F. Si separamos las cargas hasta una distancia 3d, ¿cuál será el módulo de la nueva fuerza sobre la carga 3Q?
Solución: es una aplicación directa de la ley de Coulomb. Teniendo en cuenta que la fuerza de la carga Q sobre la 3Q es de igual módulo pero de sentido contrario a la fuerza de 3Q sobre Q, la fuerza inicial sobre 3Q tendrá módulo:
$$F = K_e\,\frac{Q\cdot 3Q}{d^2} = K_e\,\frac{3Q^2}{d^2}$$
Y al separar las cargas, esta pasará a ser:
$$F' = K_e\,\frac{Q\cdot 3Q}{( 3d)^2} = K_e\,\frac{3Q^2}{9d^2} = \frac{F}{9}$$

## Ley de Coulomb — aplicación a varias cargas puntuales

- Ejercicio**: en los vértices de un triángulo equilátero de lado L se colocan cargas −e, y en su centro se coloca cierta carga Q > 0. Calcular el valor de Q para que la fuerza sobre cualquiera de las cargas de los vértices sea nula.
Solución abreviada: por la simetría de la figura, basta exigir F_tot = 0 para la carga en uno de los vértices. Eligiendo los ejes XY de la figura, con la altura del triángulo h = (√3/2)L, la fuerza sobre esa carga es la suma de las contribuciones de las otras dos cargas −e de los vértices y de la carga Q del centro. Igualando ambas componentes ( X e Y) a cero y operando se llega dos veces al mismo resultado:
$$Q = \frac{e}{3\sqrt{3}}$$
Nótese que esta solución es ficticia, ya que e es la carga más pequeña posible en estado libre en la naturaleza.

## Ley de Coulomb — distribuciones continuas de carga

El principio de superposición también nos permite escribir la ley de Coulomb para distribuciones continuas de carga. Por ejemplo, la fuerza ejercida sobre una carga q por un elemento de volumen dτ de una distribución volumétrica de carga ρ( r) sería:
$$d\vec{F} = K_e\,\frac{q\,dq}{d^2}\vec{u} = K_e\,\frac{q\,\rho\,d\tau}{d^2}\vec{u}$$
Siendo u el vector unitario que une el elemento de volumen y el punto donde calculamos el campo. Integrando a todo el volumen cargado queda:
$$\vec{F} = K_e\, q \int_V \frac{\rho}{d^2}\vec{u}\, d\tau$$
Para distribuciones superficiales o lineales se procede del mismo modo pero usando σ o λ e integrando sobre la superficie o línea, según corresponda.
- Ejercicio**: sea un segmento colocado sobre el eje X entre x = 0 y x = L, con densidad lineal de carga uniforme ( constante) λ C/m. Calcular la fuerza sobre una carga q colocada sobre el eje X a cierta distancia x₀.
Solución abreviada: con dq = λ·dx,
$$\vec{F} = K_e\, q \int_0^L \frac{\lambda\, dx}{( x_0-x)^2}\vec{u}_x = K_e\, q\lambda \left[\frac{1}{x_0-x}\right]_0^L \vec{u}_x = \frac{K_e\, q\lambda L}{x_0 ( x_0-L)}\vec{u}_x$$
Nótese que Q = λL es la carga total del segmento, por tanto:
$$\vec{F} = \frac{K_e\, qQ}{x_0 ( x_0-L)}\vec{u}_x$$
Si la carga estuviera muy lejos del origen comparado con la longitud del segmento ( x₀ ≫ L), entonces podemos aproximar el denominador por x₀², es decir, el efecto del segmento sería como el de una carga puntual Q en el origen:
$$\vec{F} \approx \frac{K_e\, qQ}{x_0^2}\vec{u}_x \qquad ( x_0 \gg L)$$

## Campo eléctrico

El concepto de campo vectorial se introduce para representar la acción a distancia que puede ejercer un cuerpo sobre otro ( por ejemplo, atracción gravitatoria, repulsión eléctrica). La fuerza sería el efecto visible, pero el campo estaría presente en el espacio incluso si no ponemos un cuerpo de prueba.
Sea una carga positiva de prueba muy pequeña q : 0. Podemos definir el campo eléctrico E en cualquier punto del espacio como:
$$\vec{E} = \lim_{q\to 0}\frac{\vec{F}}{q}$$
Siendo F la fuerza electrostática ejercida sobre q.
El campo eléctrico tiene dimensiones de fuerza por unidad de carga. En el S.I. se expresa en N/C o V/m. Es un vector que va dirigido en la misma dirección que la fuerza que sería ejercida sobre una carga positiva.
De la ley de Coulomb, deducimos que el campo creado por una carga Q situada en el origen será:
$$\vec{E} = \lim_{q\to 0} K_e\,\frac{Qq}{qr^2}\vec{u}_r = K_e\,\frac{Q}{r^2}\vec{u}_r$$
De forma más genérica, el campo eléctrico creado por una carga Q situada en el punto 1, evaluado en un punto 2, valdría:
- $$\vec{E} = K_e\,\frac{Q}{d^2}\vec{u} = K_e\,\frac{Q}{: \vec{r}_2-\vec{r}_1: ^3}(\vec{r}_2-\vec{r}_1)$$
Para distribuciones discretas, aplicamos el principio de superposición como vimos antes con la ley de Coulomb:
$$\vec{E}(\vec{r}) = K_e \sum_{i=1}^{n}\frac{q_i}{d_i^2}\vec{u}_i, \qquad \vec{d}_i = \vec{r}-\vec{r}_i$$
Análogamente, para distribuciones continuas de carga ( simulación interactiva disponible):
$$\vec{E} = K_e\int_L \frac{\lambda\,\vec{u}_d}{d^2}\, dl \quad (\text{línea}), \qquad \vec{E} = K_e\int_S \frac{\sigma\,\vec{u}_d}{d^2}\, ds \quad (\text{superficie}), \qquad \vec{E} = K_e\int_V \frac{\rho\,\vec{u}_d}{d^2}\, d\tau \quad (\text{volumen})$$
- Ejercicio**: calcular el campo en el punto P = ( 0,3) de la figura, creado por dos cargas q₁ = 8 nC y q₂ = 12 nC situadas en los puntos ( 0,0) y ( 4,0). Asumir que las distancias están expresadas en metros.
- Solución abreviada: con d₁ₚ = 3**j**,: d₁ₚ: = 3, y d₂ₚ = −4**i**+3**j**,: d₂ₚ: = 5:
$$\vec{E} = \vec{E}_1 + \vec{E}_2 = \frac{K_e q_1}{d_{1p}^2}\vec{u}_{1p} + \frac{K_e q_2}{d_{2p}^2}\vec{u}_{2p} = \frac{K_e q_1}{d_{1p}^3}\vec{d}_{1p} + \frac{K_e q_2}{d_{2p}^3}\vec{d}_{2p}$$
$$= \frac{9\cdot10^9\cdot8\cdot10^{-9}}{3^3}\,3\vec{j} + \frac{9\cdot10^9\cdot12\cdot10^{-9}}{5^3}(-4\vec{i}+3\vec{j})\ \text{N/C} = (-3{,}5\,\vec{i} + 10{,}6\,\vec{j})\ \text{N/C}$$
- O equivalentemente, en forma polar: Eₓ = −3,5 N/C, Ey = +10,6 N/C,: E: = √( 3,5² + 10,6²) = 11,2 N/C. El ángulo del vector campo con la horizontal sería α = arctan ( Ey/Eₓ) = 108°.
- Ejercicio**: calcular el campo creado por una línea recta infinita, uniformemente cargada con una densidad de carga λ, en un punto situado a cierta distancia a de la línea.
Solución abreviada: eligiendo el eje Z paralelo a la línea y el punto P sobre el eje X, la componente Z del campo es nula por la simetría del problema. Basta con integrar la componente X, con z = a·tan α, dz = ( a/cos²α)dα, y d = a/cos α:
$$E_x = \int_{-\infty}^{+\infty} K_e\,\frac{\lambda\, dz}{d^2}\cos\alpha = \frac{K_e\lambda}{a}\int_{-\pi/2}^{\pi/2}\cos\alpha\, d\alpha = \frac{2K_e\lambda}{a}$$
( Recurso de visualización: web.mit.edu/8.02t, "Line Integration".)

## Flujo

Definición: el flujo de un campo vectorial **v** a través de una superficie S es un escalar φ que viene dado por:
$$\phi = \int_S \vec{v}\cdot d\vec{s}$$
Siendo ds = ds·**u**ₛ el elemento diferencial de superficie, con **u**ₛ el vector unitario normal a la superficie en cada punto. Si llamamos α al ángulo entre **u**ₛ y **v**:
$$\phi = \int_S v\cos\alpha\, ds$$
En un diagrama de líneas de campo, se puede visualizar el significado del flujo a través de una superficie como el número de líneas de campo que la atraviesan ( analogía con un fluido).
- Ejemplo**: sea un campo eléctrico uniforme E = a**k**. Su flujo a través de una superficie cuadrada de área S en el plano XY sería:
$$\phi = \int_S \vec{E}\cdot d\vec{s} = \int_S a\vec{k}\cdot\vec{k}\, ds = a\int_S ds = aS \quad (\text{N}\cdot\text{m}^2/\text{C})$$
- Ejemplo**: sea un campo eléctrico uniforme E = a**u** que forma en todo punto un ángulo α con la normal a una superficie rectangular de área S. El flujo será:
$$\phi = \int_S \vec{E}\cdot d\vec{s} = aS\cos\alpha \quad (\text{N}\cdot\text{m}^2/\text{C})$$
Nótese que la orientación es importante: si el campo es paralelo a la superficie ( vector campo y vector superficie ortogonales) en todo punto, el flujo será nulo ( las líneas no cruzan la superficie).
Consideremos una superficie cerrada. Si no encierra fuentes ni sumideros del campo en su interior, entrarán tantas líneas como salen, y el flujo será nulo:
$$\phi = \oint_S \vec{v}\cdot d\vec{s} = 0$$
Algunas notas finales sobre el flujo y las líneas de campo:
- El vector normal a superficies cerradas se elige siempre apuntando hacia el exterior de la superficie.
- Si el flujo a través de una superficie cerrada es positivo, significa que hay más líneas salientes que entrantes atravesando dicha superficie.
- Las líneas de campo no se cruzan. Comienzan y acaban en cargas ( o en el infinito). Las cargas negativas crean líneas entrantes y las positivas líneas salientes.
- Las zonas con campo más intenso son aquellas donde las líneas de campo están más juntas, y las de campo menos intenso aquellas donde están más separadas ( la densidad de líneas representa la intensidad del campo). El flujo entrante que atraviesa una esfera pequeña alrededor de una carga es idéntico al que atraviesa una esfera mayor concéntrica con ella.

## Ley de Gauss

Consideremos una superficie esférica S de radio a centrada en una carga q, y calculemos el flujo del vector campo eléctrico a través de dicha esfera aplicando la ley de Coulomb. El vector normal a la superficie también es radial, con lo cual:
$$\phi = \int_S \vec{E}\cdot d\vec{s} = \int_S K_e\frac{q}{a^2}\vec{u}_r\cdot\vec{u}_r\, ds = K_e\frac{q}{a^2}\int_S ds = K_e\frac{q}{a^2}\cdot 4\pi a^2 = 4\pi K_e\, q$$
Definiendo ε₀ tal que K_e = 1/( 4πε₀):
$$\phi = \frac{q}{\varepsilon_0}$$
Este resultado es generalizable a cualquier otra superficie.
ε₀ se denomina permitividad ( o constante dieléctrica) del vacío. Su valor es ε₀ = 8,85·10⁻¹² F·m⁻¹ ( F = C²·N⁻¹·m⁻¹).
La ley de Gauss es una de las bases del electromagnetismo, y nos dice que el resultado anterior se puede generalizar a cualquier superficie cerrada S y número de cargas:
$$\phi = \oint_S \vec{E}\cdot d\vec{s} = \frac{Q}{\varepsilon_0}$$
El flujo del vector campo eléctrico a través de una superficie cerrada cualquiera es igual a la carga neta Q encerrada por dicha superficie, dividida por ε₀. Si por ejemplo hay n cargas puntuales encerradas, el valor de Q sería Q = Σᵢ qᵢ.
Vídeo de referencia: youtube.com/watch?v=yOv4xxopQFQ ( notación en el vídeo: E₀, ε₀).
- Ejercicio**: sea una esfera de radio 3 centrada en el origen y 3 cargas de −1 C situadas en ( 0,0,1), ( 0,1,0) y ( 4,4,4). Calcular el flujo del vector campo eléctrico a través de la esfera usando el teorema de Gauss. Asumir que las distancias están expresadas en metros.
Solución: la carga encerrada es la de las dos primeras cargas ( la tercera está fuera de la esfera), Q_encerrada = −2 C:
$$\phi = \frac{Q}{\varepsilon_0} = \frac{-2}{8{,}85\cdot10^{-12}}\ \text{C}\cdot\text{N}\cdot\text{m}^2\cdot\text{C}^{-2} = -2{,}26\cdot10^{11}\ \text{N}\cdot\text{m}^2/\text{C}$$
El signo menos indica flujo neto entrante en la esfera. Nótese que la tercera carga "no cuenta" porque produce tantas líneas entrantes como salientes al estar fuera de la esfera.
La ley de Gauss es de gran utilidad práctica ya que permite calcular el campo eléctrico de forma sencilla para distribuciones de carga que tengan cierto grado de simetría ( que permita resolver fácilmente la integral).

## Ley de Gauss — aplicación práctica

- Ejercicio**: resolver el ejercicio del hilo cargado infinito ( visto anteriormente) usando la ley de Gauss.
Solución: por simetría, E es constante sobre toda la superficie cilíndrica lateral y además es perpendicular a ella. El flujo a través de las dos bases del cilindro es nulo, pero se va a ambos lados de la igualdad al considerar h : ∞:
$$\phi = E\cdot 2\pi a\cdot h = \frac{Q}{\varepsilon_0} = \frac{\lambda\cdot h}{\varepsilon_0} \Rightarrow E = \frac{\lambda}{2\pi a\varepsilon_0} = \frac{2K_e\lambda}{a} \Rightarrow \vec{E} = \frac{2K_e\lambda}{a}\vec{u}_r$$
Idéntico al resultado calculado anteriormente.
- Ejercicio**: hallar el campo eléctrico creado en todo el espacio por un plano infinito XY, cargado uniformemente con densidad superficial de carga σ.
Solución: por simetría, E no puede tener componente paralela al plano, y estará dirigido hacia +Z sobre el plano y hacia −Z bajo el plano. Tomamos una superficie de Gauss cilíndrica, con la superficie lateral ( 3) paralela al campo ( no contribuye al flujo) y perpendicular a las dos bases ( 1 y 2), sobre las que E es constante. La carga encerrada será σ·a, de modo que:
$$\phi = E (\vec{k}\cdot a\vec{k}) + E (-\vec{k}\cdot a (-\vec{k})) = 2Ea = \frac{\sigma a}{\varepsilon_0} \Rightarrow E = \frac{\sigma}{2\varepsilon_0}$$
Nótese que E es discontinuo ( salto σ/ε₀):
$$\vec{E} = \begin{cases} \dfrac{\sigma}{2\varepsilon_0}\vec{k} & z>0 \\[4pt] -\dfrac{\sigma}{2\varepsilon_0}\vec{k} & z<0 \end{cases}$$

## Potencial eléctrico

Como vimos en el tema 0, si un campo E es conservativo, la circulación del vector entre dos puntos A y B es independiente del camino seguido, y podemos definir un potencial V tal que, para cualquier camino L1, L2, L3... entre A y B:
$$\int_{L_1}\vec{E}\cdot d\vec{l} = \int_{L_2}\vec{E}\cdot d\vec{l} = \int_{L_3}\vec{E}\cdot d\vec{l} = \cdots = -( V_B - V_A)$$
( Nótese el criterio de signos utilizado.) Si el trayecto considerado es cerrado, la circulación es nula, ya que el punto de salida y llegada coinciden:
$$\oint_L \vec{E}\cdot d\vec{l} = 0$$
Definiremos pues la diferencia de potencial eléctrico entre dos puntos A y B como:
$$V_B - V_A = -\int_A^B \vec{E}\cdot d\vec{l}$$
Sea una carga puntual q en el origen. La diferencia de potencial entre dos puntos arbitrarios A y B sólo depende de q y sus distancias respectivas a la carga, rA y rB:
$$V_B - V_A = -\int_A^B \vec{E}\cdot d\vec{l} = \frac{q}{4\pi\varepsilon_0}\left (\frac{1}{r_B}-\frac{1}{r_A}\right)$$
( Demostración de que E es conservativo y del valor de ΔV: dividir un trayecto arbitrario AB en tramos radiales y concéntricos, y notar que sólo los tramos radiales contribuyen a la integral.)
Las unidades de V en el S.I. son los voltios: 1V = 1 J/C = 1 N·m/C.
- Para que exista campo eléctrico, el potencial debe variar en el espacio. Si V es uniforme en una región, el campo eléctrico será nulo en dicha región.
- Líneas ( 2D) o superficies ( 3D) equipotenciales: son aquellas que unen puntos a un mismo potencial.
- El campo eléctrico es perpendicular a dichas superficies equipotenciales y va dirigido en el sentido de V decreciente ( analogía gravedad-campo eléctrico atractivo).
- El potencial es una función continua en puntos del espacio no ocupados por cargas. Por el contrario, el campo eléctrico puede presentar discontinuidades.
El potencial guarda estrecha relación con el concepto de energía potencial ( energía por unidad de carga, V = U/q), que veremos en detalle en el tema de energía electrostática. Al desplazar una carga por una superficie equipotencial no se realiza trabajo, ya que el desplazamiento es perpendicular al campo y por tanto a la fuerza de Coulomb ( U no cambia).
La definición dada para V se refiere a diferencias de potencial entre dos puntos. Podemos definir el potencial en un punto eligiendo un potencial de referencia ( punto tal que V = 0).

## Potencial eléctrico y campo eléctrico

El campo eléctrico deriva de un potencial, quedando completamente descrito por él. Al ser un escalar, el tratamiento usando V suele ser más simple que con E. En términos matemáticos se puede escribir como ( fuera de temario, nosotros sólo usaremos la forma integral descrita anteriormente):
$$\vec{E} = -\text{grad}\,V = -\nabla V = -\left (\frac{\partial V}{\partial x}\vec{i} + \frac{\partial V}{\partial y}\vec{j} + \frac{\partial V}{\partial z}\vec{k}\right)$$

## Potencial eléctrico — caso de una carga puntual

Cuando no existe carga en el infinito, puede tomarse este como origen de potencial ( V : 0 si r : ∞), de modo que el potencial creado por una carga q situada en el origen de coordenadas se puede definir como:
$$V ( r) - V (\infty) = \frac{q}{4\pi\varepsilon_0 r} - 0 \Rightarrow V ( r) = \frac{q}{4\pi\varepsilon_0 r}$$
De forma más genérica ( carga en un punto cualquiera r₀):
- $$V (\vec{r}) = \frac{q}{4\pi\varepsilon_0\,: \vec{r}-\vec{r}_0: }$$
- Líneas de campo radiales, hacia la carga si es negativa.
- Líneas equipotenciales concéntricas.
- Una carga positiva se movería siguiendo la dirección de potencial decreciente ( de V alto a V bajo, siendo 0 en el infinito). Una carga negativa haría lo contrario. En ambos casos ganaría energía cinética a costa de la energía potencial electrostática.

## Potencial eléctrico — distribuciones de carga

La expresión anterior es válida para una carga puntual. Para distribuciones discretas de carga utilizaremos el principio de superposición como hicimos antes con el campo ( simulación interactiva disponible):
- $$V (\vec{r}) = \frac{1}{4\pi\varepsilon_0}\sum_{i=1}^{n}\frac{q_i}{: \vec{r}-\vec{r}_i: }$$
Análogamente, para distribuciones continuas de carga:
- $$V (\vec{r}) = \frac{1}{4\pi\varepsilon_0}\int_V \frac{\rho\, d\tau}{: \vec{r}-\vec{r}_i: }$$
- Ejercicio**: una carga puntual q₁ está situada en el origen de coordenadas, y otra carga q₂ se encuentra sobre el eje X en x = a > 0. Hallar el potencial en cualquier punto del eje X.
Solución: aplicando el principio de superposición:
- $$V ( x) = \frac{q_1}{4\pi\varepsilon_0: x-x_1: } + \frac{q_2}{4\pi\varepsilon_0: x-x_2: } = \frac{1}{4\pi\varepsilon_0}\left (\frac{q_1}{: x: } + \frac{q_2}{: x-a: }\right)$$
Existen tres casos que deben tratarse por separado:
1. A la izquierda de q₁: ( x < 0) ⇒ V ( x) = ( 1/4πε₀)·(−q₁/x + q₂/( a−x))
2. Entre ambas: ( 0 < x < a) ⇒ V ( x) = ( 1/4πε₀)·( q₁/x + q₂/( a−x))
3. A la derecha de q₂: ( x > a) ⇒ V ( x) = ( 1/4πε₀)·( q₁/x + q₂/( x−a))
( Gráfica para q₁, q₂ > 0.)
- Ejercicio**: sea una esfera de radio R con carga total Q, repartida uniformemente. Hallar el campo eléctrico y el potencial en todo el espacio. ( Ver también surendranath.org/GPA/Electricity/EVGraphs/EVGraphs.html.)
Solución: la densidad de carga será ρ = 3Q/( 4πR³). Hallamos el campo usando la ley de Gauss, diferenciando interior y exterior de la esfera:
Para r < R ( crece linealmente con r):
$$E = \frac{( 4/3)\pi r^3 \rho}{4\pi\varepsilon_0 r^2}\vec{u}_r = \frac{Qr}{4\pi\varepsilon_0 R^3}\vec{u}_r$$
Para r > R ( decrece como r⁻², idéntico al creado por una carga Q en el centro de la esfera):
$$E = \frac{Q}{4\pi\varepsilon_0 r^2}\vec{u}_r$$
Aplicando ahora la definición de potencial, con origen en el infinito:
Para r < R:
$$V (\infty)-V ( r) = -\int_R^r \frac{Qr\,dr}{4\pi\varepsilon_0 R^3} - \int_\infty^R \frac{Q\,dr}{4\pi\varepsilon_0 r^2} = \frac{-Q}{4\pi\varepsilon_0}\left (\frac{R^2}{2R^3}-\frac{r^2}{2R^3}\right) + \frac{-Q}{4\pi\varepsilon_0}\left (\frac{1}{\infty}-\frac{1}{R}\right)$$
$$\Rightarrow V ( r) = \frac{Q}{8\pi\varepsilon_0 R^3}\left ( 3R^2 - r^2\right)$$
Para r > R:
$$V (\infty)-V ( r) = -\int_\infty^r \frac{Q\, dr}{4\pi\varepsilon_0 r^2} = \frac{-Q}{4\pi\varepsilon_0}\left (\frac{1}{\infty}-\frac{1}{r}\right) \Rightarrow V ( r) = \frac{Q}{4\pi\varepsilon_0 r}$$

## Dipolo eléctrico

Un dipolo eléctrico es un sistema formado por dos cargas eléctricas iguales, de signo opuesto y muy próximas entre sí. Es un caso importante a nivel molecular debido a la existencia de moléculas polares, por lo que se estudia su respuesta a campos externos.
Se define el momento dipolar **p** como un vector cuyo módulo es igual al producto de la distancia que separa a las cargas y el valor absoluto de la carga, y cuyo sentido va de la carga negativa hacia la positiva:
$$\vec{p} = q\,\vec{d}$$

## Potencial creado por un dipolo

El potencial creado por un dipolo vale:
- $$V (\vec{r}) = \frac{q}{4\pi\varepsilon_0}\left (\frac{1}{: \vec{r}-\vec{r}_+: } - \frac{1}{: \vec{r}-\vec{r}_-: }\right) = \frac{q}{4\pi\varepsilon_0}\cdot\frac{(\vec{r}-\vec{r}_-)-(\vec{r}-\vec{r}_+)}{: \vec{r}-\vec{r}_+: \cdot: \vec{r}-\vec{r}_-: }$$
Tomando el origen en el centro del dipolo, r es la distancia de éste hasta el punto donde queremos calcular V. Si r ≫ d, se puede aproximar el denominador de la segunda fracción por r² y el numerador por d·cos θ ( ver figura):
$$V (\vec{r}) \approx \frac{qd\cos\theta}{4\pi\varepsilon_0 r^2} = \frac{p\cos\theta}{4\pi\varepsilon_0 r^2}$$

## Campo eléctrico creado por un dipolo

El campo eléctrico creado por el dipolo es la suma de los campos creados por cada carga individual, y se puede aproximar por:
$$\vec{E}(\vec{r}) = \frac{1}{4\pi\varepsilon_0\, r^3}\left (\frac{3 (\vec{p}\cdot\vec{r})}{r^2}\vec{r} - \vec{p}\right)$$
Nótese el decrecimiento rápido ( término r⁻³) y la simetría alrededor de la línea que une ambas cargas.
Simulaciones y material multimedia online: surendranath.org/GPA/Electricity/ElectricField/FieldLines.html; vídeo: youtube.com/watch?v=RZxyjv8YF3k.

## Respuesta de un dipolo a un campo eléctrico

Un dipolo expuesto a un campo tiende a rotar hasta orientarse paralelamente a él. El momento del par de fuerzas que aparece vale:
$$\vec{\tau} = q\vec{d}\times\vec{E} = \vec{p}\times\vec{E}$$
La fuerza neta sobre el centro de masas será nula si el campo es uniforme, por tanto no habría desplazamiento. En campos no uniformes sí puede haber fuerza neta ( ejemplo: una molécula polarizada sometida al campo de una carga puntual). El vector momento dipolar p es de gran importancia para la formulación de la electrostática en medios materiales.
- Ejercicio**: un dipolo eléctrico forma un ángulo de 30 grados con un campo eléctrico uniforme de 2·10⁵ N/C, experimentando un momento de 4 N·m. Hallar el valor de las cargas que constituyen el dipolo, sabiendo que su longitud es de 2 cm.
Solución:
$$\tau = pE\sin\alpha = qdE\sin\alpha \Rightarrow q = \frac{\tau}{dE\sin\alpha} = \frac{4\ \text{Nm}}{2\cdot10^{-2}\,\text{m}\cdot 2\cdot10^{5}\,\text{NC}^{-1}\cdot 0{,}5} = 0{,}002\ \text{C} = 2\ \text{mC}$$
Este momento hará girar al dipolo para alinearse con el campo.
En el tema de electrostática en medios dieléctricos veremos que existen dipolos moleculares inducidos y permanentes, y su importancia para el estudio de la electrostática en el interior de medios dieléctricos. El agua es un claro ejemplo de molécula con momento dipolar permanente y por tanto se reorientará si se sumerge en un campo electrostático.
Dipolos moleculares y calentamiento por microondas: vídeo youtube.com/watch?v=kp33ZprO0Ck; simulación interactiva Phet en phet.colorado.edu/es/simulation/microwaves.

## Apéndice - Teorema de Earnshaw ( 1842)

"Un conjunto de cargas puntuales no se puede mantener en un estado de equilibrio mecánico estacionario exclusivamente mediante la interacción electrostática de las cargas."
Es consecuencia de la ley de Gauss. Para que una carga de prueba positiva esté en un equilibrio estable, todas las líneas de campo a su alrededor deben apuntar hacia el punto ocupado por la carga ( para que así la fuerza electrostática tienda a llevar de vuelta la carga a dicho punto si ésta se mueve ligeramente). Si todas las líneas de campo apuntan hacia el punto de equilibrio, necesariamente debe haber carga en dicho punto, lo cual contradice la suposición de partida.
