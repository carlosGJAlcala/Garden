# Introducción

*Computer Organization and Design: The Hardware/Software Interface — Arquitectura e Ingeniería de Computadores*

## Introducción

*Abstracciones informáticas y tecnología*

### La revolución informática

- Progreso en la tecnología informática, sustentado por la Ley de Moore.
- Hace que las aplicaciones novedosas sean factibles: computadoras en automóviles, celulares, Proyecto Genoma Humano, World Wide Web, los motores de búsqueda.
- Las computadoras son omnipresentes.

### clases de computadoras

- Computadoras personales: propósito general, variedad de software, sujeto a compensación de costo/rendimiento.
- Computadoras servidor: basado en red, alta capacidad, rendimiento, fiabilidad; varía desde servidores pequeños hasta el tamaño de un edificio.

### Clases de computadoras

- Supercomputadoras: cálculos científicos y de ingeniería de alta gama; la capacidad más alta pero representa una pequeña fracción del mercado general de computadoras.
- Ordenadores integrados: ocultos como componentes de sistemas; restricciones estrictas de potencia/rendimiento/costo.

### La era PostPC

- Dispositivo móvil personal ( PMD): de pilas, se conecta a Internet, cientos de dólares; teléfonos inteligentes, tabletas, gafas electrónicas.
- Computación en la nube: computadoras a escala de almacén ( WSC), software como servicio ( SaaS); una parte del software se ejecuta en un PMD y una parte se ejecuta en la nube. Ejemplos: Amazon y Google.

### Lo que vas a aprender

- Cómo se traducen los programas al lenguaje máquina y cómo los ejecuta el hardware.
- La interfaz hardware/software.
- Lo que determina el rendimiento del programa y cómo se puede mejorar.
- Cómo los diseñadores de hardware mejoran el rendimiento.
- ¿Qué es el procesamiento paralelo?

### Comprender el rendimiento

- Algoritmo: determina el número de operaciones ejecutadas.
- Lenguaje de programación, compilador, arquitectura: determinan el número de instrucciones de máquina ejecutadas por operación.
- Procesador y sistema de memoria: determinan qué tan rápido se ejecutan las instrucciones.
- Sistema de E/S ( incluido el sistema operativo): determina qué tan rápido se ejecutan las operaciones de E/S.

### Ocho grandes ideas

- Diseño para la Ley de Moore.
- Usa la abstracción para simplificar el diseño.
- Hacer el caso común rápido.
- Rendimiento vía paralelismo.
- Rendimiento vía canalización.
- Rendimiento vía predicción.
- Jerarquía de memoria.
- Confianza vía redundancia.

### Debajo de su programa

- Software de la aplicación: escrito en lenguaje de alto nivel.
- Software del sistema:
  - Compilador: traduce código HLL a código de máquina.
  - Sistema operativo: código de servicio — manejo de entrada/salida, administrar la memoria y el almacenamiento, programar tareas y compartir recursos.
- Hardware: procesador, memoria, controladores de E/S.

### Niveles de descripción y diseño de un computador

Niveles de abstracción de un computador, de arriba a abajo:

- **Aplicación**: ofimática ( MS-Office, Contaplus, D-Base), comunicaciones ( Netscape, Explorer, Mail), diseño ( AutoCAD, ...), multimedia, juegos, etc.
- **Lenguaje de alto nivel**: for, while, repeat, procedure, ... ( Pascal, Fortran, C, Cobol, Basic, ..., Módula, C++, Java, ...)
- **Sistema Operativo / Compilador**: gestión de memoria, gestión de procesos, gestión de ficheros ( compilación, enlazado, ubicación).
- **Arquitectura del repertorio de instrucciones**: registros, registro de estado, contador de programa.
- **Organización**: hardware del sistema.
- **Circuito Digital**.
- **Físico**: CPU, memoria, bus, E/S.

Ejemplo de código de bajo nivel correspondiente:

```asm
Loop: move #$10,R0
      load R1 ( dir1),R2
      add  R2,R0
      sub  #1,R1
      beq  Loop
```

*Diagrama de la diapositiva: pirámide de niveles de abstracción software/hardware ( Aplicación → Lenguaje de alto nivel → SO/Compilador → ISA/Registros → Organización → Circuito Digital → Físico), con R0/R7 y el fragmento de código ensamblador situados junto al nivel de ISA. El layout visual exacto no se pudo recuperar de la extracción OCR; el contenido textual se ha preservado en la lista anterior.*

