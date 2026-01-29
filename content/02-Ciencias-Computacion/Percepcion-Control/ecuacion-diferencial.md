---
title: "Ecuacion Diferencial"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
Las **ecuaciones diferenciales** son uno de los **pilares fundamentales de la ciencia moderna**, especialmente en la ingeniería, la física y la tecnología. Representan el **puente entre el cambio y la estructura**, permitiendo modelar **cómo evolucionan los sistemas dinámicos en el tiempo**. Su invención y sistematización marcaron un **antes y un después** en la forma en que los humanos comprenden, describen y predicen el comportamiento del mundo natural.

---

##  ¿Qué es una ecuación diferencial?


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Una **ecuación diferencial** es una relación matemática entre una función desconocida y sus derivadas respecto a una o más variables independientes. En términos simples:

> Describe **cómo cambia algo que cambia**.

Por ejemplo:
$$

dydt=ky\frac{dy}{dt} = ky
$$

Dice: “la tasa de cambio de yy respecto al tiempo es proporcional a su valor actual”, lo que da lugar al crecimiento exponencial. Esto modela desde **poblaciones biológicas** hasta **intereses bancarios** o **procesos radiactivos**.

---

##  ¿Por qué se utilizan?

Porque permiten modelar sistemas **dinámicos**, es decir, aquellos en los que el estado **evoluciona con el tiempo**. Estos sistemas son la norma en la realidad física, no la excepción.

###  Son esenciales para describir:

- **Movimiento**: las leyes de Newton son ecuaciones diferenciales (2ª ley: F=maF = ma).
    
- **Circuitos eléctricos**: las leyes de Kirchhoff generan EDs con voltaje y corriente.
    
- **Mecánica de fluidos**: Navier-Stokes son EDs parciales.
    
- **Epidemias**: el modelo SIR usa EDs para modelar el número de infectados.
    
- **Economía**: modelos de crecimiento, inflación o consumo.
    
- **Robótica**: posición, velocidad, aceleración de actuadores.
    

---

##  ¿Por qué fueron un antes y un después?

Antes de las ecuaciones diferenciales, la física se apoyaba en **geometría estática** o proporciones. La aparición de las EDs permitió **pasar del análisis cualitativo al cuantitativo**, de la descripción al **pronóstico matemático**.

###  Nacimiento de las EDs

Las ecuaciones diferenciales aparecen **formalmente en el siglo XVII** con **Newton** y **Leibniz**, que inventan el **cálculo diferencial e integral** para resolver problemas de movimiento.

- Newton, en los _Principia Mathematica_ (1687), plantea la **segunda ley del movimiento** como una relación diferencial.
    
- Leibniz desarrolla notación moderna (dy/dxdy/dx) y pone las bases del análisis moderno.
    

###  Avances posteriores

- **Euler** (siglo XVIII): sistematiza el estudio de EDs ordinarias y ofrece soluciones generales.
    
- **Lagrange y Laplace**: aplican EDs al estudio de la mecánica, la electricidad y la astronomía.
    
- **Fourier** y **Poisson**: usan EDs parciales para calor y ondas.
    
- En el siglo XX, las EDs son el motor de la **teoría de sistemas, control automático**, y simulación de procesos complejos.
    

---

##  Impacto en ingeniería y ciencia

###  En ciencia:

- Permiten describir el **universo físico** con precisión: desde el péndulo hasta la expansión del cosmos.
    
- Son la base de la **mecánica cuántica**, **relatividad**, **biología matemática** y **climatología**.
    

### ️ En ingeniería:

- Se utilizan para:
    
    - Modelar y simular sistemas eléctricos, térmicos, mecánicos.
        
    - Diseñar controladores (PID, adaptativos, LQR).
        
    - Analizar estabilidad y dinámica de sistemas complejos.
        
    - Automatizar procesos industriales.
        

---

##  ¿Qué ventajas tienen?

|Ventaja|Implicación en la práctica|
|---|---|
|Modelan el cambio continuo|Permiten estudiar sistemas físicos realistas|
|Permiten simulación|Se pueden resolver numéricamente (MATLAB, Python)|
|Son predictivas|Se pueden anticipar comportamientos futuros|
|Unifican física y matemática|Conectan teoría con observación experimental|

---

##  Solución de ecuaciones diferenciales

###  Analíticas:

- Métodos clásicos: separación de variables, factores integrantes, método de Euler, Laplace.
    
- Limitados a ecuaciones “simples”.
    

###  Numéricas:

- Para sistemas complejos: Runge-Kutta, Euler, simulaciones en Simulink.
    
- Usados en casi todas las aplicaciones de ingeniería actuales.
    

---

##  Conclusión

