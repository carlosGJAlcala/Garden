---
title: "Buffers De Memoria Ciclicos"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
Un **buffer cíclico** (también conocido como **circular buffer** o **ring buffer**) es una estructura de datos que permite almacenar elementos en una **cola de tamaño fijo**, donde el final del buffer se conecta con el principio formando una **estructura circular lógica**. Es ampliamente utilizado en **sistemas embebidos**, **procesamiento de señales**, **robótica**, y **aplicaciones de tiempo real**, donde es necesario gestionar flujos de datos de forma eficiente y continua sin incurrir en problemas de rendimiento o fragmentación de memoria.

---

##  ¿Cómo funciona un buffer cíclico?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Imagina un array con N posiciones, y dos punteros:

- `head` (o `write_ptr`): indica **dónde escribir** el siguiente dato.
    
- `tail` (o `read_ptr`): indica **dónde leer** el próximo dato.
    

### ️ Comportamiento:

1. **Escritura**: cuando se escribe un nuevo dato, se coloca en la posición `head`, y luego `head` se incrementa (circularmente).
    
2. **Lectura**: al leer un dato, se toma de la posición `tail`, y luego `tail` se incrementa (circularmente).
    
3. Si `head == tail`, el buffer está **vacío** (lectura sin datos).
    
4. Si al escribir `head + 1 == tail`, el buffer está **lleno** (escritura sin espacio), y puede sobrescribir o bloquear, según la política.
    

---

##  Ejemplo gráfico (buffer de tamaño 5)

```text
[0] [1] [2] [3] [4]
 ↑              ↑
 TAIL         HEAD
```

Si insertas un nuevo dato, HEAD se moverá a la posición 0 nuevamente (mod N), creando el comportamiento **circular**.

---

##  Propiedades principales

|Propiedad|Detalle|
|---|---|
|Estructura|Array de tamaño fijo|
|Índices|Punteros cíclicos (modulo N)|
|Eficiencia|Tiempo constante O(1) en lectura y escritura|
|Uso de memoria|Muy eficiente, sin realocaciones ni fragmentación|
|Overwriting|Opcional: puede sobrescribir datos viejos si se llena|
|Sincronización|Requiere semáforos/mutexes en entornos multihilo|

---

##  Ejemplo en C (buffer de enteros)

```c
#define SIZE 10
int buffer[SIZE];
int head = 0;
int tail = 0;

int is_empty() { return head == tail; }
int is_full()  { return (head + 1) % SIZE == tail; }

void insert(int data) {
    if (!is_full()) {
        buffer[head] = data;
        head = (head + 1) % SIZE;
    } else {
        // Política: sobrescribir o descartar
    }
}

int read() {
    if (!is_empty()) {
        int val = buffer[tail];
        tail = (tail + 1) % SIZE;
        return val;
    } else {
        return -1; // Buffer vacío
    }
}
```

---

##  ¿Dónde se usa un buffer cíclico?

###  Robótica

- Almacenamiento de lecturas de sensores (LIDAR, IMU, sonar, etc.) para procesamiento posterior.
    
- Gestión de comandos motores (velocidades, trayectorias, posiciones) sin perder datos.
    
- Buffer intermedio entre threads en sistemas ROS o RTOS.
    

###  Audio / vídeo en tiempo real

- Streaming de frames de audio o vídeo sin lag ni pérdidas.
    
- Captura y reproducción en aplicaciones multimedia.
    

###  Sistemas operativos / controladores

- Buffers UART/RS-232.
    
- Buffers de red en stacks TCP/IP embebidos.
    

###  Telecomunicaciones

- Enrutamiento de paquetes en routers o switches.
    
- Compensación de jitter en buffers de reproducción.
    

---

##  Ventajas del buffer cíclico

- **Eficiencia temporal y espacial**: no necesita realocar memoria ni mover datos.
    
- **Predicción y estabilidad**: esencial en sistemas de tiempo real.
    
- **Control de flujo**: permite desacoplar productores y consumidores.
    

---

## ️ Consideraciones de diseño

1. **Tamaño**: debe elegirse en función del ancho de banda y la frecuencia de lectura/escritura.
    
2. **Política de colisión**:
    
    - ¿Qué hacer cuando se llena? ¿Sobrescribir? ¿Descartar?
        
3. **Entornos concurrentes**:
    
    - Usar **mutexes o semáforos** si hay múltiples productores o consumidores.
        
4. **Delay controlado**:
    
    - En sistemas como audio/video, un buffer demasiado pequeño genera pérdidas; uno demasiado grande introduce latencia.
        

---

##  Conclusión

El **buffer cíclico** es una de las estructuras más eficientes para manejar datos en flujo continuo, especialmente cuando se necesita bajo consumo de CPU, latencia mínima y uso controlado de memoria. Su implementación es simple, pero poderosa, y forma parte integral de cualquier arquitectura robusta en sistemas embebidos, tiempo real, y robótica.