### Niveles de código de programa

- Lenguaje de alto nivel: nivel de abstracción más cercano al dominio del problema; proporciona productividad y portabilidad.
- Lenguaje ensamblador: representación textual de instrucciones; representación de hardware.
- Dígitos binarios ( bits): instrucciones y datos codificados.

### ISA: Interfaz Crítica entre software y hardware

- software
- instruction set
- hardware

Propiedades:
- Permanencia con el tiempo / tecnología ( portabilidad).
- Proporciona funcionalidad eficaz a los niveles superiores.
- Permite implementación eficiente en los niveles inferiores.

### Componentes de una computadora ( El panorama)

- Mismos componentes para todo tipo de ordenador: escritorio, servidor, integrado.
- Entrada/salida incluye:
  - Dispositivos de interfaz de usuario: pantalla, teclado, ratón.
  - Dispositivos de almacenamiento: disco duro, CD/DVD, flash.
  - Adaptadores de red: para comunicarse con otras computadoras.

### Pantalla táctil

- Dispositivo PostPC: reemplaza el teclado y el mouse.
- Tipos resistivos y capacitivos.
- La mayoría de las tabletas y los teléfonos inteligentes usan tecnología capacitiva.
- Capacitivo permite múltiples toques simultáneamente.

### Através del espejo

- Pantalla LCD: elementos de imagen ( píxeles).
- Refleja el contenido de la memoria intermedia de cuadros.

### Abriendo la Caja

- Pantalla LCD multitáctil capacitiva.
- Batería de 3,8 V, 25 vatios-hora.
- Tablero de computadora.

### Dentro del procesador ( CPU)

- Datapath: realiza operaciones en los datos.
- Control: ruta de datos de secuencias, memoria, ...
- Memoria caché: pequeña memoria SRAM rápida para acceso inmediato a los datos.

### Dentro del procesador

Apple A5/A12

### Abstracciones ( El panorama)

- La abstracción nos ayuda a lidiar con la complejidad: oculta detalles de nivel inferior.
- Arquitectura del conjunto de instrucciones ( ISA): la interfaz hardware/software.
- Interfaz binaria de la aplicación: la interfaz del software del sistema ( ISA + SO).
- Implementación: los detalles subyacentes y la interfaz.

### Un lugar seguro para los datos

- Memoria principal volátil: pierde instrucciones y datos cuando se apaga.
- Memoria secundaria no volátil: disco magnético, memoria flash, disco óptico ( CDROM, DVD).

### Redes

- Comunicación, intercambio de recursos, acceso no local.
- Red de área local ( LAN): Ethernet.
- Red de área amplia ( WAN): Internet.
- Red inalámbrica: Wi-Fi, Bluetooth.

### Tendencias tecnológicas

- La tecnología electrónica sigue evolucionando: mayor capacidad y rendimiento, costo reducido ( capacidad DRAM).

| Año | Tecnología | Rendimiento/costo relativo |
| --- | --- | --- |
| 1951 | Tubo vacío | 1 |
| 1965 | Transistor | 35 |
| 1975 | Circuito integrado ( CI) | 900 |
| 1995 | CI de muy gran escala ( VLSI) | 2.400.000 |
| 2013 | IC de ultra gran escala | 250.000.000.000 |

### Tecnología de semiconductores

- Silicio: semiconductor.
- Añadir materiales para transformar propiedades: conductores, aisladores.
- Cambiar.

### Fabricación de circuitos integrados

- Rendimiento: proporción de troqueles de trabajo por oblea.

### Oblea Intel Core i7

- Oblea de 300 mm, 280 chips, tecnología de 32 nm.
- Cada chip es de 20,7 x 10,5 mm.

### Intel® Core 10th Gen

- 300mm wafer, 506 chips, 10nm technology.
- Each chip is 11.4 x 10.7 mm.

### Costo del circuito integrado

$$\text{Cost per die} = \frac{\text{Cost per wafer}}{\text{Dies per wafer} \times \text{Yield}}$$

$$\text{Dies per wafer} \approx \frac{\text{Wafer area}}{\text{Die area}}$$

$$\text{Yield} = \frac{1}{\left(1 + \frac{\text{Defects per area} \times \text{Die area}}{2}\right)^2}$$

