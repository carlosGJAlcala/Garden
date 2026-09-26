---
title: "El procesador- microarquitectura"
---

# Capítulo 3

## El procesador: microarquitectura

### Temas

- Análisis de rendimiento
- Procesador de ciclo único
- Procesador multiciclo
- Procesador canalizado
- Microarquitectura avanzada

### Introducción

- Microarquitectura: cómo implementar una arquitectura en hardware.
- Procesador:
  - Ruta de datos: bloques funcionales.
  - Control: señales de control.

### Microarquitectura

Múltiples implementaciones para una única arquitectura:
- Ciclo único: cada instrucción se ejecuta en un solo ciclo.
- Multiciclo: cada instrucción se divide en una serie de pasos más cortos.
- Canalizado: cada instrucción dividida en una serie de pasos y múltiples instrucciones ejecutadas a la vez.

### Rendimiento del procesador

$$\text{Tiempo de ejecución} = (\#\text{instrucciones})(\text{ciclos/instrucción})(\text{segundos/ciclo})$$

Definiciones:
- CPI: ciclos/instrucción.
- Período de reloj: segundos/ciclo.
- IPC: instrucciones/ciclo = 1/CPI.

El desafío es satisfacer las restricciones de costo, potencia y rendimiento.

### Procesador RISC-V

Considerar un subconjunto de instrucciones RISC-V:
- Instrucciones de ALU tipo R: `add`, `sub`, `and`, `or`, `slt`.
- Instrucciones de memoria: `lw`, `sw`.
- Instrucciones de salto: `beq`.

### Elementos Arquitectónicos del Estado

Determina todo sobre un procesador — estado arquitectónico:
- 32 registros.
- PC.
- Memoria.

### Introducción

Factores de rendimiento de la CPU:
- Recuento de instrucciones: determinado por ISA y compilador.
- CPI y tiempo de ciclo: determinado por el hardware de la CPU.

Examinaremos dos implementaciones de RISC-V: una versión simplificada y una versión segmentada más realista. Subconjunto simple, muestra la mayoría de los aspectos:
- Referencia de memoria: `ld`, `sd`.
- Aritmético/lógico: `add`, `sub`, `and`, `or`.
- Transferencia de control: `beq`.

### Introducción

Ejecución de instrucciones:
- PC: memoria de instrucciones, búsqueda de instrucción.
- Números de registro: registrar archivo, leer registros.
- Dependiendo de la clase de instrucción:
  - Utilice ALU para calcular resultado aritmético, dirección de memoria para cargar/almacenar, o comparación para salto.
  - Acceder a la memoria de datos para cargar/almacenar.
  - PC ← dirección de destino o PC + 4.

### Descripción general de la CPU

*Diagrama de la diapositiva: esquema de bloques de alto nivel de la CPU ( ruta de datos + control). El layout no se pudo recuperar de la extracción OCR.*

### Multiplexores

No puedo simplemente unir los cables: usar multiplexores.

### Control

*Diagrama de la diapositiva: bloque de control conectado a la ruta de datos. El layout no se pudo recuperar de la extracción OCR.*

### Conceptos básicos de diseño lógico

- Información codificada en binario: bajo voltaje = 0, alto voltaje = 1. Un cable por bit; datos de varios bits codificados en buses de varios hilos.
- Elemento combinacional: opera con datos; la salida es una función de la entrada.
- Elementos de estado ( secuenciales): almacenan información.

### Elementos combinacionales

- Puerta AND: Y = A y B.
- Sumador: Y = A + B.
- Unidad aritmética/lógica: Y = F ( A, B).
- Multiplexor: Y = S ? I1 : I0.

*Diagrama de la diapositiva: símbolos de puerta AND, sumador, ALU y multiplexor con sus entradas ( A, B, S, I0, I1) y salida ( Y). El layout no se pudo recuperar de la extracción OCR.*

### Elementos secuenciales

Registro: almacena datos en un circuito. Utiliza una señal de reloj para determinar cuándo actualizar el valor almacenado. Activado por borde: actualización cuando Clk cambia de 0 a 1.

Registro con control de escritura: solo se actualiza en el flanco del reloj cuando la entrada de control de escritura es 1. Se usa cuando el valor almacenado se requiere más adelante ( forward).

*Diagrama de la diapositiva: símbolo de registro D con entradas D, Reloj ( y Escribir en la segunda versión) y salida Q. El layout no se pudo recuperar de la extracción OCR.*

### Metodología de sincronización

La lógica combinacional transforma los datos durante los ciclos de reloj, entre los flancos del reloj: entrada de elementos de estado, salida a elemento de estado. El retraso más largo determina el período del reloj.

### Creación de una ruta de datos

Ruta de datos: elementos que procesan datos y direcciones en la CPU ( registros, ALUs, muxes, memorias, …). Construiremos una ruta de datos RISC-V de forma incremental, refinando el diseño de la vista general.

### Obtención de instrucciones

*Diagrama de la diapositiva: etapa de búsqueda de instrucción — PC, memoria de instrucciones, e incremento de PC en 4 ( registro de instrucción de 64 bits) para obtener la siguiente instrucción. El layout no se pudo recuperar de la extracción OCR.*

### Instrucciones de formato R

Leer dos operandos de registro, realizar operaciones aritméticas/lógicas, escribir resultado de registro.

### Instrucciones de carga/almacenamiento

Leer operandos de registro; calcular la dirección utilizando el desplazamiento de 12 bits ( usar ALU, con desplazamiento de extensión de signo). Cargar: leer memoria y actualizar registro. Almacenar: escribir el valor del registro en la memoria.

### Instrucciones de salto condicional

Leer operandos de registro, comparar operandos ( usar ALU, restar y verificar la salida cero). Calcular dirección de destino: desplazamiento con extensión de signo, desplazado a la izquierda 1 lugar ( desplazamiento de media palabra), y sumado al valor del PC.

### Instrucciones de salto

Simplemente redirige los cables: cable de bit de signo replicado.

### Componer los elementos

La ruta de datos de primera generación hace una instrucción en un ciclo de reloj. Cada elemento de ruta de datos solo puede hacer una función a la vez; por lo tanto, necesitamos memorias separadas de instrucciones y datos. Use multiplexores donde se usen fuentes de datos alternativas para diferentes instrucciones.

### R-Type/Load/Store Datapath

*Diagrama de la diapositiva: ruta de datos para instrucciones tipo R, load y store. El layout no se pudo recuperar de la extracción OCR.*

### Ruta de datos completa

*Diagrama de la diapositiva: ruta de datos completa de ciclo único, incluyendo la lógica de salto ( beq). El layout no se pudo recuperar de la extracción OCR.*

### Control de ALU

ALU utilizada para:
- Cargar/Almacenar: F = agregar ( add).
- Salto condicional: F = restar ( subtract).
- Tipo R: F depende del código de operación.

| Control ALU | Función |
| --- | --- |
| 0000 | AND |
| 0001 | OR |
| 0010 | Agregar ( add) |
| 0110 | Sustraer ( subtract) |

### Control de ALU ( derivación)

Suponga que ALUOp de 2 bits se deriva del código de operación; la lógica combinacional deriva el control de la ALU:

| Código de operación | ALUOp | Operación | Campo de código de función | Función ALU | Control ALU |
| --- | --- | --- | --- | --- | --- |
| ld | 00 | load register | XXXXXXXXXXX | add | 0010 |
| sd | 00 | store register | XXXXXXXXXXX | add | 0010 |
| beq | 01 | branch on equal | XXXXXXXXXXX | subtract | 0110 |
| R-type | 10 | add | 100000 | add | 0010 |
| R-type | 10 | subtract | 100010 | subtract | 0110 |
| R-type | 10 | and | 100100 | and | 0000 |
| R-type | 10 | or | 100101 | or | 0001 |

### La unidad de control principal

Señales de control derivadas de la instrucción.

*Diagrama de la diapositiva: unidad de control principal, sus entradas ( campos de la instrucción) y señales de control de salida. El layout no se pudo recuperar de la extracción OCR.*

### Ruta de datos con control

*Diagrama de la diapositiva: ruta de datos completa con las señales de control superpuestas. El layout no se pudo recuperar de la extracción OCR.*

### Instrucción tipo R

*Diagrama de la diapositiva: ruta activa de la ruta de datos durante la ejecución de una instrucción tipo R. El layout no se pudo recuperar de la extracción OCR.*

### Instrucción de carga

*Diagrama de la diapositiva: ruta activa de la ruta de datos durante la ejecución de una instrucción de carga ( lw). El layout no se pudo recuperar de la extracción OCR.*

### Instrucción de bifurcación en igualdad

*Diagrama de la diapositiva: ruta activa de la ruta de datos durante la ejecución de una instrucción beq. El layout no se pudo recuperar de la extracción OCR.*

### Problemas de rendimiento

El retraso más largo determina el período del reloj. Camino crítico: instrucción de carga — memoria de instrucciones → banco de registros → ALU → memoria de datos → banco de registros. No es factible variar el período para diferentes instrucciones: viola el principio de diseño de hacer el caso común rápido. Mejoraremos el rendimiento canalizando ( pipeline).

## Procesador de ciclo único

### Rendimiento

$$\text{Tiempo de ejecución del programa} = (\#\text{instrucciones}) \times CPI \times T_c$$

### Rendimiento del procesador de ciclo único

*Diagrama de la diapositiva: ruta de datos completa de ciclo único con las señales de control ( PCSrc, ResultSrc, MemWrite, ALUControl, ALUSrc, ImmSrc, RegWrite, etc.) y los bloques PC, memoria de instrucciones, banco de registros, ALU, memoria de datos y unidad de extensión de signo. El layout no se pudo recuperar de la extracción OCR.*

Camino crítico de un solo ciclo:

$$T_{c\_single} = t_{pcq\_PC} + t_{mem} + \max[t_{RFread}, t_{dec} + t_{ext} + t_{mux}] + t_{ALU} + t_{mem} + t_{mux} + t_{RFsetup}$$

Por lo general, las rutas limitantes son: memoria, ALU, archivo de registro. Entonces:

$$T_{c\_single} = t_{pcq\_PC} + t_{mem} + t_{RFread} + t_{ALU} + t_{mem} + t_{mux} + t_{RFsetup} = t_{pcq\_PC} + 2t_{mem} + t_{RFread} + t_{ALU} + t_{mux} + t_{RFsetup}$$

### Ejemplo de rendimiento de ciclo único

| Elemento | Parámetro | Retraso ( ps) |
| --- | --- | --- |
| Register clock-to-Q | t_pcq_PC | 40 |
| Register setup | t_setup | 50 |
| Multiplexer | t_mux | 30 |
| AND-OR gate | t_and-or | 20 |
| ALU | t_ALU | 120 |
| Decoder ( Control Unit) | t_dec | 25 |
| Extend unit | t_ext | 35 |
| Memory read | t_mem | 200 |
| Register file read | t_RFread | 100 |
| Register file setup | t_RFsetup | 60 |

$$T_{c\_single} = t_{pcq\_PC} + 2t_{mem} + t_{RFread} + t_{ALU} + t_{mux} + t_{RFsetup} = 40 + 2(200) + 100 + 120 + 30 + 60 = 750\ ps$$

### Ejemplo de rendimiento de ciclo único ( continuación)

Programa con 100 mil millones de instrucciones:

$$\text{Tiempo de ejecución} = \#\text{instrucciones} \times CPI \times T_c = (100 \times 10^9)(1)(750 \times 10^{-12}s) = 75\ \text{segundos}$$

## Procesador multiciclo

### Rendimiento del procesador multiciclo

Las instrucciones toman diferente número de ciclos:
- 3 ciclos: `beq`.
- 4 ciclos: tipo R, `addi`, `sw`, `jal`.
- 5 ciclos: `lw`.

El IPC es el promedio ponderado. Punto de referencia SPECINT2000: 25% cargas, 10% almacenamiento, 13% saltos, 52% tipo R.

$$CPI_{medio} = (0{,}13)(3) + (0{,}52 + 0{,}10)(4) + (0{,}25)(5) = 4{,}12$$

### Camino crítico multiciclo

*Diagrama de la diapositiva: ruta de datos multiciclo con registros intermedios ( OldPC, ALUOut, etc.) y señales de control ( AdrSrc, MemWrite, IRWrite, ResultSrc, ALUControl, ALUSrcA/B, RegWrite, etc.). El layout no se pudo recuperar de la extracción OCR.*

Rutas críticas potenciales: calcular PC+4, leer memoria.

Suposiciones: el banco de registros es más rápido que la memoria; la memoria de escritura es más rápida que la de lectura.

$$T_{c\_multi} = t_{pcq} + t_{dec} + 2t_{mux} + \max(t_{ALU}, t_{memoria}) + t_{setup}$$

### Ejemplo de rendimiento multiciclo

| Elemento | Parámetro | Retraso ( ps) |
| --- | --- | --- |
| Register clock-to-Q | t_pcq_PC | 40 |
| Register setup | t_setup | 50 |
| Multiplexer | t_mux | 30 |
| AND-OR gate | t_and-or | 20 |
| ALU | t_ALU | 120 |
| Decoder ( Control Unit) | t_dec | 25 |
| Extend unit | t_ext | 35 |
| Memory read | t_mem | 200 |
| Register file read | t_RFread | 100 |
| Register file setup | t_RFsetup | 60 |

$$T_{c\_multi} = t_{pcq} + t_{dec} + 2t_{mux} + \max(t_{ALU}, t_{memoria}) + t_{setup} = 40 + 25 + 2(30) + \max(120,200) + 60 = 375\ ps$$

### Ejemplo de rendimiento multiciclo ( continuación)

Para un programa con 100 mil millones de instrucciones ejecutándose en un procesador RISC-V multiciclo:
- CPI = 4,12 ciclos/instrucción.
- Tiempo de ciclo de reloj: T_c_multi = 375 ps.

$$\text{Tiempo de ejecución} = (\#\text{instrucciones}) \times CPI \times T_c = (100 \times 10^9)(4.12)(375 \times 10^{-12}) = 155\ \text{segundos}$$

Esto es más lento que el procesador de ciclo único ( 75 seg.)

## Procesador canalizado

### Analogía de canalización

Lavandería canalizada: ejecución superpuesta. El paralelismo mejora el rendimiento.

- Cuatro cargas: aceleración = 8/3,5 = 2,3.
- Sin escalas: aceleración = 2n/( 0,5n + 1,5) ≈ 4 ( n = número de etapas).

### Tubería ( pipeline) RISC-V

Cinco etapas, un paso por etapa:
- **IF**: instrucción recuperada de la memoria.
- **ID**: decodificación de instrucción y lectura de registro.
- **EX**: ejecutar operación o calcular dirección.
- **MEM**: acceso a operando de memoria.
- **WB**: escribir el resultado de nuevo en el registro.

### Estimación rendimiento del cauce ( pipeline)

Suponga que el tiempo para las etapas es 100ps para registro de lectura o escritura y 200ps para otras etapas. Compare la ruta de datos canalizada con la ruta de datos de ciclo único:

| Instr | Instr fetch | Register read | ALU op | Memory access | Register write | Tiempo Total |
| --- | --- | --- | --- | --- | --- | --- |
| ld | 200ps | 100ps | 200ps | 200ps | 100ps | 800ps |
| sd | 200ps | 100ps | 200ps | 200ps | | 700ps |
| R-format | 200ps | 100ps | 200ps | | 100ps | 600ps |
| beq | 200ps | 100ps | 200ps | | | 500ps |

### Desempeño del pipeline

Ciclo único ( Tc = 800ps) frente a canalizado ( Tc = 200ps).

### Aceleración del cauce

Si todas las etapas están equilibradas ( es decir, todas toman el mismo tiempo):

$$\frac{\text{Tiempo entre instrucciones canalizadas}}{\text{Tiempo entre instrucciones no canalizadas}} = \text{Número de etapas}$$

Si no está equilibrado, la aceleración es menor. La aceleración se debe al aumento del rendimiento; la latencia ( tiempo para cada instrucción) no disminuye.

### Segmentación y Diseño ISA

RISC-V ISA diseñado para usar pipeline:
- Todas las instrucciones son de 32 bits: más fácil de obtener y decodificar en un ciclo ( cf. x86: instrucciones de 1 a 17 bytes).
- Formatos de instrucción pocos y regulares: puede decodificar y leer registros en un solo paso.
- Direccionamiento de carga/almacenamiento: puede calcular la dirección en la 3ª etapa, acceder a la memoria en la 4ª etapa.

### Peligros ( Hazards)

Situaciones que impiden iniciar la siguiente instrucción en el siguiente ciclo:
- **Peligros estructurales**: un recurso requerido está ocupado.
- **Riesgo de datos**: debe esperar a que la instrucción anterior complete su lectura/escritura de datos.
- **Peligro de control**: decidir sobre la acción de control depende de la instrucción previa.

### Riesgos estructurales

Conflicto por el uso de un recurso: en tubería RISC-V con una sola memoria, cargar/almacenar requiere acceso a datos y la búsqueda de instrucciones tendría que detenerse para ese ciclo, causando una "burbuja" de tubería. Por lo tanto, las rutas de datos segmentadas requieren memorias de instrucciones/datos separadas ( o cachés separadas).

### Riesgos de datos

Una instrucción depende de la finalización del acceso a los datos por una instrucción anterior:

```asm
add x19, x0, x1
sub x2, x19, x3
```

### Reenvío ( Forwarding) o derivación ( Bypassing)

Usar el resultado cuando se calcula; no esperar a que se almacene en un registro. Requiere conexiones adicionales en la ruta de datos.

### Peligro de datos en la carga de memoria

No siempre se pueden evitar las paradas mediante el reenvío: si el valor no se calcula cuando es necesario, ¡no se puede avanzar hacia atrás en el tiempo!

### Reordenación de código para evitar paradas

Reordenar el código para evitar el uso del resultado de carga en la siguiente instrucción. Código C: `a = b + e; c = b + f;`

Código original ( 13 ciclos, con paradas):
```asm
ld   x1, 0 ( x0)
ld   x2, 8 ( x0)
suma x3, x1, x2
parada
SD   x3, 24 ( x0)
ld   x4, 16 ( x0)
suma x5, x1, x4
parada
SD   x5, 32 ( x0)
```

Código reordenado ( 11 ciclos, sin paradas):
```asm
ld   x1, 0 ( x0)
ld   x2, 8 ( x0)
ld   x4, 16 ( x0)
suma x3, x1, x2
SD   x3, 24 ( x0)
suma x5, x1, x4
SD   x5, 32 ( x0)
```

### Peligros de control ( saltos)

El salto determina el flujo de control: obtener la siguiente instrucción depende del resultado de la condición de salto. El pipeline no siempre puede obtener la instrucción correcta, ya que todavía se está trabajando en la etapa de identificación del salto. En pipeline RISC-V: necesidad de comparar registros y calcular el objetivo al principio del cauce; se agrega hardware para hacerlo en la etapa de ID.

### Parada ( Burbuja o Stall) en salto

Espere hasta que se determine el resultado de la condición de salto antes de obtener la siguiente instrucción.

### Predicción de salto

Los pipelines más largos no pueden determinar fácilmente el resultado del salto de manera temprana; la penalización de parada se vuelve inaceptable. Predecir el resultado del salto: solo se detiene si la predicción es incorrecta. En el pipeline RISC-V se puede predecir saltos no tomados, obteniendo instrucciones después del salto sin demora.

### Predicción de saltos más realista

- Predicción estática de salto: basada en el comportamiento típico de un salto ( ejemplo: saltos en bucle y sentencia if). Predecir los saltos hacia atrás tomados; predecir saltos hacia delante no tomados.
- Predicción de salto dinámica: el hardware mide el comportamiento real de los saltos ( por ejemplo, registrar el historial reciente de cada salto), suponiendo que el comportamiento futuro continuará la tendencia. Cuando se equivoque, deténgase mientras vuelve a buscar y actualice el historial.

### Resumen de canalización

El pipeline mejora las prestaciones al aumentar el rendimiento en las instrucciones: ejecuta varias instrucciones en paralelo, aunque cada instrucción tiene la misma latencia. Sujeto a peligros ( estructura, datos, control). El diseño del conjunto de instrucciones afecta la complejidad de la implementación de la canalización.

### Ruta de datos canalizada de RISC-V

*Diagrama de la diapositiva: ruta de datos segmentada en 5 etapas ( IF/ID/EX/MEM/WB); el flujo de derecha a izquierda ( de MEM/WB de vuelta al banco de registros) genera los peligros. El layout no se pudo recuperar de la extracción OCR.*

### Registros del pipeline

Necesita registros entre etapas para guardar la información producida en el ciclo anterior.

### Operación de pipeline

Flujo de instrucciones ciclo a ciclo a través de la ruta de datos segmentada:
- Diagrama de pipeline de "ciclo de reloj único": muestra el uso de canalización en un solo ciclo, destacando los recursos utilizados.
- Diagrama de "ciclo de reloj múltiple": gráfico de funcionamiento en el tiempo.

Veremos los diagramas de "ciclo de reloj único" para cargar y almacenar.

### Ejecución de carga y almacenamiento, etapa por etapa

*Diagramas de la diapositiva ( 8 láminas consecutivas): la ruta de datos segmentada con la etapa activa resaltada en cada ciclo — IF, ID, EX, MEM y WB para una instrucción de carga ( lw), y EX, MEM y WB para una instrucción de almacenamiento ( sw). Una de las láminas señala un "número de registro erróneo" y presenta la ruta de datos corregida para la carga. El layout de estos diagramas no se pudo recuperar de la extracción OCR.*

### Diagrama de tubería de ciclo múltiple ( uso de recursos)

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Diagrama de tubería de ciclo múltiple ( forma tradicional)

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Diagrama de pipeline de ciclo único

Estado de la tubería en un ciclo dado.

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Control canalizado ( simplificado)

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Control canalizado

Señales de control derivadas de la instrucción, como en la implementación de ciclo único.

*Diagrama de la diapositiva ( control completo). El layout no se pudo recuperar de la extracción OCR.*

### Riesgos de datos en las instrucciones ALU

Considere esta secuencia:

```asm
sub x2, x1, x3
and x12, x2, x5
or  x13, x6, x2
add x14, x2, x2
sd  x15, 100 ( x2)
```

Podemos resolver los peligros con el reenvío. ¿Cómo detectamos cuándo reenviar?

### Dependencias y reenvío ( forwarding)

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Detección de la necesidad de reenviar

Pasar números de registro a lo largo de la tubería, por ejemplo, ID/EX.RegisterRs1 = número de registro para Rs1 que se encuentra en el registro de tubería ID/EX. Los números de registro de operandos ALU en la etapa EX están dados por ID/EX.RegistroRs1, ID/EX.RegistroRs2.

Riesgos de datos cuando:
1. a. EX/MEM.RegistroRd = ID/EX.RegistroRs1 → reenviar desde registro de canalización.
   b. EX/MEM.RegistroRd = ID/EX.RegistroRs2 → reenviar desde registro de canalización.
2. a. MEM/WB.RegistroRd = ID/EX.RegistroRs1 → reenviar desde registro de canalización.
   b. MEM/WB.RegistroRd = ID/EX.RegistroRs2 → reenviar desde registro de canalización.

### Detección de la necesidad de reenviar ( continuación)

¡Pero solo si la instrucción de reenvío escribirá en un registro! ( EX/MEM.RegWrite, MEM/WB.RegWrite). Y solo si Rd para esa instrucción no es x0 ( EX/MEM.RegisterRd ≠ 0, MEM/WB.RegisterRd ≠ 0).

### Rutas de reenvío

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Condiciones de reenvío

| control mux | Fuente | Explicación |
| --- | --- | --- |
| ForwardA = 00 | ID/EX | El primer operando ALU proviene del archivo de registro. |
| ForwardA = 10 | EX/MEM | El primer operando de ALU se reenvía desde el resultado de ALU anterior. |
| ForwardA = 01 | MEM/WB | El primer operando de ALU se reenvía desde la memoria de datos o desde un resultado de ALU anterior. |
| ForwardB = 00 | ID/EX | El segundo operando ALU proviene del archivo de registro. |
| ForwardB = 10 | EX/MEM | El segundo operando de ALU se reenvía desde el resultado de ALU anterior. |
| ForwardB = 01 | MEM/WB | El segundo operando de ALU se reenvía desde la memoria de datos o desde un resultado de ALU anterior. |

### Riesgo de datos dobles

Considere la secuencia:

```asm
add x1, x1, x2
add x1, x1, x3
add x1, x1, x4
```

Ambos peligros ocurren; se quiere usar el más reciente. Revisar la condición de peligro del MEM; reenviar solo si la condición de peligro EX no es verdadera.

### Condición de reenvío revisada

Peligro MEM:

```
if ( MEM/WB.RegWrite
     and ( MEM/WB.RegistroRd ≠ 0)
     and not ( EX/MEM.RegWrite and ( EX/MEM.RegisterRd ≠ 0)
               and ( EX/MEM.RegistroRd ≠ ID/EX.RegistroRs1))
     and ( MEM/WB.RegisterRd = ID/EX.RegisterRs1)) ForwardA = 01

if ( MEM/WB.RegWrite
     and ( MEM/WB.RegistroRd ≠ 0)
     and not ( EX/MEM.RegWrite and ( EX/MEM.RegisterRd ≠ 0)
               and ( EX/MEM.RegistroRd ≠ ID/EX.RegistroRs2))
     and ( MEM/WB.RegisterRd = ID/EX.RegisterRs2)) ForwardB = 01
```

### Detección de riesgos de carga

Compruebe cuándo se decodifica la instrucción en la etapa de ID. Los números de registro de operandos ALU en la etapa ID están dados por IF/ID.RegistroRs1, IF/ID.RegistroRs2.

Peligro de uso de la carga cuando:

```
ID/EX.MemRead and
(( ID/EX.RegisterRd = IF/ID.RegisterRs1) or
 ( ID/EX.RegisterRd = IF/ID.RegisterRs2))
```

Si se detecta, detener e insertar la burbuja.

### Cómo detener el pipeline

- Forzar los valores de control en el registro ID/EX a 0: un nop ( sin operación) pasará por EX, MEM y WB.
- Impedir la actualización de PC y registro IF/ID: la instrucción de uso se decodifica de nuevo, y la siguiente instrucción se obtiene de nuevo.
- La parada de 1 ciclo sí permite que MEM lea datos con `ld`; puede pasar posteriormente a la etapa EX.

### Peligro de datos de uso de carga

Parada insertada aquí.

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Ruta de datos con detección de peligros

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Paradas y rendimiento

Las paradas reducen el rendimiento, pero son necesarias para obtener resultados correctos. El compilador puede organizar el código para evitar peligros y paradas; requiere conocimiento de la estructura del pipeline.

### Riesgos en saltos en el procesador canalizado

Controlar los hazard en saltos ( `beq`):
- Salto no determinado hasta la etapa de ejecución de la canalización.
- Instrucciones después del salto obtenidas antes de que ocurra el salto.
- Varias ( 2) instrucciones deben vaciarse si ocurre el salto.

### Controlar los peligros

*Diagrama de la diapositiva: cronograma de pipeline mostrando el vaciado ( flush) de 2 instrucciones tras una bifurcación tomada — instrucciones `beq s1, s2, L1` ( dirección 20), `sub s8, t1, s3` ( 24), `or s9, t6, s5` ( 28) y `L1: add s7, s3, s4` ( 58) a lo largo de 10 ciclos de reloj, con las etapas IF/ID/EX/MEM/WB de las dos instrucciones tras el salto vaciadas. El layout exacto no se pudo recuperar de la extracción OCR.*

Penalización por error de predicción de salto: el número de instrucciones vaciadas cuando se toma un salto ( en este caso, 2 instrucciones).

### Riesgos de control: Lógica de vaciado ( flush)

Si se toma un salto en la etapa de ejecución, es necesario vaciar las instrucciones en las etapas Fetch y Decode. Haga esto borrando los registros Decode y Execute Pipeline usando FlushD y FlushE.

Ecuaciones:
```
FlushD = PCSrcE
FlushE = lwStall OR PCSrcE
```

### Riesgos de control: hardware de vaciado

*Diagrama de la diapositiva: ruta de datos segmentada completa con la unidad de riesgos ( Hazard Unit) y las señales FlushD/FlushE/StallD/StallF. El layout no se pudo recuperar de la extracción OCR.*

### Procesador canalizado RISC-V con unidad de riesgo

*Diagrama de la diapositiva: versión completa de la ruta de datos segmentada con la unidad de riesgos ( Hazard Unit), reenvío y detección de peligros de carga integrados. El layout no se pudo recuperar de la extracción OCR.*

### Riesgos por salto ( otra versión)

Si el destino del salto se determina en MEM: vaciar estas instrucciones ( establecer los valores de control en 0).

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Reduciendo el retraso por salto

Mueva el hardware para determinar el resultado a la etapa de identificación: sumador de direcciones de destino, comparador de registros.

Ejemplo: rama tomada.

```asm
36: sub x10, x4, x8
40: beq x1, x3, 16   // bifurcación relativa a PC, a 40+16*2=72
44: and x12, x2, x5
48: orr x13, x2, x6
52: suma x14, x4, x2
56: sub x15, x6, x7
72: ld x4, 50 ( x7)
```

### Ejemplo: salto tomado

*Diagrama de la diapositiva ( 2 láminas): cronograma del pipeline mostrando la resolución del salto en la etapa ID. El layout no se pudo recuperar de la extracción OCR.*

### Riesgos de datos para saltos

Si un registro de comparación es un destino de la 2ª o 3ª instrucción ALU anterior, puede resolverse mediante reenvío.

*Diagrama de la diapositiva: cronograma de pipeline ( `add x1,x2,x3`, `add x4,x5,x6`, …, `beq x1,x4,target`) mostrando las etapas IF/ID/EX/MEM/WB de cada instrucción a lo largo del tiempo. El layout no se pudo recuperar de la extracción OCR.*

### Peligros de datos para saltos ( uso tras carga, 2ª anterior)

Si un registro de comparación es un destino de la instrucción ALU anterior o de la 2ª instrucción de carga anterior, necesita 1 ciclo de parada.

*Diagrama de la diapositiva: cronograma de pipeline ( `lw x1,addr`, `add x4,x5,x6`, `beq` parado, `beq x1,x4,target`) mostrando la parada de 1 ciclo. El layout no se pudo recuperar de la extracción OCR.*

### Peligros de datos para saltos ( uso tras carga, inmediatamente anterior)

Si un registro de comparación es un destino de la instrucción de carga inmediatamente anterior, necesita 2 ciclos de parada.

*Diagrama de la diapositiva: cronograma de pipeline ( `lw x1,addr`, `beq` parado dos veces, `beq x1,x0,target`) mostrando las dos paradas. El layout no se pudo recuperar de la extracción OCR.*

### Rendimiento canalizado

Ejemplo de rendimiento del procesador canalizado. Punto de referencia SPECINT2000: 25% cargas, 10% saltos, 13% saltos condicionales, 52% tipo R.

Suponer: 40% de las cargas ( load) usadas por la siguiente instrucción; 50% de los saltos mal predichos ( lo ideal es 1, pero…). ¿Cuál es el IPC promedio?

- Carga: CPI = 1 cuando no se detiene, 2 cuando se detiene. Entonces, CPI_lw = 1( 0,6) + 2( 0,4) = 1,4.
- Salto condicional: CPI = 1 cuando no se detiene, 3 cuando se detiene. Entonces, CPI_beq = 1( 0,5) + 3( 0,5) = 2.

$$CPI_{medio} = (0{,}25)(1{,}4) + (0{,}1)(1) + (0{,}13)(2) + (0{,}52)(1) = 1{,}23$$

### Ejemplo de rendimiento del procesador canalizado ( ruta crítica)

Ruta crítica del procesador canalizado:

$$T_{c\_canalizado} = \max\begin{cases} t_{pcq} + t_{memoria} + t_{configuración} & \text{Buscar} \\ 2(t_{RFleer} + t_{configurar}) & \text{Descodificar} \\ t_{pcq} + 4t_{mux} + t_{ALU} + t_{AND\text{-}OR} + t_{configuración} & \text{Ejecutar} \\ t_{pcq} + t_{memoria} + t_{configuración} & \text{Memoria} \\ 2(t_{pcq} + t_{mux} + t_{RFescritura}) & \text{Write Back} \end{cases}$$

Las etapas de decodificación y reescritura utilizan el archivo de registro en cada ciclo, entonces cada etapa obtiene la mitad del tiempo del ciclo ( T_c/2) para hacer su trabajo. O, dicho de otra manera, 2x de su trabajo debe caber en un ciclo ( T_c).

### Ruta crítica segmentada: caso de salto que requiere forwarding

*Diagrama de la diapositiva: ruta de datos segmentada con la unidad de riesgos, mostrando la ruta crítica para la resolución de un salto que necesita reenvío en la etapa de ejecución. El layout no se pudo recuperar de la extracción OCR.*

### Ejemplo de rendimiento canalizado

| Element | Parameter | Delay ( ps) |
| --- | --- | --- |
| Register clock-to-Q | t_pcq_PC | 40 |
| Register setup | t_setup | 50 |
| Multiplexer | t_mux | 30 |
| AND-OR gate | t_and-or | 20 |
| ALU | t_ALU | 120 |
| Decoder ( Control Unit) | t_dec | 25 |
| Extend unit | t_ext | 35 |
| Memory read | t_mem | 200 |
| Register file read | t_RFread | 100 |
| Register file setup | t_RFsetup | 60 |

$$T_{c\_canalizado} = t_{pcq} + 4t_{mux} + t_{ALU} + t_{AND\text{-}OR} + t_{configuración} = 40 + 4(30) + 120 + 20 + 50 = 350\ ps$$

### Ejemplo de rendimiento canalizado ( continuación)

Programa con 100 mil millones de instrucciones:

$$\text{Tiempo de ejecución} = (\#\text{instrucciones}) \times CPI \times T_c = (100 \times 10^9)(1.23)(350 \times 10^{-12}) = 43\ \text{segundos}$$

### Comparación de rendimiento del procesador

| Procesador | Tiempo de ejecución ( segundos) | Aceleración ( ciclo único como línea de base) |
| --- | --- | --- |
| Ciclo único | 75 | 1 |
| Multiciclo | 155 | 0,5 |
| Canalizado | 43 | 1,7 |

### Observaciones finales

- ISA influye en el diseño de la ruta de datos y el control; el diseño influye en el control y ruta de datos de la ISA.
- La canalización mejora el rendimiento de las instrucciones mediante el paralelismo: más instrucciones completadas por segundo, aunque la latencia para cada instrucción no se reduce.
- Peligros: estructurales, datos, control. Las dependencias limitan el paralelismo alcanzable.
