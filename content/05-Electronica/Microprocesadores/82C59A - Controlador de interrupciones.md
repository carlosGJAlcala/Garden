---
title: "82C59A - Controlador de interrupciones"
---

# 82C59A

Controlador de Interrupciones Prioritarias CMOS de Harris

## Características

### Versiones Disponibles
- Operación a 12.5MHz: 82C59A-12
- Operación a 8MHz: 82C59A
- Operación a 5MHz: 82C59A-5

### Descripción General

El 82C59A de Harris es un controlador de interrupciones prioritarias CMOS de alto rendimiento fabricado usando un proceso CMOS avanzado de 2 µm. El 82C59A está diseñado para aliviar al CPU del sistema de la tarea de sondeo en un sistema de prioridad multinivel. La velocidad alta y la configuración estándar de la industria del 82C59A lo hacen compatible con microprocesadores como 80C286, 80286, 80C86/88, 8086/88, 8080/85 y NSC800.

### Características Principales

- Operación de Alta Velocidad sin Estado de Espera con configuración de 12.5MHz
- Compatible con Pines con NMOS 8259A
- Compatible con 80C86/88/286 y 8080/85/86/88/286
- Controlador de Prioridad de Ocho Niveles, Expandible a 64 Niveles
- Modos de Interrupción Programable
- Capacidad de Máscara Individual de Solicitud
- Diseño de Circuito CMOS Completamente Estático
- Completamente Compatible con TTL
- Operación de Bajo Consumo de Potencia
  - ICCSB: 10 mA Máximo
  - ICCOP: 1 mA/MHz Máximo
- Suministro de Energía Único de 5V

### Rangos de Temperatura de Operación

| Variante | Rango de Temperatura |
|---|---|
| C82C59A | 0°C a +70°C |
| I82C59A | -40°C a +85°C |
| M82C59A | -55°C a +125°C |

## Información de Pedido

| Velocidad | Tipo de Paquete | Rango de Temperatura | PKG. NO. |
|---|---|---|---|
| 5MHz | CP82C59A-5 | 28 Ld PDIP | E28.6 |
| 8MHz | CP82C59A | 28 Ld PDIP | E28.6 |
| 12.5MHz | CP82C59A-12 | 28 Ld PDIP | E28.6 |
| 5MHz | IP82C59A-5 | 28 Ld PDIP | E28.6 |
| 8MHz | IP82C59A | 28 Ld PDIP | E28.6 |
| 12.5MHz | IP82C59A-12 | 28 Ld PDIP | E28.6 |
| 5MHz | CS82C59A-5 | 28 Ld PLCC | N28.45 |
| 8MHz | CS82C59A | 28 Ld PLCC | N28.45 |
| 12.5MHz | CS82C59A-12 | 28 Ld PLCC | N28.45 |
| 5MHz | IS82C59A-5 | 28 Ld PLCC | N28.45 |
| 8MHz | IS82C59A | 28 Ld PLCC | N28.45 |
| 12.5MHz | IS82C59A-12 | 28 Ld PLCC | N28.45 |
| 5MHz | CD82C59A-5 | CERDIP | F28.6 |
| 8MHz | CD82C59A | CERDIP | F28.6 |
| 12.5MHz | CD82C59A-12 | CERDIP | F28.6 |
| 5MHz | ID82C59A-5 | CERDIP | F28.6 |
| 8MHz | ID82C59A | CERDIP | F28.6 |
| 12.5MHz | ID82C59A-12 | CERDIP | F28.6 |
| 5MHz | MD82C59A-5/B | CERDIP | F28.6 |
| 8MHz | MD82C59A/B | CERDIP | F28.6 |
| 12.5MHz | MD82C59A-12/B | CERDIP | F28.6 |
| 5MHz | MR82C59A-5/B | 28 Pad CLCC | J28.A |
| 8MHz | MR82C59A/B | 28 Pad CLCC | J28.A |
| 12.5MHz | MR82C59A-12/B | 28 Pad CLCC | J28.A |
| 5MHz | CM82C59A-5 | 28 Ld SOIC | M28.3 |
| 8MHz | CM82C59A | 28 Ld SOIC | M28.3 |
| 12.5MHz | CM82C59A-12 | 28 Ld SOIC | M28.3 |

**Advertencia:** Estos dispositivos son sensibles a descargas electrostáticas. Los usuarios deben seguir procedimientos apropiados de manipulación de circuitos integrados. Número de archivo: 2784.2

Copyright © Harris Corporation 1997

## Configuración de Pines

### Vista Superior

**82C59A (PDIP, CERDIP, SOIC)**
```
      1  28
  CS  1  28  VCC
  WR  2  27  A0
  RD  3  26  INTA
  D7  4  25  IR7
  D6  5  24  IR6
  D5  6  23  IR5
  D4  7  22  IR4
  D3  8  21  IR3
  D2  9  20  IR2
  D1 10  19  IR1
  D0 11  18  IR0
CAS0 12  17  INT
CAS1 13  16  SP/EN
GND 14  15  CAS2
```

**82C59A (PLCC, CLCC)**
```
      1  28
  4  3  2  1  28  27  26
       RD WR GND A0 INTA
  5       25    IR7
  6       24    IR6
  7       23    IR5
  8       22    IR4
  9       21    IR3
 10       20    IR2
 11       19    IR1
 12 13 14 15 16 17 18
CAS0 CAS1 GND CAS2 SP/EN INT IR0
```

## Descripción de Pines

| Pin | Símbolo | Tipo | Descripción |
|---|---|---|---|
| 28 | VCC | I | Suministro de energía +5V. Se recomienda un condensador de 0.1 µF entre los pines 28 y 14 para desacoplamiento. |
| 14 | GND | I | Tierra |
| 1 | CS | I | SELECCIÓN DE CIRCUITO: Un nivel bajo en este pin habilita las comunicaciones RD y WR entre la CPU y el 82C59A. Las funciones de INTA son independientes de CS. |
| 2 | WR | I | ESCRITURA: Un nivel bajo en este pin cuando CS es bajo habilita al 82C59A para aceptar palabras de comando desde la CPU. |
| 3 | RD | I | LECTURA: Un nivel bajo en este pin cuando CS es bajo habilita al 82C59A para liberar estado en el bus de datos para la CPU. |
| 4-11 | D7-D0 | I/O | BUS DE DATOS BIDIRECCIONAL: La información de control, estado y vector de interrupción se transfiere a través de este bus. |
| 12, 13, 15 | CAS0-CAS2 | I/O | LÍNEAS EN CASCADA: Las líneas CAS forman un bus privado del 82C59A para controlar una estructura múltiple de 82C59A. Estos pines son salidas para un 82C59A maestro y entradas para un 82C59A esclavo. |
| 16 | SP/EN | I/O | ESCLAVO PROGRAMACIÓN/BÚFER DE HABILITACIÓN: Este es un pin de función dual. En modo Buffered puede usarse como salida para controlar transceptores de búfer (EN). Cuando no está en modo Buffered se usa como entrada para designar un maestro (SP=1) o esclavo (SP=0). |
| 17 | INT | O | INTERRUPCIÓN: Este pin se pone alto siempre que se afirma una solicitud de interrupción válida. Se utiliza para interrumpir la CPU, por lo tanto, se conecta al pin de interrupción de la CPU. |
| 18-25 | IR0-IR7 | I | SOLICITUDES DE INTERRUPCIÓN: Entradas asincrónicas. Una solicitud de interrupción se ejecuta elevando una entrada IR (de bajo a alto) y manteniéndola alta hasta que sea reconocida (Modo Disparado por Flanco), o simplemente por un nivel alto en una entrada IR (Modo Disparado por Nivel). Se implementan resistencias de pull-up internas en IR0-7. |
| 26 | INTA | I | RECONOCIMIENTO DE INTERRUPCIÓN: Este pin se usa para habilitar datos de vector de interrupción del 82C59A en el bus de datos mediante una secuencia de pulsos de reconocimiento de interrupción emitidos por la CPU. |
| 27 | A0 | I | LÍNEA DE DIRECCIÓN: Este pin actúa en conjunción con los pines CS, WR y RD. Es utilizado por el 82C59A para descifrar varias palabras de comando que la CPU escribe y el estado que la CPU desea leer. Típicamente se conecta a la línea de dirección A0 de la CPU (A1 para 80C86/88/286). |

