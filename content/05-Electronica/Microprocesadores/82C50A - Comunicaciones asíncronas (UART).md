---
title: "82C50A - Comunicaciones asíncronas (UART)"
---

# 82C50A - Elemento de Comunicaciones Asíncronas CMOS

**Harris Semiconductor**
**Marzo de 1997**

## Características

- UART/BRG en un solo chip
- DC a 625K Baudios (Reloj de 0 a 10MHz)
- Entrada de cristal o reloj externo
- Generador de velocidad en baudios incluido (Divisor de 1 a 65535, genera reloj 16X)
- Modo de interrupción con prioridades
- Compatible completamente con TTL/CMOS
- Interfaz orientada al bus del microprocesador
- Compatible con 80C86/80C88
- Proceso CMOS Escalonado SAJI IV
- Bajo consumo de potencia (típicamente 1mA/MHz)
- Interfaz de módem
- Generación y detección de ruptura de línea
- Modos de retroalimentación y eco
- Transmisor y receptor con búfer duplicado
- Suministro único de 5V

## Descripción

El 82C50A Elemento de Comunicaciones Asíncronas (ACE) es un Receptor/Transmisor Asincrónico Universal (UART) programable de alto rendimiento y generador de velocidad en baudios (BRG) en un solo chip. Utilizando el proceso CMOS Escalonado SAJI IV avanzado de Harris Semiconductor, el ACE soportará velocidades de datos de DC a 625K baudios (reloj de 0-10MHz).

El circuito receptor del ACE convierte bits de inicio, datos, parada y paridad en una palabra de datos paralela. El circuito transmisor convierte una palabra de datos paralela en forma serie y añade los bits de inicio, paridad y parada. La longitud de la palabra es programable a 5, 6, 7 u 8 bits de datos. La selección del bit de parada ofrece una opción de 1, 1.5 o 2 bits de parada.

El generador de velocidad en baudios divide el reloj por un divisor programable de 1 a 2^16-1 para proporcionar velocidades en baudios estándar RS-232C al usar cualquiera de tres cristales estándar de la industria (1.8432MHz, 2.4576MHz o 3.072MHz).

Una salida de reloj de búfer programable (BAUDOUT) proporciona un oscilador de búfer o reloj de velocidad en baudios 16X (16 veces la velocidad de datos) para uso general del sistema.

Para cumplir con los requisitos del sistema de una CPU interfazada con un canal asincrónico, se proporcionan las señales de control de módem RTS, CTS, DSR, DTR, RI y DCD. Las entradas y salidas han sido diseñadas con compatibilidad completa TTL/CMOS para facilitar el diseño del sistema TTL/NMOS/CMOS mixto.

## Información de Pedido

| Paquete | Rango de Temperatura (°C) | Número de Pieza | Código de Paquete |
|---|---|---|---|
| PDIP | 0 a +70 | CP82C50A-5 | E40.6 |
| PDIP | -40 a +85 | IP82C50A-5 | E40.6 |
| PLCC | 0 a +70 | CS82C50A-5 | N44.65 |
| PLCC | -40 a +85 | IS82C50A-5 | N44.65 |
| CERDIP | 0 a +70 | CD82C50A-5 | F40.6 |
| CERDIP | -40 a +85 | ID82C50A-5 | F40.6 |
| CERDIP | -55 a +125 | MD82C50A-5/B | F40.6 |

## Diagrama Funcional

*Nota: El diagrama funcional original del datasheet muestra la interconexión de los bloques principales del 82C50A. La estructura incluye interfaz del microprocesador, UART completo con receptor y transmisor, generador de velocidad en baudios, control de línea, control de módem y estructura de interrupciones. Los bloques principales son: Interfaz de Microprocesador (CS0, CS1, CS2, ADS, A0, A1, A2), UART (receptor con buffer y registro de desplazamiento, transmisor con buffer y registro de desplazamiento), Generador de velocidad en baudios (con latches divisores LS y MS), Control de línea, Control de módem y Registro de estado del módem.*

## Configuración de Pines

### 82C50A (PDIP, CERDIP) - Vista Superior

| Pin | Señal | Pin | Señal |
|---|---|---|---|
| 1 | D0 | 40 | VCC |
| 2 | D1 | 39 | RI |
| 3 | D2 | 38 | DCD |
| 4 | D3 | 37 | DSR |
| 5 | D4 | 36 | CTS |
| 6 | D5 | 35 | MR |
| 7 | D6 | 34 | OUT1 |
| 8 | D7 | 33 | DTR |
| 9 | RCLK | 32 | RTS |
| 10 | SIN | 31 | OUT2 |
| 11 | SOUT | 30 | INTRPT |
| 12 | CS0 | 29 | NC |
| 13 | CS1 | 28 | A0 |
| 14 | CS2 | 27 | A1 |
| 15 | BAUDOUT | 26 | A2 |
| 16 | XTAL1 | 25 | ADS |
| 17 | XTAL2 | 24 | CSOUT |
| 18 | DOSTR | 23 | DDIS |
| 19 | DOSTR | 22 | DISTR |
| 20 | GND | 21 | DISTR |

### 82C50A (PLCC) - Vista Superior

*Nota: El diagrama PLCC original del datasheet tiene problemas de legibilidad en el OCR. La configuración general sigue el mismo esquema de 44 pines con los mismos nombres de señal. Los pines están distribuidos alrededor del perímetro del paquete PLCC.*

## Descripción de Pines

### DISTR, DISTR (Pines 22, 21)

**Tipo:** Entrada
**Nivel Activo:** H (Pin 22), L (Pin 21)

**Descripción:** Señales de strobe de lectura de datos. DISTR y DISTR son entradas que causan que el 82C50A envíe datos al bus de datos (D0-D7). La salida de datos depende del registro seleccionado por las entradas de dirección A0, A1, A2. Las entradas de selección de chip CS0, CS1, CS2 habilitan las entradas DISTR y DISTR. Solo se usa DISTR activa o DISTR activa, no ambas, para recibir datos del 82C50A durante una operación de lectura. Si se usa DISTR como entrada de lectura, DISTR debe estar conectada alto. Si se usa DISTR como entrada de lectura activa, DISTR debe estar conectada bajo.

### DOSTR, DOSTR (Pines 19, 18)

**Tipo:** Entrada
**Nivel Activo:** H (Pin 19), L (Pin 18)

**Descripción:** Señales de strobe de escritura de datos. DOSTR y DOSTR son entradas que causan que datos del bus de datos (D0-D7) sean ingresados al 82C50A. La entrada de datos depende del registro seleccionado por las entradas de dirección A0, A1, A2. Las entradas de selección de chip CS0, CS1, CS2 habilitan las entradas DOSTR y DOSTR. Solo se usa DOSTR activa o DOSTR activa, no ambas, para transmitir datos al 82C50A durante una operación de escritura. Si se usa DOSTR como entrada de escritura, DOSTR debe estar conectada alto. Si se usa DOSTR como entrada de escritura, DOSTR debe estar conectada bajo.

### D0-D7 (Pines 1-8)

**Tipo:** E/S
**Descripción:** Bits de datos 0-7. El bus de datos proporciona ocho líneas de entrada/salida de tres estados para la transferencia de datos, control e información de estado entre el 82C50A y la CPU. Para formatos de caracteres de menos de 8 bits, D7, D6 y D5 son "sin importancia" para operaciones de escritura de datos y 0 para operaciones de lectura de datos. Estas líneas normalmente están en estado de alta impedancia excepto durante operaciones de lectura. D0 es el bit menos significativo (LSB) y es el primer bit de datos serie recibido o transmitido.

### A0, A1, A2 (Pines 28, 27, 26)

**Tipo:** Entrada
**Nivel Activo:** H

**Descripción:** Selección de registro. Las líneas de dirección seleccionan los registros internos durante operaciones del bus de la CPU. Ver Tabla 1.

### XTAL1, XTAL2 (Pines 16, 17)

**Tipo:** E/S (XTAL1), Salida (XTAL2)

**Descripción:** Conexiones de cristal/reloj para el generador de velocidad en baudios interno. XTAL1 también puede utilizarse como entrada de reloj externo, en cuyo caso XTAL2 debe dejarse sin conectar.

### SOUT (Pin 11)

**Tipo:** Salida

**Descripción:** Salida de datos serie. Salida de datos serie del circuito transmisor del 82C50A. Una marca (1) es un lógico uno (alto) y un espacio (0) es un lógico cero (bajo). SOUT se mantiene en la condición de marca cuando el transmisor está deshabilitado, MR es verdadero, el registro transmisor está vacío, o cuando está en modo de retroalimentación. SOUT no es afectado por la entrada CTS.

### GND (Pin 20)

**Tipo:** Conexión a tierra

**Descripción:** Conexión a tierra de la fuente de alimentación (VSS).

### CTS (Pin 36)

**Tipo:** Entrada
**Nivel Activo:** L

**Descripción:** Listo para enviar. El estado lógico del pin CTS se refleja en el bit CTS del Registro de Estado del Módem (MSR), escrito como MSR(4). Un cambio de estado en el pin CTS desde la lectura anterior del MSR causa el establecimiento de DCTS (MSR(0)) del Registro de Estado del Módem. Cuando el pin CTS está ACTIVO (bajo), el módem indica que los datos en SOUT pueden ser transmitidos en el enlace de comunicaciones. Si el pin CTS cambia a INACTIVO (alto), el 82C50A no debe permitir que se transmitan datos fuera de SOUT. El pin CTS no afecta la operación del modo de retroalimentación.

### DSR (Pin 37)

**Tipo:** Entrada
**Nivel Activo:** L