- Relación no lineal con el área y la tasa de defectos.
- El costo y el área de la oblea son fijos.
- Tasa de defectos determinada por el proceso de fabricación.
- Área de matriz determinada por la arquitectura y el diseño del circuito.

### Definición de rendimiento

¿Qué avión tiene el mejor rendimiento? Comparativa entre Boeing 777, Boeing 747, BAC/Sud Concorde y Douglas DC-8-50.

*Gráficos de la diapositiva: barras comparando Passenger Capacity, Cruising Range ( miles), Cruising Speed ( mph) y Passengers × mph para los cuatro aviones. Los valores numéricos de las barras no se pudieron recuperar con fiabilidad de la extracción OCR.*

### Rendimiento

Dos conceptos clave:

| Avión | Vía a París | Velocidad | Pasajeros | Throughput ( p·km/h) |
| --- | --- | --- | --- | --- |
| Boeing 747 | 6,5 horas | 970 km/h | 470 | 455.900 |
| Concorde | 3 horas | 2.160 km/h | 132 | 285.120 |

- **Tiempo de Ejecución ( TEj)**: tiempo que tarda en completarse una tarea ( tiempo de respuesta, latencia).
- **Rendimiento ( Performance, Throughput)**: tareas por hora, día, …

"X es n veces más rápido que Y" significa:

$$\frac{TEj(Y)}{TEj(X)} = \frac{Performance(X)}{Performance(Y)} = n$$

Reducir el TEj incrementa el rendimiento.

### Tiempo de respuesta y rendimiento

- Tiempo de respuesta: cuánto se tarda en hacer una tarea.
- Rendimiento: trabajo total realizado por unidad de tiempo, por ejemplo, tareas/transacciones/… por hora.
- ¿Cómo se ven afectados el tiempo de respuesta y el rendimiento por…
  - ¿Reemplazar el procesador con una versión más rápida?
  - ¿Agregar más procesadores?
- Nos centraremos en el tiempo de respuesta por ahora...

### Tiempo de respuesta y rendimiento ( cont.)

$$T = I \times CPI \times T_c$$

- **I** ( recuento de instrucciones): se reduce si el compilador genera menos instrucciones máquina o/y menos bucles. OJO: recuento dinámico, no estático.
- **CPI**: se reduce el nº de ciclos de c/instr, o si la ejecución de las instr. se solapa ( segmentación y ejecución superescalar).
- **T_c** ( procesador): se incrementa la frecuencia de reloj mejorando la tecnología del CI, o reduciendo el procesamiento por ciclo.

Observar que no son factores independientes: mejorar uno puede empeorar otro.

### Rendimiento

$$T_{CPU} = N \times CPI \times T_c$$

- N: nº de instrucciones ( Compiladores y LM).
- CPI: ciclos medios por instrucción ( LM, implementación, paralelismo).
- T_c: período de reloj ( implementación, tecnología).

$$CPI = \frac{T_{CPU} \times \text{Frecuencia de reloj}}{\text{Número de Instrucciones}} = \frac{\text{Ciclos}}{\text{Número de Instrucciones}}$$

Si asumimos que existen n tipos de instrucciones:

$$T_{CPU} = T_c \times \sum_{j=1}^{n} ( CPI_j \times I_j) \quad ( I_j = \text{nº instrucciones tipo } j \text{ ejecutadas})$$

$$CPI = \sum_{j=1}^{n} CPI_j \times F_j \quad ( \text{donde } F_j \text{ es la frecuencia de aparición de la instrucción tipo } j)$$

Ejemplo: ALU 1 ciclo ( 50%), Ld 2 ciclos ( 20%), St 2 ciclos ( 10%), saltos 2 ciclos ( 20%).

CPI: ALU 0.5, Ld 0.4, St 0.2, salto 0.4 → CPI TOTAL = 1.5

### Desempeño relativo

Definir rendimiento = 1/Tiempo de ejecución.

"X es n veces más rápido que Y":

$$\frac{Performance_X}{Performance_Y} = \frac{Execution\ time_Y}{Execution\ time_X} = n$$

Ejemplo: tiempo necesario para ejecutar un programa: 10s en A, 15s en B.

$$\frac{Tiempo\ de\ ejecución_B}{Tiempo\ de\ ejecución_A} = \frac{15\,s}{10\,s} = 1,5$$

Entonces A es 1,5 veces más rápido que B.

### Medición del tiempo de ejecución

