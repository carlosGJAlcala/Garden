---
title: "Amplificadores operacionales"
tags: [universidad, 1cuatri, electronica]
date: 2026-08-13
lang: es
---
# EGIC_T2_AO 2021-22

Fundamentos de Electrónica. Tema 2: Amplificadores Operacionales. El A.O. Ideal.

- Asistencia: https://forms.office.com/r/JA8myuJJAZ
- Exit ticket: https://forms.office.com/r/kbm7jLH0Wg

## Índice

1. Amplificadores Operacionales
   - El A.O. ideal: símbolo, propiedades y zonas de funcionamiento. Función de transferencia.
   - Concepto de realimentación.
2. Configuraciones básicas del AO en Zona Lineal
   - Seguidor de tensión
   - Inversor
   - No-Inversor
   - Sumador inversor
   - Diferenciador
   - Integrador
3. Configuraciones básicas del AO en No Zona Lineal
   - Comparador
   - Comparador con histéresis
   - 555 (no incluido en este tema)

## 1. El A.O. Ideal

### Símbolo, modelo y función de transferencia

- Amplificador integrado (C.I.).
- Gran versatilidad: muchos tipos y aplicaciones; configuraciones típicas sencillas de analizar y diseñar.
- 1ª aproximación: el A.O. ideal.
- Es un amplificador diferencial ideal, caracterizado por (modelo ideal):
  - Impedancia de entrada infinita (Ze → ∞)
  - Impedancia de salida nula (Zs = 0)
  - Ganancia diferencial en lazo abierto infinita (Ad → ∞)
  - CMRR → ∞ (rechazo total al modo común)
- Alimentación simétrica: V CC y V EE.

*Diagrama de la diapositiva: símbolo del amplificador operacional con sus dos entradas (v+ no inversora, v- inversora), la salida vS y las alimentaciones VCC/VEE, junto con el modelo equivalente de fuente de tensión dependiente Ad·vD con impedancia de entrada Ze e impedancia de salida Zs. El layout exacto no se pudo recuperar de la extracción OCR.*

### Símbolo, modelo y función de transferencia (ii): zonas de funcionamiento

- Zona lineal: vS proporcional a vD = (v+ - v-).
- Zona no lineal: saturación.
- Para estar en la zona lineal: vD = 0.
- Si el A.O. no está en zona lineal, la salida es constante (saturada, en alta o baja):
  1. vS ≈ VCC (si vD > 0)
  2. vS ≈ VEE (si vD < 0)
- En ambas zonas, las corrientes de entrada son nulas (i+ = i- = 0).

*Diagrama de la diapositiva: curva de transferencia del A.O. (vS frente a vD), con la zona lineal (pendiente muy pronunciada en torno a vD=0) entre las dos zonas de saturación (vS=VCC y vS=VEE). El layout exacto no se pudo recuperar de la extracción OCR.*

### Fijando la zona de trabajo

- ¿Cómo se logra fijar la zona de trabajo del A.O.? Mediante el uso (o no) de redes externas que devuelven parte de la señal de la salida de vuelta a la entrada: realimentación (Re).
- Es un tema fundamental y será estudiado con detalle en su momento.
- Para mantener al AO en zona lineal, se necesita realimentación negativa (Re-).
- Si no hay realimentación, o esta es contraria (positiva, Re+), el AO pasa a zona no lineal.

### Fijando la zona de trabajo (ii): tipo de realimentación

- ¿Cómo sabemos el tipo de Re? Observando la existencia o no de redes pasivas conectando la salida con la entrada:
  - Si se derivan al terminal (v-) será Re-.
  - Si se derivan al terminal (v+) será Re+.
- Ojo: si la red de realimentación fuese activa, más complicada o dependiente de la frecuencia (L, C, …), es necesario estudiar en detalle el sentido de la Re.

*Diagrama de la diapositiva: comparación entre un A.O. en zona no lineal (sin Re, o con red pasiva llevando la señal al terminal v+) y un A.O. en zona lineal (con red pasiva llevando la señal al terminal v-). El layout exacto no se pudo recuperar de la extracción OCR.*

### Aplicaciones en Zona Lineal: el cortocircuito virtual

- Condición necesaria: Re-.
- En estas condiciones, con el A.O. en zona lineal:
  - La vD de entrada al AO es nula: vD = (v+ - v-) = 0.
  - Además, en el AO ideal las corrientes en las entradas son nulas: i+ = i- = 0.
