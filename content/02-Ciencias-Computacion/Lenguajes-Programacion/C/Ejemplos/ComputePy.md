---
title: "Computepy"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - c
---
El código que has proporcionado es un programa que utiliza **hilos (threads)** para realizar una estimación de Pi mediante el método de Monte Carlo, una técnica probabilística para aproximar el valor de Pi utilizando puntos aleatorios dentro de un cuadrado unitario y verificando cuántos de esos puntos caen dentro de un círculo de radio 1. A continuación, te proporcionaré una explicación detallada del código.

### 1. **Explicación del archivo principal (`main.c`)**


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Condiciones-de-Carrera|Condiciones de Carrera]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

```c
#include <stdio.h>
#include <stdlib.h>

#include "compute.h"

int main(int argc, char * argv[]) {

    int points, threads;
    char * endptr = NULL;

    /* First, we have to check the number of arguments */
    if (argc != 3) {
        printf("error: invalid number of arguments\n"
               "usage: %s points threads\n"
               "\tpoints: number of points to use [1-500000000]\n"
               "\tthreads: number of threads to use [1-8]\n", argv[0]);
        return 1;
    }

    /* Now we have to convert and check argument 1, the number of points */
    points = strtol(argv[1], &endptr, 10);
    if (*endptr != '\0') {
        printf("error: %s cannot be casted to a decimal integer\n", argv[1]);
        return 1;
    } else if (points <= 0 || points > 500000000) {
        printf("error: points %s is out of range\n", argv[1]);
        return 1;
    }

    /* And finally argument 2, the number of threads */
    threads = strtol(argv[2], &endptr, 10);
    if (*endptr != '\0') {
        printf("error: %s cannot be casted to a decimal integer\n", argv[2]);
        return 1;
    } else if (threads <= 0 || threads > 8) {
        printf("error: threads %s is out of range\n", argv[2]);
        return 1;
    }

    /* Call the compute function */
    compute(points, threads);

    return 0;
}
```

#### **Descripción:**
1. **Argumentos de la línea de comandos**:
   - El programa espera dos argumentos:
     - **`points`**: El número de puntos aleatorios que se usarán para la simulación de Monte Carlo.
     - **`threads`**: El número de hilos que se utilizarán para realizar los cálculos.

2. **Comprobación de argumentos**:
   - Se asegura de que el número de puntos sea un valor entre 1 y 500,000,000, y que el número de hilos esté entre 1 y 8.
   - Si los valores no cumplen con estas condiciones, se imprime un mensaje de error y se termina el programa.

3. **Llamada a la función `compute()`**:
   - Una vez que los argumentos son validados, se llama a la función `compute()` para realizar el cálculo de Pi usando el método de Monte Carlo.

### 2. **Archivo de cabecera (`compute.h`)**

```c
#ifndef __COMPUTE_H__
#define __COMPUTE_H__

void compute(int npoints, int nthreads);

#endif // __COMPUTE_H__
```

#### **Descripción:**
- El archivo `compute.h` es un encabezado que declara la función `compute`, que se define en otro archivo (probablemente `compute.c`).
- La función `compute` se encarga de realizar la estimación de Pi utilizando los puntos y hilos proporcionados.

### 3. **Archivo de implementación (`compute.c`)**

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include "compute.h"

/* Global variable to store the number of hits */
unsigned int hits;

/* Mutex for mutual exclusion */
pthread_mutex_t mutex;

/* Thread function */
void *thread_function(void *data)
{
    double x, y;
    struct drand48_data randBufferX, randBufferY;
    int points = *((int *)data);
    int contador = 0;

    /* Loop to calculate how many points fall within the circle */
    for (int i = 0; i < points; i++) {
        drand48_r(&randBufferX, &x);
        drand48_r(&randBufferY, &y);
        
        /* Check if the point is inside the unit circle using Pythagoras' theorem */
        if ((x * x + y * y) < 1) {
            contador++;
        }
    }

    /* Protect the global variable 'hits' with a mutex */
    pthread_mutex_lock(&mutex);
    hits += contador;
    pthread_mutex_unlock(&mutex);

    return NULL;
}

void compute(int npoints, int nthreads)
{
    int npoints_per_thread = npoints / nthreads; // Points per thread
    int leftover_points = npoints % nthreads; // Leftover points that are not evenly divisible
    pthread_mutex_init(&mutex, NULL);

    pthread_t thread_id[nthreads];

    /* Launch threads to calculate points */
    for (int i = 0; i < nthreads; i++) {
        int points_for_thread = (i == nthreads - 1) ? npoints_per_thread + leftover_points : npoints_per_thread;
        pthread_create(&thread_id[i], NULL, thread_function, &points_for_thread);
    }

    /* Wait for all threads to finish */
    for (int i = 0; i < nthreads; i++) {
        pthread_join(thread_id[i], NULL);
    }

    /* Calculate and print the value of Pi */
    double pi = 4.0 * hits / npoints;
    printf("Pi approximation: %.8f\n", pi);
}
```

#### **Descripción del código en `compute.c`:**

1. **Variables globales**:
   - `hits`: Esta variable guarda el número total de puntos que caen dentro del círculo unitario.
   - `mutex`: Un mutex que asegura la exclusión mutua cuando varios hilos intentan modificar la variable `hits` al mismo tiempo.

2. **`thread_function`**:
   - Esta función se ejecuta en cada hilo y simula la generación de puntos aleatorios dentro de un cuadrado de tamaño 1x1.
   - Usa el generador de números aleatorios `drand48_r()` para obtener dos coordenadas (`x` y `y`).
   - Se verifica si el punto cae dentro de un círculo de radio 1 (usando el teorema de Pitágoras: \( x^2 + y^2 < 1 \)).
   - Si el punto está dentro del círculo, se incrementa un contador local.
   - Después de que el hilo termine, el contador local se suma al total global `hits` de manera segura, usando un `mutex` para evitar condiciones de carrera.

3. **`compute`**:
   - **Distribución de puntos entre hilos**: El número total de puntos se divide de manera equitativa entre los hilos. Si no se puede dividir de manera exacta, los puntos restantes se asignan al último hilo.
   - **Creación de hilos**: Se crean los hilos utilizando `pthread_create`, pasando la función `thread_function` y el número de puntos a procesar por cada hilo.
   - **Espera de hilos**: Después de crear todos los hilos, el programa espera a que todos terminen utilizando `pthread_join`.
   - **Cálculo de Pi**: Finalmente, se calcula una aproximación de Pi usando la fórmula:

   \[
   \pi \approx 4 \times \frac{\text{número de puntos dentro del círculo}}{\text{número total de puntos}}
   \]

   Se imprime el valor de Pi con 8 decimales.

### **Conclusión**:

Este programa implementa el método de Monte Carlo para estimar el valor de Pi, utilizando **hilos (threads)** para mejorar el rendimiento y dividir el trabajo. Cada hilo genera un conjunto de puntos aleatorios y cuenta cuántos caen dentro de un círculo de radio 1. La variable global `hits` es protegida con un **mutex** para evitar condiciones de carrera cuando varios hilos modifican esta variable al mismo tiempo.

El programa utiliza:
- **pthread** para la concurrencia.
- **Mutex** para sincronización entre hilos.
- **drand48_r()** para generar números aleatorios de manera segura en múltiples hilos.

Este enfoque divide la carga de trabajo entre los hilos, permitiendo que el cálculo sea más rápido en sistemas con múltiples núcleos.