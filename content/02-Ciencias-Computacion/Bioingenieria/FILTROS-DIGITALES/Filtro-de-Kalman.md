---
title: "Filtro De Kalman"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - filtros-digitales
---


El **filtro de Kalman** es un algoritmo recursivo de estimación óptima que combina **mediciones ruidosas** con un **modelo matemático** del sistema para estimar el estado real de un proceso en cada instante de tiempo.  
Se basa en un modelo de **espacio de estados** y en la teoría de estimación estadística, siendo óptimo cuando el ruido es **gaussiano** y el sistema es **lineal**.

---

## 1. Modelo de espacio de estados


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Forense/guia/Acceso-y-analisis-de-memoria-en-Linux-y-Windows|Acceso y analisis de memoria en Linux y Windows]].

El sistema se modela con dos ecuaciones:

1. **Ecuación de estado** (evolución del sistema):
$$
\mathbf{x}_k = \mathbf{F}_k \mathbf{x}_{k-1} + \mathbf{B}_k \mathbf{u}_k + \mathbf{w}_k
$$

2. **Ecuación de observación** (medición):
$$
\mathbf{z}_k = \mathbf{H}_k \mathbf{x}_k + \mathbf{v}_k
$$

Donde:
- \( \mathbf{x}_k \) → vector de estado en el instante \( k \).
- \( \mathbf{F}_k \) → matriz de transición de estados.
- \( \mathbf{B}_k \) → matriz de control.
- \( \mathbf{u}_k \) → vector de control.
- \( \mathbf{z}_k \) → vector de medición.
- \( \mathbf{H}_k \) → matriz de observación.
- \( \mathbf{w}_k \) → ruido de proceso (\( \mathcal{N}(0, Q_k) \)).
- \( \mathbf{v}_k \) → ruido de medición (\( \mathcal{N}(0, R_k) \)).

---

## 2. Algoritmo del filtro de Kalman

Se compone de dos fases: **predicción** y **actualización**.

### Predicción:
1. Estado predicho:
$$
\hat{\mathbf{x}}_{k|k-1} = \mathbf{F}_k \hat{\mathbf{x}}_{k-1|k-1} + \mathbf{B}_k \mathbf{u}_k
$$

2. Covarianza predicha:
$$
\mathbf{P}_{k|k-1} = \mathbf{F}_k \mathbf{P}_{k-1|k-1} \mathbf{F}_k^T + \mathbf{Q}_k
$$

---

### Actualización:
1. Ganancia de Kalman:
$$
\mathbf{K}_k = \mathbf{P}_{k|k-1} \mathbf{H}_k^T \left( \mathbf{H}_k \mathbf{P}_{k|k-1} \mathbf{H}_k^T + \mathbf{R}_k \right)^{-1}
$$

2. Estado actualizado:
$$
\hat{\mathbf{x}}_{k|k} = \hat{\mathbf{x}}_{k|k-1} + \mathbf{K}_k \left( \mathbf{z}_k - \mathbf{H}_k \hat{\mathbf{x}}_{k|k-1} \right)
$$

3. Covarianza actualizada:
$$
\mathbf{P}_{k|k} = \left( \mathbf{I} - \mathbf{K}_k \mathbf{H}_k \right) \mathbf{P}_{k|k-1}
$$

---

## 3. Características

- **Recursivo**: No necesita almacenar todas las mediciones anteriores.
- **Óptimo**: Si el sistema es lineal y el ruido es blanco gaussiano.
- **Rápido**: Adecuado para tiempo real.

---

## 4. Aplicaciones en señales biomédicas

- **ECG**: Eliminación de ruido en la línea base manteniendo morfología de la señal.
- **EEG**: Filtrado de artefactos preservando ondas cerebrales.
- **HRV**: Estimación suave de la frecuencia cardíaca instantánea.
- **Seguimiento de parámetros fisiológicos**: Estimación de presión arterial o glucosa.

---

## 5. Ventajas y limitaciones

**Ventajas**:
- Filtrado y predicción simultáneos.
- Adaptable a sistemas dinámicos.
- Robusto ante ruido gaussiano.

**Limitaciones**:
- Requiere conocer matrices \( Q_k \) y \( R_k \) correctamente.
- Menos efectivo si el sistema es altamente no lineal (en ese caso se usan EKF o UKF).
- Sensible a errores de modelado.

---

## 6. Ejemplo en MATLAB

```matlab
% Definición de matrices (ejemplo simple)
F = [1 1; 0 1];
H = [1 0];
Q = eye(2)*0.01;
R = 0.1;
x = [0; 1];
P = eye(2);

% Medición simulada con ruido
z = [0.9, 2.0, 3.1, 4.05, 5.0] + 0.1*randn(1,5);

for k = 1:length(z)
    % Predicción
    x = F*x;
    P = F*P*F' + Q;
    
    % Actualización
    K = P*H'/(H*P*H' + R);
    x = x + K*(z(k) - H*x);
    P = (eye(2) - K*H)*P;
    
    fprintf('Estado estimado en paso %d: %f %f\n', k, x(1), x(2));
end
