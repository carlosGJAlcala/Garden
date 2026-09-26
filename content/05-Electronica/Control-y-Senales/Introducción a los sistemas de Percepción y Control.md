---
title: "Introducción a los sistemas de Percepción y Control"
tags: [universidad, 4anyo, pyc]
date: 2026-08-12
lang: es
---
# Introducción a los sistemas de Percepción y Control
Grado en Ingeniería de Computadores - Percepción y Control
Manuel Ocaña Miguel / Ángel Llamazares Llamazares
1. Introducción a los sistemas de Percepción y Control
2. Definición de robot móvil
3. Partes principales: actuadores, sensores y procesadores
4. Tipos de robots móviles
5. Modelos de movimiento
6. Mapas de entorno
Laboratorio: Introducción a ROS ( Robot Operating System).
### Introducción a los sistemas de control
Historia: aunque la mayoría de la teoría fue desarrollada en los últimos 70 años, la teoría de control se basa fundamentalmente en:
- Primero se desarrolló parte de la teoría de los servomecanismos, usando "servo" ( del latín esclavo).
- Desarrollos matemáticos de Laplace y Fourier ( transformadas de Laplace y Z).
- Teoría de estabilidad de sistemas lineales ( Nyquist).
Ejemplos:
- Doméstico: sistemas de climatización que regulan la temperatura y humedad; horno; robots domésticos ( aspirador, cortacésped).
- Industria: sistemas de control de calidad; mando de máquinas herramientas; robots y cadenas de ensamblaje.
- Espacial: satélites y vehículos espaciales cuentan con sofisticados sistemas de control, sin cuyo uso sería imposible su desarrollo.
Sistema de control en "lazo cerrado" ( existe realimentación). Ejemplo: mantener una velocidad.
Vídeo: componentes de un sistema de control en "lazo cerrado":
https://es.mathworks.com/videos/understanding-control-systems-part-3-components-of-a-feedback-control-system-123645.html
#### Definiciones
- Variable Controlada ( C): la cantidad o condición que se mide o controla.
- Señal de Referencia ( R): valor que debería tener la variable controlada.
- Planta ( G): proceso, parte de un equipo o conjunto de partes del mismo que se van a controlar.
- Regulador o Controlador ( F): encargado de generar la señal de Acción ( A).
- Realimentación ( H): o cadena de retorno, encargada de observar o medir la variable controlada y proporcionar la correspondiente señal de realimentación ( B).
- Señal de Error ( E): diferencia entre la señal de referencia ( R) y la señal de realimentación ( B).
- Cadena Directa ( FG): producto FG.
- Cadena Abierta ( FGH): producto FGH.
- Cadena Cerrada ( M): sistema realimentado completo.
- Perturbaciones: todo aquello que afecta negativamente al valor de salida del sistema.
- Control realimentado: operación que en presencia de perturbaciones tiende a reducir la diferencia ( E) entre la variable realimentada ( B) y la entrada de referencia ( R).
Sistema de control en "lazo cerrado" ( existe realimentación). Ejemplo: seguir una trayectoria.
- Señal de Referencia ( R): camino que deseamos seguir.
- Planta ( G): aparato locomotor.
- Regulador o Controlador ( F): cerebro.
- Realimentación ( H): sentido de la vista.
- Señal de Error ( E): diferencia entre la señal de referencia ( R) y la señal de realimentación ( B), se realiza en el cerebro.
- Perturbaciones: que por ejemplo se haga de noche, que andemos por un desierto, etc.
Vídeo con ejemplos de sistemas en "lazo cerrado":
https://es.mathworks.com/videos/understanding-control-systems-part-2-feedback-control-systems-123501.html
Sistema de control en "lazo abierto" ( sin realimentación). Ejemplo: seguir una trayectoria con los ojos cerrados.
- Señal de Referencia ( R): camino que deseamos seguir.
- Planta ( G): aparato locomotor.
- Regulador o Controlador ( F): cerebro.
- Realimentación ( H): no existe.
- Señal de Error ( E): no tenemos con qué comparar.
- Perturbaciones: cualquier cosa podrá afectar al seguimiento de la trayectoria.
Vídeo con ejemplos de sistemas en "lazo abierto":
https://es.mathworks.com/videos/understanding-control-systems-part-1-open-loop-control-systems-123419.html
Pregunta de clase: ¿Una tostadora es un sistema de control en lazo cerrado o en lazo abierto?
### Introducción a los sistemas de percepción
#### Definiciones
Sistema de medida: su función esencial es la asignación objetiva ( independiente del observador) y empírica ( basada en la experimentación) de un número a una propiedad o cualidad de un objeto o evento.
Objetivos de los sistemas de medida:
- Vigilancia o seguimiento de procesos: medida de la temperatura ambiente y de los contadores de agua y gas.
- Control de un proceso. Como ejemplo se puede considerar un termostato ( cuando alcanza una determinada temperatura conmuta y puede dar lugar al efecto contrario que originó su conmutación), el control del nivel de un depósito, guiado de un robot en un entorno, etc.
- Ingeniería experimental. Cuando se miden las fuerzas y aceleraciones que actúan sobre un vehículo cuando éste choca contra un objeto ( sistemas de airbag). Los resultados obtenidos de esta forma tienen su principal campo de aplicación en el diseño asistido por ordenador o CAD ( Computer Aided Design).
Diferencia entre transductor y sensor:
- Transductor: dispositivo que convierte una señal de una forma física ( mecánica, térmica, magnética, eléctrica, óptica y molecular o química) en otra señal, que se corresponde con la primera, pero de otra forma física distinta. Acopla la magnitud a medir al sistema de medida. Como el tratamiento de la señal de salida del transductor es normalmente llevado a cabo por equipos o circuitos electrónicos, los considerados comúnmente transductores son aquellos que ofrecen una señal de salida eléctrica: tensión, corriente.
- Sensor: elemento directamente en contacto con la magnitud a medir y no tiene por qué proporcionar ninguna salida eléctrica. Capta esta magnitud para posteriormente transformarla y obtener una salida eléctrica.
Ejemplo: micrófono magnético.
Pregunta de clase: ¿Qué es un robot?
### ¿Qué es un robot? ( I)
Palabra creada en 1920 por el escritor checo Karel Capek a partir del término checo "robota", que significa "servidumbre, siervo, trabajador forzado", para referirse a cualquier máquina, de forma humana o no, que pudiera llevar a cabo tareas inteligentes.
RAE: "Máquina o ingenio electrónico programable, capaz de manipular objetos y realizar operaciones antes reservadas sólo a las personas".
En términos científicos no existe una definición generalmente aceptada. Por ejemplo: "Dispositivo generalmente mecánico, que desempeña tareas automáticamente, ya sea de acuerdo a supervisión humana directa, a través de un programa predefinido o siguiendo un conjunto de reglas generales, utilizando técnicas de inteligencia artificial. Generalmente estas tareas reemplazan, asemejan o extienden el trabajo humano, como ensamble en manufactura, manipulación de objetos pesados o peligrosos, trabajo en el espacio, etc."
### ¿Qué es un robot? ( II)
Clasificación general de los robots según su capacidad de desplazamiento:
1. Robots manipuladores ( base anclada).
2. Robots móviles ( posibilidad de desplazamiento).
3. Robots híbridos ( móviles con manipulación).
Esquema general de un sistema robótico: percepción externa ( visión, tacto, audición, proximidad, otros) sobre el entorno, sistema de control ( estructura mecánica, actuadores), percepción interna ( sensores) y actuadores.
Partes principales:
- Sensores ( percepción).
- Procesadores ( sistema de control).
### Actuadores
- Convierten las órdenes del sistema de control en acciones físicas ( movimientos).
- Locomoción ( desplazamiento).
- Manipulación ( manejo de objetos).
- Actuador se refiere al elemento que genera movimiento, no a la parte mecánica. Ejemplo: el actuador es el motor, no la rueda que mueve.
Tipos de actuadores utilizados en robótica: neumáticos e hidráulicos ( aplicaciones industriales) y eléctricos ( los más utilizados en robótica móvil).
Pregunta de clase: escribe algún ejemplo de actuador.
### Sensores ( I)
Clasificación de los sensores:
- Según el origen de la información:
 - Propioceptivos: informan del estado del propio robot ( encoders, estado de la batería, orientación del robot, etc.).
 - Extereoceptivos: informan del estado del entorno en el que se encuentra el robot ( medidores de distancia, visión, etc.).
