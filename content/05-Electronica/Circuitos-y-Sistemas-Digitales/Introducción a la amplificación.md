---
title: "Introducción a la amplificación"
---

# Fundamentos de Electrónica - Tema 1: Introducción
## Índice
1. Introducción
2. Principios de modelado
3. Amplificación
4. Amplificadores ideales
5. Amplificadores multietapa
6. Amplificadores reales: efectos de carga
7. Respuesta frecuencial
## 1. Introducción
### Sistemas Electrónicos ( SSEE) en la sociedad moderna
Los sistemas electrónicos están imbricados en nuestra actividad diaria de forma más o menos visible:
- Televisión y radio, teléfonos móviles, electrodomésticos, computadores, automóviles, entretenimiento
- Servicios de comunicaciones ( públicos y privados), satélites GPS, redes de comunicaciones
La función principal de los SSEE es extraer, almacenar, transportar o procesar la información de una señal.
Otros SSEE se centran en proporcionar, mantener o controlar la energía suministrada a otros elementos:
- Altavoces, motores eléctricos, fuentes de alimentación, generadores y distribución eléctrica
### Tecnología básica común
Todos los sistemas comparten una tecnología básica común:
- Procesan la información contenida en las señales eléctricas: tensión, corriente, potencia = f ( tiempo)
- Señales que pueden ser tanto analógicas como digitales
- Utilizan dispositivos electrónicos para realizar tales funciones
- Unos pocos elementos básicos: diodos, transistores, resistores, baterías
- Realizan todas las funciones necesarias
### Del conjunto al bloque
Un ejemplo es el esquema de bloques de un receptor de radio. Cada bloque realiza una función muy concreta en el receptor. En el esquema hay bloques que procesan señales de diversa naturaleza: señales digitales, señales analógicas, e incluso ambas a la vez.
## 2. Repaso: Análisis de circuitos
### Conocimientos previos necesarios
- Circuitos en DC y AC: tensiones, corrientes y potencias
- Teoremas: Thévenin, Norton y superposición
- Estructuras repetidas en circuitos
#### Divisor de tensión
v_T = v_1 × R_2 / ( R_1 + R_2)
#### Divisor de corriente
i_1 = i_T × R_2 / ( R_1 + R_2)
i_2 = i_T × R_1 / ( R_1 + R_2)
El análisis de amplificadores y otros circuitos electrónicos se simplifica mucho si se hace uso metódico de estas estructuras.
### Teorema de Thevenin
Se sustituye el circuito por un generador y una impedancia en serie equivalentes.
- V_TH = tensión entre terminales A-B cuando la carga está desconectada
- R_TH = resistencia equivalente vista desde A-B
### Teorema de Norton
Establece que cualquier circuito lineal se puede sustituir por una fuente equivalente de intensidad en paralelo con una impedancia equivalente.
- I_N = corriente de cortocircuito
- R_N = resistencia equivalente
### Principio de superposición
Para un sistema lineal con múltiples fuentes independientes:
1. Apagar todas las fuentes independientes excepto una. Calcular la salida ( tensión o corriente) debido a la única fuente activa.
2. Repetir el paso anterior para cada una de las fuentes independientes presentes en el circuito.
3. La contribución total viene dada por la suma algebraica de las contribuciones de cada una de las fuentes independientes.
Convenciones: Apagar fuente de tensión ≡ Cortocircuito; Apagar fuente de corriente ≡ Circuito abierto
## 2. Fundamentos: definiciones de señales
### Nomenclatura de las señales eléctricas
Tomaremos como ejemplo un amplificador de señal analógica. Diferenciamos las partes continuas y las variables:
- La fuente de energía es normalmente de corriente continua ( batería)
- La información reside en las variaciones de la señal ( variable con t)
En un amplificador:
- Generador: fuente de información ( variable con t)
- Carga ( Load): objetivo de la señal amplificada
- Batería: fuente de energía ( continua)
Tensiones y corrientes por la carga:
- v_L ( t) = tensión
- i_L ( t) = corriente
### Definición de variables
v_L ( t) = V_L + v_l ( t) = continua + info f ( t)
i_L ( t) = I_L + i_l ( t) = continua + info f ( t)
Nota importante: mucho ojo al uso de mayúsculas, minúsculas y subíndices. En posteriores lecciones veremos cómo manejar adecuadamente todos estos conceptos, según el tipo de circuito y/o de señales implicados.
## 2. Modelado: dipolos
### Concepto de modelo
Descripción matemática del comportamiento de un dispositivo o circuito en el rango o margen de actuación especificado. Los modelos eléctricos más simples establecen las relaciones de corriente-tensión entre sus extremos o conexiones. Si estas relaciones se muestran de forma gráfica, se conocen como curvas ( v-i).
### Para un dipolo:
- Relaciones básicas: v = Z·i o i = v/Z
- Se pueden dar varios casos:
 - v = K₁·i
 - i = K₂·v
 - v = f ( i)
