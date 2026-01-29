---
title: "Análisis mediante WPT (Wavelet Packet Transform)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - bioingenieria
  - senales_medicas
---
# Análisis mediante WPT (Wavelet Packet Transform)


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

La **Transformada de Paquetes Wavelet** (WPT, *Wavelet Packet Transform*) es una extensión de la **Transformada Wavelet Discreta (DWT)** que ofrece una **descomposición más completa** de la señal.  
Mientras que en la DWT solo se descompone la parte de baja frecuencia (aproximaciones) en cada nivel, la WPT descompone **tanto las aproximaciones como los detalles**, lo que proporciona una **mayor resolución en el dominio tiempo-frecuencia**.

Esto la convierte en una herramienta muy potente para el análisis de **señales biomédicas**, especialmente cuando se requiere un estudio detallado de todas las bandas de frecuencia.

---

## 1. Fundamento teórico

En la WPT, una señal \( x(t) \) se representa como la suma de **funciones wavelet** y **funciones de escalamiento** en todos los nodos de un árbol de descomposición completo:

$$
x(t) = \sum_{n} c_{n} \, \psi_{n}(t)
$$

Donde:  
- \( \psi_{n}(t) \): funciones base obtenidas por traslación, escalamiento y filtrado.  
- \( c_{n} \): coeficientes asociados a cada nodo del árbol de descomposición.  

A diferencia de la DWT, el número de subbandas crece exponencialmente con el nivel de descomposición, lo que permite un análisis fino de frecuencias intermedias.

---

## 2. Proceso de análisis

1. **Nivel inicial**: la señal pasa por un filtro paso bajo (LPF) y un filtro paso alto (HPF), generando la aproximación \( A_1 \) y el detalle \( D_1 \).  
2. **Descomposición completa**: en la WPT, tanto \( A_1 \) como \( D_1 \) se vuelven a descomponer en nuevas subbandas \( A_{2,0} \), \( D_{2,0} \), \( A_{2,1} \), \( D_{2,1} \).  
3. **Repetición por niveles**: el proceso se repite hasta alcanzar el nivel deseado, obteniendo un **árbol binario completo** de subbandas.  
4. **Selección de nodos**: dependiendo de la aplicación, se pueden usar todas las subbandas o solo aquellas que contengan información relevante.

---

## 3. Ventajas frente a DWT

- **Mayor resolución frecuencial**: todas las bandas de frecuencia son analizadas en cada nivel.  
- **Flexibilidad**: permite seleccionar nodos específicos para centrarse en ciertas frecuencias.  
- **Adecuada para señales complejas**: ideal para señales con contenido relevante tanto en baja como en alta frecuencia.  
- **Base para análisis espectral adaptativo**: utilizada en clasificación de patrones y extracción de características.

---

## 4. Aplicaciones en señales médicas

- **ECG**: identificación precisa de complejos QRS, ondas P y T en entornos con mucho ruido.  
- **EEG**: detección de patrones epilépticos y análisis de bandas cerebrales (\( \delta, \theta, \alpha, \beta, \gamma \)).  
- **EMG**: estudio detallado de la actividad muscular en diferentes rangos de frecuencia.  
- **Análisis de variabilidad cardíaca (HRV)**: separación precisa de componentes de baja y alta frecuencia para evaluar el sistema nervioso autónomo.

---

## 5. Ejemplo práctico

En un análisis de ECG:  
- **Nivel 1**: separación en bajas y altas frecuencias.  
- **Nivel 2 y 3**: descomposición de cada banda para aislar frecuencias asociadas a eventos cardíacos.  
- **Selección de nodos**: uso de nodos específicos que contienen la mayor energía del complejo QRS.  
- **Reconstrucción**: aplicación de la **Transformada Inversa WPT (IWPT)** para obtener la señal filtrada o segmentada.

---
