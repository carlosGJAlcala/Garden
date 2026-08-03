---
title: "Filtro LMS (Least Mean Squares) en DSP"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - filtros-digitales
---
# Filtro LMS (Least Mean Squares) en DSP

El **filtro LMS** (*Least Mean Squares*) es un filtro adaptativo ampliamente utilizado en **procesamiento digital de señales (DSP)**.  
Su objetivo es ajustar dinámicamente sus coeficientes para **minimizar el error cuadrático medio** entre la salida del filtro y una señal deseada de referencia.


Se emplea en aplicaciones como:
- Eliminación de ruido adaptativa (ANC).
- Cancelación de eco.
- Predicción de señales.
- Procesamiento de señales biomédicas (ECG, EEG).

---

## 1. Principio de funcionamiento

El algoritmo LMS se basa en el **descenso de gradiente estocástico** para actualizar los coeficientes del filtro en cada instante de tiempo.

Sea:
- \( x(n) \): señal de entrada.
- \( d(n) \): señal deseada (referencia).
- \( y(n) \): salida del filtro.
- \( e(n) = d(n) - y(n) \): señal de error.
- \( \mathbf{w}(n) \): vector de coeficientes del filtro adaptativo.
- \( \mu \): paso de adaptación (*step size*).

---

## 2. Ecuaciones del algoritmo LMS

1. **Salida del filtro FIR adaptativo**:
$$
y(n) = \mathbf{w}^T(n) \, \mathbf{x}(n)
$$
donde:
$$
\mathbf{x}(n) = [x(n), x(n-1), \dots, x(n-M+1)]^T
$$

2. **Cálculo del error**:
$$
e(n) = d(n) - y(n)
$$

3. **Actualización de coeficientes**:
$$
\mathbf{w}(n+1) = \mathbf{w}(n) + \mu \, e(n) \, \mathbf{x}(n)
$$

---

## 3. Parámetros clave

- **Paso de adaptación (\(\mu\))**:  
  Controla la velocidad y estabilidad de la convergencia.  
  Para estabilidad, se debe cumplir:
  $$
  0 < \mu < \frac{1}{\lambda_{\text{max}}}
  $$
  donde \( \lambda_{\text{max}} \) es el mayor valor propio de la matriz de autocorrelación de \( x(n) \).

- **Número de coeficientes (M)**:  
  Determina la capacidad de modelado del filtro.  
  Un valor mayor → mayor precisión pero más coste computacional.

---

## 4. Ventajas y limitaciones

**Ventajas**:
- Implementación sencilla.
- Bajo coste computacional.
- Adaptativo, funciona en entornos variables.

**Limitaciones**:
- Convergencia más lenta que algoritmos como **RLS**.
- Sensible a la elección de \(\mu\).
- Rendimiento limitado si la señal tiene gran correlación.

---

## 5. Aplicaciones en señales biomédicas

- **ECG**: Eliminación de interferencia de red (50/60 Hz) usando una referencia sinusoidal.
- **EEG**: Cancelación de artefactos oculares (EOG) a partir de canales de referencia.
- **EMG**: Filtrado de interferencias de baja y alta frecuencia adaptativamente.
Con el LMS, conseguimos sacar la el ecg fetal, ya que el LMS es un cancelador de ruido y a partir de la señal del tórax con la del abdomen podemos quitarle el ruido a la señal de la madre, que dicho ruido se va a componer principalmente por el ecg fetal, sumándole una pequeña parte del ruido aleatorio que hemos generado anteriormente.
---

## 6. Diagrama de bloques del filtro LMS

Entrada \( x(n) \) → Filtro FIR adaptativo → Salida \( y(n) \)  
\(\quad\) ↘ Comparación con \( d(n) \) → Error \( e(n) \) → Actualización de \( \mathbf{w}(n) \)

---
![[assets/Pasted image 20250808214641.png]]

## Función de transferencia del filtro LMS

En un **filtro adaptativo LMS**, la **función de transferencia** no es fija, ya que los coeficientes del filtro cambian en el tiempo según la regla de adaptación.  
Sin embargo, en un instante dado \( n \), el filtro LMS se comporta como un **filtro FIR** con una función de transferencia definida por:

$$
H_n(z) = \sum_{k=0}^{M-1} w_k(n) \, z^{-k}
$$

Donde:
- \( M \): número de coeficientes (orden del filtro + 1).  
- \( w_k(n) \): coeficiente adaptativo en el instante \( n \).  
- \( z^{-k} \): retardo discreto en el dominio \( z \).

---

## 1. Relación entrada-salida en el dominio \( z \)

Si la señal de entrada es \( X(z) \) y la salida es \( Y(z) \), para un instante fijo \( n \):

$$
Y(z) = H_n(z) \cdot X(z)
$$

Como \( H_n(z) \) cambia con \( n \), el filtro es **tiempo-variantes** (*time-varying system*).

---

## 2. Interpretación

- Si los coeficientes \( w_k(n) \) convergen a valores estables, \( H_n(z) \) tiende a la **función de transferencia óptima** que minimiza el error cuadrático medio.
- Antes de la convergencia, \( H_n(z) \) evoluciona en cada iteración, adaptándose a las características de la señal y la referencia.

---

## 3. Caso particular: filtro FIR adaptativo

Cuando el LMS ha convergido, el filtro puede considerarse **invariante en el tiempo**, y su función de transferencia final será:

$$
H(z) = \sum_{k=0}^{M-1} w_k \, z^{-k}
$$

Donde \( w_k \) son los coeficientes finales después de la adaptación.

---

## 4. Nota sobre estabilidad

La estabilidad del filtro LMS depende del **paso de adaptación** (\( \mu \)), no de la función de transferencia fija, ya que el sistema es adaptativo.  
La condición típica es:

$$
0 < \mu < \frac{1}{\lambda_{\text{max}}}
$$

siendo \( \lambda_{\text{max}} \) el mayor valor propio de la matriz de autocorrelación de la entrada.

---