- Tiempo transcurrido: tiempo total de respuesta, incluyendo todos los aspectos ( procesamiento, E/S, sobrecarga del sistema operativo, tiempo de inactividad). Determina el rendimiento del sistema.
- Tiempo de CPU: tiempo dedicado a procesar un trabajo determinado ( descuenta tiempo de E/S, acciones de otros trabajos). Comprende el tiempo de CPU del usuario y el tiempo de CPU del sistema.
- Los diferentes programas se ven afectados de manera diferente por la CPU y el rendimiento del sistema.

### Reloj de la CPU

- Operación de hardware digital gobernado por un reloj de tasa constante: período de reloj ( ciclos) → transferencia de datos y computación → actualizar estado.
- Período de reloj: duración de un ciclo de reloj, por ejemplo, 250ps = 0,25ns = 250×10⁻¹² s.
- Frecuencia de reloj ( tasa): ciclos por segundo, por ejemplo, 4,0 GHz = 4000 MHz = 4,0 × 10⁹ Hz.

### Tiempo de CPU

$$\text{CPU Time} = \text{CPU Clock Cycles} \times \text{Clock Cycle Time} = \frac{\text{CPU Clock Cycles}}{\text{Clock Rate}}$$

- Rendimiento mejorado por: reducción del número de ciclos de reloj, aumento de la frecuencia del reloj.
- El diseñador de hardware a menudo debe compensar la frecuencia del reloj con el recuento de ciclos.

### Ejemplo de tiempo de CPU

Un programa tarda 10 segundos en ejecutarse en el ordenador A, que tiene una frecuencia de reloj de 2 GHz. Queremos que el computador B tarde 6 segundos en ejecutar el mismo programa. En este caso, se puede introducir una mejora para incrementar la frecuencia de reloj, pero esto supone que el ordenador B necesitará 1,2 veces más ciclos de reloj que el A para ejecutar el mismo programa. ¿Cuál es la frecuencia de reloj que cumple con estas condiciones?

### Ejemplo de tiempo de CPU ( solución)

- Computadora A: reloj de 2 GHz, tiempo de CPU de 10 s.
- Diseño de la computadora B: apunta a 6 segundos de tiempo de CPU. Puede hacer un reloj más rápido, pero causa 1,2× ciclos de reloj.
- ¿Cuál debe ser la frecuencia del reloj de la computadora B?

$$\text{Clock Rate}_B = \frac{\text{Clock Cycles}_B}{\text{CPU Time}_B} = \frac{1.2 \times \text{Clock Cycles}_A}{6s}$$

$$\text{Clock Cycles}_A = \text{CPU Time}_A \times \text{Clock Rate}_A = 10s \times 2\text{GHz} = 20 \times 10^9$$

$$\text{Clock Rate}_B = \frac{1.2 \times 20 \times 10^9}{6s} = \frac{24 \times 10^9}{6s} = 4\text{GHz}$$

### Recuento de instrucciones y CPI

$$\text{Clock Cycles} = \text{Instruction Count} \times \text{Cycles per Instruction}$$

$$\text{CPU Time} = \text{Instruction Count} \times CPI \times \text{Clock Cycle Time} = \frac{\text{Instruction Count} \times CPI}{\text{Clock Rate}}$$

- Recuento de instrucciones para un programa: determinado por programa, ISA y compilador.
- Ciclos promedio por instrucción: determinado por el hardware de la CPU.
- Si diferentes instrucciones tienen diferentes CPI, el CPI promedio se ve afectado por la combinación de instrucciones.

### Ejemplo de IPC

Tenemos dos implementaciones del mismo ISA. La implementación A tiene un periodo de reloj de 250 ps y un CPI de 2, para un programa, mientras que la B tiene un periodo de reloj de 500 ps y un CPI de 1,2, para el mismo programa. ¿Qué ordenador es más rápido ejecutando este programa y por cuánto?

### Ejemplo de IPC ( solución)

- Computadora A: Tiempo de ciclo = 250ps, CPI = 2.0.
- Computadora B: Tiempo de ciclo = 500ps, CPI = 1.2.
- Misma ISA. ¿Cuál es más rápido y por cuánto?

$$\text{CPU Time} = \text{Instruction Count} \times CPI \times \text{Cycle Time}$$

$$\text{CPU Time}_A = I \times 2.0 \times 250ps = I \times 500ps$$

