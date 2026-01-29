---
title: "suma de valores"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - r
---

**PRÁCTICA 1: Análisis de Estadística Descriptiva**

En esta práctica se va a realizar un análisis de estadística descriptiva sobre los datos contenidos en un dataset. El conjunto de datos con el que trabajaremos, **Motor Trend Car Road Tests**, contiene información extraída de la revista _Motor Trend US_ de 1974, y comprende el consumo de combustible y 10 aspectos del diseño y rendimiento de 32 modelos de automóviles de los años 1973-1974.

En R, como parte del paquete **“datasets”**, hay una copia parcial de este dataset denominada **“mtcars”** lista para utilizarse. Utilizaremos esta copia para la práctica.
```r
View(mtcars)
n=length(mtcars$mpg)
install.packages("modeest")
i
```
### **Pasos a seguir en la práctica:**


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

**1. Tamaño muestral y la suma de todos los valores de la variable consumo (mpg)**

- Obtener el tamaño muestral de la variable **mpg**.
- Calcular la suma de todos los valores de **mpg**.
```r
paste("El tamaño muestral es: ", length(mtcars$cyl))
# suma de valores
paste("EL consumo total de todos los modelos es de:", sum(mtcars$mpg))

```
**2. Cálculo de las medias aritmética y geométrica de la variable consumo (sin usar la función “mean”)**

- Calcular la **media aritmética** de **mpg**.
- Calcular la **media geométrica** de **mpg**.
```r
consumo = sum(mtcars$mpg)/length(mtcars$mpg)
paste("la media aritmética del consumo es:", consumo)
paste("La media geométrica del consumo es: ", prod(mtcars$mpg)**(1/32))

```
**3. Obtener y mostrar por pantalla la media aritmética y la mediana de la variable consumo utilizando funciones internas de R.**
```r
paste("la media aritmetica es:", mean(mtcars$mpg), "y la mediana es:", median(mtcars$mpg))

```
**4. Almacenar en un vector las desviaciones de la media de todos los elementos de la variable consumo.**
```r

```
**5. Calcular la desviación típica y la varianza de la variable consumo sin utilizar funciones estadísticas internas de R (utilizando el vector de desviaciones).**
```r
v = c(mtcars$mpg)
v2 = v - consumo
varianza=(sum((mtcars$mpg-consumo)**2)/n)
paste("la desviación típica es: ", varianza**(1/2) , "y la varianza es: ", varianza)

```
**6. Utilizar funciones estadísticas de R para calcular y mostrar la desviación típica y la varianza de la variable consumo.**

- Comparar los resultados con los obtenidos en el paso 5 y comentar.
```r
paste("La desviación típica según R es:",sd(mtcars$mpg))
paste("La desviación típica según R es:",var(mtcars$mpg))
paste("Esto se debe a que R utiliza la formula para calcular la desviación y la varianza en muestras de poblaciones, y estas utilizan N-1 en lugar de N, para añadir cierto margen de error al estudio")

```
**7. Calcular la moda de las variables número de cilindros (cyl) y número de marchas (gear).**
```r
paste("La moda del nº de cilindros es:", modeest::mfv(mtcars$cyl), "y la moda del nº de marchas es:", modeest::mfv(mtcars$gear))

```
**8. Calcular el rango y la amplitud de la variable consumo (mpg).**
```r
paste("El rango del cunsumo es", range(mtcars$mpg))
paste("y la amplitud es: ", max(mtcars$mpg)-min(mtcars$mpg))
```
**9. Calcular los cuartiles de la variable consumo (mpg).**
```r
paste("Los cuartiles del consumo son: ", quantile(mtcars$mpg, .25), "," , quantile(mtcars$mpg, .50), ",", quantile(mtcars$mpg, .75), ".")

```
**10. Calcular los percentiles 47, 54 y 82 de la variable consumo (mpg).**
```r
paste("Los cuantiles 47,54 y 82 del consumo son: ", quantile(mtcars$mpg, .47), "," , quantile(mtcars$mpg, .54), ",", quantile(mtcars$mpg, .82), ".")

```
**11. Crear el histograma de frecuencias absolutas y absolutas acumuladas para la variable consumo (mpg).**
```r
(hist(mtcars$mpg))
plot.ecdf(mtcars$mpg)
```
**12. Cargar un nuevo dataset completo, con información de 155 automóviles en lugar de los 32 del dataset “mtcars”.**  
Para ello, cargar el dataset desde un archivo CSV con el siguiente código:

```r
cardata <- read.csv(file="cardata.csv", header=TRUE, sep=";")
```


```r
cardata <- read.csv(file = "cardata(2)(2)", header = TRUE, sep=";")

paste("El tamaño muestral es: ", length(cardata$mpg))
paste("La media es: ", mean(cardata$mpg, na.rm = TRUE))
paste("La mediana es: ", median(cardata$mpg, na.rm = TRUE))
```
**13. Utilizando el nuevo dataset (`cardata`), calcular:**

- El tamaño muestral.
- La media de la variable **mpg**.
- La mediana de la variable **mpg**.
```r

```
