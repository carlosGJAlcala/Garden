---
title: "Algoritmos genéticos"
---

# 11. Algoritmos Genéticos

Aprendizaje Evolutivo y Algoritmos Genéticos  
Prof. Ignacio Olmeda  
AI LAB

## Introducción histórica

Canon (1932) fue probablemente el primero en entender la evolución como un mecanismo de aprendizaje completamente diferente al que realizan los individuos, que se basa principalmente en ensayo y error.

Obsérvese que los humanos somos capaces de aprender porque, de hecho, pertenecemos a una clase de "máquinas de computación" capaces de hacerlo, y esta capacidad es simplemente el resultado de la evolución.

Turing (1950) también señaló la conexión obvia entre el aprendizaje automático y la evolución, vislumbrando el uso de principios evolutivos en la construcción de máquinas pensantes.

Los algoritmos evolutivos son una forma poderosa y alternativa de entender el aprendizaje, ofrecen una alternativa donde técnicas clásicas como el descenso de gradiente o la búsqueda puramente aleatoria han demostrado ser insatisfactorias.

## Concepto básico de Algoritmos Genéticos

Los Algoritmos Genéticos (AG) son técnicas de búsqueda heurística basadas en los principios de la evolución natural que fueron enunciados por Darwin en *El Origen de las Especies* en 1859.

Según estos principios, la selección natural establece un vínculo entre el rendimiento de los seres vivos y los cromosomas que codifican su información genética.

El proceso de selección natural tiene como resultado que los cromosomas que codifican características exitosas se reproduzcan más frecuentemente que aquellos que no lo hacen.

Los AG fueron propuestos por primera vez por Holland en 1962, pero solo después de 1975, con la publicación de su libro *Adaptation in Natural and Artificial Systems*, se hicieron relativamente populares.

Otras propuestas como la Programación Evolutiva (Fogel et al., 1966), Estrategias Evolutivas (Rechenberg, 1971; Schwefel, 1974) o, más recientemente, Programación Genética (Koza, 1992) comparten ideas similares consistentes en aplicar principios evolutivos a la solución de problemas generales.

De manera similar a otras técnicas de aprendizaje automático como las Redes Neuronales Artificiales, los AG son simplemente abstracciones algorítmicas con poca o ninguna relación con los procesos reales que emulan.

## Características distintivas de los AG

Nótese que en todos los algoritmos vistos previamente, la modificación de la solución se realiza directamente.

Al contrario, la evolución es un proceso biológico que actúa sobre los cromosomas en lugar de su expresión biológica (el ser vivo que codifican).

En contraste, los AG operan sobre versiones codificadas de las soluciones. Esta es una característica fundamental de los AG, una de sus fortalezas pero también una de sus limitaciones.

De hecho, dado que la codificación es tan importante, el rendimiento del algoritmo depende fuertemente de encontrar una codificación que facilite los procedimientos de búsqueda.

La codificación, según algunos practicantes, es más un arte que una ciencia, y puede revelar o destruir el poder de los AG.

Otra característica distintiva importante de los AG frente a procedimientos más "clásicos" es que los AG son inherentemente paralelos.

La mayoría de los algoritmos intentan encontrar versiones mejoradas de una solución inicial, mientras que los AG buscan un conjunto completo de mejores soluciones.

En este sentido, los AG implementan no solo una búsqueda en profundidad sino también una búsqueda en amplitud.

Para los AG no es esencial encontrar, en alguna iteración, una solución mejor que la anterior, sino encontrar un conjunto de soluciones que, globalmente, sean mejores que las anteriores.

## Características matemáticas de los AG

Los AG caen dentro de la clase de algoritmos heurísticos; aunque existen algunos resultados de convergencia, no puede demostrarse generalmente que converjan al óptimo global (o incluso local).

Sin embargo, han demostrado su flexibilidad y potencia en muchas aplicaciones que van desde Finanzas hasta Electrónica.

Los AG también son robustos y aceptan análisis post-optimalidad de una manera natural: cuando la función objetivo cambia, partes significativas de los algoritmos son reutilizables, en contraste con otros métodos que requieren una reescritura completa de los procedimientos y código.