## Diagrama Funcional

```
                     INTA          INT
                                    
        DATA                        
        D7-D0    --------- 
                 BUFFER 
                 CONTROL LOGIC
                 -------- 
          IR0                REQUEST 
                 READ         IR1    
          IR2    WRITE    SERVICE     
          IR3    IN LOGIC   PRIORITY  
          IR4    LOGIC      REG       
          IR5    REG (ISR)  (IRR)     
          IR6                        
          IR7                        
                                     
       CAS0         CASCADE           
       CAS1         BUFFER      INTERRUPT MASK REG
       CAS2     COMPARATOR          (IMR)
                                     
       SP/EN                         
                                     
                       INTERNAL BUS
```

## Descripción Funcional

### Interrupciones en Sistemas de Microcomputadora

El diseño de sistemas de microcomputadora requiere que dispositivos de entrada/salida como teclados, pantallas, sensores y otros componentes reciban servicio de manera eficiente para que el microcomputador pueda asumir grandes cantidades de las tareas totales del sistema con poco o ningún efecto en el rendimiento.

El método más común para servir estos dispositivos es el enfoque de sondeo. Esto es donde el procesador debe probar cada dispositivo en secuencia y efectivamente "preguntar" a cada uno si necesita servicio. Es fácil ver que una gran parte del programa principal está pasando por este ciclo de sondeo continuo y que tal método tendría un efecto serio y perjudicial en el rendimiento del sistema, limitando así las tareas que podría asumir el microcomputador y reduciendo la rentabilidad del uso de tales dispositivos.

Un método más deseable sería uno que permitiera al microprocesador ejecutar su programa principal y solo detenerse para servir dispositivos periféricos cuando el dispositivo mismo le dice que lo haga. En efecto, el método proporcionaría una entrada asincrónica externa que informaría al procesador que debería completar cualquier instrucción que se esté ejecutando actualmente y buscar una nueva rutina que servirá al dispositivo solicitante. Una vez completado este servicio, sin embargo, el procesador resumiría exactamente donde se dejó.

Este es el método impulsado por interrupción. Es fácil ver que el rendimiento del sistema aumentaría drásticamente y, por lo tanto, el microcomputador podría asumir más tareas para mejorar aún más su rentabilidad.

### El Controlador de Interrupciones Programable (PIC)

El Controlador de Interrupciones Programable (PIC) funciona como un administrador general en un sistema impulsado por interrupción. Acepta solicitudes de equipos periféricos, determina cuál de las solicitudes entrantes es de mayor importancia (prioridad), determina si la solicitud entrante tiene un valor de prioridad más alto que el nivel siendo atendido actualmente, y emite una interrupción a la CPU basada en esta determinación.

Cada dispositivo periférico o estructura generalmente tiene un programa o "rutina" especial asociado con sus requisitos operacionales específicos; esto se refiere como una "rutina de servicio". El PIC, después de emitir una interrupción a la CPU, debe de alguna manera ingresar información en la CPU que pueda "apuntar" el contador de programa a la rutina de servicio asociada con el dispositivo solicitante. Este "puntero" es una dirección en una tabla de vectores y a menudo se conocerá, en este documento, como datos de vectorización.

### Descripción Funcional del 82C59A

El 82C59A es un dispositivo específicamente diseñado para uso en tiempo real en sistemas de microcomputadora impulsados por interrupción. Gestiona ocho niveles de solicitudes y tiene características integradas para la capacidad de expansión a otros 82C59A (hasta 64 niveles). Es programado por software del sistema como un periférico de entrada/salida. Al programador se le ofrece una selección de modos de prioridad para que la manera en que el 82C59A procesa las solicitudes pueda ser configurada para que coincida con los requisitos del sistema. Los modos de prioridad pueden ser cambiados o reconfigurados dinámicamente en cualquier momento durante la operación del programa principal. Esto significa que la estructura de interrupción completa puede ser definida como se requiera, basada en el entorno total del sistema.

### Registro de Solicitud de Interrupción (IRR) e Registro en Servicio (ISR)

Las interrupciones en las líneas de entrada IR son manejadas por dos registros en cascada, el Registro de Solicitud de Interrupción (IRR) y el Registro en Servicio (ISR). El IRR se usa para indicar todos los niveles de interrupción que solicitan servicio, y el ISR se usa para almacenar todos los niveles de interrupción que se están sirviendo actualmente.

### Resolvedor de Prioridad

Este bloque de lógica determina las prioridades de los bits establecidos en el IRR. La prioridad más alta es seleccionada e ingresada en el bit correspondiente del ISR durante la secuencia INTA.

### Registro de Máscara de Interrupción (IMR)

El IMR almacena los bits que deshabilitan las líneas de interrupción a enmascarar. El IMR opera en la salida del IRR. El enmascaramiento de una entrada de prioridad más alta no afectará las líneas de solicitud de interrupción de prioridad más baja.

### Búfer en Cascada/Comparador

Este bloque de función almacena y compara los IDs de todos los 82C59A utilizados en el sistema. Los tres pines de entrada/salida asociados (CAS0-2) son salidas cuando el 82C59A se usa como maestro y son entradas cuando el 82C59A se usa como esclavo. Como maestro, el 82C59A envía el ID del dispositivo esclavo que interrumpe a las líneas CAS0-2. El esclavo, así seleccionado, enviará su dirección de subrutina preprogramada al Bus de Datos durante el siguiente pulso o dos pulsos consecutivos de INTA. (Ver sección "Cascada del 82C59A").

### Secuencia de Interrupción

**Salida de Interrupción (INT)**

Esta salida va directamente a la entrada de interrupción de la CPU. El nivel VOH en esta línea está diseñado para ser completamente compatible con los niveles de entrada 8080, 8085, 8086/88, 80C86/88, 80286 y 80C286.

**Reconocimiento de Interrupción (INTA)**

Los pulsos INTA causarán que el 82C59A libere información de vectorización en el bus de datos. El formato de estos datos depende del modo del sistema (µPM) del 82C59A.

**Búfer de Bus de Datos**

Este búfer 3-estado bidireccional de 8 bits se utiliza para interfaz el 82C59A al Bus de Datos del Sistema. Las palabras de control e información de estado se transfieren a través del Búfer de Bus de Datos.

**Lógica de Control de Lectura/Escritura**

La función de este bloque es aceptar comandos de salida de la CPU. Contiene el registro de Palabra de Comando de Inicialización (ICW) y el registro de Palabra de Comando de Operación (OCW) que almacenan los diversos formatos de control para la operación del dispositivo. Este bloque de función también permite que el estado del 82C59A sea transferido al Bus de Datos.

**Selección de Circuito (CS)**

Un nivel BAJO en esta entrada habilita el 82C59A. No ocurrirá lectura o escritura del dispositivo a menos que el dispositivo sea seleccionado.

**Escritura (WR)**

Un nivel BAJO en esta entrada habilita a la CPU para escribir palabras de comando (ICWs y OCWs) en el 82C59A.

**Lectura (RD)**

