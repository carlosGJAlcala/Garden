---
title: "Introducción a la teoría de control"
tags: [universidad, 4anyo, pyc]
date: 2026-08-12
lang: es
---
# T3. IntroduccionTeoriaControl 2017 2018

Grado en Ingeniería de Computadores
Percepción y Control
Tema 3. Introducción a la
Teoría de Control
Elena López Guillén
Manuel Ocaña Miguel
Daniel Pizarro Pérez
Departamento
de Electrónica
Índice del Tema

## 1. introducción a los sistemas de control ( 2 h)

1. INTRODUCCIÓN A LOS SISTEMAS DE CONTROL ( 2 h)

## 2. métodos de análisis de sistemas de control ( 4 h)

2. MÉTODOS DE ANÁLISIS DE SISTEMAS DE CONTROL ( 4 h)

## 3. métodos de diseño de controladores ( 2 h)

3. MÉTODOS DE DISEÑO DE CONTROLADORES ( 2 h)
Departamento Grado en Ingeniería de Computadores –Percepción y Control 2
de Electrónica

## 1. introducción a los

1. Introducción a los
sistemas de control
Departamento
de Electrónica
Índice

## 1. introducción a los sistemas de control

1. INTRODUCCIÓN A LOS SISTEMAS DE CONTROL

- 1.1. ¿Qué es un sistema de control?
- 1.2. Control en lazo abierto y en lazo cerrado
- 1.3. Ejemplos de sistemas de control
- 1.4. Evolución de la teoría de control
- 1.5. Modelado de sistemas dinámicos
  - 1.5.1. Tipos de sistemas
  - 1.5.2. Ecuaciones diferenciales de los sistemas físicos
  - 1.5.3. Herramienta matemática: la transformada de Laplace
  - 1.5.4. Función de transferencia
  - 1.5.5. Matriz de transferencia
  - 1.5.6. Representación de sistemas de control mediante diagramas de bloques
- 1.6. Estabilidad absoluta de sistemas de control
- 1.7. Efectos de la realimentación

Departamento Grado en Ingeniería de Computadores –Percepción y Control 4
de Electrónica

Introducción a los sistemas de control

### 1.1 ¿Qué es un sistema de control?

Sistema de control: Interconexión de componentes que regulan el comportamiento de un
sistema o proceso para conseguir que éste se comporte de la manera deseada.

```
Variable no manipulable (PERTURBACIÓN)

Variable manipulable                                       Variable controlada
(ENTRADA) ──► Proceso a controlar (PLANTA) ──► (SALIDA)
```

OBJETIVO: actuar convenientemente sobre la señal de ENTRADA para que la SALIDA
se comporte de la manera deseada ( según una señal de REFERENCIA) sin
que afecten ( o lo menos posible) las PERTURBACIONES o errores
internos del proceso a controlar.

Departamento Grado en Ingeniería de Computadores –Percepción y Control 5
de Electrónica

Introducción a los sistemas de control

### 1.2 Control en lazo abierto y en lazo cerrado

#### a) Control en lazo abierto

La salida no tiene efecto sobre la acción de control.

```
Respuesta deseada (REFERENCIA) ──► [Acción de control] ──► CONTROLADOR ──► Proceso a controlar (PLANTA) ──► Variable controlada (SALIDA)

Ej: Temperatura deseada ──► Ej: Sistema de aire acondicionado (Ej: Aire expulsado) ──► Ej: Temperatura habitación (Ej: Habitación cerrada)
```

CARACTERÍSTICAS:

- Fácil construcción
- Necesidad de conocer muy bien el comportamiento de la planta
- Muy sensible a perturbaciones externas y/o variaciones de parámetros internos de la planta (Ej: ¿y si abrimos una ventana?)

Departamento Grado en Ingeniería de Computadores –Percepción y Control 6
de Electrónica

Introducción a los sistemas de control

#### b) Control en lazo cerrado (realimentado)

La salida se mide y se compara con la señal de referencia para corregir convenientemente
la acción de control.

```
                              Error      Acción de
Respuesta deseada  ──►  COMPARADOR  ──►  control  ──►  CONTROLADOR  ──►  Proceso a controlar (PLANTA)  ──►  Variable controlada (SALIDA)
(REFERENCIA)                 ▲                                                                                          │
                              │                                                                                         │
                              └───────────────────────────────────  MEDIDOR  ◄──────────────────────────────────────────┘

Ej: Temperatura deseada  ──►  COMPARADOR  ──►  Ej: Sistema de aire acondicionado  ──►  Ej: Aire expulsado  ──►  Ej: Habitación cerrada (PLANTA)  ──►  Ej: Temperatura habitación (SALIDA)
                                                                                                                                     │
                                                                                                                                     │
                                                                                            Ej: Sensor de temperatura (MEDIDOR)  ◄────┘
```

CARACTERÍSTICAS: Ej: Sensor de temperatura

- Más complejos y caros (necesidad de sensor y comparador)
- No es necesario conocer con precisión el proceso a controlar
- Insensible a perturbaciones externas o variaciones de parámetros (Ej: ¿y si abrimos una ventana?)
- Necesidad de asegurar la estabilidad del sistema realimentado

Departamento Grado en Ingeniería de Computadores –Percepción y Control 7
de Electrónica

Introducción a los sistemas de control

### 1.3 Ejemplos de sistemas de control
Control manual de la dirección de un automóvil:
Departamento Grado en Ingeniería de Computadores –Percepción y Control 8
de Electrónica
Introducción a los sistemas de control
Control de la renta nacional ( ejemplo de aplicación a un modelo económico):
Departamento Grado en Ingeniería de Computadores –Percepción y Control 9
de Electrónica
Introducción a los sistemas de control
Control automático de una unidad de disco:
Departamento Grado en Ingeniería de Computadores –Percepción y Control 10
de Electrónica
Introducción a los sistemas de control
Control digital ( por ordenador) de la temperatura de un horno eléctrico:
Departamento Grado en Ingeniería de Computadores –Percepción y Control 11
de Electrónica
Introducción a los sistemas de control
Control multivariable para un generador de caldera:
Departamento Grado en Ingeniería de Computadores –Percepción y Control 12
de Electrónica
Introducción a los sistemas de control
#### Control de un robot móvil (sistema multisensorial)