- Se tiene que la entrada del AO en zona lineal se comporta como un cortocircuito virtual: al mismo tiempo es cortocircuito (v = 0) y circuito abierto (i = 0).
- Esta característica es exclusiva del AO ideal.
- Si trazamos su curva (i-v) de entrada, se tiene un único punto (la intersección de un c.c. con un c.a.): (iD, vD) = (0, 0).
- Esto simplifica mucho el trabajo con AO's.

## 2. Configuraciones básicas del AO en Zona Lineal

### 2.1. Amplificador seguidor: vS = vE

- Amplificador de tensión ideal (A = 1).
- Señal de salida igual a la de entrada.
- Permite adaptar impedancias entre dos circuitos, ya que la impedancia de entrada es muy grande y la de salida muy pequeña.
- Impedancias: Ze → ∞ (muy alta), Zs → 0 (muy pequeña).

*Diagrama de la diapositiva: seguidor de tensión (buffer), con la salida realimentada directamente al terminal v-, la señal vE aplicada en v+, y la salida vS = vE. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.1. Amplificador seguidor: aplicación típica

- Adaptación entre un sensor y el circuito de medida: permite que la señal del sensor no se vea afectada por el equipo de medida.
- Como la impedancia de entrada del seguidor es muy alta, la corriente suministrada por el sensor es prácticamente cero (no depende de Rg).
- Además, vS tampoco depende de RL, ya que la Zs del operacional es prácticamente cero.
- Aplicación típica: acoplar un sensor de señal muy débil (corriente máxima del orden de µA) con un equipo de medida, sin que este cargue al sensor.

*Diagrama de la diapositiva: sensor (fuente vg con resistencia interna Rg) conectado a la entrada del seguidor de tensión (i=0), cuya salida vS ataca al equipo de medida (resistencia de carga RL). El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.2. Amplificador inversor: vS = -k·vE

- Amplificador de tensión inversor.
- El módulo de la ganancia de este amplificador es igual a la relación R2/R1.
- La señal de salida está invertida con respecto a la entrada.
- Ganancia: vS = -(R2/R1)·vE

*Diagrama de la diapositiva: amplificador inversor con R1 entre vE y el terminal v- (nudo virtual), R2 realimentando la salida vS al mismo terminal v-, y v+ a masa. Datos del ejemplo: R1 = 1 KΩ, R2 = 5 KΩ; forma de onda con t = 0,5 ms/div, vE = 2 V/div, vS = 5 V/div. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.2. Amp. inversor: impedancias terminales

- Para la estimación de las impedancias se aplican las técnicas ya estudiadas en Análisis de Circuitos.
- Impedancia de entrada: Ze = R1 (vista desde vE, ya que el terminal v- es un cortocircuito virtual a masa).
- Impedancia de salida: Zs ≈ 0 (la salida del A.O. ideal se comporta como una fuente de tensión ideal).

*Diagrama de la diapositiva: circuitos equivalentes para el cálculo de la impedancia de entrada (viendo R1 desde vE) y de la impedancia de salida (cortocircuitando la entrada y aplicando una fuente de prueba en vS) del amplificador inversor. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.3. Amplificador no-inversor: vS = +k·vE

- Amplificador de tensión no inversor ideal.
- Analizamos el circuito usando las propiedades del A.O. (cortocircuito virtual e i+ = i- = 0).
- El módulo de la ganancia de este amplificador es igual a (1 + R2/R1).
- Ganancia: vS = (1 + R2/R1)·vE
- Señal de salida no invertida respecto a la entrada.
- Inconveniente (leve): k sólo puede ser mayor que 1.

*Diagrama de la diapositiva: amplificador no inversor con vE aplicada directamente en v+, R1 entre v- y masa, y R2 realimentando vS al terminal v-. Datos del ejemplo: R1 = 1 KΩ, R2 = 5 KΩ; forma de onda con t = 0,5 ms/div, vE = 2 V/div, vS = 5 V/div. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.4. Sumador (inversor): vS = -k·∑vEi

- Se obtiene una señal de salida que es proporcional a la suma ponderada, en la relación Ra/Ri, de las diferentes tensiones de entrada.
- El resultado de dicha suma está invertido.
- Con AO ideal (i+ = i- = 0), la impedancia de entrada de cada rama es diferente si las diferentes Ri lo son (Ze,i = Ri).
- La corriente total que llega al nudo virtual (v-) es la suma de las corrientes de cada rama de entrada: iT = iE1 + iE2 + … + iEn, con iEi = vEi/Ri.
- Ganancia (con Ra la resistencia de realimentación): vS = -Ra·(vE1/R1 + vE2/R2 + … + vEn/Rn)
- Caso particular con todas las Ri iguales entre sí: vS = -(Ra/Ri)·∑vEi