Finalmente, como veremos, los AG son no determinísticos sino estocásticos, es decir, cada vez que se ejecutan en un problema particular pueden proporcionar diferentes soluciones.

## Operadores básicos de los AG

En su forma más básica, los AG emplean tres operadores: Selección, Cruce (Crossover) y Mutación.

Estos operadores imitan los que se encuentran en Genética, que es también la fuente de muchos otros operadores como diploidismo, parasitismo, elitismo, etc.

Los AG son conceptualmente muy simples y se pueden explicar mejor con un ejemplo simple tomado de Goldberg (1996).

En lo que sigue, asumamos que queremos resolver el siguiente problema trivial:

$$\text{Maximizar } x^2$$
$$\text{s.a. } x = 1, 2, 3, 4, ..., 32$$

### Función de aptitud inicial

El algoritmo comienza tomando una población inicial de soluciones candidatas, por ejemplo: {1, 3, 8, 5}. Estas soluciones pueden obtenerse por muestreo aleatorio del espacio de valores viables.

Cada individuo en esta población inicial y subsecuentes se evalúa según una función de aptitud (fitness) que representa qué tan bien la solución resuelve el problema, qué tan bien se adapta el "individuo" al "ambiente".

Las funciones de aptitud no necesitan ser iguales a la función objetivo a resolver, pero por simplicidad, asumiremos tal caso.

Nótese entonces que la aptitud de cada uno de los individuos en la población inicial es:

$$F(1) = 1^2 = 1, \quad F(3) = 3^2 = 9, \quad F(8) = 8^2 = 64, \quad F(5) = 5^2 = 25$$

Una característica importante de los AG es que emplean únicamente información que proviene de la función de aptitud, es decir, los AG no emplean ninguna propiedad funcional de la función objetivo, como si la función es continua, derivable, etc.

Esta es una característica muy poderosa de los AG en situaciones donde el rendimiento puede medirse pero no hay "pista" de la estructura específica de la función objetivo.

Por ejemplo, podemos conocer las valoraciones de productos de algunos consumidores pero no sabemos realmente qué funciones emplean para calificarlos o incluso qué características de los productos se toman en cuenta.

### Genotipo y fenotipo

La función de aptitud se evalúa sobre el fenotipo del individuo, que son simplemente las características observables o rasgos del individuo (p. ej., la altura en humanos).

La Genética tiene que ver principalmente con el genotipo, es decir, la forma en que el espécimen está codificado genéticamente.

El genotipo es el factor más importante para determinar el fenotipo, es decir, la mayoría de la apariencia del individuo depende de su codificación genética.

El genoma humano está codificado en un alfabeto que emplea cuatro bases químicas: Adenina (A), Timina (T), Guanina (G) y Citosina (C).

### Codificación binaria

Volviendo a la descripción de un AG básico, en Algorítmica es muy común usar el alfabeto binario. Hay muchas formas de codificar cualquier información, y en particular, números en código binario. Para nuestro ejemplo, basta considerar la descomposición del número en potencias de 2 y luego usar la función indicadora de la potencia correspondiente:

$$x = \sum_{i=0}^{n} a_i 2^i, \quad a_i \in \{0, 1\}$$

Ejemplos:

- $8 = 0 \times 2^5 + 0 \times 2^4 + 1 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 0 \times 2^0 \approx 001000$
- $5 = 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 \approx 000101$
- $3 = 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 0 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 \approx 000011$
- $1 = 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 \approx 000001$

El proceso de transformar el fenotipo en genotipo se llama **codificación**.

### Importancia de la codificación

En muchas situaciones, porciones del individuo codificado supuestamente encapsulan características que son importantes para resolver una tarea particular. Por ejemplo, podríamos pensar que algunas variables de la función objetivo deberían tener algún valor particular para que la solución codificada sea una cadena específica.

No solo eso, nótese que la versión codificada debe representar correctamente la epistasis, es decir, cuando ocurre alguna cadena particular en la versión codificada del individuo, entonces otra cadena particular debería también ocurrir, de modo que modificar cualquiera de las cadenas tenga que ser seguido por la modificación de la otra.

