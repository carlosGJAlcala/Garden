---
title: "Simulación de circuitos cuánticos (TFM)"
---

# Simulación de Circuitos Cuánticos

*Trabajo de Fin de Máster — Carlos Garrido Junco*

## Resumen

Este documento explica las diferencias entre diferentes simuladores cuánticos que se disponen actualmente.

También se hace un breve repaso de la historia de la computación cuántica, narrando sus logros y su proyección a futuro.

Como necesidad impiedosa, será necesario fundamentar la base matemática en la que se basan los computadores cuánticos y sus mecanismos físicos y cómo son posibles.

Para comparar los diferentes simuladores mencionados en el texto, no solo se tiene en cuenta un mero punto de rendimiento comparando con dichos algoritmos, sino también la experiencia de usuario, la cuesta de aprendizaje de estos y sus aplicaciones a futuro en entornos reales.

**Palabras clave:** Computación cuántica, algoritmos cuánticos, emulación, qubit, puerta lógica cuántica.

## Abstract

This document explains the differences between various quantum simulators currently available.

It also briefly reviews the history of quantum computing, describing its achievements and future prospects.

As a matter of urgency, it will be necessary to establish the mathematical foundation on which quantum computers are based, their physical mechanisms, and how they are possible.

To compare the different simulators mentioned in the text, we take into account not only a mere performance point compared to these algorithms, but also the user experience, the learning curve, and their future applications in real-world environments.

**Keywords:** Quantum computing, quantum algorithms, emulation, qubit, quantum logic gate.

## Introducción

> En algún momento, todo se va al carajo. Entonces puedes aceptarlo, o puedes ponerte a trabajar. Así es como sobreviví: resolviendo un problema, y luego otro, y luego el siguiente. Si resuelves los suficientes, puedes volver a casa.
>
> — Andy Weir, *The Martian* (adaptación cinematográfica, 2015) \### Presentación {#sec:presentacion}

La posibilidad de aprovechar las propiedades cuánticas de la materia para poder realizar cómputos, si bien ya era conocida previamente, fue definitivamente propuesta por David Deutsch en 1985 (Deutsch 1985). Desde entonces cobró vigor la iniciativa de diseñar algoritmos que pudieran ejecutarse sobre tal tipo de computadores.

Puesto que tecnológicamente son posibles solamente versiones de baja capacidad, a las que no es fácil acceder, la forma más sencilla de probar tales algoritmos es ejecutarlos sobre simuladores que se computen clásicamente. En este trabajo se propone estudiar y comparar los distintos simuladores que han ido apareciendo con el tiempo, especialmente en lo concerniente a su capacidad y eficiencia.

En cuanto a los antecedentes, el concepto de aprovechar los fenómenos cuánticos surge en la década de los ochenta, con Richard Feynman (Feynman 1982) y Yuri Manin, que fueron los que sugirieron que los sistemas cuánticos podían resolver problemas matemáticos de forma más eficiente que los computadores clásicos, y David Deutsch lo formalizó con la creación del primer algoritmo cuántico.

Este modelo introduce el concepto de *Qubit*, un bit que puede estar en una superposición cuántica de estados (Lloyd 1996). Se pueden emplear para el diseño de algoritmos como el algoritmo de Deutsch-Jozsa, el algoritmo de Shor y el de Grover.

Debido a que el hardware cuántico aún está en una fase muy temprana y con recursos limitados, la simulación de estos en computadoras clásicas ha sido clave para poder probarlos. Algunas plataformas para simular algoritmos cuánticos son las siguientes: Qiskit (IBM), Cirq (Google), Microsoft QDK y QuEST (Quantum Exact Simulation Toolkit) (Microsoft Learn 2025c).

Estas simulaciones son necesarias; se necesitan para poder desarrollar algoritmos cuánticos de forma eficiente, para poder adelantar el trabajo de diseño y desarrollo. Además, permiten optimizar el diseño de la arquitectura del hardware. También sirven para probar, entre otros, los siguientes conceptos: *machine learning* cuántico, química cuántica y aplicaciones en criptografía.

Por último, el hardware actual para realizar computación cuántica se encuentra en la fase *NISQ* (Noisy Intermediate-Scale Quantum), donde dichos sistemas están en un estado de desarrollo estancado debido al ruido.

### Objetivos y campo de aplicación

El objetivo de este TFM es ahondar en los conceptos previamente descritos, centrándose en los diferentes simuladores, analizando cuáles son sus diferencias y evaluando sus capacidades y limitaciones. A través de dicho estudio se busca:

- Explicar el estado actual de los ordenadores cuánticos y por qué son importantes los simuladores cuánticos.

- Explicar la base teórica en que se fundamentan los ordenadores cuánticos.

- **Investigar aplicaciones** prácticas de los simuladores en áreas como optimización, criptografía, química cuántica y *machine learning* cuántico.

- **Probar algunos algoritmos cuánticos** en los diferentes simuladores seleccionados.

- **Evaluar y comparar los diferentes simuladores**, determinando sus ventajas y desventajas en términos de rendimiento y otros factores.

### Historia

> La historia es como un polvo suspendido en el aire: en cuanto se levanta un poco de viento, todo se remueve
>
> — Liu Cixin Las ciencias de la computación derivan de las matemáticas discretas y de la lógica computacional, las cuales involucran muchos siglos de evolución de las matemáticas. Estas se remontan al siglo XXX antes de Cristo (hace 5000 años) en el Antiguo Egipto y Babilonia, aunque las demostraciones matemáticas comienzan con los griegos; cabe destacar que Aristóteles en el siglo IV antes de Cristo desarrolla la lógica formal, que determina la forma de ver el mundo desde Occidente. Dicho conocimiento estuvo a punto de perderse durante la Edad Media si no hubiera sido por los árabes. Este conocimiento vuelve a Occidente durante el Renacimiento. La lógica formal se ve rejuvenecida gracias a matemáticos como Descartes y Leibniz, y en el siglo XIX surge la lógica booleana en la que se sustentan las computadoras clásicas.Entre los siglos XIX y XX surgen figuras como David Hilbert, que promueve la idea de que cualquier problema puede ser resuelto a través de la lógica matemática. Sin embargo, Kurt Gödel, con su teorema de incompletitud (Da Silva 2014), demostró que lo que pretendía Hilbert era imposible. Esto significó un nuevo quiebre en las matemáticas que, como respuesta, impulsaron y crearon las ciencias de la computación en las que destaca Alan Turing. Alan Turing basándose en los trabajos de Gödel con el problema de decisión planteado por David Hilbert y Wilhelm Ackermann (1928). En dicho problema se busca determinar un procedimiento matemático y determinista (algoritmo) que indique si una sentencia matemática es verdadera o falsa. Si se lograse un algoritmo que determina si una sentencia es verdadera o no, Hilbert tendría razón. Alan Turing, inspirado en el teorema de incompletitud de Gödel, demostró mediante el problema de parada (Alfonseca 2000) (determinar si un algoritmo termina o no) que las matemáticas no son un sistema completo como pretendía Hilbert. Esto sentó las bases teóricas de los ordenadores clásicos, los cuales se basan en la lógica de Aristóteles, muy diferente a la forma de ver el mundo en Oriente.La lógica de Aristóteles ve el mundo de manera bivalente (verdadero/falso). Esto ha contribuido enormemente a todo el desarrollo científico que se vivió en Occidente. Se fundamenta en tres principios que están en la base de todo razonamiento lógico correcto:

- **Principio de identidad**: A es A.

- **Principio de no contradicción**: Una proposición no puede ser al mismo tiempo verdadera y falsa.

- **Principio del tercero excluido**: Toda proposición es falsa o verdadera, no hay otra opción.

Con estos tres principios desarrolló las reglas del silogismo (Wikipedia 2025b), que es un razonamiento que parte de dos premisas y extrae una conclusión. Es un método deductivo: con premisas verdaderas se obtiene un resultado verdadero.

- Premisa 1: Todos los hombres son mortales.

- Premisa 2: Sócrates es hombre.

- Conclusión: Sócrates es mortal.

Esta forma de ver el mundo se contrapone de manera intuitiva a como es la realidad cuántica, ya que principios como el principio de no contradicción se contraponen con el principio de superposición, en el cual un sistema puede estar en dos estados simultáneamente al mismo tiempo. Este choque tan grande entre el pensamiento de Aristóteles, que fue la base de todo el pensamiento occidental, y la mecánica cuántica hizo que científicos como Albert Einstein negaran la naturaleza probabilística de los sistemas cuánticos y sostuvieran que debían existir variables ocultas que no conocíamos (Wikipedia 2025c)

Con el cambio de enfoque a principios de la década de los 60, Rolf Landauer se preguntaba si las leyes físicas imponían alguna limitación al proceso de cómputo, sobre todo relacionado con la disipación de calor por los ordenadores, y si este proceso era inherente a la física o debido a la eficiencia de la tecnología disponible. Este concepto lo relacionó con la entropía de un sistema de la siguiente forma: "En toda operación lógicamente irreversible que manipula información, como la reinicialización de memoria, hay aumento de entropía, y una cantidad asociada de energía es disipada como calor". Este principio es relevante en informática reversible y en informática cuántica. Landauer demostró que, para hacer computadoras más eficientes en cuanto a energía, sus operaciones tienen que ser reversibles para que no se pierda la información en forma de calor. Esto hace que, en teoría, las computadoras cuánticas sean más eficientes, aunque actualmente, en la práctica, el consumo de energía es mucho mayor por las limitaciones técnicas (Bonillo 2013).

Otra idea germen de la computación cuántica es el efecto túnel. Dicho efecto se lleva a especificar de la siguiente manera: si el canal de un transistor, que es la distancia que separa su colector y su emisor, debido a que los electrones son partículas cuánticas y se comportan como onda y partícula, son capaces de atravesar dicho canal (Bonillo 2013) si la distancia en el canal llega a ser menor que $1.2$ nm. El efecto túnel es un problema en la computación clásica, aunque en la cuántica no es un problema, sino todo lo contrario, ya que se utiliza en sistemas de qubits basados en túneles cuánticos, por ejemplo, los quantum dot o dispositivos Josephson. La búsqueda de superar dicha limitación o incluso aprovecharla impulsó o hizo interesante la creación de computadoras cuánticas.

Como hemos mencionado anteriormente, aunque Feynman y Yuri Manin en la década de los 80 sugirieron sistemas que podían aprovechar dichos fenómenos cuánticos, no fue hasta que en 1985 David Deutsch formaliza dicha propuesta con la creación de un algoritmo que lleva su nombre. En este deja claro que utilizando principios como el entrelazamiento cuántico y el principio de superposición, pueden resolverse ciertos problemas de una manera más eficiente que en un ordenador clásico. También formalizó el concepto de máquina de Turing cuántica (QTM) (Wikipedia contributors 2025b). Es una extensión de la máquina de Turing tradicional incorporando operaciones cuánticas. Ambas máquinas, al ser completas, pueden realizar los mismos problemas en términos que son computables, pero no significa que todos los problemas los hagan con el mismo nivel de eficiencia. Hay problemas en los que los ordenadores cuánticos son más eficientes y en otros los ordenadores clásicos muestran un mejor desempeño. Para clarificar, una máquina de Turing es una cinta en la cual se pueden realizar ciertas operaciones y tiene una serie de símbolos; una QTM es una extensión en la cual se incorpora el principio de superposición y el entrelazamiento cuántico(Bonillo 2013).

En los 90 la teoría empezó a plasmarse y aparecen algoritmos cuánticos como el algoritmo de Shor (1994), un algoritmo para la factorización de números grandes. Este algoritmo es famoso porque consigue factorizar números en tiempo polinómico, lo cual es mucho más rápido que los mejores algoritmos clásicos conocidos, tales como el algoritmo de Pollard o el algoritmo paso de gigante paso de enano para hallar el logaritmo discreto. La importancia de este algoritmo radica en que la factorización de números grandes es la base de la seguridad de muchos sistemas criptográficos clásicos, como el algoritmo RSA o el algoritmo de curvas elípticas. Con este algoritmo, los ordenadores cuánticos dejaron de verse como algo de nicho(Bonillo 2013).

En 1998 fue desarrollado el primer ordenador cuántico experimental por un equipo de investigadores del *MIT (Massachusetts Institute of Technology)* y científicos de la Universidad de Oxford, con lo cual dichos ordenadores dejaron de ser algo hipotético. Este dispositivo utilizaba *resonancia magnética nuclear (RMN)* para manipular *moléculas líquidas*. Utilizaba como qubit el *espín de los núcleos atómicos*. El espín es una propiedad cuántica fundamental que describe el momento angular intrínseco de una partícula subatómica, como un electrón o un núcleo atómico. En términos simples, el espín puede ser visualizado como una especie de "imán cuántico": si está arriba, es un 1, y si está abajo, representa un 0. Para manipular dicho espín se utiliza un *campo electromagnético* extremadamente fuerte, mediante pulsos de ondas calibrados en frecuencia y duración. El proceso de medición se consigue mediante los ecos que devuelven dichos núcleos atómicos (eco cuántico). Estos ordenadores, como el resto que sucederán, tienen el mayor problema hasta la actualidad: la *decoherencia cuántica*. Cuando el sistema se mide, la función de onda colapsa de forma probabilística. La medición no tiene que ser algo intencionado y de ahí el problema: cualquier ruido electromagnético va a conseguir que se pierda esa coherencia cuántica y, por lo tanto perder la superposición, con lo cual se pierden las ventajas que tienen frente a un ordenador clásico. Solo interesa hacer dicha medición al final del algoritmo para saber el resultado(Bonillo 2013).

En 2001, *IBM consiguió un hito importante en la computación cuántica al factorizar el número 15 utilizando 7 qubits*; dicho logro se obtuvo mediante *resonancia magnética nuclear (RMN)*. IBM fue pionero en el uso de superconductores, pero fue D-Wave (2007) el que sacó el primer ordenador(D-Wave One) cuántico que utilizaba superconductores; aunque era un *quantum annealing* (técnica de optimización para encontrar el mínimo de una función de coste), no era una máquina cuántica universal. Lo interesante es el uso de superconductores, ya que dicha tecnología a día de hoy es la dominante porque pueden comportarse como qubits controlados con alta fidelidad, operan en frecuencias de microondas y es más fácil la lectura de sus estados cuánticos. En 2011, D-Wave, basado en los superconductores, lanzó la *primera computadora cuántica comercial*; aunque su diseño también era para problemas específicos, no era una QTM completa(Jones 2013).

*Google consiguió lograr la supremacía cuántica* (2019) con su procesador cuántico *Sycamore*. Este chip cuántico, compuesto por 53 qubits superconductores, realizó una tarea que tomaría a un supercomputador 10 000 años en tan solo 200 segundos. Dicha tarea consistía en generar y verificar una secuencia de números aleatorios. Aunque IBM refutó algunas de las estimaciones de Google, sugiriendo que podría tomar “solo” unos pocos días en lugar de milenios (CUÁNTICA and FLORES, n.d.).

El objetivo es lograr el santo grial: 1000 qubits lógicos; esto permitiría resolver problemas aún más complejos que no son factibles para los ordenadores cuánticos actuales, abriendo la puerta a nuevas aplicaciones en áreas como la simulación de materiales, la criptografía cuántica y la optimización de procesos en diversos campos. Esto es muy difícil actualmente, porque controlar $2^{1000}$ estados de forma que evolucione exactamente como queremos sin que caiga en la decoherencia es muy difícil, porque sería controlar más estados que partículas que tiene el universo, ya que $2^{1000} > 10^{80}$ (partículas que hay en el espacio)(Dyakonov 2019).

![[Google_Sycamore_quantum_computer.jpg]]
*Google Sycamore quantum computer*

## Estudio teórico

> ¡Qué follón!
>
> — Juan Cuesta, \*Aquí no hay quien viva\* \### Introducción {#sec:introduccion-teoria}

En este apartado se describe el estado del arte de los simuladores cuánticos y se explica la base teórica de su funcionamiento, explicando las matemáticas que subyacen detrás de ellos.

### Estado del Arte

Los simuladores cuánticos son una herramienta esencial para comprender y explorar los sistemas cuánticos complejos que resultan intratables para ordenadores clásicos. Existen dos grandes enfoques de simuladores: los simuladores cuánticos digitales, que utilizan puertas cuánticas y algoritmos para emular el comportamiento de un sistema cuántico (estos son los que trataremos en dicho TFM), y los simuladores analógicos, que recrean la dinámica del sistema utilizando otro sistema cuántico controlado.

Este concepto se lo debemos a Richard Feynman, quien argumentó que los ordenadores clásicos no podrían simular eficientemente la física debido al crecimiento exponencial del espacio de Hilbert (Feynman 1982).

Los simuladores analógicos han mostrado resultados pioneros como la observación del magnetismo cuántico, la localización de Anderson y la dinámica de fases cuánticas.

Los simuladores cuánticos analógicos son bastante útiles para estudiar modelos concretos de materia condensada, física de partículas o química cuántica. Algunos ejemplos son átomos ultrafríos en redes ópticas que sirven para simular modelos de Hubbard, iones atrapados que se usan para emular modelos de Ising y Heisenberg, defectos en diamantes que simulan dinámica de espines cuánticos y decoherencia, y cavidades ópticas que simulan la interacción luz-materia y efectos QED cuántica.

Los simuladores digitales son realmente útiles para el desarrollo y la prueba de conceptos de algoritmos cuánticos sin tener un sistema real con que probarlos.

Plataformas como Qiskit y Cirq han sido fundamentales para el desarrollo de dichas pruebas, permitiendo simular y desplegar estos algoritmos en hardware cuántico real o simulador.

Estas plataformas utilizan la nube, por lo cual se pueden hibridar dichos sistemas entre sistemas clásicos y sistemas cuánticos, permitiendo que los computadores cuánticos sean servicios solicitados por aplicaciones que son ejecutadas en sistemas tradicionales.(Microsoft 2025)

Por otro lado, aunque se habla de procesadores que tienen cientos, incluso miles de qubits, se refieren a qubits físicos, que no son lo mismo que qubits lógicos, y los ordenadores cuánticos, lo máximo que manejan actualmente es un número de 50 qubits lógicos hasta 2025. El número permitido de qubits en simuladores cuánticos está en la mayoría de los casos rondando los 30 qubits; por lo tanto, son una alternativa gratuita que casi está a la par en número de qubits.

### Fundamentos de la computación cuántica

#### Principios matemáticos de la computación cuántica

La computación cuántica difiere de la computación clásica en que su elemento mínimo no es el bit, es el qubit. Se explicarán más adelante en profundidad, pero resumiendo, un qubit puede adquirir dos estados: o bien un uno, o un cero, o una superposición de ambos estados, siendo bastante útil para nuevos algoritmos que se aprovechan de dicha superposición, haciendo que algoritmos que serían inabarcables en un computador clásico vuelvan dichos problemas en problemas de tiempo polinómico. Estos computadores disponen de diferentes puertas lógicas, que, dichas puertas lógicas, no son las habituales en la computación clásica a la que estamos acostumbrados, ya que deben ser reversibles, deben ser pulsos que cambian el estado cuántico del sistema sin perder la coherencia del sistema, es decir, sin que los qubits colapsen.

La computación cuántica se trata de una combinación de tres características ligadas a la mecánica cuántica: superposición, entrelazamiento e interferencia (Wikipedia contributors 2025a).

Otra diferencia fundamental: la computación clásica se centra en el álgebra de Boole; en cambio, la computación cuántica se fundamenta en el álgebra lineal, en el estudio de espacios vectoriales, matrices y operaciones lineales en dichos espacios.

Para lograr un entendimiento claro, se necesita un dominio del álgebra lineal. En este TFM, no profundizaremos mucho, pero daremos unas bases para que el lector pueda comprender más o menos el funcionamiento de las puertas lógicas y la construcción de dichos algoritmos.

#### Espacios vectoriales. Notación de Dirac

Un espacio vectorial es un conjunto de vectores que conforma un espacio en el cual se pueden sumar y multiplicar por ellos mismos y por números escalares.

El espacio vectorial que nos interesa es el $\mathbb{C}^n$, que es el espacio de las $n$-tuplas de números complejos. Los vectores pueden ser vectores fila o columna. La traspuesta de un vector es una operación reversible que vuelve un vector columna a un vector fila y viceversa.(Castillo Gómez 2024)

$$\begin{bmatrix}
    z_1 \\
    z_2
\end{bmatrix}^\dagger = 
\begin{bmatrix}
    z_1 & z_2
\end{bmatrix}$$

En la computación cuántica se utilizan vectores columna para representar los estados del sistema.

$$\begin{bmatrix}
    z_1 \\
    \vdots \\
    z_n
\end{bmatrix}$$

La **suma de vectores** se realiza de la siguiente manera:

$$\begin{bmatrix}
    z_1 \\
    \vdots \\
    z_n