**Descripción:** Listo para conjunto de datos. El estado lógico del pin DSR se refleja en MSR(5) del Registro de Estado del Módem. DDSR (MSR(1)) indica si el pin DSR ha cambiado de estado desde la lectura anterior del MSR. Cuando el pin DSR está ACTIVO (bajo), el módem indica que está listo para intercambiar datos con el 82C50A, mientras que el pin DSR INACTIVO (alto) indica que el módem no está listo para el intercambio de datos. La condición ACTIVA indica solo la condición del equipo de comunicaciones de datos local (DCE) y no implica que se haya establecido un circuito de datos con equipos remotos.

### DTR (Pin 33)

**Tipo:** Salida
**Nivel Activo:** L

**Descripción:** Terminal de datos lista. El pin DTR puede ser establecido (bajo) escribiendo un lógico 1 en MCR(0), bit 0 del Registro de Control del Módem. Esta señal se borra (alto) escribiendo un lógico 0 en el bit DTR (MCR(0)) o siempre que se aplique MR ACTIVO (alto) al 82C50A. Cuando está ACTIVO (bajo), el pin DTR indica al DCE que el 82C50A está listo para recibir datos. En algunos casos, el pin DTR se usa como indicador de encendido. El estado INACTIVO (alto) causa que el DCE desconecte el módem del circuito de telecomunicaciones.

### RTS (Pin 32)

**Tipo:** Salida
**Nivel Activo:** L

**Descripción:** Solicitud de envío. La señal RTS es una salida utilizada para habilitar el módem. El pin RTS es establecido bajo escribiendo un lógico 1 en MCR(1), bit 1 del Registro de Control del Módem. El pin RTS se reinicia alto por Reset Maestro. Cuando está ACTIVO, el pin RTS indica al DCE que el 82C50A tiene datos listos para transmitir. En operaciones de media dupla, RTS se usa para controlar la dirección de la línea.

### BAUDOUT (Pin 15)

**Tipo:** Salida

**Descripción:** Salida de reloj 16X utilizada para la sección del transmisor (16X = 16 veces la velocidad de datos). La velocidad del reloj BAUDOUT es igual a la frecuencia del oscilador de referencia dividida por el divisor especificado en los latches divisores del generador de velocidad en baudios DLL y DLM. BAUDOUT puede ser utilizado por la sección del receptor conectando esta salida a RCLK.

### OUT1 (Pin 34)

**Tipo:** Salida
**Nivel Activo:** L

**Descripción:** Salida 1. Esta es una salida de propósito general que puede ser programada ACTIVA (bajo) estableciendo MCR(2) (OUT1) del Registro de Control del Módem a un nivel alto. El pin OUT1 es establecido alto por Reset Maestro. El pin OUT1 es INACTIVO (alto) durante la operación en modo de retroalimentación.

### OUT2 (Pin 31)

**Tipo:** Salida
**Nivel Activo:** L

**Descripción:** Salida 2. Esta es una salida de propósito general que puede ser programada ACTIVA (bajo) estableciendo MCR(3) del Registro de Control del Módem a un nivel alto. El pin OUT2 es establecido alto por Reset Maestro. La señal OUT2 es INACTIVA (alto) durante la operación en modo de retroalimentación.

### RI (Pin 39)

**Tipo:** Entrada
**Nivel Activo:** L

**Descripción:** Indicador de anillo. Cuando está bajo, RI indica que se ha recibido una señal de timbre de teléfono por el módem o conjunto de datos. La señal RI es una entrada de control de módem cuya condición es probada leyendo MSR(6) (RI). La salida del Registro de Estado del Módem TERI (MSR(2)) indica si la entrada RI ha cambiado de bajo a alto desde la lectura anterior del MSR. Si la interrupción está habilitada (IER(3) = 1) y RI cambia de bajo a alto, se genera una interrupción. El estado ACTIVO (bajo) de RI indica que el DCE está recibiendo una señal de timbre. RI aparecerá ACTIVA aproximadamente el mismo tiempo que el segmento ACTIVO del ciclo de timbre. El estado INACTIVO de RI ocurrirá durante los segmentos INACTIVOS no detectados por el DCE. Este circuito no está deshabilitado por la condición INACTIVA de DTR.

### DCD (Pin 38)

**Tipo:** Entrada
**Nivel Activo:** L

**Descripción:** Detector de portadora de datos. Cuando está ACTIVO (bajo), DCD indica que la portadora de datos ha sido detectada por el módem o conjunto de datos. DCD es una entrada de módem cuya condición puede ser probada por la CPU leyendo MSR(7) (DCD) del Registro de Estado del Módem. MSR(3) (DDCD) del Registro de Estado del Módem indica si la entrada DCD ha cambiado desde la lectura anterior del MSR. DCD no tiene efecto en el receptor. Si DCD cambia de estado con la interrupción de estado del módem habilitada, se genera una interrupción.

Cuando DCD está ACTIVO (bajo), la señal de línea recibida del terminal remoto está dentro de los límites especificados por el fabricante del DCE. La señal INACTIVA (alto) indica que la señal no está dentro de los límites especificados o no está presente.

### MR (Pin 35)

**Tipo:** Entrada
**Nivel Activo:** H

**Descripción:** Reset maestro. La entrada MR fuerza el 82C50A a un modo inactivo en el cual todas las actividades de datos serie se suspenden. El Registro de Control del Módem (MCR) junto con sus salidas asociadas se borran. El Registro de Estado de Línea (LSR) se borra excepto por los bits THRE y TEMT, que se establecen. El 82C50A permanece en un estado inactivo hasta que se programa para reanudar las actividades de datos serie. La entrada MR es una entrada activada por disparador Schmitt. Ver las características eléctricas DC para los niveles de voltaje de entrada lógica del disparador Schmitt. Ver Tabla 7 para un resumen del efecto del Reset Maestro en la operación del 82C50A.

### INTRPT (Pin 30)

**Tipo:** Salida
**Nivel Activo:** H

**Descripción:** Solicitud de interrupción. La salida INTRPT se activa (alto) cuando una de las siguientes interrupciones tiene una condición ACTIVA (alto) y está habilitada por el Registro de Habilitación de Interrupción: bandera de error del receptor, datos recibidos disponibles, registro transmisor vacío, y estado del módem. INTRPT se reinicia bajo al servicio apropiado o una operación MR. Ver Figura 1. Estructura de control de interrupciones.

### SIN (Pin 10)

**Tipo:** Entrada
**Nivel Activo:** H

**Descripción:** Entrada de datos serie. La entrada SIN es la entrada de datos serie desde la línea de comunicaciones o módem a los circuitos receptores del 82C50A. Una marca (1) es alto, y un espacio (0) es bajo. Las entradas de datos en SIN se deshabilitan cuando se opera en modo de retroalimentación.

### VCC (Pin 40)

**Tipo:** Entrada

**Descripción:** Suministro de energía positiva de +5V. Se recomienda un capacitor de desacoplamiento de 0.1µF desde VCC (pin 40) a GND (pin 20).

### CS0, CS1, CS2 (Pines 12, 13, 14)

**Tipo:** Entrada
**Nivel Activo:** H, H, L

**Descripción:** Selección de chip. Las entradas de selección de chip actúan como señales de habilitación para las entradas de escritura (DOSTR, DOSTR) y lectura (DISTR, DISTR). Las entradas de selección de chip están enganchadas por la entrada ADS.

### NC (Pin 29)

**Descripción:** No conectar.

### CSOUT (Pin 24)

**Tipo:** Salida
**Nivel Activo:** H

**Descripción:** Salida de selección de chip. Cuando está ACTIVA (alto), este pin indica que el chip ha sido seleccionado por entradas CS0, CS1 y CS2 activas. No se puede iniciar ninguna transferencia de datos hasta que CSOUT sea un lógico 1, ACTIVO (alto).

### DDIS (Pin 23)

**Tipo:** Salida
**Nivel Activo:** H (Activo), L (Inactivo)

**Descripción:** Deshabilitación del controlador. Esta salida es INACTIVA (bajo) cuando la CPU está leyendo datos del 82C50A. Una salida DDIS ACTIVA (alto) puede usarse para deshabilitar un transceptor externo cuando la CPU está leyendo datos.

### ADS (Pin 25)

**Tipo:** Entrada
**Nivel Activo:** L

**Descripción:** Strobe de dirección. Cuando está ACTIVO (bajo), ADS engancha las entradas de selección de registro (A0, A1, A2) y selección de chip (CS0, CS1, CS2). Se requiere un ADS activo cuando los pines de selección de registro no son estables durante la duración de la operación de lectura o escritura, modo multiplexado. Si no se requiere, la entrada ADS debe estar conectada bajo, modo no multiplexado.

### RCLK (Pin 9)

**Tipo:** Entrada

**Descripción:** Entrada de reloj de velocidad en baudios 16X para la sección del receptor del 82C50A. Esta entrada puede proporcionarse desde la salida BAUDOUT o un reloj externo.

## Registros Accesibles

El 82C50A contiene tres tipos de registros internos utilizados en la operación del dispositivo: registros de control, registros de estado y registros de datos. Los registros de control son el registro de selección de velocidad en baudios DLL y DLM, registro de control de línea, registro de habilitación de interrupción y registros de control del módem, mientras que los registros de estado son el registro de estado de línea y el registro de estado del módem. Los registros de datos son el registro de buffer del receptor y el registro de espera del transmisor. Las entradas de dirección, lectura y escritura se utilizan en conjunto con el bit de acceso al latch divisor en el registro de control de línea (LCR(7)) para seleccionar el registro a leer o escribir (ver Tabla 1).

### Tabla 1: Acceso a Registros Internos del 82C50A

