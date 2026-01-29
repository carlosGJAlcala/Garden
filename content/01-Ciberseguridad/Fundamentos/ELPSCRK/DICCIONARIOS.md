---
title: "Práctica 6: Auditoría de Redes Inalámbricas"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - elpscrk
---
# **Práctica 6: Auditoría de Redes Inalámbricas**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/Pyrit|Pyrit]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**Estudiantes:**

- **Jonnathan Sebastián Avendaño Castillo**
- **Carlos Garrido Junco**

**Asignatura:** Auditoría de Redes Inalámbricas  
**Universidad:** Universidad Autónoma de Hidalgo (UAH)  
**Curso:** P

---

## **Índice**

1. Tamaño Teórico del Diccionario
2. Generación del Diccionario con Crunch
3. Estimación del Tiempo de Verificación
4. Generación de Diccionario con un Patrón Específico
5. Realización del Ataque para Obtener la Clave
6. Tiempo de Obtención de la Clave
7. Generación de Diccionarios Específicos con Crunch
8. Influencia de CCMP y TKIP en la Resistencia de la Red
9. Generación de Diccionario Usando Crunch con Información Adicional
10. Estimación del Tiempo Medio para Obtener la Clave
11. Órdenes Necesarias para Realizar el Ataque

---



## **1. Tamaño Teórico del Diccionario**

En esta sección se calcula el tamaño teórico del diccionario compuesto por todas las posibles claves de hasta **9 caracteres**, considerando que el tamaño mínimo de la clave en PSK es de **8 caracteres**.

### **Cálculo del Tamaño**

- Usando un alfabeto de **62 caracteres** (26 letras mayúsculas + 26 letras minúsculas + 10 números), las posibles combinaciones para las claves de **8** y **9 caracteres** son:

    - **Combinaciones para 9 caracteres**:  
      \[
      62^9 \approx 1.375543 \times 10^{16} \quad \text{combinaciones}
      \]

    - **Combinaciones para 8 caracteres**:  
      \[
      62^8 \approx 2.540 \times 10^{14} \quad \text{combinaciones}
      \]

### **Total de combinaciones posibles**

Sumando las combinaciones para 8 y 9 caracteres:

\[
62^9 + 62^8 \approx 1.829587 \times 10^{16} \quad \text{combinaciones}
\]



Este formato es más limpio y fácil de leer, con las ecuaciones bien presentadas. ¡Avísame si necesitas más ajustes o ayuda con otros apartados!
## **2. Generación del Diccionario con Crunch**

Para la generación del diccionario utilizamos la herramienta **Crunch**, que permite crear diccionarios personalizados. El siguiente comando genera un diccionario con combinaciones de entre **8** y **9 caracteres** alfanuméricos:

bash

Copiar código

`crunch 8 9 -f /usr/share/crunch/charset.lst mixalpha-numeric`

### **Tamaño del Diccionario Generado**

- El diccionario generado tendrá aproximadamente **1.375543 x 10^16** combinaciones, lo cual ocuparía un espacio de aproximadamente **121 PB**.

---

## **3. Estimación del Tiempo de Verificación**

Para estimar el tiempo necesario para verificar todas las combinaciones del diccionario, utilizamos **Pyrit** y su comando `benchmark` para obtener la velocidad de verificación en PMKs/s.

### **Cálculo del Tiempo Medio**

Con una **velocidad de verificación de 7,180 PMKs/s** y un diccionario de **1.375543 x 10^16** combinaciones, el tiempo estimado de verificación es el siguiente:

Tiempo estimado=1.375543×10167180×2≈957,898,791,911 segundos\text{Tiempo estimado} = \frac{1.375543 \times 10^{16}}{7180 \times 2} \approx 957,898,791,911 \text{ segundos}Tiempo estimado=7180×21.375543×1016​≈957,898,791,911 segundos

Esto equivale a **1.1 millones de años**, por lo que resulta impracticable realizar un ataque de diccionario a este nivel.