```
                              Entorno
                                 │
                            (SENSORES)
                                 │
                                 ▼
                SISTEMA DE PERCEPCIÓN DEL ENTORNO:
                        - Visión
                        - Tacto
                        - Audición
                        - Proximidad
                        - Otros
                                 │
                                 ▼
                        SISTEMA DE CONTROL
```

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 13
de Electrónica

Introducción a los sistemas de control

### 1.4 Evolución de la teoría de control

Se distinguen dos grandes grupos o enfoques en la teoría de control:

```
                                  Teorías de control
                    ┌───────────────────────┴───────────────────────┐
          Basadas en modelos                            Basadas en comportamientos
     ┌──────────────┴──────────────┐                  ┌────────────┼────────────┐
Teoría de control          Teoría de control      Control        Control      Control
clásica                    moderna (V.V.E.E)       robusto        neuronal     borroso
  │
  ├─ Dominio del tiempo (continuo o discreto)
  └─ Dominio de la frecuencia
```

Nos centramos en la teoría clásica de control, sólo aplicable a SISTEMAS LINEALES E INVARIANTES
EN EL TIEMPO (sistemas LTI – linear and time invariant systems).

Departamento Grado en Ingeniería de Computadores –Percepción y Control 14
de Electrónica

Introducción a los sistemas de control

### 1.5 Modelado de sistemas dinámicos
Para diseñar y analizar sistemas de control se utilizan modelos matemáticos de los sistemas
físicos que los componen.

MODELO DE UN SISTEMA: descripción matemática del mismo que permite predecir su
comportamiento sin necesidad de experimentar sobre él.

```
SISTEMA REAL  ──(modelado)──►  MODELO DEL SISTEMA  ──►  Análisis de comportamiento
```

¿Para qué sirven?

- Para mejorar la comprensión del sistema
- Para simular el comportamiento del sistema
- Punto de partida para el diseño de controladores

Departamento Grado en Ingeniería de Computadores –Percepción y Control 15
de Electrónica

Introducción a los sistemas de control

#### 1.5.1. Tipos de sistemas (revisión)

```
x(t) ──►  SISTEMA  ──►  y(t)
```

| Lineales | No lineales |
| --- | --- |
| Si al aplicar x₁(t) la salida es y₁(t)… y al aplicar x₂(t) la salida es y₂(t)…, entonces al aplicar a·x₁(t)±b·x₂(t), la salida es a·y₁(t)±b·y₂(t). Permiten aplicar SUPERPOSICIÓN | No cumplen la condición de linealidad |

| Invariantes | Variantes |
| --- | --- |
| Si al aplicar x(t) la salida es y(t)…, entonces al aplicar x(t-T), la salida es y(t-T). La salida es la misma independientemente del momento en que se aplica la entrada | No cumplen la condición de invarianza |

| Causales | No causales |
| --- | --- |
| La salida nunca precede a la entrada | No cumplen la propiedad de causalidad |

| Estables | Inestables |
| --- | --- |
| Ante entradas acotadas, sólo producen salidas acotadas | No cumplen condición de estabilidad |

| Estáticos | Dinámicos |
| --- | --- |
| La salida sólo depende del valor de la entrada en el tiempo actual | La salida depende de la entrada y del momento en que se aplicó ("evolucionan" ante la aplicación de una entrada) |

| Continuos (en tiempo continuo) | Discretos (en tiempo discreto) |
| --- | --- |
| Las señales de entrada y salida pueden cambiar en cualquier instante de tiempo | Las señales de entrada y salida sólo cambian en instantes de tiempo periódicos |

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 16
de Electrónica

Introducción a los sistemas de control

#### 1.5.2. Ecuaciones diferenciales de los sistemas físicos

Permiten modelar en el dominio del tiempo el comportamiento dinámico de sistemas físicos
(mecánicos, eléctricos, térmicos, etc.) a partir de sus leyes físicas.

Ej: Ecuación diferencial para el siguiente sistema eléctrico:

$$x(t) = R \cdot i(t) + L \cdot \frac{di(t)}{dt} + \frac{1}{C}\int i(t)\,dt$$

```
x(t) ──►  SISTEMA ELÉCTRICO  ──►  y(t)
```

donde $y(t) = \dfrac{1}{C}\displaystyle\int i(t)\,dt$

Utilizando el operador derivada $D = \dfrac{d}{dt}$:

$$x(t) = R\cdot i(t) + LD\cdot i(t) + \frac{1}{CD}\cdot i(t) = \left[R + LD + \frac{1}{CD}\right] i(t) \;\Rightarrow\; i(t) = \frac{x(t)}{R + LD + \dfrac{1}{CD}}$$

$$y(t) = \frac{1}{CD}\cdot i(t) = \frac{\frac{1}{CD}}{R+LD+\frac{1}{CD}}\cdot x(t) = \frac{1}{CLD^2+RCD+1}\cdot x(t)$$

$$CLD^2y(t) + RCDy(t) + y(t) = x(t)$$

Conocida la entrada x(t), permite obtener la salida y(t), despejándola de la ecuación diferencial:

$$CL\,y''(t) + RC\,y'(t) + y(t) = x(t)$$

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 17
de Electrónica

Introducción a los sistemas de control
#### 1.5.3. Herramienta matemática: la transformada de Laplace

Facilita la resolución de ecuaciones diferenciales para sistemas lineales e invariantes,
convirtiéndolas en ecuaciones algebraicas.

```
DOMINIO DEL TIEMPO                                     DOMINIO DE LAPLACE (o de la frecuencia compleja)

Ecuación diferencial lineal  ──Transformada de Laplace──►  Transformada de Laplace de la ecuación diferencial

        │                                                              │
        │ Integración de la ec. diferencial                           │ Operaciones algebraicas
        ▼                                                              ▼

Solución en el dominio del tiempo  ◄──Transformada inversa de Laplace──  Solución en el dominio de Laplace
```

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 18
de Electrónica

Introducción a los sistemas de control

##### a) Definición de transformada de Laplace

$\mathcal{L}$: Transformada de Laplace de f(t)

Función o señal en el dominio del tiempo: f(t) → F(s)

s es una variable compleja (se habla de PLANO s).

Para señales causales (no existen para t<0), se utiliza la TRANSFORMADA DE LAPLACE UNILATERAL:

$$F(s) = \mathcal{L}[f(t)] = \int_{0}^{\infty} f(t)\cdot e^{-st}\,dt$$

Para señales típicas, encontramos TABLAS DE TRANSFORMADAS, que podemos utilizar para
evitar resolver la integral anterior en cada caso.

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 19
de Electrónica

Introducción a los sistemas de control