### Ejemplos de dipolos elementales:
- *Resistor**: v = i·R
- *Generador de tensión ideal**: i = f ( v_S)
- *Generador de corriente ideal**: v = f ( i_S)
## 2. Modelado: cuadripolos
### Definición
Cuadripolo: tienen cuatro terminales ( o polos). Dos terminales de entrada y dos de salida ( puertos).
Una red lineal ( R, L, C + generadores) tiene cuatro variables eléctricas por conocer: v₁, i₁, v₂, i₂. La estructura interna del cuadripolo define relaciones entre ellas.
Todas las variables quedan fijadas una vez se conocen el generador y la carga.
### Modelos básicos de cuadripolos:
**Modelo "h" ( híbrido, Serie-paralelo):**
- v₁ = h₁₁·i₁ + h₁₂·v₂
- i₂ = h₂₁·i₁ + h₂₂·v₂
**Modelo "z" ( solo serie):**
- v₁ = z₁₁·i₁ + z₁₂·i₂
- v₂ = z₂₁·i₁ + z₂₂·i₂
**Modelo "g" ( híbrido, Paralelo-serie):**
- i₁ = g₁₁·v₁ + g₁₂·i₂
- v₂ = g₂₁·v₁ + g₂₂·i₂
**Modelo "y" ( solo paralelo):**
- i₁ = y₁₁·v₁ + y₁₂·v₂
- i₂ = y₂₁·v₁ + y₂₂·v₂
### Interpretación de parámetros
**Parámetros con subíndices iguales:** impedancias terminales
- X₁₁: impedancia ( admitancia) de entrada
- X₂₂: impedancia ( admitancia) de salida
**Parámetros con subíndices diferentes:** de transferencia de señal
- X₁₂: transferencia inversa ( señal en entrada debida a salida)
- X₂₁: transferencia directa ( señal en salida debida a entrada)
### Modelos ideales de cuadripolos:
**Modelo "h": CCCS ( Current Controlled Current Source)**
- h₂₁ = trans-corriente ( A/A)
- Ecuaciones ideales: i₁ = 0; i₂ = h₂₁·i₁
**Modelo "y": VCCS ( Voltage Controlled Current Source)**
- y₂₁ = transconductancia ( 1/Ω)
- Ecuaciones ideales: v₁ = 0; i₂ = y₂₁·v₁
**Modelo "g": VCVS ( Voltage Controlled Voltage Source)**
- g₂₁ = trans-tensión ( V/V)
- Ecuaciones ideales: i₁ = 0; v₂ = g₂₁·v₁
**Modelo "z": CCVS ( Current Controlled Voltage Source)**
- z₂₁ = transresistencia (Ω)
- Ecuaciones ideales: i₁ = 0; v₂ = z₂₁·i₁
## 2. Modelado: amplificadores y cuadripolos
### El amplificador como cuadripolo
- Entrada: generador de señal ( fuente)
- Salida: carga ( destino)
- En muchos casos, hay un terminal común a entrada y salida ( masa)
- El efecto de la alimentación ( batería) se estudiará en su momento
Son muy útiles las relaciones gráficas ( curvas v-i):
- Curvas de entrada: relacionan corriente y tensión en entrada ( v₁, i₁)
- Curvas de salida: relacionan corriente y tensión en salida ( v₂, i₂)
- Función de transferencia: muestra cómo se relacionan las variables de salida con las de entrada
## 3.1. Amplificación: generalidades
### Definición
Un amplificador es un circuito electrónico cuya función es proporcionar en su salida una copia de la señal de entrada en las condiciones de nivel y calidad requeridas.
Normalmente se especifica el nivel necesario de un parámetro eléctrico: tensión, corriente o potencia. Los parámetros necesarios dependen de la aplicación.
Ejemplo: para escuchar una TV a volumen normal se necesita alrededor de 1 W en el altavoz ( una carga R_L de unos 8 Ω). Pero en una actuación en público, los amplificadores rondan los kW.
### Ejemplo de aplicación
Se dispone de un lector de cintas de música ( fuente) que da una tensión en circuito abierto de 100 mV rms y tiene una impedancia interna de 22 kΩ. Para poder oír la señal en el altavoz ( carga) que es de 8 Ω, se necesitan unos 100 mW.
**¿Se podría oír música conectando la fuente de tensión y carga directamente?**
Solución: Conexión directa:
P = V²/( R_ef·( R_ef + R_L)) = V²_m/( R_ef·R_L)
P ≈ 0,165 nW
Evidentemente necesitaremos un amplificador que nos permita llegar a la potencia requerida. Para transferir la señal de fuente a carga con el nivel de potencia requerido:
P_m = 100 mW
V_ef = 894 mV
A_v = 8,9
v_L ( t) = 8,9·v_s ( t)
### Fuente de energía en el amplificador
En el ejemplo anterior, la carga recibe 100 mW pero el generador no entrega potencia alguna ( P_s = 0 W), pues i_s = 0.
Si el generador dependiente es pasivo, surge la pregunta: ¿de dónde sale la potencia que recibe la carga?
La respuesta es clara: de la fuente de energía ( batería, fuente de alimentación).
El modelo del amplificador recoge el modo en el que la señal se transfiere de entrada a salida. La fuente de energía está implícita en el modelo a través de la constante del generador dependiente. Los terminales de alimentación de energía son diferentes a los de entrada y salida de señal.
Energía y señal están relacionadas entre sí, se tratan por separado, pero sin energía no hay señal.
### Modelo básico de un amplificador lineal
Se define como un cuadripolo Q con parámetros adecuados para las componentes de señal variable.
El amplificador básico tiene solo tres parámetros:
- Las dos impedancias terminales ( parámetros 11 y 22): Z_e y Z_s
- El parámetro de transferencia directa ( transmitancia, 21): A_x
Con solo tres parámetros las ecuaciones se simplifican mucho:
Y = A_x·X
El tipo ( modelo) de A_x define el tipo de amplificador A_x.
## 3.2. Tipos de amplificadores
### Clasificación según entradas y salidas
Según el tipo de generador y de carga se tienen las variables entrada/salida más adecuadas:
**Generadores ( entradas X_e):**
- De tensión ( v_e), como micrófonos
- De corriente ( i_e), como fotodetectores
**Cargas ( salidas X_s):**
- Que necesitan tensión ( v_s), como altavoces
- Que necesitan corriente ( i_s), como dispositivos bobinados
En consecuencia, se tienen cuatro combinaciones posibles de entradas-salidas, X_s y X_e, preferidas según la aplicación dada. Cada combinación define un tipo de amplificador A_x.
Comenzaremos el estudio de cada tipo con el A_v de tensión.
### 3.2.1. Amplificador de tensión
**Características:**
- Las variables preferentes en entrada y salida son tensiones
- El generador de salida del amplificador tiene un VCVS
- Las medidas "en circuito" son sencillas de hacer
- En paralelo con los terminales: con voltímetro, osciloscopio o similar
**Ecuaciones en el amplificador:**
- v_i = R_i·i_i
- v_o = A_vo·v_i - R_o·i_o
**En generador y carga:**
- v_s = v_i + R_s·i_i
- v_o = R_L·i_o
**Ejercicio:** ¿Cómo se mediría el parámetro del VCVS? ¿Tiene relación con ello el nombre A_vo?
### 3.2.2. Otros amplificadores: de corriente
**Características:**
- Las variables preferentes en entrada y salida son corrientes
- El generador de salida del amplificador tiene un CCCS
- Las medidas "en circuito" son más complicadas ( como un amperímetro)
**Medida de la transmitancia:**
A_i = G_isc = i_o / i_e ( salida en c.c.)
En esencia, la salida de un amplificador de corriente se modela a partir de un equivalente Norton de todo el circuito. De igual manera, el amplificador de tensión es un equivalente Thévenin. Si es posible, se puede pasar de uno a otro tipo simplemente convirtiendo el generador de salida, referenciando la variable de entrada adecuada.
### 3.2.3. Amplificadores de transimpedancia y transadmitancia
**Amplificador de transimpedancia, A_z:**
- La transmitancia tiene unidades de Z ( salida v_o; entrada i_e)
- Modelo: CCVS
- R_moc = transresistencia
**Amplificador de transadmitancia, A_y:**
- La transmitancia tiene unidades de Y ( salida i_o; entrada v_e)
- Modelo: VCCS
- G_msc = transconductancia
## 3.3. Ganancias
### Definición
Es la relación existente entre las variables eléctricas consideradas en entrada y salida del amplificador. Dan una medida de la transferencia real de señal de entrada a salida. En general, pueden ser números complejos ( módulo-fase).
### Cinco definiciones básicas
| Variable salida | Variable entrada | Ganancia | Unidades | Nomenclatura |
|---|---|---|---|---|
| P_o | P_i | P_o/P_i | W/W | Ganancia de potencia |
| v_o | v_i | v_o/v_i | V/V | De ( trans)-tensión |
| i_o | i_i | i_o/i_i | A/A | De ( trans)-corriente |
| v_o | i_i | v_o/i_i | Ω | De transimpedancia |
| i_o | v_i | i_o/v_i | 1/Ω | De transadmitancia |
### 3.3.1. Ganancia de potencia
Se define como:
G_P = P_o / P_i
Donde P_o es la potencia entregada a la carga y P_i es la potencia en la entrada del amplificador.
En el amplificador de la figura:
- P_o = v_o·i_o = i_o²·R_L = v_o²/R_L
- P_i = v_i·i_i = i_i²·R_i = v_i²/R_i
G_P = ( v_o·i_o)/( v_i·i_i) = ( R_i·R_L)/( 2)·( v_o/v_i)²
Múltiples maneras para obtener el valor del parámetro deseado. Aplicables todas las técnicas y reglas del análisis de circuitos lineales.
### 3.3.2. Ganancia de potencia: el deciBelio
Es habitual manejar las ganancias en unidades logarítmicas.
Las ganancias prácticas se dan en un rango muy amplio. Muchos efectos se modelan u operan mejor con logaritmos:
- Percepción humana: octavas en música; intensidad sonora
- Los productos se transforman en sumas; las exponenciales en productos
**Definición del decibelio ( dB):**
Sobre la relación de potencias:
G_PdB = 10·log ( G_P) ( dB)
Por extensión, se puede aplicar al resto de ganancias, pero ojo con las dimensiones y los valores complejos.
Ganancias muy usadas en dB:
- G_VdB = 20·log ( G_V) ( dB)
- G_IdB = 20·log ( G_I) ( dB)
- G_ZdB = 20·log ( G_Z) ( dBΩ)
### Ejemplo: Ejercicio 1.20 ( Malik)
Halle la ganancia de tensión necesaria si un amplificador de tensión con impedancia de entrada infinita y nula en la salida se conecta a una fuente de señal de 2 miliVoltios ( rms) con resistencia interna de 200 Ω sobre una carga de 50 Ω que necesite 1/2 W de potencia.
**Solución:**
- P = 0.5 W
- V² = 2 × P × R_L = 2 × 0.5 × 50 = 50
- V_rms = 5√2 V
- A_v = V/V_g = 5√2 / 0.002 = 2500
## 4. Amplificadores ideales
### Definición
Un amplificador puede ser descrito con cualquiera de las cinco ganancias básicas G_x. El tipo de ganancia más conveniente para modelar un amplificador real viene definido frecuentemente por la aplicación.
En audio, se prefiere la ganancia de tensión, pues generador y carga se caracterizan mejor de esa manera y además es más fácil de medir.
### Características de amplificadores ideales
Sus impedancias terminales son ideales ( según el caso: cero o ∞)
- La señal entregada en la salida no depende del valor de la carga, R_L
- No extraen potencia alguna del generador de señal ( P_e = 0)
- Alguna de sus ganancias ( y siempre G_P) tiende a infinito
- Un solo amplificador ideal para cada tipo de amplificador
### Los cuatro amplificadores ideales
| X_s | X_e | Nombre | Modelo | Z_e | Z_s | Transmitancia |
|---|---|---|---|---|---|---|
| v_s | v_e | A. Tensión | VCVS | ∞ | 0 | A_v = trans-tensión ( V/V) |
| i_s | i_e | A. Corriente | CCCS | 0 | ∞ | A_i = trans-corriente ( A/A) |
| v_s | i_e | A. Transimpedancia | CCVS | 0 | 0 | r_m = transresistencia (Ω) |
| i_s | v_e | A. Transadmitancia | VCCS | ∞ | ∞ | g_m = transconductancia ( 1/Ω) |
### 4.1. Amplificador ideal de tensión ( inversor)
**Ejemplo de amplificador ideal de tensión inversor:**
**Ecuaciones:**
- v_L = v_o + 2v_i = 2v_s
- G_V = -2
La salida se puede obtener gráficamente mediante la función de transferencia.
Note que la transmitancia -2V_i es la derivada de la función de transferencia dv_o/dv_i.
**Ganancias para el A_V ideal:**
- G_P = v_L·i_L / ( v_i·i_i) = P_L / P_i
- G_P ( ideal) = 2 ( ya que P_i = 0)
**Otras ganancias:**
- G_I = i_o/i_i ( cuando i_i = 0)
- G_Z = v_o/i_i ( cuando i_i ≠ 0)
- G_Y = i_o/v_i = v_o / ( v_i × R_L) = 2/R_L
El nombre de amplificador inversor deriva del hecho de que la señal de salida está invertida respecto a la de entrada.
## 5. Amplificadores multietapa
### Concepto
Un amplificador práctico suele estar formado por varios amplificadores elementales combinados. La combinación más común es la serie o cascada. En este caso, cada amplificador elemental es una etapa.
**Ventajas de la estructura en cascada:**
- Cada etapa se analiza/diseña por separado
- Es más fácil cumplir las especificaciones globales por partes
- En la primera etapa ( etapa de entrada) se piensa en el generador
- En la última etapa ( etapa de salida) se piensa en la carga
### Ejemplo: dos amplificadores en cascada
Las ganancias de cada etapa son:
- A_v1 = v_1/v_e
- A_v2 = v_s/v_1
La ganancia total del amplificador es el producto de ambas ganancias:
A_v_total = A_v1 × A_v2 = v_s/v_e
Si operamos en dB tenemos una relación muy útil:
A_v,dB = 20·log ( A_v1·A_v2) = 20·log ( A_v1) + 20·log ( A_v2) = A_v1,dB + A_v2,dB
### Ejercicio 1.30 ( Malik)
Para el amplificador de dos etapas, calcule:
- a) La ganancia de tensión de v_i a v_L
- b) La ganancia de corriente ( i_L/i_i)
- c) La ganancia de potencia, tomando la potencia de entrada como la que se tiene en la entrada a la primera etapa
## 6. Amplificadores reales: efectos de carga
### Características
En general, un amplificador real presenta impedancias en sus terminales de entrada y salida:
- En entrada Z_e es distinta de cero o infinito
- En salida, el generador no es ideal ( Z_s distinta de cero o infinito)
Las impedancias terminales provocan una disminución de la señal que puede transferirse a la salida.
### Análisis de efectos de carga
En un amplificador real, el generador entrega tensión v_i al amplificador. La tensión en la carga viene dada por:
v_L = v_o × R_L / ( R_o + R_L)
Donde R_o es la resistencia de salida del amplificador.
De igual manera, la tensión en entrada del amplificador es:
v_i = v_s × R_i / ( R_s + R_i)
Donde R_i es la resistencia de entrada del amplificador.
Vemos diferentes términos interesantes en cada expresión:
**La ganancia salida/entrada, A_v, vale:**
A_v = ( A_vo × R_i × R_L) / (( R_s + R_i) × ( R_o + R_L))
Amplificador real de tensión ( A_v)
Si definimos otra ganancia referida al generador v_s, se tiene entonces:
G_V = A_v = ( A_vo × R_i × R_L) / (( R_s + R_i) × ( R_o + R_L))
Aparecen dos términos, en impedancias, que hacen que la nueva ganancia sea siempre inferior a la transmitancia A_vo:
- Son los factores de carga de entrada y salida
- Alejan al amplificador real de la situación ideal ( máxima ganancia)
- Pero si los factores de carga ≈1, se tiene que G_V ≈ A_vo
Un amplificador real se comportaría como ideal si los efectos de carga en entrada y salida son despreciables (≈1) con un diseño adecuado:
R_s << R_i, R_o << R_L : A_v ≈ A_vo
### Ejercicio 2.1
Sobre el amplificador de la figura adjunta:
1. Determine las ganancias de corriente y potencia
2. ¿Qué tensión habría en la carga si ésta se conectase directamente al generador?
3. Admitiendo un error de aproximación de alrededor del 10%, ¿qué valores debieran tener las impedancias terminales del amplificador ( Z_e y Z_s) para considerarle ideal?
### Ejercicio 2.2
Haga una tabla que indique qué condiciones han de cumplir las impedancias terminales ( Z_e y Z_s) de cada tipo de amplificador real para aproximarse a la situación ideal correspondiente.
## 7. Respuesta frecuencial
### Concepto
La respuesta frecuencial de un amplificador modela la dependencia con la frecuencia de sus parámetros. Todas las características varían con ω: impedancias, ganancias, etc. Afectan en módulo y fase a parámetros y señales.
### Bandas de frecuencia
Pueden reconocerse zonas o bandas de frecuencia con comportamientos similares:
- La banda de frecuencias medias es aquella en la que los parámetros pueden considerarse constantes reales
## 8. Bibliografía
Referencias del Tema 1:
- Electrónica. Allan R. Hambley. Ed. Pearson Education, Madrid 2001. ISBN: 84-205-2999-0
 - Capítulo 1, completo: páginas 2 a 56
- Circuitos Electrónicos. Análisis diseño y simulación. Norbert R. Malik. Ed. Prentice Hall, Madrid 1996. ISBN: 84-89660-03-4
 - Capítulo 1, salvo secciones 1.5.5, 1.5.4, 1.6.7 y 1.6.8
- Otros materiales de los profesores de la asignatura
