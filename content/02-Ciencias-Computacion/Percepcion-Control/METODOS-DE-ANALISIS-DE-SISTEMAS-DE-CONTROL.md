---
title: "Metodos De Analisis De Sistemas De Control"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
El **análisis de sistemas de control** consiste en estudiar el comportamiento dinámico y estable de un sistema, a partir de su representación matemática, para **evaluar su desempeño, estabilidad, precisión, rapidez y robustez**. Existen varios métodos de análisis, clasificados según el dominio de trabajo (tiempo o frecuencia) y la representación del sistema (ecuaciones diferenciales, funciones de transferencia, espacio de estados, etc.).

A continuación, se presenta una explicación detallada, técnica y orientada a nivel de ingeniería.

---

##  Clasificación de los métodos de análisis


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Percepcion-Control/SISTEMA-DE-LAZO|SISTEMA DE LAZO]]. [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]]. [[01-Ciberseguridad/Herramientas/Modulo-de-python3-httpserver|Modulo de python3 httpserver]].

###  1. Análisis en el **Dominio del Tiempo**

Evalúa cómo responde el sistema ante una **entrada determinada** (escalón, impulso, rampa...), observando su evolución temporal.

#### a) **Respuesta temporal (transitoria y estacionaria)**

- Mide cómo el sistema responde ante entradas típicas:
    
    - **Escalón unitario**
        
    - **Impulso unitario**
        
    - **Rampa**
        
- Se analiza:
    
    - Tiempo de establecimiento tst_s
        
    - Tiempo de subida trt_r
        
    - Sobreimpulso MpM_p
        
    - Error en régimen permanente esse_{ss}
        

#### b) **Error en régimen permanente**

- Se calcula usando el **teorema del valor final**:
    $$

    lim⁡t→∞e(t)=lim⁡s→0sE(s)\lim_{t \to \infty} e(t) = \lim_{s \to 0} s E(s)
    $$

- Depende del tipo de entrada y del tipo del sistema (número de polos en el origen).
    
- Se define la **constante de posición KpK_p**, velocidad KvK_v o aceleración KaK_a, según el tipo de entrada.
    

#### c) **Simulación temporal**

- Uso de herramientas como **MATLAB/Simulink** para obtener gráficas de respuesta en tiempo real ante diversas entradas.
    

---

###  2. Análisis en el **Dominio de la Frecuencia**

Estudia cómo responde el sistema a señales senoidales de distintas frecuencias. Muy útil para analizar **robustez**, **estabilidad relativa** y **diseño de compensadores**.

#### a) **Diagramas de Bode**

- Representación logarítmica de:
    
    - Ganancia (en dB) vs frecuencia (log(ω))
        
    - Fase vs frecuencia
        
- Permite obtener:
    
    - Margen de ganancia GMGM
        
    - Margen de fase PMPM
        
    - Frecuencia de cruce de ganancia / fase
        

#### b) **Diagrama de Nyquist**

- Representa la respuesta en frecuencia compleja$$
 G(jω)G(j\omega).$$

    
- El **criterio de Nyquist** se usa para analizar la **estabilidad de lazo cerrado** basándose en la cantidad de rodeos al punto −1-1 en el plano complejo.
    

#### c) **Diagrama de Nichols**

- Relación entre ganancia (dB) y fase (º).
    
- Útil en el diseño de compensadores de fase o ganancia.
    

---

###  3. Análisis mediante **Lugar de las Raíces (Root Locus)**

Estudia cómo se mueven los **polos del sistema de lazo cerrado** en el plano ss cuando se varía un parámetro (usualmente la ganancia KK).

- Permite visualizar:
    
    - Estabilidad.
        
    - Rapidez de la respuesta (polos más a la izquierda → más rápido).
        
    - Oscilaciones (parte imaginaria).
        
    - Posiciones dominantes.
        
- Método gráfico que facilita el diseño interactivo de controladores.
    

---

###  4. Análisis en el **Espacio de Estados**

Representa el sistema como un conjunto de **ecuaciones diferenciales de primer orden** en forma matricial. Fundamental para sistemas multivariable (MIMO) y control moderno.

#### a) **Forma general**
$$

x˙(t)=Ax(t)+Bu(t)y(t)=Cx(t)+Du(t)\dot{x}(t) = A x(t) + B u(t) \\ y(t) = C x(t) + D u(t)
$$

- x(t)x(t): vector de estado
    
- u(t)u(t): entrada
    
- y(t)y(t): salida
    

#### b) **Ventajas del espacio de estados**

- Válido para sistemas **no lineales** y **tiempo variante**.
    
- Permite análisis de **controlabilidad** y **observabilidad**.
    
- Facilita el diseño de:
    
    - **Controladores en tiempo discreto**.
        
    - **Observadores de estado** (ej. de Luenberger, Kalman).
        
    - **Control óptimo** (LQR, MPC).
        

---

###  5. Análisis de Estabilidad

Evalúa si el sistema se mantiene acotado ante una entrada acotada (criterio BIBO) o si la salida tiende a cero cuando no hay entrada (criterio asintótico).

#### a) **Método de Routh-Hurwitz**

- Permite determinar estabilidad sin calcular raíces del polinomio característico.
    
- Se construye la tabla de Routh y se verifica el número de cambios de signo.
    

#### b) **Criterio de Nyquist**

- Ya mencionado: analiza estabilidad considerando la respuesta en frecuencia abierta y la cantidad de polos en el semiplano derecho.
    

#### c) **Ubicación de los polos**

- Un sistema es estable si **todos los polos de la función de transferencia están en el semiplano izquierdo** (parte real negativa).
    

---

##  Ejemplo práctico de combinación de métodos

Un ingeniero que diseña un controlador PID puede:

1. Analizar la **respuesta al escalón** (dominio temporal).
    
2. Validar la **estabilidad con el lugar de raíces**.
    
3. Evaluar el **margen de fase con Bode**.
    
4. Verificar el error de seguimiento con el **teorema del valor final**.
    
5. Simular el comportamiento completo en **Simulink**.
    

---

##  Conclusión

Los **métodos de análisis de sistemas de control** proporcionan una caja de herramientas matemáticas y gráficas que permiten **evaluar y optimizar el comportamiento dinámico** de sistemas físicos o digitales. La elección del método dependerá del tipo de sistema, los objetivos del diseño y las herramientas disponibles. Para un ingeniero, **dominar tanto los métodos clásicos (transferencia, Bode, lugar de raíces)** como los **modernos (espacio de estados, control multivariable)** es fundamental para abordar problemas de control robusto, adaptativo y en tiempo real.

¿Deseas que te prepare un resumen visual en forma de tabla o diagrama conceptual con todos estos métodos?