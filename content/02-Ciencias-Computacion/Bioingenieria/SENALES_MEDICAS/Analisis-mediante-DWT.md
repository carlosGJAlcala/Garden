---
title: "Análisis mediante DWT (Transformada Wavelet Discreta)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# Análisis mediante DWT (Transformada Wavelet Discreta)


> **Relacionado**: [[03-Desarrollo-Software/Concurrencia/Mecanismos/Monitores|Monitores]].

La **Transformada Wavelet Discreta** (DWT, *Discrete Wavelet Transform*) es una técnica de análisis de señales que descompone una señal en diferentes **niveles de resolución** o **bandas de frecuencia**.  
A diferencia de la **CWT** (Transformada Wavelet Continua), que analiza la señal en todos los desplazamientos y escalas posibles, la DWT utiliza un **conjunto discreto de escalas y traslaciones**, lo que la hace **computacionalmente más eficiente** y adecuada para procesamiento digital.

En el contexto de **señales biomédicas** (ECG, EEG, EMG), la DWT es especialmente útil para la **compresión, eliminación de ruido y detección de patrones**.

---

## 1. Fundamento teórico

La DWT representa una señal \( x(t) \) como una combinación de funciones **wavelet** y **de escalamiento**:

$$
x(t) = \sum_{k} a_{j_0, k} \, \varphi_{j_0, k}(t) \;+\; \sum_{j=j_0}^{J} \sum_{k} d_{j, k} \, \psi_{j, k}(t)
$$

Donde:  
- \( \varphi_{j_0, k}(t) \): funciones de escalamiento (aproximación).  
- \( \psi_{j, k}(t) \): funciones wavelet (detalles).  
- \( a_{j_0, k} \): coeficientes de aproximación.  
- \( d_{j, k} \): coeficientes de detalle.  
- \( j \): nivel de descomposición.  
- \( k \): índice de traslación.

---

## 2. Proceso de análisis

La DWT se implementa de forma eficiente mediante **bancos de filtros**:

1. **Filtro paso bajo (LPF)**: extrae la información de baja frecuencia (aproximaciones).  
2. **Filtro paso alto (HPF)**: extrae la información de alta frecuencia (detalles).  
3. **Diezmado (downsampling)**: reducción del número de muestras a la mitad tras cada filtrado.

Este proceso se repite recursivamente sobre la salida de baja frecuencia, generando una **estructura piramidal de descomposición**.

---

## 3. Ventajas frente a CWT

- **Menor coste computacional**: trabaja con un conjunto discreto de escalas y desplazamientos.  
- **Eficiencia en compresión**: ideal para reducir el tamaño de señales y mantener la información esencial.  
- **Capacidad de filtrado**: permite eliminar ruido sin distorsionar eventos importantes.  
- **Adecuada para tiempo real**: se usa en monitores y sistemas embebidos.

---

## 4. Aplicaciones en señales médicas

- **ECG**: eliminación de artefactos de línea base y detección automática de complejos QRS.  
- **EEG**: identificación de picos epilépticos y análisis de ritmos cerebrales.  
- **EMG**: filtrado de ruido y segmentación de contracciones musculares.  
- **Compresión**: reducción del tamaño de registros médicos manteniendo características relevantes.

---

## 5. Ejemplo práctico en ECG

1. **Nivel 1**: eliminación de ruido de alta frecuencia (artefactos musculares).  
2. **Nivel 2**: filtrado de interferencia de red (50/60 Hz).  
3. **Nivel 3 y superiores**: aislamiento de ondas P, QRS y T.  

Mediante umbralización (*thresholding*) de los coeficientes de detalle, se puede suprimir el ruido y reconstruir la señal limpia con la **Transformada Inversa Wavelet Discreta (IDWT)**.

---