\end{bmatrix}
+
\begin{bmatrix}
    z_1' \\
    \vdots \\
    z_n'
\end{bmatrix}
=
\begin{bmatrix}
    z_1 + z_1' \\
    \vdots \\
    z_n + z_n'
\end{bmatrix}$$

De igual manera, en el espacio $\mathbb{C}^n$ existe la multiplicación de vectores por productos escalares:

$$z \begin{bmatrix}
    z_1 \\
    \vdots \\
    z_n
\end{bmatrix}
\equiv
\begin{bmatrix}
    z z_1 \\
    \vdots \\
    z z_n
\end{bmatrix},$$

En los sistemas cuánticos, un qubit es representado por un vector columna de dos elementos que, al sumar sus cuadrados, debe ser igual a uno. Cada elemento del sistema representa la probabilidad de que colapse a un estado u otro.

La notación de Dirac, también conocida como la notación *bra-ket*, es el estándar en la mecánica cuántica, utilizada para describir los estados cuánticos dentro de la mecánica cuántica. Su nombre viene porque el producto de dos estados se nombra con los paréntesis angulares “angle bracket”: (Castillo Gómez 2024) $\langle \phi | \psi \rangle$ Consistiendo $\phi$ en la parte izquierda (bra) y $\psi$ en la parte derecha (ket).

- El ket representa una matriz columna dentro del espacio de Hilbert.

- El bra es el vector transpuesto o el vector fila.

Dentro del espacio vectorial se posee el **vector cero**. Este vector no utiliza la notación vectorial de Dirac, ya que $|0\rangle$ representa un estado de un *qubit* y no al vector cero:

$$|0\rangle = 
\begin{bmatrix}
    1 \\
    0
\end{bmatrix}$ El vector $|j\rangle$ es aquel cuyo componente $j$ tiene el valor 1 y el resto de los componentes son 0. La siguiente convención se usa para representar *qubits* que codifican los valores de cero y uno: $\begin{bmatrix}
    1 \\
    0
\end{bmatrix}
= |0\rangle, \quad
\begin{bmatrix}
    0 \\
    1
\end{bmatrix}
= |1\rangle$ Un *qubit* puede representarse de la siguiente forma: $a =
\begin{bmatrix}
    a_0 \\
    a_1
\end{bmatrix}
= a_0 |0\rangle + a_1 |1\rangle =
a_0
\begin{bmatrix}
    1 \\
    0
\end{bmatrix}
+ a_1
\begin{bmatrix}
    0 \\
    1
\end{bmatrix}$$ Las propiedades que tiene son las siguientes:

- Dado cualquier *bra* $\langle \phi |$ y *kets* $|\psi_1\rangle$ y $|\psi_2\rangle$, y números complejos $c_1$ y $c_2$, entonces, puesto que los núcleos son *funcionales lineales*, $\langle \phi | \left( c_1 |\psi_1\rangle + c_2 |\psi_2\rangle \right) = c_1 \langle \phi | \psi_1 \rangle + c_2 \langle \phi | \psi_2 \rangle.$

- Dado cualquier *ket* $|\psi\rangle$, núcleos $\langle \phi_1 |$ y $\langle \phi_2 |$, y números complejos $c_1$ y $c_2$, entonces, por la definición de la adición y la *multiplicación escalar* de funcionales lineales, $\left( c_1 \langle \phi_1 | + c_2 \langle \phi_2 | \right) |\psi\rangle = c_1 \langle \phi_1 | \psi \rangle + c_2 \langle \phi_2 | \psi \rangle.$

- Dados cualesquiera *kets* $|\psi_1\rangle$ y $|\psi_2\rangle$, y números complejos $c_1$ y $c_2$, de las propiedades del producto interno (con $c^*$ denotando la *conjugación compleja* de $c$), $c_1 |\psi_1\rangle + c_2 |\psi_2\rangle$ es dual a $c_1^* \langle \psi_1 | + c_2^* \langle \psi_2 |.$

- Dado cualquier *bra* $\langle \phi |$ y el *ket* $|\psi\rangle$, una propiedad axiomática del producto interno da $\langle \phi | \psi \rangle = \langle \psi | \phi \rangle^*.$

Los *bra-ket* son bastante útiles porque facilitan los cálculos en la mecánica cuántica. Permiten expresar operadores y proyecciones entre estados. Es independiente de la base específica.

#### Espacio de Hilbert

El **espacio de Hilbert** es una generalización del espacio euclidiano que es formado por el producto escalar de varios vectores y es completo a la norma inducida. Esto significa que cualquier sucesión de Cauchy en este espacio va a converger. Dicho de grueso modo, no hay "lagunas" dentro del espacio; la sucesión de vectores se acercará entre los dos. Esto es útil porque garantiza que las sucesiones convergentes no se escapen fuera del espacio. En la computación cuántica se utiliza para describir vectores de estado en un espacio de Hilbert. Estos vectores representan la probabilidad de que el vector colapse a cero o a uno.(Wikipedia 2024c) La norma de un estado $|\psi\rangle$ es la raíz cuadrada de su propio producto interno, de la siguiente manera:

$$\| |\psi\rangle \| \equiv \sqrt{\langle \psi | \psi \rangle}$$

Dicha magnitud representa la longitud en el espacio de Hilbert. Para que un vector se considere un estado válido, tiene que estar dicho vector normalizado.

$$\frac{|\psi\rangle}{\| |\psi\rangle \|}$$

Esto es válido para cualquier vector que no sea cero.

Resumiendo, en la computación cuántica, los espacios de Hilbert se utilizan para modelar qubits y las transformaciones sobre ellos.

##### Producto interior. Normas.

También es conocido como producto escalar; es una operación algebraica que toma dos vectores y retorna un valor numérico. Dados dos vectores $\mathbf{u} = (u_1, u_2, \ldots, u_n)$ y $\mathbf{v} = (v_1, v_2, \ldots, v_n)$, su **producto escalar** se define como: $\mathbf{u} \cdot \mathbf{v} = u_1 \cdot v_1 + u_2 \cdot v_2 + \ldots + u_n \cdot v_n$ Cumple las siguientes propiedades:

1.  **Linealidad:** $$\langle au + bv, w \rangle = a \langle u, w \rangle + b \langle v, w \rangle,
        \quad \forall a,b \in \mathbb{K}.$$

2.  **Simetría (o hermiticidad en el caso complejo):** $\langle u, v \rangle = \overline{\langle v, u \rangle}.$

3.  **Positividad:** $$\langle v, v \rangle \geq 0 
        \quad \text{y} \quad 
        \langle v, v \rangle = 0 \iff v = 0.$$

A partir del producto interior se define una **norma inducida**: $\|v\| = \sqrt{\langle v, v \rangle}.$

Esta norma permite medir la longitud de los vectores y definir conceptos como convergencia y ortogonalidad dentro del espacio.

##### Producto tensorial

Se puede construir con dos vectores $\psi \in H^{(n)}$ y $\phi \in H^{(n')}$ un nuevo vector dentro del espacio de Hilbert con mayor dimensión mediante la operación del producto tensorial $\psi \otimes \phi$. Este nuevo vector tiene la dimensión $H^{(n \cdot n')}$ y se obtiene por cada elemento $\psi$. Dicho resultado se puede observar con el siguiente ejemplo: $$\psi \otimes \phi =
\begin{bmatrix}
    \psi_0 \\
    \psi_1
\end{bmatrix}
\otimes
\begin{bmatrix}
    \phi_0 \\
    \phi_1
\end{bmatrix}
=
\begin{bmatrix}
    \psi_0 \phi_0 \\
    \psi_0 \phi_1 \\
    \psi_1 \phi_0 \\
    \psi_1 \phi_1
\end{bmatrix}.$$ La importancia de este radica en que sirve para describir un estado formado por varios qubits. Gracias a este se modela la superposición de estados y el entrelazamiento cuántico.

#### Qubit

El término de *qubit* surge por Benjamin Schumacher, quien describía la forma de comprimir la información en un estado y poder almacenar esta compresión de Schumacher (Schumacher 1995). Un *qubit* es un sistema cuántico con dos estados propios y que puede ser manipulado arbitrariamente, es decir, se trata de un sistema que puede ser descrito mediante la mecánica cuántica y que puede verse como un vector de módulo unitario en un espacio vectorial complejo bidimensional. Los estados en los que puede estar son $|1\rangle$ o $|0\rangle$ y, además, se puede encontrar en un estado de superposición de ambos estados.

La importancia de esto radica en que estos sistemas son altamente paralelizables, en los cuales el sistema puede representar simultáneamente los valores 0 y 1. No todos los algoritmos pueden aprovechar esto, solo los algoritmos cuánticos que operan sobre estados de superposición y realizan simultáneamente todas las combinaciones. Tal es el grado de paralelización que un *qubit* puede hacer 2 operaciones al mismo tiempo; con 2 *qubits* se pueden realizar 4 operaciones al mismo tiempo, y así, con cada vez más *qubits*, se tiene un crecimiento exponencial. Para hacerse una idea, un computador cuántico de 30 *qubits* equivaldría a un procesador convencional de 10 teraflops, mientras que actualmente los ordenadores trabajan en el orden de gigaflops (flops = operaciones de coma flotante).(Bonillo 2013)

La siguiente característica importante es que múltiples *qubits* pueden presentarse en un estado de entrelazamiento cuántico, por lo cual una operación sobre un *qubit* puede afectar a varios al mismo tiempo. Un sistema de dos *qubits* entrelazados no puede descomponerse en factores independientes; esto puede emplearse para hacer comunicación.(Bonillo 2013) Para finalizar, los *qubits* se representan mediante la esfera de Bloch, y los operadores que se le aplican cambian la probabilidad de que colapse en un estado u otro dentro de la esfera de Bloch. (Bonillo 2013)

![[Figura-21-Esfera-de-Bloch-El-estado-ps-se-encuentra-en-la-superficie-de-la-esfera.png]]
*Esfera de Bloch*

#### Postulados de la mecánica cuántica

Para entender el funcionamiento de los ordenadores cuánticos, es importante hacer una aproximación a la mecánica cuántica; esta puede ser de dos formas distintas.(Bonillo 2013) La primera es a través de aquellos problemas que la mecánica clásica no puede resolver, que son los siguientes:

- La ley de radiación espectral del cuerpo negro.

- El efecto fotoeléctrico.

- Las capacidades caloríficas de los sólidos.

- El espectro atómico del átomo de hidrógeno.

- El efecto Compton.

![[radiacion-cuerpo-negro.png]]
*Radiación de cuerpo negro*
![[efecto fotoelectrico.png]]
*Efecto fotoeléctrico*
![[espectrohidrogeno.jpg]]
*Espectro del hidrógeno*
![[compton1.jpg]]
*Efecto Compton*

*Fenómenos cuánticos fundamentales*

La segunda forma es a través de una vía más axiomática. Partimos de postulados fundamentales y de estos se deducen resultados sobre el comportamiento de sistemas físicos de escala nanométrica. Dichos resultados luego se contrastan mediante experimentación. En este trabajo lo abordamos desde la segunda forma. El formalismo más conocido es el de Schrödinger, que se basa en la descripción ondulatoria de la materia. Pero el que nos interesa es el de Heisenberg y Dirac, porque emplea álgebra de vectores, operadores y matrices. Schrödinger demostró que tanto el suyo como este son equivalentes.

![[Padres de la física cuantica.png]]
*Paul Dirac, Heisenberg y Erwin Schrödinger*

Los postulados en los que se centra principalmente son:

El **primer postulado**, el estado de un sistema físico está descrito por una función $\Psi(q,t)$ de las coordenadas ($q$) y del tiempo ($t$). Contiene toda la información que se puede determinar de un sistema.

El **segundo postulado** es que a los observables físicos les corresponde un operador lineal y hermítico que actúa sobre la función de onda. Estos operadores son las funciones que realizamos sobre nuestra función de onda para obtener un observable físico. Los observables físicos son todos aquellos valores que podemos medir de forma real de la función de onda. En nuestro circuito cuántico serían las puertas cuánticas, que manipulan la superposición sin que esta colapse.

El **tercer postulado** se refiere a las mediciones, que solo pueden dar autovalores del operador correspondiente. Por ejemplo, al medir un qubit, el único resultado que puede dar es 0 o 1. El autovalor es el número que multiplica la función de onda como resultado de aplicarle un operador. Ya que la función de onda es una autofunción, es decir, al multiplicarla por un operador está devolviendo la función de onda por un autovalor, y son estos autovalores los valores a medir (Departamento de Física 2020). Para clarificar esto de una manera más sencilla: la función de onda contiene toda la información de nuestro sistema, pero para poder obtenerla hay que utilizar operadores. Cuando se aplican estos operadores, la función de onda queda multiplicada por un autovalor. En el caso de la computación cuántica, este autovalor sería 0 o 1 una vez colapse la función de onda.

El **cuarto postulado** se centra en el colapso de la función de onda. Después de realizar una medición, el sistema colapsa a la autofunción asociada al valor medido. Lo cual quiere decir que, antes de medir, el sistema podría estar en una superposición de estados. Tras medir y obtener el autovalor, el estado colapsa a la autofunción correspondiente. Dicho colapso no es gradual y es aleatorio.

El **quinto postulado** es la ecuación de Schrödinger,(Wikipedia 2025a) que determina la evolución en el tiempo del estado de un sistema cuántico:

$$i\hbar \frac{\partial \Psi(q,t)}{\partial t} = \hat{H} \Psi(q,t)$$

donde $\hbar = \frac{h}{2\pi}$, siendo $h$ una constante conocida como la constante de Planck, y donde $H$ es el operador hamiltoniano, que representa la energía que se le suministra al sistema. El operador hamiltoniano es bastante útil porque en él se basa la construcción de las diferentes puertas lógicas.(Bonillo 2013)

Nuestras puertas lógicas van a resultar en transmitir energía al sistema para cambiar el estado de nuestro sistema, manteniendo la coherencia. Por ejemplo, en un sistema que utiliza los espines de los núcleos atómicos como estados de qubit, el cambio en este se hace mediante impulsos electromagnéticos.

### Puertas lógicas cuánticas

Es un circuito que opera sobre un pequeño número de *qubits*. Por lo que hemos visto en capítulos anteriores, estas puertas son reversibles, a diferencia de las puertas lógicas clásicas. Estas puertas se representan mediante matrices unitarias. Las más comunes son las que operan en un espacio de uno o dos *qubits*, lo que significa que las matrices pueden ser de $2 \times 2$ o de $4 \times 4$, con filas ortonormales.

A continuación se explican las más comunes (Wikipedia 2024d).

#### Puerta X

Esta puerta es como la puerta NOT clásica; si llega un 0, lo transforma en un 1; en cambio, si llega un 1, lo transforma en un 0; invierte los estados bases. También actúa sobre la superposición, la cual se vuelve bastante interesante.

La matriz de puerta x es la siguiente: $$X =
\begin{bmatrix}
    0 & 1 \\
    1 & 0
\end{bmatrix}$$ Su acción sobre los estados bases es la siguiente: $$X|0\rangle = |1\rangle$$ $$X|1\rangle = |0\rangle$$ Cuando está en superposición, actúa sobre la amplitud, cambiándola, como se puede ver en el ejemplo:

$$X|\psi\rangle = X(\alpha|0\rangle + \beta|1\rangle) = \alpha|1\rangle + \beta|0\rangle$$

#### Puerta Z

La puerta Z cambia solo la fase al estado si es $|1\rangle$; si es $|0\rangle$, no le cambia la fase. Esto es muy útil porque afecta al fenómeno de interferencia; estas fases no alteran la probabilidad de medición, sino que alteran la evolución del sistema cuando hay superposición.

La matriz es la siguiente: $$Z =
\begin{bmatrix}
    1 & 0 \\
    0 & -1
\end{bmatrix}$$ Su acción sobre los estados es la siguiente: $$Z|0\rangle = |0\rangle$$ $$Z|1\rangle = -|1\rangle$$ La transformación que realiza es la siguiente: $$Z|\psi\rangle = Z(\alpha|0\rangle + \beta|1\rangle) = \alpha|0\rangle - \beta|1\rangle$$

#### Puerta Y

Es una combinación de la puerta X y de la puerta Z. Es especialmente útil en la rotación del plano complejo.

Su representación matricial es la siguiente: $$Y =
\begin{bmatrix}
    0 & -i \\
    i & 0
\end{bmatrix}$ Y los vectores en notación de Dirac son: $|0\rangle =
\begin{bmatrix}
    1 \\
    0
\end{bmatrix},
\quad
|1\rangle =
\begin{bmatrix}
    0 \\
    1
\end{bmatrix}$$ Su acción sobre los estados es la siguiente:

$Y|0\rangle = i|1\rangle$ $Y|1\rangle = -i|0\rangle$ La transformación que realiza es la siguiente: $Y(\alpha|0\rangle + \beta|1\rangle) = -i\beta|0\rangle + i\alpha|1\rangle$

#### Puerta S

Si es cero no cambia su estado pero si es uno lo multiplica por el número imaginario i: $$S|0\rangle = |0\rangle$$ $$S|1\rangle = i|1\rangle$$ Su matriz es la siguiente: $$S =
\begin{bmatrix}
    1 & 0 \\
    0 & i
\end{bmatrix}$ La transformación que realiza es la siguiente: $S(\alpha|0\rangle + \beta|1\rangle) = \alpha|0\rangle + i\beta|1\rangle$ Es una puerta bastante útil porque permite controlar la fase sin alterar las probabilidades de estas. También, tiene la propiedad curiosa de que aplicar dos veces la misma puerta resulta en una puerta Z. $S^2 =
\begin{bmatrix}
    1 & 0 \\
    0 & i
\end{bmatrix}
\cdot
\begin{bmatrix}
    1 & 0 \\
    0 & i
\end{bmatrix}
=
\begin{bmatrix}
    1 \cdot 1 & 0 \cdot i \\
    0 \cdot 1 & i \cdot i
\end{bmatrix}
=
\begin{bmatrix}
    1 & 0 \\
    0 & i^2
\end{bmatrix}
=
\begin{bmatrix}
    1 & 0 \\
    0 & -1
\end{bmatrix}
= Z$$

#### Puerta I

Es la puerta identidad que se corresponde a la matriz identidad por lo tanto no hace nada. Su matriz es la siguiente: $$I =
\begin{bmatrix}
    1 & 0 \\
    0 & 1
\end{bmatrix}$$ La transformación que realiza es la siguiente: $$I(\alpha|0\rangle + \beta|1\rangle) = \alpha|0\rangle + \beta|1\rangle$$ Aunque la utilidad de dicha puerta parece ponerse en duda viendo que no hace nada, sin embargo, dicha puerta también es muy útil, ya que se utiliza para mantener la sincronía entre distintos qubits del circuito, produciendo espera activa en un qubit mientras otros realizan operaciones.

#### H-Hadamard

Esta puerta pone en superposición el *qubit*; es de las más importantes, si no la más importante, ya que para el empleo de dichos algoritmos cuánticos es necesaria. Esta puerta realiza la siguiente operación dentro de la esfera de Bloch:

$|0\rangle \rightarrow \frac{|0\rangle + |1\rangle}{\sqrt{2}} \equiv |+\rangle$ $|1\rangle \rightarrow \frac{|0\rangle - |1\rangle}{\sqrt{2}} \equiv |-\rangle,$ La rotación en la esfera de Bloch se realiza a uno de los siguientes estados: $\{|+\rangle, |-\rangle\}$ . Si es cero, lo pone en estado positivo; si es uno, lo pone en estado negativo. Haciendo que el qubit esté en estado de superposición tanto para 0 como para 1 y solo cuando se mide en uno de estos estados, colapse en uno de los dos.

Se representa de la siguiente manera: $$H = \frac{1}{\sqrt{2}} \begin{bmatrix} 
    1 & 1 \\
    1 & -1 
\end{bmatrix}$$ Se utiliza $\frac{1}{\sqrt{2}}$ porque, al elevarlo al cuadrado, como vimos en capítulos anteriores, nos proporciona la probabilidad de que el *qubit* sea 0, que es 0.5

#### Puertas CTRL

##### Puerta CNOT

La más común es la puerta CNOT. Si las puertas Hadamard son las que ponen en superposición los *qubits*, las puertas CTRL son las que establecen el entrelazamiento entre los distintos *qubits*.

La puerta CNOT, su funcionamiento es parecido al de la puerta clásica XOR; tiene unos qubits de control y otros que son objetivos. Si el qubit de control es 0, no hace nada; si es 1, cambia el qubit objetivo aplicando una puerta NOT.

Su tabla de verdad sería la siguiente: $$\begin{array}{cc|c}
    \text{Control} & \text{Objetivo} & \text{Salida} \\
    \hline
    |0\rangle & |0\rangle & |0\rangle|0\rangle \\
    |0\rangle & |1\rangle & |0\rangle|1\rangle \\
    |1\rangle & |0\rangle & |1\rangle|1\rangle \\
    |1\rangle & |1\rangle & |1\rangle|0\rangle \\
