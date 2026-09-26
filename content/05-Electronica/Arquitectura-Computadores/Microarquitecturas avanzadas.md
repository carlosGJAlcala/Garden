---
title: "Microarquitecturas avanzadas"
---

# Micro/Arquitecturas Avanzadas

*Bibliografía: basado en los temas 4 y 6 de "Computer Organization and Design. RISC-V Edition", David A. Patterson, John Hennessy. 2nd Edition, Morgan-Kaufman 2021.*

## Predicción de bifurcación dinámica

En pipelines más profundos y superescalares, la penalización por salto es más significativa. Usar predicción dinámica:
- Búfer de predicción de bifurcación ( salto condicional), también conocido como tabla de historial de saltos.
- Indexado por direcciones de instrucciones de bifurcación recientes.
- Almacena el resultado ( tomado/no tomado).

Para ejecutar una bifurcación: verifique la tabla, espere el mismo resultado, comience a buscar desde la predicción. Si es incorrecto, vacíe el pipeline y cambie la predicción.

### Predictor de 1 bit: deficiencia

¡Las ramas del bucle interno se predijeron mal dos veces!

```
exterior: …
  interior: …
    beq …, …, interior
  …
beq …, …, exterior
```

Predicción errónea tomada en la última iteración del bucle interno. Luego predice erróneamente como no tomado en la primera iteración del ciclo interno la próxima vez.

### Predictor de 2 bits

Solo cambia la predicción tras dos predicciones erróneas sucesivas.

### Cálculo del destino del salto

Incluso con el predictor, aún es necesario calcular la dirección de destino ( penalización de 1 ciclo por un salto tomado).

- Búfer de destino de bifurcación: caché de direcciones de destino.
- Indexado por PC cuando se obtiene la instrucción.
- Si la condición y la instrucción se predicen, se puede buscar el objetivo inmediatamente.

## Excepciones e interrupciones

Eventos "inesperados" que requieren un cambio en el flujo de control. Diferentes ISA usan los términos de manera diferente:
- **Excepción**: surge dentro de la CPU ( por ejemplo, código de operación indefinido, llamada al sistema).
- **Interrupción**: desde un controlador de E/S externo.

Tratar con ellos sin sacrificar el rendimiento es difícil.

### Manejo de excepciones

- Guarde el PC de la instrucción infractora ( o interrumpida). En RISC-V: contador de programa de excepción de supervisor ( SEPC).
- Guardar indicación del problema. En RISC-V: registro de causa de excepción del supervisor ( SCAUSE). 64 bits, pero la mayoría de los bits no se utilizan. Campo de código de excepción: 2 para código de operación indefinido, 12 para mal funcionamiento del hardware, …
- Saltar al controlador: asumir en 0000 0000 1C09 0000 hexadecimal.

### Un mecanismo alternativo

Interrupciones vectorizadas: dirección del controlador determinada por la causa. Dirección de vector de excepción que se sumará a un registro base de tabla de vectores:
- Código de operación indefinido: 00 0100 0000.
- Mal funcionamiento del hardware: 01 1000 0000.
- …

Instrucciones ya sea para tratar con la interrupción, o saltar al controlador real.

### Acciones del controlador

Lea la causa y transfiérala al responsable del tratamiento; determinar la acción requerida.
- Si es reiniciable: tomar acción correctiva, utilice SEPC para volver al programa.
- De lo contrario: terminar programa, informe de error usando SEPC, SCAUSE, …

### Excepciones en una canalización

Otra forma de "hazard" de control. Considere un mal funcionamiento cuando se va a sumar en la etapa EX:

```asm
add x1, x2, x1
```

- Evita que x1 sea mal modificado.
- Completar instrucciones anteriores.
- Flush add e instrucciones posteriores.
- Establecer valores de registro SEPC y SCAUSE.
- Transferir el control al controlador.

Similar a salto mal predicho: usar gran parte del mismo hardware.

### Pipeline con excepciones ( y final)

*Diagrama de la diapositiva: ruta de datos segmentada con la lógica añadida para excepciones ( Exception Cause y Supervisor Exception PC) junto con la ya añadida para el salto. El layout no se pudo recuperar de la extracción OCR.*

### Propiedades de excepción

Excepciones reiniciables: el pipeline puede vaciar la instrucción; el controlador se ejecuta, luego vuelve a la instrucción, que se recupera y ejecuta desde cero. El PC se guarda en el registro SEPC, que identifica la instrucción causante.

### Ejemplo de excepción

Excepción en `add` en la dirección 4c:

```asm
40: sub x11, x2, x4
44: and x12, x2, x5
48: orr x13, x2, x6
4c: add x1, x2, x1
50: sub x15, x6, x7
54: ld  x16, 100 ( x7)
…
Handler:
1c090000: sd x26, 1000 ( x10)
1c090004: sd x27, 1008 ( x10)
…
```

*Diagramas de la diapositiva ( 2 láminas adicionales): cronograma del pipeline mostrando la detección de la excepción y el salto al manejador. El layout no se pudo recuperar de la extracción OCR.*

### Múltiples Excepciones

La canalización se superpone a varias instrucciones: podría tener múltiples excepciones a la vez.
- Enfoque simple: tratar la excepción desde la instrucción más temprana, vaciar las instrucciones subsiguientes ( excepciones "precisas").
- En pipelines complejos, con múltiples instrucciones emitidas por ciclo y finalización fuera de orden, ¡mantener excepciones precisas es difícil!

### Excepciones imprecisas

Simplemente detenga el pipeline y guarde el estado. Incluya causa( s) de excepción; deja que el manejador trabaje qué instrucción( es) tenían excepciones y cuál completar o hacer "flush" ( puede requerir una finalización "manual"). Simplifica el hardware, pero el software del controlador es más complejo. No es factible para pipelines complejas con lanzamiento múltiple y fuera de orden.

## Paralelismo a nivel de instrucción ( ILP)

Canalización ( pipeline): ejecutar múltiples instrucciones en paralelo. Para aumentar más con ILP ( dos formas):
- Canalización más profunda ( más etapas): menos trabajo por etapa ⇒ ciclo de reloj más corto.
- Lanzamiento múltiple ( repetir etapas en paralelo): replicar etapas de canalización ⇒ múltiples canalizaciones, iniciar múltiples instrucciones por ciclo de reloj.

CPI < 1, así que use Instrucciones por Ciclo ( IPC). Por ejemplo, 4 GHz de 4 vías de emisión múltiple: 16 BIPS, CPI pico = 0,25, IPC pico = 4. Pero las dependencias reducen esto en la práctica.

### Lanzamiento múltiple ( VLIW?)