| DLAB | A2 | A1 | A0 | Nemónico | Registro |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | RBR | Registro de Buffer del Receptor (solo lectura) |
| 0 | 0 | 0 | 0 | THR | Registro de Espera del Transmisor (solo escritura) |
| 0 | 0 | 0 | 1 | IER | Registro de Habilitación de Interrupción |
| X | 0 | 1 | 0 | IIR | Registro de Identificación de Interrupción (solo lectura) |
| X | 0 | 1 | 1 | LCR | Registro de Control de Línea |
| X | 1 | 0 | 0 | MCR | Registro de Control del Módem |
| X | 1 | 0 | 1 | LSR | Registro de Estado de Línea |
| X | 1 | 1 | 0 | MSR | Registro de Estado del Módem |
| X | 1 | 1 | 1 | SCR | Registro de Borrador |
| 1 | 0 | 0 | 0 | DLL | Latch Divisor (LSB) |
| 1 | 0 | 0 | 1 | DLM | Latch Divisor (MSB) |

*Nota: X = "Sin importancia", 0 = Lógico bajo, 1 = Lógico alto*

Los bits individuales dentro de estos registros se refieren por el nemónico del registro y el número de bit entre paréntesis. Por ejemplo, LCR(7) se refiere al bit 7 del Registro de Control de Línea.

El Registro de Buffer del Transmisor y el Registro de Buffer del Receptor son registros de datos que contienen de 5 a 8 bits de datos. Si se transmiten menos de ocho bits de datos, los datos se justifican a la derecha hacia el LSB. El bit 0 de una palabra de datos es siempre el primer bit de datos serie recibido y transmitido. Los registros de datos del 82C50A tienen búfer duplicado para que las operaciones de lectura y escritura puedan realizarse simultáneamente mientras el UART realiza la conversión serie a paralela y paralela a serie. Esto proporciona al microprocesador mayor flexibilidad en su temporización de lectura y escritura.

## Registro de Control de Línea (LCR)

### Estructura del Registro LCR

| Bit | Campo | Función |
|---|---|---|
| 7 | DLAB | Bit de acceso al latch divisor |
| 6 | Rompimiento | Control de ruptura |
| 5 | Paridad fija | Paridad fija |
| 4 | EPS | Selección de paridad par |
| 3 | PEN | Habilitación de paridad |
| 2 | STB | Selección del bit de parada |
| 1 | WLS1 | Bit 1 de selección de longitud de palabra |
| 0 | WLS0 | Bit 0 de selección de longitud de palabra |

### Descripción de Bits LCR

**LCR(0) y LCR(1) - Bits de selección de longitud de palabra (WLS0, WLS1):**

El número de bits en cada carácter serie transmitido o recibido se programa de la siguiente manera:

| LCR(1) | LCR(0) | Longitud de Palabra |
|---|---|---|
| 0 | 0 | 5 bits |
| 0 | 1 | 6 bits |
| 1 | 0 | 7 bits |
| 1 | 1 | 8 bits |

**LCR(2) - Selección del bit de parada (STB):**

LCR(2) especifica el número de bits de parada en cada carácter transmitido. Si LCR(2) es lógico 0, se genera un bit de parada en los datos transmitidos. Si LCR(2) es lógico 1 cuando se selecciona una longitud de palabra de 5 bits, se generan 1.5 bits de parada. Si LCR(2) es lógico 1 cuando se selecciona una longitud de palabra de 6, 7 u 8 bits, se generan dos bits de parada. El receptor verifica dos bits de parada si se programa.

**LCR(3) - Habilitación de paridad (PEN):**

Cuando LCR(3) es alto, se genera y se verifica un bit de paridad entre el último bit de palabra de datos y el bit de parada.

**LCR(4) - Selección de paridad par (EPS):**

Cuando la paridad está habilitada (LCR(3) = 1), LCR(4) = 0 selecciona paridad impar, y LCR(4) = 1 selecciona paridad par.

**LCR(5) - Paridad fija:**

Cuando la paridad está habilitada (LCR(3) = 1), LCR(5) = 1 causa que la transmisión y recepción de un bit de paridad esté en el estado opuesto al indicado por LCR(4). Esto permite al usuario forzar la paridad a un estado conocido y al receptor verificar el bit de paridad en un estado conocido.

**LCR(6) - Control de ruptura:**

Cuando LCR(6) se establece en lógico 1, la salida serie (SOUT) se fuerza al estado de espaciado (lógico 0). La ruptura se deshabilita estableciendo LCR(6) en lógico 0. El bit de control de ruptura solo actúa en SOUT y no tiene efecto en la lógica del transmisor. El control de ruptura permite a la CPU alertar a una terminal en un sistema de comunicaciones de computadora. Si se utiliza la siguiente secuencia, no se transmitirán caracteres erróneos o ajenos porque cause la ruptura:

1. Cargar un carácter de relleno de todos los ceros en respuesta a THRE.
2. Establecer ruptura en respuesta al siguiente THRE.
3. Esperar a que el transmisor esté inactivo (TEMT = 1) y borrar la ruptura cuando se debe restaurar la transmisión normal.

Durante la ruptura, el transmisor puede usarse como un temporizador de caracteres para establecer con precisión la duración de la ruptura.

**LCR(7) - Bit de acceso al latch divisor (DLAB):**

LCR(7) debe ser establecido alto (lógico 1) para acceder a los latches divisores DLL y DLM del generador de velocidad en baudios durante una operación de lectura o escritura. LCR(7) debe ser bajo para acceder al buffer del receptor, el registro de espera del transmisor o el registro de habilitación de interrupción.

## Registro de Estado de Línea (LSR)

El LSR es un registro único que proporciona indicaciones de estado. El LSR es generalmente el primer registro leído por la CPU para determinar la causa de una interrupción o para sondear el estado del 82C50A.

### Bits de LSR 0 a 7

| Bit | Nemónico | Descripción | Lógico 1 | Lógico 0 |
|---|---|---|---|---|
| 0 | DR | Datos listos | Listo | No listo |
| 1 | OE | Error de desbordamiento | Error | Sin error |
| 2 | PE | Error de paridad | Error | Sin error |
| 3 | FE | Error de encuadre | Error | Sin error |
| 4 | BI | Interrupción de ruptura | Ruptura | Sin ruptura |
| 5 | THRE | Registro de espera del transmisor vacío | No vacío | Vacío |
| 6 | TEMT | Transmisor vacío | Vacío | No vacío |
| 7 | - | No utilizado | Permanentemente 0 | - |

### Descripción de Bits LSR

**LSR(0) - Datos listos (DR):**

Datos listos se establece alto cuando se ha recibido un carácter entrante y se ha transferido al Registro de Buffer del Receptor. LSR(0) se reinicia bajo por una lectura de CPU de los datos en el Registro de Buffer del Receptor.

**LSR(1) - Error de desbordamiento (OE):**

El indicador de error de desbordamiento indica que los datos en el Registro de Buffer del Receptor no fueron leídos por la CPU antes de que el siguiente carácter fuera transferido al Registro de Buffer del Receptor, sobrescribiendo el carácter anterior. El indicador OE se reinicia siempre que la CPU lee el contenido del Registro de Estado de Línea.

**LSR(2) - Error de paridad (PE):**

El error de paridad indica que el carácter de datos recibido no tiene la paridad par o impar correcta, según sea seleccionado por el bit de selección de paridad par (LCR(4)). El bit PE se establece alto tras la detección de un error de paridad y se reinicia bajo cuando la CPU lee el contenido del LSR.

**LSR(3) - Error de encuadre (FE):**

El error de encuadre indica que el carácter recibido no tenía un bit de parada válido. LSR(3) se establece alto cuando el bit de parada que sigue al último bit de datos o bit de paridad se detecta como un bit cero (nivel de espaciado). El indicador FE se reinicia bajo cuando la CPU lee el contenido del LSR.

**LSR(4) - Interrupción de ruptura (BI):**

La interrupción de ruptura se establece alto cuando la entrada de datos recibida se mantiene en el estado de espaciado (lógico 0) durante más tiempo que una transmisión de palabra completa (bit de inicio + bits de datos + paridad + bits de parada). El indicador BI se reinicia cuando la CPU lee el contenido del Registro de Estado de Línea.

LSR(1) - LSR(4) son las condiciones de error que producen una interrupción de estado de línea del receptor (interrupción de prioridad 1 en el Registro de Identificación de Interrupción (IIR)) cuando se detecta cualquiera de las condiciones. Esta interrupción se habilita estableciendo IER(2) = 1 en el Registro de Habilitación de Interrupción.

**LSR(5) - Registro de espera del transmisor vacío (THRE):**

THRE indica que el 82C50A está listo para aceptar un nuevo carácter para transmisión. El bit THRE se establece alto cuando un carácter se transfiere del Registro de Espera del Transmisor al Registro de Desplazamiento del Transmisor. LSR(5) se reinicia bajo por la carga del Registro de Espera del Transmisor por la CPU. LSR(5) no se reinicia por una lectura de CPU del LSR.

Cuando la interrupción THRE está habilitada (IER(1) = 1), THRE causa una interrupción de prioridad 3 en el IIR. Si THRE es la fuente de interrupción indicada en el IIR, INTRPT se borra por una lectura del IIR.

**LSR(6) - Transmisor vacío (TEMT):**

TEMT se establece alto cuando el Registro de Espera del Transmisor (THR) y el Registro de Desplazamiento del Transmisor (TSR) están ambos vacíos. LSR(6) se reinicia bajo cuando un carácter se carga en el THR y permanece bajo hasta que el carácter se transfiere fuera de SOUT. TEMT no se reinicia bajo por una lectura de CPU del LSR.

**LSR(7) - Este bit está permanentemente establecido en lógico 0.**