Un nivel BAJO en esta entrada habilita al 82C59A para enviar el estado del Registro de Solicitud de Interrupción (IRR), Registro en Servicio (ISR), Registro de Máscara de Interrupción (IMR), o el nivel de interrupción (en modo de sondeo) en el Bus de Datos.

**A0**

Esta señal de entrada se usa en conjunción con las señales WR y RD para escribir comandos en los diversos registros de comando, así como para leer los diversos registros de estado del circuito. Esta línea puede estar conectada directamente a una de las líneas de dirección del sistema.

### Secuencia de Eventos en Sistema 8080/8085

Estos eventos ocurren en un sistema 8080/8085:

1. Una o más de las líneas de SOLICITUD DE INTERRUPCIÓN (IR0-IR7) se elevan a alto, estableciendo el bit o bits correspondientes en el IRR.

2. El 82C59A evalúa esas solicitudes en el resolvedor de prioridad y envía una interrupción (INT) a la CPU, si es apropiado.

3. La CPU reconoce el INT y responde con un pulso INTA.

4. Al recibir un INTA desde la CPU, el bit ISR de prioridad más alto se establece, y el bit correspondiente en el IRR se reinicia. El 82C59A también liberará un código de instrucción CALL (11001101) en el bus de datos de 8 bits a través de D0-D7.

5. Esta instrucción CALL iniciará dos pulsos INTA adicionales a ser enviados al 82C59A desde la CPU.

6. Estos dos pulsos INTA permiten al 82C59A liberar su dirección de subrutina preprogramada en el bus de datos. La dirección de 8 bits inferior se libera en el primer pulso INTA y la dirección de 8 bits superior se libera en el segundo pulso INTA.

7. Esto completa la instrucción CALL de 3 bytes liberada por el 82C59A. En modo AEOI, el bit ISR se reinicia al final del tercer pulso INTA. De lo contrario, el bit ISR permanece establecido hasta que se emita un comando EOI apropiado al final de la secuencia de interrupción.

### Secuencia de Eventos en Sistema 80C86/88/286

Los eventos que ocurren en un sistema 80C86/88/286 son los mismos hasta el paso 4.

4. El 82C59A no impulsa el bus de datos durante el primer pulso INTA.

5. La CPU 80C86/88/286 iniciará un segundo pulso INTA. Durante este pulso INTA, el bit ISR apropiado se establece y el bit correspondiente en el IRR se reinicia. El 82C59A produce el puntero de 8 bits en el bus de datos para ser leído por la CPU.

6. Esto completa el ciclo de interrupción. En modo AEOI, el bit ISR se reinicia al final del segundo pulso INTA. De lo contrario, el bit ISR permanece establecido hasta que se emita un comando EOI apropiado al final de la subrutina de interrupción.

Si no hay solicitud de interrupción presente en el paso 4 de cualquiera de las secuencias (es decir, la solicitud fue demasiado corta), el 82C59A emitirá un nivel de interrupción 7. Si un esclavo es programado en el bit IR 7, las líneas CAS permanecen inactivas y las direcciones de vector se emiten desde el 82C59A maestro.

## Salidas de Secuencia de Interrupción

### Modo de Respuesta de Interrupción 8080, 8085

Esta secuencia está sincronizada por tres pulsos INTA. Durante el primer pulso INTA, el código de operación CALL es habilitado en el bus de datos.

**Datos del Primer Byte de Vector de Interrupción: Hex CD**

| Datos | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| Código de Llamada | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 1 |

Durante el segundo pulso INTA, la dirección inferior del programa de servicio apropiado es habilitada en el bus de datos.

Cuando interval = 4 bits, A5-A7 son programados, mientras que A0-A4 son automáticamente insertados por el 82C59A. Cuando interval = 8, solo A6 y A7 son programados, mientras que A0-A5 son automáticamente insertados.

**Contenido del Segundo Byte de Vector de Interrupción (Intervalo = 4)**

| IR | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 7 | A7 | A6 | A5 | 1 | 1 | 1 | 0 | 0 |
| 6 | A7 | A6 | A5 | 1 | 1 | 0 | 0 | 0 |
| 5 | A7 | A6 | A5 | 1 | 0 | 1 | 0 | 0 |
| 4 | A7 | A6 | A5 | 1 | 0 | 0 | 0 | 0 |
| 3 | A7 | A6 | A5 | 0 | 1 | 1 | 0 | 0 |
| 2 | A7 | A6 | A5 | 0 | 1 | 0 | 0 | 0 |
| 1 | A7 | A6 | A5 | 0 | 0 | 1 | 0 | 0 |
| 0 | A7 | A6 | A5 | 0 | 0 | 0 | 0 | 0 |

**Contenido del Segundo Byte de Vector de Interrupción (Intervalo = 8)**

| IR | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 7 | A7 | A6 | 1 | 1 | 1 | 0 | 0 | 0 |
| 6 | A7 | A6 | 1 | 1 | 0 | 0 | 0 | 0 |
| 5 | A7 | A6 | 1 | 0 | 1 | 0 | 0 | 0 |
| 4 | A7 | A6 | 1 | 0 | 0 | 0 | 0 | 0 |
| 3 | A7 | A6 | 0 | 1 | 1 | 0 | 0 | 0 |
| 2 | A7 | A6 | 0 | 1 | 0 | 0 | 0 | 0 |
| 1 | A7 | A6 | 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | A7 | A6 | 0 | 0 | 0 | 0 | 0 | 0 |

Durante el tercer pulso INTA, la dirección superior del programa de servicio apropiado, que fue programado como byte 2 de la secuencia de inicialización (A8-A15), es habilitada en el bus.

**Contenido del Tercer Byte de Vector de Interrupción**

| Bit | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| Dirección | A15 | A14 | A13 | A12 | A11 | A10 | A9 | A8 |

### Modo de Respuesta de Interrupción 80C86, 80C88, 80C286

El modo 80C86/88/286 es similar al modo 8080/85 excepto que solo dos ciclos de Reconocimiento de Interrupción son emitidos por el procesador y no se envía código de operación CALL al procesador. El primer ciclo de reconocimiento de interrupción es similar al de sistemas 8080/85 en que el 82C59A lo usa para congelar internamente el estado de las interrupciones para resolución de prioridad y, como maestro, emite el código de interrupción en las líneas en cascada. En este primer ciclo, no emite ningún dato al procesador y deja sus búferes de bus de datos deshabilitados. En el segundo ciclo de reconocimiento de interrupción en modo 86/88/286, el maestro (o esclavo si es programado así) enviará un byte de datos al procesador con el código de interrupción reconocido compuesto como se indica a continuación (nota el estado del control de modo ADI es ignorado y A5-A11 no se utilizan en modo 86/88/286).

**Contenido del Byte de Vector de Interrupción para Sistema 80C86/88/286**

| IR | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 7 | T7 | T6 | T5 | T4 | T3 | 1 | 1 | 1 |
| 6 | T7 | T6 | T5 | T4 | T3 | 1 | 1 | 0 |
| 5 | T7 | T6 | T5 | T4 | T3 | 1 | 0 | 1 |
| 4 | T7 | T6 | T5 | T4 | T3 | 1 | 0 | 0 |
| 3 | T7 | T6 | T5 | T4 | T3 | 0 | 1 | 1 |
| 2 | T7 | T6 | T5 | T4 | T3 | 0 | 1 | 0 |
| 1 | T7 | T6 | T5 | T4 | T3 | 0 | 0 | 1 |
| 0 | T7 | T6 | T5 | T4 | T3 | 0 | 0 | 0 |

## Programación del 82C59A

### Introducción

El 82C59A acepta dos tipos de palabras de comando generadas por la CPU:

1. **Palabras de Comando de Inicialización (ICWs):** Antes de que pueda comenzar la operación normal, cada 82C59A en el sistema debe ser llevado a un punto de partida mediante una secuencia de 2 a 4 bytes regulados por pulsos WR.

