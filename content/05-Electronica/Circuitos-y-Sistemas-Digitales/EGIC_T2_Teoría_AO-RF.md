---
title: "EGIC_T2_Teoría_AO-RF"
tags: [universidad, 1cuatri, electronica]
date: 2026-08-14
lang: es
---
# Amplificadores Operacionales - Respuesta en Frecuencia
Electrónica
## Índice
**1. Introducción**
- Objetivos y herramientas
- Modelado de señales
- Caracterización de amplificadores en el dominio de la frecuencia
- Bandas de frecuencia del amplificador
- Frecuencia de corte. Ancho de banda ( BW)
- Efecto de las limitaciones de alta y baja frecuencia
**2. Función de transferencia**
- Laplace, Fourier, polos y ceros
- Representación gráfica: diagrama de Bode
- Diagrama de Bode de módulo
**3. Diagrama de Bode**
- Términos básicos
- Módulo y fase
- Ejemplos
**4. Análisis por bandas de frecuencia**
- Función de transferencia en función de la ganancia en frecuencias medias
- Simplificación de la F.T. a frecuencias medias, bajas y altas
- Frecuencias de corte
- Polo dominante
- Sin polo
**5. Aplicaciones básicas: Filtros con AO ideal**
- Filtro paso bajo con polo
- Filtro paso alto polo-cero
- Otros filtros
- Otras configuraciones básicas
## Referencias
Material de estudio recomendado:
**Malik:**
- Capítulo 2, secciones 2.2 a 2.3.4; 2.5.1 a 2.5.10; y 2.6
**Sedra-Smith:**
- Capítulo 2, secciones 2.1 a 2.6; y 2.9
**Hambley:**
- Capítulo 2
Nota: En todos los casos se excluyen las dependencias internas con la frecuencia y el trabajo en "gran señal".
## Introducción
### Motivación
Señales y amplificadores:
- Los amplificadores han de procesar señales de muy diversa naturaleza
### Objetivos básicos
- Adaptar niveles de la señal ( tensión, corriente, potencia)
- Optimizar la interconexión a generadores y cargas
- Ajustar las características en frecuencia de la información de entrada
 - Por ejemplo: modificar o seleccionar las componentes de la señal
## Objetivos y herramientas
### Necesidades desde el punto de vista de la Ingeniería
- Poder analizar el comportamiento de los circuitos en el dominio de la frecuencia
- En función de tal análisis, conocer las dependencias y relaciones entre dispositivos, circuitos y sus prestaciones ( ganancias, etc.)
- Tener capacidad para ajustar y adaptar las características del amplificador a la aplicación deseada
### Herramientas necesarias
- *Conocimiento de las características de los dispositivos** en función de la frecuencia (ω)
- *Conocimiento de técnicas de análisis específicas:** por ejemplo, Bode, para identificar las dependencias importantes
- *Conocimiento de configuraciones típicas:** por ejemplo, filtros de señal
## Modelado de señales
Las señales reales son muy complejas de modelar:
- Fenómenos electromagnéticos ( ecuaciones de Maxwell)
- Ecuaciones diferenciales complejas de variables complejas
- El problema general se simplifica según el caso
### Ejemplo: El condensador
**Fundamento físico ( dominio del tiempo):**
i_C ( t) = C · dv_C ( t)/dt
Exacto pero difícil de analizar.
**Simplificación ( dominio de la frecuencia):**
- Solo válido para Régimen Permanente Senoidal ( R.P.S.)
- Limitado, pero fácil de analizar
- Concepto de impedancia: Z_C = 1/( jωC)
## Caracterización de amplificadores
La respuesta en frecuencia describe cómo varía la ganancia ( amplitud y fase) en función de la frecuencia de la señal de entrada.
### Bandas de frecuencia
- *Baja frecuencia:** Donde domina el efecto de condensadores de acoplamiento
- *Frecuencias medias:** Zona plana donde la ganancia es constante
- *Alta frecuencia:** Donde domina el efecto de capacidades parásitas
### Frecuencia de corte ( f_c)
Frecuencia donde la ganancia cae 3 dB respecto al valor en frecuencias medias:
|A (ω_c)| = |A_m| / √2
### Ancho de banda ( BW)
BW = f_cH - f_cL
Donde:
- f_cH: frecuencia de corte superior
- f_cL: frecuencia de corte inferior
## Efecto de las limitaciones de frecuencia
Las limitaciones tanto en baja como en alta frecuencia afectan:
- Al ancho de banda útil del amplificador
- A la forma de la respuesta en frecuencia
- A la estabilidad del sistema en retroalimentación