\end{array}$ Su matriz es la siguiente: $\text{CNOT} =
\begin{bmatrix}
    1 & 0 & 0 & 0 \\
    0 & 1 & 0 & 0 \\
    0 & 0 & 0 & 1 \\
    0 & 0 & 1 & 0
\end{bmatrix}$$ La transformación sería la siguiente: $$|\psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)$$

##### Puerta Toffoli

Es una de las puertas más conocidas y más importantes, también conocida como CCNOT. Su función es la siguiente: tiene 2 *qubits* de control y 1 *qubit* objetivo. Si las dos entradas del *qubit* de control se activan con 1, esta cambia el estado del *qubit* objetivo, funcionando como una puerta AND clásica. Su tabla de verdad es la siguiente:$$\begin{array}{ccc|c}
    \text{Control}_1 & \text{Control}_2 & \text{Objetivo} & \text{Salida} \\
    \hline
    |0\rangle & |0\rangle & |0\rangle & |0\rangle|0\rangle|0\rangle \\
    |0\rangle & |0\rangle & |1\rangle & |0\rangle|0\rangle|1\rangle \\
    |0\rangle & |1\rangle & |0\rangle & |0\rangle|1\rangle|0\rangle \\
    |0\rangle & |1\rangle & |1\rangle & |0\rangle|1\rangle|1\rangle \\
    |1\rangle & |0\rangle & |0\rangle & |1\rangle|0\rangle|0\rangle \\
    |1\rangle & |0\rangle & |1\rangle & |1\rangle|0\rangle|1\rangle \\
    |1\rangle & |1\rangle & |0\rangle & |1\rangle|1\rangle|1\rangle \\
    |1\rangle & |1\rangle & |1\rangle & |1\rangle|1\rangle|0\rangle \\
\end{array}$ Su matriz es la siguiente: $\text{Toffoli} =
\begin{bmatrix}
    1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\
    0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\
    0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\
    0 & 0 & 0 & 0 & 0 & 0 & 1 & 0 \\
\end{bmatrix}$$ Se expresa de la siguiente forma: $$\text{Toffoli}(|a\rangle \otimes |b\rangle \otimes |c\rangle) = |a\rangle \otimes |b\rangle \otimes |c \oplus (a \cdot b)\rangle$$

### Algoritmos Cuánticos

En computación cuántica, un algoritmo cuántico es aquel que se ejecuta en un modelo realista de computación cuántica (Wikipedia 2024a). En esta sección se explican algunos de los algoritmos más relevantes de la historia.

![[Quantum_Fourier_transform_on_three_qubits.svg.png]]
*Transformada cuántica de Fourier sobre tres qubits, basada en la aplicación reiterada de la puerta cuántica de Hadamard y de puertas de cambio de fase*

#### Deutsch-Jozsa

Esta sección la empezamos con el algoritmo Deutsch-Jozsa, porque fue el primero en demostrar que había problemas computacionales que se podían resolver de manera más eficiente utilizando un algoritmo cuántico que su homologo clásico.(Qiu and Zheng 2018)

##### Planteamiento

El problema de Deutsch-Jozsa es, dada una función f, saber si esa función es constante o es balanceada. En el caso de que sea constante la entrada, no influye en el resultado. Si es balanceada, la mitad de las entradas corresponde a cero y la otra mitad corresponde a uno.

$f$ la podemos ejemplificar de la siguiente manera, siendo $n$ el número de bits de entrada:

$$f: \{0,1\}^n \rightarrow \{0,1\}$$

- **Función constante:** $f(x) = c$ para todo $x$, donde $c$ es un valor fijo en $\{0,1\}$.

- **Función balanceada:** $f(x) = 0$ para exactamente la mitad de las entradas y $f(x) = 1$ para la otra mitad.

##### Resolución Clásica

La resolución clásica es probar la mitad de entradas más uno en el peor de los casos para poder determinar si es balanceada o es constante. Las consultas quedarán de la siguiente manera: $f(0,0,0,\ldots) \rightarrow 0$ y $f(1,0,0,\ldots) \rightarrow 1$.

En el peor, de los casos, sería la mitad más uno: $2^{n-1} + 1$.

##### Resolución Cuántica

Lo primero que podemos notar es que la salida en la resolución es un 1 dado $n$ *bits*, lo que rompe con la reversibilidad.

Antes de nada, quiero hacer un pequeño inciso para que el lector entienda la importancia de la reversibilidad. Es una característica inherente a la computación cuántica, como hemos visto en apartados anteriores, que viene dada desde la ecuación de Schrödinger. Esto es debido a que todo sistema cuántico cerrado está gobernado por dicha ecuación y su solución es una transformación unitaria. Las matrices unitarias, por definición, tienen inversa (la conjugada de la transpuesta). Por lo tanto, ninguna información puede perderse en la evolución del sistema. Solamente se pierde dicha propiedad cuando se mide el sistema y la función de onda colapsa a uno de sus autovalores. Pero en nuestro caso, nos interesa mantener el mayor tiempo posible la superposición de estados para poder ejecutar nuestro algoritmo, y solamente nos interesa que pierda dicha propiedad cuando deseamos obtener el resultado. Por eso, nuestro objetivo es mantener dicha propiedad.

Dado $n$ *bits* que dan como resultado un *bit*, a partir de ese *bit* no se puede obtener la entrada. Por lo tanto, el primer gran cambio que se tiene en la resolución cuántica es que el número de *qubits* de entrada debe ser el mismo que el de salida. Aparte de eso, para poder conservar la reversibilidad, se necesita un *qubit* adicional en el cual se pueda volver a la entrada, ya que, por definición, el resultado se XOR-ea en este.

Dada la definición más común de oráculos, aunque hay otros:

$$U_f |x\rangle |y\rangle = |x\rangle |y \oplus f(x)\rangle$$

El $\oplus$ es la operación xor.

El circuito queda de la siguiente manera:

![[circuito de Deutsch-Jozsa.png]]
*Esquema genérico del circuito de Deutsch-Jozsa*

Otro concepto importante es el *phase kickback* o retroceso de fase, el cual es un fenómeno cuántico que ocurre principalmente en computación cuántica cuando se utilizan puertas controladas, como es nuestro caso la puerta CNOT, en un circuito que está en superposición. Si tienes dos *qubits*, el *qubit* de control que está en un estado de superposición y el *qubit* objetivo está en un estado propio, al aplicar una operación al *qubit* objetivo, la fase queda reflejada hacia atrás en el *qubit* de control.

Esto es muy importante porque, al medir el resultado, solo nos interesa ver los *qubits* de entrada y no el auxiliar, porque si ha habido un cambio en el oráculo. Es decir, si es balanceada, porque la salida depende de la entrada, va a quedar reflejada en la fase de los $x$ *qubits*, y es por eso que solo se miden los $x$ *qubits* y no el *qubit* auxiliar.

Teniendo en cuenta los conceptos anteriores, como la reversibilidad, phase kickback y la definición común de un oráculo, vamos a explicar el funcionamiento de dicho algoritmo en sus distintas etapas:

1.  **Preparación:** Los primeros $n$ *qubits* están en $|0\rangle$, mientras que el auxiliar es inicializado en $|1\rangle$.

    $$|\psi_0\rangle = |0\rangle^{\otimes n} |1\rangle.$$

    El bit auxiliar es inicializado a uno porque, por la definición del oráculo, dependiendo del resultado, afectará al resto de registros introduciendo una fase negativa.

2.  **Superposición mediante puertas de Hadamard:**

    Introducimos la superposición mediante puertas $H$, para así poder hacer con una única consulta todos los posibles valores.

    $$|\psi_1\rangle = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1} |x\rangle (|0\rangle - |1\rangle).$$

    Este sería el estado conjunto tanto de los $n$ qubits como del registro auxiliar. El registro auxiliar, al estar en uno, su resultado queda de la forma $(|0\rangle - |1\rangle)$.

3.  **Aplicar el oráculo cuántico:**

    Este paso es muy importante de entender y, como diría mi tutor de TFM, "es donde la matan", así que rogaría al lector que preste sumamente atención. Primero, la transformación es la siguiente. Teniendo en cuenta que partimos de un estado de superposición, aplicamos el oráculo:

    $$U_f |x\rangle |y\rangle = |x\rangle |y \oplus f(x)\rangle$$

    La transformación es la siguiente:

    \$\$

    \$\$

    Al hacer una serie de operaciones sabiendo que $f(x)$ puede ser igual a 0 o 1, cuando es uno, añade una fase negativa a los $n$ qubits; por lo tanto, nos queda de la siguiente manera:

    \$\$

    \$\$

    Como se puede apreciar, el resultado $f(x)$ es guardado en forma de fase en los $x$ qubits y se podrá saber si es balanceada o no observando dichos qubits.

4.  **Puerta de Hadamard a los $x$ qubits:**

    En este paso nos interesa deshacernos de la superposición y, sabiendo que la puerta Hadamard es reversible por sí misma, aplicamos dicha puerta.

    Para entender este paso, primero hay que tener en cuenta que el producto escalar bit a bit (mod 2) entre los vectores $x$ y $z$ se define de la siguiente manera:

    $$x \cdot y = x_0 y_0 \oplus x_1 y_1 \oplus \cdots \oplus x_{n-1} y_{n-1}$$

    El vector $z$ es una etiqueta que recorre los estados bases sobre los cuales está proyectado tu estado final.

    Por último, hay que tener en cuenta que la parte del vector auxiliar ya no nos interesa; por lo tanto, la podemos obviar.

    Teniendo en cuenta lo anterior, la transformación al aplicar una segunda Hadamard a un estado en superposición sería la siguiente:

    \$\$

    \$\$

    Al pasar por una segunda Hadamard, el estado $|\psi_3\rangle$, que está en función de $x$, tiene que reescribirse en función de $z$ y para su amplitud queda dada por la suma de sus interferencias, como se puede ver en el paso anterior, donde se hace el producto escalar de $x \cdot z$.

5.  **Medición:**

    Para la medición, nos tenemos que fijar en el resultado de $z$. Si $z$ es igual a cero, después de aplicar la segunda Hadamard, los qubits en el estado final son una función constante; en cambio, si $z$ es distinto, significa que es balanceada.

    - Si $z$ es cero, nos queda la siguiente función que, al medir la amplitud, nos dará como resultado 1 (es constante):

      $$\left| \frac{1}{2^n} \sum_{x=0}^{2^n - 1} (-1)^{f(x)} \right|^2,$$

    - En cambio, si es balanceada, nunca obtendrás $z=1$ y, por lo tanto, obtendrás la mitad de los valores $= -1$ y la otra mitad 1. Por lo tanto, se anulan entre ellos y la amplitud da igual a 0.

##### Diseño del algoritmo

Para diseñar el oráculo, primero debemos tener en cuenta si la función $f(x)$ es constante o balanceada.

- **Caso constante:** El oráculo es muy sencillo:

  - Si $f(x) = 0$, entonces no se realiza ninguna operación y se aplica una puerta identidad $I$ al qubit auxiliar.

  - Si $f(x) = 1$, se aplica una puerta NOT (X) al qubit auxiliar.

- **Caso balanceado:** Es decir, $f(x)$ devuelve 1 para la mitad de las entradas y 0 para la otra mitad. En este caso, para implementar el oráculo se utilizan puertas CNOT. Como recordamos anteriormente, las puertas CNOT funcionan de forma análoga a una compuerta clásica XOR.

![[oraculoDeut.png]]
*Circuito del oráculo para funciones balanceadas.*

Se pueden invertir los resultados de dicho oráculo utilizando puertas X.

![[oraculoDeutPuertaX.png]]
*Circuito del oráculo invertido para funciones balanceadas*

El circuito completo del algoritmo de Deutsch-Jozsa quedaría de la siguiente forma:

![[circuitocompleotDeutshc.png]]
*Circuito completo del algoritmo de Deutsch-Jozsa.*

#### Bernstein-Vazirani

El algoritmo de Bernstein-Vazirani es uno de los problemas sencillos para entender cómo los ordenadores cuánticos pueden explotar la superposición y la interferencia.

##### Planteamiento

Es parecido al Deutsch-Josza; el oráculo es una caja negra que toma una entrada de valores numéricos y los multiplica por un valor que es $s$ módulo dos. El objetivo es hallar s a partir de la entrada de valores, con el menor número posible de entradas.

La salida, al ser módulo 2, solo devuelve 0 o 1, como se puede ver en el siguiente ejemplo:

$$f(\{x_0, x_1, x_2, \ldots, x_n\}) \rightarrow 0 \ \text{o} \ 1 \quad \text{donde } x_n \text{ es } 0 \text{ o } 1$$

##### Resolución Clásica

Sabiendo que el oráculo devuelve la siguiente salida:

$$f_s(x) = s \cdot x \bmod 2$$

La resolución clásica consiste en hacer una especie de máscara (AND) utilizando la entrada en la cual se pasa un uno en una posición determinada, como puede ser al principio de todo, y en el resto de la entrada se pasa cero. Este uno va cambiando de posición en un circuito clásico mediante un shifter. Con esto, podemos hallar $s$, ya que devolverá un uno si en la posición donde está un 1 en la entrada $x$, también hay un 1 en esa misma posición del vector $s$.

| **Entrada ($x$)** | **Salida ($f_s(x)$)** |
|:------------------|:----------------------|
| …0                |                       |
| 010…0             |                       |
| …0                |                       |
| 000…1             |                       |

Ejemplo de entradas y salidas en el algoritmo de Bernstein–Vazirani para $s = 000\ldots1$

Como se puede ver en el ejemplo anterior, sabemos que el vector $s$ está compuesto por todos ceros, salvo el último valor que es un uno. En el modelo clásico, como podemos observar, para evaluar $s$, se necesitan hacer exactamente $n$ (longitud del vector $x$) entradas. En cambio, con el algoritmo cuántico, lo hace con una sola llamada.

##### Resolución Cuántica

La resolución de dicho problema es muy parecida a la de Deutsch y Jozsa; para su resolución, nos basaremos, como en el caso anterior, en el retardo de fase previamente visto.

$$\begin{aligned}
    |\psi\rangle = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} |x\rangle (|0\rangle - |1\rangle). \tag{1}
\end{aligned}$$

Tiene unos pequeños cambios respecto al algoritmo anterior.

1.  **Inicialización:**

    Los *qubits* $x$ están en el valor: $|0\rangle^{\otimes n}$ y el *qubit* auxiliar se inicializa en uno con una puerta $X$ y luego, con una puerta $H$, queda en el estado $|-\rangle$, como se puede observar:

    $$|-\rangle = \frac{1}{\sqrt{2}} \left( |0\rangle - |1\rangle \right).$$

2.  **Aplicar puertas de Hadamard a las entradas**

    Nos aprovechamos de la superposición mediante puertas Hadamard $H^{\otimes n}$, generando todos los posibles valores de $x \in \{0,1\}^n$.

3.  **Aplicar el oráculo:**

    Al igual que el algoritmo anterior, la definición más común de oráculo es la siguiente:

    $$U_f |x\rangle |y\rangle = |x\rangle |y \oplus f(x)\rangle.$$

4.  **Aplicar puertas de Hadamard nuevamente:**

    Para finalizar, volvemos a aplicar las puertas Hadamard otra vez; a diferencia de la anterior, también se las aplicamos al qubit auxiliar.

5.  **Medición:**

    Finalmente, se mide el registro de entrada. El resultado será exactamente la cadena oculta $s$.

El circuito queda de la siguiente forma:

![[circuito de Benstein Vazirani.png]]
*Circuito de Bernstein-Vazirani*

##### Diseño del algoritmo

Lo primero que tenemos que saber es cómo se codifica dicho oráculo. Este oráculo se construye solo con puertas controladas $X$ o CNOT, siendo que, si averiguamos uno en el *qubit* auxiliar, se activa. Cada elemento del vector $s$ que sea 1 lo codificamos con CNOT, y los ceros los ponemos con puerta de identidad, para provocar un retraso.

![[oraculo Benstein-Vazirani.png]]
*Oráculo de Bernstein-Vazirani*

En este caso, el vector $s$ corresponde al valor 110.

El truco en este algoritmo es que, al poner cuatro puertas Hadamard rodeando una puerta CNOT, esta se invierte:

Ya que $(H \otimes H) \cdot \text{CNOT} \cdot (H \otimes H) = \text{CNOT reverso}$.

Esto sucede porque la puerta Hadamard cambia la base computacional de $\{|0\rangle, |1\rangle\}$ a la base diagonal $\{|+\rangle, |-\rangle\}$, que está realizada con las puertas $X$ y $Z$, dando la siguiente relación. Por eso, en algunos diagramas se pone directamente la puerta $Z$:

$$H \cdot X \cdot H = Z$$

$$H \cdot Z \cdot H = X$$

Lo que hace es que, cuando lo rodeas, cambia el sentido, invirtiendo la dirección.

El truco para poder resolverlo es rodearlo con Hadamards:

![[circuito de Benstein Vazirani. oraculo rodeado de hadamarts png.png]]
*Circuito de Benstein Vazirani, oráculo rodeado de Hadamard*

En los bits que sean cero, las Hadamards se anulan.

![[circuito de Benstein Vazirani. oraculo rodeado de hadamarts Anuladas.png]]
*Circuito de Benstein Vazirani, oráculo rodeado de Hadamard anuladas*

Aplicamos dos puertas H en qubit auxiliar, que al ser reversibles no afectan al qubit auxiliar, pero sí que consiguen invertir el CNOT.

![[circuitoHadarmardsAnuladas.png]]
*circuito de Benstein Vazirani. oráculo rodeado de hadamarts anuladas 2*

Y sabiendo la propiedad antes dicha, todo sería equivalente a quitar las Hadamards e invertir los CNOT. Así, al activar el último *qubit*, se van a activar los *qubits* que tengan un 1 en su cadena $s$.

![[circuito de Benstein Vazirani. solucionpng.png]]
*Circuito de Benstein Vazirani. Solución*

#### Grover

##### Planteamiento

Es el algoritmo más rápido para buscar un elemento en un conjunto desordenado de $N$ elementos. Dicha búsqueda se realiza en un tiempo cuadrático, es decir, $O(\sqrt{N})$, en lugar de un tiempo $O(N)$. Este algoritmo es muy útil y tiene muchas aplicaciones, entre ellas, en el ámbito de la ciberseguridad, donde sería útil para buscar dentro de un conjunto desordenado cuál es la clave correcta de un cifrado, pudiendo reducir cualquier ataque de fuerza bruta a un algoritmo criptográfico como es el AES-256 a un tiempo cuadrático.

Por poner un ejemplo, tenemos una caja negra que puede responder si la entrada es correcta o no (oráculo). El objetivo es encontrar esa entrada.(Long 2001)

##### Resolución Clásica

La resolución clásica consiste en crear un circuito en el cual, si el bit correspondiente es un 1, no se hace nada, y si es un 0, se introduce una puerta NOT. Las salidas están conectadas a una puerta AND. En el caso de que se introduzcan todos unos, da como resultado 1, lo que indica que hemos obtenido la combinación correcta. Dicho circuito sería nuestro oráculo. El objetivo sería probar todas las combinaciones hasta que la salida dé como resultado una cadena de todos 1s, que se conecta a una puerta AND, y este AND devuelve, por lo tanto, 1, significando que hemos encontrado la entrada deseada por el oráculo.

![[circuitoClasico.png]]
*Circuito clásico del oráculo de búsqueda de combinación correcta de bits*

##### Resolución Cuántica

Para la resolución cuántica, primero empleamos puertas Hadamard en todos los *qubits* con el objetivo de crear un estado de superposición, de modo que se genere un estado superpuesto de todas las combinaciones posibles, entre las cuales se encuentra la combinación correcta. El siguiente elemento en nuestro circuito es el oráculo, que está construido con puertas $X$ y puertas de CTRLNOT.

Se produce un fenómeno curioso en el oráculo: la respuesta correcta le introduce un retraso de faseo *phase kickback*, induciendo un cambio de signo de amplitud. Esto se debe a las puertas CTRL, que, como hemos visto anteriormente, generan un retroceso de fase en la combinación que las activa.

![[Oraculo Grover.png]]
*Oráculo de Grover*

En el siguiente paso aplicamos la difusión, también llamada el operador de difusión de Grover, que refleja todas las amplitudes respecto a la media. En este proceso, el valor buscado se va a volver a reflejar sobre su media y con más amplitud, mientras que el resto de los valores, al hacer la media con el valor reflejado, pierden significancia.