- Según la procedencia de la energía:
 - Pasivos: reciben información de la energía del entorno ( brújula, cámara visible, etc.).
 - Activos: emiten energía ( en forma de radiación, por ejemplo) y comprueban su efecto sobre el entorno ( infrarrojos, láser, etc.).
Pregunta de clase: clasifica estos sensores.
### Sensores ( II)
Ejemplos de sensores más utilizados en robótica móvil ( uso típico / sensor / propioceptivo o extereoceptivo / activo o pasivo):
- Sensores táctiles ( detección de contacto físico): sensores de contacto, bumpers ( extereoceptivo, pasivo); sensor táctil óptico ( extereoceptivo, activo).
- Posición y velocidad: potenciómetros ( propioceptivo, pasivo); máquinas síncronas y resolvedores ( propioceptivo, pasivo); encóders ópticos, magnéticos, inductivos o capacitivos, para medida de posición/velocidad de ruedas ( propioceptivo, activo).
- Orientación: brújulas ( extereoceptivo, pasivo); giróscopos, para orientación del robot respecto a un eje de referencia fijo ( propioceptivo, pasivo); inclinómetros ( extereoceptivo, pasivo); GPS ( extereoceptivo, activo/pasivo).
- Balizas fijas ( localización en un sistema de referencia fijo): balizas RF ( extereoceptivo, activo); balizas ultrasónicas activas ( extereoceptivo, activo); balizas reflectivas ( extereoceptivo, activo).
- Distancia: sensores de ultrasonidos ( extereoceptivo, activo); sensores láser, por reflectividad, tiempos de vuelo, etc. ( extereoceptivo, activo).
- Movimiento ( velocidad relativa a objetos): radar Doppler ( extereoceptivo, activo); sonido Doppler ( extereoceptivo, activo).
- Sensores visuales: cámaras CCD/CMOS ( extereoceptivo, pasivo/activo); odometría visual, para distancia visual, reconocimiento de objetos, etc. ( propioceptivo, pasivo); medición de distancia ( extereoceptivo, activo).
Preguntas de clase: ¿Cuál crees que es el sensor láser? ¿Dónde crees que está la cámara omnidireccional? ¿Dónde crees que están los bumpers ( sensores de contacto)?
### Sensores ( III)
Ejemplo de robot móvil con sistema multisensorial: cámara omnidireccional, cámara pan-tilt, unidad de medida inercial, ultrasonidos, láser, bumpers, encóders.
### Procesadores ( I)
- Antes de 1970 los cómputos se realizaban fuera del robot ( ordenadores demasiado grandes y pesados).
- A partir de los años 80 ya se utilizaban procesadores específicos dentro de la estructura mecánica del robot.
- Desde comienzos de los 90 los ordenadores personales ( PC) se han insertado como elementos principales de cómputo de los robots de investigación, dejando los procesadores específicos para tareas de bajo nivel muy concretas ( procesamiento de imágenes, control de motores y lectura de sensores, etc.).
La configuración más frecuente hoy en día consiste en un PC y varios microcontroladores. En los microcontroladores se ejecuta un SO de bajo nivel ( por ejemplo, ARCOS en los Pioneer) y la comunicación con el PC se realiza a través del puerto serie RS232 respetando cierto protocolo. De esta manera se concentra la mayor parte del cómputo en el PC, que es sencillo de actualizar cuando queda obsoleto.
### Procesadores ( II)
Ejemplo de arquitectura de procesadores de un robot Amigobot: CPU y microcontrolador Hitachi H8S.
Clasificación general: vehículos con ruedas, pistas de deslizamiento, robots con patas, robots articulados, robots submarinos y aéreos.
### Vehículos con ruedas ( I)
Características principales:
- Solución simple y eficiente para terrenos duros, planos y libres de obstáculos.
- Velocidades relativamente altas.
- Buena capacidad de "carga".
- Deslizamientos y vibraciones.
- Poco eficiente en terrenos blandos.
- Maniobrabilidad limitada excepto en configuraciones especiales.
### Vehículos con ruedas ( II): tipos de ruedas
Atendiendo a la tracción:
- Motriz: su velocidad la fija un motor asociado a la rueda.
- Pasiva: no lleva motor, su movimiento queda fijado por el del vehículo ( sólido rígido).
Atendiendo a la dirección:
- Directriz: su ángulo de dirección lo fija un motor asociado a la rueda.
- Fija: no puede cambiar de dirección.
- Libre: puede girar libremente, quedando su dirección determinada por el movimiento del vehículo ( sólido rígido). Ruedas tipo castor.
- Omnidireccional: puede girar en cualquier dirección de forma instantánea ( ruedas suecas o esféricas).
Tipos ilustrados: rueda libre, rueda directriz descentrada ( castor), rueda sueca, rueda fija ( omnidireccional).
### Vehículos con ruedas ( III): ejemplos ruedas suecas
Robot PPRK, Robotnik XL-Gen, KUKA omniMove.
### Ruedas suecas / Mecanum / Ilion ( omnidireccionales)
Rueda "normal" en rodadura, pero que permite el deslizamiento lateral.
- Ventajas: omnidireccionalidad.
- Desventajas: grandes deslizamientos; implementación y control más complicada.
Fuente: https://riunet.upv.es - Movilidad inteligente en entornos industriales.
### Vehículos con ruedas ( IV): rodadura ideal
Se produce cuando:
- No hay deslizamiento lateral de la rueda ( dirección perpendicular a la rodadura).
- No hay deslizamiento translacional entre la rueda y el suelo.
- Como máximo hay un eje de dirección.
- El eje de dirección es perpendicular al suelo.
Este modelo es válido a velocidades suficientemente bajas. En estas condiciones la distancia avanzada por el punto central de la rueda por cada giro de la misma es la longitud de la circunferencia = 2πr ( siendo r el radio de la rueda).
### Vehículos con ruedas ( V): condiciones de rodadura ideal en vehículos a ruedas
Puesto que un vehículo es un sólido rígido se deben cumplir ciertas restricciones para que exista rodadura ideal:
1. Centro Instantáneo de Rotación ( ICR): todos los ejes de rodadura ( perpendiculares al plano de la rueda) deben confluir en un mismo punto ( ICR).
2. Sólo existen tres grados de libertad en las variables de velocidad y dirección de las "n" ruedas: v_r1 × cos ( r1) = v_r2 × cos ( r2).
### Vehículos con ruedas ( VI): consideraciones en la elección del tipo/disposición de ruedas ( sistemas de locomoción)
1. Estabilidad: número de puntos de contacto, centro de gravedad, estática/dinámica...
2. Maniobrabilidad: omnidireccional, restricciones, geometría...
 - Omnidireccionalidad total: capacidad para desplazarse instantáneamente en cualquier dirección del plano sin "reorientar" el "cuerpo" del robot.
 - Omnidireccionalidad parcial: capacidad para rotar sobre su propio centro.
