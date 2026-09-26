---
title: "Problemas en la construcción de modelos de IA"
---

# Problemas en la Construcción de Modelos de Aprendizaje Automático

Profesor Ignacio Olmeda 
AI LAB

## Sesgo y Varianza

Como hemos visto, los modelos pueden tener muchas parametrizaciones diferentes y variarán en lo bien que se ajusten a los datos.

Por ejemplo, en el siguiente ejemplo, dejemos que los puntos azules representen los datos de entrenamiento y los verdes los datos de prueba.

[Gráfico X-Y](diagrama)

Supongamos que ajustamos un modelo lineal minimizando la distancia cuadrada a los puntos azules.

El modelo lineal no podrá capturar exactamente la relación entre X e Y en los datos de entrenamiento porque no todos los datos caen a lo largo de una línea: la relación podría ser no lineal o estar afectada por ruido.

$$Y = f(X), \quad f \text{ no lineal} \quad \neq \alpha + \beta X$$$

$$Y = \alpha + \beta X + \varepsilon$$
Ahora supongamos que utilizamos un modelo no lineal/no paramétrico que, con suficiente complejidad, podría aproximar perfectamente los puntos de datos.

![Curva ajustada sin error](diagram)

La curva pasa exactamente sobre los datos de entrenamiento.

Obviamente, podemos concluir que el segundo modelo (no paramétrico) es mejor en el conjunto de datos de entrenamiento que el primero (lineal).

El segundo modelo es capaz de ajustar los datos de entrenamiento porque es más flexible; puede representar exactamente los datos de entrenamiento. Se dice que tiene un **sesgo bajo**.

El primer modelo tiene muchas restricciones en la forma de su función, lo que lo hace incapaz de capturar los datos de entrenamiento. Tiene un **sesgo alto**.

En términos intuitivos, podemos considerar el sesgo como una **sobresimplificación** de relación oculta entre X e Y.

Nótese que el sesgo es fácilmente evitable: simplemente podemos aumentar la complejidad del modelo para reducirlo. Sin embargo, esto tendrá consecuencias, como veremos ahora.

Ahora centrémonos en el conjunto de datos de prueba. En el primer modelo tenemos:

![Error en prueba - modelo lineal](diagram)

Y en el segundo:

![Error en prueba - modelo no paramétrico](diagram)

Nótese que los errores en el conjunto de prueba son mayores para el segundo modelo que para el primero.

Debemos concluir que, aunque sea más simple, ¡el primer modelo es mejor en el conjunto de prueba!

Cuando usamos los mismos modelos en datos nuevos, la aparente flexibilidad del segundo modelo —más complejo— se convierte en una desventaja: es perfecto para los datos de entrenamiento, pero esto lo hace imperfecto para los datos de prueba.

Cuando un modelo exhibe una gran diferencia entre los datos y la predicción en datos nuevos, se dice que tiene una **varianza alta**.

En contraste, el primer modelo hizo pocas suposiciones sobre los datos; es “igualmente simple” en los conjuntos de entrenamiento y prueba, lo que le permite ajustarse mejor al conjunto de prueba. Tiene una **varianza baja**.

### Resumen: El Dilema Sesgo-Varianza

- Primer modelo: sesgo alto & varianza baja
- Segundo modelo: sesgo bajo & varianza alta

Esto se conoce como el **dilema sesgo-varianza**: los modelos flexibles tienen un sesgo más bajo pero una varianza más alta que los modelos más rígidos.

Este dilema es inevitable: es imposible tener modelos con sesgo bajo y también con varianza baja. Hay un **compromiso** entre estas dos.

Un buen modelo es aquel que tiene una buena relación sesgo/varianza: captura correctamente la relación en los datos de entrenamiento y permite hacer predicciones correctas en los datos de prueba.

*(Diagrama: Error vs. Complejidad del modelo, mostrando Sesgo, Varianza y Error total)*

El dilema sesgo-varianza es uno de los aspectos más importantes a tener en cuenta al construir modelos bajo el paradigma no paramétrico del Aprendizaje Automático.

No se debe ser tentado por modelos complejos que proporcionan una explicación “perfecta” del pasado porque estos modelos, la mayoría de las veces, proporcionarán malas predicciones.