*Diagrama de la diapositiva: sumador inversor con n entradas vE1…vEn, cada una a través de su resistencia Ri hasta el nudo virtual (terminal v-), y Ra realimentando la salida vS a ese mismo nudo. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.5. Diferenciador. Vs = K·(dVe/dt)

- La señal de salida vS es proporcional a la variación de la señal de entrada, es decir, a su derivada temporal.
- Para señales sinusoidales de entrada, la salida está desfasada 90º en atraso.
- Relación entrada-salida (dominio del tiempo): vS = -RC·(dvE/dt)
- Dominio de Laplace: vS(s) = -RCs·vE(s)
- Régimen permanente sinusoidal: vS = -RCjω·vE
- Datos del ejemplo de la diapositiva: R = 2 KΩ, C = 150 nF; t = 0,5 ms/div, vE = 2 V/div.
- Problema de estabilidad: en continua el condensador se comporta como un circuito abierto y no hay realimentación negativa; cualquier pequeña componente continua en vE produce la saturación del AO.
- Solución: colocar una resistencia R1 (de valor elevado) en paralelo con el condensador, para evitar esto.
- Una aplicación habitual del diferenciador es como detector de flancos.

*Diagrama de la diapositiva: diferenciador con el condensador C entre vE y el nudo virtual (v-), y la resistencia R realimentando vS a ese mismo nudo; variante con R1 en paralelo con C para el problema de estabilidad en continua. El layout exacto no se pudo recuperar de la extracción OCR.*

### 2.6. Integrador. Vs = K·∫Ve dt

- La señal de salida es proporcional a la integral de la señal de entrada.
- Para señales sinusoidales de entrada, la salida está desfasada 90º en adelanto.
- Relación entrada-salida (dominio del tiempo): vS(t) = -(1/RC)·∫vE dt + vC(t0)
- Dominio de Laplace: vS(s) = -(1/RCs)·vE(s)
- Régimen permanente sinusoidal: vS = -(1/RCjω)·vE
- Datos del ejemplo de la diapositiva: R = 2 KΩ, C = 13 nF; t = 0,5 ms/div, vE = 2 V/div, vS = 5 V/div.

*Diagrama de la diapositiva: integrador con la resistencia R entre vE y el nudo virtual (v-), y el condensador C realimentando vS a ese mismo nudo. El layout exacto no se pudo recuperar de la extracción OCR.*

## 3. Configuraciones básicas del AO en No Zona Lineal

### Función de transferencia (zona no lineal)

- Consideramos el A.O. ideal.
- A.O. sin realimentación (A.O. sin R.): saturación.
  - vS ≈ VCC si V+ > V- (vD > 0)
  - vS ≈ VEE si V- > V+ (vD < 0)
- Con realimentación negativa (R-): zona lineal.
- Con realimentación positiva (R+), o sin realimentación: saturación.
- Aplicaciones de la zona no lineal (saturación):
  - Comparador.
  - Cambiador de forma de onda (de señal analógica a salida cuadrada de niveles VCC y VEE): conmutación.

### 3.1 Comparador (no inversor)

- Comparador no inversor.
- A.O. sin R.: saturación.
  - vS ≈ VCC si vE > VCOMP
  - vS ≈ VEE si vE < VCOMP
- Conmutación de la salida cuando vE cruza el nivel de referencia VCOMP.

*Diagrama de la diapositiva: comparador no inversor, con vE aplicada en v+ y la tensión de referencia VCOMP en v-; forma de onda de vE frente al tiempo y la conmutación correspondiente de vS entre VCC y VEE al cruzar VCOMP. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.1 Comparador — ejemplo de aplicación

- Ejemplo: activar una alarma, alimentando a 5V el circuito digital emisor de una señal acústica sonora, cuando la señal vE proveniente del sensor sea mayor de 2V.
- Comparador no inversor, con VCOMP = 2V (referencia del sensor) y alimentación del comparador VCC = 5V, VEE = 0V en este ejemplo.
- La salida vS del comparador alimenta directamente el pin de alimentación del circuito digital.

*Diagrama de la diapositiva: comparador no inversor conectado a un sensor (referencia VCOMP = 2V en v-) cuya salida vS alimenta el pin de alimentación de un circuito digital emisor de sonido. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.1 Comparador — problemática del ruido

- Una señal de entrada vE con ruido, cerca del nivel de comparación VCOMP, produce conmutaciones indeseadas (rebotes) en la salida vS.
- ¿Cómo solucionar este problema? (se resuelve introduciendo realimentación positiva, dando lugar al comparador con histéresis del siguiente apartado).