El diseño del difusor de Grover es el siguiente: en las entradas se introduce una puerta $H$, seguida de puertas $X$, para luego continuar con un CTRL $Z$. Para finalizar, se deshacen los estados introducidos por las puertas $X$ y las puertas $H$. Al ser puertas reversibles, con volver a introducirlas, pero en orden inverso, es suficiente.

Este proceso a continuación lo explico con más detalle:

1.  **Hadamard (H) en cada qubit:** Convertimos el estado actual de la base computacional a la base de Fourier.

2.  **Puertas NOT (X) en cada qubit:** Invertimos los *qubits* con el objetivo de que la siguiente puerta solo interactúe sobre los estados $|0\rangle$.

3.  **Control-Z global:** Esta puerta va a invertir la fase del estado que tiene todo ceros y no afecta a los demás. El estado que estamos buscando es el que actualmente tiene todo ceros debido a las puertas $X$ y el oráculo.

4.  **Deshacer NOT (X):** Aplicamos puertas $X$ para regresar al estado anterior.

5.  **Deshacer las Hadamard:** Volvemos a aplicar puertas Hadamard para volver a la base original.

![[Difusor de Grover.png]]
*Difusor de Grover*

El lector puede preguntarse por qué necesitamos un operador de difusión como el operador de Grover si en los algoritmos anteriores, como Deutsch-Jozsa y Bernstein-Vazirani, no los necesitamos. La respuesta está en la fase. Esto es debido a que estos algoritmos tienen una estructura global, es decir, a partir de una entrada se podía deducir información de otras. En cambio, con Grover queremos buscar una única entrada que dé la respuesta correcta; el resto de las entradas no nos da información, es a grosso modo "buscar una aguja en un pajar".

En los otros algoritmos, al tener una estructura global y regular, genera una interferencia directa dando la respuesta válida, mientras que con Grover tenemos que recrear dicha interferencia con el difusor. Esta interferencia genera estados constructivos que favorecen la probabilidad de los estados más probables y estados destructivos que reducen la probabilidad de los estados menos probables.

Al medirlo, el estado más probable será el estado buscado debido al operador de Grover, que realiza una reflexión sobre la media.

Este proceso de oráculo más difusor de Grover se tiene que repetir $\left(\frac{\pi}{4}\right) \cdot \sqrt{N}$ veces, debido a que el resultado que genera es probabilístico.

Este algoritmo se puede utilizar, dado un mensaje cifrado por un algoritmo de cifrado simétrico como es el AES, para encontrar una clave que descifre dicho mensaje. El lector podría pensar, leyendo la explicación anterior, que para encontrar un valor en una base de datos de longitud $x$ necesitamos $x + 1$, siendo el $+1$ el qubit extra para marcar la solución (el flag de Grover), siendo en el AES-256 solamente necesarios $256 + 1$ qubits. Pero la realidad es otra: se produce una gran sobrecarga, siendo necesarios $66\,681$ qubits lógicos. Esto se debe a dos problemas principales:

1.  El oráculo de Grover tiene que simular el AES dentro. Todo el algoritmo de AES debe implementarse como un circuito cuántico reversible. Cada operación clásica irreversible que pierde información tiene que transformarse en un conjunto de puertas que necesitan qubits adicionales para que pueda ser reversible (ancillas).

2.  El AES tiene operaciones no lineales, como la *S-box*, lo que hace que la implementación requiera muchas más puertas Toffoli y lógica adicional. Cada ronda del AES guarda un bloque de ancillas (qubits auxiliares que no forman parte de los estados) para hacer las operaciones reversibles y mantener dicho oráculo reversible.

Estos dos problemas conllevan que su implementación sea de naturaleza no trivial.

#### Shor

##### Planteamiento

Este algoritmo es uno de los más importantes dentro de la computación cuántica debido a que dejó de verse la computación cuántica como algo de nicho. Su importancia radica en que puede romper la seguridad de sistemas criptográficos asimétricos basados en RSA y en curvas elípticas. Estos sistemas tienen su dificultad en descomponer un número en los dos primos que lo componen. La mejor solución clásica tarda un tiempo subexponencial en factorizar $N$, mientras que el algoritmo de Shor lo hace en un tiempo polinómico $O((\log N)^3)$.

La idea principal es reducir el problema de la factorización a la búsqueda del **período** $r$ de una función $f(x) = a^x \bmod N$, siendo $a$ un coprimo de $N$. Si se conoce este período, se puede obtener un factor no trivial usando el MCD (máximo común divisor).(Monz et al. 2016)

##### Resolución Clásica

En la computación clásica no existe ningún algoritmo eficiente que resuelva el problema de encontrar el período de una función $f(x) = a^x \bmod N$. Los algoritmos clásicos para obtener la factorización de $N$ son el de Fermat, el de rho de Pollard o el método general del crivillo, pero todos ellos son mucho menos eficientes que el algoritmo de Shor. Algunos de estos son el de Fermat, el de rho de Pollard y el método general del crivillo, entre otros.

##### Resolución Cuántica

El objetivo es encontrar la raíz no trivial, es decir, $X^2 = 1 \mod(N)$, porque sabiendo que $N = p \cdot q$, se tiene que $X^2 - 1 = 0 \mod(N)$, lo que implica que $N = (X^2 + 1) \cdot (X^2 - 1)$. Por lo tanto, $(X^2 + 1)$ contiene $p$ y $(X^2 - 1)$ contiene $q$. Si hacemos el `gcd` de $N$ con $(X^2 + 1)$, obtenemos $p$, y con el `gcd` de $(X^2 - 1)$ obtenemos $q$.

Como podemos observar, el objetivo es encontrar ese $X$ que al elevarlo nos da 1 $\mod(N)$. Pero esto es igual que, dado un número, encontrar su período. El período es encontrar en un anillo el número que, al elevar dicha función (el orden), al ser periódica, da comienzo a otro período de la misma. Este orden tiene que ser 2 para cumplir nuestro objetivo. Podría parecer muy complicado, pero basta con que el exponente sea par porque $(a^3)^2 = X^2$, donde $X = a^3$. Encontrar un número con un exponente par dentro de nuestro conjunto tiene más del 50% de probabilidad. Por lo tanto, si conseguimos encontrar un período par para un número $a$, podremos encontrar $p$ y $q$.

El algoritmo de Shor se divide en dos partes. La primera parte es la estimación de fase cuántica (QPE), con la cual conseguimos obtener, mediante mediciones parciales, el período más $k$, pero $k$ no nos interesa. Para poder deshacernos de él, utilizamos la transformada cuántica de Fourier. El proceso puede resumirse de la siguiente manera:

1.  Se elige un valor $a$ tal que $\gcd(a, N) = 1$.

2.  Se construye un operador cuántico $U$ tal que $U |x\rangle = |a \cdot x \bmod N\rangle$, esto es lo mismo que, dado un número, nos lo va a devolver multiplicado por el período más algo.

3.  Se prepara un estado superpuesto que contenga información de todos los posibles valores de $x$.

4.  Se aplica la QPE al operador $U$. Al medir el operador $U$, se forza $x$ a estar en un estado de superposición con los elementos que conforman su período, por ejemplo, $| \frac{1}{\sqrt{3}} \rangle (|1\rangle + |3\rangle + |5\rangle)$. Cada uno de los posibles estados corresponde a una representación del siguiente modo del período $|x + k \cdot r\rangle$.

5.  Se aplica la QFT, la transformada cuántica de Fourier. Transformas los vectores a un único plano, que es el plano $X$. Gracias a esta operación se obtiene la siguiente aproximación $\psi_s = \frac{s}{r}$. La QFT es la siguiente operación:

    $$|u_s\rangle = \frac{1}{\sqrt{r}} \sum_{k=0}^{r-1} e^{-2\pi i k s / r} |y \rangle$$

6.  Se aplican varias mediciones y se hace el `gcd` de los distintos $(s/r)$ para así obtener $r$, que es el período.

7.  Ya con el período, si es un período par, obtenemos $p$ y $q$.

La QFT nos devuelve s/r porque, al igual que la transformada clásica que convierte una secuencia de valores, por ejemplo, de una señal, nos devuelve las frecuencias que componen dicha señal. En la transformada cuántica de Fourier, nos devuelve el periodo en forma de frecuencia, porque dicha función es periódica.

![[shor-algorithm.png]]
*Algoritmo de Shor*

#### VQE Variational Quantum Eigensolver

##### Planteamiento

Uno de los algoritmos que trata de resolver el problema de la energía del estado fundamental de forma más eficiente es el VQE (Variational Quantum Eigensolver). Este problema consiste en encontrar la energía más baja posible dentro de un sistema físico en el contexto de la mecánica cuántica y la química cuántica. El *ground state* es el estado más estable y de menor energía de un sistema cuántico. Es interesante saber determinar la energía de un estado porque es clave para saber si dicho sistema es estable. Los sistemas, cuanto menor es la energía que tienen, más estables son y más difícil es que reaccionen con otros elementos. Por ejemplo, los gases nobles, al tener su última capa llena de electrones, son sistemas inertes que no interactúan debido a su baja energía. Esta energía se mide en electronvoltios. Un electronvoltio es la energía que gana un electrón al pasar por un campo eléctrico con un voltio de potencial.

Para poder ejemplificar mejor esto, el hidrógeno tiene -13.6 eV, lo que significa que para perder su electrón necesita una energía de 13.6 electronvoltios. Esta energía la puede recibir en forma de fotón, que es la partícula del campo electromagnético.

Hallar el *ground state* es importante porque se puede predecir cómo reaccionan ciertos elementos con otros. Utilizando la ecuación de Schrödinger, se puede hallar una solución para sistemas simples como un electrón, para el hidrógeno, pero para moléculas más complejas se convierte en un problema verdaderamente complicado, siendo en algunos casos de tipo NP. Resumiendo, significa entender la forma más estable y básica de un sistema.(Tilly et al. 2022)

![[groundstate.png]]
*ground state vs excited state*

##### Resolución Clásica

La forma clásica trata de encontrar el valor mínimo de $E_0$ tal que:

$$\hat{H} | \psi_0 \rangle = E_0 | \psi_0 \rangle$$

1.  $\hat{H}$: el Hamiltoniano del sistema (representa la energía total: cinética + potencial).

2.  $| \psi_0 \rangle$: el estado fundamental (función de onda de menor energía).

3.  $E_0$: la energía del estado fundamental.

Los métodos clásicos que utilizan computadoras normales son el método variacional, Hartree-Fock, DFT y el más exacto, el de la diagonalización directa del Hamiltoniano, aunque su costo es exponencial. El más utilizado es el DFT, ya que ofrece una buena precisión y su coste computacional es bastante razonable.

El método variacional se basa en la idea simple de que cualquier función de onda normalizada tiene una energía esperada mayor o igual que la energía del estado fundamental, es decir, $E_0$:

$$E[\psi] = \frac{\langle \psi | \hat{H} | \psi \rangle}{\langle \psi | \psi \rangle} \geq E_0$$

Si podemos variar $\psi$ para minimizar esa energía, nos aproximamos a $E_0$.

Los pasos que debes seguir:

1\. Necesitas el Hamiltoniano que describe toda la energía cinética y potencial del sistema. Por ejemplo, para un átomo de hidrógeno:

$$\hat{H} = - \frac{\hbar^2}{2m} \nabla^2 - \frac{4\pi \epsilon_0 e^2}{r}$$

2\. Tienes que elegir una función de onda tentativa (*ansatz*), por ejemplo, para el hidrógeno:

$$\psi(r) = A e^{-\alpha r}$$

donde $\alpha$ es el parámetro variacional (positivo) y $A$ es una constante de normalización.

Tenemos que hallar el parámetro variacional. Para ello, la energía esperada es:

$$E[\alpha] = \frac{\int \psi^*(r) \hat{H} \psi(r) \, d^3r}{\int \psi^*(r) \psi(r) \, d^3r}$$

Luego, para hallar la solución, minimizamos esta energía utilizando la derivada respecto al parámetro variacional e igualándola a cero:

$$\frac{dE}{d\alpha} = 0$$

La interpretación de $E[\alpha]$ es una cota superior.

Como se puede observar, tiene la limitación de que escoger un buen *ansatz* es clave y puede ser difícil, ya que depende de la simetría del sistema. En este caso, como el hidrógeno tiene simetría esférica y su energía decae en el infinito, se utiliza una exponencial negativa.

##### Resolución Cuántica

El método variacional clásico y el VQE (Variational Quantum Eigensolver) se basan en el mismo principio físico: encontrar una cota superior con el objetivo de poder minimizar dicha función con parámetros variacionales para encontrar $E_0$. Este algoritmo es una combinación híbrida de computación clásica con computación cuántica. Los pasos que sigue son los siguientes:

1.  Escoge un *ansatz* cuántico: una familia de circuitos cuánticos $U(\vec{\theta})$ que preparan estados $|\psi(\vec{\theta})\rangle$.

2.  En el ordenador cuántico, ejecuta el circuito y mide la energía esperada $\langle \hat{H} \rangle$.

3.  Una CPU clásica ajusta los parámetros $\vec{\theta}$ para minimizar la energía.

4.  Se repite hasta que se aproxima a $E_0$.

La principal ventaja que tiene sobre su homólogo clásico radica en el problema de por qué resolver el problema de energía base. En los átomos grandes, como puede ser el plomo, que tiene 82 electrones, los electrones de la capa superior están en un estado de entrelazamiento, lo que implica que no se puede describir su estado sin tener en cuenta al resto. Esto hace que el resultado no sea solo el resultado de 82 funciones de onda; la función de onda va a ser muy difícil de describir. El VQE tiene la ventaja de que puede usar qubits entrelazados de forma natural y permite describir funciones de onda más complejas.

#### VQC Variational Quantum Circuits

##### Planteamiento

Después de hablar del VQE (Variational Quantum Eigensolver), el VQC (Variational Quantum Classifier) es otro algoritmo híbrido cuántico, pero aplicado al *M*achine Learning\*. Se centra en problemas de optimización, clasificación o simulación cuántica utilizando tanto recursos cuánticos como clásicos. A diferencia del VQE, se centra en, mediante la utilización de parámetros variacionales, encontrar un modelo que separe correctamente los datos de distintas clases.(Chen et al. 2020)

##### Resolución Clásica

Cualquier modelo de clasificación, como pueden ser redes neuronales, random forests, K-NN, Naive Bayes, SVM, y regresión logística, es aplicable en este contexto. La ventaja que tiene el VQC es que, al utilizar el espacio de Hilbert para clasificar, este tiene una dimensionalidad exponencial con respecto al número de qubits, lo que permite representar funciones altamente no lineales, lo que confiere una ventaja sobre clasificadores clásicos como los mencionados anteriormente.

##### Resolución Cuántica

1.  Como en cualquier modelo, es el preprocesamiento de los datos $n$.

2.  Se transforma el vector de entrada clásico en un estado cuántico. Esto se hace mediante rotaciones, utilizando por ejemplo $R_Y$ o $R_X$.

3.  Se construye el circuito variacional (*ansatz*). Este circuito representa el modelo y depende de los parámetros libres. Se ejecuta y se miden los parámetros, comparándolos con la precisión. Dependiendo de esto, utilizando algoritmos clásicos de optimización como COBYLA, SPSA, o gradient descent, se ajustan los parámetros $\vec{\theta}$ con el objetivo de minimizar la función de pérdida.

4.  Repetir este procedimiento hasta que haya convergencia.

![[VQC.png]]
*Variational Quantum Circuits VQC*

### Límite de los simuladores cuánticos

En computación cuántica, simular un sistema de $n$ qubits de forma general implica representar el *vector de estado* con $2^n$ amplitudes complejas, lo que conlleva un coste de memoria y tiempo que crece exponencialmente con $n$. Por ejemplo:

- 1 qubit $\rightarrow 2^1 = 2$ amplitudes.

- 10 qubits $\rightarrow 2^{10} = 1024$ amplitudes.

- 50 qubits $\rightarrow 2^{50}$ amplitudes, lo que resulta inabordable para un PC, superando los $128$ terabytes de memoria.

Nos referimos a amplitudes porque en computación cuántica no se representa el dato de un sistema con bits clásicos, sino con amplitudes que describen la probabilidad de que un sistema esté en un estado cuántico. Normalmente, las amplitudes se representan en los simuladores con dos números de coma flotante, uno para la parte real y otro para la parte imaginaria, siendo ambos de tipo *double*, ocupando 64 bits cada uno. Ocupando en total cada amplitud 16 bytes.

El **teorema de Gottesman-Knill** (Wikipedia contributors 2024) indica que, si solo utilizamos **puertas Clifford** (Hadamard $H$, rotación de fase $S$, CNOT y las puertas de Pauli $X$, $Y$, $Z$), dicho circuito puede simularse de forma eficiente en un ordenador clásico mediante el *formalismo de estabilizadores*.

#### Formalismo de estabilizadores

En lugar de representar el estado cuántico como un vector de dimensión $2^n$, se puede describir como un conjunto de operadores que “estabilizan” el estado. Las puertas Clifford preservan esta estructura, lo que aporta las siguientes ventajas (Salcedo, n.d.):

- Representar el estado con memoria que crece como $O(n^2)$ en vez de $O(2^n)$.

- Requerir pocas operaciones para actualizar su estado.

Si solo se utilizan puertas Clifford, es posible simular miles de qubits sin problema. Sin embargo, si alguna puerta del circuito no es Clifford (por ejemplo, la puerta $T$ o una rotación $\pi/8$), la estructura de estabilizadores se rompe y el coste de simulación vuelve a crecer de forma exponencial con $n$. Esto sucede porque:

- Puertas Clifford $\Rightarrow$ mantienen el grupo de estabilizadores.

- Puertas no Clifford $\Rightarrow$ generan estados que no pueden describirse únicamente con estabilizadores.

En términos de complejidad computacional:

- Circuitos cuánticos generales $\Rightarrow$ clase **BQP** (difíciles de simular clásicamente) (Wikipedia 2024b).

- Circuitos Clifford $\Rightarrow$ pertenecen a **P** (simulación clásica eficiente).

El teorema de Gottesman-Knill explica por qué un simulador clásico puede manejar circuitos Clifford con miles de qubits, pero no circuitos generales, cuya simulación se vuelve intratable a partir de aproximadamente $30$–$40$ qubits.

### Principales tecnologías de implementación de qubits

Es interesante saber cuáles son las principales tecnologías de implementación de qubits en computación cuántica con sus ventajas y desventajas.

- **Superconductores (IBM, Google, Rigetti, OQC, IQM)**. Representan la tecnología más madura y fácil de fabricación, con compuertas rápidas en el orden de nanosegundos. Pero presentan el problema de tener una decoherencia muy rápida y la necesidad de estar a una temperatura cercana al cero absoluto.(Alfaraz Delgado 2019) Actualmente es la tecnología que más qubits físicos presenta, como el IBM Condor. (Castelvecchi 2023)

- **Iones atrapados (IonQ, Quantinuum)**. Son átomos cargados en trampas electromagnéticas manipulados con un láser. Presentan una buena integridad de los datos, son sistemas que tardan en caer en la decoherencia. Pero presenta a cambio el problema de que las operaciones en estos circuitos son muy lentas, en el orden de los milisegundos, y son sistemas difíciles de escalar. Son ideales cuando se requiere demostrar algoritmos cuánticos con unos pocos qubits (Brown et al. 2021).

- **Átomos neutros (QuEra, Pasqal)**. A diferencia de los iones atrapados, no tienen carga y para atraparlos se utilizan láseres muy enfocados que generan un campo eléctrico tan intenso que inducen en ellos un dipolo inducido (Garcı́a and Garcı́a, n.d.). Son la gran apuesta a medio plazo, presentan buena escalabilidad, se puede tener miles de átomos en redes ópticas que se manipulan mediante estados de Rydberg. No presentan una integridad tan alta como los iones atrapados y también presentan tiempos lentos en las operaciones cuánticas (Viveros, n.d.).

- **Fotones (Xanadu)**. Los fotones se pueden utilizar para codificar qubits utilizando sus grados de libertad, como son la polaridad (horizontal y vertical), la trayectoria (estar en el camino óptico 0 o en otro 1) y el número de fotones. Tienen la ventaja de que presentan una baja decoherencia, son sistemas muy estables, ya que los fotones, al no tener masa y no interactuar entre ellos, tienen una gran escalabilidad y pueden estar a temperatura ambiente, a diferencia de los otros. Pero tienen el inconveniente de que son muy difíciles de implementar puertas lógicas. Se utilizan más en comunicación cuántica que en computación (Pérez Romero 2025).

- **Recocido cuántico (annealing) (D-Wave)**. Tienen miles de qubits más que en cualquier otro y son sistemas óptimos para resolver problemas de optimización QUBO. La desventaja es que solo resuelve problemas de este tipo porque no es un computador cuántico universal. Se encuentra en la situación de que para aplicaciones reales a corto plazo son la tecnología más prometedora, pero con el inconveniente de que solo sirve para problemas de optimización (Osaba et al. 2025).

