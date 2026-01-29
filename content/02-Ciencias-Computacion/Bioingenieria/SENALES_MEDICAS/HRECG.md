---
title: "HRECG (High Resolution Electrocardiography)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# HRECG (High Resolution Electrocardiography)


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

La **Electrocardiografía de Alta Resolución** (*High Resolution Electrocardiography*, HRECG) es una técnica avanzada que permite registrar la actividad eléctrica del corazón con una resolución temporal y de amplitud mucho mayor que la electrocardiografía convencional.  
Su objetivo principal es **detectar potenciales ventriculares tardíos** y otras señales de baja amplitud que no son visibles en un ECG estándar.

---

## 1. Principio de funcionamiento

En la HRECG:
1. Se emplea un sistema de adquisición de alta frecuencia de muestreo (500–1000 Hz o más).
2. Se utilizan amplificadores de muy bajo ruido y gran estabilidad.
3. Se aplican técnicas de **promediado de señales** para reducir el ruido de fondo y mejorar la relación señal/ruido (SNR).

El promediado permite aislar componentes repetitivos del ECG y eliminar variaciones aleatorias.

---

## 2. Procedimiento típico

1. **Colocación de electrodos**: Se siguen derivaciones ortogonales especiales (X, Y, Z) o derivaciones estándar amplificadas.
2. **Adquisición prolongada**: Registro de varios cientos de latidos.
3. **Alineación de complejos QRS**: Sincronización precisa de cada complejo.
4. **Promediado vectorial**: Reducción del ruido para resaltar señales de baja amplitud.
5. **Análisis en dominio temporal y frecuencial**.

---

## 3. Parámetros de interés

En el análisis temporal se suelen extraer:

- **Duración del QRS filtrado**: \( QRS_f \) → duración total del complejo QRS tras filtrado de alta resolución.
- **RMS40**: Valor cuadrático medio de los últimos 40 ms del QRS.
  
$$
RMS40 = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i)^2}
$$

- **LAS40** (*Low Amplitude Signal 40 ms*): Duración de la señal con amplitud < 40 μV al final del QRS.

---

## 4. Análisis frecuencial

Además del dominio temporal, se puede aplicar la **Transformada de Fourier (FFT)** o la **Transformada Wavelet** para detectar componentes de alta frecuencia (> 40 Hz) al final del QRS, indicativas de inestabilidad eléctrica.

---

## 5. Aplicaciones clínicas

- **Estratificación de riesgo post-infarto**: Detección de pacientes con mayor riesgo de arritmias ventriculares malignas.
- **Diagnóstico de miocardiopatías**.
- **Evaluación de arritmias ventriculares**.
- Monitorización en deportistas con riesgo cardiovascular.

---

## 6. Ventajas y limitaciones

**Ventajas**:
- Mayor sensibilidad para detectar alteraciones eléctricas sutiles.
- Complementa al ECG convencional.

**Limitaciones**:
- Requiere equipamiento especializado.
- Mayor tiempo de adquisición y análisis.
- Puede verse afectado por ruido electromiográfico si no se filtra adecuadamente.