- Lanzamiento múltiple estático ( "multiple issue"): el compilador agrupa las instrucciones que se emitirán juntas, empaquetándolas en "ranuras de emisión". El compilador detecta y evita peligros ( "hazards").
- Lanzamiento múltiple dinámico: la CPU examina el flujo de instrucciones y elige las instrucciones para emitir cada ciclo. El compilador puede ayudar reordenando las instrucciones. La CPU resuelve los peligros utilizando técnicas avanzadas en tiempo de ejecución.

### Lanzamiento múltiple ( SweRV EH1)

*Diagrama de la diapositiva: microarquitectura del núcleo SweRV EH1. El layout no se pudo recuperar de la extracción OCR.*

## Especulación ( predicción)

"Adivina" qué hacer con una instrucción: iniciar la operación lo antes posible, comprobar si la conjetura fue correcta. Si es así, completa la operación; si no, retrocede y haz lo correcto. Problema múltiple, común a estático y dinámico.

Ejemplos:
- Especular sobre el resultado de la condición de salto: revertir si la ruta tomada es diferente.
- Especular cambiando orden de ejecución: especular sobre la instrucción load ( rango de direcciones, puede quedarse fuera de alcance) → puede aparecer una excepción nueva. Revertir si se actualiza la ubicación.

### Compilador / Especulación de hardware

- El compilador puede reordenar las instrucciones ( por ejemplo, mover "load" antes del salto, o adelantar/retrasar LDs vs SWs). Puede incluir instrucciones de "reparación" para recuperarse de una suposición incorrecta.
- El hardware puede buscar instrucciones por adelantado para ejecutar. Almacenar los resultados en un buffer hasta que determine que realmente se necesitan. Vaciar búferes en predicciones resultantes incorrectas.

### Especulaciones y excepciones

¿Qué pasa si ocurre una excepción en una instrucción ejecutada especulativamente? ( por ejemplo, carga especulativa antes de la comprobación de puntero nulo).
- Especulación estática: puede agregar soporte ISA para diferir excepciones.
- Especulación dinámica: puede retrasar las excepciones hasta que finalice la instrucción ( lo que puede que no ocurra).

## Procesadores superescalares y fuera de orden

### Procesadores superescalares

Múltiples copias de la ruta de datos ejecutan múltiples instrucciones a la vez. Las dependencias dificultan la emisión de varias instrucciones a la vez.

*Diagrama de la diapositiva: ruta de datos superescalar con banco de registros de múltiples puertos ( A1-A6, RD1-RD6, WD1-WD3), memoria de instrucciones y memoria de datos duplicadas. El layout no se pudo recuperar de la extracción OCR.*

### RISC-V superescalar: paralelismo espacial

RISC-V Pipeline visto antes → paralelismo temporal. Superescalar → paralelismo espacial.

*Diagrama de la diapositiva: ruta de datos con dos puertos de lectura del banco de registros ( A1/RD1, A2/RD2) y dos de escritura ( WD1, WD2). El layout no se pudo recuperar de la extracción OCR.*

RIPES: simulador de superescalar — Releases · mortbopet/Ripes ( github.com).

### Ejemplo superescalar

IPC ideal: 2. IPC real: 2.

*Diagrama de la diapositiva: cronograma de pipeline superescalar de 2 vías a lo largo de 8 ciclos para las instrucciones `lw s7, 40(s0)`, `add s8, t1, t2`, `sub s9, s1, s3`, `and s10, s3, t4`, `or s11, s1, t5`, `sw s5, 80(s2)`, mostrando las etapas IM/RF/EX/DM/RF de cada una emitidas en pares. El layout exacto no se pudo recuperar de la extracción OCR.*

### Superescalar con Dependencias

IPC ideal: 2. IPC real: 6/4 = 1,5.

*Diagrama de la diapositiva: mismo tipo de cronograma que el ejemplo anterior, pero con instrucciones `lw s8,40(s0)`, `or s11,t5,t6`, `sw s7,80(s11)`, `add s9,s8,t1`, `sub s8,t2,t3`, `and s10,s4,s8`, señalando dependencias RAW y WAR ( en particular, una latencia de 2 ciclos entre la carga y el uso de s8) que reducen el IPC real. El layout exacto no se pudo recuperar de la extracción OCR.*

### Procesador fuera de orden ( OOO)

- Mira hacia adelante a través de múltiples instrucciones.
- Emite tantas instrucciones como sea posible a la vez.
- Emite instrucciones desordenadas ( siempre que no haya dependencias).
- Dependencias:
  - RAW ( lectura después de escritura): una instrucción escribe, la instrucción posterior lee un registro.
  - WAR ( escribir después de leer): una instrucción lee, la instrucción posterior escribe un registro.
  - WAW ( escribir tras escribir): una instrucción escribe, la instrucción posterior escribe el registro.

### Out of Order Processor ( OOO)

- Paralelismo de nivel de instrucción ( ILP): número de instrucciones que se pueden emitir simultáneamente ( promedio < 3).
- Marcador ( scoreboard): tabla que realiza un seguimiento de instrucciones en espera de emisión, unidades funcionales disponibles y dependencias.

El paralelismo a nivel de instrucción ( ILP) es el número de instrucciones que se pueden ejecutar simultáneamente para un programa y una microarquitectura en particular. Los estudios teóricos han demostrado que el ILP puede ser bastante grande para microarquitecturas desordenadas con predictores de bifurcación perfectos y un número enorme de unidades de ejecución. Sin embargo, los procesadores prácticos rara vez logran un ILP superior a dos o tres, incluso con rutas de datos superescalares de seis vías con ejecución desordenada.

### Ejemplo de procesador fuera de orden

IPC ideal: 2. IPC real: 6/4 = 1,5.

*Diagrama de la diapositiva: cronograma de pipeline fuera de orden con las mismas instrucciones del ejemplo "Superescalar con Dependencias", mostrando cómo `and s10,s4,s8` puede ejecutarse antes al reordenar, y señalando que el WAR de s8 en `sub` no depende del s8 de `add`. El layout exacto no se pudo recuperar de la extracción OCR.*

### Cambio de nombre de registros

IPC ideal: 2. IPC real: 6/3 = 2.

*Diagrama de la diapositiva: mismo ejemplo, renombrando el destino de `sub` a `r0` para eliminar la falsa dependencia WAR sobre s8, permitiendo alcanzar IPC = 2. El layout exacto no se pudo recuperar de la extracción OCR.*

El renombramiento de registros tiene sentido en la ejecución fuera de orden para eliminar las antidependencias WAR y WAW, que podrían dar problemas al reordenar.

### Cambio de nombre de registros ( cómo se hace)

Estaciones de reserva y el búfer de reordenación proporcionan el cambio de nombre efectivo de los registros:
- Sobre la emisión de instrucciones a la estación de reserva: si el operando está disponible en el archivo de registros o en el búfer de reordenación, se copia a la estación de reserva; si ya no se requiere en el registro, se puede sobrescribir.
- Si el operando aún no está disponible, será proporcionado a la estación de reservas por una unidad funcional; es posible que no se requiera actualizar el registro.