La conclusión: la tecnología con más madurez y escala (IBM y Google). Los iones atrapados son los más fiables y, en cuanto a escalabilidad, lo mejor son átomos neutros. Para comunicaciones, los fotones, y en cuanto a problemas de optimización, lo mejor son D-Wave.

## Desarrollo

> Si no puedes explicarlo de manera sencilla, no lo entiendes lo suficientemente bien
>
> — Richard Feynman \### Introducción {#sec:introduccion-desarrollo}

Esta sección está dedicada a la exploración de las bases tecnológicas que sustentan el desarrollo y la implementación de los algoritmos cuánticos. Para nuestra prueba utilizaremos los siguientes: Deutsch-Jozsa, Bernstein-Vazirani y el algoritmo de Grover. La finalidad de dicha sección es explorar los distintos entornos y ejecutar los distintos algoritmos con el fin de poder comparar sus diferencias.

Los simuladores juegan un papel fundamental, como hemos dicho anteriormente, debido al estado actual de la computación cuántica, para la creación de nuevos algoritmos y para su desarrollo e implementación.(Quantiki 2025)

### Desarrollo del sistema de comparación

Para comparar los diferentes sistemas, se ejecutarán en ellos los algoritmos de Grover, Deutsch y Bernstein. Estos algoritmos serán ejecutados en los diferentes simuladores y se recogerán las siguientes métricas:

- **Tiempo de ejecución (performance):** Se hará con los diferentes algoritmos por cada simulador y haciendo una media entre todos. Para ello, se puede utilizar el siguiente fragmento de código:

  ```

          import time

          start_time = time.time()

          # Aquí va la ejecución de tu circuito cuántico

          end_time = time.time()

          print(f"Tiempo de ejecución: {end_time - start_time:.4f} segundos")
  ```

- **Uso de la memoria:** Puede medirse con la biblioteca `psutil` o `memory_profiler` en Python. Dicha métrica tomará el mismo enfoque que la anterior, comparando los diferentes algoritmos propuestos en los diferentes simuladores.

- **Escalabilidad:** Se compara cómo se comportan los diferentes simuladores al aumentar el número de qubits. Un ejemplo en Qiskit puede ser el siguiente:

  ```

  from qiskit import QuantumCircuit, Aer
  import time

  def measure_scalability(num_qubits):

      qc = QuantumCircuit(num_qubits)

  # Aplicar compuertas CX en cadena
  for i in range(num_qubits - 1):
      qc.cx(i, i + 1)

  # Medir todos los qubits
      qc.measure_all()

  # Ejecutar en el simulador
      simulator = Aer.get_backend('aer_simulator')

      start_time = time.time()
      simulator.run(qc).result()
      end_time = time.time()

      return end_time - start_time

  # Probar con diferentes tamaños de circuito
  for n in range(5, 21, 5):
      time_taken = measure_scalability(n)
      print(f"Tiempo para {n} qubits: {time_taken:.4f} segundos")
  ```

### QuEST

Fue desarrollado en 2018 por investigadores de la Universidad de Oxford con el objetivo de crear una herramienta robusta y escalable para la simulación de circuitos cuánticos.

Tiene de ventaja que la codificación se hace directamente en C, mejorando el rendimiento. También dispone de una gran precisión a la hora de obtener los resultados y soporta una amplia gama de puertas lógicas cuánticas. Además, destaca por su capacidad de poder paralelizar las simulaciones, pudiendo usar múltiples núcleos de CPU para distribuir las tareas. Además, soporta aceleración por GPU. Dispone de una API en C++ que facilita su integración con otros proyectos de simulación cuántica, permitiendo su integración con otros flujos.

Es el que tiene una mayor curva de aprendizaje debido a que está escrito en C y carece de documentación actualizada. La documentación disponible en el sitio oficial está desactualizada y los métodos actuales son totalmente distintos a los que se describen en la página web. Para poder ejecutar y comprender el simulador, es necesario realizar ingeniería inversa debido a la escasa información existente. Tampoco dispone de una interfaz gráfica (GUI) (QuEST Project 2025).

#### Código de los distintos algoritmos

Para la prueba hemos conseguido ejecutar el algoritmo de Bernstein Vazirani.

``` c
#include "quest.h"
#include <stdio.h>

void applyBernsteinVazirani(Qureg qureg, int numQubits, int secret);
void applyOracle(Qureg qureg, int numQubits, int secret);
void measureResult(Qureg qureg, int secret);
int main() {
    initQuESTEnv();
    int numQubits = 15;
    int secret = 5;
    Qureg qureg = createQureg(numQubits);
    applyBernsteinVazirani(qureg, numQubits, secret);
    destroyQureg(qureg);
    finalizeQuESTEnv();
    return 0;
}

void applyBernsteinVazirani(Qureg qureg, int numQubits, int secret) {
    initZeroState(qureg);
    applyPauliX(qureg, 0);
    for (int q=0; q<numQubits; q++) applyHadamard(qureg, q);
    applyOracle(qureg, numQubits, secret);
    for (int q=0; q<numQubits; q++) applyHadamard(qureg, q);
    measureResult(qureg, secret);
}
void applyOracle(Qureg qureg, int numQubits, int secret) {
    int bits = secret;
    for (int q=1; q<numQubits; q++) {
        int bit = bits % 2;
        bits /= 2;
        if (bit) applyControlledPauliX(qureg, q, 0);
    }
}
void measureResult(Qureg qureg, int secret) {
    int ind = 2*secret + 1;
    int prob = applyQubitMeasurement(qureg, ind);
    printf("success probability: %d \n", prob);
}
 
```

#### Obtención de métricas

##### Comprobación de los resultados

No ha sido una tarea fácil la ejecución del algoritmo, debido a que los métodos que se encuentran en la documentación oficial están desactualizados, como se ha comentado con anterioridad, y algunos apartados de la página web están caídos.

![[Quest_error.png]]
*404 fichero no encontrado: https://quest-kit.github.io/*

Hemos conseguido ejecutarlo cambiando los métodos desactualizados por otros cuyo nombre parecía similar en el código; aun así, no genera los resultados esperados.

![[Quest_resultadoBernsteinVazirani.png]]
*Resultado de bernstein Vazirani*

Actualmente, lamentablemente no se recomienda dicho simulador por la falta de documentación y la poca retrocompatibilidad de versiones.

### Qiskit Aer

Es desarrollado por IBM con el fin de simular circuitos cuánticos en entorno clásico y ejecutar algoritmos cuánticos en hardware real, ya que IBM es de las empresas que más dinero está invirtiendo en la creación de ordenadores cuánticos. Aer es el módulo encargado de simular circuitos cuánticos en hardware clásico antes de ejecutarlos en cuántico real y el núcleo es Qiskit Terra, que permite crear, optimizar y compilar circuitos cuánticos para ejecutarlos en distintos simuladores. Aer proviene del latín, que significa aire, y fue elegido de manera simbólica: "Simular el entorno en el que funcionan los sistemas cuánticos, incluyendo el ruido, la decoherencia y otros fenómenos que ‘flotan en el aire’ alrededor del sistema cuántico ideal".(IBM 2025)

Tiene la ventaja de que se codifica en Python con librerías de C; es la misma dinámica que se emplea en el desarrollo de inteligencia artificial: emplear un lenguaje con una curva de aprendizaje no muy elevada y dotarlo de librerías y módulos escritos en C con el objetivo de transferir la carga más pesada a un lenguaje compilado para mejorar la eficiencia. Otra ventaja es que consigue añadir efectos de ruido y errores en la simulación mediante errores de *bit flip* o *phase flip*, lo que permite ver su comportamiento en un circuito real ante el ruido.

Tiene un gran desempeño porque cuenta con soporte eficiente en Linux vía `qiskit-aer-gpu`, que permite usar CUDA 11 para ejecutar en GPU.

Las desventajas que presenta son que depende del hardware disponible de forma local y que, a pesar de presentar un lenguaje con una curva no muy pronunciada, sigue siendo difícil debido a que las simulaciones con ruido y decoherencia requieren un conocimiento profundo de la herramienta.

#### Código de los distintos algoritmos

A continuación, se muestra la codificación de los diferentes algoritmos propuestos para el entorno de Qiskit:

``` python
import numpy as np
from qiskit import *
from qiskit_aer import *
from qiskit.visualization import *
import altair as alt
import pandas as pd

n = 3
oraculo_balanceado = QuantumCircuit(n + 1)
string_binario = "101"
for qubit in range(len(string_binario)):
    if string_binario[qubit] == '1':
        oraculo_balanceado.x(qubit)
oraculo_balanceado.barrier()
for qubit in range(n):
    oraculo_balanceado.cx(qubit, n)
oraculo_balanceado.barrier()
for qubit in range(len(string_binario)):
    if string_binario[qubit] == '1':
        oraculo_balanceado.x(qubit)
circuito = QuantumCircuit(n + 1, n)
for qubit in range(n):
    circuito.h(qubit)
circuito.x(n)
circuito.h(n)
circuito = circuito.compose(oraculo_balanceado)
for qubit in range(n):
    circuito.h(qubit)
circuito.barrier()
for i in range(n):
    circuito.measure(i, i)
aer_sim = Aer.get_backend('aer_simulator')
resultados = aer_sim.run(circuito).result()
respuesta = resultados.get_counts()
assert respuesta.get('000', 0) == 0
df = pd.DataFrame(list(respuesta.items()), columns=['Resultado', 'Conteo'])
chart = alt.Chart(df).mark_bar().encode(
    x='Resultado:O',
    y='Conteo:Q'
).properties(title='Histograma de Resultados')
chart.display()
```

``` python
import numpy as np
from qiskit import *
from qiskit_aer import *
from qiskit.visualization import *
import altair as alt
import pandas as pd

n = 3
s = '011'
circuito = QuantumCircuit(n + 1, n)
circuito.h(n)
circuito.z(n)
for i in range(n):
    circuito.h(i)
circuito.barrier()
s = s[::-1]
for q in range(n):
    if s[q] == '0':
        circuito.id(q)
    else:
        circuito.cx(q, n)
circuito.barrier()
for i in range(n):
    circuito.h(i)
for i in range(n):
    circuito.measure(i, i)
aer_sim = Aer.get_backend('aer_simulator')
resultados = aer_sim.run(circuito).result()
respuesta = resultados.get_counts()
df = pd.DataFrame(list(respuesta.items()), columns=['Resultado', 'Conteo'])
chart = alt.Chart(df).mark_bar().encode(x='Resultado:O', y='Conteo:Q').properties(title='Histograma de Resultados')
chart.display()
```

``` python
import numpy as np
from qiskit import *
from qiskit_aer import *
from qiskit.visualization import *
from qiskit.circuit.library import MCXGate
import altair as alt
import pandas as pd

n = 3
grover = QuantumCircuit(3)
for qubit in range(n):
    grover.h(qubit)
grover.cz(0, 2)
grover.cz(1, 2)
for qubit in range(n):
    grover.h(qubit)
for qubit in range(n):
    grover.x(qubit)
grover.h(n - 1)
puertamultix = MCXGate(n - 1)
grover.append(puertamultix, list(range(n)))
grover.h(n - 1)
for qubit in range(n):
    grover.x(qubit)
for qubit in range(n):
    grover.h(qubit)
grover.measure_all()
grover.draw()
aer_sim = Aer.get_backend('aer_simulator')
resultados = aer_sim.run(grover).result()
respuesta = resultados.get_counts()
df = pd.DataFrame(list(respuesta.items()), columns=['Resultado', 'Conteo'])
chart = alt.Chart(df).mark_bar().encode(
    x='Resultado:O',
    y='Conteo:Q'
).properties(title='Histograma de Resultados')
chart.display()
```

#### Obtención de métricas

Para ello hemos utilizado el cuaderno de Jupyter para realizar las siguientes comprobaciones.

##### Comprobación de los resultados

En el algoritmo de Deutsch-Jozsa buscamos si la función es balanceada. En nuestro caso es una función balanceada porque hemos sido nosotros quienes hemos construido el oráculo con puertas CNOT, por lo que la salida depende de la entrada.

![[qiskit_Deutshc.png]]
*Código de Deutsch*

Al hacer la medición, nos sale 111 con una probabilidad del 100%, por lo tanto, la probabilidad de que salga 000 es cero, lo que indica que es una función balanceada. Si la función fuera constante, la medición solo daría el estado 000 con probabilidad 1. Esto se debe a que, si fuera constante, $f(x) = 0$ $\forall x$ o $f(x) = 1$ $\forall x$, todas las fases se reforzarían de forma constructiva en el estado 000 y destructiva en todos los demás, al aplicarle Hadamard a la salida del oráculo.

![[qiskit_Deutshc_resultado.png]]
*Deutsch resultado*

Qiskit nos da la opción de poder dibujar el circuito que hemos hecho:

![[qiskit_Deutshc_circuito.png]]
*Deutsch circuito generado por Qiskit*

En el algoritmo Bernstein-Vazirani, hemos escogido como cadena secreta el 011, que multiplica a nuestra entrada y luego hace módulo 2.

![[qiskit_BernsteinVarizani_codigo.png]]
*Bernstein-Vazirani código*

Al ejecutar dicho algoritmo podemos comprobar que sale el resultado esperado:

![[qiskit_BernsteinVarizani_resultado.png]]
*Bernstein-Vazirani resultado*

El circuito quedaría de la siguiente manera:

![[qiskit_BernsteinVarizani_circuito.png]]
*Bernstein-Vazirani circuito generado por Qiskit*

Con el algoritmo de Grover intentamos buscar un elemento en un conjunto. Se puede parecer al de Bernstein-Vazirani, pero con la diferencia de que el resto de las salidas no aporta información sobre la salida deseada. Para ello, se utiliza el principio de superposición para probar todas las posibles entradas en el oráculo. Este cambiará la fase de la salida que estamos buscando. Cambiar la fase no cambia la salida, porque al medir la probabilidad, se mide el cuadrado de esta.

![[qiskit_grover.png]]
*Grover código*

Para poder obtener el elemento buscado, se maximiza la probabilidad de que colapse en los elementos que tengan una fase negativa mediante el difusor de Grover, que aplica una reflexión sobre la media. Al ejecutarlo, podemos comprobar que nos devuelve 101 y el elemento 110 con mayor probabilidad que el anterior. Esto es correcto porque, como se puede observar en el oráculo, hemos marcado como solución las cadenas 101 y 110.

![[qiskit_grover_resultados.png]]
*Grover resultado*

Como se puede observar, los resultados esperados son los correctos.

Y el circuito que nos genera es el siguiente:

![[qiskit_grover_circuito.png]]
*Grover circuito generado por Qiskit*

##### Tiempo de ejecución

A los algoritmos ya vistos anteriormente, incorporamos el siguiente fragmento de código para comprobar su tiempo de ejecución:

```
    
    import time
    start_time = time.time()
    # Aquí va la ejecución de tu circuito cuántico
    end_time = time.time()
    print(f"Tiempo de ejecución: {end_time - start_time:.4f} segundos")
    
```

Para el algoritmo de Deutsch insertamos el código para obtener la medición del tiempo, como se puede observar en la siguiente imagen.

![[qiskit_Deutshc_metricas.png]]
*Deutsch código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0364$ segundos.

Para el algoritmo de Bernstein-Vazirani:

![[qiskit_BernsteinVarizani_Metricas.png]]
*Bernstein-Vazirani código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0247$ segundos.

El algoritmo de Grover:

![[qiskit_grover_metricas.png]]
*Grover código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0182$ segundos.

##### Uso de la memoria

Se utiliza el siguiente fragmento de código para comprobar su uso de memoria:

```
    
    import psutil
    import time
    # Obtiene el proceso actual
    process = psutil.Process()
    # Memoria antes de la simulación (en bytes)
    memory_before = process.memory_info().rss
    # Algoritmo a ejecutar
    # Memoria después de la simulación (en bytes)
    memory_after = process.memory_info().rss
    # Convertir de bytes a MB
    memory_used = (memory_after - memory_before) / (1024 ** 2)  
    print(f"Uso de memoria: {memory_used:.2f} MB")
    
```

Para el algoritmo de Deutsch:

Obtenemos que la memoria usada es de:$2.42$ MB.

Para el algoritmo de Bernstein-Vazirani:

Obtenemos que la memoria usada es de:$2.33$ MB.

Y para el algoritmo de Grover:

Obtenemos que la memoria usada es de:$2.89$ MB.

##### Escalabilidad

Para la escalabilidad hemos utilizado el siguiente fragmento de código:

```
import time
import gc
import psutil
from qiskit import QuantumCircuit, transpile, Aer

simulator = Aer.get_backend('aer_simulator')
process = psutil.Process()

def build_chain_circuit(num_qubits: int) -> QuantumCircuit:
    qc = QuantumCircuit(num_qubits, num_qubits)
    for i in range(num_qubits - 1):
        qc.cx(i, i + 1)
        qc.measure(range(num_qubits), range(num_qubits))
    return qc

def measure_scalability(num_qubits):
    t0 = time.time()
    qc = build_chain_circuit(num_qubits)
    # Menos trabajo del transpilador = menos CPU
    tqc = transpile(qc, simulator, optimization_level=3)
    _ = simulator.run(tqc, shots=1).result()
    t1 = time.time()
    return t1 - t0

# Probar con diferentes tamaños de circuito
for n in range(1, 32):
    memory_before = process.memory_info().rss
    t = measure_scalability(n)
    # Memoria después de la simulación (en bytes)
    memory_after = process.memory_info().rss
    memory_used = (memory_after - memory_before) / (1024 ** 2)
    print(f"Tiempo para {n} qubits: {t:.4f} s")
    print(f"Uso de memoria para {n} qubits: {memory_used:.2f} MB")
    gc.collect()
    time.sleep(1)
```

Lo ejecutamos y el resultado que obtenemos es el siguiente para distintos números de qubits:

![[qiskit_escalabilidad.png]]
*Escalabilidad con un diferente número de qubits*

| **Qubits** | **Tiempo (s)** | **Memoria (MB)** |
|:----------:|:--------------:|:----------------:|
|     1      |     0.0601     |       5.05       |
|     2      |     0.0481     |       0.30       |
|     3      |     0.0503     |       0.05       |
|     4      |     0.0484     |       0.02       |
|     5      |     0.0482     |       0.11       |
|     6      |     0.0475     |       0.07       |
|     7      |     0.0479     |       0.00       |
|     8      |     0.0484     |       0.00       |
|     9      |     0.0508     |       0.00       |
|     10     |     0.0489     |       0.00       |
|     11     |     0.0526     |       0.00       |
|     12     |     0.0497     |       0.00       |
|     13     |     0.0485     |       0.14       |
|     14     |     0.0485     |       0.02       |
|     15     |     0.0486     |       0.01       |
|     16     |     0.0492     |       0.00       |
|     17     |     0.0495     |       0.00       |
|     18     |     0.0491     |       0.00       |
|     19     |     0.0491     |       0.00       |
|     20     |     0.0496     |       0.00       |
|     21     |     0.0497     |       0.04       |
|     22     |     0.0502     |       0.00       |
|     23     |     0.0490     |       0.00       |
|     24     |     0.0507     |       0.00       |
|     25     |     0.0508     |       0.00       |
|     26     |     0.0491     |       0.00       |
|     27     |     0.0495     |       0.00       |
|     28     |     0.0520     |       0.01       |
|     29     |     0.0487     |       0.00       |
|     30     |     0.0497     |       0.00       |

Tiempo y memoria consumida en función del número de qubits

Viendo los datos anteriores, podemos ver que el consumo de memoria es casi mínimo y escala muy bien. Para probar el escalado de dicho circuito, como se puede observar, hemos utilizado puertas CNOT.

En lugar de consumir memoria como simuladores como el de Cirq, aprovecha más la CPU y se paraliza en los diferentes núcleos para aprovechar mejor el uso de CPU.

![[qiskit_cpu uso.png]]
*consumo de CPU general*

La vista en los diferentes núcleos:

![[qiskit_cpunucleos.png]]
*Consumo CPU en diferentes núcleos*

Hemos observado que tiene un límite a la hora de escalar el número de qubits, que son 30 qbits.

![[qiskit_error, el máximo de qubits son 30.png]]
*Error, el máximo de qubits son 30*

#### IBM Quantum Experience

Es la plataforma de IBM, la cual permite a los usuarios acceder a computadoras cuánticas y simuladores a través de la nube. Utiliza el marco de desarrollo Qiskit, como hemos mencionado anteriormente, que está basado en Python e integra diferentes tecnologías como Aer, Terra, entre otras.

