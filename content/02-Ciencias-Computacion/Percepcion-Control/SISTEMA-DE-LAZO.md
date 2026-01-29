---
title: "Sistema De Lazo"
date: 2025-01-01
tags:
  - ciencias-computacion
---

## ️ Sistemas de Lazo: Definición y Principios Fundamentales


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Los **sistemas de control en lazo** son configuraciones en las que una **señal de salida** es utilizada como **retroalimentación** para ajustar la **entrada** del sistema, con el objetivo de **mantener el comportamiento deseado** del sistema bajo control frente a perturbaciones internas o externas.

La clasificación más básica los divide en:

- **Sistemas de lazo abierto (open-loop)**
    
- **Sistemas de lazo cerrado (closed-loop o feedback systems)**
    

---

##  1. Sistema de Lazo Abierto

En un sistema de lazo abierto:

- La **entrada de control** genera una acción sobre el sistema sin considerar el resultado real de esa acción.
    
- No existe retroalimentación.
    
- Es adecuado cuando el modelo del sistema es muy preciso y no hay perturbaciones externas significativas.
    

### Ejemplo:

Control de una **lavadora automática**:

- El usuario selecciona el ciclo de lavado (entrada).
    
- El sistema ejecuta el ciclo sin medir si la ropa ya está limpia (no hay retroalimentación).
    

### Ventajas:

- Simplicidad de diseño.
    
- Bajo coste computacional.
    

### Inconvenientes:

- No corrige errores.
    
- Sensible a perturbaciones y variaciones en el sistema.
    

---

##  2. Sistema de Lazo Cerrado

En un sistema de lazo cerrado:

- Se mide la **salida real** del sistema y se compara con la **salida deseada**.
    
- La **diferencia (error)** entre ambas se utiliza para ajustar dinámicamente la entrada.
    
- Este tipo de sistema se adapta mejor a condiciones cambiantes o no modelables.
    

### Ejemplo:

Control de velocidad de un **motor DC**:

- Se desea mantener una velocidad constante de 3000 rpm.
    
- Un sensor mide la velocidad real y la compara con el valor deseado.
    
- El controlador ajusta el voltaje de entrada al motor para corregir el error.
    

### Estructura general del sistema:

```
Entrada deseada → [Controlador] → [Sistema/planta] → Salida real
                                     ↑               ↓
                                 Sensor ← Comparador (real - deseado)
```

---

##  Componentes de un sistema en lazo cerrado

1. **Referencia (r)**: valor deseado que se quiere alcanzar (setpoint).
    
2. **Sensor**: mide el estado actual del sistema (salida y).
    
3. **Comparador**: calcula el error `e(t) = r(t) - y(t)`.
    
4. **Controlador (C(s))**: transforma el error en una acción de control.
    
5. **Actuador**: aplica la señal de control a la planta.
    
6. **Planta (P(s))**: el sistema físico a controlar.
    
7. **Perturbaciones (d)**: entradas no deseadas que afectan el sistema.
    
8. **Retroalimentación**: puede ser unitaria o ponderada.
    

---

##  Representación Matemática

Usando funciones de transferencia en el dominio de Laplace:

- Si `R(s)` es la entrada, `Y(s)` la salida y `H(s)` la función de transferencia del sensor (retroalimentación), la salida del sistema cerrado es:
    

Y(s)=C(s)P(s)1+C(s)P(s)H(s)R(s)Y(s) = \frac{C(s) P(s)}{1 + C(s) P(s) H(s)} R(s)

Donde:

- `C(s)` es el controlador,
    
- `P(s)` es la planta,
    
- `H(s)` es la retroalimentación (a menudo = 1),
    
- El denominador 1+C(s)P(s)H(s)1 + C(s)P(s)H(s) es el **polinomio característico**, cuya estabilidad determina el comportamiento del sistema.
    

---

##  Objetivos del Control con Lazo Cerrado

1. **Estabilidad**:
    
    - El sistema no debe divergir ante pequeñas perturbaciones.
        
2. **Precisión**:
    
    - La salida debe coincidir con la referencia a lo largo del tiempo (mínimo error en régimen permanente).
        
3. **Rapidez**:
    
    - Capacidad de alcanzar el valor deseado en el menor tiempo posible.
        
4. **Robustez**:
    
    - Capacidad del sistema para seguir funcionando correctamente ante incertidumbre en el modelo o perturbaciones.
        

---

##  Comparativa entre Lazo Abierto y Cerrado

|Característica|Lazo Abierto|Lazo Cerrado|
|---|---|---|
|Retroalimentación|No|Sí|
|Precisión|Limitada|Alta|
|Robustez|Poca|Alta ante perturbaciones|
|Complejidad|Baja|Alta (sensor, cálculo, análisis)|
|Costo computacional|Bajo|Medio a alto (según el controlador)|
|Sensibilidad|Alta|Menor, especialmente ante errores|

---

##  Ejemplos en Aplicaciones Reales

- **Robótica móvil**: mantener una trayectoria (PID en posición y orientación).
    
- **Drones**: control de actitud (giroscopios y controladores PID o LQR).
    
- **Electrónica de potencia**: regulación de tensión de salida.
    
- **Climatización (HVAC)**: mantener temperatura deseada.
    
- **Sistemas biomédicos**: control de infusores de medicamentos o respiradores.
    

---

##  Tipos de Controladores en Lazo Cerrado

- **Proporcional (P)**: rápido, pero con error en régimen permanente.
    
- **Proporcional-Integral (PI)**: elimina el error, pero puede oscilar.
    
- **Proporcional-Derivativo (PD)**: mejora la respuesta transitoria.
    
- **PID**: combina todos los anteriores, el más utilizado en la industria.
    

---

###  Conclusión

Los **sistemas de lazo cerrado** son fundamentales para el control automático, permitiendo que los sistemas físicos respondan de forma estable, precisa y robusta frente a variaciones internas y perturbaciones externas. Su correcta modelación y diseño es una piedra angular en campos como la robótica, la automatización industrial, la mecatrónica y los sistemas embebidos. La elección entre un lazo abierto o cerrado, y el tipo de controlador a emplear, dependerá de los requisitos dinámicos del sistema, su sensibilidad al entorno y el coste computacional permitido.

¿Deseas que desarrolle un ejemplo con ecuaciones diferenciales o simulación en MATLAB/Simulink para ilustrar el diseño de un sistema en lazo cerrado?