Tres banderas de error OE, FE y PE proporcionan el estado de cualquier condición de error detectada en el circuito receptor. Durante la recepción de los bits de parada, las banderas de error se establecen alto por una condición de error. Las banderas de error no se reinician por la ausencia de una condición de error en el siguiente carácter recibido. Las banderas reflejan el último carácter solo si no se produjo un desbordamiento. El error de desbordamiento (OE) indica que un carácter en el Registro de Buffer del Receptor ha sido sobrescrito por un carácter del Registro de Desplazamiento del Receptor antes de ser leído por la CPU. El carácter se pierde. El error de encuadre (FE) indica que el último carácter recibido contenía bits de parada incorrectos (bajos). Esto es causado por la ausencia del bit de parada requerido o por un bit de parada demasiado corto para ser detectado. El error de paridad (PE) indica que el último carácter recibido contenía un error de paridad basado en la paridad programada y calculada del carácter recibido.

La interrupción de ruptura (BI) indica que el último carácter recibido fue un carácter de ruptura. Un carácter de ruptura es un carácter de datos inválido, con el carácter completo, incluyendo paridad y bits de parada, lógico cero.

La lectura del LSR borra LSR(1) - LSR(4) (OE, PE, FE y BI).

## Registro de Control del Módem (MCR)

El MCR controla la interfaz con el módem o conjunto de datos como se describe a continuación. El MCR se puede escribir y leer. Las salidas RTS, DTR, OUT1 y OUT2 están directamente controladas por sus bits de control en este registro. Una entrada alta afirma un bajo (verdadero) en los pines de salida.

### Bits del MCR 0 a 7

| Bit | Nemónico | Función |
|---|---|---|
| 0 | DTR | Terminal de datos lista |
| 1 | RTS | Solicitud de envío |
| 2 | OUT1 | Salida 1 |
| 3 | OUT2 | Salida 2 |
| 4 | LOOP | Retroalimentación local |
| 5 | - | 0 (Permanentemente) |
| 6 | - | 0 (Permanentemente) |
| 7 | - | 0 (Permanentemente) |

### Descripción de Bits MCR

**MCR(0) - Terminal de datos lista (DTR):**

Cuando MCR(0) se establece alto, la salida DTR se fuerza bajo. Cuando MCR(0) se reinicia bajo, la salida DTR se fuerza alto. La salida DTR del 82C50A puede ser ingresada en un controlador de línea inversor EIA como el 1488 para obtener la polaridad correcta en la entrada del módem o conjunto de datos.

**MCR(1) - Solicitud de envío (RTS):**

Cuando MCR(1) se establece alto, la salida RTS se fuerza bajo. Cuando MCR(1) se reinicia bajo, la salida RTS se fuerza alto. La salida RTS del 82C50A puede ser ingresada en un controlador de línea inversor EIA como el 1488 para obtener la polaridad correcta en la entrada del módem o conjunto de datos.

**MCR(2) - Salida 1 (OUT1):**

Cuando MCR(2) se establece alto, la salida OUT1 se fuerza bajo. Cuando MCR(2) se reinicia bajo, la salida OUT1 se fuerza alto. OUT1 es una salida designada por el usuario.

**MCR(3) - Salida 2 (OUT2):**

Cuando MCR(3) se establece alto, la salida OUT2 se fuerza bajo. Cuando MCR(3) se reinicia bajo, la salida OUT2 se fuerza alto. OUT2 es una salida designada por el usuario.

**MCR(4) - Retroalimentación local (LOOP):**

MCR(4) proporciona una característica de retroalimentación local para pruebas de diagnóstico del 82C50A. Cuando MCR(4) se establece alto, la salida serie (SOUT) se establece en el estado de marcación (lógico 1), y la entrada de datos del receptor serie (SIN) se desconecta. La salida del Registro de Desplazamiento del Transmisor se retroalimenta a la entrada del Registro de Desplazamiento del Receptor. Los cuatro pines de entrada de control del módem (CTS, DSR, DCD y RI) se desconectan. Las cuatro salidas de control del módem (DTR, RTS, OUT1 y OUT2) se conectan internamente a las cuatro entradas de control del módem. Los pines de salida de control del módem se fuerzan a su estado inactivo (alto). En el modo de diagnóstico, los datos transmitidos se reciben inmediatamente. Esto permite al procesador verificar las rutas de datos de transmisión y recepción del 82C50A.

En el modo de diagnóstico, el receptor y transmisor están completamente operacionales. Los controles de interrupción del módem también son operacionales, pero las fuentes de interrupción son ahora los cuatro bits inferiores del MCR en lugar de las cuatro entradas de control de módem. Las interrupciones todavía están controladas por el Registro de Habilitación de Interrupción.

**MCR(5) - MCR(7) - Estos bits están permanentemente establecidos en lógico 0.**

## Registro de Estado del Módem (MSR)

El MSR proporciona a la CPU el estado de las líneas de entrada del módem desde el módem o dispositivo periférico. El MSR permite a la CPU leer las entradas de señal del módem mediante la interfaz de acceso al bus de datos del 82C50A. Además de la información de estado actual, cuatro bits del MSR indican si las entradas del módem han cambiado desde la última lectura del MSR. Los bits de estado delta se establecen alto cuando una entrada de control del módem cambia de estado y se reinician bajo cuando la CPU lee el MSR.

### Bits del MSR 0 a 7

| Bit | Nemónico | Descripción |
|---|---|---|
| 0 | DCTS | Delta Listo para Enviar |
| 1 | DDSR | Delta Listo para Conjunto de Datos |
| 2 | TERI | Borde Posterior del Indicador de Anillo |
| 3 | DDCD | Delta Detector de Portadora de Datos |
| 4 | CTS | Listo para Enviar |
| 5 | DSR | Listo para Conjunto de Datos |
| 6 | RI | Indicador de Anillo |
| 7 | DCD | Detector de Portadora de Datos |

### Descripción de Bits MSR

**MSR(0) - Delta Listo para Enviar (DCTS):**

DCTS indica que la entrada CTS (Pin 36) al 82C50A ha cambiado de estado desde la última vez que fue leída por la CPU.

**MSR(1) - Delta Listo para Conjunto de Datos (DDSR):**

DDSR indica que la entrada DSR (Pin 37) al 82C50A ha cambiado de estado desde la última vez que fue leída por la CPU.

**MSR(2) - Borde Posterior del Indicador de Anillo (TERI):**

TERI indica que la entrada RI (Pin 39) al 82C50A ha cambiado de estado de bajo a alto desde la última vez que fue leída por la CPU. Las transiciones de alto a bajo en RI no activan TERI.

**MSR(3) - Delta Detector de Portadora de Datos (DDCD):**

DDCD indica que la entrada DCD (Pin 38) al 82C50A ha cambiado de estado desde la última vez que fue leída por la CPU.

**MSR(4) - Listo para Enviar (CTS):**

Listo para enviar (CTS) es el estado de la entrada CTS (Pin 36) del módem indicando al 82C50A que el módem está listo para recibir datos de la salida del transmisor del 82C50A (SOUT). Si el 82C50A está en modo de retroalimentación (MCR(4) = 1), MSR(4) es equivalente a RTS en el MCR.

**MSR(5) - Listo para Conjunto de Datos (DSR):**

Listo para conjunto de datos (DSR) es un estado de la entrada DSR (Pin 37) del módem al 82C50A que indica que el módem está listo para proporcionar datos recibidos a la circuitería receptora del 82C50A. Si el 82C50A está en modo de retroalimentación (MCR(4) = 1), MSR(5) es equivalente a DTR en el MCR.

**MSR(6) - Indicador de Anillo:**

Indica el estado de la entrada RI (Pin 39). Si el 82C50A está en modo de retroalimentación (MCR(4) = 1), MSR(6) es equivalente a OUT1 en el MCR.

**MSR(7) - Detector de Portadora de Datos:**

Indica el estado de la entrada del Detector de Portadora de Datos (DCD) (Pin 38). Si el 82C50A está en modo de retroalimentación (MCR(4) = 1), MSR(7) es equivalente a OUT2 del MCR.

Las entradas de estado del módem (RI, DCD, DSR y CTS) reflejan las líneas de entrada del módem con cualquier cambio de estado. La lectura del registro MSR borrará las indicaciones de estado delta del módem pero no tiene efecto en los bits de estado. Los bits de estado reflejan el estado de los pines de entrada independientemente de las señales de control de máscara. Si un DCTS, DDSR, TERI o DDCD son verdaderos y un cambio de estado ocurre durante una operación de lectura (DISTR, DISTR), el cambio de estado no se indica en el MSR. Si DCTS, DDSR, TERI o DDCD son falsos y un cambio de estado ocurre durante una operación de lectura, el cambio de estado se indica después de la operación de lectura.

Para el LSR y MSR, el establecimiento de bits de estado se inhibe durante operaciones de lectura del registro de estado (DISTR, DISTR). Si una condición de estado se genera durante una lectura (DISTR, DISTR) y la misma condición de estado ocurre, ese bit de estado se borrará en el borde posterior de la lectura (DISTR, DISTR) en lugar de ser establecido de nuevo.

*Nota: El estado (alto o bajo) de los bits de estado son versiones invertidas de los pines de entrada reales.*

## Registro del Selector de Velocidad en Baudios (BRSR)

