---
title: "Sistemas de percepción"
tags: [universidad, 4anyo, pyc]
date: 2026-08-12
lang: es
---
# Sistemas de Percepción
Grado en Ingeniería de Computadores - Percepción y Control. Manuel Ocaña Miguel, Ángel Llamazares.
1. Introducción a los sistemas de medida
2. Circuitos de acondicionamiento
3. Caracterización de sensores
4. Ejemplos de sensores
5. Filtrado y fusión sensorial
6. Tipos de actuadores: motores y servos
7. SAD - Conceptos generales y definiciones fundamentales
8. Parámetros característicos de un SAD
9. Configuraciones de los SAD
10. El PC en la adquisición de datos
Laboratorio ( grupo reducido): sensores y actuadores en ROS.
Participa: ¿qué es un sistema en lazo cerrado? ( enlace en BB)
### Introducción a los sistemas de medida ( I)
Definiciones:
- Sistema de medida: asignación objetiva ( independiente del observador) y empírica ( basada en la experimentación) de un número a una propiedad o cualidad de un objeto o evento.
- Objetivos de los sistemas de medida: vigilancia o seguimiento de procesos, control de un proceso, ingeniería experimental.
- Aplicación en un sistema de control: imprescindible para conseguir un sistema de control en "lazo cerrado" ( con realimentación).
### Introducción a los sistemas de medida ( II)
Diferencia entre transductor y sensor:
- Transductor: dispositivo que convierte una señal de una forma física ( mecánica, térmica, magnética, eléctrica, óptica y molecular o química) en otra señal, que se corresponde con la primera, pero de otra forma física distinta. Su función es acoplar la magnitud a medir al sistema de medida. Como el tratamiento de la señal de salida del transductor es normalmente llevado a cabo por equipos o circuitos electrónicos, los considerados comúnmente transductores son aquellos que ofrecen una señal de salida eléctrica: tensión, corriente.
- Sensor: elemento directamente en contacto con la magnitud a medir y no tiene por qué proporcionar ninguna salida eléctrica. Capta esta magnitud para posteriormente transformarla y obtener una salida eléctrica.
Ejemplo: micrófono magnético.
### Ejemplo de sistemas de percepción en un robot
Las 4 preguntas que debe responder un robot móvil son: ¿Dónde estoy? ¿Dónde tengo que ir? ¿Qué hay a mi alrededor? ¿Cómo llego?
Por percepción se entiende la función que permite al robot obtener, elaborar e interpretar la información de su entorno por medio del uso de diferentes sensores.
### Sistemas de adquisición de datos ( I)
- Controlar un proceso implica adquirir una serie de datos, analizarlos, tratarlos y almacenarlos, para lograr una presentación clara y eficaz de la evolución de dicho proceso.
- ¿Cómo son estos datos, analógicos o digitales? Generalmente analógicos.
- ¿Cómo se tratan, almacenan o analizan? Es mucho más eficaz cuando se hace digitalmente.
- ¿Qué implica? Una transformación de los datos desde el campo analógico al campo digital, sin que por ello se deban perder aspectos fundamentales para el proceso que se desea controlar.
- Este conjunto de módulos se denomina Sistema de Adquisición de Datos ( SAD). Estructura general de un SAD.
### Sistemas de adquisición de datos ( II)
Acondicionadores:
- A partir de la señal eléctrica de salida de un transductor, generan una señal apta para ser presentada, registrada o que permita un procesado posterior mediante el equipo electrónico adecuado.
- Normalmente son circuitos electrónicos que ofrecen funcionalidades de amplificación, filtrado, adaptación de impedancia, modulación/demodulación, codificación/decodificación, conversión A/D y D/A, etc.
- Pueden integrar varios de los circuitos anteriores para conseguir sus objetivos. Dada la estandarización de las salidas de los transductores y de las entradas a los equipos de procesado, estos circuitos actualmente suelen venir integrados en un único chip.
### Características básicas de los sensores ( I)
Las medidas se realizan en el mundo real con errores asociados, es decir, con incertidumbre. Es necesario caracterizarlos.
- Valores máx/mín: límites máximos y mínimos del sensor.
- Rango dinámico: indica el cociente entre los valores de entrada máximo y mínimo del sensor, normalmente se mide en decibelios ( dB). Ejemplo: medida de tensión mínima = 1 mV y máxima = 20 V : 20·log ( 20/0.001) = 86 dB.
### Características básicas de los sensores ( II)
- Resolución: mínima diferencia entre dos valores que el sensor es capaz de apreciar. "Cuánto tiene que cambiar la magnitud que está midiendo para que el sensor detecte una variación." Normalmente el límite inferior del rango dinámico coincide con la resolución. Por ejemplo, en sensores digitales coincide con la resolución del A/D: entrada ADC 0-5V con 8 bits : 5V / 256 = 19,53 mV.
- Linealidad: expresa lo constante que es la variación de la señal de salida en función de la señal de entrada. Esta linealidad es menos importante si posteriormente se trata en un PC.
- Frecuencia o ancho de banda: la velocidad con la que se entregan los datos. Normalmente hay un límite superior que depende del sensor y, en su caso, de la velocidad de muestreo. También puede existir un límite inferior, como por ejemplo en los sensores de aceleración.
### Rendimiento ( I)
Características que son especialmente relevantes en el mundo real:
- Sensibilidad: mínimo cambio que se debe producir en la entrada para provocar un cambio en la salida. En el mundo real, se suele confundir con sensibilidad indeseada o acoplamiento de otros parámetros del entorno.
- Sensibilidad cruzada: sensibilidad a otros parámetros del entorno que son ortogonales a los parámetros que mide el sensor ( por ejemplo, la brújula magnética).
- Error / exactitud: el error es la diferencia entre el valor medido por el sensor y el valor real. La exactitud es el grado de conformidad entre el valor medido y el real, y se define como exactitud = 1 - |m - r| / r, donde m es el valor medido y r el valor real. Ejemplo: temperatura real = 22 ℃, temperatura medida = 21 ℃, error = 1 ℃, exactitud = 1 - |21-22| / 22 = 0,9545.
### Rendimiento ( II)
- Precisión: a menudo se confunde con la exactitud. Indica la repetitividad en los resultados del sensor.
- Error sistemático ( errores determinísticos): causados por factores que pueden ser modelados ( en teoría), lo que implica que se puede realizar una predicción. Ejemplo: error de distorsión de un sensor láser provocado por la óptica.
- Error aleatorio ( no determinístico): no se puede realizar ninguna predicción. Se pueden describir de forma probabilística, utilizando funciones de densidad de probabilidad para caracterizarlos. Ejemplo: variaciones de pequeña escala ( movimientos por debajo de la longitud de onda) en la medida de la señal WiFi.
### Sensores de odometría
- Se utilizan para medir la posición o velocidad en motores.
- La velocidad de las ruedas se integra para obtener el avance estimado del robot: odometría.
Encoders ópticos:
- Utilizan fotointerruptores formados por un emisor-receptor junto con una rejilla asociada a la rueda o motor para llevar la cuenta de las vueltas.
- Son sensores propioceptivos. Además, la estimación de la posición está referenciada a un sistema de coordenadas local.
- Sólo son útiles en desplazamientos cortos ya que tienen errores acumulativos y problemas con deslizamientos.
- Las resoluciones típicas son del orden de 2.000 pulsos por vuelta. Para una mayor resolución: colocar varios sensores en cuadratura, o usar encoders multivuelta ( 2 encoders + reductora).
Participa: ¿dónde crees que podemos encontrar encoders? ( enlace en BB)
### Sensores de contacto
- Los sensores de contacto ( bumpers) son extereoceptivos.
- Se utilizan para detectar el impacto de un objeto con el robot.
- Utilizan la deformación mecánica que sufren determinados dispositivos para cerrar o abrir un circuito e indicar que se ha producido un impacto.
- Ejemplos de sensores de contacto: interruptores, fibras ópticas, etc.
Participa: ¿los bumpers son sensores activos o pasivos? ( enlace en BB)
### Sensores de orientación ( I)
Pueden ser:
- Propioceptivos: giróscopos.
- Extereoceptivos: compass/brújulas, inclinómetros.
Se utilizan para determinar la orientación/inclinación de los robots. Permiten integrar el movimiento para conseguir una estimación de la pose ( posición + orientación) sobre un mapa, llamado "dead reckoning". Este procedimiento se utilizaba antiguamente en navegación marítima.
### Sensores de orientación ( II)
Brújula o "compass": desde el año 2000 a.C. los chinos utilizaban una pieza de magnetita suspendida en un hilo para guiar los carros a través de la tierra. Utilizan el campo magnético de la Tierra para obtener una medida absoluta de orientación:
1. Brújulas magnéticas mecánicas.
2. Medida directa del campo magnético basados en sensores:
 3. De efecto Hall: cuando se aplica una corriente constante a lo largo de un material semiconductor, existirá una diferencia de potencial en una dirección perpendicular, a lo ancho del semiconductor, basado en la orientación relativa del semiconductor a las líneas de flujo magnético.
 4. Magneto-resistivos: aprovechan la propiedad de un material que cambia su resistencia en presencia del campo magnético.