Ejemplo de WAW:
```asm
lw  s7, 0 ( t3)
add s7, s1, t2
```
¿Puedo descartar `lw s7, 0(t3)`?

## SIMD

- Datos múltiples de instrucción única ( SIMD): la instrucción única actúa sobre múltiples datos a la vez. Aplicación común: gráficos. Se puede aplicar a operaciones aritméticas cortas ( también llamada aritmética empaquetada).
- Por ejemplo, agregue ocho elementos de 8 bits:

*Diagrama de la diapositiva: suma SIMD empaquetada de 8 elementos de 8 bits ( posiciones de bit 63:56 … 7:0), D0 = a7..a0, D1 = b7..b0, D2 = ( a+b)7..( a+b)0. El layout exacto no se pudo recuperar de la extracción OCR.*

## Lanzamiento múltiple estático

El compilador agrupa las instrucciones en "paquetes de emisión": grupo de instrucciones que pueden ser emitidas en un solo ciclo, determinado por los recursos de tubería requeridos. Piense en un paquete de emisión como una instrucción muy larga que especifica varias operaciones simultáneas ⇒ Palabra de instrucción muy larga ( VLIW).

### Programación de lanzamientos múltiples estáticos

El compilador debe eliminar algunos/todos los peligros:
- Reordenar instrucciones en paquetes de emisión: no hay dependencias dentro de un paquete; posiblemente algunas dependencias entre paquetes.
- Varía entre las ISA; el compilador debe saberlo.
- Rellenar con nop si es necesario.

### RISC-V con emisión dual estática

Paquetes de dos instrucciones: una instrucción ALU/branch y una de carga/almacenamiento, alineadas a 64 bits ( ALU/salto, luego cargar/almacenar). Rellene una instrucción no utilizada ( p. ej. por dependencias) con nop.

| Address | Instruction type | Pipeline Stages |
| --- | --- | --- |
| n | ALU/branch | IF ID EX MEM WB |
| n+4 | Load/store | IF ID EX MEM WB |
| n+8 | ALU/branch | · IF ID EX MEM WB |
| n+12 | Load/store | · IF ID EX MEM WB |
| n+16 | ALU/branch | · · IF ID EX MEM WB |
| n+20 | Load/store | · · IF ID EX MEM WB |

### Riesgos en el RISC-V de doble emisión

Más instrucciones ejecutándose en paralelo: peligro de datos EX. El reenvío evitó las paradas en el caso de una sola emisión ( single-issue); ahora no se puede usar el resultado de ALU en cargar/almacenar en el mismo paquete ( van a la vez por dos pipelines distintos):

```asm
add x10, x0, x1
ld  x2, 0 ( x10)
```

Dividido en dos paquetes, una parada. Peligro de uso de "load": todavía un ciclo de retraso, pero ahora dos instrucciones; se requiere una programación más agresiva.

### Ejemplo de programación

Programe esto para RISC-V de doble emisión:

```asm
Loop: ld   x31,0 ( x20)   // x31=array element
      add  x31,x31,x21   // add scalar in x21
      sd   x31,0 ( x20)  // store result
      addi x20,x20,-8    // decrement pointer
      blt  x22,x20,Loop  // branch if x22 < x20
```

| | ALU/branch | Load/store | cycle |
| --- | --- | --- | --- |
| Loop: | nop | ld x31,0 ( x20) | 1 |
| | addi x20,x20,-8 | nop | 2 |
| | add x31,x31,x21 | nop | 3 |
| | blt x22,x20,Loop | sd x31,8 ( x20) | 4 |

IPC = 5/4 = 1,25 ( cf. pico IPC = 2).

### Desenrollado de bucle

Replicar el cuerpo del bucle para tener más paralelismo: reduce la sobrecarga de instrucciones de control de bucle. Usar diferentes registros por replicación ( llamado "cambio de nombre de registro") para evitar las "antidependencias ( no son dependencias reales)" transportadas por bucles, entre repeticiones: escritura seguida de una lectura del mismo registro ( WAR), también conocido como "dependencia del nombre" — reutilización del mismo registro para otro asunto.

### Ejemplo de desenrollado ( "unrolling") de bucle

CPI = 14/8 = 1,75. Más cerca de 2, pero a costo de registros ( se han introducido los registros adicionales x28, x29 y x30) y tamaño de código.

| | ALU/branch | Load/store | cycle |
| --- | --- | --- | --- |
| Loop: | addi x20,x20,-32 | ld x28, 0 ( x20) | 1 |
| | nop | ld x29, 24 ( x20) | 2 |
| | add x28,x28,x21 | ld x30, 16 ( x20) | 3 |
| | add x29,x29,x21 | ld x31, 8 ( x20) | 4 |
| | add x30,x30,x21 | sd x28, 32 ( x20) | 5 |
| | add x31,x31,x21 | sd x29, 24 ( x20) | 6 |
| | nop | sd x30, 16 ( x20) | 7 |
| | blt x22,x20,Loop | sd x31, 8 ( x20) | 8 |

Comparar con la versión sin "unrolling":
```asm
Loop: ld   x31,0 ( x20)   // x31=array element
      add  x31,x31,x21   // add scalar in x21
      sd   x31,0 ( x20)  // store result
      addi x20,x20,-8    // decrement pointer
      blt  x22,x20,Loop  // branch if x22 < x20
```

## Lanzamiento Múltiple Dinámico

Procesadores "superescalares": la CPU decide si emite 0, 1, 2, … cada ciclo. Evita riesgos estructurales y de datos, y la necesidad de reordenación por el compilador ( aunque todavía puede ayudar). Semántica de código asegurada por la CPU.

### Programación de canalización dinámica

Permita que la CPU ejecute instrucciones desordenadas para evitar bloqueos, pero confirme el resultado en los registros en orden.

Ejemplo:
```asm
ld   x31,20 ( x21)
add  x1,x31,x2
sub  x23,x23,x3
andi x5,x23,20
```

Puede iniciar `sub` mientras `add` está esperando `ld`.

### CPU programada dinámicamente

*Diagrama de la diapositiva: CPU con estaciones de reserva y búfer de reordenación ( ROB), que conserva dependencias, mantiene operandos pendientes, envía resultados a cualquier estación de reserva en espera, y usa el ROB para escrituras de registro y para suministrar operandos a instrucciones emitidas. El layout no se pudo recuperar de la extracción OCR.*

Para ver cómo funciona esto conceptualmente, considere los siguientes pasos:

1. Cuando se emite una instrucción, se copia en una estación de reserva para la unidad funcional apropiada. Los operandos que están disponibles en el archivo de registro o en el búfer de reordenación también se copian inmediatamente en la estación de reservas. La instrucción se almacena en búfer en la estación de reserva hasta que todos los operandos y la unidad funcional estén disponibles. Para la instrucción de emisión, la copia de registro del operando ya no es necesaria, y si se produce una escritura en ese registro, el valor podría sobrescribirse.
2. Si un operando no está en el archivo de registro o en el búfer de reordenación, debe estar esperando ser producido por una unidad funcional. Se realiza un seguimiento del nombre de la unidad funcional que producirá el resultado. Cuando esa unidad finalmente produce el resultado, se copia directamente en la estación de reserva de espera desde la unidad funcional sin pasar por los registros.

Estos pasos utilizan eficazmente el búfer de reorden y las estaciones de reserva para implementar el cambio de nombre del registro.

- **Ejecución fuera de orden**: una situación en la ejecución canalizada cuando una instrucción bloqueada para ejecutar no hace que las siguientes instrucciones esperen.
- **Confirmación en orden**: una confirmación en la que los resultados de la ejecución canalizada se escriben en el mismo orden en que se obtienen las instrucciones, según el estado visible del programador. ( Today, all dynamically scheduled pipelines use in-order commit.)

### Especulación

Predecir salto y continuar emitiendo; no haga efectivo el valor ( commit unit) hasta que se determine el resultado.

Carga la especulación: evite la carga y el retraso de pérdida de caché.
- Predecir la dirección efectiva.
- Predecir valor cargado.
- Cargar antes de completar los almacenamientos pendientes ( pasa valores almacenados a la unidad de carga).
- No haga efectiva la carga hasta que se elimine la especulación.

### ¿Funciona el lanzamiento múltiple?

Sí, pero no tanto como nos gustaría:
- Los programas tienen dependencias reales que limitan el ILP; algunas dependencias son difíciles de eliminar ( por ejemplo, alias de puntero).
- Cierto paralelismo es difícil de exponer: tamaño de ventana limitado durante la emisión de instrucciones.
- Retrasos de memoria y ancho de banda limitado: es difícil mantener las pipelines llenas.
- La especulación puede ayudar si se hace bien.

El paralelismo a nivel de instrucción ( ILP) es el número de instrucciones que se pueden ejecutar simultáneamente para un programa y una microarquitectura en particular. Los estudios teóricos han demostrado que el ILP puede ser bastante grande para microarquitecturas desordenadas con predictores de bifurcación perfectos y un número enorme de unidades de ejecución. Sin embargo, los procesadores prácticos rara vez logran un ILP superior a dos o tres, incluso con rutas de datos superescalares de seis vías con ejecución desordenada.

### Eficiencia energética

La complejidad de la programación dinámica y las especulaciones requiere energía; múltiples núcleos más simples pueden ser mejores.

| Microprocessor | Year | Clock Rate | Pipeline Stages | Issue Width | Out-of-Order/Speculation | Cores/Chip | Power |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Intel 486 | 1989 | 25 MHz | 5 | 1 | No | 1 | 5 W |
| Intel Pentium | 1993 | 66 MHz | 5 | 2 | No | 1 | 10 W |
| Intel Pentium Pro | 1997 | 200 MHz | 10 | 3 | Yes | 1 | 29 W |
| Intel Pentium 4 Willamette | 2001 | 2000 MHz | 22 | 3 | Yes | 1 | 75 W |
| Intel Pentium 4 Prescott | 2004 | 3600 MHz | 31 | 3 | Yes | 1 | 103 W |
| Intel Core | 2006 | 3000 MHz | 14 | 4 | Yes | 2 | 75 W |
| Intel Core i7 Nehalem | 2008 | 3600 MHz | 14 | 4 | Yes | 2-4 | 87 W |
| Intel Core Westmere | 2010 | 3730 MHz | 14 | 4 | Yes | 6 | 130 W |
| Intel Core i7 Ivy Bridge | 2012 | 3400 MHz | 14 | 4 | Yes | 6 | 130 W |
| Intel Core Broadwell | 2014 | 3700 MHz | 14 | 4 | Yes | 10 | 140 W |
| Intel Core i9 Skylake | 2016 | 3100 MHz | 14 | 4 | Yes | 14 | 165 W |
| Intel Ice Lake | 2018 | 4200 MHz | 14 | 4 | Yes | 16 | 185 W |

### Cortex A53 e Intel i7

| Característica | Cortex A53 | Intel Core i7 920 |
| --- | --- | --- |
| Mercado | Dispositivo móvil | Servidor, nube |
| Potencia | 100 milivatios ( 1 núcleo a 1 GHz) | 130 vatios |
| Velocidad de reloj | 1,5 GHz | 2,66 GHz |
| Núcleos/chip | 4 ( configurables) | 4 |
| ¿Punto flotante? | Sí | Sí |
| ¿Lanzamiento múltiple? | Dinámica | Dinámica |
| Pico de instrucciones/ciclo de reloj | 2 | 4 |
| Etapas | 8 | 14 |
| Modalidad de canalización | Estático en orden | Dinámica fuera de orden con especulación |
| Predicción | Híbrido | 2 niveles |
| Cachés/núcleo de primer nivel | 16-64 KiB I, 16-64 KiB D | 32 KiB I, 32 KiB D |
| Cachés/núcleo de segundo nivel | 128-2048 KiB ( depende de la plataforma) | 256 KiB ( por núcleo) |
| Cachés de tercer nivel ( compartido) | — | 2-8 MB |

### Pipeline ARM Cortex-A53

*Diagrama de la diapositiva: etapas del pipeline del Cortex-A53. El layout no se pudo recuperar de la extracción OCR.*

### Rendimiento ARM Cortex-A53

La composición estimada del IPC en el ARM A53 muestra que los estancamientos de los pipelines son significativos, pero compensados por las fallas de caché en los programas de peor rendimiento. Estos se restan del IPC medido por un simulador detallado para obtener las paradas del pipeline. Las paradas de pipeline incluyen los tres peligros.

### Pipeline Core i7

*Diagrama de la diapositiva: etapas del pipeline del Core i7. El layout no se pudo recuperar de la extracción OCR.*

### Rendimiento del núcleo i7

La tasa de predicción errónea para los puntos de referencia enteros SPECCPU2006 en el Intel Core i7 6700. La tasa de predicción errónea se calcula como la proporción de ramas completadas que se predicen erróneamente frente a todas las ramas completadas. ( CPI para SPECCPUint2006 benchmarks on the i7 6700.)

## Multiplicar Matriz ( DGEMM)

Versión C optimizada de DGEMM usando intrínsecos de C para generar las instrucciones AVX subword-parallel para x86. Código C desenrollado para x86:

```c
#include <x86intrin.h>
#define UNROLL ( 4)

void dgemm ( int n, double* A, double* B, double* C)
{
  for ( int i = 0; i < n; i+=UNROLL*4 )
    for ( int j = 0; j < n; j++ ) {
      __m256d c[4];
      for ( int x = 0; x < UNROLL; x++ )
        c[x] = _mm256_load_pd ( C+i+x*4+j*n);

      for ( int k = 0; k < n; k++ )
      {
        __m256d b = _mm256_broadcast_sd ( B+k+j*n);
        for ( int x = 0; x < UNROLL; x++)
          c[x] = _mm256_add_pd ( c[x],
                   _mm256_mul_pd ( _mm256_load_pd ( A+n*k+x*4+i), b));
      }

      for ( int x = 0; x < UNROLL; x++ )
        _mm256_store_pd ( C+i+x*4+j*n, c[x]);
    }
}
```

### Multiplicar Matriz ( ensamblador x86)

El lenguaje ensamblador x86 para el cuerpo de los bucles anidados generados al compilar el código C desenrollado:

```asm
vmovapd (%r11),%zmm4          # Cargar 8 elementos de C en %zmm4
mov %rbx,%rcx                 # registro %rcx = %rbx
xor %eax,%eax                 # registro %eax = 0
vmovapd 0x20 (%r11),%zmm3     # Carga 8 elementos de C en %zmm3
vmovapd 0x40 (%r11),%zmm2     # Carga 8 elementos de C en %zmm2
vmovapd 0x60 (%r11),%zmm1     # Carga 8 elementos de C en %zmm1
vbroadcastsd (%rax,%r8,8),%zmm0 # Hacer 8 copias del elemento B en %zmm0
agregue $0x8,%rax             # registre %rax = %rax + 8
vfmadd231pd (%rcx),%zmm0,%zmm4      # Mul paralelo y agregar %zmm0, %zmm4
vfmadd231pd 0x20 (%rcx),%zmm0,%zmm3 # Mul paralelo y agregar %zmm0, %zmm3
vfmadd231pd 0x40 (%rcx),%zmm0,%zmm2 # Mul paralelo y agregar %zmm0, %zmm2
vfmadd231pd 0x60 (%rcx),%zmm0,%zmm1 # Multi paralelo y agregar %zmm0, %zmm1
agregar %r9,%rcx               # registrar %rcx = %rcx + %r9
cmp %r10,%rax                  # comparar %r10 con %rax
jne 50 <dgemm+0x50>            # saltar si no %r10 != %rax
agregar $0x1, %esi             # registrar %esi = %esi + 1
vmovapd %zmm4, (%r11)          # Almacenar %zmm4 en 8 elementos C
vmovapd %zmm3, 0x20 (%r11)     # Almacenar %zmm3 en 8 elementos C
vmovapd %zmm2, 0x40 (%r11)     # Almacenar %zmm2 en 8 elementos C
vmovapd %zmm1, 0x60 (%r11)     # Almacenar %zmm1 en 8 elementos C
```

### Impacto en el rendimiento

*Diagrama de la diapositiva: gráfico del impacto en el rendimiento de las distintas optimizaciones ( AVX, desenrollado, FMA, etc.) sobre DGEMM. El layout no se pudo recuperar de la extracción OCR.*

## Multiproceso y multiprocesadores

### Introducción

Objetivo: conectar varias computadoras para obtener un mayor rendimiento.

- Multiprocesadores: escalabilidad, disponibilidad, eficiencia energética.
- Paralelismo a nivel de tarea ( nivel de proceso): alto rendimiento para trabajos independientes.
- Programa de procesamiento en paralelo: un solo programa se ejecuta en múltiples procesadores.
- Microprocesadores multinúcleo: chips con múltiples procesadores ( núcleos).

### Técnicas de Arquitectura Avanzada

- Subprocesos múltiples: por ejemplo, un procesador de textos con subprocesos para escribir, revisar la ortografía, imprimir.
- Multiprocesadores: múltiples procesadores ( núcleos) en un solo chip.

### Hilos: Definiciones

- **Proceso**: programa que se ejecuta en una computadora. Se pueden ejecutar varios procesos a la vez ( por ejemplo, navegar por Internet, reproducir música, escribir un artículo).
- **Hilo**: parte de un programa. Cada proceso tiene varios subprocesos ( por ejemplo, un procesador de textos puede tener subprocesos para escribir, revisar la ortografía, imprimir).

### Subprocesos en un procesador convencional

Sistema de un solo núcleo: un hilo se ejecuta a la vez. Cuando un subproceso se detiene ( por ejemplo, esperando memoria): se almacena el estado arquitectónico de ese hilo, se carga y ejecuta el estado arquitectónico del subproceso de espera ( "cambio de contexto"). Al usuario le parece que todos los subprocesos se ejecutan simultáneamente.

### Programación en paralelo

El software paralelo es el problema: necesidad de obtener una mejora significativa del rendimiento; de lo contrario, simplemente use un monoprocesador más rápido, ¡ya que es más fácil! Dificultades: fraccionamiento, coordinación, gastos generales de comunicaciones.

### Ley de Amdahl

La parte secuencial puede limitar la aceleración. Ejemplo: 100 procesadores, ¿aceleración de 90×?

$$T_{nueva} = \frac{T_{paralelizable}}{100} + T_{secuencial}$$

$$Speedup = \frac{1}{(1-F_{paralelizable}) + F_{paralelizable}/100} = 90$$

Resolviendo: F_paralelizable = 0,999. Necesita que la parte secuencial sea 0,1% del tiempo original.

### Ejemplo de escala

Carga de trabajo: suma de 10 escalares y suma de matriz de 10×10. Acelerar de 10 a 100 procesadores.

- Procesador único: Tiempo = ( 10 + 100) × t_suma.
- 10 procesadores: Tiempo = 10 × t_suma + 100/10 × t_suma = 20 × t_suma. Aceleración = 110/20 = 5,5 ( 55% del potencial de 10).
- 100 procesadores: Tiempo = 10 × t_suma + 100/100 × t_suma = 11 × t_suma. Aceleración = 110/11 = 10 ( 10% del potencial de 100).

Supone que la carga se puede equilibrar entre procesadores.

### Ejemplo de escalado ( continuación)

¿Qué pasa si el tamaño de la matriz es 100×100?

- Procesador único: Tiempo = ( 10 + 10000) × t_suma.
- 10 procesadores: Tiempo = 10 × t_suma + 10000/10 × t_suma = 1010 × t_suma. Aceleración = 10010/1010 = 9,9 ( 99% del potencial).
- 100 procesadores: Tiempo = 10 × t_suma + 10000/100 × t_suma = 110 × t_suma. Aceleración = 10010/110 = 91 ( 91% del potencial).

Asumiendo carga balanceada.

### Escalado fuerte vs débil