$$\text{CPU Time}_B = I \times 1.2 \times 500ps = I \times 600ps$$

$$\frac{\text{CPU Time}_B}{\text{CPU Time}_A} = \frac{I \times 600ps}{I \times 500ps} = 1.2$$

...por tanto, A es más rápido, por un factor de 1,2.

### IPC en más detalle

Si diferentes clases de instrucción toman diferentes números de ciclos:

$$\text{Clock Cycles} = \sum_{i=1}^{n} ( CPI_i \times \text{Instruction Count}_i )$$

IPC medio ponderado:

$$CPI = \frac{\text{Clock Cycles}}{\text{Instruction Count}} = \sum_{i=1}^{n} CPI_i \times \frac{\text{Instruction Count}_i}{\text{Instruction Count}}\ \text{( Frecuencia relativa)}$$

### Ejemplo de IPC

Un diseñador de compiladores tiene que decidir entre dos secuencias de código para un computador particular, usando instrucciones de las clases A, B y C. Se proporcionan los siguientes datos:

| Clase | A | B | C |
| --- | --- | --- | --- |
| CPI por clase | 1 | 2 | 3 |
| Inst. en secuencia 1 | 2 | 1 | 2 |
| Inst. en secuencia 2 | 4 | 1 | 1 |

¿Qué secuencia de código ejecuta más instrucciones? ¿Cuál es el CPI de cada secuencia? ¿Cuál es más rápida?

Secuencia 1: IC = 5. Secuencia 2: IC = 6.

$$\text{Ciclos de reloj}_1 = 2\times1 + 1\times2 + 2\times3 = 10 \qquad \text{Ciclos de reloj}_2 = 4\times1 + 1\times2 + 1\times3 = 9$$

Promedio CPI secuencia 1 = 10/5 = 2,0. Promedio CPI secuencia 2 = 9/6 = 1,5.

### Resumen de Rendimiento

$$\text{CPU Time} = \frac{\text{Instructions}}{\text{Program}} \times \frac{\text{Clock cycles}}{\text{Instruction}} \times \frac{\text{Seconds}}{\text{Clock cycle}}$$

El rendimiento depende de:
- Algoritmo: afecta IC, posiblemente CPI.
- Lenguaje de programación: afecta IC, CPI.
- Compilador: afecta IC, CPI.
- Arquitectura del conjunto de instrucciones: afecta a IC, CPI, T_c.

### Rendimiento global del computador: Benchmarks

- La única forma fiable es ejecutando distintos programas reales.
- Programas "de juguete": 10~100 líneas de código con resultado conocido. Ej.: Criba de Eratóstenes, Puzzle, Quicksort.
- Programas de prueba ( benchmarks) sintéticos: simulan la frecuencia de operaciones y operandos de un abanico de programas reales. Ej.: Whetstone, Dhrystone.
- Programas reales típicos con cargas de trabajo fijas ( actualmente la medida más aceptada): SPEC.
- Otros:
  - HPC: LINPACK, SPEChpc96, NAS Parallel Benchmark.
  - Servidores: SPECweb, SPECSFS ( File servers), TPC-C, SPECjbb ( Java).
  - Gráficos: SPECviewperf ( OpenGL), SPECapc ( aplicaciones 3D).
  - Winbench, EEMBC.

### SPEC CPU Benchmark

- Programas utilizados para medir el rendimiento, supuestamente típico de la carga de trabajo real.
- Corporación de Evaluación de Desempeño Estándar ( SPEC). Desarrolla puntos de referencia para CPU, E/S, Web, ...
- SPEC. CPU2006: tiempo transcurrido para ejecutar una selección de programas; E/S insignificante, por lo que se centra en el rendimiento de la CPU.
- Normalizar en relación con la máquina de referencia.
- Resumir como media geométrica de los índices de rendimiento: CINT2006 ( entero) y CFP2006 ( coma flotante).

$$\sqrt[n]{\prod_{i=1}^{n} \text{Execution time ratio}_i}$$

### CINT2006 para Intel Core i7 920

- https://browser.geekbench.com/
- https://www.spec.org/ ( El más serio, pagando)
- https://www.eembc.org/coremark/
- https://github.com/eembc/coremark
- Lista histórica: https://github.com/kreier/benchmark
- Para RISC-V: https://github.com/kreier/benchmark/tree/main/embench
- https://www.embench.org/