El 82C50A contiene un Generador de Velocidad en Baudios programable (BRG) que divide el reloj (DC a 10MHz) por cualquier divisor de 1 a 2^16-1 (ver también descripción BRG). La frecuencia de salida del generador de baudios es 16X la velocidad de datos (divisor # = frecuencia de entrada / (velocidad en baudios x 16)). Dos registros de latch divisor de 8 bits almacenan el divisor en formato binario de 16 bits.

Estos registros de latch divisor deben ser cargados durante la inicialización. Al cargar cualquiera de los latches divisores, un contador de baudios de 16 bits se carga inmediatamente. Esto previene conteos largos en la carga inicial.

### Cálculo del Número Divisor de Ejemplo

**Dado:**
- Velocidad en baudios deseada: 1200 Baudios
- Frecuencia de entrada: 1.8432MHz

**Fórmula:**
Divisor # = Frecuencia de entrada / (Velocidad en baudios x 16)
Divisor # = 1843200 / (1200 x 16)

**Respuesta:**
Divisor # = 96 = 0x60
DLL = 0x60
DLM = 0x00

**Verificación:**
El divisor # 96 dividirá la frecuencia de entrada 1.8432MHz a 19200, que es 16 veces la velocidad en baudios deseada.

### Latch Divisor Byte Menos Significativo (DLL)

| Bit | Descripción |
|---|---|
| 0 | Bit 0 |
| 1 | Bit 1 |
| 2 | Bit 2 |
| 3 | Bit 3 |
| 4 | Bit 4 |
| 5 | Bit 5 |
| 6 | Bit 6 |
| 7 | Bit 7 |

### Latch Divisor Byte Más Significativo (DLM)

| Bit | Descripción |
|---|---|
| 0 | Bit 8 |
| 1 | Bit 9 |
| 2 | Bit 10 |
| 3 | Bit 11 |
| 4 | Bit 12 |
| 5 | Bit 13 |
| 6 | Bit 14 |
| 7 | Bit 15 |

## Registro de Buffer del Receptor (RBR)

La circuitería del receptor en el 82C50A es programable para 5, 6, 7 u 8 bits de datos por carácter. Para palabras de menos de 8 bits, los datos se justifican a la derecha hacia el bit menos significativo (LSB = Bit de Datos 0 (RBR(0))). El bit 0 de datos de una palabra de datos (RBR(0)) es el primer bit de datos recibido. Los bits no utilizados en un carácter de menos de 8 bits se sacan bajo por el 82C50A.

Los datos recibidos en el pin de entrada SIN se desplazan en el Registro de Desplazamiento del Receptor por el reloj 16X proporcionado en la entrada RCLK. Este reloj se sincroniza con los datos entrantes basados en la posición del bit de inicio. Cuando un carácter completo se desplaza en el Registro de Desplazamiento del Receptor, los bits de datos ensamblados se cargan en paralelo en el Registro de Buffer del Receptor. Se establece la bandera DR en el registro LSR.

El búfer duplicado de los datos recibidos permite la recepción continua de datos sin perder datos recibidos. Mientras que el Registro de Desplazamiento del Receptor está desplazando un nuevo carácter en el 82C50A, el Registro de Buffer del Receptor está sosteniendo un carácter previamente recibido para que la CPU lo lea. Si no se lee los datos en el RBR antes de la recepción completa del siguiente carácter, se pierden datos en el Registro de Buffer del Receptor. La bandera OE en el registro LSR indica la condición de desbordamiento.

### Bits de RBR 0 a 7

| Bit | Descripción |
|---|---|
| 0 | Bit de datos 0 |
| 1 | Bit de datos 1 |
| 2 | Bit de datos 2 |
| 3 | Bit de datos 3 |
| 4 | Bit de datos 4 |
| 5 | Bit de datos 5 |
| 6 | Bit de datos 6 |
| 7 | Bit de datos 7 |

## Registro de Espera del Transmisor (THR)

El Registro de Espera del Transmisor (THR) sostiene datos paralelos del bus de datos (D0-D7) hasta que el Registro de Desplazamiento del Transmisor está vacío y listo para aceptar un nuevo carácter para transmisión. La longitud de palabra del transmisor y el número de bits de parada son los mismos que el receptor. Si el carácter tiene menos de ocho bits, los bits no utilizados en el bus de datos del microprocesador se ignoran por el transmisor.

El bit de datos 0 (THR(0)) es el primer bit de datos serie transmitido. La bandera THRE (LSR(5)) refleja el estado del THR. La bandera TEMT (LSR(6)) indica si tanto el THR como el TSR están vacíos.

### Bits de THR 0 a 7

| Bit | Descripción |
|---|---|
| 0 | Bit de datos 0 |
| 1 | Bit de datos 1 |
| 2 | Bit de datos 2 |
| 3 | Bit de datos 3 |
| 4 | Bit de datos 4 |
| 5 | Bit de datos 5 |
| 6 | Bit de datos 6 |
| 7 | Bit de datos 7 |

## Registro de Borrador (SCR)

Este registro de lectura/escritura de 8 bits no tiene efecto en el 82C50A. Se intenta que sea un registro de borrador para ser utilizado por el programador para mantener datos temporalmente.

### Bits de SCR 0 a 7

| Bit | Descripción |
|---|---|
| 0 | Bit de datos 0 |
| 1 | Bit de datos 1 |
| 2 | Bit de datos 2 |
| 3 | Bit de datos 3 |
| 4 | Bit de datos 4 |
| 5 | Bit de datos 5 |
| 6 | Bit de datos 6 |
| 7 | Bit de datos 7 |

## Estructura de Interrupción

### Registro de Identificación de Interrupción (IIR)

El 82C50A tiene capacidad de interrupción para interfaz a microprocesadores actuales. Para minimizar la sobrecarga de software durante las transferencias de caracteres de datos, el 82C50A prioriza interrupciones en cuatro niveles. Los cuatro niveles de condiciones de interrupción son los siguientes:

1. **Nivel 1 (Prioridad más alta):** Estado de línea del receptor
2. **Nivel 2:** Datos recibidos disponibles
3. **Nivel 3:** Registro de espera del transmisor vacío
4. **Nivel 4 (Prioridad más baja):** Estado del módem

La información que indica que una interrupción priorizada está pendiente y el tipo de interrupción se almacena en el Registro de Identificación de Interrupción (IIR). Cuando se accede durante el tiempo de selección de chip, el IIR indica la interrupción de prioridad más alta pendiente. No se reconocen otras interrupciones hasta que la interrupción sea servida por la CPU. El contenido del IIR se indica en la Tabla 2 y se describe a continuación.

**IIR(0):**

IIR(0) puede ser utilizado en un entorno de prioridad conectada por hardware o sondeo para indicar si una interrupción está pendiente. Cuando IIR(0) es bajo, una interrupción está pendiente, y el contenido del IIR puede ser utilizado como un puntero a la rutina de servicio de interrupción apropiada. Cuando IIR(0) es alto, no hay interrupción pendiente.

**IIR(1) e IIR(2):**

IIR(1) e IIR(2) se utilizan para identificar la interrupción de prioridad más alta pendiente como se indica en la Tabla 2.

**IIR(3) - IIR(7):**

Estos cinco bits del IIR son lógico 0.

### Tabla 2: Registro de Identificación de Interrupción

| Bit 2 | Bit 1 | Bit 0 | Nivel de Prioridad | Bandera de Interrupción | Fuente de Interrupción | Control de Reinicio |
|---|---|---|---|---|---|---|
| X | X | 1 | Ninguno | Ninguno | Ninguno | - |
| 1 | 1 | 0 | Primero | Estado de línea del receptor | OE, PE, FE o BI | Lectura de LSR |
| 1 | 0 | 0 | Segundo | Datos recibidos disponibles | Datos disponibles del receptor | Lectura de RBR |
| 0 | 1 | 0 | Tercero | THRE | THRE | Lectura de IIR si THRE es la fuente de interrupción o escritura en THR |
| 0 | 0 | 0 | Cuarto | Estado del módem | CTS, DSR, RI, DCD | Lectura de MSR |

*Nota: X = No definido, puede ser 0 o 1*

## Registro de Habilitación de Interrupción (IER)

El Registro de Habilitación de Interrupción (IER) es un registro de escritura utilizado para habilitar independientemente las cuatro interrupciones del 82C50A que activan la salida de interrupción (INTRPT). Todas las interrupciones están deshabilitadas por reinicio de IER(0) - IER(3) del Registro de Habilitación de Interrupción. La interrupción del sistema se inhibe estableciendo IER(0) - IER(3) bajo. Todas las interrupciones están deshabilitadas por reinicio del IER(0) - IER(3). El contenido del Registro de Habilitación de Interrupción se indica en la Tabla 3 y se describe a continuación.

**IER(0):**

Cuando se programa alto (IER(0) = Lógico 1), IER(0) habilita la interrupción de datos recibidos disponibles.

**IER(1):**

Cuando se programa alto (IER(1) = Lógico 1), IER(1) habilita la interrupción de registro de espera del transmisor vacío.

**IER(2):**

Cuando se programa alto (IER(2) = Lógico 1), IER(2) habilita la interrupción de estado de línea del receptor.

**IER(3):**

Cuando se programa alto (IER(3) = Lógico 1), IER(3) habilita la interrupción de estado del módem.

**IER(4) - IER(7):**

Estos cuatro bits del IER son lógico 0.

### Tabla 3: Resumen del Registro de Habilitación de Interrupción del 82C50A

| Bit | Campo | Descripción |
|---|---|---|
| 0 | ERBFI | Habilitar interrupción de datos recibidos disponibles |
| 1 | ETBEI | Habilitar interrupción de registro de espera del transmisor vacío |
| 2 | ELSI | Habilitar interrupción de estado de línea del receptor |
| 3 | EDSSI | Habilitar interrupción de estado del módem |
| 4-7 | - | 0 (permanentemente) |

### Figura 1: Estructura de Control de Interrupción del 82C50A

*Nota: La estructura de control de interrupción original del datasheet muestra cómo las diversas señales de interrupción (DR del LSR, THRE del LSR, OE/PE/FE/BI del LSR, DCTS/DDSR/TERI/DDCD del MSR) se combinan a través de puertas habilitadas por el IER para producir la salida INTRPT en el pin 30.*

## Resumen de Registros Accesibles

### Tabla 3: Resumen de Registros Accesibles del 82C50A (Continuación)

| Nemónico de Registro | Bit 7 | Bit 6 | Bit 5 | Bit 4 | Bit 3 | Bit 2 | Bit 1 | Bit 0 |
|---|---|---|---|---|---|---|---|---|
| RBR (Solo lectura) | Bit de datos 7 (MSB) | Bit de datos 6 | Bit de datos 5 | Bit de datos 4 | Bit de datos 3 | Bit de datos 2 | Bit de datos 1 | Bit de datos 0 (LSB) |
| THR (Solo escritura) | Bit de datos 7 | Bit de datos 6 | Bit de datos 5 | Bit de datos 4 | Bit de datos 3 | Bit de datos 2 | Bit de datos 1 | Bit de datos 0 |
| DLL | Bit 7 | Bit 6 | Bit 5 | Bit 4 | Bit 3 | Bit 2 | Bit 1 | Bit 0 |
| DLM | Bit 15 | Bit 14 | Bit 13 | Bit 12 | Bit 11 | Bit 10 | Bit 9 | Bit 8 |
| IER | 0 | 0 | 0 | 0 | EDSSI (Habilitar interrupción de estado del módem) | ELSI (Habilitar interrupción de estado de línea del receptor) | ETBEI (Habilitar interrupción de registro de espera del transmisor vacío) | ERBFI (Habilitar interrupción de datos recibidos disponibles) |
| IIR (Solo lectura) | 0 | 0 | 0 | 0 | 0 | ID de interrupción bit 1 | ID de interrupción bit 0 | Interrupción pendiente "0" = Interrupción pendiente, "1" = Sin interrupción |
| LCR | DLAB (Bit de acceso al latch divisor) | Rompimiento (Control de ruptura) | Paridad fija (Paridad fija) | EPS (Selección de paridad par) | PEN (Habilitación de paridad) | STB (Número de bits de parada) | WLS1 (Selección de longitud de palabra) | WLS0 (Selección de longitud de palabra) |
| MCR | 0 | 0 | 0 | LOOP (Retroalimentación) | OUT2 (Salida 2) | OUT1 (Salida 1) | RTS (Solicitud de envío) | DTR (Terminal de datos lista) |
| LSR | 0 | TEMT (Transmisor vacío) | THRE (Registro de espera del transmisor vacío) | BI (Interrupción de ruptura) | FE (Error de encuadre) | PE (Error de paridad) | OE (Error de desbordamiento) | DR (Datos listos) |
| MSR | DCD (Detector de portadora de datos) | RI (Indicador de anillo) | DSR (Listo para conjunto de datos) | CTS (Listo para enviar) | DDCD (Delta detector de portadora de datos) | TERI (Borde posterior del indicador de anillo) | DDSR (Delta listo para conjunto de datos) | DCTS (Delta listo para enviar) |
| SCR | Bit 7 | Bit 6 | Bit 5 | Bit 4 | Bit 3 | Bit 2 | Bit 1 | Bit 0 |

*LSB: Bit de datos 0 es el primer bit transmitido o recibido*

## Transmisor

La sección del transmisor serie consiste en un Registro de Espera del Transmisor (THR), Registro de Desplazamiento del Transmisor (TSR) y lógica de control asociada. El Registro de Espera del Transmisor Vacío (THRE) y el Registro de Desplazamiento del Transmisor Vacío (TEMT) son dos bits en el Registro de Estado de Línea que indican el estado del THR y TSR. Para transmitir una palabra de 5 a 8 bits, la palabra se escribe a través de D0-D7 al THR. El microprocesador debe realizar una operación de escritura solo si THRE está alto. THRE se establece alto cuando la palabra se transfiere automáticamente del THR al TSR durante la transmisión del bit de inicio.

Cuando el transmisor está inactivo, tanto THRE como TEMT están altos. La primera palabra escrita causa que THRE se reinicie a 0. Después de la finalización de la transferencia, THRE se pone alto nuevamente. TEMT permanece bajo durante al menos la duración de la transmisión de la palabra de datos. Si se transmite un segundo carácter al THR, THRE se reinicia bajo. Puesto que la palabra de datos no puede ser transferida del THR al TSR hasta que el TSR esté vacío, THRE permanece bajo hasta que el TSR haya completado la transmisión de la palabra. Cuando se ha transmitido la última palabra fuera del TSR, TEMT se establece alto. THRE se establece alto un tiempo de transferencia de THR a TSR después.

## Receptor

Los datos asíncronos serie se ingresan en el pin SIN. El estado inactivo de la línea que proporciona la entrada a SIN es alto. Un circuito de detección del bit de inicio busca continuamente una transición de alto a bajo desde el estado inactivo. Cuando se detecta la transición, se reinicia un contador y cuenta el reloj 16X a 7,5, que es el centro del bit de inicio. El bit de inicio es válido si SIN sigue siendo bajo en la muestra de punto medio del bit de inicio. La verificación del bit de inicio previene que el receptor ensamble un carácter de datos incorrecto debido a un pico de ruido que va bajo en la entrada SIN.

El Registro de Control de Línea determina el número de bits de datos en un carácter (LCR(0), LCR(1)), número de bits de parada (LCR(2)), si se utiliza paridad (LCR(3)) y la polaridad de la paridad (LCR(4)). La información de estado para el receptor se proporciona en el Registro de Estado de Línea. Cuando se transfiere un carácter del Registro de Desplazamiento del Receptor al Registro de Buffer del Receptor, la indicación de datos recibidos en LSR(0) se establece alto. La CPU lee el Registro de Buffer del Receptor a través de D0-D7. Esta lectura reinicia LSR(0). Si D0-D7 no se leen antes de una nueva transferencia de caracteres del RSR al RBR, la indicación de estado de error de desbordamiento se establece en LSR(1). La verificación de paridad prueba la paridad par u impar en el bit de paridad que precede al primer bit de parada. Si hay un error de paridad, el error de paridad se establece en LSR(2). Hay circuitería que prueba si el bit de parada es alto. Si no lo es, se genera una indicación de error de encuadre en LSR(3).

El centro del bit de inicio se define como el recuento de reloj 7,5. Si los datos en SIN son una onda cuadrada simétrica, el centro de las celdas de datos ocurrirá dentro de +/- 3.125% del centro real, proporcionando un margen de error de 46.875%. El bit de inicio puede comenzar hasta un ciclo de reloj 16X antes de ser detectado.

## Generador de Velocidad en Baudios (BRG)

El BRG genera la temporización para la función UART, proporcionando velocidades en baudios estándar ANSI/CCITT. El oscilador que impulsa el BRG puede ser proporcionado con la adición de un cristal externo a las entradas XTAL1 y XTAL2, o un reloj externo a XTAL1. En cualquier caso, se proporciona una salida de reloj de búfer, BAUDOUT, para otros relojes del sistema. Si se utilizan dos 82C50As en la misma placa, uno puede usar un cristal y la salida de reloj de búfer puede ser enrutada directamente a XTAL1 del segundo 82C50A.

La velocidad de datos se determina por los registros de latch divisor DLL y DLM y la entrada de frecuencia o cristal externo, proporcionando BAUDOUT una salida 16X la velocidad de datos. La velocidad de bits se selecciona programando los dos latches divisores, Byte de Latch Divisor Más Significativo y Byte de Latch Divisor Menos Significativo. La configuración de DLL = 1 y DLM = 0 selecciona el divisor para dividir por 1 (dividir por 1 da la velocidad en baudios máxima para una frecuencia de entrada dada en XTAL1). El oscilador incluido se optimiza para un cristal de 10MHz. Generalmente, las frecuencias más altas son menos costosas que los cristales de menor frecuencia.

El BRG puede usar cualquiera de tres cristales populares diferentes para proporcionar velocidades en baudios estándar. La frecuencia de estos tres cristales comunes en el mercado es 1.8432MHz, 2.4576MHz y 3.072MHz. Con estos cristales estándar, velocidades de bits estándar de 50 a 38.5kbps están disponibles. Las siguientes tablas ilustran los divisores necesarios para obtener velocidades estándar usando estas tres frecuencias de cristal.

### Tabla 4: Velocidades en Baudios Usando Cristal de 1.8432MHz

| Velocidad en Baudios Deseada | Divisor Usado Para Generar Reloj 16X | Diferencia de Porcentaje de Error Entre Deseado y Real |
|---|---|---|
| 50 | 2304 | - |
| 75 | 1536 | - |
| 110 | 1047 | 0.026 |
| 134.5 | 857 | 0.058 |
| 150 | 768 | - |
| 300 | 384 | - |
| 600 | 192 | - |
| 1200 | 96 | - |
| 1800 | 64 | - |
| 2000 | 58 | 0.69 |
| 2400 | 48 | - |
| 3600 | 32 | - |
| 4800 | 24 | - |
| 7200 | 16 | - |
| 9600 | 12 | - |
| 19200 | 6 | - |
| 38400 | 3 | - |
| 56000 | 2 | 2.86 |

### Tabla 5: Velocidades en Baudios Usando Cristal de 2.4576MHz

| Velocidad en Baudios Deseada | Divisor Usado Para Generar Reloj 16X | Diferencia de Porcentaje de Error Entre Deseado y Real |
|---|---|---|
| 50 | 3072 | - |
| 75 | 2048 | - |
| 110 | 1396 | 0.026 |
| 134.5 | 1142 | 0.0007 |
| 150 | 1024 | - |
| 300 | 512 | - |
| 600 | 256 | - |
| 1200 | 128 | - |
| 1800 | 85 | 0.392 |
| 2000 | 77 | 0.260 |
| 2400 | 64 | - |
| 3600 | 43 | 0.775 |
| 4800 | 32 | - |
| 7200 | 21 | 1.587 |
| 9600 | 16 | - |
| 19200 | 8 | - |
| 38400 | 4 | - |

### Tabla 6: Velocidades en Baudios Usando Cristal de 3.072MHz

| Velocidad en Baudios Deseada | Divisor Usado Para Generar Reloj 16X | Diferencia de Porcentaje de Error Entre Deseado y Real |
|---|---|---|
| 50 | 3840 | - |
| 75 | 2560 | - |
| 110 | 1745 | 0.026 |
| 134.5 | 1428 | 0.034 |
| 150 | 1280 | - |
| 300 | 640 | - |
| 600 | 320 | - |
| 1200 | 160 | - |
| 1800 | 107 | 0.312 |
| 2000 | 96 | - |
| 2400 | 80 | - |
| 3600 | 53 | 0.628 |
| 4800 | 40 | - |
| 7200 | 27 | 1.23 |
| 9600 | 20 | - |
| 19200 | 10 | - |
| 38400 | 5 | - |

## Reset

Después del encendido, la entrada de reset maestro Schmitt trigger del 82C50A (MR) debe mantenerse alta durante TMRW ns para resetear los circuitos del 82C50A a un modo inactivo hasta la inicialización. Un nivel alto en MR causa lo siguiente:

1. Inicializa los contadores de reloj interno del transmisor y receptor.
2. Borra el Registro de Estado de Línea (LSR), excepto el bit de Registro de Desplazamiento del Transmisor Vacío (TEMT) y Registro de Espera del Transmisor Vacío (THRE), que se establecen. El Registro de Control del Módem (MCR) también se borra. Todos los elementos discretos, elementos de memoria y funciones diversas asociados con estos bits de registro también se borran o se apagan. Los latches divisores, Registro de Buffer del Receptor, Registro de Buffer del Transmisor no se ven afectados.

Después de la extirpación de la condición de reset (MR bajo), el 82C50A permanece en modo inactivo hasta que se programa.

Un reset de hardware del 82C50A establece los bits THRE y TEMT en el LSR. Cuando las interrupciones se habiliten posteriormente, ocurre una interrupción debido a THRE.

Se proporciona un resumen del efecto de un reset maestro en el 82C50A en la Tabla 7.

### Tabla 7: Operaciones de Reset del 82C50A

| Registro/Señal | Control de Reset | Reset |
|---|---|---|
| Registro de Habilitación de Interrupción | Reset Maestro | Todos los bits bajo (0-3 forzados, 4-7 permanentes) |
| Registro de Identificación de Interrupción | Reset Maestro | Bit 0 es alto, bits 1 y 2 bajo, bits 3-7 permanentemente bajo |
| Registro de Control de Línea | Reset Maestro | Todos los bits bajo |
| Registro de Control del Módem | Reset Maestro | Todos los bits bajo |
| Registro de Estado de Línea | Reset Maestro | Todos los bits bajo, excepto bits 5 y 6 están altos |
| Registro de Estado del Módem | Reset Maestro | Bits 0-3 bajo, bits 4-7 señal de entrada |
| SOUT | Reset Maestro | Alto |
| INTRPT (Errores del receptor) | Lectura LSR / MR | Bajo |
| INTRPT (Datos recibidos disponibles) | Lectura RBR / MR | Bajo |
| INTRPT (THRE) | Lectura IIR / Escritura THR / MR | Bajo |
| INTRPT (Cambios de estado del módem) | Lectura MSR / MR | Bajo |
| OUT2 | Reset Maestro | Alto |
| RTS | Reset Maestro | Alto |
| DTR | Reset Maestro | Alto |
| OUT1 | Reset Maestro | Alto |

## Programación

El 82C50A se programa mediante los registros de control LCR, IER, DLL, DLM y MCR. Estas palabras de control definen la longitud del carácter, número de bits de parada, paridad, velocidad en baudios e interfaz del módem.

Aunque los registros de control se pueden escribir en cualquier orden, el IER debe escribirse en último lugar porque controla las habilitaciones de interrupción. Una vez que el 82C50A está programado y operativo, estos registros se pueden actualizar en cualquier momento en que el 82C50A no esté transmitiendo o recibiendo datos.

Un reset de software del 82C50A es un método útil para retornar a un estado completamente conocido sin un reset del sistema. Tal reset consiste en escribir los registros LCR, latches divisores y MCR. Los registros LSR y RBR deben ser leídos antes de habilitar interrupciones para borrar cualquier bit de datos o estado residual que pueda ser inválido para operación posterior.

## Operación de Cristal

El circuito oscilador de cristal del 82C50A está diseñado para operar con un cristal de resonancia en paralelo de modo fundamental. La Tabla 8 muestra los parámetros de cristal requeridos y la configuración del circuito de cristal, respectivamente.

### Tabla 8: Parámetros Típicos del Circuito Oscilador de Cristal

| Parámetro | Especificación |
|---|---|
| Frecuencia | 1.0 a 10MHz |
| Tipo de operación | Resonancia en paralelo, modo fundamental |
| Capacitancia de carga (CL) | 20 o 32pF (Típico) |
| RSERIES (Máx) | 100Ω (f = 10MHz, CL = 32pF), 200Ω (f = 10MHz, CL = 20pF) |

Cuando se utiliza una fuente de reloj externo, la entrada XTAL1 es impulsada y la salida XTAL2 se deja sin conectar. El consumo de energía cuando se usa un reloj externo es típicamente el 50% del requerido cuando se usa un cristal. Esto se debe a la naturaleza sinusoidal de la circuitería de conducción cuando se usa un cristal.

La frecuencia máxima del 82C50A es 10MHz con un reloj externo o un cristal conectado a XTAL1 y XTAL2. Utilizando el reloj externo o cristal y un divisor de uno, el BAUDOUT máximo es 10MHz y la velocidad de datos máxima es 625Kbps.

## Especificaciones Absolutas Máximas

| Parámetro | Especificación |
|---|---|
| Voltaje de suministro | +8.0V |
| Voltaje de entrada, salida o E/S | GND -0.5V a VCC +0.5V |

## Condiciones de Operación

| Parámetro | Especificación |
|---|---|
| Rango de voltaje de operación | +4.5V a +5.5V |
| Rango de temperatura de operación C82C50A-5 | 0°C a +70°C |
| Rango de temperatura de operación I82C50A-5 | -40°C a +85°C |
| Rango de temperatura de operación M82C50A-5 | -55°C a +125°C |
| Temperatura de unión máxima | 175°C (Paquete cerámico), 150°C (Paquete plástico) |
| Rango de temperatura máxima de almacenamiento | -65°C a +150°C |
| Temperatura máxima de fusión de plomo (soldadura 10s) | +300°C (Solo punta de plomo para paquetes de montaje superficial) |

## Características de Oblea

| Parámetro | Especificación |
|---|---|
| Recuento de puertas | 1788 puertas |

*Precaución: Los esfuerzos superiores a los enumerados en "Especificaciones absolutas máximas" pueden causar daño permanente al dispositivo. Esta es solo una clasificación de esfuerzo y la operación del dispositivo en estas o cualquier otra condición por encima de las indicadas en las secciones operacionales de esta especificación no está implícita.*

*Notas:*
*1. θJA se mide con el componente montado en una placa de evaluación en aire libre.*

## Información Térmica

| Tipo de Paquete | θJA (°C/W) | θJC (°C/W) |
|---|---|---|
| Paquete CERDIP | 35 | 10 |
| Paquete DIP plástico | 50 | N/A |
| Paquete LCC plástico | 46 | N/A |

## Especificaciones Eléctricas DC

**VCC = 5.0V ± 10%, TA = 0°C a +70°C (C82C50A-5), TA = -40°C a +85°C (I82C50A-5), TA = -55°C a +125°C (M82C50A-5)**

### Voltajes y Corrientes

| Símbolo | Parámetro | Mín. | Máx. | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| VIH | Voltaje de entrada lógico uno | 2.0 (I82C50A-5, C82C50A-5), 2.2 (M82C50A-5) | - | V | - |
| VIL | Voltaje de entrada lógico cero | - | 0.8 | V | - |
| VTH | Voltaje de entrada lógico uno del disparador Schmitt | 2.0 (82C50A-5, C82C50A-5), 2.2 (M82C50A-5) | - | V | Entrada MR |
| VTL | Voltaje de entrada lógico cero del disparador Schmitt | - | 0.8 | V | Entrada MR |
| VIH (CLK) | Voltaje lógico uno del reloj | VCC-0.8 | - | V | Reloj externo |
| VIL (CLK) | Voltaje lógico cero del reloj | - | 0.8 | V | Reloj externo |
| VOH | Voltaje de salida alto | 3.0 (IOH = -2.5mA), VCC-0.4 (IOH = -100mA) | - | V | - |
| VOL | Voltaje de salida bajo | - | 0.4 | V | IOL = +2.5mA |
| II | Corriente de fuga de entrada | -1.0 | +1.0 | µA | VIN = GND o VCC, pines DIP 9, 10, 12, 13, 14, 18, 19, 21, 22, 25-28, 35-39 |
| IO | Corriente de fuga de entrada/salida | -10.0 | +10.0 | µA | VO = GND o VCC, pines DIP 1-8 |
| ICCOP | Corriente de suministro de operación | - | 6 | mA | Reloj externo F = 2.4576MHz, VCC = 5.5V, VIN = VCC o GND, salidas abiertas |
| ICCSB | Corriente de suministro en espera | - | 100 | µA | VCC = 5.5V, VIN = VCC o GND, salidas abiertas |

### Capacitancia

**TA = 25°C**

| Símbolo | Parámetro | Típico | Unidades | Condiciones de prueba |
|---|---|---|---|---|
| CIN | Capacitancia de entrada | 15 | pF | FREQ = 1MHz, todas las mediciones se refieren a GND del dispositivo |
| COUT | Capacitancia de salida | 15 | pF | - |
| CI/O | Capacitancia E/S | 20 | pF | - |

## Especificaciones Eléctricas AC

**VCC = 5.0V ± 10%, TA = 0°C a +70°C (C82C50A-5), TA = -40°C a +85°C (I82C50A-5), TA = -55°C a +125°C (M82C50A-5)**

### Requisitos de Temporización - 82C50A-5

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (1) TAW | Ancho de strobe de dirección | 50 | - | ns | - |
| (2) TAS | Tiempo de configuración de dirección | 60 | - | ns | Nota 1 |
| (3) TAH | Tiempo de retención de dirección | 0 | - | ns | - |
| (4) TCS | Tiempo de configuración de selección de chip | 60 | - | ns | Nota 1 |
| (5) TCH | Tiempo de retención de selección de chip | 0 | - | ns | - |
| (6) TDIW | Ancho de strobe DISTR/DISTR | 150 | - | ns | - |
| (7) TRC | Retardo de ciclo de lectura | 270 | - | ns | Nota 1 |
| (8) RC | Ciclo de lectura = TAR + TDIW + TRC | 500 | - | ns | - |
| (9) TDD | Retardo DISTR/DISTR a deshabilitación de controlador | - | 75 | ns | - |
| (10) TDDD | Retardo DISTR/DISTR a datos | - | 120 | ns | - |
| (11) THZ | DISTR/DISTR a retardo de datos flotantes | 10 | 75 | ns | - |
| (12) TDOW | Ancho de strobe DOSTR/DOSTR | 150 | - | ns | - |
| (13) TWC | Retardo de ciclo de escritura | 270 | - | ns | Nota 1 |
| (14) WC | Ciclo de escritura = TAW + TDOW + TWC | 500 | - | ns | - |
| (15) TDS | Tiempo de configuración de datos | 90 | - | ns | - |
| (16) TDH | Tiempo de retención de datos | 60 | - | ns | - |

*Nota: 1. Al usar el 82C50A en modo multiplexado (ADS operativo), funcionará en sistemas 80C86/88 con una frecuencia de operación máxima de 3MHz.*

### Especificaciones Eléctricas AC - Temporización

**VCC = 5.0V ± 10%, TA = 0°C a +70°C (C82C50A-5), TA = -40°C a +85°C (I82C50A-5), TA = -55°C a +125°C (M82C50A-5)**

**82C50A-5**

#### Operación Desmultiplexada

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (17) TCSC | Retardo de salida de selección de chip desde selección | - | 125 | ns | - |
| (18) TRA | Tiempo de retención de dirección desde DISTR/DISTR | 20 | - | ns | - |
| (19) TRCS | Tiempo de retención de selección de chip desde DISTR/DISTR | 20 | - | ns | - |
| (20) TAR | Retardo DISTR/DISTR desde dirección | 80 | - | ns | - |
| (21) TCSR | Retardo DISTR/DISTR desde selección de chip | 80 | - | ns | - |
| (22) TWA | Tiempo de retención de dirección desde DOSTR/DOSTR | 20 | - | ns | - |
| (23) TWCS | Tiempo de retención de selección de chip desde DOSTR/DOSTR | 20 | - | ns | - |
| (24) TAW | Retardo DOSTR/DOSTR desde dirección | 80 | - | ns | - |
| (25) TCSW | Retardo DOSTR/DOSTR desde selección | 80 | - | ns | - |
| (26) TMRW | Ancho de pulso de reset maestro | 500 | - | ns | - |
| (27) TXH | Duración del pulso alto del reloj | 40 | - | ns | - |
| (28) TXL | Duración del pulso bajo del reloj | 40 | - | ns | - |

#### Generador de Baudios

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (29) N | Divisor de baudios | 1 | 2^16-1 | - | - |
| (30) TBLD | Retardo de borde negativo de salida de baudios | - | 250 | ns | - |
| (31) TBHD | Retardo de borde positivo de salida de baudios | - | 250 | ns | - |
| (32) TLW | Tiempo bajo de salida de baudios | 40 | - | ns | TXL = 50ns |
| (33) THW | Tiempo alto de salida de baudios | 40 | - | ns | TXH = 50ns |

#### Receptor

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (34) TSCD | Retardo desde RCLK a tiempo de muestra | - | 250 | ns | - |
| (35) TSiNT | Retardo desde parada a establecer interrupción | 1 | 1 | Ciclos BAUDOUT | - |
| (36) TRiNT | Retardo desde DISTR/DISTR (lectura RBR) a restablecer interrupción | - | 250 | ns | - |

#### Transmisor

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (37) THR | Retardo desde DOSTR/DOSTR a restablecer interrupción | - | 250 | ns | - |
| (38) TlRS | Retardo desde reset INTR inicial a inicio de transmisión | 8 | 24 | Ciclos BAUDOUT | - |
| (39) TS1 | Retardo desde escritura inicial a interrupción | 16 | 32 | Ciclos BAUDOUT | - |
| (40) TSTi | Retardo desde parada a interrupción (THRE) | 8 | 24 | Ciclos BAUDOUT | - |
| (41) TiR | Retardo desde DISTR/DISTR (lectura IIR) a restablecer interrupción (THRE) | - | 250 | ns | - |

#### Control del Módem

| Símbolo | Parámetro | Mín. | Máx | Unidades | Condiciones de prueba |
|---|---|---|---|---|---|
| (42) TMDO | Retardo desde DOSTR/DOSTR a salida | - | 500 | ns | - |
| (43) TSIM | Retardo para establecer interrupción desde entrada del módem | - | 500 | ns | - |
| (44) TRiM | Retardo para restablecer interrupción desde DISTR/DISTR (lectura MSR) | - | 500 | ns | - |

### Circuito de Prueba AC

**Definición de Tabla de Condiciones de Prueba**

| Salida del dispositivo bajo prueba | Punto de prueba | IOH | IOL | V1 | R1 | C1 (Nota) |
|---|---|---|---|---|---|---|
| - | - | -2.5mA | +2.5mA | 1.7V | 520Ω | 100pF |

*Nota: Incluye capacitancia de estancia y estancia jig.*

### Entrada de Prueba AC, Forma de Onda de Salida

| Entrada | Salida |
|---|---|
| VIH + 0.4V | VOH |
| 1.5V | 1.5V |
| VIL - 0.4V | VOL |

**Prueba AC:**

Todas las señales de entrada deben cambiar entre VIL -0.4V y VIH +0.4V. Los tiempos de subida y caída de la entrada se conducen a 1ns/V.

## Formas de Onda de Temporización

### Figura 3: Entrada de Reloj Externo

*Muestra las señales XTAL1 oscilando entre 0.8V y 2.0V con los tiempos tXH (duración del pulso alto) y tXL (duración del pulso bajo) marcados.*

### Figura 4: Puntos de Prueba AC

*Muestra los puntos de prueba AC con niveles de voltaje VIH + 0.4V, 1.5V, VIL - 0.4V y VOL.*

### Figura 5: Temporización de BAUDOUT

*Nota original: Muestra los diagramas de temporización para BAUDOUT con diferentes valores de divisor, incluyendo las especificaciones de tiempo para tBLD (retardo de borde negativo), tBHD (retardo de borde positivo), tHW (tiempo alto) y tLW (tiempo bajo).*

*Nota: tBLD (N=1) es la única especificación medida desde el borde descendente de XTAL1. Todos los demás tBLD y tBHD se miden desde el borde ascendente de XTAL1.*

### Figura 6: Ciclo de Escritura

*Muestra la temporización para operaciones de escritura, incluyendo ADS, direcciones (A2, A1, A0), selección de chip (CS2, CS1, CS0), CSOUT, DOSTR/DOSTR y datos (D0-D7). Los tiempos de configuración y retención se marcan con tAW, tAS, tAH, tCS, tCH, tDOW, tWC, tDS y tDH.*

*Nota: Los tiempos marcados con † solo aplican cuando ADS está conectado bajo.*

### Figura 7: Ciclo de Lectura

*Muestra la temporización para operaciones de lectura, incluyendo ADS, direcciones (A2, A1, A0), selección de chip (CS2, CS1, CS0), CSOUT, DISTR/DISTR, deshabilitación del controlador (DDIS) y datos (D0-D7). Los tiempos incluyen tAW, tAS, tAH, tCS, tCH, tDIW, tRC, tDD, tDDD y tHZ.*

*Nota: Los tiempos marcados con † solo aplican cuando ADS está conectado bajo.*

### Figura 8: Temporización del Receptor

*Muestra la temporización del receptor incluyendo RCLK, SAMPLE CLK, SIN (entrada de datos serie con bits de inicio, datos de 5-8 bits, paridad y parada), interrupción y DISTR/DISTR. Los tiempos tSCD, tSINT, tRINT se marcan.*

*Nota 1: Ver temporización del ciclo de escritura.*
*Nota 2: Ver temporización del ciclo de lectura.*

### Figura 9: Temporización del Transmisor

*Muestra la temporización del transmisor incluyendo SOUT (salida serie con bits de inicio, datos de 5-8, parada), DOSTR/DOSTR, interrupción THRE, DISTR/DISTR y lectura IIR. Los tiempos tIRS, tSTI, tHR, tSI, tIR se marcan.*

*Nota 1: Ver temporización del ciclo de escritura.*
*Nota 2: Ver temporización del ciclo de lectura.*

### Figura 10: Temporización de Controles del Módem

*Muestra la temporización del control del módem incluyendo DOSTR/DOSTR (escritura de MCR), RTS/DTR/OUT1/OUT2, CTS/DSR/DCD/RI, interrupción y DISTR/DISTR (lectura MSR). Los tiempos tMDO, tRIM y tSIM se marcan.*

*Nota 1: Ver temporización del ciclo de escritura.*
*Nota 2: Ver temporización del ciclo de lectura.*

---

*Documento de especificaciones técnicas del circuito integrado Harris 82C50A UART/BRG. Traducido del inglés y formateado en Markdown. Algunos diagramas y formas de onda originales no se pudieron reconstruir completamente debido a limitaciones del formato OCR.*