##### b) Pares importantes de transformadas de Laplace

| f(t) | F(s) |
| --- | --- |
| Impulso unitario δ(t) | 1 |
| Escalón unitario u(t) | 1/s |
| t | 1/s² |
| tⁿ | n!/s^(n+1) |
| e^(-at) | 1/(s+a) |
| t·e^(-at) | 1/(s+a)² |
| tⁿ·e^(-at) | n!/(s+a)^(n+1) |
| sen(ωt) | ω/(s²+ω²) |
| cos(ωt) | s/(s²+ω²) |

Departamento Grado en Ingeniería de Computadores –Percepción y Control 20
de Electrónica

(ver más en tablas de transformadas)

Introducción a los sistemas de control

##### c) Propiedades importantes de la transformada de Laplace

| Operación dominio tiempo | Resultado dominio Laplace |
| --- | --- |
| A·f(t) | A·F(s) |
| f₁(t)±f₂(t) | F₁(s)±F₂(s) |
| e^(-at)·f(t) | F(s+a) |
| f(t-t₀) | F(s)·e^(-t₀s) |
| f'(t) | s·F(s)-f(0) |
| fⁿ(t) | sⁿ·F(s) − Σ (r=1 a n) s^(n-r)·f^(r-1)(0) |
| $\int_{0}^{t} f(\tau)\,d\tau$ | F(s)/s |
| f₁(t)*f₂(t) | F₁(s)⋅F₂(s) |

(ver más en tablas de propiedades)

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 21
de Electrónica

Introducción a los sistemas de control

##### d) Teoremas importantes de la transformada de Laplace

Teorema del valor inicial: permite calcular el valor inicial de la señal a partir de su
transformada.

$$f(0^+) = \lim_{t \to 0^+} f(t) = \lim_{s \to \infty} s\cdot F(s)$$

Teorema del valor final: permite calcular el valor final de señales estables a partir de
su transformada. La señal es estable si s·F(s) presenta todos los polos en el semiplano
izquierdo del plano S.

$$\lim_{t \to \infty} f(t) = \lim_{s \to 0} s\cdot F(s)$$

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 22
de Electrónica

Introducción a los sistemas de control

##### e) Transformada inversa de Laplace

$\mathcal{L}^{-1}$: Transformada de F(s) → f(t), función o señal en el dominio del tiempo

Definición:

$$f(t) = \mathcal{L}^{-1}[F(s)] = \frac{1}{2\pi j}\int_{c-j\infty}^{c+j\infty} F(s)\cdot e^{st}\cdot ds$$

(donde c es una constante real mayor que las partes reales de todos los polos de F(s))

En la práctica, en ingeniería de control, suele ser más sencillo utilizar tablas de
transformadas. Si la transformada buscada no viene directamente en las tablas, se
expande F(s) en fracciones parciales de manera que los términos obtenidos sí que
puedan encontrarse directamente en las tablas.

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 23
de Electrónica

##### f) Expansión en Fracciones Parciales

(revisar expansión en fracciones parciales de F(s) = B(s)/A(s), siendo B(s) y A(s) polinomios en s, y A(s) de grado mayor que B(s))

*(Las siguientes fórmulas de descomposición en fracciones parciales quedaron con los caracteres esparcidos en celdas de tabla rotas del extractor de PDF, incluyendo exponentes/subíndices intercalados fuera de orden. Dado que es una derivación matemática con varios coeficientes (no una simple frase), no se ha reconstruido el álgebra exacta por el riesgo de introducir un error en un apunte de estudio — se preserva el enunciado de cada ejemplo, que sí es legible, y se apuntan los fragmentos numéricos identificables.)*

**Ej 1**: Transformada inversa cuando F(s) contiene polos reales simples

```
F(s) = (s+3) / [(s+1)(s+2)] = 2/(s+1) + (-1)/(s+2)  ⟶  f(t) = 2e^(-t) - e^(-2t), t ≥ 0
```

**Ej 2**: Transformada inversa cuando F(s) contiene polos reales múltiples

*(Numerador s²+2s+3 sobre (s+1)³, descompuesto en fracciones parciales sobre (s+1)³, (s+1)² y (s+1) con coeficientes 2, 0, 1 respectivamente; resultado del tipo f(t) = t·e^(-t) + e^(-t) = (t+1)e^(-t), t ≥ 0.)*

**Ej 3**: Transformada inversa cuando F(s) contiene polos complejos conjugados

*(Numerador 2s+12 sobre s²+2s+5, reescrito como 5·(s+1)/[(s+1)²+2²] + 2·2/[(s+1)²+2²]; resultado: f(t) = 5e^(-t)sen(2t) + 2e^(-t)cos(2t), t ≥ 0.)*

##### g) Ejemplo de Resolución de una Ecuación Diferencial Utilizando la Transformada de Laplace

*(Diagrama: entrada x(t) → SISTEMA DINÁMICO → salida y(t))*

Obtener y(t) si se aplica la entrada x(t)=3u(t) y el sistema parte del reposo (condiciones iniciales nulas):

```
y''(t) + 2y'(t) + 5y(t) = x(t)     (modelo en el dominio del tiempo)
```

1. Sustituimos la entrada en la ecuación diferencial:

```
y''(t) + 2y'(t) + 5y(t) = 3u(t)
```

2. Pasamos al dominio de Laplace:

```
s²Y(s) + 2sY(s) + 5Y(s) = 3/s
```

3. Solución en el dominio de Laplace (operaciones algebraicas):

```
Y(s) = 3 / [s·(s² + 2s + 5)]
```

4. Transformada inversa para obtener solución en dominio tiempo:

*(El resultado final quedó igualmente scrambleado por el extractor; los fragmentos legibles son "e^(-t)sen(2t)", "e^(-t)cos(2t)" con denominadores 5 y 10, compatibles con una solución del tipo y(t) = 3/5 − (3/5)e^(-t)cos(2t) − (3/10)e^(-t)sen(2t), t ≥ 0 — no se afirma como resultado exacto por no poder verificar los coeficientes con certeza.)*

Grado en Ingeniería de Computadores –Percepción y Control
Departamento 25
de Electrónica
Introducción a los sistemas de control

#### 1.5.4. Función de Transferencia (FT)

Permite modelar directamente en el dominio de Laplace el comportamiento de sistemas dinámicos lineales e invariantes siempre que partan del reposo (condiciones iniciales nulas).

*(Diagrama: entrada x(t) → SISTEMA con FT H(s) → salida y(t))*