Solo de esta manera aseguramos que la versión decodificada tenga alguna interpretación. Por ejemplo, cuando una variable es igual a cero, otra también debería ser igual a cero.

La necesidad de que la codificación conserve el "significado" de las versiones decodificadas hace que la codificación sea extremadamente importante en la aplicación de AG.

## Operador de selección

El primer operador de los AG se llama selección. En la selección, los individuos mejor adaptados al ambiente (con los valores más altos de sus funciones de aptitud) tienen una probabilidad más alta de "sobrevivir" y de transmitir su información genética a sus descendientes.

En los AG este procedimiento se implementa calculando una probabilidad para cada uno de los individuos dependiendo de su aptitud correspondiente, de modo que una aptitud más alta corresponde a una probabilidad más alta.

Una forma trivial es dividir la aptitud del individuo por la suma de aptitudes de la población de n individuos:

$$p(\text{individuo } i) = \frac{F(\text{individuo } i)}{\sum_{i=1}^{n} F(\text{individuo } i)}$$

Nótese que en algunos contextos sería necesaria alguna transformación de la función de aptitud para proporcionar valores positivos.

Obsérvese también que la función anterior cumple los requisitos para ser una probabilidad, ya que es positiva, acotada y suma uno.

Esta implementación precedente de la selección se llama **selección por ruleta** (roulette wheel selection) y, como veremos, hay posibles modificaciones a este esquema.

### Ejemplo de selección por ruleta

En nuestro ejemplo:

$$\sum_{i=1}^{n} F(\text{individuo } i) = 1 + 9 + 64 + 25 = 99$$

Así:

- $p(1) \approx 1\% \quad p(3) \approx 9\% \quad p(8) \approx 65\% \quad p(5) \approx 25\%$

Ahora, el mecanismo de selección implica muestreo aleatorio de la distribución de probabilidad anterior para seleccionar individuos que se reproduzcan.

Asumamos que seleccionamos dos "padres" de la distribución anterior mediante muestreo dos veces.

Ejemplo: "Madre" 8 (65%) ≈ 001000, "Padre" 3 (9%) ≈ 000011

## Operador de cruce

El siguiente operador básico de los AG es el cruce (crossover, también llamado recombinación). Consiste en el intercambio de información genética entre la "madre" y el "padre".

Para hacer esto primero seleccionamos un punto de cruce aleatorio que servirá para dividir la cadena codificada y luego intercambiamos las subcadenas de padre y madre para crear un nuevo individuo.

Ejemplo:

- "Madre" (8) ≈ 001000
- "Padre" (3) ≈ 000011
- "Descendencia" ≈ 001011 (11 decodificado)

## Operador de mutación

El último operador básico es la mutación, consiste en cambiar aleatoriamente una de las posiciones de la secuencia genética de la descendencia.

Ejemplo:

- Antes de la mutación: ≈ 001011
- Después de la mutación: ≈ 001111

La mutación se realiza usando una probabilidad extremadamente baja, de lo contrario toda la estructura creada por los AG sería destruida y el procedimiento sería equivalente a una búsqueda aleatoria.

Nótese también que la mutación es esencial para evitar que las poblaciones se "atasquen" (no se puedan crear nuevas descendencias), por ejemplo:

{001000, 001000, 001000, ..., 001000}

Con mutación: ≈ 001001

## Iteración generacional

Nótese que la selección, cruce y mutación pueden aplicarse para crear una generación completa de descendencias y no solo una.

Cuando hacemos eso, podemos reemplazar la "vieja" generación de individuos por una "nueva", que, esperemos, exhibirá un comportamiento mejor.

Nótese que, de hecho, la mejor solución de la nueva "generación" no es necesariamente mejor que la anterior, simplemente requerimos que, en general, la población completa sea mejor.

## Algoritmo GA básico

Todos los pasos mencionados se repetirán hasta que el algoritmo proporcione alguna solución con el nivel de calidad deseado o hasta que las mejoras en la función objetivo no sean significativas.

Un algoritmo AG se ejecutaría así:

- **Paso 1:** Generar una población inicial aleatoria
- **Paso 2:** Codificar las soluciones
- **Paso 3:** Evaluar la aptitud de cada uno de los individuos; detener si se alcanza optimalidad
- **Paso 4:** Realizar selección
- **Paso 5:** Realizar cruce
- **Paso 6:** Realizar mutación
- **Paso 7:** Ir al paso 3

### Tabla de correspondencia: Conceptos biológicos y AG

| Concepto Biológico | Algoritmo de Optimización |
|---|---|
| Aptitud (Fitness) | Función Objetivo |
| Individuo | Solución |
| Generación | Iteración |
| Fenotipo | Solución Decodificada |
| Genotipo | Solución Codificada |
| Gen | Cadena Binaria |

## Modificaciones del algoritmo básico

Muchos investigadores y practicantes han sugerido un número considerable de modificaciones del AG básico para tratar problemas generales o para adaptarse a aplicaciones particulares.

Entre estas variaciones podemos mencionar nuevos operadores, nuevas formas de codificación y nuevas formas de selección.

### Operador de inversión

Con respecto a otros operadores, uno de los primeros propuestos fue la Inversión, introducida por Holland (1975) en su descripción fundamental de los AG. Simplemente consiste en reemplazar una subcadena en un cromosoma por su versión "espejo", es decir:

- Antes de la inversión: 011100101000
- Después de la inversión: 011110001000

### Cruce uniforme

El cruce uniforme intenta evitar que las características beneficiosas de los "padres" sean destruidas por el cruce, particularmente cuando tales características están codificadas en una cadena larga, lo que aumenta la probabilidad de ser destruidas.

El cruce uniforme consiste en decidir aleatoriamente qué padre contribuirá con cada bit particular a la descendencia. Asumamos que definimos una "plantilla" que asigna qué bits pertenecen a qué padre. El cruce uniforme funciona así:

- Madre (1): 10010101000101
- Padre (0): 11100011011111
- Plantilla: 11011000111000
- Descendencia: 10110011000111

### Cruce multipunto

El cruce multipunto consiste en seleccionar dos o más puntos para intercambiar las subcadenas de los individuos padres. Esto evita el problema de que, de lo contrario, las posiciones al comienzo o final de alguna cadena siempre sean destruidas.

Ejemplo con cruce de un punto:

- "Madre" (8) ≈ 001000
- "Padre" (3) ≈ 100011
- "Descendencia 1": ≈ 001011 (extremo destruido)
- "Descendencia 2": ≈ 100000 (comienzo destruido)

Por ejemplo, usando cruce de dos puntos, donde solo la subcadena entre los dos puntos de corte se intercambia, se producirá:

- "Madre" (8) ≈ 001000
- "Padre" (3) ≈ 100011
- "Descendencia 1" ≈ 001000 (comienzo y extremo de la madre conservados)
- "Descendencia 2" ≈ 101011 (comienzo y extremo del padre conservados)

### Variaciones en selección: Selección elitista

Con respecto a la selección, se han propuesto varias variaciones. Una de las más ampliamente empleadas es la selección elitista, que consiste en elegir solo las mejores descendencias en una iteración particular.

Las descendencias se ordenan según sus funciones de aptitud y un número fijo o variable de las más aptas se eligen para reemplazar a los peores individuos en la generación anterior.

Nótese que la selección elitista asegura monotonicidad en el proceso de optimización, ya que el mejor individuo de una iteración particular es al menos tan bueno como el de la anterior.

### Variaciones en selección: Selección por umbral

Otra alternativa es la selección por umbral (cutoff selection), cuando solo se seleccionan individuos que muestran alguna mejora o cuya función de aptitud está por encima de cierto punto de corte.

### Algoritmos híbridos

Los algoritmos híbridos consisten en combinar otros algoritmos que pueden funcionar bien en una situación particular con AG.

Un ejemplo podría ser una combinación de métodos basados en gradiente y AG. Podría emplearse un algoritmo basado en gradiente en algunas iteraciones hasta que falla en producir una solución mejorada. Entonces, podríamos cambiar a un AG para explorar otras cuencas de atracción donde, nuevamente, el algoritmo basado en gradiente podría usarse.