Las **ecuaciones diferenciales cambiaron la historia del pensamiento humano**, permitiendo **formalizar las leyes del cambio**. Son esenciales para modelar cualquier sistema físico, económico o biológico que evolucione en el tiempo. Su aplicación es universal: desde el diseño de un dron o un motor eléctrico, hasta la predicción del clima o la simulación del corazón humano. En la ingeniería moderna, son **la columna vertebral del modelado matemático y el análisis dinámico**.

¿Quieres que te muestre cómo se resuelve una ED de primer o segundo orden con condiciones iniciales? ¿O cómo se representa gráficamente en MATLAB o Python?
Una **ecuación diferencial** es una relación matemática que involucra una **función desconocida** y sus **derivadas** respecto a una o más variables independientes. En el contexto de **sistemas de control**, las ecuaciones diferenciales describen el **comportamiento dinámico** de sistemas físicos, eléctricos, mecánicos, térmicos, etc., relacionando la entrada u(t)u(t), la salida y(t)y(t), y sus derivadas.

---

##  Ecuaciones diferenciales en sistemas de control

Los sistemas dinámicos se modelan mediante ecuaciones diferenciales **ordinarias** (ODEs), donde la variable independiente es generalmente el tiempo tt.

###  Forma general (lineal e invariante en el tiempo):
$$

andny(t)dtn+an−1dn−1y(t)dtn−1+⋯+a1dy(t)dt+a0y(t)=bmdmu(t)dtm+⋯+b0u(t)a_n \frac{d^n y(t)}{dt^n} + a_{n-1} \frac{d^{n-1} y(t)}{dt^{n-1}} + \dots + a_1 \frac{dy(t)}{dt} + a_0 y(t) = b_m \frac{d^m u(t)}{dt^m} + \dots + b_0 u(t)
$$

- y(t)y(t): salida del sistema
    
- u(t)u(t): entrada del sistema
    
- ai,bja_i, b_j: coeficientes constantes (si es LTI)
    
- El **orden** de la ecuación es el mayor grado de derivada de y(t)y(t)
    

---

##  Ejemplos por orden

### 1️⃣ Primer orden

Sistema RC (carga de un condensador):
$$

RCdy(t)dt+y(t)=u(t)RC \frac{dy(t)}{dt} + y(t) = u(t)
$$

- Entrada: voltaje aplicado
    
- Salida: voltaje en el condensador
    

---

### 2️⃣ Segundo orden

Sistema masa-resorte-amortiguador:
$$

md2y(t)dt2+cdy(t)dt+ky(t)=F(t)m \frac{d^2 y(t)}{dt^2} + c \frac{dy(t)}{dt} + k y(t) = F(t)
$$

- Entrada: fuerza F(t)F(t)
    
- Salida: posición y(t)y(t)
    
- Coeficientes:
    
    - mm: masa
        
    - cc: coef. de amortiguamiento
        
    - kk: constante del resorte
        

---

### 3️⃣ Tercer orden

Sistema eléctrico con RLC + controlador:
$$

Ld3y(t)dt3+Rd2y(t)dt2+1Cdy(t)dt+y(t)=u(t)L \frac{d^3 y(t)}{dt^3} + R \frac{d^2 y(t)}{dt^2} + \frac{1}{C} \frac{dy(t)}{dt} + y(t) = u(t)
$$

- Típico en modelos eléctricos complejos o mecatrónicos.
    

---

##  Relación con función de transferencia

Aplicando la **transformada de Laplace**, estas ecuaciones se convierten en **funciones de transferencia**:

Ejemplo:
$$

τdy(t)dt+y(t)=Ku(t)⟶G(s)=Y(s)U(s)=Kτs+1\tau \frac{dy(t)}{dt} + y(t) = K u(t) \quad \longrightarrow \quad G(s) = \frac{Y(s)}{U(s)} = \frac{K}{\tau s + 1}
$$

Esto permite:

- Análisis algebraico.
    
- Diseño de controladores.
    
- Simulación en el dominio de Laplace.
    

---

## ️ Linealidad y tiempo invarianza

Una ecuación diferencial es:

- **Lineal** si los términos con y(t)y(t) o sus derivadas están en forma lineal (no se elevan al cuadrado, no aparecen como productos).
    
- **Invariante en el tiempo** si los coeficientes ai,bja_i, b_j son constantes.
    

---

##  Conclusión

Las **ecuaciones diferenciales** son el lenguaje matemático natural para describir **sistemas dinámicos físicos**. Su análisis permite entender cómo un sistema responde a estímulos (entradas) y cómo evoluciona su estado (salida). En sistemas de control, se usan para obtener funciones de transferencia, diseñar controladores y predecir estabilidad y rendimiento.

¿Te gustaría que resuelva un ejemplo paso a paso partiendo de una ecuación diferencial real y obteniendo su función de transferencia o su solución temporal?