Por supuesto, los modelos que son malos al capturar relaciones en los datos de entrenamiento continuarán siendo malos para hacer predicciones.

Los buenos modelos representan los datos de entrenamiento pero no los sobre-representan.

### Descomposición del Error

El error de cualquier modelo puede descomponerse en términos de los conceptos de sesgo y varianza que acabamos de ver. Omitiendo los detalles matemáticos, puede demostrarse que para cualquier modelo:

$$\text{Error} = (\text{Sesgo}^2 + \text{Varianza}) + \text{Error irreductible (o inevitable)}$$

La expresión anterior nos dice que hay dos tipos de errores:

- **Error del modelo** (errores de sesgo + varianza): debido al uso de un modelo inapropiado y que puede reducirse eligiendo correctamente el modelo adecuado.
- **Error inevitable**: debido a la relación estocástica entre variables de entrada y salida, y que no puede reducirse independientemente de elección del modelo.

## Underfiting y Overfitting

El dilema sesgo-varianza es una consecuencia directa de relación no perfecta (estocástica) entre variables explicativas y explicadas.

$$Y = f(X tención \theta) + \varepsilon$$

Necesitamos modelos con suficiente flexibilidad para ajustar la relación que vincula las variables, pero sería inútil intentar ajustar el componente aleatorio porque, por definición, es aleatorio y por lo tanto impredecible.

Cuando el modelo es demasiado flexible, actúa como una “base de datos” que simplemente “recuerda” los datos de entrenamiento.

Nótese que los datos de entrenamiento incluyen un componente aleatorio que no va a ocurrir en el futuro, por lo que es inútil “recordarlo”.

### Ejemplo Numérico

Supongamos que la verdadera relación es:

$$Y = 2X + \varepsilon$$

Si tuviéramos la siguiente base de datos:

| X (verdadero) | Y (observado) | $\varepsilon$ |
|---|---|---|
| 2 | 3.6 | 0.40 |
| 1 | 1.8 | 0.20 |
| 3 | 6.6 | 0.60 |
| 0 | 0.3 | 0.30 |
| 2 | 3.7 | 0.30 |
| 4 | 8.2 | 0.20 |

No estaríamos interesados en “aprender” el componente aleatorio $\varepsilon$ porque en otro ejemplo podríamos tener:

| X (verdadero) | Y (observado) | $\varepsilon$ |
|---|---|---|
| 2 | 4.3 | 0.30 |
| 1 | 2.1 | 0.10 |
| 3 | 6.3 | 0.30 |
| 0 | 0.2 | 0.20 |
| 2 | 3.6 | 0.40 |
| 4 | 7.6 | 0.40 |

El componente aleatorio no nos dice nada sobre la verdadera relación entre X e Y.

Si empleamos un modelo demasiado complejo de modo que represente exactamente los datos de entrenamiento, lo estamos forzando a “recordar” factores aleatorios que serán inútiles para la predicción.

Estamos haciendo **overfitting** de los datos; deberíamos haber empleado un modelo más simple.

*(Diagrama: Relación verdadera vs. Relación ajustada con sobreajuste)*

Alternativamente, el modelo empleado puede ser demasiado simple, lo que lo hace fallar al capturar la relación entre Y e X.

Por ejemplo, podríamos proponer un modelo trivial:

$$Y = \alpha$$$

*(Diagrama: Relación verdadera vs. Relación ajustada con subajuste)*

Estamos haciendo **underfitting** de los datos; es decir, deberíamos haber empleado un modelo más complejo.

### Síntesis

- Los modelos que hacen underfitting de los datos de entrenamiento tendrán un pobre desempeño en los datos de prueba: son “demasiado simples”.
- Los modelos que hacen overfitting de los datos de entrenamiento tendrán un pobre desempeño en los datos de prueba: son “demasiado complejos”.
- Habrá un modelo con una complejidad óptima, ni demasiado simple ni demasiado complejo, que capturará la verdadera relación entre X e Y.

Nótese que los conceptos de overfitting y underfitting están estrechamente relacionados con el dilema sesgo-varianza:

- Los modelos con sesgo alto hacen underfitting de los datos.
- Los modelos con varianza alta hacen overfitting de los datos.

En términos generales, tendremos la siguiente forma de curva de aprendizaje:

*(Diagrama: Curva de aprendizaje mostrando Error de entrenamiento, Error de prueba, zona de Underfitting, zona óptima y zona de Overfitting en relación a Complejidad del modelo)*
El equilibrio óptimo entre sesgo y varianza depende principalmente del contexto o del problema. En algunos casos, los modelos tienden a tener una varianza alta y fácilmente hacen overfitting de los datos, lo que lleva a malas predicciones.

En otros casos, no es necesario preocuparse tanto por controlar la complejidad, ya que el modelo es relativamente robusto en términos del equilibrio sesgo-varianza.

Como veremos más adelante, existen varias técnicas para controlar la complejidad de los modelos y lograr un equilibrio razonable entre capacidad de representación y poder predictivo.

## Funciones de Pérdida y Medidas de Rendimiento

Como hemos visto, la definición del Aprendizaje Automático implica mejorar alguna medida particular al realizar una tarea.

Esta medida debe estar bien definida, ser fácil de calcular y comprensible. Además, debe ser consistente con el algoritmo empleado para mejorarla, de modo que el aprendizaje se realice eficientemente.

Esta medida se llama **función de pérdida**.

La elección de función de pérdida es crucial al desarrollar cualquier aplicación de Aprendizaje Automático. Una mala elección de función de pérdida llevará a un modelo pobre, incluso cuando los datos son buenos y suficientes.

### Definición Formal del Problema de Aprendizaje

Podemos definir genéricamente el problema de Aprendizaje como encontrar los parámetros óptimos de modo que la pérdida, calculada como la “distancia” entre el valor predicho y el valor real, sea minimizada.

Como vemos, el aprendizaje puede definirse formalmente de esta manera, y por lo tanto, la calidad del aprendizaje depende crucialmente de elección de función de pérdida.

Nótese que los parámetros $W$ serán óptimos solo bajo tal función de pérdida, por lo que debe ser consistente con el problema en cuestión.

También debe ser posible optimizar la función de pérdida de manera eficiente.

### Medidas de Rendimiento (Métricas)

Después de que se ha construido un modelo, se pueden emplear otras medidas para evaluarlo. Tales medidas se llaman **medidas de rendimiento** (también denominadas **métricas**).

Las medidas de rendimiento no necesariamente tienen que ser las mismas que las funciones de pérdida empleadas al construir el algoritmo.

Nótese que, en principio, esto es de alguna manera una inconsistencia, ya que el modelo se optimiza usando una función y luego se evalúa usando otra.

Esto se hace por varias razones:

1. **En primer lugar**, las funciones de pérdida y rendimiento pueden estar estrechamente relacionadas. La situación más obvia es la del MAE (Error Absoluto Medio) y el MSE (Error Cuadrado Medio) cuando no hay grandes discrepancias en el rango de datos: una medida conducirá a resultados similares a la otra, por lo que el rendimiento y la pérdida serán consistentes.

2. **En segundo lugar**, existen algoritmos muy eficientes para funciones de pérdida particulares (por ejemplo, el algoritmo de retropropagación para minimizar el error cuadrado medio). Estos algoritmos pueden no existir o ser costosos de diseñar para funciones de rendimiento arbitrarias.

3. **En tercer lugar**, las funciones de rendimiento pueden ser una especie de pruebas estadísticas que se pueden usar para, por ejemplo, comparar modelos alternativos.

4. **Finalmente**, usar una función de rendimiento diferente a la función de pérdida puede evitar algunos problemas de overfitting. En algunos casos, los modelos “explotan” exitosamente propiedades de función de rendimiento, permitiéndose estar cerca en algún sentido estadístico, pero lejos en un sentido geométrico (el cuarteto de Anscombe, por ejemplo).

El uso de diferentes funciones de rendimiento/pérdida sigue siendo un área de debate entre teóricos y profesionales.

### Funciones de Pérdida en Regresión

Por ejemplo, cuando introdujimos modelos lineales en regresión, mencionamos que las predicciones pueden evaluarse usando el error cuadrado medio (MSE):

$$\text{m.s.e.} = g(\hat{Y}, Y) = \frac{1}{n}\sum {i=1}^{n}(y i - \hat{y} i)^2$$$

