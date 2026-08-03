---
title: "Algoritmos no supervisados"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---

# Algoritmos no supervisados


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Los modelos como ChatGPT utilizan la distancia coseno para evaluar la similitud entre una consulta y un conjunto de documentos. En este enfoque, la consulta se representa como un vector y se compara con los vectores embebidos de los documentos mediante el coseno del ángulo entre ellos. Cuanto más cercano sea este valor a 1, mayor será la similitud entre la consulta y el documento.

En el ámbito de los sistemas de recomendación de productos, se utilizan reglas de asociación para identificar patrones en los datos de compra de los usuarios. Estas reglas permiten descubrir relaciones entre diferentes productos con el fin de sugerir aquellos que tienen una alta probabilidad de ser adquiridos en conjunto.

Para optimizar el procesamiento de datos en dispositivos con recursos limitados, como una Raspberry Pi, se aplican técnicas de reducción de dimensionalidad. Estas técnicas permiten disminuir la cantidad de variables en un conjunto de datos sin perder información significativa, lo que facilita la ejecución de modelos con menor costo computacional.

## Algoritmo k-means

El algoritmo k-means es un método de agrupamiento en el que la "k" representa el número de clústeres deseados. Su funcionamiento es el siguiente:

1. Se seleccionan k centroides iniciales de manera aleatoria dentro del conjunto de datos.
2. Cada punto de datos se asigna al clúster cuyo centroide esté más cercano, según una medida de distancia, generalmente la euclidiana.
3. Se recalculan los centroides como el promedio de los puntos asignados a cada clúster.
4. El proceso se repite hasta que los centroides dejan de cambiar significativamente o se alcanza un criterio de parada.

El resultado de este procedimiento puede visualizarse mediante un diagrama de Voronoi, que ilustra cómo se distribuyen los puntos alrededor de sus respectivos centroides.

Para evaluar la calidad de los clústeres obtenidos, se utilizan métricas como el índice de Dunn, que mide la separación entre los grupos y la compactación de los puntos dentro de cada clúster. Un buen agrupamiento se caracteriza por presentar puntos cercanos a su centroide y alejados de los otros clústeres.

El algoritmo k-means tiene un costo computacional significativo, ya que requiere múltiples cálculos de distancia y actualización de centroides. Además, puede verse afectado por el problema de la alta dimensionalidad, donde la efectividad de las medidas de distancia se reduce debido a la dispersión de los datos.

Otra métrica utilizada para evaluar el rendimiento del clustering es el coeficiente de silueta, que indica qué tan bien definido está un clúster. Su valor oscila entre -1 y 1, donde valores cercanos a 1 indican una buena asignación, valores cercanos a 0 sugieren solapamiento entre clústeres y valores negativos indican que los puntos están mal agrupados. Si el coeficiente de silueta es bajo, puede ser recomendable aumentar el número de clústeres para mejorar la segmentación de los datos.

Una mejora el KMeans ++ tiene una inicialización inteligente de los centroides.