2. **Palabras de Comando de Operación (OCWs):** Estas son las palabras de comando que ordenan al 82C59A que opere en varios modos de interrupción. Entre estos modos están:
   - a. Modo completamente anidado
   - b. Modo de prioridad rotativa
   - c. Modo de máscara especial
   - d. Modo de sondeo

Las OCW pueden ser escritas en el 82C59A en cualquier momento después de la inicialización.

### Palabras de Comando de Inicialización 1 y 2 (ICW1, ICW2)

A5-A15: Dirección de página inicial de rutinas de servicio. En un sistema 8080/85, los 8 niveles de solicitud generarán LLAMADAS a 8 ubicaciones igualmente espaciadas en memoria. Estas pueden ser programadas para estar espaciadas en intervalos de 4 u 8 ubicaciones de memoria, por lo tanto, las 8 rutinas ocuparán una página de 32 o 64 bytes, respectivamente.

### Formato ICW1

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 0 | A7 | A6 | A5 | 1 | LTIM | ADI | SNGL | IC4 |

**Descripción de Bits:**
- IC4: 1 = ICW4 necesario; 0 = ICW4 no necesario
- SNGL: 1 = Simple; 0 = Modo en cascada
- ADI: Intervalo de dirección de LLAMADA; 1 = Intervalo de 4; 0 = Intervalo de 8
- LTIM: 1 = Modo disparado por nivel; 0 = Modo disparado por flanco
- A7-A5: de Dirección de vector de interrupción (solo modo MCS-80/85)

### Formato ICW2

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 1 | A15 (o T7) | A14 (o T6) | A13 (o T5) | A12 (o T4) | A11 (o T3) | A10 (o T2) | A9 (o T1) | A8 (o T0) |

**Descripción de Bits:**
- A15-A8: de Dirección de vector de interrupción (modo MCS-80/85)
- T7-T3: de Dirección de vector de interrupción (modo 8086/8088)

### Formato ICW3 - Dispositivo Maestro

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 1 | S7 | S6 | S5 | S4 | S3 | S2 | S1 | S0 |

**Descripción de Bits:**
- S7-S0: 1 = La entrada IR tiene un esclavo; 0 = La entrada IR no tiene esclavo

### Formato ICW3 - Dispositivo Esclavo

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 0 | 0 | ID2 | ID1 | ID0 |

**Descripción de Bits:**
- ID2-ID0: ID del Esclavo

| ID Esclavo | Código Binario |
|---|---|
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

### Formato ICW4

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | SFNM | BUF | M/S | AEOI | µPM |

**Descripción de Bits:**
- µPM: 1 = Modo 8086/8088; 0 = Modo MCS-80/85
- AEOI: 1 = Modo Fin Automático de Interrupción; 0 = Fin Normal de Interrupción
- M/S: Si se selecciona modo buffered: M/S = 1 significa que el 82C59A es programado como maestro; M/S = 0 significa esclavo. Si BUF = 0, M/S no tiene función.
- BUF: 0X = Modo no buffered; 1 0 = Modo buffered esclavo; 1 1 = Modo buffered maestro
- SFNM: 1 = Modo completamente anidado especial; 0 = Modo completamente anidado normal

### Especificaciones de Dirección

La dirección tiene formato de 2 bytes (A0-A15). Cuando el intervalo de rutina es 4, A0-A4 son automáticamente insertados por el 82C59A, mientras que A5-A15 son programados externamente. Cuando el intervalo de rutina es 8, A0-A5 son automáticamente insertados por el 82C59A mientras que A6-A15 son programados externamente.

El intervalo de 8 bytes mantendrá compatibilidad con software actual, mientras que el intervalo de 4 bytes es mejor para una tabla de saltos compacta.

En un sistema 80C86/88/286, A15-A11 son insertados en los cinco bits más significativos del byte de vectorización y el 82C59A establece los tres bits menos significativos de acuerdo con el nivel de interrupción. A10-A5 son ignorados y ADI no tiene efecto.

- LTIM: Si LTIM = 1, entonces el 82C59A operará en modo de interrupción por nivel. La lógica de detección de flanco en las entradas de interrupción será deshabilitada.
- ADI: Intervalo de dirección ALL. Si ADI = 1 entonces intervalo = 4; si ADI = 0 entonces intervalo = 8.
- SNGL: Simple. Significa que este es el único 82C59A en el sistema. Si SNGL = 1, no se emitirá ICW3.
- IC4: Si este bit está establecido - debe emitirse ICW4. Si ICW4 no es necesario, establecer IC4 = 0.

### Palabra de Comando de Inicialización 3 (ICW3)

Esta palabra es leída solo cuando hay más de un 82C59A en el sistema y se utiliza cascada, en cuyo caso SNGL = 0. Cargará el registro esclavo de 8 bits. Las funciones de este registro son:

a. En modo maestro (ya sea cuando SP = 1, o en modo buffered cuando M/S = 1 en ICW4), se establece un "1" para cada esclavo en el bit correspondiente a la línea IR apropiada para el esclavo. El maestro luego liberará el byte 1 de la secuencia de llamada (para sistema 8080/85) y habilitará el esclavo correspondiente para liberar los bytes 2 y 3 (para 80C86/88/286, solo byte 2) a través de las líneas en cascada.

b. En modo esclavo (ya sea cuando SP = 0, o si BUF = 1 y M/S = 0 en ICW4), los bits 2-0 identifican al esclavo. El esclavo compara su entrada en cascada con estos bits y si son iguales, los bytes 2 y 3 de la secuencia de llamada (o solo byte 2 para 80C86/88/286) son liberados por él en el Bus de Datos.

**Nota:** (La dirección del esclavo debe corresponder a la línea IR a la que está conectado en la identificación del maestro).

### Palabra de Comando de Inicialización 4 (ICW4)

- SFNM: Si SFNM = 1, el modo completamente anidado especial es programado.
- BUF: Si BUF = 1, el modo buffered es programado. En modo buffered, SP/EN se convierte en una salida de habilitación y la determinación maestro/esclavo es por M/S. Este modo es entrado después de inicialización a menos que otro modo sea programado. Las solicitudes de interrupción son ordenadas en prioridad del 0 al 7 (0 más alto). Cuando una interrupción es reconocida, la solicitud de prioridad más alta es determinada y su vector colocado en el bus. Además, un bit del registro de Servicio de Interrupción (IS0-7) es establecido.
- M/S: Si se selecciona modo buffered: M/S = 1 significa que el 82C59A es programado como maestro; M/S = 0 significa esclavo. Si BUF = 0, M/S no tiene función.
- AEOI: Si AEOI = 1, el modo automático de fin de interrupción es programado.
- µPM: Modo de Microprocesador: µPM = 0 establece el 82C59A para operación de sistema 8080/85; µPM = 1 establece el 82C59A para operación de sistema 80C86/88/286.

## Palabras de Comando de Operación (OCWs)

Después de que las Palabras de Comando de Inicialización (ICWs) son programadas en el 82C59A, el dispositivo está listo para aceptar solicitudes de interrupción en sus líneas de entrada. Sin embargo, durante la operación del 82C59A, se puede seleccionar una selección de algoritmos que ordenan al 82C59A que opere en varios modos a través de las Palabras de Comando de Operación (OCWs).

### Formato de Operación de Palabras de Comando

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| **OCW1** | 1 | M7 | M6 | M5 | M4 | M3 | M2 | M1 | M0 |

### Palabra de Comando de Operación 1 (OCW1)

OCW1 establece y reinicia los bits de máscara en el Registro de Máscara de Interrupción (IMR). M7-M0 representan los ocho bits de máscara. M = 1 indica que el canal está enmascarado (inhibido); M = 0 indica que el canal está habilitado.