## Otros algoritmos evolutivos

### Estrategias Evolutivas

Las Estrategias Evolutivas (originalmente *evolutionsstrategie*, en alemán; y de aquí en adelante ES) revisitan las ideas de Darwin (1859) para quien la selección y la mutación fueron los operadores genéticos más importantes (Schwefel, 1995).

Nótese que la selección y la mutación sirven propósitos diferentes y de algún modo antagónicos: "la selección explota la información de aptitud para guiar la búsqueda hacia regiones del espacio de búsqueda prometedoras, mientras que la variación (mutación) explora el espacio de búsqueda" (Beyer y Schwefel, 2002).

### Características de ES

En ES no hay diferencia entre el fenotipo y el genotipo, por lo que las descendencias se generan directamente del individuo padre sin la intervención de ninguna codificación.

Otra diferencia importante es que la reproducción opera usando un individuo (asexualmente), de modo que las descendencias son simplemente variaciones de la solución padre.

En cierto sentido, podemos pensar en ES como una forma de autoadaptación.

Hay varias versiones de ES en su formulación básica llamadas (1,λ), (μ,λ) y (μ+λ).

### Estrategia (1,λ)

En la estrategia (1,λ), un individuo genera λ descendencias simplemente generando individuos en la vecindad de la solución padre.

Asumamos que x es la solución padre, la descendencia puede generarse como $x' = x + \varepsilon$, donde ε es una perturbación aleatoria de x (que, obviamente, puede ser multivariante, según la dimensión de x).

Por ejemplo, asumamos que x es un vector N-dimensional de características:

$$x = (x_1, x_2, \ldots, x_N)$$

Entonces, la descendencia i puede generarse por muestreo aleatorio de una distribución normal multivariante con media cero y matriz de covarianza Σ:

$$x'_i = x_i + \varepsilon_i, \quad \varepsilon_i \sim N(0, \Sigma)$$

Cuando las características son independientes, entonces Σ podría ser diagonal.

### Convergencia de ES

Nótese que las ES son alguna variación de búsqueda aleatoria, pero introducen ideas novedosas que aumentan el poder de la búsqueda aleatoria no informada.

Después de que se crean las descendencias, su función de aptitud se evalúa y se elige la mejor solución entre los candidatos.

El algoritmo entonces itera hasta que se alcanza convergencia:

$$||x_{\text{iteración}(i)} - x_{\text{iteración}(i-1)}|| \leq \eta$$

o se cumple algún criterio de parada, por ejemplo:

$$\text{fitness} - x_{\text{iteración}(i)} \geq \tau$$

### Modificación adaptativa: Regla 1/5

Una de las ideas novedosas de ES es modificar el factor aleatorio de acuerdo con algunos criterios, así como introducir algún "sesgo" en los parámetros de la distribución (la media y la varianza de la característica, en el caso gaussiano).

Pueden encontrarse pruebas de convergencia de ES (sin recombinación) con solo supuestos leves en la función objetivo (p. ej., Rudolph, 1997) y esto ha atraído interés desde sectores más "formales".

Desde el punto de vista práctico, estas (y otras) técnicas heurísticas pueden emplearse como una alternativa cuando no existen algoritmos eficientes o incluso conocidos.

Con respecto a esto, Schwefel (1995) propuso usar la **regla 1/5 de éxito**, que consiste en aumentar o reducir la varianza del factor aleatorio dependiendo de si las mutaciones exitosas son demasiado exitosas o demasiado inefectivas. La regla 1/5 es:

$$\sigma_t = \begin{cases}
\alpha \sigma_{t-1}, & \text{si } p > 1/5 \\
(1/\alpha) \sigma_{t-1}, & \text{si } p < 1/5 \\
\sigma_{t-1}, & \text{si } p = 1/5
\end{cases}$$

donde α es una constante. Schwefel sugiere $\alpha = 0.85^{1/n}$ donde n es la dimensión de x.

Aunque esta regla es puramente heurística, ha demostrado ser extremadamente efectiva en lograr una tasa óptima para aproximar el óptimo.