3. Controlabilidad: sencillo/complejo.
En general hay compromiso entre estos tres aspectos.
### Vehículos con ruedas ( VII): configuraciones típicas ( sistemas de locomoción)
1. Triciclo clásico: rueda delantera motriz y directriz. Ruedas traseras fijas y pasivas.
2. Ackermann: utilizado en vehículos de cuatro ruedas convencionales. Se usa de forma generalizada en robots móviles en exteriores.
3. Direccionamiento diferencial: dos ruedas motrices fijas montadas sobre el mismo eje.
4. Direccionamiento síncrono ( synchro drive): actuación simultánea de todas las ruedas, que giran de forma síncrona.
### Vehículos con ruedas ( VIII): direccionamiento diferencial
- Dos ruedas motrices fijas montadas sobre el mismo eje.
- El direccionamiento viene dado por la diferencia de velocidades entre las dos ruedas. Consigue omnidireccionalidad parcial ( movimiento en sentido contrario de las dos ruedas).
- Tres grados de libertad: ángulo de las ruedas ( fijo), velocidad de la rueda derecha, velocidad de la rueda izquierda.
- Necesidad de control para mantener el movimiento en línea recta.
- Necesidad de una o más ruedas tipo castor para soporte.
- Configuración muy frecuente en robots para interiores, normalmente más pequeños y que soportan menos carga.
### Pistas de deslizamiento y articulados
Pistas de deslizamiento:
- Vehículos tipo oruga en los que tanto la impulsión como el direccionamiento se consiguen mediante pistas de deslizamiento.
- Las pistas actúan como ruedas de gran diámetro, permitiendo superar desniveles del terreno superiores a las ruedas convencionales.
- Útiles en navegación "campo a través" o en terrenos irregulares.
- Deslizamientos implícitos. Imposible localización mediante odometría.
- Suelen utilizarse en funcionamiento teleoperado.
Robots articulados:
- Para terrenos difíciles a los que debe adaptarse el cuerpo del robot.
- Normalmente se articulan dos o más módulos con locomoción a ruedas.
- La redundancia en la estructura ofrece la posibilidad de intercambiar segmentos y facilitar su transporte.
- Son configuraciones recientes. Prototipos de laboratorio. Control complejo.
### Robots con patas
- Permiten aislar el cuerpo del terreno empleando puntos discretos de soporte.
- Mejores propiedades que las ruedas para atravesar terrenos difíciles llenos de obstáculos o desniveles.
- Permiten conseguir la omnidireccionalidad.
- Menor deslizamiento.
- Mayor complejidad de los mecanismos de control y mayor consumo de energía en la locomoción.
- Gran variedad de estructuras y tipos de patas.
- Son de interés los robots trepadores utilizados en tareas de inspección y reparación en paredes verticales.
- Reciente campo de interés: los robots humanoides ( bípedos).
### Robots submarinos y aéreos
- Mayor dificultad de control: movimiento tridimensional.
- No puede obviarse el estudio dinámico, al contrario de lo que sucede con los robots "terrestres" en la mayoría de los casos.
### Robots aéreos
Auge de los robots aéreos: de ala fija, de hélice multi-rotor ( por ejemplo, cuadricópteros).
Movimientos básicos de un cuadricóptero: ascender/descender, giro izquierda/derecha, avanza/retrocede, mueve izquierda/derecha, posición estable ( compensa gravedad).
### Variables para caracterizar el movimiento ( I): posición del robot en el plano
Viene dada por la posición de un punto del móvil ("punto de referencia") y el ángulo de un eje del mismo ("eje de referencia"): P = [x, y, θ]ᵗ. Se llama pose ( posición + orientación).
Puede estar referenciado respecto a:
- Sistema de referencia global: un sistema de referencia externo fijo.
- Sistema de referencia del robot ( local): tiene como origen el punto de referencia del robot y cuyo eje de abscisas coincide con su eje de referencia.
### Variables para caracterizar el movimiento ( II): cambios de un sistema de referencia a otro
Del sistema local al global:
```
[xg] [xr] [cosθ -senθ] [x]
[yg] = [yr] + [senθ cosθ] × [y]
```
Del sistema global al local:
```
[x] [ cosθ senθ] [xg - xr]
[y] = [-senθ cosθ] × [yg - yr]
```
Ejercicio: demostrar matemáticamente que las ecuaciones anteriores son correctas. Pista: relaciones trigonométricas del triángulo rectángulo.
### Variables para caracterizar el movimiento ( III): convertir medida del sistema de referencia del sensor al del robot
Ejercicio: calcular las coordenadas del punto en el sistema de coordenadas del robot ( X_punto, Y_punto) a partir de los datos del sensor ( dist, X_sensor, Y_sensor, θ_sensor).
### Variables para caracterizar el movimiento ( IV): velocidad global del robot
Caracteriza el movimiento del móvil respecto al sistema de referencia global mediante dos componentes:
- Velocidad lineal ( v): velocidad del "punto de referencia" en la dirección del "eje de referencia".
- Velocidad angular ( W/ω): velocidad de variación del ángulo del eje de referencia respecto al sistema de referencia global.
V_W = [v, W]ᵗ
Integración de la velocidad global ( P') para obtener la posición:
```
 [x'] [v×cosθ] [cosθ 0]
P' = [y'] = [v×senθ] = [senθ 0] × [v]
 [θ'] [ W ] [ 0 1] [W]
```
### Variables para caracterizar el movimiento ( V)
Ejercicio: calcular la pose del robot en el instante actual ( x ( t), y ( t), θ( t)) en función de las velocidades actuales ( v ( t), W ( t)) y la posición anterior ( x ( t-1), y ( t-1), θ( t-1)) y el tiempo t.
### Tipos de modelos de movimiento
Existen dos tipos de modelos de movimiento:
1. Modelo dinámico: describe el movimiento del móvil en función de los pares y/o fuerzas internas ( sistemas de actuación) y/o externas ( rozamientos, deslizamientos, etc.).
2. Modelo cinemático: describe el movimiento del móvil en función de las velocidades y giros aplicados a las ruedas ( parámetros de control), sin tener en cuenta las fuerzas que los generan.
Dentro del estudio cinemático se distinguen dos casos:
a) Cinemática directa: obtención de la posición en función de los parámetros de control ( parámetros de control : posición: x, y, θ).
b) Cinemática inversa: obtención de los parámetros de control que permiten llegar a una determinada posición ( posición: x, y, θ : parámetros de control).
### Modelos cinemáticos de móviles a ruedas ( I)
1. Hipótesis de partida:
 - El robot se mueve sobre una superficie plana.
 - Los ejes de guiado son perpendiculares al suelo.
 - Condiciones de rodadura ideal ( no hay deslizamientos).
 - El robot no tiene partes flexibles.
 - Durante un periodo de tiempo suficientemente pequeño en el que se mantiene constante la consigna de dirección, el vehículo se moverá de un punto al siguiente a lo largo de un arco de circunferencia.
 - El robot se comporta como un sólido rígido, de manera que si existen partes móviles ( ruedas tipo castor), éstas se situarán en la posición adecuada para proporcionar rodadura ideal.