### Formato OCW2

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 0 | R | SL | EOI | 0 | 0 | L2 | L1 | L0 |

**R, SL, EOI:** Estos tres bits controlan los modos Rotación y Fin de Interrupción y combinaciones de los dos.

**L2, L1, L0:** Estos bits determinan el nivel de interrupción actuado cuando el bit SL está activo.

### Tabla de Función OCW2

| R | SL | EOI | L2:L1:L0 | Función |
|---|---|---|---|---|
| 0 | 0 | 1 | x:x:x | Comando EOI no específico |
| 0 | 1 | 1 | 0:1:0 | Comando EOI específico |
| 1 | 0 | 1 | x:x:x | Comando Rotar en EOI no específico |
| 1 | 0 | 0 | x:x:x | Comando Rotar en modo EOI automático (establecer) |
| 0 | 0 | 0 | x:x:x | Comando Rotar en modo EOI automático (reiniciar) |
| 1 | 1 | 1 | x:x:x | Comando Rotar en EOI específico |
| 1 | 1 | 0 | x:x:x | Comando Establecer Prioridad |
| 0 | 1 | 0 | x:x:x | Operación nula |

### Formato OCW3

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 0 | 0 | ESMM | SMM | 0 | 1 | P | RR | RIS |

**ESMM:** Habilitar Modo de Máscara Especial. Cuando este bit está establecido a 1, habilita el bit SMM para establecer o reiniciar el Modo de Máscara Especial. Cuando ESMM = 0, el bit SMM se convierte en "sin importancia".

**SMM:** Modo de Máscara Especial. Si ESMM = 1 y SMM = 1, el 82C59A entrará en Modo de Máscara Especial. Si ESMM = 1 y SMM = 0, el 82C59A revertirá al modo de máscara normal. Cuando ESMM = 0, SMM no tiene efecto.

### Tabla de Comando de Lectura de Registro

| RR | RIS | Función |
|---|---|---|
| 0 | 1 | Leer registro IR en siguiente pulso RD |
| 0 | 1 | Leer registro IS en siguiente pulso RD |
| x | x | Sin acción |

**P:** 1 = Comando de sondeo; 0 = Sin comando de sondeo

### Tabla de Modo de Máscara Especial

| ESMM | SMM | Función |
|---|---|---|
| 0 | 1 | Reiniciar máscara especial |
| 0 | 1 | Establecer máscara especial |
| x | x | Sin acción |

## Modo Completamente Anidado

Este modo es entrado después de la inicialización a menos que otro modo sea programado. Las solicitudes de interrupción son ordenadas en prioridad del 0 al 7 (0 más alto). Cuando una interrupción es reconocida, la solicitud de prioridad más alta es determinada y su vector colocado en el bus. Además, un bit del registro de Servicio de Interrupción (IS0-7) es establecido. Este bit permanece establecido hasta que el microprocesador emita un comando Fin de Interrupción (EOI) inmediatamente antes de retornar de la rutina de servicio, o si el bit AEOI (Fin Automático de Interrupción) está establecido, hasta el borde final del último INTA. Mientras el bit IS está establecido, todas las interrupciones futuras de la misma prioridad o inferior son inhibidas, mientras que los niveles superiores generarán una interrupción (que será reconocida solo si el flip-flop de habilitación de interrupción interno del microprocesador ha sido re-habilitado a través de software).

### Tabla OCW1

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 1 | M7 | M6 | M5 | M4 | M3 | M2 | M1 | M0 |

Máscara de Interrupción:
- 1 = Máscara establecida
- 0 = Máscara reiniciada

### Tabla OCW2

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 0 | R | SL | EOI | 0 | 0 | L2 | L1 | L0 |

**Nivel de IR a Ser Actuado**

| | | | | | | | |
|---|---|---|---|---|---|---|---|
| L2 | 0 | 1 | 0 | 1 | 0 | 1 | 0 | 1 |
| L1 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 |
| L0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 |
| IR | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

### Tabla OCW3

| A0 | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| 0 | 0 | ESMM | SMM | 0 | 1 | P | RR | RIS |

**Comando de Lectura de Registro**

| RR | RIS | Función |
|---|---|---|
| 0 | 1 | Leer registro IR en siguiente pulso RD |
| 0 | 1 | Leer registro IS en siguiente pulso RD |
| x | x | Sin acción |

**Comando de Sondeo**
- 1 = Comando de sondeo
- 0 = Sin comando de sondeo

**Tabla de Modo de Máscara Especial**

| ESMM | SMM | Función |
|---|---|---|
| 0 | 1 | Reiniciar máscara especial |
| 0 | 1 | Establecer máscara especial |
| x | x | Sin acción |

## Fin de Interrupción (EOI)

El bit en Servicio (IS) puede ser reiniciado ya sea automáticamente después del borde final del último pulso INTA en secuencia (cuando el bit AEOI en lCW1 está establecido) o por una palabra de comando que debe ser emitida al 82C59A antes de retornar de una rutina de servicio (Comando EOI). Un comando EOI debe ser emitido dos veces si se sirve un esclavo en modo Cascada, una vez para el maestro y una vez para el esclavo correspondiente.

Hay dos formas de comando EOI: Específico y No Específico. Cuando el 82C59A es operado en modos que preservan la estructura completamente anidada, puede determinar cuál bit IS debe ser reiniciado en EOI. Cuando se emite un comando No Específico, el 82C59A reiniciará automáticamente el bit IS más alto de aquellos que están establecidos, ya que en modo completamente anidado el nivel IS más alto fue necesariamente el último nivel reconocido y atendido. Un EOI no específico puede ser emitido con OCW2 (EOI = 1, SL = 0, R = 0).

Cuando se utiliza un modo que puede perturbar la estructura completamente anidada, el 82C59A puede no ser capaz de determinar el último nivel reconocido. En este caso, debe ser emitido un Fin de Interrupción Específico que incluya como parte del comando el nivel IS a ser reiniciado. Un EOI específico puede ser emitido con OCW2 (EOI = 1, SL = 1, R = 0, y L0-L2 es el nivel binario del bit IS a ser reiniciado).

Un bit IRR que está enmascarado por un bit IMR no será reiniciado por un EOI no específico si el 82C59A está en Modo de Máscara Especial.

### Rotación Automática (Dispositivos de Prioridad Igual)

En algunas aplicaciones hay un número de dispositivos que interrumpen de prioridad igual. En este modo, un dispositivo, después de ser atendido, recibe la prioridad más baja, por lo que un dispositivo solicitando una interrupción tendrá que esperar, en el peor de los casos, hasta que cada uno de los 7 otros dispositivos sea atendido al menos una vez.

Por ejemplo, si el estado de prioridad e "en servicio" es:

**Antes de Rotación (IR4 es la prioridad más alta requerida siendo servida)**

| Estado IS | IS7 | IS6 | IS5 | IS4 | IS3 | IS2 | IS1 | IS0 |
|---|---|---|---|---|---|---|---|---|
| | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 |
| Estado de Prioridad | 2 | 1 | 0 | 7 | 6 | 5 | 4 | 3 |
| | más bajo | | | | | | | más alto |

**Después de Rotación (IR4 fue atendido, todas las otras prioridades rotadas correspondientemente)**

| Estado IS | IS7 | IS6 | IS5 | IS4 | IS3 | IS2 | IS1 | IS0 |
|---|---|---|---|---|---|---|---|---|
| | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| Estado de Prioridad | 2 | 1 | 0 | 7 | 6 | 5 | 4 | 3 |
| | más alto | | | | | | | más bajo |