Hasta ahora, hemos usado una notación compacta para simplificar, pero en realidad lo que queremos hacer es calcular el MSE en todas las observaciones $y_1, y_2, \ldots, y_n$:

$$\text{m.s.e.} = g(Y, \hat{Y}) = \frac{1}{n}\sum {i=1}^{n}(y i - \hat{y} i)^2$$$

Como se mencionó, en este contexto, el aprendizaje puede interpretarse como el proceso de minimizar alguna pérdida; es decir, encontrar los parámetros óptimos $\beta_0, \beta_1, \beta_2, \ldots, \beta_n$ de modo que (por ejemplo) el error MSE sea minimizado:

$$\min {\beta 0, \beta 1, \beta 2, \ldots, \beta n} g(Y, \hat{Y}) = \frac{1}{n}\sum {i=1}{n}(y i - \hat{y} i)^2$$$$$

$$= \frac{1}{n}\sum {i=1}^{n}\left(y i - \beta 0 - \beta 1 X i - \beta 2 X i^2 - \ldots - \beta n X i^n\right)^2$$$$

### Características del MSE

Nótese que el MSE tiene una serie de características que no son obvias pero deben tenerse en cuenta:

- El MSE será sesgado si alguna predicción es particularmente mala.
- El MSE se expresa en unidades cuadradas, no en las mismas unidades de variable que queremos predecir.
- El MSE es sensible a la unidad de medida.
- El MSE no considera proporcionalidad: 4 es el doble de 2 y 8 es el doble de 4, pero en el primer caso el MSE es 4 y en el segundo caso es 16.

Esto, entre otras razones, hace que el MSE no sea una pérdida perfecta en cualquier situación.

La ubicuidad del MSE en muchas aplicaciones de Aprendizaje Automático se debe al hecho de que existen algoritmos de aprendizaje eficientes para él, ya que, como se mencionó, muchos usan descenso de gradiente.

Sin embargo, en otros contextos, podemos preferir emplear otras medidas.

Por ejemplo, podríamos emplear el error cuadrado medio de raíz (RMSE), que corrige el efecto de usar unidades cuadradas:

$$\text{r.m.s.e.} = g(\hat{Y}, Y) = \sqrt{\frac{1}{n}\sum {i=1} {n}(y i - \hat{y} i)^2}$$$

O el error absoluto medio (MAE) que penaliza por igual en todo el rango de Y:

$$\text{m.a.e.} = g(Y, \hat{Y}) = \frac{1}{n}\sum {i=1}^{n}

## Error Absoluto Porcentual Medio

Finalmente, es común expresar el error en términos porcentuales. En tal caso, podemos emplear el error absoluto porcentual medio (MAPE):

