---
title: "Algoritmo De Retroproyeccion"
date: 2025-01-01
tags:
  - ciencias-computacion
---

## **Algoritmo de Retroproyección**


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

El **algoritmo de retroproyección** (backprojection algorithm) es un procedimiento matemático utilizado para reconstruir una imagen bidimensional o tridimensional a partir de un conjunto de proyecciones adquiridas desde diferentes ángulos. Es un pilar en técnicas de **imagen médica** como la **tomografía computarizada (CT)**, la **tomografía por emisión de positrones (PET)** o la **tomografía computarizada por emisión de fotón único (SPECT)**.

Su objetivo es **convertir la información angular obtenida por un detector en una representación espacial coherente del objeto** que está siendo estudiado.

---

### 1. Principio de Funcionamiento

En un sistema de tomografía, el objeto es irradiado (rayos X, rayos gamma, ultrasonido, etc.) desde múltiples direcciones. Cada detector registra la **atenuación** o respuesta del haz al atravesar el objeto, produciendo un **perfil de proyección**.

El algoritmo de retroproyección consiste en **reproyectar** cada perfil de proyección de vuelta al espacio de la imagen, siguiendo la geometría de adquisición, y sumarlos todos para estimar la distribución interna de la variable medida (densidad, actividad radiactiva, etc.).

En términos sencillos:

1. Se adquieren proyecciones desde distintos ángulos.
    
2. Cada proyección se “extiende” o “difunde” a lo largo del ángulo correspondiente.
    
3. Se suman todas las retroproyecciones para formar una imagen aproximada del objeto.
    

---

### 2. Formulación Matemática

Si definimos:

$$ pθ(t)p_{\theta}(t) =$$ proyección medida en un ángulo θ\theta y desplazamiento tt.
    
$$ f(x,y)f(x, y) = $$distribución espacial de la variable física que queremos reconstruir.
    

La retroproyección básica puede expresarse como:

$$fRB(x,y)=∫0πpθ(xcos⁡θ+ysin⁡θ) dθf_{RB}(x, y) = \int_{0}^{\pi} p_{\theta}(x \cos \theta + y \sin \theta) \, d\theta$$

Donde fRB(x,y)f_{RB}(x, y) es la imagen obtenida por retroproyección directa (sin filtrado).  
Este método genera una imagen borrosa debido a la superposición de proyecciones, por lo que normalmente se emplea la **retroproyección filtrada (Filtered Backprojection - FBP)**.

---

### 3. Retroproyección Filtrada (FBP)

Para mejorar la nitidez, antes de retroproyectar se **filtran** las proyecciones en el dominio de la frecuencia mediante un **filtro de rampa** u otros filtros modificados (Shepp-Logan, Hamming, Hann). Esto compensa la pérdida de información de altas frecuencias durante la adquisición.

Pasos:

1. Aplicar la **Transformada de Fourier** a cada proyección.
    
2. Multiplicar el espectro por un filtro adecuado.
    
3. Realizar la transformada inversa para obtener la proyección filtrada.
    
4. Retroproyectar las proyecciones filtradas.
    

---

### 4. Aplicaciones Clínicas

- **Tomografía Computarizada (CT)**: Reconstrucción de cortes axiales de tejidos blandos, huesos y órganos.
    
- **PET/SPECT**: Distribución de radiotrazadores en el cuerpo para estudios metabólicos y funcionales.
    
- **Microscopía de rayos X y tomografía industrial**: Análisis no destructivo de materiales.
    

---

### 5. Ventajas y Limitaciones

**Ventajas:**

- Rápido y computacionalmente eficiente.
    
- Fácil de implementar.
    
- Base de muchos sistemas comerciales de imagen médica.
    

**Limitaciones:**

- La retroproyección simple produce imágenes difusas.
    
- Requiere filtrado para obtener imágenes de calidad.
    
- Sensible al ruido y a artefactos por datos incompletos o mal calibrados.
    

---