---
title: "Mapa De Entorno"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
Un **mapa de entorno** en robótica representa la **estructura espacial del espacio que rodea al robot**, y es esencial para que pueda **navegar**, **localizarse** y **tomar decisiones autónomas**. Dependiendo del tipo de robot y su aplicación, este mapa puede ser **estático** (cuando el entorno no cambia) o **dinámico** (cuando hay personas, objetos móviles, etc.).

---

###  ¿Para qué sirve un mapa de entorno?


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

- **Localización**: el robot sabe dónde está dentro del entorno.
    
- **Planificación de trayectorias**: calcula cómo ir de un punto A a un punto B evitando obstáculos.
    
- **Detección de obstáculos**: distingue qué zonas son transitables y cuáles no.
    
- **Exploración**: si el entorno es desconocido, puede ir construyendo el mapa mientras se mueve (**SLAM**).
    

---

### ️ Tipos de mapas de entorno

#### 1. **Mapas de ocupación (Occupancy Grid)**

- Dividen el entorno en una **malla (grid)** donde cada celda representa una zona.
    
- Cada celda puede estar:
    
    - **Ocupada** (valor 1),
        
    - **Libre** (valor 0),
        
    - **Desconocida** (valor intermedio o -1).
        
- Son muy usados en navegación 2D (robots móviles, aspiradoras, etc.).
    

#### 2. **Mapas métricos (continuos)**

- Representan el entorno con medidas reales: distancias, posiciones exactas (x, y, z).
    
- Se pueden usar para generar mapas 3D (LIDAR, RGB-D).
    
- Muy usados en drones, vehículos autónomos y robots industriales.
    

#### 3. **Mapas topológicos**

- No representan la forma exacta del entorno, sino los **lugares clave y sus conexiones**.
    
- Por ejemplo: “cocina conectada con pasillo, pasillo conectado con salón”.
    
- Más ligeros en memoria y útiles en navegación de interiores.
    

#### 4. **Mapas semánticos**

- Añaden **información contextual**: identifican objetos y zonas con significado (una puerta, una mesa, una zona peligrosa).
    
- Usados en aplicaciones donde el robot debe interactuar con el entorno (robots de servicio, asistenciales, etc.).
    

---

###  ¿Cómo se construye un mapa?

1. **Sensores**:
    
    - LIDAR, sonar, infrarrojos, cámaras estéreo, sensores de profundidad (Kinect, RealSense).
        
    - Proporcionan datos sobre obstáculos y distancias.
        
2. **Procesamiento con SLAM**:
    
    - **SLAM** (Simultaneous Localization and Mapping) permite que el robot **construya un mapa mientras se localiza en él**.
        
    - Hay SLAM 2D (cartografía plana) y SLAM 3D (con altura).
        
    - Ejemplo de algoritmos: GMapping, Hector SLAM, Cartographer.
        
3. **Visualización en ROS**:
    
    - Se usan herramientas como **`rviz`** para ver el mapa en tiempo real.
        
    - También se pueden grabar con `rosbag` o guardar como archivo `.pgm` + `.yaml`.
        

---

###  Ejemplo en ROS

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch
```

- Este comando lanza un nodo SLAM con LIDAR.
    
- El robot explora y va generando un **mapa de ocupación**.
    

El archivo generado puede ser:

- `map.pgm`: imagen del mapa.
    
- `map.yaml`: indica resolución, origen y dimensiones.
    

---

### ️ Riesgos de ciberseguridad

- Si un atacante **altera el mapa**, el robot puede:
    
    - Chocar con obstáculos.
        
    - No encontrar rutas válidas.
        
    - Perderse o comportarse de forma errática.
        
- Si el robot **depende de mapas externos (cloud)**, debe usarse cifrado y autenticación.
    
- También es posible atacar los **sensores** para falsear datos y alterar el mapa generado.
    

---

###  Conclusión

El **mapa de entorno** es una representación clave para que un robot pueda actuar inteligentemente en su espacio. Dependiendo de la aplicación, puede ser un mapa de ocupación 2D, un modelo 3D o una red topológica/semántica. En sistemas como ROS, se construyen en tiempo real usando sensores y algoritmos SLAM, y son esenciales para la localización, navegación y planificación del movimiento.