$$\text{m.a.p.e.} = g(Y, \hat{Y} = \frac{1}{n}\sum {i=1}{n}\frac{fligy i - \hat{y} i perpetua}{y i}$$$

### Funciones de Pérdida en Clasificación

En el caso de clasificación binaria, medidas como el MSE no parecen conformarse con el objetivo que queremos lograr, que es minimizar el número de clasificaciones erróneas.

La entropía cruzada se ha propuesto como una función de pérdida apropiada en el caso de clasificación binaria.
En cuanto a las funciones de rendimiento, en el caso de regresión, podemos usar algún estadístico como el R-cuadrado:

$$R^2 = \frac{\sum {i=1}^n (y i-\bar y)^2 - \sum {i=1}^n (y i-\hat y i)^2}{\sum {i=1}^n (y i-\bar y)^2}\in [0,1]$$$$$

El R-cuadrado mide qué fracción de variación de variable dependiente es explicada por el modelo.

Los buenos modelos tienen un valor alto de R-cuadrado (cercano a uno), y los malos modelos tienen un valor bajo (cercano a cero).

### Matriz de Confusión

En el caso de clasificación binaria (p. ej. Y={0,1}, Y={-1,1}), una de las medidas de rendimiento más empleadas es la matriz de confusión.

Simplemente registra el número de veces que el modelo predice correctamente la clase 0, el número de veces que predice correctamente la clase 1, y los errores al predecir cada una de las clases.

Llamando 1 a la clase "positiva" y 0 a la clase "negativa", tenemos:

Silencio Silencio REAL: Positivo Silencio REAL: Negativo
Silencio...
TENIDO PREDICCIÓN: Positivo ANTE Verdadero Positivo (TP)
TENIDO PREDICCIÓN: Negativo ANTE Falso Negativo (FN) ANTE Verdadero Negativo (TN)

Obsérvese que las predicciones correctas (en verde) se ubican en la diagonal principal, mientras que las predicciones incorrectas o errores (en rojo) están en la diagonal inversa de tabla.

Los diferentes términos usados en una matriz de confusión son los siguientes:

- **Verdadero Positivo (TP):** Son los casos en los que predijimos la clase "positiva" y, de hecho, la clase era "positiva".
- **Verdadero Negativo (TN):** Son los casos en los que predijimos la clase "negativa" y, de hecho, la clase era "negativa".
- **Falso Positivo (FP):** Predijimos la clase "positiva" pero la clase era "negativa".
- **Falso Negativo (FN):** Predijimos la clase "negativa" pero la clase era "positiva".

Una medida de exactitud global del algoritmo es:

$$\text{accuracy} = \frac{TP+TN}{TP+TN+FP+FN}$

La tasa de clasificación errónea mide con qué frecuencia el algoritmo hizo una predicción incorrecta; es simplemente:

$$\text{misclassification\ rate} = 1-\text{accuracy} = \frac{FP+FN}{TP+TN+FP+FN}$

Idealmente, nos gustaría que la suma de diagonal principal fuera el número total de predicciones.

La mayoría de las veces el algoritmo hará predicciones incorrectas, prediciendo positivo cuando es negativo, o lo contrario.

### Precisión y Exhaustividad (Precision y Recall)

A partir de matriz de confusión se han propuesto varias medidas; por ejemplo, la precisión:

$$\text{precision} = \frac{TP}{TP+FP}$

Otra medida es la exhaustividad (recall):

$$\text{recall} = \frac{TP}{TP+FN}$

Intuitivamente, supongamos que la clase "positiva" representa buenos candidatos para un empleo y la clase "negativa" malos candidatos.

La precisión intenta responder a la pregunta: de los candidatos que consideramos buenos, ¿qué porcentaje eran realmente buenos?

La exhaustividad (recall) intenta responder a la pregunta: de los candidatos que son buenos, ¿qué porcentaje detectamos correctamente que eran buenos?

Por supuesto, nos gustaría aumentar ambas medidas al mismo tiempo, pero puede demostrarse que hay un compromiso entre ambas: cuando aumentamos una de las medidas, la otra disminuirá.

Estas dos medidas son particularmente útiles cuando las clases están desbalanceadas.

### Puntuación F1

Es posible combinar precisión y exhaustividad en una única métrica llamada puntuación F1 (F1 score), que puede usarse para comparar dos o más clasificadores con diferente precisión/exhaustividad.

$$F1 = \frac{2} {\frac{1}{\text{recall}}+\frac{1}{\text{precision}}}} = \frac{2\times \text{recall}\times \text{precision}{\text{recall}+\text{precision}}}$$$$

La puntuación F1 es la media armónica de precisión y la exhaustividad y, a diferencia de media habitual, no trata todos los valores por igual, dando mucho más peso a los valores bajos.

El F1 puede variar entre 0 y 1, y la puntuación será alta si tanto la exhaustividad como la precisión son altas.

### Coeficiente de Correlación de Matthews

Otra medida popular de exactitud es el coeficiente de correlación de Matthews (Matthews correlation coefficient, MCC):