Dos formas de definirla:

1. Cociente entre Y(s) y X(s) para cualquier entrada x(t):

```
H(s) = Y(s) / X(s)
```

2. Transformada de Laplace de la respuesta impulsiva del sistema h(t) (respuesta cuando en la entrada se aplica un impulso unitario x(t)=δ(t)):

```
H(s) = L[h(t)]
```

##### Ej: FT del Sistema Eléctrico de la Diapositiva 14

Ecuación diferencial del sistema (modelo en dominio del tiempo):

*(Diagrama: entrada x(t) → SISTEMA ELÉCTRICO → salida y(t))*

```
CL·y''(t) + RC·y'(t) + y(t) = x(t)
```

Obtenemos la FT utilizando la primera definición de la diapositiva anterior. Para ello:

1. Pasamos la ecuación diferencial al dominio de Laplace:

```
CLs²Y(s) + RCsY(s) + Y(s) = X(s)
```

2. Obtenemos H(s)=Y(s)/X(s):

```
H(s) = Y(s)/X(s) = 1 / (CLs² + RCs + 1) = (1/CL) / [s² + (R/L)s + 1/(CL)]
```

A partir de la FT H(s)=B(s)/A(s) definimos:

1. Polos del sistema: valores de s para los que H(s)→∞ (raíces de A(s))
2. Ceros del sistema: valores de s para los que H(s)→0 (raíces de B(s))
3. Orden del sistema: grado de A(s) (siempre mayor o igual que el de B(s))

#### 1.5.5. Matriz de Transferencia

La FT sólo permite modelar sistemas SISO (Single Input – Single Output).

Para sistemas MIMO (Multiple Input – Multiple Output) lineales e invariantes, podemos aplicar superposición para obtener la MATRIZ DE TRANSFERENCIA: las FT's entre cada salida y entrada suponiendo el resto de entradas nulas:

*(Fórmula con notación matricial e índices dobles (Gᵢⱼ), parcialmente esparcida por el extractor en celdas de tabla; se preserva el significado: cada elemento Gᵢⱼ(s) = Yᵢ(s)/Xⱼ(s) evaluado con las demás entradas nulas.)*

```
Gᵢⱼ(s) = Yᵢ(s) / Xⱼ(s)   (con xₖ(t)=0 para k≠j)

| Y₁(s) |   | G₁₁(s)  G₁₂(s)  ...  G₁ₘ(s) |   | X₁(s) |
| Y₂(s) |   | G₂₁(s)  G₂₂(s)  ...  G₂ₘ(s) |   | X₂(s) |
|  ...  | = |   ...     ...   ...   ...   | · |  ...  |
| Yₙ(s) |   | Gₙ₁(s)  Gₙ₂(s)  ...  Gₙₘ(s) |   | Xₘ(s) |
```

#### 1.5.6. Representación de Sistemas de Control Mediante Diagramas de Bloques

Los sistemas de control se representan mediante diagramas de bloques, cada uno de ellos con su FT.

*(Diagrama de bloques con varias funciones de transferencia H1(s), H2(s), H3(s), H5(s) combinadas en serie, paralelo y realimentación entre la entrada X(s) y la salida Y(s).)*

Para obtener la FT total del sistema H_TOT(s) = Y(s)/X(s) recurrimos a reglas básicas de simplificación de diagramas de bloques.

##### Reglas Básicas de Simplificación de Diagramas de Bloques

**a) Conexión en serie.** Se multiplican las funciones de transferencia:

```
H_TOT(s) = H1(s) · H2(s)
```

**b) Conexión en paralelo.** Se suman las funciones de transferencia:

```
H_TOT(s) = H1(s) + H2(s)
```

**c) Conexión en realimentación (negativa, para sistema estable).**

FT o "ganancia" en lazo cerrado:

```
H_TOT(s) = G(s) / [1 + G(s)·H(s)]
```

Se define también la FT o "ganancia" en lazo abierto:

```
H_Lazo(s) = G(s) · H(s)
```

### 1.6 Estabilidad Absoluta de Sistemas de Control

La condición necesaria y suficiente para que un sistema de control sea estable es que todos los polos de la función de transferencia del sistema tengan partes reales negativas (se encuentren en el semiplano izquierdo del plano s).

*(Diagrama del plano S dividido en zona estable y zona inestable, separadas por el límite de estabilidad.)*

Tipos de análisis de estabilidad:

a) Estabilidad absoluta. Clasificación del sistema como ESTABLE/INESTABLE
b) Estabilidad relativa. Evaluación de la estabilidad en función de un parámetro del sistema

### 1.7 Efectos de la Realimentación

Sistema de control realimentado. Permite:

*(Diagrama: Referencia r(t) → Controlador → Planta G(s) → Salida y(t), con realimentación K=1 a través de Sensor H(s))*

1. Estabilización de plantas inestables diseñando H(s) de manera que todos los polos del sistema en lazo cerrado estén en el semiplano izquierdo.
2. Mejora de la respuesta temporal del sistema, acelerando el transitorio y reduciendo el error en régimen permanente gracias a la acción del controlador sobre los polos del sistema.
3. Rechazo a perturbaciones. Si la salida se ve afectada por una perturbación, el sistema tiende a reducir de nuevo el error modificando convenientemente la señal de control.
4. Reducción de la sensibilidad ante variaciones en parámetros de la planta.

## 2. Métodos de Análisis de Sistemas de Control
Departamento
de Electrónica
Índice

## 2. métodos de análisis de sistemas de control

2. MÉTODOS DE ANÁLISIS DE SISTEMAS DE CONTROL
2.1. Introducción
2.2. Análisis de la respuesta temporal
2.2.1. Concepto de respuesta temporal
2.2.2. Sistemas de primer orden
2.2.3. Sistemas de segundo orden
2.2.4. Efecto de polos y ceros adicionales
2.2.5. Especificaciones de la respuesta temporal
2.2.6. Lugares geométricos del plano s
2.2.7. Error en régimen permanente
2.3. Análisis mediante el lugar de las raíces
2.3.1. Concepto de lugar de las raíces
2.3.2. Ejemplos e interpretación del lugar de las raíces
2.4. Análisis de la respuesta frecuencial
2.4.1. Concepto de respuesta frecuencial
Departamento Grado en Ingeniería de Computadores –Percepción y Control 34
de Electrónica
Métodos de análisis de sistemas de control
### 2.1 Introducción

