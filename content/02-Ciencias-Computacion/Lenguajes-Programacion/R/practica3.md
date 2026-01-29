---
title: "Practica3"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - r
---

**PECL3**

En esta práctica vamos a trabajar la adquisición, pre-procesado (limpieza) y obtención de datasets. Los datasets con los que hemos trabajado hasta el momento no surgen de la nada. Son datos extraídos de observaciones, recopilados de encuestas, descargados de instituciones que los hacen públicos o sencillamente obtenidos de APIs en Internet.

Hoy día, la ciencia de los datos (data science), entendida como la ciencia que se encarga de la recolección, organización, análisis e interpretación de los datos, es de particular importancia, lo que se refleja en enormes cifras de negocio e inmejorables perspectivas laborales para aquellos capaces de dominarla. La ciencia de los datos comporta programación, matemáticas y estadística.

Puesto que, de modo general, el trabajo en ciencia de los datos conlleva un 80% de limpieza y obtención de datos, y un 20% de obtención y análisis de los resultados, vamos a aplicar lo aprendido en Fundamentos de la Programación y Estadística a un ejemplo real de ciencia de los datos. Para ello, se llevará a cabo un trabajo en grupo (idealmente de 2 o 3 personas) en el que se obtengan datos, se limpien y se haga un análisis sobre los mismos, siguiendo grosso modo las siguientes directrices:

1. **Personas que forman el equipo** (idealmente 2 o 3).
2. **Documentar brevemente el API que se va a utilizar.** El uso del API de LOL, al haber sido explicado en clase, puede ser más recomendable. No obstante, hay muchos otros:
    - Twitter: [Twitter API Documentation](https://developer.twitter.com/en/docs/basics/getting-started)
    - Fortnite: [Fortnite API Documentation](https://fortniteapi.com/docs)
    - Cualquier otro de [ProgrammableWeb](https://www.programmableweb.com/).
3. **Qué dataset/s han creado y para qué.**
4. **Cómo se han limpiado los datos obtenidos**, qué datos han sido seleccionados y por qué.
5. **Uno o varios análisis sobre los datos obtenidos.** Se debe incluir un ejemplo al menos de contraste de hipótesis sobre el/los datasets y una explicación de alto nivel de lo que significa lo obtenido. Ejemplos:
    - **[Explicación de alto nivel]**: "En Fortnite, las partidas en las que quedas entre los 5 primeros es casi seguro que recorrerás al menos 3 km”.
    - **[Contraste de hipótesis]**: “¿Es cierto o es falso que en LOL cuando ganas la partida recoges un 10% más de oro, como mínimo, que cuando pierdes?”.

**IMPORTANTE. Se valorará:**

- La **API utilizada**.
- La **idoneidad del proceso seguido**, desde el planteamiento de la pregunta o hipótesis hasta el resultado final, con las debidas justificaciones.
- Se tendrá también en cuenta la **narrativa del caso**, es decir, que seáis capaces de explicar el trabajo realizado, desde la elección de la API hasta la conclusión final, de tal forma que quede enmarcado en un trabajo que tenga sentido en su conjunto y que resulte accesible a sus lectores. Se trata de analizar con sentido y saber comunicar, por lo que la redacción también tiene cierto peso.
- La **profundidad o complejidad** de la hipótesis es lo menos relevante. Lo importante es que sigáis un proceso completo y lleguéis a alguna conclusión relevante sobre la hipótesis planteada.

**FECHA LÍMITE**: El trabajo final, que responderá al menos a los 5 puntos anteriores, debe entregarse por el Aula Virtual antes del 28 de diciembre a las 23:59h.

---

**Instalación de paquetes en R**

```r
install.packages("tidyverse")
install.packages("prob")
```

**Carga de librerías**

```r
library("prob")
library(tidyverse)
```

### **Ejercicio 1**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]]. [[01-Ciberseguridad/Herramientas/Modulo-de-python3-httpserver|Modulo de python3 httpserver]]. [[03-Desarrollo-Software/Distribuido/Apache-httpd|Apache httpd]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/Apache-Axis-Java-y-HTTP|Apache Axis Java y HTTP]]. [[02-Ciencias-Computacion/Matematicas/Aritmetica-modular/Teorema-Chino-de-los-Restos-CRT|Teorema Chino de los Restos CRT]].

```r
a = data.frame(c(rolldie(3, 8, makespace = TRUE)))
colnames(a) = c("tirada1", "tirada2", "tirada3", "probs")
t = subset(a, ((tirada1 == 2) | (tirada3 == 5)))
paste("Esta es la probabilidad de tener un 2 en la tirada 1 y un 5 en la tirada 3:", (sum(t$probs)))

p = c(a$tirada1 + a$tirada2 + a$tirada3)
j = subset(a, (p > 15))
paste("Esta es la probabilidad de que la suma sea mayor de 15:", (length(j$tirada1) / length(a)))
```

### **Ejercicio 2**

```r
nsamp(nsamp(13, 6), 26) * 7
```

### **Ejercicio 3**

**a)**

```r
dbinom(60, 100, 0.60)
```

**b)**

```r
z = (pbinom(60, 100, 0.60, lower.tail = FALSE))
vendedor1 = (pbinom(70, 100, 0.60, lower.tail = FALSE))
vendedor2 = (pbinom(70, 200, 0.40, lower.tail = FALSE))
vendedor3 = (pbinom(70, 400, 0.20, lower.tail = FALSE))
paste("El mejor vendedor debido a su eficacia global es el vendedor 2 porque tiene una probabilidad de vender al menos 70 productos de: ", round(vendedor2 * 100, 2), "%")
```

### **Ejercicio 4**

**a)**

```r
v1 <- group_by(champions, by = Champion)
summarise(v1, n(), sum(Resultado == 1) / (sum(Resultado == 1) + sum(Resultado == 0)) * 100)
```

**b) y c)**

```r
summarise(v1, n(), sd(Resultado))
summarise(v1, n(), mean(Resultado))
cait = -dnorm(0, mean = 0.833, sd = 0.389) + pnorm(3, mean = 0.833, sd = 0.389)
ezreal = -dnorm(0, mean = 0.267, sd = 0.458) + pnorm(3, mean = 0.267, sd = 0.458)
paste("El campeón con más probabilidad de promocionar es Cait con una probabilidad de ganar de:", round(cait * 100, 2), "y la probabilidad de promocionar con el peor, que es Ezreal, es de:", round(ezreal * 100, 2))
```

### **Ejercicio 5**

**a)**

```r
probs1 = c(rnorm(100, mean = 0, sd = 1))
probs2 = c(rnorm(100, mean = 0, sd = 2))
probs3 = c(rnorm(100, mean = 2, sd = 1))
dis1 = data.frame(cbind(probs1))
dis2 = data.frame(cbind(probs2))
dis3 = data.frame(cbind(probs3))
```

**b)**

```r
hist(probs1)
hist(probs2)
hist(probs3)
```

**c)**

```r
dnorm(1, mean = 0, sd = 1)
dnorm(1, mean = 0, sd = 2)
dnorm(1, mean = 2, sd = 1)
```

**d)**

```r
pnorm(2, mean = 0, sd = 1, lower.tail = F)
pnorm(2, mean = 0, sd = 2, lower.tail = F)
pnorm(2, mean = 2, sd = 1, lower.tail = F)
```

---

Este formato hace que el contenido esté más organizado y sea más fácil de seguir. Cada ejercicio está claramente separado y los resultados de los ejercicios están ubicados justo debajo de su enunciado correspondiente.