- Escalado fuerte: tamaño del problema fijo ( como en el ejemplo).
- Escalado débil: tamaño del problema proporcional al número de procesadores.

10 procesadores, matriz 10×10: Tiempo = 20 × t_suma.
100 procesadores, matriz 32×32: Tiempo = 10 × t_suma + 1000/100 × t_suma = 20 × t_suma.

Rendimiento constante en este ejemplo.

### Multi-hilo

- Múltiples copias del estado arquitectónico; múltiples hilos activos en seguida. Cuando un hilo se detiene, otro se ejecuta inmediatamente. Si un subproceso no puede mantener ocupadas todas las unidades de ejecución, otro subproceso puede usarlas.
- No aumenta el paralelismo a nivel de instrucción ( ILP) de un solo subproceso, pero aumenta el rendimiento. Intel llama a esto "hiperhilo" ( hyperthreading).

### Multiprocesadores

Múltiples procesadores ( núcleos) con un método de comunicación entre ellos. Tipos:
- Homogéneo: múltiples núcleos con memoria principal compartida.
- Heterogéneo: núcleos separados para diferentes tareas ( por ejemplo, DSP y CPU en el teléfono celular).
- Clústeres: cada núcleo tiene su propio sistema de memoria.

### Instrucciones y flujos de datos

Una clasificación alternativa:

| | Flujo de datos simple | Flujo de datos múltiple |
| --- | --- | --- |
| Flujo de instrucciones simple | SISD: Intel Pentium 4 | SIMD: instrucciones SSE de x86 |
| Flujo de instrucciones múltiple | MISD: no hay ejemplos hoy | MIMD: Intel Xeon e5345 |

SPMD: programa único, datos múltiples — un programa paralelo en una computadora MIMD, con código condicional para diferentes procesadores.

### Procesadores vectoriales

Unidades de función altamente canalizadas: transmitir datos desde/hacia registros vectoriales a unidades. Datos recopilados de la memoria en registros; resultados almacenados de registros a la memoria.

Ejemplo: extensión de vector a RISC-V. v0 a v31: registros de 32 × 64 elementos ( elementos de 64 bits). Instrucciones vectoriales:
- `fld.v`, `fsd.v`: vector de carga/almacenamiento.
- `fadd.dv`: agregar vectores de doble.
- `fadd.d.vs`: agregue escalar a cada elemento del vector de doble.

Reduce significativamente el ancho de banda de búsqueda de instrucciones.

### Ejemplo: DAXPY ( Y = a × X + Y)

Código RISC-V convencional:

```asm
fld  f0,a ( x3)       // carga escalar a
addi x5,x19,512       // fin del arreglo X
bucle:
fld  f1,0 ( x19)      // carga x[i]
fmul.d f1,f1,f0       // a * x[i]
fld  f2,0 ( x20)      // carga y[i]
fadd.d f2,f2,f1       // a * x[i] + y[i]
fsd  f2,0 ( x20)      // almacena y[i]
addi x19,x19,8        // incrementa el índice a x
addi x20,x20,8        // incrementa el índice a y
bltu x19,x5,bucle     // repetir si no se hace
```

Código vectorial RISC-V:

```asm
fld    f0,a ( x3)     // carga escalar a
fld.v  v0,0 ( x19)    // cargar el vector x
fmul.d.vs v0,v0,f0    // multiplicación vector-escalar
fld.v  v1,0 ( x20)    // carga el vector y
fadd.dv v1,v1,v0      // añadir vector-vector
fsd.v  v1,0 ( x20)    // almacena el vector y
```

### Vector vs Escalar

Arquitecturas vectoriales y compiladores:
- Simplifican la programación de datos en paralelo, con declaración explícita de ausencia de dependencias transportadas por bucle. Comprobación reducida en hardware.
- Los patrones de acceso regulares se benefician de la memoria intercalada y de ráfagas. Evitan los riesgos de control al evitar los bucles.
- Más general que las extensiones de medios ad-hoc ( como MMX, SSE). Mejor combinación con la tecnología del compilador.

### SIMD ( extensiones multimedia)

Operar por elementos en vectores de datos: por ejemplo, instrucciones MMX y SSE en x86. Múltiples elementos de datos en registros de 128 bits de ancho. Todos los procesadores ejecutan la misma instrucción al mismo tiempo, cada uno con diferente dirección de datos, etc. Simplifica la sincronización; hardware de control de instrucción reducido. Funciona mejor para aplicaciones altamente paralelas de datos.

### Extensiones vectoriales vs. multimedia

Las instrucciones vectoriales tienen un ancho de vector variable; las extensiones multimedia tienen un ancho fijo. Las unidades vectoriales pueden ser una combinación de unidades funcionales segmentadas y en matriz.

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

## Subprocesos ( Hilos) múltiples

Realización de múltiples hilos de ejecución en paralelo: replicar registros, PC, etc.; cambio rápido entre hilos.
- Multihilo de grano fino: cambiar hilos después de cada ciclo ( ejecución de instrucciones intercaladas). Si un hilo se detiene, otros se ejecutan.
- Multihilo de grano grueso: solo lo activa la parada larga ( por ejemplo, L2-cache miss). Simplifica el hardware, pero no oculta las paradas breves ( p. ej., riesgos de datos).

### Hilos múltiples simultáneos

En el procesador programado dinámicamente de múltiple "issue": organiza el lanzamiento de instrucciones de varios hilos; las instrucciones de hilos independientes se ejecutan cuando las unidades de función están disponibles. Dentro de los hilos, las dependencias se manejan mediante organización del lanzamiento de instrucciones y el cambio de nombre de los registros.

Ejemplo: Intel Pentium-4 HT — dos hilos: registros duplicados, unidades de función compartidas y cachés.

### Ejemplo de subprocesos ( hilos) múltiples

*Diagrama de la diapositiva: los cuatro subprocesos en la parte superior muestran cómo se ejecutaría cada uno solo en un procesador superescalar estándar sin compatibilidad con subprocesos múltiples; los tres ejemplos en la parte inferior muestran cómo se ejecutarían juntos en tres opciones de hilos múltiples. La dimensión horizontal representa la capacidad de emisión de instrucciones en cada ciclo de reloj; la vertical, una secuencia de ciclos de reloj. Un cuadro vacío ( blanco) indica que el espacio de emisión correspondiente no se utiliza en ese ciclo. Los tonos de gris y color corresponden a cuatro subprocesos diferentes en los procesadores multiproceso. El layout exacto no se pudo recuperar de la extracción OCR.*

### Futuro de hilos múltiples

¿Sobrevivirá? ¿En qué forma? Consideraciones de energía ⇒ microarquitecturas simplificadas. Formas más simples de subprocesamiento múltiple: tolerar la latencia de pérdida de caché, el cambio de hilo puede ser más efectivo. Múltiples núcleos simples pueden compartir recursos de manera más efectiva.

