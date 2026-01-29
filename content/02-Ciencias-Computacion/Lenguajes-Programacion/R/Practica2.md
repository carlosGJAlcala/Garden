---
title: "hay q mirar la moda"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - r
---
```r
#install.packages("dplyr")
#install.packages("modeest")
#install.packages("ggplot2")
#install.packages("tidyverse")
library("tidyverse")
library("ggplot2")
library("modeest")
library("dplyr")

#ejercicio 1
absoluta= c(table(cardata$mpg))
relativo= hist(cumsum(cardata$mpg))
relativa=prop.table(mtcars$mpg[-108])
tabla = data.frame (cbind(absoluta,relativa))

#ejercicio 2
tabla2= table(cut(cardata$mpg, 10))
tablaabsoluta2= data.frame(cbind(tabla2))
d=c(cardata$mpg)
hist(d,10)

#ejercicio 3
paste("esta es la moda",mfv(cardata$mpg))
paste("esta es la moda del desplazamiento", mfv(cardata$disp))
# hay q mirar la moda

#ejercicio 4
origen= c(cardata$origin)
paste("la media es: ", mean(origen), "y la mediana es: ",median(origen),"(3 es USA, 2 es UE,y 1 es ASIA)")

#ejercicio 5
estudio= group_by(cardata,by=cardata$origin)
summarise(estudio,n(),max(na.omit(horsepower)-min(na.omit(horsepower))))

estudio2=group_by(cardata,by=cardata$origin)
summarise(estudio2,n(),mean(na.omit(horsepower)))

#ejercicio 6
#consumo es y; potencia es x
potencia=  sum(cardata$horsepower [-52][-72][-100][-103])
consumo= (sum(cardata$mpg[-108]))
mediaconsumo <- (sum(cardata$mpg[-108]))/(length(cardata$mpg[-108]))
mediapotencia <- sum(cardata$horsepower [-52][-72][-100][-103])/(length(cardata$origin)-4)

varianzaconsumo <- ((sum (cardata$mpg[-108])**2)/length(cardata$mpg [-108]))-(mediaconsumo**2)
varianzapotencia <- ((sum(cardata$horsepower [-52][-72][-100][-103])**2)/length(cardata$origin)-4)-(mediapotencia**2)

covarianza <- (1/length(cardata$origin))*(potencia*mediapotencia)*(consumo*mediaconsumo)

# la formula de la recta regresion ser  

y=  mediaconsumo+(covarianza/varianzapotencia)
x= -mediapotencia
paste ("y=",y,x,"x")
 
#Ejercicio 7
regresion <- lm(cardata$mpg~cardata$horsepower)
summary(regresion)

#Ejercicio 8
plot(cardata$horsepower, cardata$mpg, xlab = "Potencia del motor", ylab = "Consumo")
abline(regresion, col = "red")

# ejercicio 9

nuevoconsumo= c(cardata$mpg[-108])*235.21
plot(nuevoconsumo,cardata$horsepower)
regresionconsumo = lm(nuevoconsumo~cardata$horsepower[-52][-72][-100][-103])
summary(regresion)


#Ejercicio 10

accel_mpg = cor(cardata_2_2_$accel,cardata_2_2_$mpg, use ="pairwise.complete.obs", method = c("pearson"))
weight_mpg = cor(cardata_2_2_$accel,cardata_2_2_$weight, use ="pairwise.complete.obs",method = c("pearson"))
price_mpg = cor(cardata_2_2_$price,cardata_2_2_$mpg, use ="pairwise.complete.obs",method = c("pearson"))

paste("La correlaci n entre la aceleraci n y el consumo es: ", accel_mpg, ". ")
paste("La correlaci n entre el peso y el consumo es: ", weight_mpg)
paste("La correlaci n entre el precio del veh culo y el consumo es: ", price_mpg)

#Ejercicio 11

paste("La correlaci n entre la aceleraci n y el consumo (0.227), aunque no muy alta, muestra que en efecto hay relaci n entre aceleraci n y consumo, y que a mayor consumo, mayor aceleraci n.")
paste("La correlaci n entre el precio y el consumo (-0.0009), no es lo suficientemente distinta de cero como para poder asumir que exista una relaci n entre ambas variables")
paste("Finalmente, la correlaci n entre el peso y consumo (-0.046), tampoco es lo suficientemente distinta de 0 como para poder asumir que exsista relaci n")

# ejercicio 12

plot(cardata$mpg, cardata$weight)
as= lm(cardata$weight~cardata$mpg)
abline(as)
t.test(cardata$mpg)
t.test(cardata$weight)
```