Hay dos maneras de lograr Rotación Automática usando OCW2, la Rotación en Comando EOI No Específico (R = 1, SL = 0, EOI = 1) y la Rotación en Modo EOI Automático que es establecida por (R = 1, SL = 0, EOI = 0) y reiniciada por (R = 0, SL = 0, EOI = 0).

### Rotación Específica (Prioridad Específica)

El programador puede cambiar prioridades programando la prioridad más baja y así fijando todas las demás prioridades; es decir, si IR5 es programado como el dispositivo de prioridad más baja, entonces IR6 tendrá la más alta.

El comando Establecer Prioridad es emitido en OCW2 donde: R = 1, SL = 1, L0-L2 es el código de nivel de prioridad binario del dispositivo de prioridad más baja.

Observe que en este modo el estado interno es actualizado por control de software durante OCW2. Sin embargo, es independiente del comando Fin de Interrupción (EOI) (también ejecutado por OCW2).

Los cambios de prioridad pueden ser ejecutados durante un comando EOI usando el comando Rotar en EOI Específico en OCW2 (R = 1, SL = 1, EOI = 1, y L0-L2 = nivel IR para recibir prioridad más baja).

### Máscaras de Interrupción

Cada entrada de Solicitud de Interrupción puede ser enmascarada individualmente por el Registro de Máscara de Interrupción (IMR) programado a través de OCW1. Cada bit en el IMR enmascara un canal de interrupción si está establecido (1). El bit 0 enmascara IR0, El bit 1 enmascara IR1, y así sucesivamente. El enmascaramiento de un canal IR no afecta la operación de otros canales.

### Modo de Máscara Especial

Algunas aplicaciones pueden requerir que una rutina de servicio de interrupción altere dinámicamente la estructura de prioridad del sistema durante su ejecución bajo control de software. Por ejemplo, la rutina puede desear inhibir solicitudes de prioridad más baja durante una porción de su ejecución pero habilitar algunas de ellas para otra porción.

La dificultad aquí es que si se reconoce una Solicitud de Interrupción y un comando Fin de Interrupción no reinicia su bit IS (es decir, mientras se ejecuta una rutina de servicio), el 82C59A habría inhibido todas las solicitudes de prioridad más baja sin una manera fácil para que la rutina las habilite.

Aquí es donde el Modo de Máscara Especial entra. En el Modo de Máscara Especial, cuando un bit de máscara es establecido en OCW1, inhibe más interrupciones en ese nivel e habilita interrupciones de todos los demás niveles (más bajos así como más altos) que no están enmascarados. Por lo tanto, cualquier interrupción puede ser selectivamente habilitada cargando el registro de máscara.

El Modo de Máscara Especial es establecido por OCW3 donde: ESMM = 1, SMM = 1, y reiniciado donde ESMM = 1, SMM = 0.

### Comando de Sondeo

En este modo, la salida INT no es usada o el flip-flop de Habilitación de Interrupción interno del microprocesador está reiniciado, deshabilitando su entrada de interrupción. El servicio a dispositivos es logrado por software usando un comando de Sondeo. El comando de Sondeo es emitido estableciendo P = 1 en OCW3. El 82C59A trata el siguiente pulso RD al 82C59A (es decir, RD = 0, CS = 0) como un reconocimiento de interrupción, establece el bit IS apropiado si hay una solicitud, y lee el nivel de prioridad. La interrupción es congelada desde WR a RD.

La palabra habilitada en el bus de datos durante RD es:

| Bit | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|
| | I | - | - | - | - | W2 | W1 | W0 |

**W0-W2:** Código binario del nivel de solicitud de prioridad más alto requerido servicio.
**I:** Igual a un "1" si hay una interrupción.

Este modo es útil si hay una rutina de comando común para varios niveles para que la secuencia INTA no sea necesaria (ahorran espacio ROM). Otra aplicación es usar el modo de sondeo para expandir el número de niveles de prioridad a más de 64.

## Lectura del Estado del 82C59A

La entrada estado de varios registros internos puede ser leída para actualizar la información del usuario en el sistema. Los siguientes registros pueden ser leídos vía OCW3 (IRR e ISR) u OCW1 (IMR).

**Registro de Solicitud de Interrupción (IRR):** Registro de 8 bits que contiene los niveles que solicitan que una interrupción sea reconocida. El nivel de solicitud más alto es reiniciado desde el IRR cuando una interrupción es reconocida. IRR no es afectado por IMR.

**Registro en Servicio (ISR):** Registro de 8 bits que contiene los niveles de prioridad que están siendo atendidos. El ISR es actualizado cuando se emite un Comando Fin de Interrupción.

**Registro de Máscara de Interrupción:** Registro de 8 bits que contiene las líneas de solicitud de interrupción que están enmascaradas.

- El IRR puede ser leído cuando, anterior al pulso RD, se emite un Comando de Lectura de Registro con OCW3 (RR = 1, RIS = 0).
- El ISR puede ser leído cuando, anterior al pulso RD, se emite un Comando de Lectura de Registro con OCW3 (RR = 1, RIS = 1).

No hay necesidad de escribir un OCW3 antes de cada operación de lectura de estado, siempre que la lectura de estado corresponda con la anterior: es decir, el 82C59A "recuerda" si el IRR o ISR han sido previamente seleccionados por el OCW3. Esto no es cierto cuando se utiliza sondeo. En el modo de sondeo, el 82C59A trata la RD siguiente a una operación de "escritura de sondeo" como un INTA. Después de la inicialización, el 82C59A está establecido a IRR.

Para leer el IMR, no se necesita OCW3. El búfer de bus de datos de salida contendrá el IMR siempre que RD esté activo y A0 = 1 (OCW1).

El sondeo anula la lectura de estado cuando P = 1, RR = 1 en OCW3.

## Modos Disparados por Flanco y Nivel

Este modo es programado usando bit 3 en lCW1.

Si LTlM = "0", una solicitud de interrupción será reconocida por una transición de bajo a alto en una entrada IR. La entrada IR puede permanecer alta sin generar otra interrupción.

Si LTIM = "1", una solicitud de interrupción será reconocida por un nivel "alto" en una entrada IR, y no hay necesidad de detección de flanco. La solicitud de interrupción debe ser removida antes de que se emita el comando EOI o la interrupción de la CPU sea habilitada para prevenir una segunda interrupción de ocurrir.

El diagrama de célula de prioridad muestra un circuito conceptual de la circuitería de entrada sensible a nivel y sensible a flanco del 82C59A. Asegúrese de notar que el pestillo de solicitud es un pestillo D tipo transparente.

En los modos disparados por flanco y nivel, las entradas IR deben permanecer altas hasta después del borde de caída del primer INTA. Si la entrada IR baja antes de este tiempo, ocurrirá un IR7 PREDETERMINADO cuando la CPU reconozca la interrupción. Esto puede ser un salvaguardia útil para detectar interrupciones causadas por ruido espurio en las entradas IR. Para implementar esta característica, la rutina IR7 es usada para "limpiar" simplemente ejecutando una instrucción de retorno, ignorando así la interrupción. Si IR7 es necesario para otros propósitos, un IR7 predeterminado aún puede ser detectado leyendo el ISR. Una interrupción IR7 normal establecerá el bit ISR correspondiente, un IR7 predeterminado no lo hará. Si ocurre una interrupción IR7 predeterminada durante una rutina IR7 normal, sin embargo, el ISR permanecerá establecido. En este caso es necesario mantener un seguimiento de si se ingresó previamente a la rutina IR7. Si ocurre otro IR7, es un predeterminado.

En aplicaciones sensibles a potencia, es aconsejable colocar el 82C59A en modo disparado por flanco con las líneas IR normalmente altas. Esto minimizará la corriente a través de las resistencias de pull-up internas en los pines IR.