Dentro de la TEORÍA CLÁSICA de control, se aplican diferentes métodos de análisis de sistemas de control:

1. Análisis de la respuesta temporal. Consiste en estudiar la respuesta del sistema ante la aplicación de diferentes "entradas de prueba".
2. Análisis mediante el lugar de las raíces. Permite estudiar las características del sistema ante la variación de un parámetro del mismo.
3. Análisis de la respuesta frecuencial. Consiste en aplicar entradas senoidales de distintas frecuencias y estudiar la atenuación y desfasaje introducidos por el sistema.

### 2.2 Análisis de la Respuesta Temporal

#### 2.2.1. Concepto de Respuesta Temporal

Es la evolución de la salida y(t) ante la aplicación de una determinada entrada x(t) conocida.

*(Diagrama: entrada x(t) → SISTEMA DINÁMICO H(s) → salida y(t))*

¿Cómo obtenemos y(t)?

Se utilizan "entradas de prueba" típicas:
- Impulso: x(t)=δ(t) -> en este caso y(t)=h(t)=L⁻¹(H(s))
- Escalón: x(t)=u(t)
- Rampa: x(t)=t·u(t)
- Parábola: x(t)=t²·u(t)

Para obtener y(t) a partir de una entrada de prueba x(t):

1. Y(s) = H(s)·X(s) → y(t) = L⁻¹[Y(s)]
2. Podemos deducir las características de y(t) a partir de H(s) (sus polos y ceros), sin necesidad de realizar la transformada inversa anterior para volver al dominio del tiempo.

##### Ejemplo de Respuesta Temporal de un Sistema Estable

Entrada escalón: x(t)=R·u(t)

*(Diagrama: entrada R·u(t) → SISTEMA ESTABLE H(s) → salida y(t), que se estabiliza en el valor y_ss)*

La respuesta consta de dos partes:
- **Régimen transitorio**: parte inicial de la respuesta, antes de que se estabilice el valor final. Depende de los polos y ceros de H(s), y no de la entrada aplicada.
- **Régimen permanente**: cuando se estabiliza el valor final y(t→∞). Depende de la entrada aplicada. Concepto de ganancia estática H_ss (ganancia introducida por el sistema en régimen permanente):

```
H_ss = y_ss / R = lim(s→0) s·Y(s) / R = lim(s→0) s·H(s)·(R/s) / R = lim(s→0) H(s)
```

#### 2.2.2. Sistemas de Primer Orden

Sistema de primer orden estándar (sin ceros adicionales), con H_ss=1:

```
H(s) = 1 / (τ·s + 1)
```

El polo del sistema se encuentra en s = -1/τ:

- Si τ<0 → polo en semiplano derecho → sistema inestable.
- Si τ>0 → polo en semiplano izquierdo → sistema estable (caso de interés).

Respuesta al escalón unitario x(t)=u(t):

```
Y(s) = H(s)·X(s) = 1/(τ·s+1) · 1/s  →  y(t) = (1 - e^(-t/τ))·u(t)
```

τ = constante de tiempo del sistema (determina la duración del régimen transitorio). Es el tiempo que tarda la respuesta en alcanzar el 63% del valor final. El régimen transitorio se considera prácticamente extinguido tras t≈5τ.

Generalización del sistema de primer orden estándar:

1. Si la ganancia estática es A:

```
H(s) = A / (τ·s + 1)
```

   La respuesta al escalón unitario alcanza el 63% de A (0.63·A) en t=τ, y se estabiliza en A tras t≈5τ.

2. Si además tiene un retardo (tiempo muerto) L:

```
H(s) = A / (τ·s + 1) · e^(-L·s)
```

   La respuesta al escalón unitario es igual que en el caso anterior pero desplazada L unidades de tiempo: alcanza el 63% de A en t=L+τ, y se estabiliza en A tras t≈L+5τ.

#### 2.2.3. Sistemas de Segundo Orden

Sistema de segundo orden estándar (sin ceros adicionales), con H_ss=1:

```
H(s) = ωn² / (s² + 2·ξ·ωn·s + ωn²)
```

Los parámetros que lo caracterizan son:

- ξ → coeficiente de amortiguamiento (adimensional)
- ωn → pulsación natural (rad/s)

Siendo ωd = ωn·√(1-ξ²) la pulsación amortiguada, los polos del sistema son:

```
s1,2 = -ξ·ωn ± j·ωn·√(1-ξ²) = -ξ·ωn ± j·ωd
```

*Interpretación geométrica de ωn y ξ (plano s):*

- ωn es la distancia de los polos al origen: dist = √((ξωn)² + ωd²) = ωn
- ξ es el coseno del ángulo η: ξ = cos(η)

Respuesta al escalón unitario x(t)=u(t):

```
Y(s) = H(s)·X(s) = ωn² / [s·(s² + 2ξωn·s + ωn²)]

y(t) = 1 - [1/√(1-ξ²)]·e^(-ξωn·t)·sen(ωd·t + atan(√(1-ξ²)/ξ))
```

Notar que:

- La envolvente exponencial de la amplitud depende únicamente de -ξωn, que es la PARTE REAL DE LOS POLOS.
- La frecuencia de la oscilación es la de la pulsación amortiguada ωd, que es la PARTE IMAGINARIA DE LOS POLOS.
- La forma de esta respuesta varía en función del coeficiente de amortiguamiento, lo que da lugar a una clasificación de los sistemas de segundo orden.

##### Clasificación de los sistemas de segundo orden (en función de ξ)

**1. ξ<0 → SISTEMA INESTABLE**

Como ωn>0, la parte real de los polos es positiva:

- Si los polos tienen parte imaginaria, existe parte oscilatoria, con envolvente creciente.
- Si los polos no tienen parte imaginaria (reales), no hay oscilación: suma de dos exponenciales crecientes.

**2. ξ=0 → SISTEMA OSCILANTE (límite de la estabilidad)**

Como ξ=0, los polos tienen parte real nula (sobre el eje imaginario), en s=±j·ωn. La amplitud de la respuesta senoidal es constante:

```
y(t) = 1 - sen(ωn·t + π/2) = 1 - cos(ωn·t)
```

La frecuencia de oscilación es la de la pulsación natural ωn.

**3. 0<ξ<1 → SISTEMA SUBAMORTIGUADO**

Polos complejos conjugados en el semiplano izquierdo. Existe parte oscilatoria con envolvente decreciente. La frecuencia de oscilación es la de la pulsación amortiguada ωd.