Tiene una interfaz bastante accesible en la que se encuentra el IBM Quantum Composer, una herramienta gráfica para diseñar circuitos cuánticos en la que se pueden arrastrar las puertas lógicas cuánticas. Permite crear circuitos sin tener que escribir código. Además, el IBM Quantum Lab está basado en Jupyter Notebook. También ofrece acceso gratuito a dispositivos cuánticos con una cantidad limitada de tiempo y ofrece planes premium para poder acceder a hardware más avanzado.

Primero, creamos una cuenta. Cuando la tengamos, nuestro panel será el siguiente, en el cual seleccionaremos el compositor para diseñar los diferentes algoritmos:

![[tutoriales-Deutsch-Jozsa_Compositor00.png]]
*Panel de usuario*

El panel del compositor se compone de un panel principal en el cual se desarrolla el algoritmo cuántico utilizando las diferentes puertas lógicas que vienen en el panel izquierdo. Dichos algoritmos se desarrollan mediante un mecanismo de "drag and drop". Abajo está el panel de la probabilidad de los resultados y, a la derecha de este panel, en la parte inferior, la esfera de Bloch. En el panel derecho tenemos un panel en el cual se va generando el código de nuestro algoritmo, en el cual podemos escoger que sea para Python o OpenQASM.

![[tutoriales-Deutsch-Jozsa_Compositor1.png]]
*Panel compositor*

En el caso de querer ejecutar el algoritmo que creamos en una computadora cuántica, tendremos que crear una instancia:

![[tutoriales-Deutsch-Jozsa_Crear_una_nueva_Instancia.png]]
*Crear una nueva instancia*

Para poder utilizar hardware real, hay que pagar una suscripción.

En dicha plataforma hemos probado los diferentes algoritmos. Tiene la ventaja, como se ve a continuación, de que los resultados y la construcción de dichos algoritmos se realizan de forma muy visual, y los resultados se van observando en la parte inferior mientras construyes el algoritmo, sin tener que ejecutarlo.

En las siguientes imágenes se pueden observar los diferentes algoritmos propuestos construidos en el simulador.

![[tutoriales-Deutsch-Jozsa_AlgoritmoDeutsch-Jozsa.png]]
*Algoritmo Deutsch Jozsa*
![[tutoriales-Benstein-Vazirani_Benstein-Vazirani.png]]
*Bernstein Vazirani*
![[tutoriales-grover_Grover010.png]]
*Grover cadena buscada 010*

### Cirq

Es una librería de código abierto creada por Google, que nace en 2018 con la idea de ofrecer un marco ligero centrado en dispositivos NISQ. Al igual que Qiskit, está escrita en Python.

La arquitectura se organiza en paquetes modulares, siendo *cirq-core* el que concentra todas las estructuras básicas de qubit, puertas y transformadores, mientras que los subpaquetes, como *cirq-google*, exponen una interfaz con servicios en la nube, con acceso a procesadores como Sycamore. También cuenta con simuladores clásicos, siendo el más habitual el *CirqSimulator*. Si se necesita mayor potencia, se puede utilizar el módulo *qsim* (backend acelerado con AVX2/AVX-512, GPU o TPU).

Tiene como ventaja su cercanía al hardware (calibraciones, tiempos de puertas y medidores de fidelidad), lo que ayuda a sacar el mayor rendimiento de los procesadores NISQ. Su enfoque modular permite añadir módulos sin requerir un núcleo monolítico muy grande, y las simulaciones con *qsim* proporcionan gran velocidad en CPU y GPU. También tiene como ventaja que, aunque fue desarrollado por Google, es *open source*, lo que permite que pueda ser adoptado por otras plataformas, como Azure, e integrarse con ellas (Microsoft Learn 2025a).

Como desventaja, al centrarse en los detalles específicos de los dispositivos, algunos flujos son menos portables que en marcos más abarcativos. Además, existen limitaciones en simulación, ya que, como todo simulador clásico, el uso de la memoria crece exponencialmente con el número de qubits, de modo que simulaciones realmente grandes exigen un hardware de gran rendimiento (Microsoft Learn 2025b).

#### Código de los distintos algoritmos

A continuación, se muestra la codificación de los diferentes algoritmos propuestos para el entorno de Cirq:

``` python
import cirq
from cirq.contrib.svg import SVGCircuit
import matplotlib.pyplot as plt
import psutil
import time

process = psutil.Process()
memory_before = process.memory_info().rss
start_time = time.time()
qc = cirq.Circuit()
q0, q1, q2, q3 = cirq.LineQubit.range(4)
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.X(q3))
qc.append(cirq.H(q3))
qc.append(cirq.X(q0))
qc.append(cirq.X(q2))
qc.append(cirq.CX(q0, q3))
qc.append(cirq.CX(q1, q3))
qc.append(cirq.CX(q2, q3))
qc.append(cirq.X(q0))
qc.append(cirq.X(q2))
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.measure(q2, q1, q0))
s = cirq.Simulator()
samples = s.run(qc, repetitions=1000)
cirq.plot_state_histogram(samples, plt.subplot())
plt.show()
SVGCircuit(qc)
```

``` python
import cirq
from cirq.contrib.svg import SVGCircuit
import matplotlib.pyplot as plt
import psutil
import time

process = psutil.Process()
memory_before = process.memory_info().rss
start_time = time.time()
qc = cirq.Circuit()
q0, q1, q2, q3 = cirq.LineQubit.range(4)
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.X(q3))
qc.append(cirq.H(q3))
qc.append(cirq.CX(q0, q3))
qc.append(cirq.H(q3))
qc.append(cirq.H(q3))
qc.append(cirq.CX(q2, q3))
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.H(q3))
qc.append(cirq.measure(q2, q1, q0))
s = cirq.Simulator()
samples = s.run(qc, repetitions=1000)
cirq.plot_state_histogram(samples, plt.subplot())
plt.show()
SVGCircuit(qc)
```

``` python
import cirq
from cirq.contrib.svg import SVGCircuit
import matplotlib.pyplot as plt
import psutil
import time

process = psutil.Process()
memory_before = process.memory_info().rss
start_time = time.time()
qc = cirq.Circuit()
q0, q1, q2, q3 = cirq.LineQubit.range(4)
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.X(q0))
qc.append(cirq.X(q2))
qc.append(cirq.CCNOT(q0, q1, q2))
qc.append(cirq.Z(q2))
qc.append(cirq.CCNOT(q0, q1, q2))
qc.append(cirq.X(q0))
qc.append(cirq.X(q2))
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.X(q0))
qc.append(cirq.X(q1))
qc.append(cirq.X(q2))
qc.append(cirq.CCNOT(q0, q1, q2))
qc.append(cirq.Z(q2))
qc.append(cirq.CCNOT(q0, q1, q2))
qc.append(cirq.X(q0))
qc.append(cirq.X(q1))
qc.append(cirq.X(q2))
qc.append(cirq.H(q0))
qc.append(cirq.H(q1))
qc.append(cirq.H(q2))
qc.append(cirq.measure(q2, q1, q0))
s = cirq.Simulator()
samples = s.run(qc, repetitions=1000)
cirq.plot_state_histogram(samples, plt.subplot())
plt.show()
SVGCircuit(qc)
```

#### Obtención de métricas

También utilizamos los cuadernos de Jupyter, como hemos hecho en Qiskit.

##### Comprobación de los resultados

En el algoritmo de Deutsch buscamos si la función es balanceada, con el siguiente algoritmo.

![[cirq_Deutshc.png]]
*Código de Deutsch*

Al hacer la medición, nos sale 111, que es 7, como se puede observar en la siguiente imagen.

![[cirq_Deutshc_resultado.png]]
*Deutsch resultado*

En el algoritmo Bernstein-Vazirani, hemos escogido como cadena secreta el 101, que multiplica a nuestra entrada y luego hace módulo 2.

Cirq nos da, también, la opción de poder dibujar el circuito que hemos hecho:

![[cirq_Deutshc_circuito.png]]
*Deutsch circuito generado por Cirq*
![[cirq_BernsteinVarizani_codigo.png]]
*Bernstein-Vazirani código*

Al ejecutar dicho algoritmo, podemos comprobar que sale el resultado esperado, que es 5 (101):

![[cirq_BernsteinVarizani_resultado.png]]
*Bernstein-Vazirani resultado*

El circuito quedaría de la siguiente manera:

![[cirq_BernsteinVarizani_circuito.png]]
*Bernstein-Vazirani circuito generado por Cirq*

Con el algoritmo de Grover intentamos buscar un elemento en un conjunto; en este caso, buscamos un elemento específico.

![[cirq_grover.png]]
*Grover código*

Después de repetir 1000 veces, sale el 2 y otro elemento con una ligera probabilidad mayor. En ocasiones, sale con mayor probabilidad el 6 que el 2, a diferencia de Qiskit, que siempre daba el elemento deseado.

![[cirq_grover_resultados.png]]
*Grover resultado*

Como se puede observar, los resultados esperados son correctos.

El circuito de Grover generado es el siguiente:

![[cirq_grover_circuito.png]]
*Grover circuito generado por Cirq*

##### Tiempo de ejecución

Al igual que con Qiskit, utilizamos el siguiente fragmento de código para comprobar su tiempo de ejecución:

Para el algoritmo de Deutsch:

![[cirq_Deutshc_metricas.png]]
*Deutsch código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0155$ segundos.

Para el algoritmo de Bernstein-Vazirani:

![[cirq_BernsteinVarizani_Metricas.png]]
*Bernstein-Vazirani código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0158$ segundos.

El algoritmo de Grover:

![[cirq_grover_metricas.png]]
*Grover código con métricas*

Obtenemos que tarda en ejecutarse:

$0.0190$ segundos.

##### Uso de la memoria

Es el mismo fragmento de código que con Qiskit.

Para el algoritmo de Deutsch:

Obtenemos que la memoria usada es de:

$0.65$ MB.

Para el algoritmo de Bernstein-Vazirani:

Obtenemos que la memoria usada es de:

$0.57$ MB.

Y para el algoritmo de Grover:

Obtenemos que la memoria usada es de:

$0.89$ MB.

##### Escalabilidad

Para la escalabilidad hemos utilizado el siguiente fragmento de código:

```
    
import cirq
import time

# Construir un circuito en cadena de CNOTs
def build_chain_circuit(num_qubits: int) -> cirq.Circuit:
    qubits = cirq.LineQubit.range(num_qubits)
    ops = []
    for i in range(num_qubits - 1):
        ops.append(cirq.CNOT(qubits[i], qubits[i+1]))
        ops.append(cirq.measure(*qubits, key='m'))
    return cirq.Circuit(ops)

# Medir tiempo de ejecución para un número de qubits
def measure_scalability(num_qubits: int) -> float:
    circuit = build_chain_circuit(num_qubits)
    simulator = cirq.Simulator()
    start = time.time()
    _ = simulator.run(circuit, repetitions=1)
    end = time.time()
    return end - start

# Probar diferentes tamaños de circuito
for n in range(5, 21, 5):
    t = measure_scalability(n)
    print(f"Tiempo para {n} qubits: {t:.4f} s")
    
```

Lo ejecutamos y el resultado que obtenemos es el siguiente para distintos números de qubits:

![[cirq_escalabilidad.png]]
*Escalabilidad con un diferente número de qubits*

En la siguiente tabla se puede observar los resultados obtenidos:

| **Qubits** | **Tiempo (s)** | **Memoria (MB)** |
|:----------:|:--------------:|:----------------:|
|     1      |     0.0015     |       0.19       |
|     2      |     0.0007     |       0.06       |
|     3      |     0.0005     |       0.01       |
|     4      |     0.0006     |       0.00       |
|     5      |     0.0005     |       0.02       |
|     6      |     0.0005     |       0.07       |
|     7      |     0.0006     |       0.00       |
|     8      |     0.0009     |       0.02       |
|     9      |     0.0013     |       0.02       |
|     10     |     0.0011     |       0.01       |
|     11     |     0.0010     |       0.03       |
|     12     |     0.0011     |       0.14       |
|     13     |     0.0013     |       0.20       |
|     14     |     0.0015     |       0.32       |
|     15     |     0.0015     |       0.72       |
|     16     |     0.0024     |       1.11       |
|     17     |     0.0041     |       0.01       |
|     18     |     0.0072     |       0.01       |
|     19     |     0.0124     |       0.02       |
|     20     |     0.0249     |       0.02       |
|     21     |     0.0480     |       0.01       |
|     22     |     0.0963     |       0.01       |
|     23     |     0.1920     |       0.01       |
|     24     |     0.3958     |       0.01       |
|     25     |     0.7534     |       0.02       |
|     26     |     1.5286     |       0.02       |
|     27     |     3.1002     |       0.02       |
|     28     |     6.2709     |       0.02       |
|     29     |    13.5956     |       0.04       |
|     30     |    33.2915     |     -215.11      |

Tiempo y memoria consumida en función del número de qubits

Como se puede ver, en números grandes de qubits se observa un consumo negativo de memoria. Esto se debe a que se producen bajadas drásticas justo después de finalizar la ejecución del simulador, antes de que el comando `memory_info()` pueda medirlo. Algunas mediciones resultan incluso más bajas que al inicio de la ejecución del circuito.

Para verificarlo, hemos utilizado el administrador de tareas para comprobar su uso real, el cual, como se aprecia en las siguientes imágenes, es muy superior al consumo reportado por Qiskit. En este caso, llega a consumir casi toda la memoria RAM durante la ejecución.

También hemos notado que el consumo de memoria no presenta picos drásticos cuando se trabaja con pocos qubits.

![[cirq_memoriausada_antesdellegar39.png]]
*Uso de memoria RAM*

#### Google Quantum AI Cloud Service

Es el servicio de Google que permite a investigadores, empresas y estudiantes ejecutar circuitos en procesadores cuánticos reales. Pero conseguir acceso es muy complicado, necesita autenticación por parte de un representante de Google y te tiene que meter en una lista de acceso al hardware. Google tiene un enfoque distinto al de IBM y al de Microsoft, los cuales te dejan acceso a su hardware a cambio de una suscripción.(AI 2025)

En el caso de conseguir tener acceso, para poder utilizar el procesador cuántico desde nuestro código, tenemos que llamar a la API de Google de la siguiente manera.

Primero nos autenticamos con el siguiente código en la consola:

```
gcloud auth application-default login
```

Luego, desde Colab importamos las librerías:

```
from google.colab import auth
    auth.authenticate_user()    
```

Por último, para poder comunicarnos desde el código usamos la clase `engine` del paquete `cirq_google` para comunicarnos con nuestro servidor:

```
import cirq
    import cirq_google as cg
    engine = cg.Engine(project_id="TU_PROJECT_ID")
    processor = engine.get_processor("NOMBRE_DEL_PROCESADOR")
    sampler = processor.get_sampler()
    results = sampler.run(circuit, repetitions=...)
```

### Microsoft Quantum Development Kit QDK

QDK (Quantum Development Kit) es un conjunto de herramientas desarrollado por Microsoft con el fin del desarrollo de algoritmos cuánticos y su ejecución en plataformas de computación cuántica. Este kit está diseñado para permitir la simulación en hardware clásico o ejecutarlo en real a través de Azure Quantum.

Dispone de su propio lenguaje, que es Q#, un lenguaje de alto nivel diseñado para escribir algoritmos cuánticos. Es muy intuitivo y está altamente optimizado para describir operaciones cuánticas y algoritmos de control cuántico. Se integra bien con lenguajes como Python y C#. Incluye simuladores de alta calidad, como el Quantum Simulator, que permite ejecutar algoritmos cuánticos en hardware clásico para depurar y probar dichos algoritmos. Se puede integrar con herramientas como Visual Studio y Visual Studio Code. Además, dispone de numerosos tutoriales.

Tiene la desventaja de que los modelos de ruido y decoherencia no siempre son tan detallados o realistas como en otras plataformas específicas para la simulación de estos efectos. Además, como con otros modelos, su simulación en hardware clásico es muy limitada.

#### Código de los distintos algoritmos

A continuación, se muestra la codificación de los diferentes algoritmos propuestos para el entorno de QDK:

```
import Std.Diagnostics.*;
import Std.Math.*;
import Std.Measurement.*;
operation Main() : (String, Bool)[] {
    let nameFunctionTypeTuples = [("SimpleConstantBoolF", SimpleConstantBoolF, true), 
    ("SimpleBalancedBoolF", SimpleBalancedBoolF, false), ("ConstantBoolF", ConstantBoolF, true), ("BalancedBoolF", BalancedBoolF, false)];
    mutable results = [];
    for (name, fn, shouldBeConstant) in nameFunctionTypeTuples {
        let isConstant = DeutschJozsa(fn, 5);
        if (isConstant != shouldBeConstant) {
            let shouldBeConstantStr = shouldBeConstant ? "constant" | "balanced";
            fail $"{name} should be detected as {shouldBeConstantStr}";
        }
        let isConstantStr = isConstant ? "constant" | "balanced";
        Message($"{name} is {isConstantStr}");
        results += [(name, isConstant)];
    }
    return results;
}
operation DeutschJozsa(Uf : ((Qubit[], Qubit) => Unit), n : Int) : Bool {
    use queryRegister = Qubit[n];
    use target = Qubit();
    X(target); H(target);
    within { for q in queryRegister { H(q); } } apply { Uf(queryRegister, target); }
    mutable result = true;
    for q in queryRegister { if MResetZ(q) == One { result = false; } }
    Reset(target);
    return result;
}
operation SimpleConstantBoolF(args : Qubit[], target : Qubit) : Unit { X(target); }
operation SimpleBalancedBoolF(args : Qubit[], target : Qubit) : Unit { CX(args[0], target); }
operation ConstantBoolF(args : Qubit[], target : Qubit) : Unit { 
    for i in 0..(2^Length(args)) - 1 { ApplyControlledOnInt(i, X, args, target); } }
operation BalancedBoolF(args : Qubit[], target : Qubit) : Unit { 
    for i in 0..2..(2^Length(args)) - 1 { ApplyControlledOnInt(i, X, args, target); } }
```

```
import Std.Arrays.*;
import Std.Convert.*;
import Std.Diagnostics.*;
import Std.Math.*;
import Std.Measurement.*;

operation Main() : Int[] {
    let nQubits = 10;
    let integers = [127, 238, 512];
    mutable decodedIntegers = [];
    for integer in integers {
        let parityOperation = EncodeIntegerAsParityOperation(integer);
        let decodedBitString = BernsteinVazirani(parityOperation, nQubits);
        let decodedInteger = ResultArrayAsInt(decodedBitString);
        Fact(decodedInteger == integer, $"Decoded integer {decodedInteger}, but expected {integer}.");
        Message($"Successfully decoded bit string as int: {decodedInteger}");
        decodedIntegers += [decodedInteger];
    }
    return decodedIntegers;
}

operation BernsteinVazirani(Uf : ((Qubit[], Qubit) => Unit), n : Int) : Result[] {
    use queryRegister = Qubit[n];
    use target = Qubit();
    X(target);
    within {
        ApplyToEachA(H, queryRegister);
    } apply {
        H(target);
        Uf(queryRegister, target);
    }
    let resultArray = MResetEachZ(queryRegister);
    Reset(target);
    return resultArray;
}

operation ApplyParityOperation(
    bitStringAsInt : Int,
    xRegister : Qubit[],
    yQubit : Qubit
) : Unit {
    let requiredBits = BitSizeI(bitStringAsInt);
    let availableQubits = Length(xRegister);
    Fact(
        availableQubits >= requiredBits,
        $"Integer value {bitStringAsInt} requires {requiredBits} bits to be represented but the quantum register only has {availableQubits} qubits"
    );
    for index in IndexRange(xRegister) {
        if ((bitStringAsInt &&& 2^index) != 0) {
            CNOT(xRegister[index], yQubit);
        }
    }
}

function EncodeIntegerAsParityOperation(bitStringAsInt : Int) : (Qubit[], Qubit) => Unit {
    return ApplyParityOperation(bitStringAsInt, _, _);
}
```

```
import Std.Convert.*;
import Std.Math.*;
import Std.Arrays.*;
import Std.Measurement.*;
import Std.Diagnostics.*;
operation Main() : Result[] {
    let nQubits = 5;
    let nIterations = IterationsToMarked(nQubits);
    Message($"Number of iterations: {nIterations}");
    let results = GroverSearch(nQubits, nIterations, ReflectAboutMarked);
    return results;
}
operation GroverSearch(nQubits : Int, iterations : Int, phaseOracle : Qubit[] => Unit) : Result[] {
    use qubits = Qubit[nQubits];
    PrepareUniform(qubits);
    for _ in 1..iterations { phaseOracle(qubits); ReflectAboutUniform(qubits); }
    return MResetEachZ(qubits);
}
function IterationsToMarked(nQubits : Int) : Int {
    if nQubits > 126 { fail "This sample supports at most 126 qubits."; }
    let nItems = 2.0^IntAsDouble(nQubits);
    let angle = ArcSin(1. / Sqrt(nItems));
    let iterations = Round(0.25 * PI() / angle - 0.5);
    return iterations;
}
operation ReflectAboutMarked(inputQubits : Qubit[]) : Unit {
    Message("Reflecting about marked state...");
    use outputQubit = Qubit();
    within { X(outputQubit); H(outputQubit); for q in inputQubits[...2...] { X(q); } } apply { Controlled X(inputQubits, outputQubit); }
}
operation PrepareUniform(inputQubits : Qubit[]) : Unit is Adj + Ctl { for q in inputQubits { H(q); } }
operation ReflectAboutAllOnes(inputQubits : Qubit[]) : Unit { Controlled Z(Most(inputQubits), Tail(inputQubits)); }
operation ReflectAboutUniform(inputQubits : Qubit[]) : Unit {
    within { Adjoint PrepareUniform(inputQubits); for q in inputQubits { X(q); } } apply { ReflectAboutAllOnes(inputQubits); }
}
```

