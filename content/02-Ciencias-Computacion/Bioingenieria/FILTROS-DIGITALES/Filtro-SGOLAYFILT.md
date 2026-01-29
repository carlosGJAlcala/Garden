---
title: "Filtro SGOLAYFILT (Savitzky–Golay)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - filtros-digitales
---
# Filtro SGOLAYFILT (Savitzky–Golay)


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

La función **`sgolayfilt`** implementa un **filtro de Savitzky–Golay**, que es un método de **suavizado y diferenciación de señales** basado en **ajuste polinomial por mínimos cuadrados** dentro de una ventana deslizante.  
A diferencia de un filtro paso bajo tradicional, el filtro Savitzky–Golay preserva mejor la forma de las señales, especialmente la amplitud y anchura de picos.

En MATLAB, `sgolayfilt` se utiliza comúnmente para:
- Reducir ruido en señales sin distorsionar picos.
- Calcular derivadas suavizadas.
- Procesar datos biomédicos (ECG, EEG, espectros de HRV, etc.).

---

## 1. Principio de funcionamiento

El método ajusta un polinomio de orden \( p \) a un conjunto de \( 2m+1 \) puntos alrededor de cada muestra \( x(n) \) mediante **mínimos cuadrados**, y utiliza el valor ajustado en el centro de la ventana como salida suavizada.

Sea:
- \( p \): orden del polinomio (típicamente 2–4).
- \( 2m+1 \): tamaño de la ventana (número de puntos usados en el ajuste).
- \( x(n) \): señal de entrada.
- \( y(n) \): señal filtrada.

El ajuste minimiza:
$$
\min_{\mathbf{a}} \sum_{k=-m}^{m} \left[ x(n+k) - \sum_{i=0}^{p} a_i \, k^i \right]^2
$$

donde \( a_i \) son los coeficientes del polinomio.

---

# Filtro Savitzky–Golay (`sgolayfilt`) – Explicación avanzada

El **filtro de Savitzky–Golay** es un método de **suavizado digital** que aplica un ajuste polinomial por **mínimos cuadrados** en una ventana deslizante, y utiliza el valor del polinomio ajustado en el punto central como la salida filtrada.  
A diferencia de un filtro paso bajo FIR tradicional, el Savitzky–Golay **reduce el ruido preservando la forma y altura de picos**, lo que lo hace ideal para señales donde la geometría de las ondas es importante.

---

## 1. Origen y fundamento teórico

Este filtro fue propuesto por Abraham Savitzky y Marcel J.E. Golay en 1964 para suavizar datos espectroscópicos.  
La idea central es que un filtro promedio móvil convencional tiende a **aplanar picos y ensanchar formas**, mientras que un ajuste polinomial local:
- Suaviza el ruido.
- Mantiene la **altura y posición de los picos**.
- Preserva la **pendiente local**, lo que es útil si se desean calcular derivadas.

---

## 2. Proceso matemático

1. **Ventana deslizante**: Se elige una longitud \( L = 2m + 1 \) (impar).
2. **Ajuste polinomial**: En cada posición de la ventana, se ajusta un polinomio de orden \( p \) (típicamente \( 2 \leq p \leq 4 \)):

$$
P(k) = a_0 + a_1 k + a_2 k^2 + \dots + a_p k^p
$$

donde \( k \) va desde \( -m \) hasta \( +m \) alrededor del punto central.

3. **Minimización por mínimos cuadrados**:

$$
\min_{a_0, a_1, \dots, a_p} \sum_{k=-m}^{m} \left[ x(n+k) - P(k) \right]^2
$$

4. **Valor filtrado**: El valor suavizado en el instante \( n \) es \( P(0) = a_0 \) del polinomio ajustado.

---

## 3. Relación con un filtro FIR

Aunque conceptualmente es un ajuste polinomial, cada ventana de Savitzky–Golay se puede expresar como un conjunto fijo de **coeficientes FIR** \( h_k \):

$$
y(n) = \sum_{k=-m}^{m} h_k \, x(n+k)
$$

Por tanto, para un orden \( p \) y longitud \( L \) dados, el filtro es **lineal e invariante en el tiempo**, y su **función de transferencia** es:

$$
H(z) = \sum_{k=-m}^{m} h_k \, z^{-k}
$$

---

## 4. Elección de parámetros

- **Orden del polinomio \( p \)**:
  - Bajo (p=2 o p=3) → mayor suavizado.
  - Alto (p≥4) → más preservación de detalles pero menos filtrado de ruido.

- **Tamaño de la ventana \( L \)**:
  - Pequeña → conserva transitorios rápidos, menos suavizado.
  - Grande → mayor suavizado, pero puede distorsionar eventos cortos.

**Regla práctica**: \( L > p \) y \( L \) debe ser impar.

---

## 5. Aplicaciones típicas

- **Procesamiento biomédico**:
  - ECG: Filtrado de ruido preservando complejos QRS.
  - EEG: Reducción de artefactos preservando ondas rápidas (beta, gamma).
  - HRV: Suavizado de series temporales antes de análisis espectral.
- **Espectroscopia**: Suavizado de espectros sin distorsionar picos de absorción.
- **Análisis de datos experimentales**: Filtrado en química, física e ingeniería.

---

## 6. Ventajas y limitaciones

**Ventajas**:
- Mantiene la morfología de las señales.
- Permite derivación numérica precisa.
- Bajo coste computacional para órdenes bajos.

**Limitaciones**:
- No es óptimo para señales con picos muy estrechos si la ventana es grande.
- Puede introducir oscilaciones si el orden del polinomio es muy alto.
- No es adaptativo, requiere parámetros fijos.

---

## 7. Uso en MATLAB

```matlab
% Señal de ejemplo (ECG con ruido)
load ecg_signal

% Filtrado con polinomio cúbico y ventana de 21 muestras
y = sgolayfilt(ecg_signal, 3, 21);

% Visualización
plot(ecg_signal); hold on;
plot(y, 'LineWidth', 2);
legend('ECG original', 'ECG filtrado');