### SPECspeed 2017 Integer benchmarks on a 1.8 GHz Intel Xeon E5-2650L

## La Ley de Moore

Microelectrónica y microarquitectura.

- El escalado de la tecnología puede acabar en 10 años.
- El grosor del aislante de la puerta está limitado a 2nm.

Según INTEL ( Fuente: Intel Corporation).

### Rendimiento del monoprocesador

Limitado por potencia, paralelismo a nivel de instrucción, latencia de memoria.

### Tendencias de consumo

En tecnología CMOS IC:

$$\text{Power} = \text{Capacitive load} \times \text{Voltage}^2 \times \text{Frequency}$$

× 30 · 5V : 1V · × 1000

### Reduciendo consumo

Supongamos que una nueva CPU tiene el 85% de la carga capacitiva de la CPU antigua, con una reducción de 15% de voltaje y de 15% de frecuencia:

$$\frac{P_{new}}{P_{old}} = \frac{C_{old} \times 0.85 \times ( V_{old} \times 0.85)^2 \times ( F_{old} \times 0.85)}{C_{old} \times V_{old}^2 \times F_{old}} = 0.85^4 = 0.52$$

El muro del consumo:
- No podemos reducir más el voltaje.
- No podemos quitar más calor.
- ¿De qué otra manera podemos mejorar el rendimiento?

### Multiprocesadores

- Microprocesadores multinúcleo: más de un procesador por chip. Requiere programación paralela explícita.
- Comparar con el paralelismo de nivel de instrucción: el hardware ejecuta múltiples instrucciones a la vez, oculto del programador.
- Difícil de hacer: programación para el rendimiento, balanceo de carga, optimización de la comunicación y la sincronización.

### SPEC Power Benchmark

- Consumo de energía del servidor en diferentes niveles de carga de trabajo.
- Rendimiento: ssj_ops/seg. Potencia: vatios ( julios/seg).

$$\text{Overall ssj\_ops per Watt} = \frac{\sum_{i=0}^{10} ssj\_ops_i}{\sum_{i=0}^{10} power_i}$$

### SPECpower_ssj2008 para Xeon X5650

### Aceleración o Ganancia

- Mide el efecto de una mejora en un computador ( "A" o "G").
- Cociente entre tiempos de ejecución antes y después de la mejora de un mismo programa ( s). Adimensional.
- > 1 significa que hay mejora: T1/T2 es >1 si T2 < T1 ( T2 es menor: se redujo el tiempo de ejecución, hay ganancia).
- El programa/programas para medir se denomina "benchmark".

### Trampa: Ley de Amdahl I

Mejorar un aspecto de una computadora y esperar una mejora proporcional en el rendimiento general.

$$T_{improved} = \frac{T_{affected}}{\text{improvement factor}} + T_{unaffected}$$

Ejemplo: multiplicaciones suponen 80/100 del tiempo. ¿Cuánta mejora se necesita en multiplicaciones para un rendimiento 5 veces superior?

$$20 = \frac{80}{n} + 20 \quad \Rightarrow \quad \text{¡No se puede hacer!}$$

Corolario: hacer el caso común rápido.

### Ley de Amdahl II

Cuello de botella: subsistema o subsistemas que degradan el rendimiento general de la computadora. Mejorando el caso común, la ley de Amdahl mide el impacto en el desempeño del cambio en un subsistema.

Ley de Amdahl: A_m = factor de mejora introducido por el subsistema modificado; F_m = fracción de tiempo que el sistema completo utiliza el subsistema modificado.

Ejemplo: queremos mejorar el rendimiento de una computadora introduciendo un coprocesador matemático que realiza las operaciones en la mitad del tiempo. Calcular la ganancia en %velocidad de proceso del sistema para la ejecución de un programa si el 60% del mismo se dedica a operaciones aritméticas. Si el programa tarda 12 segundos en ejecutarse sin la actualización, ¿cuánto tardará con la mejora? A_m = 2 y F_m = 0,6.

Hacer que el sistema sea un 42% más rápido. Lo que hace que el programa tarde 8,45 segundos.

### Falacia: bajo consumo de energía en suspensión

- Referencia de potencia i7: al 100% de carga: 258W; al 50% de carga: 170W ( 66%); al 10% de carga: 121W ( 47%).
- Centro de datos de Google: funciona principalmente con una carga del 10% al 50%. Al 100% de carga menos del 1% del tiempo.
- Considere diseñar procesadores para que la potencia sea proporcional a la carga.