**4. ξ=1 → SISTEMA CRÍTICAMENTE AMORTIGUADO**

Corresponde a dos polos con la misma parte real (negativa) y sin parte imaginaria (no hay parte oscilatoria en la respuesta).

> [!note]
> No es igual que la respuesta exponencial de un sistema de primer orden.

**5. ξ>1 → SISTEMA SOBREAMORTIGUADO**

Dos polos reales en el semiplano izquierdo (suma de dos exponenciales decrecientes): una exponencial más rápida y otra más lenta. Para la misma ωn, la respuesta es más lenta que la de amortiguamiento crítico.

*Resumen de la respuesta al impulso de los sistemas de segundo orden: el original incluye aquí una figura comparativa que no se ha podido recuperar de la extracción OCR.*

#### 2.2.4. Efecto de Polos y Ceros Adicionales

Partiendo de un sistema de segundo orden estándar:

- Un cero próximo a los polos dominantes aumenta el sobreimpulso.
- Polos y ceros muy cercanos entre sí cancelan sus efectos.
- Generalmente, se ajustan los sistemas para que, en caso de existir múltiples polos, dos de ellos sean dominantes (y complejos conjugados). Polos y/o ceros al menos 5 veces más alejados del origen se desprecian. **TODOS DEBEN ESTAR EN SEMIPLANO IZQUIERDO PARA ESTABILIDAD.**
- Un cero en semiplano derecho hace que el sistema sea de FASE NO MÍNIMA (respuesta inicial en sentido contrario al valor final, respuesta mucho más rápida frente a los polos dominantes).

#### 2.2.5. Especificaciones de la Respuesta Temporal

Para sistemas de segundo orden subamortiguados (los más habituales), existen otros parámetros más intuitivos que ξ y ωn para caracterizar su respuesta temporal:

> [!note]
> Las fórmulas siguientes sólo son válidas para sistemas estándar (sin ceros adicionales).

1. **Tiempo de subida (tr)**: tiempo en pasar del 10% al 90% del valor final la primera vez.

```
tr = 1.8 / ωn
```

2. **Sobreimpulso máximo (Mp)**: diferencia entre el valor máximo y el valor final, normalizada.

```
Mp = (y_max - y_ss) / y_ss = e^(-ξπ/√(1-ξ²))
```

3. **Tiempo de pico (tp)**: tiempo en alcanzar el sobreimpulso máximo.

```
tp = π / ωd
```

4. **Tiempo de establecimiento (ts)**: tiempo en alcanzar y mantenerse dentro de un rango de error respecto al valor final (habitualmente 2%).

```
ts(2%) = 4 / (ξ·ωn)
```

#### 2.2.6. Lugares Geométricos del Plano s

1. **¿Puntos del plano s con el mismo tiempo de subida tr?**

```
tr = 1.8/ωn = cte  →  ωn = cte
```

   Son puntos sobre una circunferencia con centro en el origen del plano s y radio ωn (ωn es la distancia de los polos al origen). ωn crece → tr disminuye.

2. **¿Puntos del plano s con el mismo sobreimpulso Mp?**

```
Mp = e^(-ξπ/√(1-ξ²)) = cte  →  ξ = cte  →  η = arccos(ξ) = cte
```

   Son puntos sobre una recta que pasa por el origen formando un ángulo η con el eje real negativo (η es el ángulo formado por los polos y el eje real negativo). ξ crece → Mp disminuye. Caso ξ=0 → eje imaginario; caso ξ=1 → eje real (INESTABLE, zona límite).

3. **¿Puntos del plano s con el mismo tiempo de pico tp?**

```
tp = π/ωd = cte  →  ωd = cte
```

   Son puntos sobre una recta horizontal del plano s (y su conjugada), ya que ωd es la parte imaginaria de los polos. ωd crece → tp disminuye.

4. **¿Puntos del plano s con el mismo tiempo de establecimiento ts?**

```
ts = 4/(ξ·ωn) = 4/σ = cte  →  σ = cte
```

   Son puntos sobre una recta vertical del plano s, ya que σ=ξ·ωn es la parte real de los polos. σ crece → ts disminuye.

#### 2.2.7. Errores en Régimen Permanente

En régimen permanente interesa estudiar el error entre la señal de referencia y la señal de salida: e(t) = r(t) - y(t). Sin embargo, es más sencillo estudiar el error a la salida del comparador, e(t) (ERROR DEL SISTEMA), ya que sólo depende de:

a) La entrada aplicada (escalón, rampa, parábola, etc.)
b) El TIPO DEL SISTEMA = número de polos en el origen que presenta la GANANCIA DE LAZO G(s)·H(s):

```
G(s)·H(s) = K·(s+c1)···(s+cm) / [sᴺ·(s+p1)···(s+pn)]
```

- Si N=0 → sistema TIPO 0
- Si N=1 → sistema TIPO 1
- Si N=2 → sistema TIPO 2
- …

Una vez conocido el ERROR DEL SISTEMA (salida del comparador), suele ser sencillo calcular el error entre la referencia y la salida a partir de él. El error del sistema se calcula mediante fórmulas sencillas que utilizan los conocidos como COEFICIENTES ESTÁTICOS DE ERROR.

Para un sistema con realimentación E(s) = R(s) / [1 + G(s)·H(s)], el error en régimen permanente se obtiene mediante el teorema del valor final:

```
ess = lim(t→∞) e(t) = lim(s→0) s·E(s)
```

**1. Entrada de tipo ESCALÓN**: r(t) = R₀·u(t) → R(s) = R₀/s

```
ess = lim(s→0) s·E(s) = R₀ / (1 + Kpos),  con Kpos = lim(s→0) G(s)·H(s)
```

Kpos = COEFICIENTE ESTÁTICO DE ERROR DE POSICIÓN.

- Si el sistema es TIPO 0 → Kpos=cte. → ess=cte. Sigue el escalón con un error constante.
- Si el sistema es TIPO 1 o superior → Kpos=∞ → ess=0. Sigue el escalón sin error.

**2. Entrada de tipo RAMPA**: r(t) = R₀·t·u(t) → R(s) = R₀/s²

```
ess = lim(s→0) s·E(s) = R₀ / Kvel,  con Kvel = lim(s→0) s·G(s)·H(s)
```

Kvel = COEFICIENTE ESTÁTICO DE ERROR DE VELOCIDAD.