#### Obtención de métricas

Para ello hemos utilizado Jupyter para tomar las medidas y Visual Studio para su ejecución.

##### Comprobación de los resultados esperados

En el algoritmo de Deutsch buscamos si la función es balanceada y, al ejecutarlo, nos devuelve que la función es balanceada.

![[qs_DeutschJozsa.png]]
*Ejecución del código de Deutsch*

También puedes generar el circuito desde el propio IDE Visual Studio dando a la siguiente opción.

![[qs_generar circuito.png]]
*Generar circuito en Visual Studio Code*

El circuito generado es el siguiente:

![[qs_DeutschJozsa_circuito.png]]
*DeutschJozsa circuito generado en Visual Studio Code*

En el algoritmo Bernstein-Vazirani, hemos escogido diferentes cadenas secretas, las cuales son 127, 238, 512.

![[qs_BernsteinVazirani.png]]
*Ejecución del código de Bernstein-Vazirani*

El circuito generado es:

![[qs_BernsteinVazirani_circuito.png]]
*BernsteinVazirani circuito generado en Visual Studio Code*

Con el algoritmo de Grover intentamos buscar un elemento en un conjunto; en este caso, buscamos un elemento específico que es el siguiente: 01010.

![[qs_grover.png]]
*Ejecución del código de Grover*

Como se puede observar, los resultados esperados son el 01010.

Por último, su circuito generado es:

![[qs_generar circuito.png]]
*Grover circuito generado en Visual Studio Code*

##### Tiempo de ejecución

En Q# puro no existe una API nativa para medir el tiempo como se haría en C# con `Stopwatch`, ya que Q# está diseñado para describir algoritmos cuánticos y delegar su ejecución al *host* o simulador.

Si queremos medir el tiempo directamente desde Q#, no contamos con un temporizador integrado, pero existen dos opciones:

**Medir desde el host**

Lo habitual en Q# es que la medición del tiempo se realice desde el programa anfitrión (en F#, C# o Python), ya que Q# no dispone de interfaces para leer el reloj del sistema. Este enfoque permite conocer con precisión cuánto tarda en ejecutarse una operación cuántica y es el más utilizado, dado que Q# no ofrece primitivas para acceder al tiempo directamente.

La razón se debe a que el lenguaje está diseñado para ser agnóstico con respecto al hardware y, por lo tanto, no tiene acceso a funciones del sistema, como puede ser la medición del tiempo.

Para ello, crearemos un programa *host* en Python que mida el tiempo que tarda en ejecutarse nuestro programa escrito en Q#. Este enfoque presenta poca granularidad, ya que no solo se mide el tiempo de ejecución del circuito, sino también la carga de las librerías. Para ello utilizaremos los cuadernos de Jupyter. Para ello hay que indicar al cuaderno de Jupyter qué parte de código pertenece a qshar; para ello tenemos que importar dicha librería. En la casilla donde se ejecute qsharp, ponemos al principio %%qsharp.

Para el tiempo hemos utilizado el mismo fragmento que hemos utilizado anteriormente, que hemos mostrado anteriormente en apartados anteriores. También se puede usar %%time para mirar el tiempo de una casilla.

![[qs_DeutschJozsa_metricas.png]]
*Deutsch código con métricas*

Obtenemos que tarda en ejecutarse:$0.0204$ segundos.

Para el algoritmo de Bernstein-Vazirani:

![[qs_BernsteinVazirani_metricas.png]]
*Bernstein-Vazirani código con métricas*

Obtenemos que tarda en ejecutarse:$0.0150$ segundos.

El algoritmo de Grover:

![[qs_grover_metricas.png]]
*Grover código con métricas*

Tarda en ejecutarse:$0.0174$ segundos.

##### Uso de la memoria

Para el algoritmo de Deutsch obtenemos que la memoria usada es de: $0.66$ MB.

Para el algoritmo de Bernstein-Vazirani obtenemos que la memoria usada es de: $0.43$ MB.

En el algoritmo de Grover obtenemos que la memoria usada es de: $0.61$ MB.

##### Escalabilidad

En el caso de quieras probar las escalabilidad como en los anteriores simuladores utilizando un algoritmo que solo incorporar CNOT y Hadamard y haces mediciones como en los anteriores como el siguiente ejemplo de código:

```
import Std.Diagnostics.*;   
    import Std.Measurement.*;
    operation Main() : Unit {   
        // Lista de tamaños de qubits que queremos probar   
        let qubitCounts = [5, 10, 15, 20,30, 40, 50];       
        for n in 1  ..  100 {       
            Message($"Ejecutando CNOTChain con {n} qubits...");
            CNOTChain(n);           
        }   
    }
    operation CNOTChain(n : Int) : Unit {
        use qs = Qubit[n];      
        for q in qs {       
            H(q);
        }                   
        for i in 0 .. n - 2 {           
            CX(qs[i], qs[i + 1]);       
        }
        
        // Medimos todos los qubits para evitar estados residuales
        for q in qs {       
            _ = MResetZ(q);         
        }
    }
    
```

Primero, no hay un límite de qubits por el teorema de Gottesman–Knill, porque los circuitos solo con puertas Clifford (H, S, CNOT y Pauli) se pueden simular eficientemente con un simulador de estabilizadores, incluso con miles de qubits. Para conseguir ver el rendimiento real, hay que emplear puertas no Clifford, como por ejemplo una puerta que da una rotación con ángulo no múltiplo y rompe, por tanto, el régimen de estabilizadores, obligando al simulador a manejar estados completos de $2^n$ amplitudes.

Por otro lado, el compilador optimiza el código y borra operaciones no necesarias, haciendo que el fragmento de código anterior no sirva.

Para hacer la prueba de escalabilidad, en este caso no podemos mirar ni la memoria ni el consumo de memoria en cada iteración debido a la naturaleza del lenguaje. Hemos utilizado el código de Deutsch, al cual hemos ido aumentando el número de qubits paulatinamente, y consigue trabajar hasta con 16 qubits, aunque sabemos que el límite teórico está en 30 qubits.

![[qs_escalabilidad_ejecucion.png]]
*Escalabilidad ejecución*

Podemos ver en la siguiente imagen que toma una postura parecida a la de Qiskit, paralelizando su proceso por diferentes núcleos de la CPU y no consumiendo mucha memoria.

![[qs_escalabilidad.png]]
*Escalabilidad*

#### Estimador de recursos cuánticos

Un **estimador de recursos cuánticos** es una herramienta que calcula la cantidad de recursos necesarios para ejecutar un algoritmo cuántico en un ordenador cuántico real. Su objetivo no es simular el algoritmo a nivel físico, sino predecir, bajo ciertos modelos de hardware y corrección de errores, los siguientes aspectos clave:

- Número de *qubits lógicos* necesarios para implementar el algoritmo.

- Número de *qubits físicos* requeridos, teniendo en cuenta la codificación redundante para tolerancia a fallos.

- Tiempo estimado de ejecución en un dispositivo cuántico con características concretas.

- Coste en puertas cuánticas, incluyendo operaciones especiales como los *T states*.

![[qs_Estimador de Recursos.png]]
*Estimador de Recursos QDK*

#### Microsoft Azure Quantum

Es una plataforma de Microsoft que facilita el desarrollo y la ejecución de algoritmos cuánticos, permitiendo a los usuarios acceder a hardware real y simuladores cuánticos. Tiene acceso a diferentes proveedores de hardware cuántico y lenguajes de programación, siendo una alternativa muy interesante para los inversores.

![[Azure_Panel principal.png]]
*Panel principal de Azure*

Los diferentes tipos de hardware cuántico que dispone son los siguientes:

- **IonQ:** Con dispositivos basados en trampas de iones.

- **Honeywell:** Con sistemas cuánticos basados en trampas de iones también.

- **Quantum Circuits:** Dispositivos cuánticos superconductores.

- **Pasqal:** Dispositivos cuánticos de átomos fríos.

Además de los simuladores de alto rendimiento que dispone.

Soporta los siguientes lenguajes: Q#, Python y C, más la integración con Cirq.

Dispone de diferentes simuladores como:

- **Quantum Simulator:** Simulador completo para poder ejecutar circuitos cuánticos sin tener el hardware necesario.

- **Qsim:** Orientado a la ejecución de circuitos grandes usando hardware de alto rendimiento.

- **Simuladores híbridos:** Permite la ejecución de algoritmos cuánticos con cálculos clásicos. Es utilizado para algoritmos híbridos cuántico-clásicos.

Dispone de un kit de desarrollo (QDK) que permite depurar y ejecutar los algoritmos cuánticos. Este kit incluye el Quantum Simulator. Además, dispone de un entorno para experimentar con Q# y Python (Azure Notebooks) de manera más interactiva.

También, permite conectar los diferentes dispositivos cuánticos con nuestros algoritmos a través de la nube, para que puedan ser consumidos como servicio en forma de API para otras aplicaciones.

Por último, hemos intentado realizar una prueba en el simulador, pero la suscripción de *Azure Quantum* no está incluida en *Azure for Students*, ya que Microsoft limita los servicios a su *core*, que son las máquinas virtuales, bases de datos y almacenamiento, y no habilita a proveedores externos como IonQ, Quantinuum o Rigetti, que son la base de *Azure Quantum*.

Como se puede ver en las siguientes imágenes al estar con la cuenta de estudiante se genera el siguiente error.

Primero generamos nuestro grupo de recursos:

![[Azure_Azure de grupo de Recurso.png]]
*Grupo de recursos de Azure*

El error generado es el siguiente:

![[Azure_Error al crear el area de trabajo.png]]
*Error al crear el área de trabajo*

## Resultados

> La seguridad no trata de tecnología, sino de resultados.
>
> — Kevin Mitnick \### Introducción {#sec:introduccion-resultados}

El objetivo de esta sección es presentar los resultados obtenidos de la ejecución de los distintos algoritmos cuánticos Deutsch, Bernstein-Vazirani y Grover en varios entornos de simulación. Con el objetivo principal de comprobar su rendimiento para identificar sus puntos positivos y negativos. Además de comparar dichos simuladores por su rendimiento, también se compara a nivel de facilidad de uso y su curva de aprendizaje. En cuanto a la comparativa, se han empleado diferentes entornos y, para su ejecución, se ha elegido un conjunto de algoritmos igual para los diferentes simuladores. Para poder hacer la comparación entre ellos.

### Entorno experimental

El entorno experimental ha estado compuesto por los siguientes simuladores: Qiskit Aer, Cirq, QuEST y Microsoft Quantum Development Kit (QDK), cada uno ejecutado en su entorno correspondiente: Qiskit Aer en Python, Cirq en Python con integración de Google Quantum AI, QuEST en C/C++ y QDK en Q# mediante Visual Studio Code.

Para la visualización de los datos, en la mayoría de los casos se ha optado por usar los cuadernos de Jupyter, salvo para algunos casos como han sido QuEST y Q#, que se ha utilizado Visual Studio Code.

En todos los simuladores se ha empleado el mismo conjunto de pruebas con el fin de homogeneizarlas. En el caso de Q#, se recurrió a un programa host en Python para medir los tiempos de ejecución, ya que el lenguaje no dispone de acceso al temporizador del sistema operativo.

#### Métricas

Las métricas utilizadas fueron:

- **Tiempo de ejecución (s):** Medido en segundos, el tiempo que tarda en ejecutarse el algoritmo.

- **Uso medio de memoria (MB):** Consumo de memoria, para ello se mide el antes y el después de la ejecución del algoritmo.

- **Escalabilidad:** Capacidad del simulador para incrementar el número de qubits y ver cómo reacciona el simulador.

#### Estrategia y metodología de experimentación

Se ejecutaron los algoritmos de Deutsch, de Bernstein-Vazirani y de Grover de forma secuencial, manteniendo el mismo hardware en los distintos simuladores para comprobar la diferencia entre ellos.

1.  **Preparación del entorno:** Instalación y configuración de cada simulador, implementación del código y comprobación de su correcto funcionamiento.

2.  **Ejecución y medición:** Cada prueba se repitió un mínimo de tres veces con el objetivo de promediar los resultados.

3.  **Análisis comparativo:** Por último, se muestran los datos en una tabla comparativa.

Para la medición y visualización de resultados se emplearon herramientas como Jupyter y Visual Studio Code.

### Resultados de las comparaciones

#### Tabla comparativa a nivel general de los distintos simuladores

En las siguientes tablas se hace una comparación a nivel general de las ventajas y desventajas que tiene cada simulador.

<table style="width:100%;">
<caption>Ventajas y desventajas de los simuladores cuánticos.</caption>
<colgroup>
<col style="width: 10%" />
<col style="width: 37%" />
<col style="width: 51%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;"><strong>Simulador</strong></th>
<th style="text-align: left;"><strong>Ventajas</strong></th>
<th style="text-align: left;"><strong>Desventajas</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><strong>Qiskit Aer</strong></td>
<td style="text-align: left;"><p>• Simulación de alto rendimiento orientada a ejecución en hardware real</p>
<p>• Compatible con módulos como Qiskit Terra</p>
<p>• Amplia documentación en Internet</p>
<p>• Optimización en CPU y GPU</p></td>
<td style="text-align: left;"><p>• Requiere conocimiento profundo de las herramientas</p>
<p>• Solo funciona en el ecosistema de IBM</p>
<p>• No permite el uso de Cirq en su entorno</p>
<p>• Limitado a hardware IBM para ejecución real</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>Cirq</strong></td>
<td style="text-align: left;"><p>• Simulador de alta flexibilidad con interoperabilidad con otros frameworks</p>
<p>• Optimización en GPU y CPU</p>
<p>• Integración con Google Quantum AI</p>
<p>• Soporta variedad de backends cuánticos (Google, IonQ)</p></td>
<td style="text-align: left;"><p>• Interoperabilidad con otros frameworks, no siempre garantizada</p>
<p>• Necesita hardware de alto rendimiento para simulaciones clásicas</p>
<p>• Crecimiento del consumo exponencial a partir de 25 qubits</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><strong>QuEST</strong></td>
<td style="text-align: left;"><p>• Simulaciones precisas y de alto rendimiento</p>
<p>• Uso de aceleración en GPU y paralelización</p></td>
<td style="text-align: left;"><p>• No incluye interfaz gráfica de usuario</p>
<p>• Curva de aprendizaje alta debido a su paralelización</p>
<p>• Falta de documentación actualizada</p>
<p>• No dispone de integración con hardware cuántico real</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><strong>QDK (Microsoft)</strong></td>
<td style="text-align: left;"><p>• Integración con Azure Quantum y hardware cuántico real</p>
<p>• Lenguaje Q# especializado para algoritmos cuánticos</p>
<p>• Simuladores eficientes para pruebas y depuración</p>
<p>• Amplia documentación en Internet</p></td>
<td style="text-align: left;"><p>• Orientado principalmente a Azure</p>
<p>• Modelos de ruido y decoherencia menos detallados</p>
<p>• Aunque en teoría se puede llegar a 30 qubits a partir de los 16, tarda en ejecutarse un tiempo excesivo</p></td>
</tr>
</tbody>
</table>

Ventajas y desventajas de los simuladores cuánticos.

#### Tabla comparativa a nivel del rendimiento obtenido de los diferentes simuladores

En la siguiente tabla se muestran los resultados obtenidos de los simuladores, tomando como métrica el consumo de memoria y el tiempo en ejecución.

| **Simulador**     | **Deutsch: (segundos)/(MBytes)** | **Bernstein-Vazirani: (segundos)/(MBytes)** | **Grover: (segundos)/(MBytes)** |     |
|:------------------|:--------------------------------:|:-------------------------------------------:|:-------------------------------:|-----|
| **Qiskit Aer**    |          0.0364 / 2.42           |                0.0247 / 2.33                |          0.0182 / 2.89          |     |
| **Cirq**          |          0.0155 / 0.65           |                0.0158 / 0.57                |          0.0190 / 0.89          |     |
| **QuEST**         |               N/D                |                     N/D                     |               N/D               |     |
| **Microsoft QDK** |          0.0204 / 0.66           |                0.0150 / 0.43                |          0.0174 / 0.61          |     |

Métricas de rendimiento de los simuladores cuánticos

Podemos ver en la tabla que el que mejor desempeño muestra cuando son pocos qubits es el de Google Cirq, consumiendo la mitad de tiempo que el IBM Qiskit Aer y su consumo de memoria es parecido al de Microsoft.

Aunque, en cuanto a escalabilidad, cuando trabaja con un número mayor a partir de 25 qubits, el simulador de Google es el que peor desempeño muestra, ya que los otros presentan una mejor paralelización utilizando el formalismo de estabilizadores para poder simular eficientemente puertas de Clifford.

En cuanto al de QuEST se ha puesto N/D porque dicho simulador ha sido descartado debido a la falta de documentación sólida.

A continuación, se muestran en las siguientes gráficas los datos obtenidos:

*(Los siguientes datos corresponden a un gráfico de barras del documento original, generado con TikZ/PGFPlots; se reproducen como tabla al no disponer de un motor LaTeX para renderizarlo.)*

| Algoritmo | Qiskit Aer (s) | Cirq (s) | Microsoft QDK (s) |
| --- | --- | --- | --- |
| Deutsch-Jozsa | 0.036 | 0.015 | 0.019 |
| Bernstein-Vazirani | 0.024 | 0.016 | 0.015 |
| Grover | 0.018 | 0.019 | 0.018 |

*Gráfico comparativo de los resultados respecto al tiempo*
*(Datos del gráfico de barras original, generado con TikZ/PGFPlots, reproducidos como tabla.)*

| Algoritmo | Qiskit Aer (MB) | Cirq (MB) | Microsoft QDK (MB) |
| --- | --- | --- | --- |
| Deutsch-Jozsa | 2.4 | 0.65 | 0.68 |
| Bernstein-Vazirani | 2.3 | 0.58 | 0.45 |
| Grover | 2.9 | 0.95 | 0.62 |

*Gráfico comparativo de los resultados respecto al consumo de memoria*

En cuanto a la escalabilidad, se observan los siguientes resultados:

| **Simulador**       | **Metodología de Prueba**                                                                                                | **Resultados y Observaciones**                                                                                                                                                                                                                                                       | **Límite Práctico de Qubits** |
|:--------------------|:-------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------|
| **Qiskit Aer**      | Circuito en cadena compuesto por puertas CNOT, midiendo tiempo de ejecución con número creciente de qubits.              | Escalabilidad eficiente gracias a paralelización en CPUs multinúcleo. A partir de 25 qubits, el consumo de memoria crece exponencialmente.                                                                                                                                           |  30 qubits                    |
| **Cirq**            | Circuito en cadena similar con puertas CNOT.                                                                             | Rendimiento se degrada notablemente a partir de 25 qubits. Picos altos en uso de RAM que llegan casi al límite del sistema. Mediciones negativas aparentes por liberación abrupta de memoria tras ejecución. Más adecuado para prototipado y simulación en hardware real (Sycamore). | \< 25 qubits                  |
| **QDK (Microsoft)** | Algoritmo de Deutsch-Jozsa, debido a optimizaciones que eliminan operaciones redundantes en puertas Clifford (H y CNOT). | Ejecuciones eficientes hasta 16 qubits con bajo consumo de memoria y paralelización similar a Qiskit. Soporte teórico hasta 30 qubits en entornos estándar. Integración sólida con Azure para computación híbrida.                                                                   | 16-30 qubits                  |

Comparación de la escalabilidad de simuladores cuánticos

*(Datos del gráfico de líneas original, generado con TikZ/PGFPlots, reproducidos como tabla.)*

| Qubits | Qiskit Aer (s) | Cirq (s) |
| --- | --- | --- |
| 5 | 0.0004 | 0.0005 |
| 10 | 0.0012 | 0.0011 |
| 15 | 0.0048 | 0.0015 |
| 20 | 0.0192 | 0.0249 |
| 25 | 0.0768 | 0.7534 |
| 30 | 0.3072 | 33.2915 |

*Comparativa de tiempo de simulación en función del número de qubits (escala logarítmica en y).*