## Modo Completamente Anidado Especial

Este modo será utilizado en el caso de un sistema grande donde se utiliza cascada, y la prioridad debe ser conservada dentro de cada esclavo. En este caso, el modo completamente anidado especial será programado al maestro (usando lCW4). Este modo es similar al modo anidado normal con las siguientes excepciones:

a. Cuando una solicitud de interrupción de un cierto esclavo está en servicio, este esclavo no es bloqueado del maestro y se pueden reconocer más solicitudes de interrupción de IR de prioridad más alta dentro del esclavo por el maestro e iniciarán interrupciones al procesador. (En el modo anidado normal, un esclavo está enmascarado cuando su solicitud está en servicio y no se pueden servir solicitudes más altas del mismo esclavo.)

b. Al salir de la rutina de Servicio de Interrupción, el software debe verificar si la interrupción atendida fue la única del esclavo. Esto se hace enviando un comando Fin de Interrupción (EOI) no específico al esclavo y luego leyendo su registro En Servicio y verificando cero. Si está vacío, se puede enviar un EOI no especificado al maestro también. Si no, no se debe enviar EOI.

## Modo Buffered

Cuando el 82C59A es utilizado en un sistema grande donde se requieren búferes de conducción de bus en el bus de datos y se utiliza modo de cascada, existe el problema de habilitar búferes. El modo buffered estructurará el 82C59A para enviar una señal de habilitación en SP/EN para habilitar los búferes. En este modo, siempre que las salidas del bus de datos del 82C59A sean habilitadas, la salida SP/EN se vuelve activa.

Esta modificación obliga al uso de la programación de software para determinar si el 82C59A es un maestro o un esclavo. El bit 3 en ICW4 programa el modo buffered, y el bit 2 en lCW4 determina si es un maestro o un esclavo.

## Modo en Cascada

El 82C59A puede ser fácilmente interconectado en un sistema de un maestro con hasta ocho esclavos para manejar hasta 64 niveles de prioridad. El maestro controla los esclavos a través del bus de cascada de 3 líneas (CAS2-0). El bus de cascada actúa como selecciones de chip a los esclavos durante la secuencia INTA. Las líneas en cascada del 82C59A maestro están activas solo para entradas esclavo, las entradas no esclavo dejan la línea de cascada inactiva (baja). Por lo tanto, es necesario usar una dirección de esclavo de 0 (cero) solo después de que todas las demás direcciones sean utilizadas.

En una configuración en cascada, las salidas de interrupción del esclavo (INT) están conectadas a las entradas de solicitud de interrupción del maestro. Cuando se activa una línea de solicitud del esclavo y luego es reconocida, el maestro habilitará el esclavo correspondiente para liberar la dirección de rutina de dispositivo durante los bytes 2 y 3 de INTA. (Solo byte 2 para 80C86/88/286).

Las líneas del bus de cascada normalmente son bajas y contendrán el código de dirección del esclavo desde el borde inicial del primer pulso INTA hasta el borde final del último pulso INTA. Cada 82C59A en el sistema debe seguir una secuencia de inicialización separada y puede ser programado para trabajar en un modo de prioridad diferente. Un comando EOI debe ser emitido dos veces: una vez para el maestro y una vez para el esclavo correspondiente. Se requiere decodificación de selección de circuito para activar cada 82C59A.

**Nota:** Auto EOI es soportado en el modo esclavo para el 82C59A.

## Especificaciones Absolutas Máximas

| Parámetro | Mínimo | Máximo | Unidad |
|---|---|---|---|
| Voltaje de Suministro | - | +8.0 | V |
| Voltaje de Entrada, Salida o E/S | -GND-0.5 | +VCC+0.5 | V |
| Clasificación ESD | - | Clase I | - |

## Información Térmica (Típica)

| Tipo de Paquete | θJA (°C/W) | θJC (°C/W) |
|---|---|---|
| CERDIP | 55 | 12 |
| CLCC | 65 | 14 |
| PDIP | 55 | N/A |
| PLCC | 65 | N/A |
| SOIC | 75 | N/A |

## Condiciones de Operación

| Parámetro | Valor | Unidad |
|---|---|---|
| Rango de Voltaje de Operación | +4.5 a +5.5 | V |
| Rango de Temperatura de Almacenamiento | -65 a +150 | °C |
| Rango de Temperatura de Operación | -55 a +125 | °C |
| Voltaje Bajo de Entrada | 0 a +0.8 | V |
| Temperatura Máxima de Unión Paquete Cerámica | +175 | °C |
| Temperatura Máxima de Unión Paquete Plástico | +150 | °C |
| Temperatura Máxima de Plomo Paquete (Soldadura 10s) (PLCC y SOIC - Solo Puntas de Plomo) | +300 | °C |

## Características del Dado

| Parámetro | Valor |
|---|---|
| Conteo de Puertas | 1250 Puertas |

## Especificaciones Eléctricas DC

VCC = +5.0V ± 10%, TA = 0°C a +70°C (C82C59A), TA = -40°C a +85°C (I82C59A), TA = -55°C a +125°C (M82C59A)

| Símbolo | Parámetro | Mín | Máx | Unidad | Condiciones de Prueba |
|---|---|---|---|---|---|
| VIH | Voltaje de Entrada Lógico Uno | 2.0 (C82C59A, I82C59A); 2.2 (M82C59A) | - | V | - |
| VIL | Voltaje de Entrada Lógico Cero | - | 0.8 | V | - |
| VOH | Voltaje ALTO de Salida | 3.0 (IOH = -2.5mA); VCC-0.4 (IOH = -100 mA) | - | V | - |
| VOL | Voltaje BAJO de Salida | - | 0.4 | V | IOL = +2.5 mA |
| II | Corriente de Fuga de Entrada | -1.0 | +1.0 | µA | VIN = GND o VCC, Pines 1-3, 26-27 |
| IO | Corriente de Fuga de Salida | -10.0 | +10.0 | µA | VOUT = GND o VCC, Pines 4-13, 15-16 |
| ILIR | Corriente de Carga de Entrada IR | - | -200 (VIN = 0V); -10 (VIN = VCC) | µA | - |
| ICCSB | Corriente de Suministro de Potencia Standby | - | 10 | µA | VCC = 5.5V, VIN = VCC o GND, Salidas Abiertas, (Nota 1) |
| ICCOP | Corriente de Suministro de Potencia de Operación | - | 1 | mA/MHz | VCC = 5.0V, VIN = VCC o GND, Salidas Abiertas, TA = 25°C, (Nota 2) |

### Notas

1. Excepto para IR0-lR7 donde VIN = VCC o abierto.
2. ICCOP = 1 mA/MHz del tiempo de ciclo de lectura/escritura periférica. (ejemplo: tiempo de ciclo de lectura/escritura de E/S de 1.0 µs = 1 mA).

## Capacitancia

TA = +25°C

| Símbolo | Parámetro | Típico | Unidad | Condiciones de Prueba |
|---|---|---|---|---|
| CIN | Capacitancia de Entrada | 15 | pF | FREQ = 1 MHz, todas las mediciones referenciadas al GND del dispositivo. |
| COUT | Capacitancia de Salida | 15 | pF | - |
| CI/O | Capacitancia de E/S | 15 | pF | - |

## Especificaciones Eléctricas AC

VCC = +5.0V ± 10%, GND = 0V, TA = 0°C a +70°C (C82C59A), TA = -40°C a +85°C (I82C59A), TA = -55°C a +125°C (M82C59A)

### Requisitos de Tiempo