---

## **4. Generación de Diccionario con un Patrón Específico**

Para generar un diccionario con un patrón específico (como números en una posición determinada), utilizamos el carácter `%` en **Crunch**.

### **Comando para Generar el Diccionario**

bash

Copiar código

`crunch 8 9 -t @@@@%%%%`

### **Tiempo Estimado para Generar el Diccionario**

Este diccionario específico se generaría en un tiempo aproximado de **1.09 minutos**.

---

## **5. Realización del Ataque para Obtener la Clave**

Una vez generado el diccionario, se procede a realizar el ataque de diccionario utilizando **Pyrit** para obtener la clave PSK de la red.

### **Comando para Realizar el Ataque**

bash

Copiar código

`pyrit -r archivo.cap -i diccionario.txt`

### **Clave Obtenida**

La clave PSK obtenida fue **918856501**.

### **Tiempo de Obtención de la Clave**

El tiempo aproximado de obtención de la clave fue **111.99 segundos**, lo que corresponde a aproximadamente **2 minutos**. La clave fue obtenida en el intento **880,044 PMKs** a una velocidad de **7,858 PMKs/s**.

---

## **6. Tiempo de Obtención de la Clave**

**Estimación del Tiempo:**

La estimación fue de **1.87 minutos**, y el tiempo real fue de **1.86 minutos**, lo que confirma la precisión de nuestra estimación.

---

## **7. Generación de Diccionarios Específicos con Crunch**

A continuación, se presentan los comandos para generar diccionarios con patrones específicos:

### **I. Diccionario de Palabras de 9 Caracteres con la Primera Letra en Mayúsculas y el 9º Carácter como Símbolo**

bash

Copiar código

`crunch 9 9 -t @@@@@@@@^`

### **II. Diccionario de Teléfonos Móviles (9 Números) que Empiecen por 60912**

bash

Copiar código

`crunch 9 9 -t 60912%%%%`

### **III. Diccionario de Palabras de 8 Caracteres con "admin" en el Medio**

bash

Copiar código

`crunch 8 8 -t XXadminX`

---

## **8. Influencia de CCMP y TKIP en la Resistencia de la Red**

**Análisis de los Protocolos de Seguridad**:

- **CCMP (WPA2)** es un protocolo de cifrado más seguro que **TKIP (WPA)**, ya que fue diseñado para solucionar las vulnerabilidades de TKIP.
    
- **Impacto en el Ataque de Diccionario**:  
    El uso de CCMP o TKIP no afecta directamente la resistencia de la red ante un ataque de diccionario, ya que este ataque está centrado en la clave PSK, no en el algoritmo de cifrado. Sin embargo, CCMP proporciona una mayor protección ante otros tipos de ataques.
    

---

## **9. Generación de Diccionario Usando Crunch con Información Adicional**

Para generar un diccionario con un formato específico, utilizamos el siguiente comando:

bash

Copiar código

`crunch 8 8 -t AUTO12@@@@`

### **Tamaño del Diccionario**

- **Número de palabras**: **456,976**
- **Tamaño en bytes**: **4,569,760 bytes**

---

## **10. Estimación del Tiempo Medio para Obtener la Clave**

Para estimar el tiempo medio para obtener la clave de la red, utilizamos la siguiente fórmula:

Tiempo estimado=456,9767,180≈636 segundos≈10.6 minutos\text{Tiempo estimado} = \frac{456,976}{7,180} \approx 636 \text{ segundos} \approx 10.6 \text{ minutos}Tiempo estimado=7,180456,976​≈636 segundos≈10.6 minutos

---

## **11. Órdenes Necesarias para Realizar el Ataque**

Las órdenes para realizar el ataque con **Pyrit** son las siguientes:

bash

Copiar código

`pyrit -r archivo.cap -i diccionario.txt`

Estas órdenes se ejecutan para los archivos de captura de tráfico de red (por ejemplo, **AUT01.cap** y **AUT02.cap**).