### Estrategias (μ,λ) y (μ+λ)

La estrategia evolutiva simple (1,λ) puede extenderse para introducir competencia entre individuos intentando aumentar la eficiencia del algoritmo.

En ES (μ,λ), μ padres generan λ descendencias, donde λ puede ser igual a μ o no. Por ejemplo, una opción trivial podría ser λ=μ donde un padre simplemente genera una descendencia, mientras que la mayoría de las veces sea λ > μ.

Después de que se generan las λ descendencias, solo se seleccionan los μ individuos con el mejor rendimiento, manteniendo el tamaño de la población constante en cada una de las iteraciones.

En ES (μ+λ) (Rechenberg, 1973), los padres y las descendencias compiten para formar parte de la siguiente generación.

Nótese que tanto las ES (μ,λ) como (μ+λ) pueden añadir potencia extra debido a la posibilidad de procesamiento paralelo.

### Variantes de ES: Meta-ES

Similar a los AG, las ES tienen un número de variantes y mejoras, muchas de ellas tienen que ver con la modificación de la perturbación aleatoria.

Cuando no solo se permite que los individuos sino también parámetros que determinan mutaciones se "adapten", hablamos de meta-ES.

Nótese que, de hecho, la regla 1/5 es simplemente una forma de estrategia meta-evolutiva. Otros ejemplos podrían ser:

$$\sigma_t^{(i)} = \sigma_{t-1}^{(i)} \xi_i, \quad \xi_i \sim N(0, 1)$$

O CMA-ES, que proviene de Adaptación de Matriz de Covarianza (Covariance Matrix Adaptation).

### Recombinación en ES

Otra variante importante de ES es incorporar recombinación.

Nótese que, en este caso, la recombinación opera directamente en las soluciones y no en una versión codificada como en los AG.

La recombinación en ES funciona así: asumamos que tenemos dos soluciones alternativas x, y. Podemos pensar en varias formas de combinarlas, entre muchas:

$$z_i = \begin{cases}
\dfrac{x_i + y_i}{2} \\
x_i \text{ o } y_i \\
\dfrac{|x_i| + |y_i|}{2} (x_i, y_i) = f(i)
\end{cases}$$

### Programación Evolutiva

La Programación Evolutiva (PE), fue introducida por Fogel (1962) para idear máquinas de estados finitos que pudieran realizar ciertas operaciones.

En una máquina de estados finitos, se introduce algún símbolo de entrada en la máquina, que cambia su estado interno y produce algún símbolo de salida. Por ejemplo, considere la máquina y asuma que introducimos el símbolo 0:

- Estado presente: C B C A A B
- Símbolo de entrada (0): 1 1 1 0 1
- Siguiente estado: B C A A B C
- Símbolo de salida (β o α o γ): β α γ β β α

*(fragmento no reconstruible con confianza: diagrama de máquina de estados finitos no renderizado)*

Las máquinas de estados finitos pueden usarse para aprender la lógica de una secuencia de símbolos observados. Una máquina de estados finitos "correcta" sería capaz de predecir correctamente el siguiente símbolo en la secuencia.

Asumamos que otorgamos un punto a la máquina de estados finitos que predice correctamente el siguiente símbolo en la secuencia y que no se otorgan puntos si el símbolo se predice incorrectamente.

Fogel et al. (1966) usaron cinco máquinas de estados finitos como población inicial, cada una con cinco estados.

Cada máquina generaba una única descendencia mediante mutación simple, con probabilidades iguales de: (1) añadir un estado, (2) eliminar un estado, (3) cambiar el estado inicial, (4) cambiar un símbolo de salida, o (5) cambiar una transición de siguiente estado.

### Selección y evaluación en PE

Los padres y descendencias fueron evaluados según qué tan bien se ajustaban a la secuencia observada de símbolos. La mutación y selección se realizaron antes de que la mejor máquina de estados finitos en la población se usara para predecir el siguiente símbolo, aún no observado.

La PE ha evolucionado desde tal formalización y ahora se emplea como un marco de optimización general.

