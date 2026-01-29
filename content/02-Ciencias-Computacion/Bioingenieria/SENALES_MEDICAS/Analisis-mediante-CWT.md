---
title: "Análisis mediante CWT (Transformada Wavelet Continua)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# Análisis mediante CWT (Transformada Wavelet Continua)

La **Transformada Wavelet Continua** (CWT, *Continuous Wavelet Transform*) es una herramienta matemática utilizada para analizar señales **no estacionarias**, es decir, aquellas cuya composición en frecuencia varía con el tiempo. A diferencia de la Transformada de Fourier, que solo muestra el contenido global de frecuencia, la CWT proporciona **información temporal y frecuencial simultáneamente**.

En el análisis de **señales biomédicas** como ECG, EEG o EMG, la CWT es especialmente útil para detectar eventos transitorios, picos y cambios bruscos que no serían evidentes con métodos espectrales tradicionales.

---

## 1. Fundamento teórico

La CWT se basa en comparar la señal \( x(t) \) con una **wavelet madre** \( \psi(t) \), la cual se desplaza (*traslación*) y se escala (*dilatación* o *compresión*).

La expresión matemática de la CWT es:

$$
C(a, b) = \frac{1}{\sqrt{|a|}} \int_{-\infty}^{\infty} x(t) \, \psi^*\left(\frac{t - b}{a}\right) dt
$$

Donde:  
- \( a \): parámetro de escala (inversamente proporcional a la frecuencia).  
- \( b \): parámetro de traslación (posición temporal).  
- \( \psi(t) \): wavelet madre.  
- \( C(a, b) \): coeficientes que indican la similitud entre la señal y la wavelet.  
- \( ^* \): conjugado complejo.

---

## 2. Proceso de análisis

1. **Selección de la wavelet madre**:  
   - Morlet → Alta resolución frecuencial, útil para señales oscilatorias.  
   - Mexican Hat (Ricker) → Detección de picos y transitorios.  
   - Daubechies → Ideal para cambios bruscos en la señal.

2. **Escalado y desplazamiento**:  
   - Escalas pequeñas → Alta frecuencia (buena resolución temporal).  
   - Escalas grandes → Baja frecuencia (buena resolución frecuencial).

3. **Cálculo de coeficientes**: Cada coeficiente \( C(a, b) \) indica cuánta energía de la señal coincide con la wavelet en un instante y frecuencia determinados.

4. **Representación tiempo-frecuencia**: Se obtiene un **escalograma**, con:  
   - Eje horizontal → Tiempo.  
   - Eje vertical → Escala o frecuencia.  
   - Intensidad de color → Magnitud de \( C(a, b) \).

---

## 3. Ventajas en señales médicas

- Detección precisa de **eventos transitorios** como arritmias, picos epilépticos o artefactos musculares.
- Alta resolución temporal en altas frecuencias y alta resolución frecuencial en bajas frecuencias.
- Especialmente adecuada para **señales no estacionarias**.
- Posibilidad de filtrado selectivo y detección de patrones.

---

## 4. Ejemplo en electrocardiografía (ECG)

En un ECG, la CWT permite:
- Detectar con precisión el complejo QRS incluso en presencia de ruido.
- Analizar variaciones en ondas P y T.
- Estudiar la dinámica de la frecuencia cardíaca en situaciones clínicas diversas.
