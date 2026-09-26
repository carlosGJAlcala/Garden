---
title: "Sistemas digitales"
---


# Tema 1. Sistemas digitales
## Índice
1. Introducción
2. Sistemas embebidos
3. El microprocesador
4. El microcontrolador
5. Arduino
6. El entorno de programación
7. Programación
8. Sensores y actuadores
## 1. Introducción: ¿Qué es un sistema?
Un sistema puede ser definido como todo aquello que interactúa con su entorno. Un esquema general podría ser: Entrada : Procesamiento : Salida.
### Sistemas digitales
Recordando la introducción de la asignatura: una señal analógica ( por ejemplo, la de una sonda de temperatura, con tensión o corriente proporcional a la temperatura) pasa por un circuito amplificador, filtro, etc. ( temas 1 y 2), después por una conversión analógico-digital ( tema 3) que la transforma en una secuencia de bits ( 0 1 0 1 0 0...). Esa secuencia entra en un sistema digital de control ( tema 4), y de ahí, mediante una conversión digital-analógica ( tema 3), se actúa por ejemplo sobre un sistema de climatización.
Los sistemas digitales pueden implementarse mediante:
- Circuitos combinacionales / secuenciales: componentes discretos.
- Circuitos de lógica programable ( PLDs, FPGAs…).
- Microprocesadores.
- Microcontroladores.
- Autómatas programables ( PLC's).
- ...
En la práctica, hoy en día, el diseño de un circuito digital para una determinada aplicación no se resuelve mediante el diseño desde cero de un sistema digital dedicado y específico para dicha aplicación, sino que se implementa mediante un sistema empotrado o embebido: un sistema digital programable basado en un microprocesador o un microcontrolador cuya programación permite su uso en muy diferentes aplicaciones.
## 2. Sistemas embebidos
Un sistema embebido ( embedded) o empotrado es un sistema de computación diseñado para realizar una o algunas pocas funciones dedicadas. Al contrario de lo que ocurre con los ordenadores de propósito general, que están diseñados para cubrir un amplio rango de necesidades, los sistemas embebidos se diseñan para cubrir necesidades específicas.
Son generalmente sistemas reactivos de tiempo real:
- "Reaccionan" a eventos externos.
- Mantienen interacción permanente.
- Están continuamente funcionando.
- Están sujetos a restricciones externas de tiempo.
- Realizan varias tareas concurrentemente.
### Ejemplos
- Electrónica de consumo: TVs, lavadoras, frigoríficos, lavaplatos...
- Automóviles: control de velocidad, climatización, visualización, ABS, ASR, inyección...
- Telecomunicaciones: radios trunking, teléfonos móviles...
- Aviónica, espacial: computadores de vuelo, de misión, robots...
- Defensa: bombas y misiles inteligentes, vehículos, dirección de tiro...
**Sistema de guiado Apollo 11 ( 1969)**, primera vez que se emplearon circuitos integrados:
- Datos: 16 bits ( 15 bits datos + bit paridad).
- Memoria de tipo magnético: ROM de 36.864 × 2 bytes; RAM de 2.048 × 2 bytes.
- Número de instrucciones: 34.
- Frecuencia de reloj: 85 kHz.
- Número de puertas lógicas: 5.600.
- Peso: 30 kg. Consumo: 70 W.
**Raspberry Pi 3 Model B ( 2016)**:
- CPU ARMv8 quad-core a 1.2 GHz de 64 bits.
- 802.11n Wireless LAN, Bluetooth 4.1, Bluetooth Low Energy ( BLE).
- 1 GB de RAM.
- 40 pines GPIO.
- Slot para tarjeta Micro SD.
- 4 puertos USB, puerto Ethernet.
- Audio jack de 3.5mm combinado con vídeo compuesto.
- Salida Full HDMI, interfaz para cámara, interfaz para display.
### Características de los sistemas embebidos
**Fiabilidad y seguridad**
- Un fallo en un sistema de control puede hacer que el sistema controlado se comporte de forma peligrosa o antieconómica.
- Es importante asegurar que si el sistema de control falla lo haga de forma que el sistema controlado quede en un estado seguro.
- Hay que prever los posibles fallos o excepciones del diseño.
**Eficiencia**: gran parte de los sistemas de control deben responder con gran rapidez a los cambios en el sistema controlado.
**Bajo consumo**
- Muchos de estos sistemas están alimentados con batería o pilas. A menor consumo, mayor autonomía.
- En muchos casos hay necesidades de bajo voltaje ( 3V).
**Bajo peso**: característica deseable en sistemas portátiles. No depende únicamente del computador embarcado y su periferia, sino también de la alimentación ( baterías) o de los sensores y actuadores.
**Bajo precio**: aplicable a electrónica de consumo y otros dispositivos con mercados muy competitivos ( p. ej. telefonía móvil).
**Pequeñas dimensiones**: las dimensiones de un sistema empotrado no dependen solo de sí mismo, sino también del espacio disponible en el sistema que controla y/o monitoriza.
**Concurrencia**
- Las distintas tareas del sistema controlado o monitorizado funcionan simultáneamente.
- El sistema de control debe atenderlas y generar las acciones de control o visualización de forma simultánea.
- Si hay una sola unidad de proceso, se emplean técnicas de multiproceso mediante sistemas operativos en tiempo real. Si hay varias unidades de proceso se habla de multiprocesadores.
## 3. El microprocesador
El microprocesador es un circuito digital universal, de propósito general, muy versátil. Funciona ejecutando una serie de "pasos" básicos:
- Cada uno de los pasos es una instrucción.
- Cada elemento de información es un dato.
- El programa es el conjunto ordenado de todas las instrucciones.
Para variar la funcionalidad del circuito se modifica el programa.
El microprocesador es la unidad central de proceso que permite ejecutar un programa, pero requiere para su utilización en la práctica de:
- Reloj.
- Memoria ( ROM, RAM).
- Buses de comunicación.
- Periféricos de E/S.
Diseñar sistemas embebidos basados en microprocesadores implica diseñar, para cada problema, una placa con el micro, la memoria, etc.
## 4. El microcontrolador
Un microcontrolador es un circuito integrado de alta escala de integración que incorpora la mayor parte de los elementos que configuran un sistema informático: el microprocesador, la memoria, periféricos, E/S, etc. Un microcontrolador permite la implementación rápida de una computadora con una circuitería externa mínima, lo que convierte estos dispositivos en una buena solución para el diseño de sistemas embebidos.
Existen diferentes tipos de microcontroladores en función de su arquitectura ( Von Neumann, Harvard), las características del conjunto de instrucciones con las que se programan ( RISC, CISC), la capacidad del procesador ( 16, 32 o 64 bits), cantidad de memoria, número de periféricos, etc. Algunos de los microcontroladores más comunes son: SAM7 o SAM3 ( Atmel), ColdFire ( Motorola), Cortex-M3 o Cortex-M0 ( NXP o Texas).
La arquitectura genérica de un microcontrolador se compone de:
- Procesador: unidad de control, unidad aritmético-lógica, registros, buses, conjunto de instrucciones.
- Memoria: de programas y de datos ( ROM, EEPROM, FLASH, RAM, SRAM, DRAM, etc.).
- Periféricos: conversores analógico/digitales, puertos de comunicación serie ( SPI, I2C, USB), Ethernet, modulador de ancho de pulsos, temporizadores, contadores, entradas y salidas de propósito general.
## 5. Arduino
En 2005, la empresa Arduino lanzó al mercado una primera placa que integraba un microcontrolador ( AVR de Atmel) y algunos puertos digitales y analógicos de entrada/salida junto con un sencillo entorno de programación. En la actualidad hay comercializadas distintas alternativas ( Uno, Pro, Mega, etc.) con placas de expansión ( shields) que permiten desarrollar multitud de aplicaciones avanzadas.
Referencia: https://www.arduino.cc/en/Guide/HomePage
### Arduino UNO
Elementos principales de la placa:
- Microcontrolador AVR.
- Circuito de reloj ( 16 MHz).
- Circuito de reset.
- Conversor USB-serie.
- Regulador de alimentación.
- Pines de conexión.
Características del microcontrolador ATmega328P:
- Alimentación: 5V.
- E/S digitales: 14.
- E analógicas: 6.
- Memoria flash: 32 KB.
- SRAM: 2 KB.
- EEPROM: 1 KB.
- LED integrado: pin 13.
- Longitud: 68.6 mm. Anchura: 53.4 mm. Peso: 25 g.
La placa incluye E/S digitales, el circuito de reset, el ATmega328P, el puerto USB, la alimentación externa y las E/S analógicas.
## 6. El entorno de programación
- Gratuito.
- Interfaz gráfica en Java.
- Muy sencillo.
- Integra editor, compilador, descarga a placa y monitor serie.
- Archivos `.ino`; también soporta `.c`, `.cpp`, `.h`.
- Organización del código por pestañas.
Para descargar el entorno de programación: https://www.arduino.cc/en/Main/Software
El entorno cuenta con los botones de compilar, nuevo, guardar, cargar y abrir, una ventana de edición y una ventana de mensajes.
## 7. Programación
Un programa debe contener al menos las dos funciones siguientes:
- `void setup ()`: función que se ejecuta una única vez al comenzar la ejecución del programa, después de su descarga, después de encender la alimentación o tras la pulsación del botón de reset.
- `void loop ()`: función que se ejecuta cíclicamente de manera ininterrumpida hasta que se desconecte la alimentación de la placa.
Un ejemplo típico hace parpadear un LED de la propia placa.
### Tipos de datos
- `void`: utilizado en la declaración de funciones que no devuelven ningún valor.
- `boolean`: true o false.
- `char`: un carácter ('A', 'f', …).
- `byte`: almacena un valor numérico de 8 bits entre 0 y 255.
- `int`: número entero almacenado en 16 bits, entre -32768 y 32767.
- `unsigned int`: número entero positivo entre 0 y 65535.
- `long`: número entero almacenado en 32 bits ( de -2.147.483.648 a 2.147.483.647).
- `float`: número real.
- `array`: conjunto de variables que se acceden mediante un índice.
- `string`: array de caracteres.
Ejemplos:
```cpp
void loop ()
boolean activado = false;
char letra = 'A';
byte num = B0101; // número 5 en binario
int i = 8;
long l = 1534761;
float f = 50.0;
// array
int numeros[6]; // crea un array vacío para almacenar 6 números enteros
int numeros2[] = {2, 4, 8, 3, 6}; // array de enteros rellenado
int n = numeros2[2]; // variable entera 'n' que coge el valor de la tercera posición del array ( la primera es la posición 0)
```
### Estructuras de control
```cpp
if ( v > 50) {
 // se hace algo
}
if ( v > 50) {
 // se hace algo
} else {
 // se hace otra cosa
}
int v = 0;
while ( v < 200) {
 // se hace algo 200 veces
 v++; // se incrementa la variable v
}
for ( int v = 0; v < 6; v++) {
 println ( v); // imprime los números del 0 al 5
}
do {
 // haz algo mientras v sea menor que 5
} while ( v < 5);
switch ( v) {
 case 1:
 // haz algo si v es 1
 break;
 case 2:
 // haz algo si v es 2
 break;
 default:
 // haz algo en el resto de casos
 break;
}
```
### Funciones disponibles
**Entradas y salidas digitales**
- `pinMode ( pin, mode)`: configura un pin como entrada ( INPUT) o salida ( OUTPUT).
 ```cpp
 int pin = 12;
 pinMode ( pin, INPUT); // configura el pin 12 como entrada
 ```
- `digitalWrite ( pin, value)`: escribe un valor alto ( HIGH) o bajo ( LOW) en un pin configurado como salida.
 ```cpp
 digitalWrite ( 10, HIGH); // escribe un 1 en el pin 10
 ```
- `digitalRead ( pin)`: lee el valor de un pin previamente configurado como entrada.
 ```cpp
 int val;
 val = digitalRead ( 11); // guarda el valor del pin 11 en val
 ```
**Comunicación serie**
- `Serial.begin ( velocidad)`: configura la velocidad de la comunicación serie. Ej.: `Serial.begin ( 9600);`
- `Serial.print ( dato)`: escribe un dato por el puerto serie. Ej.: `Serial.print ("Hola");`
- `Serial.println ( dato)`: funciona igual que `Serial.print` añadiendo un salto de línea al final.
**Entradas analógicas**
- `analogRead ( pin)`: devuelve el valor de una entrada analógica.
 ```cpp
 int pinAnalog = 3;
 int valor;
 valor = analogRead ( pinAnalog);
 ```
**Temporización**
- `delay ( tiempo)`: detiene la ejecución del programa durante los milisegundos indicados en la variable tiempo. Ej.: `delay ( 500);` detiene el programa durante 500 milisegundos.
- `delayMicroseconds ( tiempo)`: detiene la ejecución del programa durante los microsegundos indicados en la variable tiempo. Ej.: `delayMicroseconds ( 500);` detiene el programa durante 500 microsegundos.
- `millis ()`: devuelve, en milisegundos, el tiempo transcurrido desde que empezó a ejecutarse el programa hasta el momento en que se ejecuta la instrucción. Ej.: `tiempotranscurrido = millis ();`
La comunidad de usuarios de Arduino es grande y facilita una amplia variedad de librerías para simplificar la programación de multitud de aplicaciones ( open source). Para utilizar una librería es necesario descargar el archivo `.zip` correspondiente, incluirla en el entorno de programación e incluirla en el programa con la instrucción `#include <NombreLibreria.h>`.
La mejor manera de empezar son los ejemplos básicos que incluye el propio entorno de programación. Existen multitud de ejemplos y librerías disponibles en internet ( hardware y software abierto).
Recursos oficiales:
- Referencia completa del lenguaje de programación: https://www.arduino.cc/en/Reference/HomePage
- Multitud de librerías para todo tipo de aplicaciones y periféricos: http://playground.arduino.cc
## 8. Sensores y actuadores
- *GP2D12**: sensor que permite medir distancias mediante infrarrojos. Indica mediante una salida analógica la distancia medida. ( https://dartecne.wordpress.com/recursos/sensores/)
- *HC-SR04**: sensor que permite medir distancias mediante ultrasonidos. Indica mediante una salida analógica la distancia medida.
- *CNY70**: sensor óptico infrarrojo, de un rango de corto alcance ( menos de 5 cm), que se utiliza para detectar colores de objetos y superficies ( emisor y receptor enfrentados a la superficie, clara u oscura, en un área marcada).
- *DHT11**: sensor de temperatura y humedad que funciona con 3.3 o 5V de alimentación. Rango de temperatura de 0º a 50º con 5% de precisión; rango de humedad del 20% al 80% con 5% de precisión; 1 muestra por segundo; bajo consumo; devuelve la medida en ºC mediante una señal digital.
- *Sistema de visualización**: dispositivo que permite mostrar información de manera gráfica. Existen muchos sistemas distintos de variada complejidad ( número de caracteres, colores, etc.) y diferentes tecnologías.
- *Motor paso a paso** ( stepper): sistema electromecánico en el que impulsos eléctricos provocan desplazamientos en ángulos discretos o pasos. Los pasos pueden ser muy pequeños, por lo que son motores muy precisos con un posicionamiento muy exacto.
