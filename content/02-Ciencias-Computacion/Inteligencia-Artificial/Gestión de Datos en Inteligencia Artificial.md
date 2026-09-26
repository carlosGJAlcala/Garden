---
title: "Gestión de Datos en Inteligencia Artificial"
---

# Gestión de Datos en Inteligencia Artificial

Prof. Ignacio Olmeda
AI LAB

## La importancia del preprocesamiento de datos e ingeniería de características

- Como hemos visto, los algoritmos de aprendizaje automático (ML) utilizan datos para desarrollar modelos predictivos.
- Antes de utilizar tales algoritmos, el desarrollador debe seguir el proceso ETL (Extraer, Transformar, Cargar), que consiste en extraer información de fuentes confiables, transformar esa información para que sea utilizable y cargar la información en el sistema que utilizaremos para alimentar el algoritmo.
- Muchos investigadores sugieren que el proceso ETL consume más del 80% del tiempo de desarrollo en un proyecto de aprendizaje automático.

## Extracción y carga de datos

- Respecto a la extracción y carga de datos, existen diversas soluciones que pueden emplearse para gestionar la cantidad masiva de datos que caracteriza a las aplicaciones de ML. Ejemplos de tales soluciones/sistemas/tecnologías comerciales son Hadoop, Hive, Spark, AWS, etc.

## Transformación de datos

- Con respecto a la transformación o procesamiento de datos, la tarea es altamente dependiente de aplicación y requiere un esfuerzo considerable del desarrollador.
- Los algoritmos de ML pueden, teóricamente, encontrar patrones ocultos en datos sin procesar; esto significa que, en principio, no es necesario transformar los datos para hacerlos accesibles.
- Sin embargo, al igual que los humanos, los algoritmos de aprendizaje automático pueden procesar más eficientemente datos con una representación particular. La representación o preprocesamiento proporciona una "pista" al algoritmo, facilitando en la mayoría de los casos el proceso de aprendizaje.

- Observe también que algunas características de las instancias que podemos querer emplear pueden no ser numéricas (p. ej., etiquetas) y, por lo tanto, no pueden ser tratadas de manera analítica eficiente.
- Por ejemplo, piense en el caso de las tareas de Amazon Mechanical Turk.
- Finalmente, muchos algoritmos requieren que la dimensionalidad de los datos de entrada se mantenga constante; por ejemplo, el mismo número de píxeles en una imagen, de modo que los datos sin procesar pueden necesitar algún tipo de transformación.
- Por estas y otras razones, el preprocesamiento de datos es una parte esencial de construcción de modelos de ML y condiciona fuertemente el resultado de todo el proceso.
- La calidad de los datos es esencial en ML, ya que los datos son la materia prima para construir los modelos.

## Características: propiedades e ingeniería

- Como mencionamos, los atributos en ML se llaman características, y pueden interpretarse como propiedades del objeto (medibles o no).
- Generalmente se requiere que las características sean independientes (sin relación entre ellas) y tengan poder discriminativo (de modo que añadan algo al problema en cuestión), pero incluso detectar tales propiedades simples es infeasible en la mayoría de los casos.
- Por ejemplo, las características pueden parecer independientes por pares, pero puede haber una variable latente que afecte a dos variables aparentemente independientes.
- Además, algunas variables pueden parecer no tener poder discriminativo, pero cuando se toman conjuntamente con otra variable, su poder puede aumentar radicalmente. Por ejemplo: $Y = X_1 \cdot X_2$.

## Ingeniería de características

- La ingeniería de características es el área del ML que intenta obtener los mejores resultados posibles de un modelo predictivo transformando datos sin procesar en características que mejor representen el problema subyacente a los modelos predictivos.
- Tenga en cuenta que las características pueden ser propiedades directamente observables (p. ej., fecha de nacimiento), deben estimarse usando un modelo o aparato (temperatura) o pueden ser subjetivas.

## Intuición sobre datos

- Para detectar si los datos en cuestión son consistentes, el primer paso es tener una vista intuitiva. La visualización y las estadísticas descriptivas permiten entender la naturaleza de los datos.
- Respecto a las estadísticas, algunas medidas estadísticas útiles son la media, la mediana (el punto central de distribución) y la moda (el valor más frecuente).
- Ejemplo: datos 4 8 3 5 6 9 2 3 1
 - Media: 4.6
 - Mediana: 4
 - Moda: 3

