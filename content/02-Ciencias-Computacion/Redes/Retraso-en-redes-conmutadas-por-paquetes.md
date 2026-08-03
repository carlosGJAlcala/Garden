---
title: "Retraso En Redes Conmutadas Por Paquetes"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
### Retraso en redes conmutadas por paquetes (_Packet-switched networks_) – Nota expandida

En una red conmutada por paquetes, como Internet, **los datos se dividen en pequeños bloques llamados paquetes**, que viajan de forma independiente desde el origen hasta el destino. A lo largo del camino, cada paquete puede experimentar distintos **tipos de retrasos (delays)**. Estos retrasos **afectan la calidad de servicio (QoS)** y el rendimiento general de la red.

---

##  Tipos de retraso (según Kurose y Ross)

Hay **cuatro fuentes principales de retraso** que sufre un paquete al pasar por un nodo (por ejemplo, un router):

---

### 1.  **Retraso de procesamiento (nodal processing delay)**

- Tiempo que tarda el router en:
    
    - Revisar errores en la cabecera.
        
    - Determinar a qué interfaz de salida debe enviar el paquete.
        
- Suele ser muy pequeño: **<1 ms**, salvo que haya inspección profunda.
    

---

### 2. ️ **Retraso de cola (queueing delay)**

- Tiempo que el paquete pasa **esperando en una cola** hasta ser transmitido.
    
- Depende del **nivel de congestión**:
    
    - Si el tráfico es bajo → cola vacía → retraso casi nulo.
        
    - Si la red está saturada → la cola crece → **retraso alto o incluso pérdida**.
        
- Es el más **variable e impredecible**.
    

---

### 3.  **Retraso de transmisión (transmission delay)**

- Tiempo necesario para **empujar los bits del paquete** a través del enlace.
    

Fórmula:

Retraso de transmisioˊn=LR\text{Retraso de transmisión} = \frac{L}{R}

- **L**: longitud del paquete en bits (por ejemplo, 1.000 bits).
    
- **R**: ancho de banda del enlace en bits/seg (por ejemplo, 1 Mbps).
    

Ejemplo:  
Un paquete de 1.000 bits en un enlace de 1 Mbps:

1.0001.000.000=0.001 segundos=1ms\frac{1.000}{1.000.000} = 0.001 \text{ segundos} = 1 ms

---

### 4.  **Retraso de propagación (propagation delay)**

- Tiempo que tarda una señal física en **viajar desde un nodo al siguiente** a través del medio (cable, fibra, aire...).
    

Fórmula:

Retraso de propagacioˊn=ds\text{Retraso de propagación} = \frac{d}{s}

- **d**: distancia del enlace (en metros).
    
- **s**: velocidad de propagación (~2 × 10⁸ m/s en cobre o fibra óptica).
    

Ejemplo:  
Distancia de 2.000 km:

2.000.0002×108=0.01 segundos=10ms\frac{2.000.000}{2 \times 10^8} = 0.01 \text{ segundos} = 10 ms

---

##  Total delay por nodo (router)

Retraso total=procesamiento+cola+transmisioˊn+propagacioˊn\text{Retraso total} = \text{procesamiento} + \text{cola} + \text{transmisión} + \text{propagación}

Si el paquete atraviesa varios routers, se suman los retrasos de cada uno.

---

##  ¿Qué causa pérdida de paquetes?

- Cuando la **cola del router se llena** (por congestión), los nuevos paquetes que llegan **se descartan**.
    
- Esto provoca:
    
    - Retransmisiones si hay protocolo confiable (como TCP).
        
    - Pérdida directa si no (como UDP en streaming en vivo).
        

---

##  Tráfico y retraso: modelo de intensidad

Definimos:

- **L**: tamaño medio de paquete.
    
- **a**: tasa de llegada de paquetes.
    
- **R**: capacidad del enlace.
    

Entonces:

Intensidad de traˊfico=LaR\text{Intensidad de tráfico} = \frac{La}{R}

- Si **La/R ≈ 0** → retraso de cola casi nulo.
    
- Si **La/R → 1** → la cola crece mucho → retrasos largos.
    
- Si **La/R > 1** → la red **no puede manejar** el tráfico → **retraso infinito + pérdida**.
    

---

### Conclusión

En una red conmutada por paquetes, **el retraso total experimentado por un paquete** depende de factores físicos (distancia, velocidad del medio) y dinámicos (congestión de red). Comprender estos retrasos es esencial para:

- **Optimizar el rendimiento de aplicaciones en tiempo real** (voz, vídeo).
    
- **Diagnosticar cuellos de botella**.
    
- **Diseñar protocolos que adapten su comportamiento** al estado de la red (como TCP).
    

---