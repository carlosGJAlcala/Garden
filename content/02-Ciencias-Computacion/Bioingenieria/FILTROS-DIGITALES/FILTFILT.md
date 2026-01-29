---
title: "FILTFILT – Filtrado sin desfase de fase"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - filtros-digitales
---
# FILTFILT – Filtrado sin desfase de fase

La función **`filtfilt`** implementa un **filtrado hacia adelante y hacia atrás** (*forward-backward filtering*) que elimina el **desfase de fase** introducido por un filtro digital.  
Esto es importante porque un filtrado causal convencional desplaza en el tiempo la señal procesada, lo que puede distorsionar eventos temporales críticos (por ejemplo, el complejo QRS en un ECG).

---

## 1. Principio de funcionamiento

En un filtrado digital causal convencional:
$$
y(n) = h(n) * x(n)
$$
la fase del filtro puede desplazar la señal.  
`filtfilt` corrige este efecto aplicando el filtro dos veces:
1. **Filtrado hacia adelante**: procesa la señal en su orden normal.
2. **Inversión temporal**: se invierte la señal resultante.
3. **Filtrado hacia atrás**: se vuelve a filtrar la señal invertida.
4. **Inversión final**: se devuelve al orden original.

Matemáticamente:
$$
y_{\text{filtfilt}}(n) = \text{reverse} \left[ \text{filter} \left( h, \text{reverse} \left[ \text{filter}(h, x) \right] \right) \right]
$$

---

## 2. Propiedades

- **Magnitud**: La respuesta en magnitud final es el cuadrado de la magnitud original del filtro:
$$
|H_{\text{filtfilt}}(e^{j\omega})| = |H(e^{j\omega})|^2
$$

- **Fase**: La fase es **cero** (lineal de pendiente nula), lo que significa que **no hay retraso de grupo**.

- **Orden efectivo**: El orden del filtro se duplica, ya que se aplica dos veces.

---

## 3. Ventajas

- Elimina completamente el **desfase temporal** introducido por el filtrado.
- Mantiene la forma temporal de eventos críticos en la señal.
- Útil en aplicaciones donde la alineación temporal es esencial.

---

## 4. Limitaciones

- No es causal → no se puede usar en procesamiento en tiempo real.
- Duplica el coste computacional y la atenuación en magnitud.
- Requiere datos antes y después de la región de interés (puede generar artefactos en bordes si no hay datos suficientes).

---

## 5. Uso en MATLAB

```matlab
% Definición de un filtro paso bajo
[b, a] = butter(4, 0.2); % Butterworth de orden 4

% Señal de entrada (ECG con ruido)
load ecg_signal

% Filtrado sin desfase de fase
y = filtfilt(b, a, ecg_signal);

% Comparación visual
plot(ecg_signal); hold on;
plot(y, 'LineWidth', 2);
legend('Señal original', 'Filtrada sin desfase');