- También es relevante evaluar algunas medidas de dispersión, como el rango (la distancia entre el valor máximo y mínimo) o la varianza.

## Medidas de co-movimiento

- También puede ser útil analizar medidas de co-movimiento, como la correlación.

$$\rho = \frac{i=1}{n} (X {1i} - \overline{X 1})(X {2i} - \overline{X 2})}{\sqrt{ =1}{i=0}{i} {2}{i}{i}} {2}{i}}}{2} {0}{1}}}{i}{i}}}}{i}=0}{i}}{i}}}}}}{i}{i}}{i}{i}}}}}}{i}}}}}}}}}}}}}}}}{2}{2}}{i}{i}}}}{i}{i}{i}}{i}}}}}}}}}}}}}}}}}}}{i}{i}{i}{i}{i}}}}}}}}}}}}}}}}{i}}}}}{i}}}{i}}}

- Otra posibilidad es utilizar la prueba de chi-cuadrado para la independencia entre variables:

$$\chi^2 {prueba} = \sum {i,j} \frac{(\text{observado} {i,j} - \text{esperado} {i,j})^2}{\text{esperado} {i,j}\approx \chi^2 {k}\text{ where } k = (r-1)(c-1)$$$$$$$$$$

- Hipótesis nula: Independencia

### Ejemplo de tabla de contingencia

**TABLA OBSERVADA:**

Silencio variable01 / variable02 Silencio 0 Silencio 1 Silencio Total Silencio
Silencio...
Silencio 0 Silencio 12 Silencio 9 Silencio 21 Silencio
Silencio 1 Silencio
Silencio Silencio Silencio . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 

**TABLA ESPERADA:**

silencio variable01 / variable02 silencio 0 silencio
silencio...
silencioso 0 silencio
silenciosamente infligidos

**Chi-cuadrado por celda:**

silencio variable01 / variable02 silencio 0 silencio
silencio...
silencio 0,69 silencio 0,56 silencio
silencio 1 silencio 0,76 silencio 0,62 silencio

- Suma chi-cuadrado: 2.63
- Valor crítico (df=1): 3.84

- Sin embargo, tales estadísticas proporcionen, en algunos casos, pobres descripciones de los datos.
- Un ejemplo paramount es el cuarteto de Anscombe, cuatro conjuntos de datos con estadísticas descriptivas simples casi idénticas pero que son muy diferentes cuando se representan gráficamente.

## Visualización de datos

- Por esta razón, cuando sea posible, generalmente es útil tener una vista intuitiva de los datos en forma de algún tipo de gráfico.
- El problema es que las relaciones entre variables podrían ser altamente no lineales, verse afectadas por ruido y también tener una dimensionalidad alta, lo que en la mayoría de los casos hace muy difícil producir tales gráficos.
- El rango de posibilidades que ofrece la visualización es enorme; es un área muy activa de investigación que está produciendo muchos resultados interesantes.

### Histogramas

- Entre los gráficos que pueden usarse para tener una vista intuitiva de los datos, probablemente el más obvio es el histograma, que muestra la dispersión y lo puntiagudo de distribución y si está sesgada.

### Gráfico de caja y bigotes

- El gráfico de caja y bigotes también es muy conveniente para entender la variabilidad entre cuartiles de distribución.

### Gráficos de dispersión

- Los gráficos de dispersión dan una intuición sobre la relación entre pares de variables.
- Un problema de los gráficos de dispersión es que pueden ser demasiado densos, haciendo imposible detectar ningún patrón en los datos.
- Una alternativa es emplear gráficos de densidad 2D, que cuentan el número de observaciones dentro de un área particular del espacio 2D.

### Gráficos de burbujas

- Los gráficos de burbujas extienden dos dimensiones a una tercera mostrando en los ejes cartesianos la tercera dimensión usando el tamaño de los puntos.
- La visualización de datos y las estadísticas descriptivas son herramientas poderosas que pueden ser útiles para entender los datos en cuestión y diagnosticar problemas con ellos.

## Preprocesamiento y ingeniería de características

- Una vista intuitiva de los datos no es suficiente para construir aplicaciones de ML exitosas.
- Hay varias cuestiones que deben abordarse para asegurar que los datos faciliten el proceso de construcción de modelos. En particular, tenemos que considerar problemas relacionados con:
 - Datos faltantes
 - Transformación de datos
 - Representación de datos
 - Datos incompletos
 - Datos desbalanceados
 - Reducción de datos

### Datos faltantes

- Los datos faltantes ocurren cuando una o más características de algunos ejemplos particulares no están disponibles.
- Esto puede deberse a varias razones y cada una de ellas debe abordarse adecuadamente:
 - Los datos existen pero son desconocidos; por ejemplo, para un individuo podríamos no conocer su fecha de nacimiento.
 - No sabemos si los datos existen o no; por ejemplo, en el atributo "piso" no sabemos si el individuo reside en un apartamento o en una casa, por lo que no sabemos si el atributo es aplicable.

- Los datos faltantes tienen diferentes consecuencias dependiendo del algoritmo aplicado. En algunos casos el algoritmo puede manejar perfectamente los datos faltantes (algunos árboles de decisión, por ejemplo), mientras que en otros casos los datos deben completarse para que el algoritmo funcione (modelos lineales, por ejemplo).

## Tipos de datos faltantes

- Los datos faltantes se denominan comúnmente:
 - **Missing Completely at Random (MCAR):** los datos faltantes son completamente aleatorios; no hay relación entre si un punto de datos está faltante y ningún valor en el conjunto de datos, ya sean faltantes u observados.
 - **Missing at Random (MAR):** la causa de los datos faltantes no está relacionada con los valores faltantes pero puede estar relacionada con los valores observados de otras variables.
 - **Missing Not at Random (MNAR):** el valor faltante depende del valor hipotético de variable.

### Estrategias para tratar datos faltantes

#### 1. Eliminación de ejemplos (listwise deletion)

- La alternativa más drástica es eliminar completamente el ejemplo que tiene una o más características incompletas.
- Esta alternativa puede ser razonable cuando hay muchos datos, pero en la mayoría de los casos no es feasible.
- Además, la pérdida de algunas características puede revelar problemas en la adquisición de datos, y la eliminación de tales ejemplos puede inducir un sesgo en los datos.

**Ejemplo:**

| Patrón | Atributo 1 | Atributo 2 | Atributo 3 | Atributo 4 | Atributo 5 |
|---|---|---|---|---|---|
| A | 1 | 4 | 3 | 0 | 2 |
| B | 4 | 6 | na | 1 | 2 |
| C | 7 | 6 | na | 1 | 2 |
| D | 1 | 5 | 3 | 6 | 8 |
| E | 8 | 3 | 7 | 1 | 2 |
| F | 1 | 6 | na | 2 | 2 |

#### 2. Eliminación de características (dropping características)

- Otra alternativa es eliminar la característica que tiene demasiados valores faltantes.
- Tenga en cuenta que esta alternativa también es muy drástica, ya que la característica eliminada puede tener un alto valor predictivo sobre la variable dependiente.

**Ejemplo:**

| Patrón | Atributo 1 | Atributo 2 | Atributo 3 | Atributo 4 | Atributo 5 |
|---|---|---|---|---|---|
| A | 1 | 4 | 3 | 0 | 2 |
| B | 4 | 6 | na | 1 | 2 |
| C | 7 | 6 | na | 1 | 2 |
| D | 1 | 5 | 3 | 6 | 8 |
| E | 8 | 3 | 7 | 1 | 2 |
| F | 1 | 6 | na | 2 | 2 |

#### 3. Imputación de datos

- La tercera posibilidad es reemplazar el valor del atributo faltante por alguna estimación del valor "esperado" de variable. Este procedimiento se llama imputación de datos.
- "Esperado" no tiene, en general, una interpretación clara. Por ejemplo, podríamos emplear la media, la mediana, la moda o incluso el valor que es más común para patrones similares.

**Ejemplo de imputación:**

Silencio Patrón Silencio Atributo 1 Silencio Atributo 2 Silencio Atributo 3 Silencio Atributo 4 Silencio Atributo 5 Silencio
Silencio...
Silencio A Silencio 1 Silencio 4 Silencio 3 Silencio 0 Silencio 2 Silencio
Silencio B Silencio 4 Silencio 4 Silencio na Silencio 1 Silencio 2
Silencio C Silencio 5 Silencio 4 Silencio 2 Silencio
Silencio D Silencio 1 Silencio 5 Silencio 6 Silencio 8 Silencio
Silencio E Silencio 8 Silencio 3 Silencio 7 Silencio 1 Silencio 2
Silencio F Silencio 1 Silencio 6 Silencio 4 Silencio 2 Silencio

- Moda: 3
- Media: 3.8
- Más cercano (patrón C): 2

### Métodos más sofisticados de imputación

- Se pueden aplicar métodos más sofisticados. Por ejemplo, se puede intentar ajustar un modelo lineal usando la característica faltante como variable independiente y usar ejemplos completos para realizar la regresión, luego usar los coeficientes estimados para pronosticar el valor de variable faltante:

$$\hat{X} 1 = \hat{\alpha} + \hat{\beta} 1 X 1 + \ldots + \hat{\beta} {k-1} X {k-1} + \hat{\beta} {k+1} X {k+1} + \ldots + \hat{\beta} n X n$$$$$$$$$$$$$$$

- En el caso de series de tiempo, hay una diversidad de métodos que pueden emplearse. Los más simples simplemente usan el último punto de datos:

$$X {t+1}^n = X t^n$$

- O una interpolación, por ejemplo:

$$X t = \frac{X {t-1}^n + X {t+1}{2}$$

- O un método más sofisticado, como estimar un modelo para predecir el valor desconocido usando los existentes.

## Transformación de datos

- La transformación de datos se refiere al proceso de modificar datos para hacerlos más adecuados para nuestros algoritmos de aprendizaje automático.
- Implica varias modificaciones posibles de datos sin procesar o incluso la eliminación de ejemplos o características que pueden distorsionar el proceso de encontrar patrones ocultos en los datos.
- Este proceso también se llama limpieza de datos.

### Normalización y estandarización

- En estadística, es muy común emplear variables que siguen una distribución normal $N(\mu, \sigma)$ y transformarlas a una distribución estándar $N(0,1)$:

$$Z = \frac{X - \mu}{\sigma} \approx N(0,1)$$

- Esto se hace porque las propiedades estadísticas de distribución normal estandarizada son bien conocidas y se pueden calcular estadísticas con una distribución conocida.
- Tales estandarizaciones también se aplican comúnmente en aprendizaje automático, aunque los propósitos no son inferenciales sino de naturaleza más práctica.

### Escalado de características

- Dado que las variables pueden ser bastante diferentes expresadas en escalas muy diferentes, esto puede afectar al proceso de aprendizaje. Observe que incluso en modelos triviales como un modelo multinomial:

$$Y = \alpha + \beta 1 X 1 + \beta 2 X 2 + \ldots + \beta n X n$$

- Los parámetros pueden tener escalas muy diferentes. Por lo tanto, por ejemplo, una randomización en el intervalo [0,1] para $\beta_1$ podría ser inapropiada si se mueve en, por ejemplo, [100.000, 200.000] para $\beta_n$.

- Otra posibilidad es emplear:

$$X' = \frac{X - \min(X)}{\max(X) - \min(X)} \in [0,1]$$

- La siguiente figura proporciona cierta intuición del proceso de normalización.

*(diagrama no reconstruible a partir de extracción)*

## Valores atípicos (outliers)

- Para algunos algoritmos de ML es particularmente relevante verificar observaciones anormales. Es casi imposible definir qué significa "anormales": las observaciones pueden parecer diferentes, pueden ser diferentes o simplemente pueden ser causadas por errores en la recopilación de datos (problemas de "dedo gordo").
- Una propiedad de distribución normal es que entre la media y 2 veces la desviación estándar podemos encontrar el 95% de las observaciones.

### Definición de outlier

- Un outlier es "una observación que se desvía tanto de otras observaciones que despierta sospechas de que fue generada por un mecanismo estadístico diferente" (Hawkins, 1980).
- Una posibilidad es considerar que una observación anormal es aquella que es "extremadamente rara" (p. ej., 5%) y luego truncar variables que están muy lejos del comportamiento "normal":

$$x' = \begin{cases} \min(x, \mu + 2\sigma), & \text{si } x ⇩ 0 \max(x, \mu - 2\sigma), &\text{si } x \leq 0 \end{cases}$$

### Métodos de detección de outliers

- Otra posibilidad es simplemente calcular el z-score de las observaciones:

$$z\text{-score} = \frac{X - \mu}{\sigma}$$

- Luego, eliminar observaciones que tengan, por ejemplo, z-score mayor que 3, 4, etc.
- Finalmente, se pueden usar métodos más sofisticados como Isolation Forests, Density-based spatial clustering of applications with noise (DBSCAN), Local Outlier Factor (LOF), etc.

*(fragmento: referencia a 'outlier.ipynb')*

## Representación de datos

- La representación de datos se refiere al procedimiento de encontrar el alfabeto óptimo para expresar los datos de modo que sea adecuado para el algoritmo de aprendizaje automático en cuestión.
- En algunos casos, la representación de datos es relativamente clara; por ejemplo, en modelos de regresión parece obvio usar números reales.
- Sin embargo, en la mayoría de los casos, la decisión no es trivial. Supongamos que tenemos una característica que representa cuatro clases A, B, C, D.

### Opciones de representación para variables categóricas

- Una posibilidad es considerarlas ordenadas y usar, por ejemplo, {1, 2, 3, 4}.
- Otra posibilidad es considerarlas desordenadas y usar una representación binaria, por ejemplo: {00, 01, 10, 11}.
- Finalmente, podemos considerar la distancia relativa entre las clases, considerando números reales, por ejemplo: {1, 1.5, 2.5, 4}.

### Codificación one-hot

- En el caso de datos categóricos donde la ordenación no tiene sentido, una posibilidad es emplear codificación one-hot, que simplemente consiste en crear variables binarias "dummy" con el mismo número de bits que el número de clases en el conjunto de datos original.

**Ejemplo con 4 clases:**

TENIDO Clase TENIDO Bit 1 ← Bit 2 TENIDO Bit 3 Silencio 4
Silencio...
Silencio A Silencio 1 Silencio 0 Silencio 0 Silencio 0
Silencio Silencio Silencio 0 Silencio 1 Silencio 0 Silencio
Silencio C Silencio 0 Silencio 0 Silencio 1 Silencio 0
Silencio D Silencio 0 Silencio 0 Silencio 0 Silencio

**Ejemplo con 7 clases:**

TENIDO Clase TENIDO Bit 1 TENIDO Bit 2 TENIDO Bit 3 Silencio 4 TENIDO Bit 5 Silencio 6 Silencio Bit 7 Silencio
Silencio...
Silencio A Silencio 1 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio
Silencio B Silencio 0 Silencio 1 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio
Silencio C Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio
Silencio D Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio
Silencio E Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio
Silencio F Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 1 Silencio 0 Silencio
Silencio G Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 0 Silencio 1 Silencio

## Datos incompletos

- Los datos incompletos son algo diferentes de los datos faltantes. En este caso nos referimos al hecho de que algunos datos pueden simplemente no existir y deben crearse "ad-hoc"; por ejemplo, usando datos simulados.
- Los datos simulados se refieren a observaciones que se crean artificialmente para completar un conjunto de datos o incluso para ser usados como base de datos única.
- En muchos casos, los datos simulados son la única alternativa cuando los datos no existen o son escasos y existe un modelo para la creación de datos.

### Ejemplo de datos simulados

- Por ejemplo, supongamos que estamos construyendo un algoritmo de ML y una de las entradas es la llegada de órdenes a algún centro. Supongamos que las órdenes llegan aleatoriamente siguiendo un paseo aleatorio discreto:

$$O t = O {t-1} + \eta t, \quad \eta t \approx N(0,1)$$

- Supongamos que necesitamos muchos ejemplos de evolución del proceso para las primeras 1000 observaciones comenzando en $O_1 = 0$. Simplemente podríamos emplear el modelo conocido para generar tales datos y luego emplearlo como entrada a nuestro algoritmo.
- Esto también es la base de los métodos de Montecarlo, que se emplean ampliamente en ML para evaluar algoritmos alternativos, medir la sensibilidad contra características y muchas otras aplicaciones además de generación de datos.

## Datos desbalanceados

- Los datos desbalanceados se refieren al problema de que algunos ejemplos de datos pueden estar subrepresentados en la base de datos.
- Esto intrínsecamente induce un sesgo en el algoritmo de aprendizaje, que prestará más atención a los datos que están sobrerrepresentados.
- Como ejemplo, supongamos que una base de datos incluye dos clases: clase A con 95% de los ejemplos y clase B con 5% de los restantes.
- Un clasificador "perezoso" puede predecir solo la clase A y aún lograr una precisión del 95%, dando la impresión errónea de un comportamiento excelente.
- El problema de datos desbalanceados es extremadamente común en ML, no solo en problemas de clasificación sino también en regresión. Por ejemplo, cuando registramos rendimientos de alguna acción, la mayoría de las observaciones están cerca de cero, por lo que el modelo está naturalmente sesgado a no considerar observaciones extremas.

## Estrategias para tratar datos desbalanceados

- Los datos desbalanceados deben tratarse adecuadamente si se quiere evitar sesgos en los datos, que frecuentemente se etiquetan incorrectamente como "sesgos algorítmicos".
- Cuando la base de datos está desbalanceada, podemos adoptar cuatro estrategias:
 - **Sobremuestreo (Oversampling):** sobremuestrear la clase subrepresentada duplicando observaciones hasta que el conjunto de datos esté balanceado.
 - **Submuestreo (Undersampling):** submuestrear la clase sobrerrepresentada eliminando observaciones hasta que el conjunto de datos esté balanceado.
 - **Creación de datos sintética:** crear datos sintéticamente, de manera similar a como mencionamos antes.
 - **Modificación de función de costo:** dar más peso a la clase/datos que están subrepresentados.

### SMOTE (Synthetic Minority Oversampling Technique)

- Respecto a la creación de datos para datos desbalanceados, un algoritmo popular es SMOTE (Synthetic Minority Oversampling Technique), que sigue estos pasos:
 1. Para cada ejemplo del conjunto minoritario, elegir los k vecinos más cercanos.
 2. Seleccionar aleatoriamente una instancia de los vecinos más cercanos.
 3. Crear una nueva instancia con características como una combinación convexa de las características de instancia original y del vecino más cercano.

- La observación sintética se crea como:

$$x' i = x i + \lambda(x j - x i)$$

- donde $\lambda$ es un número aleatorio en [0,1].

### ADASYN (Adaptive Synthetic muestreo método)

- Una técnica muy similar se llama método de sobremuestreo sintético adaptativo (ADASYN).
- En ADASYN, el número de ejemplos sintéticos generados es proporcional al número de ejemplos en el grupo de vecinos que no son de clase minoritaria.
- Observe que en este caso se generan más ejemplos sintéticos en el área donde los ejemplos de clase minoritaria son raros.

### Ventajas y desventajas de las estrategias

- Cada una de estas alternativas tiene sus inconvenientes:
 - **Sobremuestreo:** puede llevar a sobreajuste.
 - **Submuestreo:** conduce a la reducción de muestra.
 - **Datos sintéticos:** puede tener baja calidad o ser difícil de replicar.
 - **Funciones de costo modificadas:** es difícil calibrar y el algoritmo de aprendizaje necesita ser reescrito.

## Reducción de datos

- La reducción de datos se refiere al procedimiento de "comprimir" características para reducir la complejidad del problema.
- La compresión puede interpretarse de dos maneras. Primero, podemos eliminar algunas características que pueden no tener poder predictivo; en tal caso, hablamos propiamente de selección de características.
- En otros casos, podemos pensar que la granularidad del problema es demasiado alta y podemos estar interesados en combinar atributos para crear nuevos (menos) atributos; en este caso decimos que estamos realizando reducción de dimensionalidad.
- Observe que en ambos casos, el número efectivo de características se reduce, de modo que la complejidad del problema también se reduce, haciendo más fácil construir y depurar modelos de ML.

## Principio de parsimonia (Occam's Razor)

- Respecto a la reducción de complejidad, un principio bien conocido en ciencia es la navaja de Occam, que sostiene que entre hipótesis rivales, la que tiene el menor número de suposiciones es probablemente la más correcta.
- En el contexto de construcción de modelos, esto significa que los modelos con menos parámetros y características pueden proporcionar mejores explicaciones de los datos y también mejores pronósticos.

### Selección de características

- El proceso de selección de características puede realizarse bajo varios enfoques.
- En primer lugar, podemos considerar métodos para eliminar características inútiles. En este caso, podemos distinguir entre:
 - **Métodos de filtrado:** intentan eliminar ex-ante atributos redundantes o inútiles.
 - **Métodos de envoltura:** consideran la selección de características como un problema de búsqueda.
 - **Métodos de regularización:** intervienen directamente en el modelo para que descarte características de bajo valor.

### Enfoques incremental y decremental

- En segundo lugar, la elección de características puede ser:
 - **Incremental:** añadiendo una característica más al modelo de modo que el rendimiento aumente lo máximo posible.
 - **Decremental:** removiendo la característica que degrada menos el rendimiento del modelo.
- Observe que, de hecho, el modelo subyacente se modifica y el número efectivo de parámetros y la complejidad del modelo se cambian.
.