| Símbolo | Parámetro | 82C59A-5 |  | 82C59A |  | 82C59A-12 |  | Unidad | Condiciones de Prueba |
|---|---|---|---|---|---|---|---|---|---|
|  |  | Mín | Máx | Mín | Máx | Mín | Máx |  |  |
| (1) TAHRL | Configuración A0/CS a RD/INTA | 10 | - | 10 | - | 5 | - | ns | - |
| (2) TRHAX | Retención A0/CS después de RD/INTA | 5 | - | 5 | - | 0 | - | ns | - |
| (3) TRLRH | Ancho de Pulso RD/INTA | 235 | - | 160 | - | 60 | - | ns | - |
| (4) TAHWL | Configuración A0/CS a WR | 0 | - | 0 | - | 0 | - | ns | - |
| (5) TWHAX | Retención A0/CS después de WR | 5 | - | 5 | - | 0 | - | ns | - |
| (6) TWLWH | Ancho de Pulso WR | 165 | - | 95 | - | 60 | - | ns | - |
| (7) TDVWH | Configuración de Datos a WR | 240 | - | 160 | - | 70 | - | ns | - |
| (8) TWHDX | Retención de Datos después de WR | 5 | - | 5 | - | 0 | - | ns | - |
| (9) TJLJH | Ancho Bajo de Solicitud de Interrupción | 100 | - | 100 | - | 40 | - | ns | - |
| (10) TCVIAL | Configuración de Cascada a Segundo o Tercer INTA (Solo Esclavo) | 55 | - | 40 | - | 30 | - | ns | - |
| (11) TRHRL | Fin de RD a siguiente RD, Fin de INTA (dentro de secuencia INTA solamente) | 160 | - | 160 | - | 90 | - | ns | - |
| (12) TWHWL | Fin de WR a siguiente WR | 190 | - | 190 | - | 60 | - | ns | - |
| (13) TCHCL | Fin de Comando a siguiente comando (no mismo tipo de comando), Fin de secuencia INTA a siguiente secuencia INTA | 500 | - | 400 | - | 90 | - | ns | (Nota 1) |

### Respuestas de Tiempo

| Símbolo | Parámetro | 82C59A-5 |  | 82C59A |  | 82C59A-12 |  | Unidad | Condiciones de Prueba |
|---|---|---|---|---|---|---|---|---|---|
|  |  | Mín | Máx | Mín | Máx | Mín | Máx |  |  |
| (14) TRLDV | Datos Válidos desde RD/INTA | - | 160 | - | 120 | - | 40 | ns | 1 |
| (15) TRHDZ | Datos Flotantes después de RD/INTA | 5 | 100 | 5 | 85 | 5 | 22 | ns | 2 |
| (16) TJHlH | Retardo de Salida de Interrupción | - | 350 | - | 300 | - | 90 | ns | 1 |
| (17) TlALCV | Cascada Válida desde Primer INTA (Solo Maestro) | - | 565 | - | 360 | - | 50 | ns | 1 |
| (18) TRLEL | Habilitación Activa desde RD o INTA | - | 125 | - | 100 | - | 40 | ns | 1 |
| (19) TRHEH | Habilitación Inactiva desde RD o INTA | - | 60 | - | 50 | - | 22 | ns | 1 |
| (20) TAHDV | Datos Válidos desde Dirección Estable | - | 210 | - | 200 | - | 60 | ns | 1 |
| (21) TCVDV | Cascada Válida a Datos Válidos | - | 300 | - | 200 | - | 70 | ns | 1 |

### Nota

1. El peor caso de temporización para TCHCL en un sistema actual de microprocesador es típicamente mayor que los valores especificados para el 82C59A, (es decir. 8085A = 1.6 µs, 8085A-2 = 1 µs, 80C86 = 1 µs, 80C286-10 = 131 ns, 80C286-12 = 98 ns).

## Circuito de Prueba AC

Configuración del Circuito de Prueba AC para mediciones de temporización.

| Condición de Prueba | V1 | R1 | R2 | C1 |
|---|---|---|---|---|
| 1 | 1.7V | 523Ω | Abierto | 100pF |
| 2 | VCC | 1.8kΩ | 1.8kΩ | 50pF |

## Forma de Onda de Entrada y Salida de Prueba AC

Las señales de entrada deben conmutar entre VIL - 0.4V y VIH + 0.4V. Los tiempos de subida y caída de entrada se manejan a 1 ns/V.

## Formas de Onda de Temporización

### Escritura

```
CS      ___/‾‾‾‾‾\___
A0      ___/‾‾‾‾‾\___
          (1)  (2)
         TAHWL TWHAX

WR      ___/‾‾‾‾‾\___
             (4) (5)
            TWLWH

DATA    ————X==============X————
             (6)        (7)
            TDVWH      TWHDX
```

### Lectura/INTA

```
CS      ___/‾‾‾‾‾\___
A0      ___/‾‾‾‾‾\___
        (1)  (2)
       TAHRL TRHAX

RD/INTA ___/‾‾‾‾‾\___
            (3)
          TRLRH
     (18) (19)
    TRLEL TRHEH
EN      ___/‾‾‾‾\___

DATA    ————X==============X————
           (14) (15)
          TRLDV TRHDZ
               (20)
              TAHDV
```

### Otra Temporización

```
INTA    ___/‾‾‾\___
WR      ___/‾‾‾\___
            (11)
           TRHRL
RD      ___/‾‾‾\___
              (12)
             TWHWL
INTA    ___/‾‾‾\___
WR      ___/‾‾‾\___
            (13)
           TCHCL
RD      ___/‾‾‾\___
INTA    ___/‾‾‾\___
WR      ___/‾‾‾\___
```

### Secuencia INTA

```
         (16)
        TJHIH
IR      ____/‾‾‾‾‾\____
             (9)
            TJLJH

INT     ____/‾‾‾‾‾\____

INTA    ___/‾‾‾\___/‾‾‾\___/‾‾‾\___

DB      ————X==D1==X==D2==X==D3==X————

CAS0-2  ————X==ID==X                X————
            (10)  (10)
           TCVIAL TCVIAL
                    (17)   (21)
                  TIALCV TCVDV

Notas:
1. La Solicitud de Interrupción (IR) debe permanecer ALTA hasta el borde inicial del primer INTA.
2. Durante el primer INTA, el Bus de Datos no está activo en modo 80C86/88/286.
3. Modo 80C86/88/286.
4. Modo 8080/8085.
```

## Circuitos de Prueba de Quemado

### MD82C59A CERDIP

[Configuración de quemado para pruebas de confiabilidad del dispositivo CERDIP]

Parámetros:
- VCC = 5.5V ± 0.5V
- VIH = 4.5V ± 10%
- VIL = -0.2V a 0.4V
- GND = 0V
- R1 = 47kΩ ± 5%
- R2 = 510Ω ± 5%
- R3 = 10kΩ ± 5%
- R4 = 1.2kΩ ± 5%
- C1 = 0.01 µF mín.
- F0 = 100kHz ± 10%
- F1 = F0/2, F2 = F1/2, ... F8 = F7/2

### MR82C59A CLCC

[Configuración de quemado para pruebas de confiabilidad del dispositivo CLCC]

## Características del Dado

**Dimensiones del Dado:**
- 143 x 130 x 19 ± 1 mil
- (3630 x 3310 x 525 µm)

**Metalización:**
- Tipo: Si-Al-Cu
- Espesor: Metal 1: 8 kÅ ± 0.75 kÅ
- Metal 2: 12 kÅ ± 1.0 kÅ

**Vitrificación:**
- Tipo: Nitrox
- Espesor: 10 kÅ ± 3.0 kÅ

## Disposición de Máscara de Metalización

Disposición de los elementos en la máscara de metalización del dado del 82C59A mostrando la ubicación de las conexiones de entrada/salida y la topología interna del circuito.

Copyright © Harris Corporation 1997
Marzo 1997