- Si el sistema es TIPO 0 → Kvel=0 → ess=∞. El error va creciendo con el tiempo.
- Si el sistema es TIPO 1 → Kvel=cte. → ess=cte. Sigue la rampa con error constante.
- Si el sistema es TIPO 2 o superior → Kvel=∞ → ess=0. Sigue la rampa con error nulo.

**3. Entrada de tipo PARÁBOLA**: r(t) = (R₀/2)·t²·u(t) → R(s) = R₀/s³

```
ess = lim(s→0) s·E(s) = R₀ / Kacel,  con Kacel = lim(s→0) s²·G(s)·H(s)
```

Kacel = COEFICIENTE ESTÁTICO DE ERROR DE ACELERACIÓN.

- Si el sistema es TIPO 0 ó 1 → Kacel=0 → ess=∞. El error va creciendo con el tiempo.
- Si el sistema es TIPO 2 → Kacel=cte. → ess=cte. Sigue la parábola con error constante.
- Si el sistema es TIPO 3 o superior → Kacel=∞ → ess=0. Sigue la parábola con error nulo.

**Resumen y conclusión** (entrada unitaria, R₀=1):

| Tipo de sistema | Escalón | Rampa | Parábola |
| --- | --- | --- | --- |
| 0 | Kpos=K → ess=1/(1+K) | Kvel=0 → ess=∞ | Kacel=0 → ess=∞ |
| 1 | Kpos=∞ → ess=0 | Kvel=K → ess=1/K | Kacel=0 → ess=∞ |
| 2 | Kpos=∞ → ess=0 | Kvel=∞ → ess=0 | Kacel=K → ess=1/K |

Cuanto mayor es el TIPO de un sistema, mejor se comporta en régimen permanente (mayor capacidad de seguimiento de entradas complejas). Los POLOS EN EL ORIGEN en la GANANCIA DE LAZO de un sistema son beneficiosos para mejorar su respuesta en régimen permanente.

### 2.3. Análisis Mediante el Lugar de las Raíces

#### 2.3.1. Concepto de Lugar de las Raíces

Supóngase un sistema en el que existe algún parámetro variable K (típicamente en el controlador, pero puede ser en cualquier otra posición del lazo). La función de transferencia de este sistema es:

```
T(s) = K·G(s) / [1 + K·G(s)·H(s)]
```

- Los POLOS del sistema nos informan sobre la estabilidad del sistema.
- Los POLOS (junto con los ceros) nos informan sobre su respuesta temporal.

Para calcular los polos: 1 + K·G(s)·H(s) = 0 (ECUACIÓN CARACTERÍSTICA DEL SISTEMA). LOS POLOS DEL SISTEMA DEPENDEN DE K (no así los ceros).

El **LUGAR DE LAS RAÍCES** de un sistema es una gráfica que muestra cómo se "mueven" sus polos en el plano s cuando va variando el valor de K.

Ideas generales:

- Al cambiar K no aparecen nuevos polos, sólo se mueven los que hay (el orden del sistema se mantiene).
- Cada polo se mueve de forma continua por el plano s al variar K, formando una RAMA.
- El lugar de las raíces siempre es simétrico respecto al eje real (todo polo complejo tiene su conjugado).
- Si escribimos 1 + K·G(s)·H(s) = 1 + K·N(s)/D(s) = 0 → D(s) + K·N(s) = 0:
  - Para K=0, los polos están sobre los polos de la ganancia de lazo G(s)H(s).
  - Para K→∞, los polos tienden al valor de los ceros de la ganancia de lazo G(s)H(s).
- Al crecer K desde 0 hasta ∞, cada rama va desde un polo de G(s)H(s) hacia un cero de G(s)H(s) o hacia el infinito si hay más polos que ceros.

#### 2.3.2. Ejemplos e Interpretación del Lugar de las Raíces

**Ejemplo 1**

Ecuación característica:

```
1 + K / [s·(s+2)] = 0
```

- El sistema es de segundo orden (tiene 2 polos, y por lo tanto el LR tiene 2 ramas).
- Para K=0, las ramas parten de los polos de la ganancia de lazo (s=0 y s=-2).
- Para K→∞, las ramas van hacia el infinito.

Interpretación:

- El sistema siempre es estable para cualquier K>0.
- Para ganancias K pequeñas, es sobreamortiguado.
- El sistema presenta amortiguamiento crítico para un valor concreto de K.
- Para ganancias K grandes, es subamortiguado.

**Ejemplo 2**

Ecuación característica:

```
1 + K·(s²-4s+13) / [(s+3)·(s²+4s+5)] = 0
```

- El sistema es de tercer orden (tiene 3 polos, y por lo tanto el LR tiene 3 ramas).
- Para K=0, las ramas parten de los polos de la ganancia de lazo.
- Para K→∞, las ramas van hacia los ceros de la ganancia de lazo y el infinito.

Interpretación:

- El sistema se hace inestable para ganancias grandes.
- ¿Es posible una respuesta subamortiguada? ¿Existirían dos polos dominantes y un tercero despreciable?

### 2.4. Análisis de la Respuesta Frecuencial

#### 2.4.1. Concepto de Respuesta en Frecuencia

Si a un sistema lineal G(s) se le aplica una entrada sinusoidal x(t) = A·sen(ωt), la salida en régimen permanente es otra sinusoide de la misma frecuencia, pero con amplitud y desfasaje distintos:

```
y(t) = A·|G(jω)|·sen(ωt + φ)
```

La ganancia |G(jω)| y el desfasaje φ introducidos por el sistema corresponden al MÓDULO y la FASE, respectivamente, de la RESPUESTA EN FRECUENCIA del sistema, que es la función de transferencia G(s) pero evaluada en s=jω (sobre el eje imaginario del plano s) y en régimen permanente:

```
G(jω) = G(s)|s=jω = |G(jω)|·e^(jφ)
```

La respuesta en frecuencia suele mostrarse gráficamente utilizando DIAGRAMAS DE BODE.

Características de la respuesta en frecuencia:

- Puede obtenerse fácilmente de forma experimental.
- Permite obtener conclusiones generales sobre el sistema (respuesta transitoria, régimen permanente, estabilidad, etc.).
- Existen técnicas de diseño de controladores que se aplican directamente utilizando la respuesta frecuencial.

## 3. métodos de diseño

3. Métodos de diseño
de controladores
Departamento
de Electrónica
Índice

## 3. métodos de diseño de controladores