### Dificultad: MIPS como métrica de rendimiento

MIPS: millones de instrucciones por segundo. No cuenta para: diferencias en las ISA entre computadoras, diferencias en complejidad entre instrucciones.

$$MIPS = \frac{\text{Instruction count}}{\text{Execution time} \times 10^6} = \frac{\text{Clock rate}}{CPI \times 10^6} = \frac{\text{Instruction count} \times \text{Clock rate}}{\text{Instruction count} \times CPI \times 10^6}$$

El CPI varía entre los programas en una CPU determinada.

### Observaciones finales

- El costo/rendimiento está mejorando debido al desarrollo tecnológico subyacente.
- Capas jerárquicas de abstracción, tanto en hardware como en software.
- Conjunto de instrucciones - arquitectura: la interfaz hardware/software.
- Tiempo de ejecución: la mejor medida de rendimiento.
- El consumo es un factor limitante.
- Utilice el paralelismo para mejorar el rendimiento.

### Ejercicios para hacer

Más ejercicios y ejemplos. Trabajo Personal.

### Ecuaciones Rendimiento Resumen

- T = Tiempo de ejecución de un programa. T = Cy · Tc.
- Cy = Ciclos de reloj consumidos por el programa.
- Tc = Período del ciclo de reloj en segundos ( o ns). Tc = 1/f.
- f = frecuencia en Hertz ( Hz = ciclos/seg, MHz o GHz).
- Cy = I · CPI.
- I = Total de instrucciones ejecutadas ( recuento dinámico).
- CPI = Ciclos por Instrucción. Media de ciclos de reloj empleados ( mezcla particular).
- MIPS = 10⁻⁶ · I / T ( m.i.p.s.)

### Ejemplo 1

Se tiene la siguiente información sobre la mezcla de instrucciones pertenecientes a un repertorio de una máquina que ejecuta un programa Benchmark. Calcular CPI de dicha mezcla. Se debe obtener la media ponderada de 3 CPI:

| Tipo | Ciclos que consume | % uso |
| --- | --- | --- |
| Aritmética y lógica entera | 2 | 50 |
| Carga/Almacenamiento | 4 | 20 |
| Transferencia de control | 2 | 20 |
| Aritmética Coma Flotante | 8 | 10 |

Ejemplos:
```asm
add  R1,R2,R3        # R1 ← R2+R3
ld   R1, 16 ( R4)    # R1 ← M ( R4+16)
jnez R5, label1      # PC ← gets label1 ( address of next instruction)
addf F0,F5,F3        # F0 ← F5+F3, real numbers in FP representation
```

### Ejemplo 2

En un procesador de una frecuencia de 40 MHz. se ejecuta un benchmark con la mezcla de instrucciones y ciclos mostrada en la tabla a continuación. Calcular recuento de instrucciones, CPI, MIPS y Tiempo de ejecución.

| Tipo | Nº Instruc. | Ciclos |
| --- | --- | --- |
| Aritmética entera | 45.000 | 3 |
| Transferencia de datos | 32.000 | 2 |
| Coma Flotante | 15.000 | 10 |
| Transferencia de control | 8.000 | 2 |

Sol: I = 100.000; Cy = 365.000; CPI = 3,65; T ≈ 9ms; 10,95 MIPS

### Ejemplo 3

- Un programa benchmark en un procesador se ejecuta en 250 ms de los cuales, 200 ms se emplean en operaciones que manipulan números enteros.
- Se realiza un cambio en la circuitería de este procesador con el propósito de acelerar estas operaciones de enteros.
- Tras hacer estos cambios se comprueba que el mismo programa que se ejecutaba antes en 250 ms ahora tarda 210 ms.

¿Cuál es la Ganancia o Aceleración obtenida?

G = 250ms / 210ms = 1,19, o un 19% de aceleración.

### Ejemplo 3 ( continuación)

¿Cuánto se ha acelerado el procesamiento de enteros para obtener esta ganancia?

T1 = 250ms = 200ms + 50ms. T2 = 210ms = ?? + 50ms.

El tiempo de proceso de enteros (??) tras la mejora fue de 160ms. La aceleración parcial sobre los enteros es de 200ms/160ms = 1,25.

Conclusión: una aceleración de un 25% sobre los enteros permite que el benchmark se acelere un 19% ( G).