### Memoria compartida

SMP: multiprocesador de memoria compartida. El hardware proporciona un único espacio de direcciones físicas para todos los procesadores. Sincronizar variables compartidas mediante bloqueos. Tiempo de acceso a la memoria: UMA ( uniforme) frente a NUMA ( no uniforme).

### Ejemplo: Suma Reducción

Suma 64.000 números en 64 procesadores UMA. Cada procesador tiene ID: 0 ≤ Pn ≤ 63. Particionar 1000 números por procesador; suma inicial en cada procesador:

```c
suma[Pn] = 0;
for ( i = 1000*Pn; i < 1000*( Pn+1); i += 1)
  sum[Pn] += A[i];
```

Ahora necesita agregar estas sumas parciales. Reducción: divide y vencerás — la mitad de los procesadores agregan pares, luego cuartos, … Necesidad de sincronizar entre los pasos de reducción.

```c
mitad = 64;
hacer {
  sincronizar();
  if ( mitad%2 != 0 && Pn == 0)
    suma[0] += suma[mitad-1];
    /* Suma condicional necesaria cuando la mitad es impar;
       Processor0 obtiene el elemento faltante */
  mitad = mitad/2; /* línea divisoria sobre quien suma */
  if ( Pn < mitad) suma[Pn] += suma[Pn+mitad];
} mientras ( mitad > 1);
```

## GPU

### Historia de las GPU

- Primeras tarjetas de video: memoria intermedia de cuadros con generación de direcciones para salida de video.
- Procesamiento de gráficos 3D: originalmente computadoras de gama alta ( por ejemplo, SGI).
- Ley de Moore ⇒ menor costo, mayor densidad: tarjetas gráficas 3D para PC y videoconsolas.
- Unidades de procesamiento de gráficos: procesadores orientados a tareas gráficas 3D ( procesamiento de vértices/píxeles, sombreado, mapeo de texturas, rasterización).

### Gráficos en el Sistema

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Arquitecturas GPU

El procesamiento es altamente paralelo a los datos. Las GPU son altamente multiproceso: usan el cambio de subprocesos para ocultar la latencia de la memoria; menos dependencia de cachés de varios niveles; la memoria gráfica es amplia y de gran ancho de banda.

Tendencia hacia las GPU de propósito general: sistemas CPU/GPU heterogéneos ( CPU para código secuencial, GPU para código paralelo). Lenguajes de programación/API: DirectX, OpenGL, C para gráficos ( Cg), lenguaje de sombreado de alto nivel ( HLSL).

Arquitectura de dispositivo unificado de cómputo ( CUDA): plataforma informática paralela y una interfaz de programación de aplicaciones ( API) que permite que el software use ciertos tipos de unidades de procesamiento de gráficos ( GPU) para el procesamiento de propósito general, un enfoque denominado computación de propósito general en GPU ( GPGPU).

### Ejemplo: NVIDIA Tesla

Múltiples procesadores SIMD.

*Diagrama de la diapositiva: arquitectura de un procesador SIMD de NVIDIA Tesla. El layout no se pudo recuperar de la extracción OCR.*

Procesador SIMD: 16 carriles SIMD. Instrucción SIMD opera en subprocesos de 32 elementos de ancho, programada dinámicamente en un procesador de 16 de ancho durante 2 ciclos. Registros de 32.000 × 32 bits distribuidos en carriles; 64 registros por contexto de subproceso.

### Estructuras de memoria GPU

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Clasificación de GPU

No encaja bien en el modelo SIMD/MIMD: la ejecución condicional en un hilo permite una ilusión de MIMD, pero con degradación del rendimiento. Necesidad de escribir código de propósito general con cuidado.

| | Estático: descubierto en tiempo de compilación | Dinámico: descubierto en tiempo de ejecución |
| --- | --- | --- |
| Paralelismo a nivel de instrucción | VLIW | Superescalar |
| Paralelismo a nivel de datos | SIMD o Vector | Multiprocesador ( Tesla) |

### Poniendo las GPU en perspectiva

| Característica | Multinúcleo con SIMD | GPU |
| --- | --- | --- |
| Procesadores SIMD | 8 a 24 | 15 a 80 |
| SIMD/procesador | 2 a 4 | 8 a 16 |
| Soporte de hardware de subprocesos múltiples para subprocesos SIMD | 2 a 4 | 16 a 32 |
| Relación típica de rendimiento de precisión simple a precisión doble | 2:1 | 2:1 |
| Tamaño de caché | 48 MB | 6 MB |
| Tamaño de la dirección de memoria | 64 bits | 64 bits |
| Tamaño de la memoria principal | 64 GB a 1024 GB | 4 GB a 16 GB |
| Protección de memoria a nivel de página | Sí | Sí |
| Localización | Sí | No |
| Caché coherente | Sí | No |

### Guía de términos de GPU

*Diagrama/tabla de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Paso de mensajes

Cada procesador tiene un espacio de direcciones físico privado. El hardware envía/recibe mensajes entre procesadores.

### Clústeres débilmente acoplados

Red de ordenadores independientes: cada uno tiene memoria privada y sistema operativo, conectados mediante el sistema de E/S ( por ejemplo, Ethernet/conmutador, Internet). Adecuado para aplicaciones con tareas independientes: servidores web, bases de datos, simulaciones, … Alta disponibilidad, escalable, asequible.

Problemas: costo de administración ( preferir máquinas virtuales); bajo ancho de banda de interconexión ( cf. procesador/ancho de banda de memoria en un SMP).

### Reducción de Suma ( otra vez)

Suma 64.000 en 64 procesadores. Primero distribuya 1000 números a cada uno para las sumas parciales:

```c
suma = 0;
para ( i = 0; i<1000; i += 1)
  suma += AN[i];
```

Reducción: la mitad de los procesadores envían, la otra mitad reciben y agregan; la cuarta parte envía, la cuarta parte recibe y suma, …

Dadas las operaciones enviar() y recibir():

```c
límite = 64; mitad = 64; /* 64 procesadores */
do {
  mitad = ( mitad+1)/2; /* línea divisoria enviar vs. recibir */
  if ( Pn >= mitad && Pn < límite)
    enviar ( Pn - mitad, suma);
  if ( Pn < ( límite/2))
    suma += recibir();
  límite = mitad; /* límite superior de remitentes */
} while ( mitad > 1); /* salir con la suma final */
```

Enviar/recibir también proporciona sincronización. Supone que enviar/recibir toma un tiempo similar a la adición.

### Computación en red

Computadoras separadas interconectadas por redes de larga distancia ( por ejemplo, conexiones a Internet). Unidades de trabajo cedidas, resultados devueltos. Puede hacer uso del tiempo de inactividad en las PC ( por ejemplo, SETI@home, World Community Grid).

