---
title: "Representación de la HRV (Heart Rate Variability)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# Representación de la HRV (Heart Rate Variability)


> **Relacionado**: [[01-Ciberseguridad/Ingenieria-Inversa/MONA|MONA]].

La **Variabilidad de la Frecuencia Cardíaca** (*Heart Rate Variability*, HRV) es una medida de las variaciones en los intervalos entre latidos consecutivos del corazón, normalmente medidos como intervalos **R-R** en un electrocardiograma (ECG).  
La HRV es un indicador no invasivo del equilibrio entre el **sistema nervioso simpático** y el **sistema nervioso parasimpático**.

---

## 1. Obtención de la señal HRV

1. **Registro de ECG**: Adquisición de la señal con suficiente resolución temporal.
2. **Detección de picos R**: Uso de algoritmos como Pan–Tompkins para localizar los máximos del complejo QRS.
3. **Cálculo de intervalos R-R**:  
   $$
   RR_i = t_{R_{i+1}} - t_{R_i}
   $$
   donde \( t_{R_i} \) es el instante del pico R número \( i \).
4. **Interpolación y re-muestreo**: Transformación de la serie irregular de intervalos en una señal continua para análisis espectral.

---

## 2. Métodos de representación

La HRV se puede representar y analizar en **dominio temporal** y **dominio frecuencial**:

### 2.1 Dominio temporal
- **Gráfico de intervalos R-R**: Representa en el eje X el número de latido y en el eje Y la duración del intervalo \( RR_i \).
- **Diagrama de Poincaré**: Gráfico de dispersión donde se representa \( RR_{i+1} \) frente a \( RR_i \), permitiendo analizar la variabilidad y detectar patrones.
- **Métricas comunes**:
  - \( SDNN \): Desviación estándar de todos los intervalos R-R.
  - \( RMSSD \): Raíz cuadrada de la media de las diferencias cuadráticas sucesivas.

$$
SDNN = \sqrt{\frac{1}{N-1} \sum_{i=1}^{N} (RR_i - \overline{RR})^2}
$$

$$
RMSSD = \sqrt{\frac{1}{N-1} \sum_{i=1}^{N-1} (RR_{i+1} - RR_i)^2}
$$

---

### 2.2 Dominio frecuencial
El análisis frecuencial se realiza aplicando transformadas (FFT, Lomb-Scargle, Wavelet) para obtener la **densidad espectral de potencia** (PSD) de la señal HRV.

Bandas típicas:
- **ULF** (< 0.003 Hz) – Ritmos muy lentos, asociados a ritmos circadianos.
- **VLF** (0.003 – 0.04 Hz) – Regulación térmica y hormonal.
- **LF** (0.04 – 0.15 Hz) – Actividad simpática y parasimpática.
- **HF** (0.15 – 0.4 Hz) – Actividad parasimpática, asociada a la respiración.

Representación:
- **Espectro de potencia**: Eje X → frecuencia, Eje Y → potencia (ms²/Hz).
- **Cociente LF/HF**: Índice del balance simpático-parasimpático.

---

## 3. Visualizaciones comunes

1. **Serie temporal de intervalos R-R**: útil para ver variaciones globales.
2. **Poincaré plot**: identifica patrones regulares o caóticos.
3. **Espectrograma tiempo-frecuencia**: permite ver la evolución de LF y HF en el tiempo.
4. **Escalograma Wavelet**: representa la energía de la HRV a diferentes escalas.

---

## 4. Aplicaciones clínicas

- Evaluación del **estrés** y la **fatiga**.
- Monitorización de pacientes con **arritmias** o **disfunción autonómica**.
- Detección temprana de alteraciones cardiovasculares.
- Seguimiento de deportistas para optimizar entrenamiento y recuperación.
