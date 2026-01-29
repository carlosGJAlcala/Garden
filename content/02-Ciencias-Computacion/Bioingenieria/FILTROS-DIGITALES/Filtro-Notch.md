---
title: "Filtro Notch (Filtro Rechaza-Banda)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - filtros-digitales
---
# Filtro Notch (Filtro Rechaza-Banda)


> **Relacionado**: [[02-Ciencias-Computacion/Bioingenieria/FILTROS-DIGITALES/FILTFILT|FILTFILT]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Un **filtro notch** o **filtro rechaza-banda estrecha** es un filtro digital o analógico diseñado para **atenuar fuertemente una frecuencia específica** y dejar pasar el resto del espectro sin grandes alteraciones.  
En procesamiento digital de señales biomédicas, se usa principalmente para **eliminar interferencias de red eléctrica** (50 Hz o 60 Hz) en registros como ECG, EEG o EMG.

---

## 1. Principio de funcionamiento

Un filtro notch tiene una **banda de rechazo muy estrecha** centrada en una frecuencia \( f_0 \).  
Su función de transferencia típica en el dominio \( z \) para un filtro IIR de segundo orden es:

$$
H(z) = \frac{1 - 2\cos(\omega_0) z^{-1} + z^{-2}}{1 - 2r\cos(\omega_0) z^{-1} + r^2 z^{-2}}
$$

Donde:
- \( \omega_0 = \frac{2\pi f_0}{f_s} \) → frecuencia normalizada.
- \( f_0 \) → frecuencia a eliminar.
- \( f_s \) → frecuencia de muestreo.
- \( r \) → factor de selectividad (0 < r < 1, cuanto más cercano a 1, más estrecha la banda de rechazo).

---

## 2. Características

- **Banda de rechazo** centrada en \( f_0 \) con ancho controlado por \( r \).
- **Atenuación alta** en la frecuencia objetivo (idealmente infinita).
- Puede implementarse como:
  - Filtro FIR (fase lineal, pero orden más alto).
  - Filtro IIR (menor orden, más eficiente).

---

## 3. Ejemplo en MATLAB

```matlab
% Parámetros
fs = 500;          % Frecuencia de muestreo (Hz)
f0 = 50;           % Frecuencia a eliminar (Hz)
wo = f0/(fs/2);    % Frecuencia normalizada (Nyquist)
bw = wo/35;        % Ancho de banda relativo

% Diseño de filtro notch IIR
[b, a] = iirnotch(wo, bw);

% Filtrado de señal ECG con ruido de 50 Hz
y = filtfilt(b, a, ecg_signal);

% Visualización
plot(ecg_signal); hold on;
plot(y, 'LineWidth', 2);
legend('Señal original', 'Filtrada (Notch)');``
```
## 4. Aplicaciones en biomédica

- **ECG**: Eliminación de interferencia de red sin distorsionar las ondas P, QRS y T.
    
- **EEG**: Eliminación de ruido eléctrico en registros cerebrales.
    
- **EMG**: Filtrado de 50/60 Hz sin afectar armónicos de interés.
    

---

## 5. Respuesta en frecuencia

La respuesta en frecuencia de un filtro notch ideal puede representarse como:

$$∣H(ejω)∣={0,ω=ω01,ω≠ω0|H(e^{j\omega})| = \begin{cases} 0, & \omega = \omega_0 \\ 1, & \omega \neq \omega_0 \end{cases}∣H(ejω)∣={0,1,​ω=ω0​ω=ω0​​$$
En la práctica, la atenuación en ω0\omega_0ω0​ es finita y la transición alrededor de la frecuencia de rechazo depende de rrr.

---

## 6. Consideraciones

- **Si r → 1** → rechazo muy estrecho, pero respuesta más lenta (puede introducir oscilaciones).
    
- **Si r pequeño** → rechazo más ancho, riesgo de eliminar frecuencias adyacentes útiles.
    
- Ideal para eliminar una frecuencia fija y conocida.