*Diagrama de la diapositiva: señal vE con ruido oscilando en torno al nivel VCOMP, y la salida vS del comparador mostrando varias conmutaciones espurias (rebotes) en vez de una única transición limpia. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.1 Comparador (inversor)

- Comparador inversor.
- A.O. sin R.: saturación.
  - vS ≈ VCC si vE < VCOMP
  - vS ≈ VEE si vE > VCOMP
- Mismo principio que el comparador no inversor, pero con la entrada vE aplicada en v- y la referencia VCOMP en v+, lo que invierte el sentido de la conmutación.

*Diagrama de la diapositiva: comparador inversor, con vE aplicada en v- y la tensión de referencia VCOMP en v+; forma de onda de vE frente al tiempo y la conmutación correspondiente (invertida respecto al caso no inversor) de vS entre VCC y VEE. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.2 Comparador con histéresis

- A.O. con R+ (realimentación positiva): saturación con histéresis (dos niveles de conmutación, "lazo" de histéresis).
  - vS ≈ VCC si V+ > V-
  - vS ≈ VEE si V- > V+
- Conmutación entre dos niveles, lo que evita las conmutaciones indeseadas por ruido del comparador sin histéresis.
- Circuitos con A.O. con R+, pilas y resistencias: comparadores con histéresis.
- Circuitos con A.O. con R+, pilas, resistencias y condensadores: generadores de forma de onda.

## Referencias

Material de estudio:

- Malik, capítulo 2, secciones: de 2.2 a 2.3.4; de 2.5.1 a 2.5.10; y 2.6.
- Sedra-Smith, capítulo 2, secciones: de 2.1 a 2.6; y 2.9.
- Hambley, capítulo 2.
- En todos los casos: excluidas las dependencias internas con la frecuencia y el trabajo en "gran señal".
- Gráficas extraídas de los textos y secciones detallados.

## 3. Configuraciones básicas del AO en No Zona Lineal (continuación)

### 3.2 Comparador con histéresis: no inversor

- Comparador con histéresis no inversor.
- A.O. con R+.
  - vS ≈ VCC si vE > VH2 (conmuta a nivel alto)
  - vS ≈ VEE si vE < VH1 (conmuta a nivel bajo)
- Los umbrales de conmutación (VH1, VH2, "Hallo") dependen de vS a través de la realimentación positiva formada por dos resistencias, y se obtienen igualando la tensión del nudo v+ con 0V.
- Patrón estándar de este tipo de comparador con histéresis (divisor resistivo R1/R2 en la realimentación positiva desde vS): VH = ±Vsat·R1/(R1+R2), siendo Vsat la tensión de saturación de salida (VCC o VEE). La diapositiva no permite confirmar con certeza la asignación exacta de subíndices R1/R2 debido al deterioro de la tabla OCR.

*Diagrama de la diapositiva: comparador con histéresis no inversor, con vE en v+ y la realimentación positiva (divisor R1-R2) desde vS también en v+; forma de onda de vE y la conmutación de vS entre VCC y VEE en los umbrales VH1 y VH2. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.2 Comparador con histéresis no inversor: desplazamiento del centro de la zona de histéresis

- Variante del comparador con histéresis no inversor en la que se añade una tensión de referencia adicional (VP) que desplaza el centro de la ventana de histéresis respecto a 0V.
- La realimentación positiva (R+) sigue eliminando las conmutaciones indeseadas (rebotes) ante una señal de entrada con ruido.
- Los umbrales de conmutación (VH1, VH2) dependen ahora tanto de vS como de VP, siguiendo el mismo principio de divisor resistivo (R1, R2), pero centrado en torno a VP en lugar de en torno a 0V.

*Diagrama de la diapositiva: comparador con histéresis no inversor con una tensión de referencia adicional VP que desplaza el centro de la ventana de histéresis; forma de onda de vE con ruido y la salida vS conmutando limpiamente entre VCC y VEE gracias a la realimentación positiva. El layout exacto no se pudo recuperar de la extracción OCR.*

### 3.2 Comparador con histéresis: inversor

- Comparador con histéresis inversor.
- A.O. con R+: saturación con histéresis.
  - vS ≈ VCC si vE < VH1
  - vS ≈ VEE si vE > VH2
- Mismo principio que el comparador con histéresis no inversor, pero con la entrada vE aplicada en v- y la realimentación positiva (divisor R1-R2 desde vS) en v+, lo que invierte el sentido de la conmutación respecto al caso no inversor.

*Diagrama de la diapositiva: comparador con histéresis inversor, con vE aplicada en v- y la realimentación positiva (divisor R1-R2 desde vS) en v+. El layout exacto no se pudo recuperar de la extracción OCR.*