2. Restricciones cinemáticas: son dependencias de las variables que influyen en el movimiento. Dos tipos:
 - Holónomas: son restricciones en las que no intervienen las velocidades. Típicas en brazos articulados.
 - No holónomas: son restricciones dependientes de las velocidades. Típicas en muchos robots móviles.
Intuitivamente: las restricciones no holónomas no limitan la posición final a alcanzar dada una posición inicial, pero sí el camino seguido para llegar a ella.
### Modelos cinemáticos de móviles a ruedas ( II): ejemplo, robots con configuración diferencial
Parámetros de control: w_r ( velocidad angular de la rueda derecha), w_l ( velocidad angular de la rueda izquierda). r = radio de las ruedas; L = distancia entre las ruedas.
Cinemática directa:
- Velocidad lineal del robot: v = ( v_r + v_l)/2 = ( r×w_r + r×w_l)/2 = ( r/2)×( w_r + w_l)
- Velocidad angular del robot: W = ( v_r - v_l)/L = ( r×w_r - r×w_l)/L = ( r/L)×( w_r - w_l)
Sustituyendo en la ecuación general:
```
 [x'] [v×cosθ] [( r/2)cosθ ( r/2)cosθ]
P' = [y'] = [v×senθ] = [( r/2)senθ ( r/2)senθ] × [w_r]
 [θ'] [ W ] [ r/L -r/L ] [w_l]
```
Restricción no holónoma: x×senθ - y×cosθ = 0
Cinemática inversa: debido a la restricción no holónoma, la cinemática inversa es difícil de resolver. Existen múltiples ( pero no infinitas) soluciones para llegar a una posición final. Ejemplo: solución basada en la concatenación de giros sobre el sitio y trayectorias rectilíneas.
### Métodos de representación del entorno
Modelo o mapa de entorno: abstracción en la que se representan únicamente aquellas características del entorno que se consideran útiles para la navegación o localización.
Mapas métricos:
- Modelos geométricos: definen el entorno mediante sus características geométricas ( distancias, dimensiones, posiciones, etc.).
- Rejillas de ocupación: discretización del entorno en celdas. Cada celda tiene asociada una probabilidad de ocupación.
Mapas topológicos: representan las características esenciales mediante un grafo ( discretización muy gruesa). No ofrecen precisión métrica, pero no requieren mantener la consistencia métrica global. Más sencillos para la planificación ( por ejemplo, "ir a la habitación A").
Pregunta de clase: ¿Qué esperas de esta asignatura?
