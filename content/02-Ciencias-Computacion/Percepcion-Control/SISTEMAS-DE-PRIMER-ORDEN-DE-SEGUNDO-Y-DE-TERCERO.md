---
title: "Sistemas De Primer Orden De Segundo Y De Tercero"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
En ingeniería de control, los **sistemas de primer, segundo y tercer orden** se clasifican según el **grado de su [[ecuacion-diferencial]] característica**, o, de forma equivalente, según el número de **polos** en su **función de transferencia**.

Estas categorías determinan **la dinámica del sistema**: su rapidez de respuesta, su comportamiento transitorio (oscilaciones, retardo), su estabilidad y su sensibilidad a entradas o perturbaciones.

---

##  SISTEMA DE PRIMER ORDEN


> **Relacionado**: [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]]. [[01-Ciberseguridad/Herramientas/Modulo-de-python3-httpserver|Modulo de python3 httpserver]]. [[03-Desarrollo-Software/Distribuido/Apache-httpd|Apache httpd]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/Apache-Axis-Java-y-HTTP|Apache Axis Java y HTTP]]. [[02-Ciencias-Computacion/Matematicas/Aritmetica-modular/Teorema-Chino-de-los-Restos-CRT|Teorema Chino de los Restos CRT]].

###  Definición

Tiene **una única constante de tiempo**, y su comportamiento se define por una **ecuación diferencial de primer grado**.

###  Ecuación diferencial:
$$

τdy(t)dt+y(t)=Ku(t)\tau \frac{dy(t)}{dt} + y(t) = K u(t)
$$

###  Función de transferencia:
$$

G(s)=Kτs+1G(s) = \frac{K}{\tau s + 1}
$$

- KK: ganancia estática
    
- τ\tau: constante de tiempo
    

###  Respuesta al escalón unitario:
$$

y(t)=K(1−e−t/τ)y(t) = K \left(1 - e^{-t/\tau} \right)
$$

###  Características:

- Tiempo de establecimiento ≈ 4τ4\tau
    
- Respuesta suave, sin oscilaciones
    
- Muy común en sistemas térmicos, hidráulicos, algunos eléctricos (RC)
    

---

##  SISTEMA DE SEGUNDO ORDEN

###  Definición

Posee **dos polos** (pueden ser reales o complejos conjugados). Permite representar **oscilaciones**, **sobresaltos** y una gama más rica de respuestas dinámicas.

###  Ecuación diferencial:
$$

d2y(t)dt2+2ζωndy(t)dt+ωn2y(t)=ωn2u(t)\frac{d^2y(t)}{dt^2} + 2 \zeta \omega_n \frac{dy(t)}{dt} + \omega_n^2 y(t) = \omega_n^2 u(t)
$$

###  Función de transferencia:
$$

G(s)=Kωn2s2+2ζωns+ωn2G(s) = \frac{K \omega_n^2}{s^2 + 2\zeta \omega_n s + \omega_n^2}
$$

- ωn\omega_n: frecuencia natural
    
- ζ\zeta: factor de amortiguamiento
    

###  Comportamiento según ζ\zeta:

|Tipo|ζ\zeta|Comportamiento|
|---|---|---|
|Subamortiguado|0<ζ<10 < \zeta < 1|Oscilatorio, con sobreimpulso|
|Críticamente amortiguado|ζ=1\zeta = 1|Más rápido sin oscilaciones|
|Sobreamortiguado|ζ>1\zeta > 1|Lento, sin oscilaciones|
|No amortiguado|ζ=0\zeta = 0|Oscilaciones perpetuas|

###  Métricas clave:

- **Sobreimpulso MpM_p**:
    $$

    Mp=e(−πζ1−ζ2)M_p = e^{\left(-\frac{\pi \zeta}{\sqrt{1 - \zeta^2}}\right)}$$

- **Frecuencia de oscilación**:
    
    $$
ωd=ωn1−ζ2\omega_d = \omega_n \sqrt{1 - \zeta^2}$$


---

##  SISTEMA DE TERCER ORDEN

###  Definición

Tiene **tres polos**, por lo que su comportamiento es más complejo. Puede tener:

- Tres reales
    
- Un real + un par complejo conjugado
    

Se usa para modelar sistemas con **retardo**, **inercia múltiple**, o **interacción de múltiples subsistemas**.

###  Ejemplo de función de transferencia típica:

$$
G(s)=K(s+a)(s2+2ζωns+ωn2)G(s) = \frac{K}{(s + a)(s^2 + 2\zeta \omega_n s + \omega_n^2)}$$


###  Análisis típico:

- Si un polo está **mucho más lejos** que los otros dos (es decir, tiene parte real más negativa), se puede **aproximar a un sistema de segundo orden dominante**.
    
- Si todos los polos están “cerca”, se requiere simulación o análisis detallado.
    

###  Ejemplo físico:

- Un robot con tres etapas: sensor → actuador → carga.
    
- Un circuito con una combinación de RLC + retardo.
    

---

##  Comparación entre sistemas

|Orden|Nº de Polos|Posible comportamiento|Ejemplo físico|
|---|---|---|---|
|1º|1|Exponencial monótono|Sistema térmico, RC|
|2º|2|Oscilaciones, amortiguación|Servo, resorte-masa-amort.|
|3º|3|Oscilaciones + retardo|Motor + carga + control|

---

##  Conclusión

- Los **sistemas de primer orden** tienen respuesta exponencial suave.
    
- Los **de segundo orden** permiten representar **oscilaciones** y ajustar la **rapidez** y **precisión** con ζ\zeta y ωn\omega_n.
    
- Los **de tercer orden** modelan **dinámicas más realistas**, pero también más difíciles de analizar directamente; se suelen aproximar a modelos de segundo orden si hay polos dominantes.
    

En diseño de control, entender el **orden del sistema** es clave para elegir el tipo de controlador (P, PI, PID, compensador en frecuencia o espacio de estados).