### Sensores de orientación ( III)
Principales inconvenientes de las brújulas:
1. Debilidad del campo magnético de la Tierra.
2. Perturbaciones causadas por otros objetos o fuentes magnéticas.
3. No suelen ser útiles en entornos interiores.
### Sensores de orientación ( IV): giróscopos
Sensores de orientación que mantienen un sistema de coordenadas fijo. Proporcionan una medida absoluta de orientación del robot.
Esquemas básicos: mecánicos ( Gimbaled Gyro, MEMs) y ópticos ( Ring Laser Gyro - LRG).
Ejemplo de uso: principio de funcionamiento de los sistemas de navegación inercial ( A.D. King, "Inertial Navigation - Forty Years of Evolution").
### Medidores de distancia activos ( I)
- Sensores extereoceptivos activos ampliamente utilizados en sistemas de control ( robótica) y medida, por su bajo coste y por la facilidad de interpretación de las medidas.
- Información de distancia: clave para la localización y el modelado del entorno local o cercano.
- Los sensores de ultrasonidos y láser utilizan normalmente la velocidad de propagación de las ondas ( sonido o electromagnéticas) para conocer la distancia recorrida por la onda, dada por d = c·t, donde d es la distancia recorrida ( normalmente ida-vuelta), c la velocidad de propagación de la onda y t el tiempo de vuelo.
Participa: ¿cuál es la velocidad de propagación del sonido? ( enlace en BB)
### Medidores de distancia activos ( II)
Es importante matizar:
- Velocidad de propagación del sonido: aprox. 0.3 m/ms ( 331 m/s).
- Velocidad de propagación de señales electromagnéticas: 0.3 m/ns ( 300.000 km/s).
- Para 3 metros: son 10 ms en un sistema ultrasónico, y sólo 10 ns para un sensor láser.
- El tiempo de vuelo con señales electromagnéticas no es una tarea fácil, y los sensores láser son caros y delicados.
La calidad de estos sensores depende de:
1. Incertidumbres en el tiempo de llegada exacto de la señal reflejada ( imprecisión en la medida del tiempo de vuelo con sensores láser).
2. Apertura del ángulo transmitido ( sensores ultrasónicos).
3. Interacción con el objetivo ( múltiples superficies, reflexiones especulares).
4. Variación de la velocidad de propagación en el camino ( temperatura, humedad relativa).
5. Velocidad relativa del medidor y el objetivo.
### Sensores de ultrasonidos ( I)
- Emiten un paquete de ondas de presión ultrasónicas (>20 KHz), normalmente a unos 40 KHz.
- La distancia d al objeto que devuelve el eco se puede calcular en base a la velocidad de propagación del sonido c y el tiempo de vuelo t: d = c·t / 2.
- La velocidad del sonido en el aire depende de la temperatura ambiente: c = c₀·( 1 + ( Ta - 273.15)/273.15) [m/s], donde c₀ es la velocidad de los ultrasonidos a 273.15 K ( 331.45 m/s) y Ta la temperatura ambiente en Kelvin. A 20 ºC, c = 343 m/s.
### Sensores de ultrasonidos ( II)
Señales en un sensor ultrasónico: paquete de ondas del ultrasonido transmitido, señal de eco analógico con un umbral, señal de eco digital, señal integrada por el integrador ( tiempo de vuelo como señal de salida), tiempo integrado, señal de salida y blanking time.
### Sensores de ultrasonidos ( III)
- Frecuencia típica de trabajo: 40-180 KHz.
- Generación de la onda de ultrasonidos: transductores piezoeléctricos. El transmisor y receptor pueden estar separados o pueden ser el mismo transductor.
- El haz de sonido se propaga en forma de cono, con ángulos de apertura de entre 20 y 40 grados, dando lugar a regiones de profundidad constante ( segmentos de un arco de circunferencia, o esfera en 3D, con distancia equivalente).
### Sensores de ultrasonidos ( IV)
Problemas de los sensores de ultrasonidos:
- Falsa detección por emisión simultánea ( posible solución con códigos ortogonales, por ejemplo los códigos Golay).
- Superficies porosas ( absorben energía).
- Superficies que no están en dirección perpendicular a la dirección del sonido, provocando reflexión especular.
Exactitud: 98-99.1%. Rango: 12 cm - 5 m.
### Sensores láser
- Los haces transmitido y reflejado son coaxiales. El transmisor ilumina el objetivo con un haz muy direccional.
Técnicas de medida de distancia con láser:
1. Láser pulsado: medir el tiempo de vuelo directamente ( resultados en picosegundos).
2. Medir la interferencia entre la frecuencia continua modulada de la onda y la señal reflejada ( interferometría).
3. Triangulación en base a relaciones geométricas conocidas.
4. Medir la diferencia de fase. La más fácil de implementar.
### Sensores láser basados en diferencia de fase ( I)
Medida de diferencia de fase: λ = c/f, D' = L + 2D = L + λ·θ/2π, donde:
- λ es la longitud de onda.
- c es la velocidad de la luz.
- f es la frecuencia de modulación.
- D' es la distancia recorrida en ida-vuelta.
- D es la distancia al objetivo.
- θ es la diferencia de fase entre la transmitida y la reflejada ( radianes).
Ejemplo: para f = 5 MHz ( sensor A.T.&T.), λ = 60 metros.
### Sensores láser basados en diferencia de fase ( II)
Distancia D, entre el separador del haz y el objetivo: D = λ·θ / 4π.
Ambigüedad: en el ejemplo existiría para distancias separadas λ/2 = 30 m, el objetivo podría estar en 5 m, 35 m, 65 m, etc.
### Sensores láser 2D y 3D
- Si se desea realizar medidas en 2D y 3D: barridos mediante espejos motorizados en 2D ( ejemplo: SICK), o barridos en 3D ( ejemplo: Velodyne, Ouster...).
- La longitud de las líneas indica la incertidumbre de la medida, que es inversamente proporcional al cuadrado de la amplitud de la señal recibida.
### Sensores de distancia basados en triangulación ( I)
- Utilizan las propiedades geométricas de la imagen para establecer la medida de distancia.
- Por ejemplo, si se proyecta un patrón de luz perfectamente conocido ( como un punto, una línea, etc.) sobre el entorno, la luz reflejada podrá ser capturada por un sensor en forma de línea fotosensible o bien una matriz ( cámara), y se puede utilizar una triangulación sencilla para conocer la distancia.
- Si se conocen las dimensiones de un objeto en particular, se pueden establecer las relaciones geométricas entre el objeto y su imagen proyectada para conocer la distancia.
### Sensores de distancia basados en triangulación ( II)
Principio de triangulación láser 1D: la distancia es proporcional a 1/x.
### Sensores de distancia basados en triangulación ( III)
Relación geométrica: H = D·tan (α).
Luz estructurada ( visión 2D-3D): elimina el problema de correspondencia proyectando una luz estructurada sobre la escena. Se emite luz direccional ( láser) con un espejo rotativo, y se utilizan relaciones geométricas entre la imagen formada en la cámara y los ángulos del emisor-cámara con respecto a la escena.
### Sensores de visión ( I)
- La visión humana es uno de los sentidos más potentes.
- Sensor extereoceptivo que proporciona una gran cantidad de información sobre el entorno y los cambios que ocurren en él.
- Tipos: sensores CCD ( Charged Coupled Device) y sensores CMOS ( Complementary Metal Oxide Semiconductor). Ejemplos: matriz CCD 2048x2048, Sony DFW-X700, Orangemicro iBOT Firewire, Canon IXUS 300.
### Sensores de visión ( II)
Características:
- Resolución espacial: determina el número de píxeles de la imagen.
- Cuantificación: niveles de intensidad que se utilizan para representar el valor de un píxel.
### Sensores de visión ( III)
Características ( cont.):
- Tamaño, peso, consumo, etc.
- Frecuencia de adquisición: se mide en imágenes o frames por segundo (>30 fps).
- Blanco y negro o color. En imagen B/N, I ( u,v) es la intensidad del píxel de coordenadas ( u,v). En imagen color, I ( u,v) es la intensidad del píxel de coordenadas ( u,v) por cada capa de color ( R, G, B).
- Óptica: normal ( 40-50 mm), gran angular (<35 mm, útil en robótica), teleobjetivo (>70 mm), zoom ( distancia focal variable).
- Longitudes de onda detectadas: visible, infrarrojo.
- Cámaras fijas o con posibilidad de movimiento Pan-Tilt / PTZ.
- Estándar de salida: PAL, NTSC.
Participa: ¿por qué crees que debe ser la frecuencia de adquisición de una cámara > 30 fps? ( enlace en BB)
### Sensores de visión ( IV): vídeo cámara pin-hole
Modelo de cámara pin-hole: la imagen es invertida, el tamaño se reduce y se pierde la información de la profundidad ( Z).
Siendo O el sistema de referencia de la cámara y f la distancia focal, las coordenadas de un punto 3D ( x, y, z) referenciadas desde la cámara se proyectan como:
- x = f·X/Z
- y = f·Y/Z
- z = f
Donde ( u, v) son las coordenadas en píxeles del punto 3D proyectado en el plano imagen, ( u₀, v₀) representan las coordenadas en píxeles de la intersección del eje óptico y el plano imagen, y ( dx, dy) son las dimensiones en mm, en los ejes x e y respectivamente, de un píxel elemental de la matriz CCD de la cámara ( mm/píxel):
- u = x/dx + u₀
- v = y/dy + v₀
### Sensores de visión ( V): modelo de cámara estéreo
d = xr - xl es la denominada disparidad, que mide la diferencia en el eje x del plano imagen de los puntos correspondientes a las cámaras derecha e izquierda.
Problemas con la alineación: geometría epipolar ( plano epipolar OO'X, líneas epipolares).
### Sensores de visión ( VI): procesado de imágenes
- Transformaciones geométricas, histogramas, realce, suavizado...
- Segmentación: consiste en localizar los diferentes objetos que están presentes en una imagen.
- Detección de bordes: fijar la atención en una zona de la imagen.
- Clasificación: de los elementos detectados en base a unas características comunes ( redes neuronales, Support Vector Machine - SVM, CNN).
Participa: ¿qué problemas crees que tienen los sensores de visión? ( enlace en BB)
### Sensores de visión ( VII): problemas de los sensores basados en visión
- Oclusión: pérdida de visibilidad del objeto por una o varias cámaras.
- Coste computacional: procesamiento elevado ( ej. 640 x 480 x 3 = 921 Kbytes).
- Estéreo: zona muerta, correspondencia de puntos.
- Distorsiones: deformación de la imagen por perspectiva o por lente ( barril, cojín, ojo de pez).
### Balizas de referencia
- Son sensores extereoceptivos y activos.
- Es una forma típica de resolver problemas de localización.
- Se utilizan como una referencia conocida para estimar la posición del robot.
- Navegación basada en balizas es clásica desde que los humanos comenzaron a viajar: balizas/marcas naturales tales como las estrellas, montañas, sol, etc.; balizas artificiales como los faros.
- Exteriores: Sistema de Posicionamiento Global ( GPS), triangulación/trilateración con señales de RF.
- Interiores: balizas infrarrojos/ultrasonidos, WiFi, RF.
- Objetivos: evitar modificar el entorno con las balizas ( reducir costes) y flexibilidad/adaptación a los cambios en el entorno.
### Balizas exteriores ( I): GPS
- Desarrollado para uso militar, posteriormente accesible para aplicaciones comerciales.
- 24 satélites ( incluyendo tres recambios) orbitan alrededor de la Tierra cada 12 horas a una altura de 20.190 km.
- Cada satélite emite continuamente su posición y hora actual.
- Los receptores de GPS son pasivos y extereoceptivos.
- La localización del receptor GPS se realiza mediante el cálculo del tiempo de vuelo desde los diferentes satélites hasta el receptor.
- Desafíos técnicos: sincronización del tiempo entre los satélites y el receptor GPS, actualización en tiempo real de la posición exacta de los satélites, medida precisa del tiempo de vuelo, visión directa de los satélites ( ciudades, bosques, etc.).
### Balizas exteriores ( III): principio de trilateración
La medida de la distancia d1 al satélite 1 y la distancia d2 al satélite 2 proporciona la intersección de las dos esferas ( una circunferencia). La medida de la distancia d3 al satélite 3 puede proporcionar hasta 2 puntos de corte con la circunferencia obtenida anteriormente. Con la medida de la distancia d4 al satélite 4 se obtiene un único punto de corte, que corresponderá con la posición estimada del robot.
En general: du = √[( x - xAPu)² + ( y - yAPu)² + ( z - zAPu)²], para u ∈ [1,...,4].
### Balizas exteriores ( IV): estrategias de mejora del GPS
- DGPS o GPS diferencial: se utiliza una estación base de posición geográfica perfectamente conocida; esta estación realiza correcciones sobre las medidas que recibe de los diferentes satélites y las envía a los receptores que tiene en sus cercanías ( GSM, RDS, RF, etc.).
- GPS cinemático: medida de la fase de las dos portadoras ( L1, L2) en todas las señales recibidas desde los diferentes satélites en lugar de utilizar el mensaje contenido en ellas. Utiliza también una estación base para sincronizar las portadoras que se obtienen en cada uno de los receptores.
Errores típicos: GPS comercial ~15 m, DGPS ~1 m, GPS cinemático ~1 cm.
Frecuencia/ancho de banda: comerciales 1 Hz, cinemáticos 5 Hz.
### Balizas interiores ( I): sistemas de localización con RF ( WiFi)
- La señal GPS es muy débil, no se puede medir en interiores.
- Alternativas: ultrasonidos, láser, RF ( WiFi, Bluetooth, Ultra Wide Band UWB, etc.).
- Principal aplicación WiFi: WLAN ( Wireless Local Area Network), en modos Ad-Hoc "punto-punto" o Managed "administrado".
- Características: IEEE 802.11a/b/g/ac/n…, 2.4 GHz ( b/g) y 5 GHz ( a), espectro ensanchado, velocidad 54 Mbps/100 Mbps/1000 Mbps.
### Balizas interiores ( II)
- Se suele emplear la medida del nivel de señal recibido ( RSSI).
- Técnicas aplicadas a la localización: distancia a partir de modelo de propagación ( trilateración, como en GPS), o comparación con un mapa a priori ( fingerprint), calculado con un modelo o mediante una fase de entrenamiento ( manual o automática).
- Ventajas: no se necesita modificar el entorno, frecuencia de banda libre, coste muy bajo ( interfaz de comunicaciones).
- Inconvenientes: frecuencia de trabajo de 2.4 GHz ( resonancia del agua), frecuencia de banda libre, multicamino ( reflexión, refracción, difracción) en interiores.
### Balizas interiores ( III)
Modelo de nivel de señal recibido dependiente de la distancia: RSL = TSL + Gap_tx + Grx + 20·log (λ) - 20·log ( 4π) - 10·n·log ( d) - Xσ, para cada punto de acceso u ∈ U.
### Balizas interiores ( IV): dos fases del sistema de localización
1. Obtención del mapa: calculado mediante modelo de propagación ( facilidad de implantación, valor medio esperado, mayor error) o mediante entrenamiento/calibración del sistema ( calibración, histogramas, error menor).
2. Localización: a partir de la medida de la señal WiFi y el mapa a priori se obtiene la posición estimada.
Ejemplo con tres puntos de acceso ( AP1, AP2, AP3): patrones de posición y correlación cruzada de histogramas para estimar la posición mediante el valor de correlación máximo.
Participa: ¿cómo podemos solucionar los problemas en las medidas de los sensores? ( enlace en BB)
### Introducción
- En la mayoría de los casos resulta insuficiente la información proporcionada por un único sensor.
- La información puede estar contaminada con ruido o incluso puede llegar a desaparecer ( oclusiones en visión, falta de visibilidad de satélites GPS, etc.).
- Utilizar la información de diferentes sensores puede ayudar a garantizar la correcta estimación del robot dentro del entorno o bien la dinámica del mismo.
- Problemas: diferente exactitud/precisión/información/ruido de los diferentes sensores, y decidir la estrategia y algoritmo más conveniente para cada caso.
### Filtrado: ejemplo de algoritmos
- Filtro valor medio.
- Filtro mediana.
- Filtro ventana.
Comparativa: ( a) perfil bruto ( raw profile), ( b) filtro gaussiano, ( c) filtro mediana, ( d) procedimiento de corrección de outliers.
Smooth: regresión lineal ponderada localmente para suavizar datos.
### Fusión: ejemplo de estrategias y algoritmos
Estrategias: ejemplo de fusión sensorial entre odometría y GPS en un robot.
1. Odometría como estimador de la posición hasta que la distancia recorrida sea superior a un umbral ( por ejemplo 10 m) y entonces acudir a la estimación que proporciona el GPS. Desventaja: en ausencia de señal GPS en el momento de la corrección, el robot se ve obligado a navegar con la estimación de la posición dada por el odómetro, afectada por un error alto.
2. GPS como estimador de posición y, cuando no se reciba señal, acudir a la estimación del odómetro. Desventaja: la estimación en recorridos largos no es fiable debido a su elevada imprecisión.
3. GPS para mejorar continuamente la estimación proporcionada por el odómetro. Ventaja: si desaparece la señal del GPS durante un periodo de tiempo, la estimación del odómetro será fiable por haberse corregido en cada iteración con las estimaciones previas del GPS. Desventaja: sólo si la señal GPS desaparece durante largos periodos de tiempo, y aún en este caso una reducción drástica en la velocidad del robot paliaría el problema de la localización.
Algoritmos de fusión: filtros de Kalman, filtros de partículas, algoritmos basados en comportamientos, técnicas basadas en lógica borrosa, redes neuronales, etc.
Participa: escribe algún ejemplo de actuador ( enlace en BB)
### Actuadores
Convierten las órdenes del sistema de control en acciones físicas ( movimientos). Permiten:
- Locomoción ( desplazamiento).
- Manipulación ( manejo de objetos).
El actuador se refiere al elemento que genera movimiento, no a la parte mecánica. Ejemplo: el actuador es el motor, no la rueda que mueve.
Tipos de actuadores más utilizados en robótica: neumáticos e hidráulicos ( más usados en aplicaciones industriales) y eléctricos ( más usados en robótica móvil).
### Tipos de actuadores ( I): neumáticos
Aire a presión ( 5-10 bares). El flujo mueve pistones en cilindro.
Ventajas: relativamente baratos, trabajan a alta velocidad, son seguros y robustos, muy usados en aplicaciones industriales para robots de tamaño medio ( manipuladores).
Inconvenientes: poca exactitud en la posición final, difíciles de controlar ( el aire es demasiado compresible, presión del compresor inexacta), se pueden producir pérdidas de aire, requieren sistemas de limpieza y filtrado adicionales.
### Tipos de actuadores ( II): hidráulicos
Aceite mineral a 50-100 bares.
Ventajas: fuerzas y pares elevados, grandes cargas, control muy preciso y continuo ( por la incompresibilidad del aceite), amplio rango de velocidades, estabilidad en estático, seguro en entornos inflamables o explosivos, movimientos suaves a bajas velocidades.
Inconvenientes: son caros, se pueden producir fugas, difícil mantenimiento, ocupan mucho espacio.
### Tipos de actuadores ( III): eléctricos
Los más utilizados en robótica móvil, tanto para ruedas como para articulaciones.
- Motores DC: estator ( imanes) y rotor; la velocidad de giro es proporcional a la tensión aplicada; a más corriente, más par; eficientes para girar con poca fuerza y gran velocidad. Sistemas digitales lo modulan con PWM.
- Motores paso a paso: se controlan digitalmente mediante pulsos ( códigos digitales) y, a bajas velocidades, no requieren realimentación; capaces de colocarse en una posición y mantenerla; los más precisos; menores cargas que los motores DC. Se controlan mediante pulsos modulados en anchura ( 3 hilos: Vcc, tierra y PWM).
- Servomotores: motor DC + engranajes + sensor de posición + control proporcional.
### Elementos asociados: transmisiones y reductoras
- Transmiten el movimiento del actuador al elemento que mueve ( ej.: del motor a la rueda).
- Muchos tipos: engranajes, cigüeñales, poleas, levas, manivelas, cadenas, diferenciales, etc.
- Los más utilizados en robótica son los engranajes. Tipos:
 1. Ruedas dentadas ( reductoras): aumentan potencia ( par), reducen velocidad. Los motores suelen dar altas velocidades y bajo par.
 2. Engranaje en escuadras ( cónicos): cambio de dirección.
 3. Cremalleras y piñones: cambio de movimiento angular a lineal.
### Tipos de señales
Clasificación de señales:
- En función del tiempo: continuas ( definidas para cualquier instante de tiempo) y discretas ( definidas en ciertos instantes de tiempo).
- En función de su valor de amplitud: analógicas ( pueden tomar infinitos valores dentro de un determinado intervalo) y digitales ( toman solo unos determinados valores dentro del intervalo).
Se distinguen así cuatro combinaciones: analógica continua, digital continua, analógica discreta y digital discreta.
### Sistemas de adquisición de datos ( I)
- Sensores o transductores: convierten la variable física a medir ( temperatura, humedad, presión, etc.) en señal eléctrica. Esta señal eléctrica suele ser de muy bajo nivel, por lo que generalmente se requiere un acondicionamiento previo, consiguiendo así niveles de tensión/corriente adecuados para el resto de los módulos del SAD.
- Multiplexor ( MUX): selecciona la señal de entrada que va a ser tratada en cada momento. Necesario sólo si se trabaja con más de un sensor de entrada.
### Sistemas de adquisición de datos ( II)
- Amplificador de instrumentación ( AI): amplifica la señal de entrada del SAD para que su margen dinámico se aproxime lo máximo posible al margen dinámico del conversor A/D ( ADC), buscando la máxima resolución. En SAD con varios canales de entrada, cada canal tendrá un rango de entrada distinto, por lo que el amplificador debe tener ganancia programable.
- Muestreo y retención ( Sample & Hold, S/H): toma la muestra del canal seleccionado ( sample) y la mantiene ( hold) durante el tiempo que dura la conversión.
- Conversor Analógico/Digital ( ADC): proporciona un código digital de salida que representa el valor de la muestra adquirida en cada momento.
Estos son módulos fundamentales en cualquier SAD y sus características pueden condicionar al resto de los módulos/circuitos del sistema.
### Sistemas de adquisición de datos ( III)
Cadena típica: entradas analógicas : multiplexor ( Mux) : amplificador de instrumentación ( AI) : muestreo/retención ( S/H) : conversor A/D ( ADC) : controlador digital : conversor D/A ( DAC) : demultiplexor ( Demux) : postprocesado : salidas analógicas reconstruidas. Ejemplo de sensor: SHARP GP2Y.
### Módulos de un SAD ( I): puertas de transmisión
- Elemento básico de los SAD. Son interruptores controlados por una señal de entrada ( Vcontrol).
- Ideal: en ON, Ron = 0 ( Ve = Vs); en OFF, Roff = ∞ ( Vs = 0).
- Real: el comportamiento varía con la frecuencia, existen tiempos de propagación, la Ron no es exactamente cero ni la Roff infinita, etc.
- Aplicaciones: multiplexores/demultiplexores analógicos, circuitos S&H, circuitos DAC, etc.
### Módulos de un SAD ( II): multiplexores y demultiplexores
Dispositivo que permite seleccionar una señal de entre varias ( Mux), o distribuir una señal a otro punto ( Demux). Se construyen utilizando puertas de transmisión y, como éstas, suelen ser dispositivos bidireccionales. Los Mux/Demux pueden funcionar normalmente como Demux/Mux, con log2 ( n) líneas de control para n canales.
Parámetros más importantes a tener en cuenta:
1. DC: Ron y corrientes de fuga en corte y conducción.
2. AC: acoplo entrada-salida de un canal en corte ( feed through), acoplo entre canales ( crosstalk), tiempo de propagación entrada-salida ( Tmux).
### Módulos de un SAD ( III): conversor ADC
Convierte una señal analógica en digital. Cadena: señal analógica xa ( t) : muestreador : señal en tiempo discreto xm ( n) : cuantificador : señal cuantificada xc ( n) : codificador : señal digital xd ( n) ( por ejemplo, 0010111001...).
Principales módulos:
- Muestreador ( S): toma el valor de la señal en un número finito de valores, normalmente equiespaciados, denominados muestras. Suele ir acompañado de un circuito de retención ( H) debido a que el ADC tarda un tiempo Tcon ( tiempo de conversión) en realizar la conversión, y durante ese tiempo es preciso que la señal de entrada no cambie.
- Cuantificador: acota los valores de la señal de entrada a un número finito de valores.
- Codificador: asigna a cada valor cuantificado un código digital.
Participa: ¿conoces el teorema de Nyquist? ( enlace en BB)
### Muestreo ( I): teorema de Nyquist
Para que las muestras de la señal sean representativas debe cumplirse el teorema de Nyquist: fs ≥ 2·fmax, donde fs es la frecuencia de muestreo y fmax la frecuencia máxima de la señal de entrada.
En ocasiones la fs supera ampliamente a la de Nyquist:
- Ventajas: disminuir el ruido efectivo introducido por el proceso de conversión; disminuir la distorsión, simplificando el filtro antialiasing y de reconstrucción; facilitar al sistema de procesamiento la extracción de parámetros de la señal analógica.
- Inconveniente: mayor coste de ciertos circuitos y exige más velocidad de recogida de datos.
### Muestreo ( II): aliasing
Efecto aliasing ( ver vídeo de referencia). Participa: ¿qué crees que está pasando en el vídeo? ( enlace en BB)
Si la frecuencia de muestreo no cumple el teorema de Nyquist, los espectros de la señal muestreada se solaparán, y será imposible recuperar la señal original. Este efecto es el aliasing ( solape): con fs > 2·fmax no hay aliasing; con f's < 2·fmax sí lo hay.
Para prevenirlo, se suele situar un filtro antialiasing a la entrada del S/H para eliminar los armónicos de la señal superiores a fs/2, asegurando que siempre se podrá recuperar la información filtrada.
### Muestreo ( III): muestreo y retención ( S&H)
Son circuitos donde la salida sigue a la entrada durante un período de tiempo llamado tiempo de adquisición o muestreo ( Sample). Una vez adquirida, la salida se mantendrá constante al valor adquirido en la fase de muestreo; este tiempo se conoce como tiempo de retención ( Hold).
La señal de control Vs/h fija los tiempos de muestreo y retención:
- Tadq_s: tiempo de adquisición en modo Sample.
- Tap: tiempo de apertura.
- Test_h: tiempo de establecimiento en modo Hold.
### Muestreo ( IV): muestreo y retención ( S&H)
- La señal muestreada debe ser retenida antes de introducirla al ADC, debido a que este tarda un tiempo Tcon en realizar la conversión y durante ese tiempo es preciso que la señal de entrada no varíe.
- Si la señal de entrada es continua o de frecuencia muy baja no sería necesario un S&H. Hay ADCs que incluyen internamente el S&H.
- La frecuencia máxima de muestreo está limitada por el tiempo de adquisición de datos ( Tadq_s), el tiempo de apertura ( Tap) del S/H, el tiempo de establecimiento en modo Hold ( Test_h) y el tiempo de conversión ( Tcon) del conversor ADC:
fmuestreo ( máxima) = 1 / ( Tadq_s + Tap + Test_h + Tcon)
### Cuantificador ( I)
Cuantificación: proceso por medio del cual se transforma una señal de entrada con infinitos valores de amplitud en una señal con un número finito de valores N, siendo N = 2ⁿ ( n = número de bits del conversor ADC).
Escalón de cuantificación "q" ( diferencia entre las magnitudes de dos valores digitales consecutivos): q = MDE/N = ( Vemax - Vemin) / 2ⁿ = LSB, donde MDE es el margen dinámico de entrada, Vemax y Vemin son los valores máximo y mínimo de la señal de entrada, y LSB es el bit menos significativo ( Least Significative Bit).
Si Vemax y Vemin tienen el mismo signo, el cuantificador es unipolar. Si tienen distinto signo, es bipolar.
### Cuantificador ( II): errores
El error de cuantificación depende del método de conversión elegido:
- Por redondeo, el error máximo es de q/2.
- Por truncamiento, el error máximo es de q.
- En ambos casos el error medio es q/2.
Relación entrada-salida: por redondeo, si -q/2 < Ve < q/2 entonces Vs = 0 ( y así sucesivamente en escalones de q). Por truncamiento, si nq < Ve < ( n+1)q entonces Vs = nq.
### Cuantificador ( III): margen dinámico
- Es necesario ajustar el margen de la señal de entrada al margen del conversor ADC. Esto se consigue normalmente con el AI ( amplificador de instrumentación).
- Si la señal de entrada no cubre el rango del cuantificador, la relación S/N disminuye y se desperdician bits del cuantificador.
### Codificador: códigos unipolares y bipolares
Codificación: proceso de conversión de la señal digital en un código numérico con el que pueda trabajar el sistema de procesamiento digital.
En función de los valores a codificar:
- Unipolar ( Vemax y Vemin del mismo signo): se utiliza binario natural o BCD ( Código Decimal Binario).
- Bipolar ( Vemax y Vemin de distinto signo): se utiliza C2 ( complemento a 2) o binario desplazado.
Tabla de niveles ( q = escalón de cuantificación) con sus códigos C2, binario desplazado y binario natural: 3q : C2 011, desplazado 111, natural 011 ( BCD 0011); 2q : C2 010, desplazado 110, natural 010 ( BCD 0010); q : C2 001, desplazado 101, natural 001 ( BCD 0001); 0q : C2 000, desplazado 100, natural 000 ( BCD 0000); -q : C2 111, desplazado 011; -2q : C2 110, desplazado 010; -3q : C2 101, desplazado 001; -4q : C2 100, desplazado 000.
- C2 ( complemento a 2): para los números negativos se niegan todos los bits ( se halla el C1) y después se suma un 1 al resultado.
- Binario desplazado: forma práctica, empieza a contar el "000" desde el número más negativo.
- BCD ( Código Decimal Binario): cada dígito decimal se representa con 4 bits ( 10 es 0001 0000).
### Tipos de ADCs
Tipos según el método de cuantificación:
1. Flash ( paralelo o simultáneo).
2. DAC-contador.
3. Aproximaciones sucesivas.
4. Integración.
5. Delta-Sigma.
Se caracterizan por el número de bits de salida, Tcon, exactitud, y si tienen S&H. Los dos parámetros más importantes para comparar los diferentes métodos de conversión ADC son resolución y velocidad. No se puede decir que un método es superior a otro: cada uno tiene un equilibrio diferente entre ambos parámetros, por lo que cada aplicación suele imponer claramente el tipo de conversor necesario.
### Conversor Digital-Analógico ( I)
- DAC: dispositivo que recibe una información digital en forma de una palabra de n bits, y la transforma en una señal analógica.
- Transformación: correspondencia entre 2ⁿ combinaciones binarias posibles en la entrada y 2ⁿ tensiones ( o corrientes) discretas obtenidas a partir de una tensión de referencia ( Vref): Salida = K · [valor decimal del código de entrada].
- La señal así obtenida no es una señal analógica continua, sino que se obtiene un número discreto de escalones/puntos a consecuencia de la discretización de la entrada, tal como puede observarse en la curva de transferencia ideal de un DAC.
- Es necesario un filtro a la salida para obtener un valor continuo y poder hablar así de una señal analógica y continua: filtro paso bajo ( elimina armónicos no deseados y obtiene una señal analógica continua, con fc ≤ fs/2) y filtro compensador ( elimina la posible distorsión de amplitud introducida por el conversor D/A).
Cadena: código binario de entrada : conversor D/A : filtro paso bajo y de compensación : salida analógica.
### Parámetros característicos de SAD ( I)
Los parámetros que caracterizan a un SAD son básicamente tres:
1. Número de canales: depende del número de señales a adquirir.
2. Exactitud de la conversión: viene impuesta por los circuitos utilizados, es decir, por los multiplexores, amplificadores, S/H y ADC, esencialmente.
3. Velocidad de muestreo: número de muestras por unidad de tiempo ( Throughput Rate).
Participa: ¿recuerdas qué es la exactitud? ( enlace en BB)
### Parámetros característicos de SAD ( II): exactitud de la conversión
Depende de los módulos implicados, que deben cumplir con unas características mínimas:
1. Multiplexor ( MUX): baja resistencia de conducción ( Ron) y constante en el margen de variación de las señales de entrada; tiempos de establecimiento pequeños.
2. Amplificador de instrumentación ( AI): mínimas tensiones ( Vio) y corrientes de offset ( Iio), así como sus derivas; tiempo de establecimiento pequeño, aún con altas ganancias; amplio margen para programar la ganancia.
3. Circuito de muestreo y retención ( S/H): pequeña tensión de offset y deriva de ésta; máxima velocidad de caída en modo Hold, siempre y cuando la tensión a la salida del S/H esté constante el tiempo necesario para que el ADC la digitalice; tiempos de apertura, de adquisición y de asentamiento mínimos.
4. Conversor ADC: alta resolución; mínimo tiempo de conversión; error de linealidad y de ganancia pequeños.
### Parámetros característicos de SAD ( III): velocidad de muestreo ( Throughput Rate)
- Velocidad a la que el SAD puede adquirir y almacenar muestras de las entradas.
- Las muestras pueden pertenecer a un único canal o a varios, según la configuración, por lo que es fundamental revisar cuidadosamente los datos suministrados por el fabricante.
- En general debemos identificar el Throughput Rate con el número de muestras por unidad de tiempo que pueden obtenerse de un canal.
Los cuatro factores principales a tener en cuenta son:
1. Tiempo de propagación entrada-salida del multiplexor ( Tmux).
2. Tiempo de establecimiento del amplificador de instrumentación ( Tai).
3. Tiempo de adquisición ( Tadq_s), apertura ( Tap) y establecimiento ( Test_h) del circuito de muestreo y retención ( S/H).
4. Tiempo de conversión del ADC ( Tcon).
Se clasifican en función del número de canales de entrada en:
- SAD monocanales: disponen de una única entrada.
- SAD multicanal: disponen de varias entradas ( canales). Se clasifican a su vez en:
 1. SAD multicanal con muestreo secuencial de canales.
 2. SAD multicanal con muestreo simultáneo de canales.
 3. SAD multicanal paralelo.
### SAD monocanales ( I)
Configuración más general: AI ( amplificador de instrumentación), S/H ( Sample/Hold), SC ( Start Conversion), EOC ( End Of Conversion).
Características:
1. La entrada es única y es dónde se aplica la señal del sensor.
2. Todos los elementos del SAD están diseñados específicamente para la fuente de información procedente del sensor.
3. El margen dinámico del amplificador de instrumentación y el ADC están ajustados a los niveles de la señal de entrada.
4. Desventaja: sólo permite la adquisición de una entrada.
5. Ventaja: optimizado para un tipo concreto de señal.
### SAD monocanales ( II)
El tiempo que se tarda en configurar el AI ( Tai) no se tiene en cuenta en el cálculo de la frecuencia máxima ya que la entrada no cambia. La frecuencia de adquisición máxima viene dada por:
fsmax = 1 / ( Tadq_s + Tap + Test_h + Tcon)
Donde: Tadq_s es el tiempo de adquisición en modo Sample, Tap el tiempo de apertura para pasar del modo Sample a Hold, Test_h el tiempo de establecimiento en modo Hold, y Tcon el tiempo de conversión del ADC.
### SAD multicanal ( I)
- Existe la necesidad de convertir diversas señales o canales de entrada.
- Estas señales suelen requerir diferentes configuraciones de los canales de entrada ( diferentes niveles de señal, frecuencia, etc.).
- La configuración suele venir impuesta por: características de las señales analógicas de entrada ( frecuencia, aperiodicidad, etc.), información que se desee obtener de las señales, velocidad de conversión y coste.
- Existen distintas configuraciones en función de la distribución de los módulos en el sistema, dependiendo de cada aplicación en particular.
### SAD multicanal ( II-IV): muestreo secuencial de canales
Menos componentes precisa, la más económica de las opciones multicanal.
Funcionamiento:
1. Se selecciona el canal de entrada del multiplexor ( MUX).
2. Se fija la ganancia del amplificador de instrumentación ( AI).
3. El circuito de muestreo y retención ( S/H) pasa a modo Sample hasta que adquiere una muestra de la señal, momento en el que pasa al modo Hold.
4. Orden de inicio de conversión ( SC) en el ADC.
5. Una vez transcurrido el tiempo de conversión, el ADC lo indica mediante la señal de fin de conversión ( EOC).
6. Se repite el proceso con el mismo canal o bien con otro distinto.
Esta configuración permite que, durante el tiempo de conversión de un canal, se pueda estar seleccionando en el MUX, simultáneamente, el siguiente canal a muestrear. La multiplexación y la amplificación se pueden simultanear con la cuantificación, por tanto:
Tciclo = máx ( Tmux, Tai) + Tadq_s + Tap + Test_h + Tcon
Frecuencia de adquisición máxima, donde N es el número de canales de entrada del multiplexor:
fsmax = 1 / ( Tciclo · N)
### SAD multicanal ( V-VI): muestreo simultáneo de canales
Hay tantos circuitos de AI y S/H como entradas.
Ventaja: todos los circuitos S/H de entrada conmutan simultáneamente a modo Hold, manteniendo el valor de la muestra de cada señal de entrada hasta que el ADC pueda realizar la conversión, cosa que no era posible en el modelo de muestreo secuencial. Esta configuración es la indicada para sistemas de adquisición en los que es crítico que las medidas estén sincronizadas.
Su frecuencia máxima de muestreo viene dada por:
fsmax = 1 / [( Tadq_s + Tap + Test_h) + ( Tmux + Tcon) · N]
### SAD multicanal ( VII-VIII): paralelo
- En este caso, cada canal constituye un SAD independiente con todos los elementos necesarios para realizar una conversión A/D completa, con la salvedad de que, al utilizar generalmente un solo canal digital de salida, es necesario incluir un MUX digital.
Características:
- La configuración de un SAD multicanal paralelo ofrece una gran flexibilidad.
- Cada canal puede ser adaptado de forma independiente, según las necesidades requeridas por la señal a adquirir ( ganancia del amplificador, velocidad de adquisición, etc.).
- Otra ventaja adicional es que la velocidad del sistema se optimiza notablemente, ya que pueden realizarse simultáneamente varias conversiones.
- Como inconveniente fundamental cabe destacar su coste y el número de parámetros a controlar en cada instante.
- Su frecuencia máxima coincide con la del SAD monocanal:
fsmax = 1 / ( Tadq_s + Tap + Test_h + Tcon)
### Clasificación de los SAD y su conexión a los equipos de proceso ( I)
Existen dos clases genéricas de SAD:
1. SAD basados en Tarjetas de Adquisición de Datos ( TAD), conocidos como de bus interno.
2. SAD basados en interfaces estándar para instrumentación, o sistemas de bus externo.
### Clasificación de los SAD y su conexión a los equipos de proceso ( II-III)
Bus interno: SAD basados en Tarjetas de Adquisición de Datos ( TAD), con conexión directa o mediante rack de expansión. Diagrama de bloques de una TAD estándar.
### Clasificación de los SAD y su conexión a los equipos de proceso ( IV)
Bus externo:
- VXI ( Vesa eXtension for Instrumentation).
- PXI ( Pci eXtension for Instrumentation).
- GPIB ( General Purpose Instrumentation Bus).
- USB ( Universal Serial Bus).
- Ethernet.
- Wireless.
### Arquitectura del robot Pioneer ( I)
Ejemplo de arquitectura de adquisición y reproducción de un robot Pioneer, con CPU y microcontrolador Hitachi H8S.
### Microcontrolador Hitachi H8S ( I)
Características de los ADC del H8S: 8 conversores ADC, 10 bits de resolución, S&H interno, registro de aproximaciones sucesivas, pin Vref para ajustar el rango dinámico, Tc = 6.7 μs por canal ( 20 MHz).
Características de los DAC del H8S: 2 conversores DAC, 8 bits de resolución, salida desde 0V hasta Vref, Tc = 10 μs.
### Microcontrolador Hitachi H8S ( II): diagrama de bloques interno del ADC
8 conversores ADC, 10 bits de resolución, S&H interno, registro de aproximaciones sucesivas, pin Vref para ajustar rango dinámico, Tc = 6.7 μs por canal ( 20 MHz).
### Microcontrolador Hitachi H8S ( III): diagrama de bloques interno del DAC
2 conversores DAC, 8 bits de resolución, salida desde 0V hasta Vref, Tc = 10 μs.
Realiza los problemas disponibles en BlackBoard: Módulos de aprendizaje / Tema 2 / Problemas T2 SAD.
