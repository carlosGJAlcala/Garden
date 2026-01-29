---
title: "Ondas EEG (Electroencefalografía)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# Ondas EEG (Electroencefalografía)


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

La **Electroencefalografía** (EEG) es una técnica no invasiva que registra la actividad eléctrica del cerebro mediante electrodos colocados sobre el cuero cabelludo.  
El EEG refleja la **suma de los potenciales postsinápticos** de millones de neuronas corticales, especialmente de las células piramidales.  
La señal EEG se caracteriza por la presencia de diferentes **ondas** que varían en frecuencia y amplitud, y que se asocian con distintos estados cerebrales.

---

## 1. Clasificación de ondas EEG

Las ondas EEG se clasifican según su **frecuencia** y **estado funcional asociado**:

| Tipo de onda | Frecuencia (Hz) | Amplitud típica (µV) | Estado asociado |
|--------------|----------------|---------------------|-----------------|
| Delta (δ)    | 0.5 – 4        | 20 – 200            | Sueño profundo, procesos de reparación |
| Theta (θ)    | 4 – 8          | 20 – 100            | Somnolencia, meditación, creatividad |
| Alpha (α)    | 8 – 13         | 20 – 60             | Relajación, vigilia tranquila, ojos cerrados |
| Beta (β)     | 13 – 30        | 5 – 20              | Actividad mental, concentración, alerta |
| Gamma (γ)    | 30 – 100+      | 1 – 10              | Procesamiento cognitivo, integración sensorial |

---

## 2. Representación matemática de la señal EEG

Una señal EEG puede representarse como la suma de componentes oscilatorios de diferentes frecuencias:

$$
EEG(t) = \sum_{k=1}^{N} A_k \cdot \sin(2 \pi f_k t + \phi_k)
$$

Donde:  
- \( A_k \): amplitud de la componente \( k \).  
- \( f_k \): frecuencia de la componente \( k \).  
- \( \phi_k \): fase de la componente \( k \).  
- \( N \): número de componentes significativas.

---

## 3. Métodos de análisis

Para estudiar las ondas EEG se utilizan técnicas como:
- **Análisis en dominio temporal**: inspección visual de la morfología de la onda.
- **Análisis espectral (FFT)**: cálculo de la densidad espectral de potencia para cada banda.
- **Transformadas Wavelet (CWT/DWT)**: estudio tiempo-frecuencia para detectar cambios transitorios.
- **Filtros paso banda**: aislamiento de bandas específicas.

---

## 4. Aplicaciones clínicas

- **Epilepsia**: detección de descargas paroxísticas.
- **Trastornos del sueño**: estudio de fases y arquitectura del sueño.
- **Coma y muerte encefálica**: evaluación de actividad residual.
- **Neurofeedback**: entrenamiento para modular ondas cerebrales.
- **Investigación cognitiva**: correlación entre ondas EEG y funciones mentales.

---

## 5. Factores que afectan la señal

- Impedancia de electrodos y calidad del contacto.
- Artefactos musculares y oculares.
- Interferencias eléctricas (50/60 Hz).
- Estado fisiológico del sujeto (cansancio, fármacos, estrés).