En el siguiente gráfico se puede compara el máximo número de qubits que se han podido simular con cada uno de los simuladores.

*(Datos del gráfico de barras original, generado con TikZ/PGFPlots, reproducidos como tabla.)*

| Simulador | Escalabilidad (qubits simulados) |
| --- | --- |
| Qiskit Aer | 32 |
| Cirq | 30 |
| Microsoft QDK | 16 |

*Comparativa de número de qubits alcanzados entre los diferentes simuladores.*

#### Tabla comparativa a nivel de la relevancia de los diferentes simuladores

A continuación, la siguiente tabla muestra las características más relevantes para escoger un simulador u otro:

| **Característica**                | **Qiskit Aer**  | **Cirq**                    | **QuEST**                 | **QDK**                      |
|:----------------------------------|:----------------|:----------------------------|:--------------------------|:-----------------------------|
| **Característica**                | **Qiskit Aer**  | **Cirq**                    | **QuEST**                 | **QDK**                      |
| Lenguaje de programación          | Python          | Python                      | C, C++                    | Q#                           |
| Integración con hardware cuántico | Sí (IBM)        | Sí (Google y Azure Quantum) | No                        | Sí (Azure Quantum)           |
| Simulación de qubits              | Hasta 32 qubits | Hasta 30                    | Hasta 24 qubits           | Hasta 16 qubits              |
| Modelos de ruido y errores        | Sí              | Sí                          | Sí                        | Sí                           |
| Open Source                       | Sí              | Sí                          | Sí                        | APIs y herramientas C/C++    |
| Facilidad de uso                  | Alta            | Alta                        | Muy Baja                  | Media                        |
| Entorno de desarrollo             | Qiskit          | Cirq                        | APIs y herramientas C/C++ | Visual Studio, Azure Quantum |

Características de los diferentes simuladores cuánticos.

#### Tabla comparativa de los entornos de despliegue

La siguiente tabla muestra las diferencias entre las diferentes plataformas:

| **Característica**                | **Microsoft Azure Quantum**            | **IBM Quantum Experience**   | **Google Quantum AI**              |
|:----------------------------------|:---------------------------------------|:-----------------------------|:-----------------------------------|
| Lenguaje de programación          | Q#, Python                             | Python (Qiskit)              | Python (Cirq)                      |
| Integración con hardware cuántico | Sí (IonQ, Quantinuum, Rigetti, Pasqal) | Sí (propio de IBM)           | Sí (propio de Google)              |
| Simulación de qubits              | Variable                               | Hasta 32 qubits              | Hasta  40 qubits (Cirq simulators) |
| Modelos de ruido y errores        | Sí                                     | Sí                           | Sí                                 |
| Open Source                       | No                                     | Sí (Qiskit)                  | Sí (Cirq, OpenFermion)             |
| Facilidad de uso                  | Alta                                   | Alta                         | Media (orientado a investigación)  |
| Entorno de desarrollo             | Azure Portal, QDK                      | Qiskit, IBM Quantum Composer | Cirq, Jupyter Notebooks            |

Comparación entre Microsoft Azure Quantum, IBM Quantum Experience y Google Quantum AI.

A la hora de elegir una plataforma es interesante saber qué proveedores utiliza cada uno, porque dependiendo del proveedor tendremos una tecnología determinada, la cual tiene unas ventajas sobre otras dependiendo de lo que queramos probar. En la siguiente tabla podemos ver qué proveedores de hardware tenemos disponibles.

| **Proveedor nube** | **Plataforma / SDK**               | **Proveedores de hardware disponibles**                                                                                        | **Notas**                                                   |
|:-------------------|:-----------------------------------|:-------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------|
| **IBM**            | IBM Quantum, SDK Qiskit            | Solo hardware propio (procesadores superconductores: Eagle, Heron, Condor, etc.)                                               | Acceso gratuito y de pago, comunidad grande                 |
| **Google**         | Cirq, acceso vía Google Quantum AI | Solo hardware propio (superconductores, chip Sycamore)                                                                         | Acceso limitado, más orientado a investigación con partners |
| **Microsoft**      | Azure Quantum                      | IonQ (iones atrapados), Quantinuum (iones atrapados), Rigetti (superconductores), Pasqal (átomos neutros), simuladores propios | Enfocado en ecosistema híbrido clásico-cuántico             |

Principales proveedores de nube cuántica y el hardware que ofrecen.

En la siguiente tabla se explica cada proveedor para que el lector tenga una visión comparativa de cada uno:

| **Proveedor**                 | **Tecnología**                     | **Procedencia**      | **Definición breve**                                                                                                                                        |
|:------------------------------|:-----------------------------------|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IBM Quantum                   | Superconductores                   | EE.UU.               | Pionero en computación cuántica con procesadores como Eagle (127 qubits), Heron (156) y Condor (1121). Acceso global en nube con Qiskit.                    |
| Google Quantum AI             | Superconductores                   | EE.UU.               | Desarrolló el chip Sycamore y demostró la “supremacía cuántica” en 2019. Enfocado en investigación avanzada.                                                |
| Rigetti                       | Superconductores                   | EE.UU.               | Startup que ofrece acceso a procesadores cuánticos vía su plataforma Forest y AWS Braket.                                                                   |
| OQC (Oxford Quantum Circuits) | Superconductores                   | Reino Unido          | Empresa que desarrolla procesadores superconductores accesibles en la nube (AWS Braket, propios).                                                           |
| IQM                           | Superconductores                   | Finlandia            | Enfocada en construir sistemas cuánticos locales para centros de investigación y supercomputadores europeos.                                                |
| IonQ                          | Iones atrapados                    | EE.UU.               | Líder en iones atrapados, ofrece máquinas en AWS Braket, Azure Quantum y Google Cloud. Alta fidelidad en operaciones.                                       |
| Quantinuum                    | Iones atrapados                    | EE.UU. / Reino Unido | Resultado de la fusión de Honeywell Quantum Solutions (EE.UU.) con Cambridge Quantum (Reino Unido). Destacado por su corrección de errores y software TKET. |
| QuEra                         | Átomos neutros                     | EE.UU.               | Startup de Boston que usa átomos de Rydberg. Su máquina Aquila (256 qubits) está disponible en AWS Braket.                                                  |
| Pasqal                        | Átomos neutros                     | Francia              | Competidor europeo de QuEra. Enfocado en simulación cuántica y optimización industrial.                                                                     |
| Xanadu                        | Fotones                            | Canadá               | Líder en computación cuántica fotónica. Ofrece acceso en la nube (Xanadu Cloud) y SDK PennyLane para machine learning cuántico.                             |
| D-Wave                        | Recocido cuántico                  | Canadá               | Especializado en optimización mediante annealing. Ofrece miles de qubits físicos en sus sistemas Advantage.                                                 |
| SpinQ                         | NMR (resonancia magnética nuclear) | China                | Fabrica pequeños ordenadores cuánticos de sobremesa (2–3 qubits) para enseñanza e investigación básica.                                                     |

Principales proveedores de hardware cuántico, su tecnología y procedencia.

## Conclusiones y líneas futuras

### Conclusiones

Este trabajo espera servir como introducción para entender el funcionamiento de la computación cuántica, su historia, y mostrar el funcionamiento de diferentes simuladores, comparando su distinto rendimiento. Para ello se han ejecutado algoritmos como Deutsch-Jozsa, Bernstein-Vazirani y Grover. Los simuladores son una pieza central para el desarrollo de diferentes algoritmos en los cuales necesitamos probar una cantidad menor de 32 qubits.

Las pruebas han revelado que, en términos de rendimiento e integración con otros lenguajes para tomar métricas, el mejor sería Qiskit Aer; aunque tiene la desventaja de que está pensado solo para ejecutar con hardware de IBM, tiene muy buena paralelización. El de Microsoft escrito en Q# muestra muy buenos resultados también en términos de rendimiento. Pero su integración con otros lenguajes, debido a la naturaleza de Q# hace que sea más complicado. En cambio, en términos de consumo de memoria, el que peor ha mostrado resultados cuando se usa una gran cantidad (cerca de los 27 qubits) es el de Cirq. Aunque el desempeño en términos generales entre los tres es muy similar cuando se utilizan pocos qubits y probando diferentes algoritmos.

Para prueba de concepto (PoC) rápida y probar su funcionamiento de manera rápida, se recomienda el uso de Qiskit Aer o Cirq, ya que, al estar hechos en Python, su desarrollo es mucho más rápido porque presentan una curva de aprendizaje menor que Q#, y tienen acceso a funciones estándar del sistema operativo, como poder acceder al consumo de memoria y al reloj de este.

Por otro lado, el simulador de QuEST sí sus creadores proporcionan una documentación sólida y actualizada. Además, continúan con su desarrollo siguiendo el principio de que el código tiene que estar cerrado a modificaciones y abierto a extensiones, en lugar de modificar todas las API, cambiando tanto los parámetros que reciben las funciones como los valores de retorno, no conllevaría que, aunque su documentación estuviera desactualizada respecto al código que presentan, no funcionase. También el enfoque lleva a que no pueda ser usado en un proyecto serio, porque al no seguir el principio Open/Closed hace que el código no sea retrocompatible con versiones nuevas, de modo que, en el caso de bajar una versión actualizada de su código, los algoritmos que has desarrollado dejasen de funcionar. A pesar de todo lo dicho anteriormente, es una alternativa buena que no depende de las decisiones de una empresa y puede tener una buena proyección a futuro.

En cuanto a las plataformas en la nube, considero que la plataforma de IBM presenta no solo una buena documentación, sino un simulador web en el cual puedes probar los algoritmos con unos pocos qubits sin tener que instalar nada de software, el único requisito es tener una cuenta de IBM. En cambio, acceder a la plataforma de Azure, aunque presenta una sólida documentación, su simulador cuántico, al no pertenecer al core de Azure, no tiene acceso de forma gratuita con la cuenta de estudiante.

### Líneas futuras

Una futura ampliación de este trabajo sería ampliar el conjunto de algoritmos evaluados, como puede ser el algoritmo de Shor, el QVM, entre otros.

Otra dirección de interés es la combinación de computación cuántica con computación clásica y cómo combinar un servicio de computación cuántica que puede estar en la nube de Azure y ser consumido por otro.

Asimismo, resulta relevante probar con hardware cuántico real y evaluar su rendimiento, pero tanto estas pruebas como generar un servicio que utilice computación cuántica en la nube requieren no solo una inversión de tiempo, sino también una inversión económica.

Por último, una interesante ampliación o un futuro proyecto enfocado en la criptografía sería la codificación y ejecución del algoritmo de Shor con alguno de los simuladores descritos anteriormente, con la idea de factorizar claves públicas. Dicha clave debe tener una longitud máxima de 15 bits, porque, como hemos descrito anteriormente, el máximo nivel de qubits es aproximadamente de 30 qubits, y en el algoritmo de Shor necesitas la mitad de ellos para hacer la medición parcial y provocar que el sistema colapse parcialmente al conjunto de números que forman el periodo. Una vez conseguido el periodo, el objetivo sería obtener $q$ y $p$, que conforman la clave, con el fin de obtener la clave privada y poder descifrar los mensajes que han sido cifrados con la clave pública.

## Herramientas y recursos

#### Introducción

Para poder replicar dicho trabajo en estas sección se muestra las herramientas empleadas. Los códigos que se han empleado están en el siguiente enlace <https://github.com/carlosGJAlcala/TFMCodigoDeDiferentesCuanticos> y para su ejecución se ha utilizado Jupyter el proceso de instalación viene en el repositorio de Git.

#### Simuladores cuánticos

- **Qiskit Aer**: Backend de simulación incluido en Qiskit que permite ejecutar circuitos cuánticos en CPU o GPU.

- **Cirq**: Framework de Google orientado a la construcción, simulación y análisis de circuitos cuánticos en Python.

- **QuEST**: Simulador cuántico de alto rendimiento en C/C++ con soporte para ejecución distribuida y en GPU, utilizado en investigaciones técnicas avanzadas.

#### Entornos de despliegue cuántico en la nube

- **IBM Quantum Experience**: Plataforma en la nube que permite ejecutar circuitos cuánticos reales o simulados mediante el framework Qiskit.

- **Microsoft Azure Quantum**: Servicio en la nube de Microsoft que permite acceder a simuladores cuánticos y, en ciertos casos, a hardware real mediante el lenguaje Q#.

#### Librerías y entornos de desarrollo

- **Python 3**: Lenguaje de programación utilizado para desarrollar circuitos cuánticos y realizar análisis numéricos.

- **Qiskit**: Framework de IBM para desarrollar algoritmos cuánticos y simular su comportamiento.

- **NumPy y Matplotlib**: Librerías utilizadas para operaciones matemáticas, procesamiento de resultados y visualización.

- **Jupyter Notebooks**: Entorno interactivo que permite combinar código, visualizaciones y explicaciones teóricas de forma integrada.

- **Q# y .NET SDK** (opcional): Herramientas necesarias para trabajar con Azure Quantum a bajo nivel.

#### Software auxiliar

- **LaTeX**: Sistema de composición de textos utilizado para redactar este documento técnico con estructura académica.

- **Visual Studio Code / PyCharm**: Editores de código empleados para programar en Python.

- **Git y GitHub**: Herramientas de control de versiones utilizadas para gestionar el código y documentación del proyecto.

## Referencias

AI, Google Quantum. 2025. “Cirq Concepts.” <https://quantumai.google/cirq/google/concepts>.

Alfaraz Delgado, Killyam. 2019. “Dispositivos Superconductores En Computación Cuántica.”

Alfonseca, Manuel. 2000. “La máquina de Turing.” *Recuperado El Agosto de 2016, de Www. Sinewton. Org/Numero/Nuemro/43-44/Articulo33. Pdf*.

Bonillo, Vicente Moret. 2013. “Principios Fundamentales de Computación Cuántica.” *Universidad de La Coruña*.

Brown, Kenneth R, John Chiaverini, Jeremy M Sage, and Hartmut Häffner. 2021. “Materials Challenges for Trapped-Ion Quantum Computers.” *Nature Reviews Materials* 6 (10): 892–905.

Castelvecchi, Davide. 2023. “IBM Releases First-Ever 1,000-Qubit Quantum Chip.” *Nature* 624 (7991): 238–38.

Castillo Gómez, Pedro del. 2024. “Implementación de Algoritmos Cuánticos Sobre Un Computador Cuántico Emulado Clásicamente.” Trabajo Fin de Máster, Máster Universitario en Ciberseguridad.

Chen, Samuel Yen-Chi, Chao-Han Huck Yang, Jun Qi, Pin-Yu Chen, Xiaoli Ma, and Hsi-Sheng Goan. 2020. “Variational Quantum Circuits for Deep Reinforcement Learning.” *IEEE Access* 8: 141007–24.

CUÁNTICA, COMPUTACIÓN, and JUAN JOSE LEMUS FLORES. n.d. “Instituto Tecnológico Superior Zacatecas Sur.”

Da Silva, Ricardo. 2014. “Los Teoremas de Incompletitud de gödel, Teorı́a de Conjuntos y El Programa de David Hilbert.” *Episteme* 34 (1): 19–40.

Departamento de Física, Universidad de Buenos Aires, Facultad de Ciencias Exactas y Naturales. 2020. “Ecuación de Schrödinger - Teorema de Ehrenfest - Límite Clásico - Corriente de Probabilidad.” <https://materias.df.uba.ar/f4aa2020c1/files/2020/04/clase_17_184.pdf>.

Deutsch, David. 1985. “Quantum Theory, the Church-Turing Principle and the Universal Quantum Computer.” *Proceedings of the Royal Society of London. Series A, Mathematical and Physical Sciences* 400 (1818): 97–117.

Dyakonov, M. I. 2019. “When Will We Have a Quantum Computer?” *arXiv Preprint arXiv:1903.10760*. <https://arxiv.org/abs/1903.10760>.

Feynman, Richard. 1982. “Simulating Physics with Computers.” *International Journal of Theoretical Physics* 21 (6/7): 467–88.

Garcı́a, Eduardo Gómez, and Karina Jiménez Garcı́a. n.d. “El <span class="nocase">á</span>tomo Que Se Sintió Electrón.”

IBM. 2025. “Qiskit \| IBM Quantum Computing.” <https://www.ibm.com/quantum/qiskit>.

Jones, Nicola. 2013. “The Quantum Company: D-Wave Is Pioneering a Novel Way of Making Quantum Computers–but It Is Also Courting Controversy.” *Nature* 498 (7454): 286–89.

Lloyd, Seth. 1996. “Universal Quantum Simulators.” *Science* 273 (5278): 1073–78.

Long, Gui-Lu. 2001. “Grover Algorithm with Zero Theoretical Failure Rate.” *Physical Review A* 64 (2): 022307.

Microsoft. 2025. “Computación Híbrida Con Azure Quantum.” <https://learn.microsoft.com/es-es/azure/quantum/hybrid-computing-overview>.

Microsoft Learn. 2025a. “Envío de Un Circuito Con Cirq a Azure Quantum.” <https://learn.microsoft.com/es-es/azure/quantum/quickstart-microsoft-cirq>.

———. 2025b. “Q# Overview - Azure Quantum.” <https://learn.microsoft.com/en-us/azure/quantum/qsharp-overview>.

———. 2025c. “¿Qué Es La Computación Cuántica? - Azure Quantum.” <https://learn.microsoft.com/es-es/azure/quantum/overview-understanding-quantum-computing>.

Monz, Thomas, Daniel Nigg, Esteban A Martinez, Matthias F Brandl, Philipp Schindler, Richard Rines, Shannon X Wang, Isaac L Chuang, and Rainer Blatt. 2016. “Realization of a Scalable Shor Algorithm.” *Science* 351 (6277): 1068–70.

Osaba, Eneko, Iñigo Perez-Delgado, Alejandro Mata-Ali, Pablo Miranda-Rodrı́guez, Aitor Moreno-Fdez-de-Leceta, and Luka Carmona-Rivas. 2025. “Computación Cuántica En Entornos Industriales:?‘ dónde Estamos y Hacia dónde Nos Dirigimos?” *DYNA-Ingenierı́a e Industria* 100 (3).

Pérez Romero, Mauricio Nicolas. 2025. “Quantum Approximate Optimization Algorithm (QAOA) for the Max-Cut Problem Using Bell and GHZ States.”

Qiu, Daowen, and Shenggen Zheng. 2018. “Generalized Deutsch-Jozsa Problem and the Optimal Quantum Algorithm.” *Physical Review A* 97 (6): 062331.

Quantiki. 2025. “List of QC Simulators.” <https://www.quantiki.org/wiki/list-qc-simulators>.

QuEST Project. 2025. “QuEST – Quantum Exact Simulation Toolkit.” <https://quest.qtechtheory.org/>.

Salcedo, LL. n.d. “INFORMACIÓn CUÁNTICA y APLICACIONES.”

Schumacher, Benjamin. 1995. “Quantum Coding.” *Physical Review A* 51 (4): 2738.

Tilly, Jules, Hongxiang Chen, Shuxiang Cao, Dario Picozzi, Kanav Setia, Ying Li, Edward Grant, et al. 2022. “The Variational Quantum Eigensolver: A Review of Methods and Best Practices.” *Physics Reports* 986: 1–128.

Viveros, Ismael Mena. n.d. “Computación Cuántica.”

Wikipedia. 2024a. “Algoritmo Cuántico — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Algoritmo_cu%C3%A1ntico&oldid=163641747>.

———. 2024b. “BQP — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=BQP&oldid=160558747>.

———. 2024c. “Espacio de Hilbert — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Espacio_de_Hilbert&oldid=160625440>.

———. 2024d. “Puerta Cuántica — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Puerta_cu%C3%A1ntica&oldid=162710799>.

———. 2025a. “Ecuación de Schrödinger — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Ecuaci%C3%B3n_de_Schr%C3%B6dinger&oldid=168264945>.

———. 2025b. “Silogismo — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Silogismo&oldid=168842042>.

———. 2025c. “Teoría de Variables Ocultas — Wikipedia, La Enciclopedia Libre.” <https://es.wikipedia.org/w/index.php?title=Teor%C3%ADa_de_variables_ocultas&oldid=165138110>.

Wikipedia contributors. 2024. “Gottesman–Knill Theorem — Wikipedia, the Free Encyclopedia.” <https://en.wikipedia.org/w/index.php?title=Gottesman%E2%80%93Knill_theorem&oldid=1259719545>.

———. 2025a. “Quantum Computing — Wikipedia, the Free Encyclopedia.” <https://en.wikipedia.org/w/index.php?title=Quantum_computing&oldid=1299711743>.

———. 2025b. “Quantum Turing Machine — Wikipedia, the Free Encyclopedia.” <https://en.wikipedia.org/w/index.php?title=Quantum_Turing_machine&oldid=1269667421>.