$$MCC = \frac{TP \times TN - FP \times FN}{\sqrt{(TP+FP)(FN+TN)(FP+TN)}\in [-1,1]$$

Un coeficiente igual a 1 corresponde a un clasificador perfecto, mientras que un coeficiente igual a -1 corresponde a un clasificador completamente equivocado.

Tiene la ventaja de que puede usarse incluso cuando las clases están desbalanceadas.

### Matriz de Confusión Multiclase

La matriz de confusión puede extenderse a un número arbitrario de clases; por ejemplo, podríamos considerar tres clases: positiva, neutral y negativa.

TENIDO TERRITORIO REAL: Positivo TENER REAL: Neutral TEN REAL: Negativo Silencio
Silencio...
TENIDO PREDICCIÓN: Positivo Silencio Silencio Silencio
TENIDO PREDICCIÓN: Neutral Silencio Silencio Silencio Silencio
TENIDO PREDICCIÓN: Negativo Silencio Silencio Silencio

En estos casos, la medición del rendimiento es más complicada, ya que hay que considerar un número explosivo de tipos de clasificación errónea.

## División de Datos (Data Splitting)

Como se mencionó, los modelos no paramétricos tienen la capacidad de aproximar funciones arbitrarias, pero tienen el inconveniente de poder hacer overfitting del ruido.

En la curva de aprendizaje parece obvio elegir la complejidad óptima del modelo, ya que, dado que se usará con fines de pronóstico, el modelo debería ser el que minimice el error de prueba.

El problema es que, en general, no tendremos acceso al conjunto de prueba, porque precisamente consiste en observaciones que no conocemos, ya sea porque todavía no han ocurrido o, al menos, porque nuestras predicciones no podrían probarse porque no conocemos el valor de variable en estudio.

Por estas razones, tenemos que idear métodos que nos permitan aproximar el error de prueba usando solo observaciones del conjunto de entrenamiento.

La mayoría de los métodos caen dentro de lo que se llama bootstrapping; el bootstrap consiste en muestrear a lo largo del conjunto de datos que tenemos disponible y calcular alguna medida particular de él.

Se calcula la media de medida y se toma como una aproximación al valor real.

### Conjuntos de Entrenamiento, Prueba y Validación

El primer enfoque que se ha propuesto es dividir los datos de entrenamiento en tres componentes: entrenamiento puro (o conjunto de entrenamiento, de ahora en adelante), conjunto de prueba y conjunto de validación (o conjunto de desarrollo).

El conjunto de datos de entrenamiento se usa solo para calibrar el modelo.

El objetivo con este conjunto sería reducir, tanto como sea posible, el error de entrenamiento.

Después de alcanzar la calibración óptima, el segundo conjunto de observaciones se usa para calcular el error en observaciones no vistas.

Si la tasa de error en este conjunto es similar (se podrían emplear pruebas formales) a la del conjunto de entrenamiento, podemos concluir que la complejidad del modelo es adecuada y entonces usar el modelo en un entorno real.

El error en el conjunto de validación se calcula entonces y debería ser similar a los errores en los conjuntos de entrenamiento y prueba.

Si el error en el conjunto de prueba es "significativamente" mayor que el del conjunto de entrenamiento, esto es un indicador de overfitting; el modelo puede haber memorizado los datos de entrenamiento, perdiendo su capacidad de generalizar.

El tamaño de los conjuntos de entrenamiento, prueba y validación depende de disponibilidad de datos.

Hace varios años era muy común usar particiones de 60%/40% u 80%/20% en entrenamiento/prueba (sin validación).

Hoy en día, algunas aplicaciones hacen uso de cantidades enormes de datos, de modo que 90%/5%/5% es razonable, o incluso 98%/1%/1%.

### Validación Cruzada (Cross-Validation)

Para evitar el problema de una selección adversa del conjunto de prueba y obtener una estimación más fiable del error de validación, se ha propuesto el método de validación cruzada, basado en la mencionada idea del bootstrapping.

La idea es muy simple: los datos se dividen en $k$ segmentos sin solapamiento ($k=10$ es una elección popular); $k-1$ de ellos se usan para entrenamiento y el restante se usa para calcular el error de prueba; luego se usa otro conjunto de $k-1$ segmentos y se calcula el error de prueba en el segmento restante; el procedimiento continúa hasta que se han usado todos los segmentos.

$$CVE = \frac{1}{k}\sum {j=1}{k} \text{testing\ error} j$$

Puede demostrarse que el error de validación cruzada de k particiones (k-fold) se aproxima al error de prueba cuando el número de observaciones es alto.

*(Diagrama: esquema de validación cruzada de 10 particiones (10-fold), mostrando cómo en cada una de las 10 iteraciones un segmento distinto se usa como conjunto de prueba y los 9 restantes como conjunto de entrenamiento.)*

## Regularización

Como hemos mencionado, el overfitting es un problema importante en los modelos de ML no paramétricos.

Recuerde que los modelos de ML intentan ser operativos, en el sentido de que deberían proporcionar buenos pronósticos; un modelo que se ajusta correctamente a los datos de entrenamiento pero que falla al generalizar NO es un buen modelo.

Para evitar el overfitting, la complejidad del modelo debe mantener un equilibrio entre ajustarse a los datos de entrenamiento y generalizar sobre ejemplos no vistos.

El problema es que, por definición, no sabemos qué tan complejo debería ser el modelo; de lo contrario, no necesitaríamos modelos no paramétricos que aumentan su complejidad dependiendo del problema en cuestión.

Solo en el caso de los modelos lineales existen algunos procedimientos formales para seleccionar entre modelos competidores; afortunadamente, en el contexto del Aprendizaje Automático, se han desarrollado varias técnicas para controlar la complejidad del modelo.

Por ejemplo, como hemos visto antes, es posible estimar el error de predicción usando técnicas de remuestreo como la validación cruzada.

El error estimado de varias configuraciones del algoritmo, con distintos grados de complejidad, puede compararse y entonces se selecciona el modelo con el error esperado mínimo.

Obsérvese que este método consiste en seleccionar el mejor modelo entre el grupo de modelos estimados.

Otra posibilidad es controlar, ex ante, la complejidad del modelo durante el procedimiento de aprendizaje.

En principio, esto nos permitiría usar una "única" configuración, de modo que no necesitaríamos estimar diferentes modelos, reduciendo la carga computacional.

Los enfoques que intentan controlar la complejidad del modelo durante la fase de aprendizaje se conocen como regularización.

Las técnicas de regularización consisten esencialmente en modificar la función de pérdida para incluir una penalización por la complejidad del modelo.

El algoritmo de aprendizaje debe modificarse convenientemente para minimizar esta función regularizada; el modelo resultante mantendrá un equilibrio entre la precisión sobre los ejemplos de entrenamiento y la complejidad, asegurando la generalización.

## Early Stopping (Parada Temprana)

Otra posibilidad para regularizar modelos es emplear early stopping (parada temprana), que consiste esencialmente en detener el entrenamiento con los resultados que impedirán que el modelo haga overfitting.

Recuerde, a partir de curva de aprendizaje, que la curva de generalización tiene forma de U, disminuyendo primero y aumentando después con la complejidad del modelo.

Puede demostrarse que este patrón se repite si en el eje X, en lugar de considerar el número de parámetros, consideramos los ciclos de entrenamiento, porque a medida que el aprendizaje progresa, los parámetros se modifican para ajustarse cada vez más a los datos de entrenamiento.

De forma similar a los humanos, las máquinas también necesitan tiempo para aprender, y "memorizar", en cierto sentido, reduce la creatividad.

Al comienzo del entrenamiento, la mayoría de los parámetros serán pequeños (poco efectivos), y a medida que el aprendizaje progresa aumentarán su valor; el early stopping es como si hubiéramos regularizado la red.

Si detenemos el entrenamiento en el punto en que el error en la última iteración disminuyó pero el error en la siguiente iteración aumenta (punto amarillo), entonces podemos estar seguros de que la complejidad del modelo es óptima.

Para algunos autores, el early stopping proporciona una forma eficiente de controlar la complejidad sin la carga de modificar la función de pérdida y el algoritmo de entrenamiento.

Para otros, "mezcla" las fases de aprendizaje y selección de modelo, y no será tan efectivo como un procedimiento de dos pasos.

El precio que tenemos que pagar es llevar un registro de los parámetros del modelo en la fase precedente, de modo que esos parámetros se usen en caso de que el error comience a aumentar, en lugar de los actuales.

Además, obsérvese que tenemos que calcular el error en el conjunto de prueba en cada iteración.

Después de encontrar el modelo óptimo, se puede emplear el conjunto de datos completo (entrenamiento + prueba) para reentrenar el modelo.

Obsérvese que esto tiene el inconveniente de que no sabemos cuántos ciclos tendremos que ejecutar, y si es mejor reiniciar usando otro conjunto de parámetros iniciales o realizar algunos ciclos con los parámetros actuales.

En el primer caso, se ha propuesto monitorizar la función de pérdida promedio en el conjunto de validación, y continuar el entrenamiento hasta que caiga por debajo del valor del entrenamiento cuando nos detuvimos.
.