3. MÉTODOS DE DISEÑO DE CONTROLADORES
3.1. Introducción
3.1.1. Especificaciones de diseño
3.1.2. Topologías básicas de controladores
3.2. Controlador todo-nada
3.3. Acciones básicas de control
3.3.1. Acción proporcional
3.3.2. Acción integral
3.3.3. Acción derivativa
3.4. Controladores PID
3.4.1. Características generales
3.4.2. Ajuste de PIDs
Departamento Grado en Ingeniería de Computadores –Percepción y Control 62
de Electrónica
Métodos de diseño de controladores
### 3.1. Introducción

#### 3.1.1. Especificaciones de Diseño

El diseño de un controlador tiene como objetivo que el conjunto del sistema se comporte según ciertas ESPECIFICACIONES DE DISEÑO, que pueden ser de varios tipos:

1. Relativas a la estabilidad del sistema. Ejemplos: conseguir estabilizar una planta inestable, o mejorar la estabilidad relativa de un sistema.
2. Relativas al régimen transitorio de la respuesta. Ejemplos: reducir el sobreimpulso, reducir el tiempo de pico, reducir el tiempo de establecimiento, etc.
3. Relativas al régimen permanente del sistema. Ejemplos: anular el error estacionario ante entradas escalón, reducir el error ante entradas tipo rampa, etc.

#### 3.1.2. Topologías Básicas de Controladores

a) De "compensación simple": el controlador G(s) se sitúa en serie con la planta, dentro de un lazo con realimentación H(s) (CONTROLADOR - PLANTA). Según dónde se sitúe el controlador dentro del lazo, se distingue entre **controlador serie** y **controlador paralelo**.

b) De "doble compensación": se combinan dos bloques de control (CONTROL_1, CONTROL_2) junto con la planta y dos realimentaciones H(s), H2(s). Según la disposición de los bloques de control se distingue entre **controlador "feed-forward"** y **controlador "forward"**.

*Nota: los diagramas de bloques originales de esta sección no se han podido reconstruir con exactitud a partir de la extracción OCR (posiciones de bloques y flechas se perdieron); se conserva la descripción textual de cada topología.*

### 3.2. Controlador Todo-Nada

- Es el controlador más simple, pero tiene bastantes aplicaciones.
- Es un controlador NO LINEAL (no tiene función de transferencia en Laplace).
- Las funciones de transferencia típicas son:

```
Si e(t) > 0,  u(t) = U2
Si e(t) < 0,  u(t) = U1
```

  o, con una banda muerta entre E1 y E2:

```
Si e(t) > E2,  u(t) = U2
Si e(t) < E1,  u(t) = U1
```

- Ejemplo:

### 3.3. Acciones Básicas de Control

#### 3.3.1. Control Proporcional

Características:

```
u(t) = Kp·e(t)
```

- Señal de control proporcional al error (si no hay error, no hay señal de control).
- Si la planta es TIPO 0, no permite anular el error en régimen permanente ante escalón:

```
H(s) = U(s)/E(s) = Kp
```

  El error en régimen permanente disminuye al aumentar Kp, pero no llega a anularse (menor error a mayor Kp).
- Variando Kp modificamos la posición de los polos del sistema (lugar de las raíces). En muchas ocasiones, un incremento excesivo de Kp puede desestabilizar el sistema.

#### 3.3.2. Control Integral

Características:

```
u(t) = Ki·∫e(t)·dt
```

- Mientras hay error, la señal de control crece (o decrece), y se mantiene al valor alcanzado cuando desaparece el error.
- Introduce un polo en el origen en la ganancia de lazo:

```
H(s) = U(s)/E(s) = Ki/s
```

  → incrementa en 1 el TIPO del sistema, mejorando el seguimiento de entradas en régimen permanente.
- La introducción de este polo en el origen modifica el lugar de las raíces del sistema, empeorando el transitorio (más lento e inestable).

#### 3.3.3. Control Derivativo

Características:

```
u(t) = Kd·de(t)/dt
```

- Variaciones rápidas de la señal de error generan señales de control elevadas. Sin embargo, errores grandes y constantes no generan señal de control (por eso el control derivativo nunca se usa sólo).

```
H(s) = U(s)/E(s) = Kd·s
```

- En combinación con otras acciones de control (proporcional o integral), contribuye mejorando la respuesta transitoria (respuesta más rápida y estable).
- Ejemplo: control PD, H(s) = Kp + Kd·s, introduce un cero en el LR.

### 3.4. Controladores PID

#### 3.4.1. Características Generales

Combinan las acciones de control anteriores:

```
u(t) = Kp·e(t) + Ki·∫e(t)·dt + Kd·de(t)/dt

H(s) = U(s)/E(s) = Kp + Ki/s + Kd·s
```

- La acción integral mejora los errores en régimen permanente.
- La acción derivativa mejora la respuesta transitoria.
- La acción proporcional permite ajustar la estabilidad relativa.

En general, sus efectos están acoplados, por eso los PIDs suelen ajustarse por métodos experimentales. Combinaciones más usadas: P, I, PD, PI y PID.

#### 3.4.2. Ajuste de PIDs

Una de las técnicas más utilizadas es la de Ziegler-Nichols:

**a) Para plantas de primer orden** (respuesta al escalón unitario caracterizada por su ganancia estática A, constante de tiempo τ y retardo L, con H(s) = (A/(τ·s+1))·e^(-L·s)):

| Estructura | Kp | Ki | Kd |
| --- | --- | --- | --- |
| P | τ/(A·L) | — | — |
| PI | 0.9·τ/(A·L) | Kp/(3·L) | — |
| PID | 1.2·τ/(A·L) | Kp/(2·L) | Kp·0.5·L |

**b) Para plantas de segundo orden** (método de la ganancia crítica, en lazo cerrado):

1. Anular las constantes Ki y Kd, y escoger un valor bajo para Kp.
2. Ir incrementando Kp hasta que el sistema oscile, y anotar el periodo de oscilación T_osc, y el valor de la ganancia proporcional crítica Kp,osc.
3. Utilizar las siguientes reglas empíricas:

| Estructura | Kp | Ki | Kd |
| --- | --- | --- | --- |
| P | 0.5·Kp,osc | — | — |
| PI | 0.45·Kp,osc | Kp/(0.833·T_osc) | — |
| PID | 0.6·Kp,osc | Kp/(0.5·T_osc) | Kp·0.125·T_osc |

---

**Laboratorio (Grupo reducido)**: Diseño de algoritmos de control para robots Pioneer en Player/Stage.
