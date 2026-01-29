---
title: "Controlador Pid"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
El **controlador PID** (Proporcional–Integral–Derivativo) es uno de los pilares del control automático en ingeniería. Es **simple, robusto y versátil**, y se utiliza para regular variables físicas como velocidad, temperatura, posición, presión, etc., en sistemas dinámicos de muy diversa índole: mecatrónica, procesos industriales, electrónica, aeronáutica, robótica y más.

---

##  ¿Qué es un controlador PID?


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

Un **controlador PID** genera una **señal de control** u(t)u(t) a partir del **error** entre la señal deseada (referencia r(t)r(t)) y la señal real del sistema (salida y(t)y(t)):
$$

e(t)=r(t)−y(t)e(t) = r(t) - y(t)
$$

La señal de control se calcula como:
$$

u(t)=KPe(t)+KI∫0te(τ) dτ+KDde(t)dtu(t) = K_P e(t) + K_I \int_0^t e(\tau)\,d\tau + K_D \frac{de(t)}{dt}
$$

Donde:

- KPK_P: ganancia **proporcional**
    
- KIK_I: ganancia **integral**
    
- KDK_D: ganancia **derivativa**
    

---

##  Interpretación de cada término

###  Proporcional (P)

- Reacciona **instantáneamente** al error actual.
    
- Cuanto mayor el error, mayor la corrección.
    $$

- uP(t)=KP⋅e(t)u_P(t) = K_P \cdot e(t)
    $$


 Aumenta la **velocidad de respuesta**, pero **nunca elimina por completo el error en régimen permanente**.

---

###  Integral (I)

- Acumula el error a lo largo del tiempo.
    
- Elimina el error estacionario.
    $$

- uI(t)=KI∫e(t) dtu_I(t) = K_I \int e(t)\,dt
    
$$

 Mejora la **precisión**, pero puede introducir **lenteza** u **oscilaciones** si es demasiado alto.

---

###  Derivativo (D)

- Predice el futuro comportamiento del error.
    
- Reacciona a la **velocidad de cambio** del error.
    $$

- uD(t)=KD⋅de(t)dtu_D(t) = K_D \cdot \frac{de(t)}{dt}
    $$


 Mejora la **estabilidad** y **suaviza** la respuesta, pero es sensible al **ruido**.

---

##  Función de transferencia del PID (dominio de Laplace)
$$

C(s)=KP+KIs+KDsC(s) = K_P + \frac{K_I}{s} + K_D s
$$

También puede expresarse como:
$$

C(s)=KP(1+1TIs+TDs)C(s) = K_P \left(1 + \frac{1}{T_I s} + T_D s \right)
$$

donde:
$$

- TI=KPKIT_I = \frac{K_P}{K_I}: tiempo integral
    $$
$$

- TD=KDKPT_D = \frac{K_D}{K_P}: tiempo derivativo
    $$


---

##  Efectos del ajuste de parámetros

|Ganancia|Efecto positivo|Posibles riesgos|
|---|---|---|
|KPK_P alto|Respuesta más rápida|Sobreimpulso, oscilaciones|
|KIK_I alto|Cero error en régimen permanente|Oscilaciones, inestabilidad|
|KDK_D alto|Mayor amortiguación|Ruido amplificado, inestabilidad|

---

## ️ Tipos comunes de controladores

|Tipo|Componentes activos|Aplicación típica|
|---|---|---|
|P|Solo proporcional|Sistemas lentos sin precisión crítica|
|PI|Proporcional + integral|Control de temperatura, velocidad, presión|
|PD|Proporcional + derivativo|Control de posición donde el error final no es crítico|
|PID|Todos|Sistemas generales con alta exigencia de control|

---

##  Ejemplo práctico

Sistema a controlar:
$$

G(s)=1τs+1G(s) = \frac{1}{\tau s + 1}
$$

Controlador PID:
$$

C(s)=KP+KIs+KDsC(s) = K_P + \frac{K_I}{s} + K_D s
$$

Lazo cerrado:
$$

T(s)=C(s)G(s)1+C(s)G(s)T(s) = \frac{C(s) G(s)}{1 + C(s) G(s)}
$$

Al variar KP,KI,KDK_P, K_I, K_D, podemos modificar la **rapidez**, **precisión** y **estabilidad** de la respuesta.

---

##  Implementación práctica

###  En código (ejemplo en Python):

```python
error = setpoint - output
integral += error * dt
derivative = (error - prev_error) / dt
output_control = Kp * error + Ki * integral + Kd * derivative
```

###  En sistemas embebidos:

- El PID se implementa en tiempo discreto.
    
- Se usan técnicas para limitar integral (anti-windup) y filtrar derivadas (anti-noise).
    

---

##  ¿Por qué es tan usado el PID?

- **Simplicidad**: fácil de entender e implementar.
    
- **Robustez**: tolera modelos imprecisos.
    
- **Versatilidad**: se adapta a múltiples tipos de procesos.
    
- **Eficiencia**: buen rendimiento sin requerir optimización compleja.
    

Según estudios, más del **90% de los lazos de control industriales** están basados total o parcialmente en lógica PID.

---

##  Métodos de ajuste

### Manual:

- Prueba y error ajustando KPK_P, KIK_I, KDK_D.
    

### Métodos clásicos:

- **Ziegler-Nichols** (respuesta en lazo abierto o lazo cerrado).
    
- **Cohen-Coon**, **Chien-Hrones-Reswick**.
    

### Modernos:

- Optimización numérica (IA, algoritmos genéticos, etc.).
    
- Tuning automático en herramientas de control (MATLAB, LabVIEW).
    

---

##  Conclusión

El **controlador PID** representa una de las soluciones más eficaces y extendidas para el control de sistemas dinámicos. Su equilibrio entre **teoría y aplicabilidad**, junto con su flexibilidad para ser afinado a distintos entornos, lo convierten en un estándar industrial, educativo y de investigación. Aunque en sistemas muy complejos se usen técnicas avanzadas (estado, MPC, adaptativos), el **PID sigue siendo insustituible** en una enorme variedad de casos.

¿Quieres que veamos cómo se ajusta un PID sobre un sistema de segundo orden, o una simulación paso a paso con MATLAB o Python?