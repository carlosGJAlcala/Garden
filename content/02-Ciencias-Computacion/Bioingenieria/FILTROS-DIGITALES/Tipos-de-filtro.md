---
title: "Tipos De Filtro"
date: 2025-01-01
tags:
  - ciencias-computacion
---

### **1. Según su respuesta en frecuencia**


> **Relacionado**: [[02-Ciencias-Computacion/Bioingenieria/FILTROS-DIGITALES/FILTFILT|FILTFILT]]. [[02-Ciencias-Computacion/Bioingenieria/FILTROS-DIGITALES/Filtro-LMS|Filtro LMS]]. [[02-Ciencias-Computacion/Bioingenieria/FILTROS-DIGITALES/Filtro-Notch|Filtro Notch]]. [[02-Ciencias-Computacion/Bioingenieria/FILTROS-DIGITALES/Filtro-de-Kalman|Filtro de Kalman]].

- **Pasa-bajo (Low Pass Filter – LPF)**  
    Deja pasar frecuencias por debajo de un corte fcf_c y atenúa las superiores.  
    Ejemplo: eliminar ruido de alta frecuencia en ECG.
    
- **Pasa-alto (High Pass Filter – HPF)**  
    Deja pasar frecuencias superiores a fcf_c y atenúa las bajas.  
    Ejemplo: eliminar deriva de línea base en ECG.
    
- **Pasa-banda (Band Pass Filter – BPF)**  
    Deja pasar un rango específico de frecuencias.  
    Ejemplo: aislar componentes de 0.5–40 Hz en EEG.
    
- **Rechaza-banda (Band Stop Filter)**  
    Atenúa un rango específico de frecuencias.  
    Ejemplo: filtro notch para 50/60 Hz.
    

---

### **2. Según su estructura**

- **FIR (Finite Impulse Response)**  
    Respuesta finita al impulso, fase lineal posible, siempre estables.  
    Ejemplo: filtros de ventana (Hamming, Blackman).
    
- **IIR (Infinite Impulse Response)**  
    Respuesta infinita, más eficientes pero pueden tener fase no lineal.  
    Ejemplo: Butterworth, Chebyshev, Elíptico.
    

---

### **3. Según el método de diseño**

- **Butterworth** – Respuesta suave, sin ondulaciones en banda pasante/atenuada.
    
- **Chebyshev I** – Ondulación en banda pasante, transición más rápida que Butterworth.
    
- **Chebyshev II** – Ondulación en banda atenuada.
    
- **Elíptico (Cauer)** – Ondulación en ambas bandas, transición muy rápida.
    
- **Bessel** – Máxima linealidad de fase, útil para preservar forma de onda.
    

---

### **4. Según su función especial**

- **Filtro adaptativo** – Cambia sus coeficientes según la señal (LMS, RLS, NLMS).
    
- **Filtro de mediana** – No lineal, útil para eliminar picos impulsivos.
    
- **Filtro de Kalman** – Óptimo para estimar señales en presencia de ruido gaussiano.
    
- **Savitzky–Golay** – Suavizado polinomial manteniendo picos.
    
- **Filtros Wavelet** – Procesan la señal en dominio tiempo-frecuencia.
    
- **Filtros comb** – Eliminan o realzan frecuencias periódicas.
    

---

### **5. Según el dominio de trabajo**

- **Tiempo discreto** – Trabajan sobre secuencias en el dominio nn.
    
- **Frecuencia** – Diseñados y aplicados en el dominio de Fourier.
    
- **Tiempo-frecuencia** – Basados en wavelets o STFT.
    
# Comparativa de filtros digitales

| Filtro | Tipo | Cuándo usarlo | Ventajas | Limitaciones |
|--------|------|--------------|----------|--------------|
| **FILTFILT** | Lineal (FIR/IIR aplicado doble) | Cuando se necesita eliminar desfase de fase en señales offline. Ej: ECG, EEG, audio. | Fase cero, preserva forma de onda. | No causal, no apto para tiempo real. |
| **Filtro de Kalman** | Adaptativo / Estimador | Seguimiento y filtrado de señales con ruido gaussiano. Ej: HRV, sensores. | Óptimo en sistemas lineales, predice y filtra. | Requiere conocer modelo y ruido. |
| **Filtro LMS** | Adaptativo | Cancelar ruido no estacionario usando referencia. Ej: eliminar 50 Hz en ECG con referencia sinusoidal. | Simple, bajo coste computacional. | Convergencia lenta, sensible a µ. |
| **Filtro Notch** | IIR/FIR | Eliminar una frecuencia fija (50/60 Hz). Ej: ruido de red en biomédica. | Alta atenuación en frecuencia objetivo. | Puede afectar frecuencias cercanas. |
| **Filtro Savitzky–Golay** | FIR polinomial | Suavizar sin distorsionar picos. Ej: ECG, HRV, espectros. | Preserva amplitud y morfología. | No apto para ruido impulsivo fuerte. |
| **Filtro FIR Pasa-bajo** | FIR | Eliminar altas frecuencias. Ej: suavizado de señal. | Fase lineal, estable. | Orden alto para transición abrupta. |
| **Filtro FIR Pasa-alto** | FIR | Quitar deriva o variaciones lentas. Ej: eliminar línea base en ECG. | Preserva altas frecuencias. | Puede amplificar ruido de alta frecuencia. |
| **Filtro Pasa-banda** | FIR/IIR | Mantener un rango específico de frecuencias. Ej: 0.5–40 Hz en ECG. | Aísla banda de interés. | Atenúa fuera de la banda deseada. |
| **Butterworth** | IIR | Filtrado suave sin ondulación. | Transición gradual, diseño simple. | Menos selectivo que Chebyshev/Elíptico. |
| **Chebyshev I** | IIR | Transición rápida tolerando ondulación en banda pasante. | Más selectivo que Butterworth. | Ondulación en la banda útil. |
| **Chebyshev II** | IIR | Banda pasante plana, ondulación en banda de rechazo. | Mejor en pasante que Chebyshev I. | Ondulación en rechazo. |
| **Elíptico (Cauer)** | IIR | Máxima selectividad con ondulación en ambas bandas. | Muy eficiente. | Distorsión de amplitud en ambas bandas. |
| **Bessel** | IIR | Preservar la forma de onda (fase lineal). Ej: ECG. | Mínima distorsión temporal. | Menor atenuación fuera de banda. |
| **Filtro de mediana** | No lineal | Eliminar ruido impulsivo preservando bordes. Ej: imágenes, EEG con artefactos. | Muy bueno contra picos. | No apto para ruido gaussiano puro. |
| **Wavelet** | Tiempo-frecuencia | Analizar señales no estacionarias y filtrar por escalas. Ej: EEG, compresión. | Alta resolución tiempo-frecuencia. | Mayor complejidad. |