### Redes de Interconexión

Topologías de red: disposiciones de procesadores, conmutadores y enlaces ( bus, anillo, N-cubo [N=3], malla 2D, totalmente conectado).

*Diagrama de la diapositiva: las cinco topologías mencionadas. El layout no se pudo recuperar de la extracción OCR.*

### Redes multietapa

*Diagrama de la diapositiva. El layout no se pudo recuperar de la extracción OCR.*

### Características de la red

- Actuación: latencia por mensaje ( red descargada); rendimiento ( ancho de banda del enlace, ancho de banda total de la red); retrasos por congestión ( dependiendo del tráfico).
- Costo: fuerza, ruteabilidad en silicio.

### Benchmarks paralelos

- Linpack: álgebra lineal matricial.
- SPECrate: ejecución paralela de programas de CPU SPEC ( paralelismo a nivel de trabajo).
- SPLASH: aplicaciones paralelas de Stanford para memoria compartida ( mezcla de kernels y aplicaciones, fuerte escalado).
- Suite NAS ( supercomputación avanzada de la NASA): núcleos de dinámica de fluidos computacional.
- Suite PARSEC ( repositorio de aplicaciones de Princeton para computadoras con memoria compartida): aplicaciones multihilo usando Pthreads y OpenMP.

### ¿Código o Aplicaciones?

Benchmarks tradicionales: código fijo y conjuntos de datos. La programación paralela está evolucionando: ¿deberían los algoritmos, los lenguajes de programación y las herramientas ser parte del sistema? Comparar sistemas, siempre que implementen una aplicación determinada ( por ejemplo, Linpack, patrones de diseño de Berkeley). Fomentaría la innovación en los enfoques del paralelismo.

## Falacias y Trampas

### Falacias

- Canalizar es fácil (!): la idea básica es fácil, el diablo está en los detalles ( por ejemplo, detectar riesgos de datos).
- Los pipelines son independientes de la tecnología: entonces, ¿por qué no hemos hecho canalizaciones siempre? Más transistores hacen factibles técnicas más avanzadas. El diseño de ISA relacionado con pipelines debe tener en cuenta las tendencias tecnológicas.

### Trampas

Un mal diseño de ISA puede dificultar la canalización ( por ejemplo, conjuntos de instrucciones complejos como VAX, IA-32). Costes significativos para hacer que la canalización funcione:
- Enfoque micro-ops de IA-32 ( por ejemplo, modos de direccionamiento complejos, registrar efectos secundarios de actualización, indirección de memoria).
- Por ejemplo, saltos ( ramas) retrasadas: las canalizaciones avanzadas tienen ranuras de retraso largas ( recuerda lab: "delay slot").

### Observaciones finales

- ISA influye en el diseño de la ruta de datos y el control; el diseño de la ISA influye en el diseño de control y ruta de datos.
- La canalización mejora el rendimiento de las instrucciones mediante el paralelismo: más instrucciones completadas por segundo, aunque la latencia para cada instrucción no se reduce.
- Peligros: estructurales, datos, control.
- Organización del lanzamiento dinámico y múltiple ( ILP): las dependencias limitan el paralelismo alcanzable.
- La complejidad conduce al muro de consumo de potencia.

## RISC-V estado actual

Debido a que el conjunto de instrucciones base se describió por completo recientemente, en 2017, muchos chips RISC-V están en desarrollo, pero solo unos pocos están en el mercado a partir de 2022. Pero se espera que eso cambie rápidamente a medida que madure.

La mayoría de las implementaciones de procesadores existentes se encuentran en procesadores empotrados, pero chips de alto rendimiento están en el horizonte. RISC-V International ( riscv.org) proporciona una lista cada vez mayor de núcleos y plataformas SoC. Los núcleos comerciales RISC-V se encuentran en tarjetas de desarrollo HiFive de SiFive, discos duros Western Digital y GPU NVIDIA, entre otros.

A partir de 2021, dos procesadores RISC-V comerciales notables son el núcleo Freedom E310 de SiFive y el núcleo SweRV de código abierto de Western Digital, que viene en tres versiones. El Freedom E310 es un procesador empotrado utilizado en las placas de desarrollo HiFive de SiFive y RED-V de Sparkfun. Ejecuta RV32IMAC ( RV32I con multiplicar/dividir [M], accesos a memoria atómica [A] y extensiones de instrucciones comprimidas [C]) y tiene 8 KB de memoria de programa, 8 KB de ROM de máscara para código de arranque, 16 KB de SRAM de datos, y una memoria caché de instrucciones asociativa de conjunto bidireccional de 16 KB. También incluye interfaces JTAG, SPI, I2C y UART, así como una interfaz de memoria flash QSPI. El procesador funciona a 320 MHz y es un núcleo en orden de un solo problema con una canalización de 5 etapas que tiene las mismas etapas descritas en este capítulo. La figura en la página siguiente muestra un diagrama de bloques del procesador FE310-G002 que se encuentra en la placa HiFive 1.

Recuerda algunas de las ventajas de RISC-V: abierto, ISA expandible, ISA moldeable, procesadores especializados ( se acaba cumpliendo la ley de Moore), Open Cores y mucho más…

*Diagrama de bloques de Freedom E310-G002 ( cortesía de SiFive Inc., hoja de datos preliminar de SiFive FE310-G002 v1p0, ©2019). El layout no se pudo recuperar de la extracción OCR.*

### RISC-V RVFPGA for you

RISC-V FPGA, también conocido como RVfpga, son algunas de las prácticas de esta asignatura. Las primeras prácticas muestran cómo sintetizar un núcleo RISC-V comercial a un FPGA, programarlo usando ensamblador RISC-V o C, agregarle periféricos y analizar y modificar el núcleo y el sistema de memoria, incluso agregar instrucciones al núcleo. Estas prácticas utilizan el sistema en chip ( SoC) SweRVolf de código abierto ( https://github.com/chipsalliance/Cores-SweRVolf), que se basa en el núcleo SweRV EH1 comercial de código abierto de Western Digital ( https://www.westerndigital.com/company/innovations/risc-v). Las prácticas también muestran cómo usar Verilator, un simulador HDL de código abierto, y Whisper de Western Digital, un simulador de conjunto de instrucciones ( ISS) RISC-V de código abierto. RVfpga-SoC, la segunda parte, muestra cómo construir un SoC basado en SweRVolf usando bloques como el núcleo SweRV EH1, interconexión y memorias. Las prácticas luego continúan guiando al alumno ejecutando el sistema operativo Zephyr en el SoC RISC-V. Todo el software necesario y el código fuente del sistema ( archivos Verilog/SystemVerilog) son libres y las prácticas se pueden completar en simulación, por lo que no se requiere hardware. Los materiales de RVfpga están disponibles en: https://university.imgtec.com/rvfpga/.