La PE carece completamente del operador de recombinación. El cálculo de la aptitud y los operadores de selección y mutación son diferentes a los de los AG así como de las ES.

En primer lugar, la aptitud $F(x_i)$ se obtiene de los valores de la función objetivo escalándolos a valores positivos, y es posiblemente modificada añadiendo un factor aleatorio $\nu_i$.

### Mutación en PE

Las descendencias se obtienen de la mutación mediante muestreo aleatorio de una distribución normal multivariante diagonal con una varianza que depende de la función de aptitud:

$$x'_i = x_i + \sigma_i z_i, \quad z_i \sim N(0, 1)$$

$$\sigma_i = \beta F(x_i) + \gamma_i$$

Las mutaciones apropiadas para el problema en cuestión se obtienen ajustando los parámetros β y γ_i.

La selección se realiza mediante selección por torneo-q, que funciona así: para cada individuo, q individuos que compiten se seleccionan mediante muestreo aleatorio de la población de padres y descendencias. Luego, la función de aptitud del individuo se compara con la de los competidores y se cuenta el número de veces que es mejor.

### Finalización de PE

Finalmente, los 2μ individuos se ordenan en orden descendente y se seleccionan los μ individuos con los valores más altos para formar la siguiente población.

El algoritmo PE estándar impone algunas dificultades al usuario cuando se seleccionan los parámetros β y γ_i, particularmente en el caso de funciones objetivo de dimensionalidad arbitrariamente alta.

Para superar esto, Fogel (1992) propuso una modificación llamada meta-PE que autoadapta n varianzas de la misma manera que ES.

$$x'_i = x_i + \sigma'_i z_i$$

$$\sigma'^2_i = \sigma^2_i + \xi \sigma_i$$

$$z \sim N(0, 1)$$

### Meta-PE con correlaciones: R-metaEP

Además de autoadaptar desviaciones estándar, Fogel (1992) también propuso la R-metaEP, que considera el vector completo de n coeficientes de correlación:

$$\rho_{ij} = \frac{\sigma_{ij}}{\sigma_i \sigma_j}$$

muy similar a un procedimiento llamado mutaciones correlacionadas en ES.

De manera similar a ES, también existen teoremas de convergencia de PE suponiendo algunas restricciones.

### Programación Genética

La Programación Genética (PG), fue propuesta por Koza (1989) como un algoritmo evolutivo para crear programas de computadora ejecutables.

La Programación Genética consiste en una búsqueda dirigida por evolución de programas de computadora seleccionando aquellos que, cuando se ejecutan, proporcionan las mejores funciones de aptitud.

La idea es muy simple pero muy poderosa. Primero, hay que entender que los programas de computadora pueden representarse en estructuras de árbol que se evalúan recursivamente para producir las expresiones multivariantes resultantes.

Un ejemplo de estos tipos de representaciones son las expresiones S en lenguaje LISP, por ejemplo: `(- (+ 5 4) 9)`, que devuelve 0. LISP fue muy comúnmente usado para soportar PG, pero ahora muchos otros lenguajes como Python, Java y C++ han sido empleados para desarrollar aplicaciones de PG basadas en árboles.

### Representación en árbol

Por ejemplo, la función $\max(x^2, x + 3y)$ como expresión S puede escribirse como:

```
(max (* x x) (+ x (* 3 y)))
```

y puede representarse como:

```
       max
      /   \
     *     +
    / \   / \
   x   x x   *
          / \
         3   y
```

### Cruce en PG

Entonces, podemos aplicar una clase particular de cruce consistente en simplemente elegir diferentes subárboles de dos árboles completos e intercambiarlos para crear un nuevo árbol.

*(fragmento no reconstruible con confianza: diagrama de cruce de árboles no renderizado, muestra comparación antes/después con nodos max, min, +, - y variables x, y)*

### Mutación en PG

La mutación podría consistir en seleccionar un subárbol y reemplazarlo por un árbol completamente aleatorio.

Por supuesto, muchas mutaciones así como operaciones de cruce resultarán en programas de computadora no efectivos o incluso no viables, pero parte de ellos, de hecho, se ejecutarían y realizarían nuevos cálculos no considerados previamente.
