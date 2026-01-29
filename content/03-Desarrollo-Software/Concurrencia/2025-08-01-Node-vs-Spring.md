---
title: "Java (Spring) vs JavaScript (Node.js)"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
---
# Java (Spring) vs JavaScript (Node.js)


> **Relacionado**: [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Malware/Mutex-nombrados-como-IOC-en-ciberseguridad|Mutex nombrados como IOC en ciberseguridad]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Monitores|Monitores]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Semaforos|Semaforos]].

Estaba leyendo una publicación en LinkedIn donde se comparaban ambas tecnologías. El autor describía Java como un lenguaje de backend sólido, aunque con una curva de aprendizaje más elevada, mientras que JavaScript con Node.js lo presentaba como una alternativa menos robusta, pero mucho más rápida para desplegar aplicaciones.

Este post me llevó a llevarme las manos a la cabeza, debido a la simplicidad con la que se establecían los criterios para decidir cuál opción era mejor, sin analizar el rendimiento en profundidad. Voy a intentar corregir este enfoque.

En lugar de comparar Java (Spring) y JavaScript (Node.js) directamente, deberíamos preguntarnos si estamos ante un problema _CPU-bound_ o _I/O-bound_. Para entender esto, primero hay que explicar qué son los hilos y cómo se gestionan las peticiones en un lenguaje como Java.

## Java y Spring: CPU-bound

Un **hilo** es un proceso ligero que comparte con el proceso principal (y otros hilos) la memoria dinámica, las variables globales y los descriptores de archivo. Sin embargo, cada hilo tiene su propio _stack_ de ejecución.

En Java con Spring, cuando se hace una petición HTTP, esta es gestionada por un _pool_ de hilos. Es decir, un conjunto de hilos reutilizables se encarga de atender las solicitudes. Cada petición es asignada a un hilo diferente de forma paralela. El hilo principal permanece en escucha y delega en los hilos del pool la gestión de cada llamada.

Este enfoque tiene una limitación: la CPU. Los hilos compiten entre sí por el uso del procesador (_CPU-bound_), lo que produce intercambios de contexto para dar la ilusión de ejecución simultánea. Este cambio de contexto no es instantáneo, ya que implica guardar y restaurar registros de CPU, y aunque el _heap_ y la sección global son compartidos, el _stack_ no lo es.

Cuando hay muchos hilos en ejecución, se puede degradar el rendimiento y llegar incluso a un _deadlock_ (abrazo mortal), donde el sistema deja de responder. A pesar de esto, Java es más eficiente que Node en tareas que requieren gran uso de CPU, como el tratamiento o la codificación de vídeo, ya que puede dividir el trabajo en múltiples hilos.

## Node.js: I/O-bound

JavaScript ejecutándose en Node.js toma un enfoque diferente: está orientado a escenarios _I/O-bound_, donde el cuello de botella no está en la CPU, sino en las operaciones de entrada/salida (como acceder a una base de datos o al sistema de archivos).

Node.js utiliza un **único hilo principal** con un modelo basado en el **event loop**, que permite manejar múltiples peticiones concurrentes sin necesidad de múltiples hilos. Aunque el código se ejecuta en un solo hilo, las tareas bloqueantes se derivan a hilos auxiliares gestionados por las APIs nativas de C++ (Node está escrito en C++).

El modelo de ejecución incluye:

- El código que escribimos (JavaScript).
    
- El _call stack_ (pila de ejecución).
    
- Las APIs de C++ internas de Node.js.
    
- El _event loop_.
    
- La _task queue_ (cola de tareas).
    

Cuando se ejecuta nuestro código, este se carga en el _call stack_. Si una función invoca una operación bloqueante (por ejemplo, acceder a una base de datos), esta se delega a un hilo separado mediante las APIs de C++, permitiendo que el _call stack_ siga ejecutando otras tareas.

Una vez que la operación bloqueante finaliza, se encola un _callback_ en la _task queue_. Si el _call stack_ está vacío, el _event loop_ lo inserta y continúa la ejecución.

Este enfoque minimiza los cambios de contexto, ya que el hilo principal nunca se bloquea. Es ideal para aplicaciones web donde la mayoría de las tareas son E/S (lectura de ficheros, consultas a base de datos, etc.).

## Comparativa final

- **Java/Spring (multihilo)** es óptimo para tareas intensivas en CPU, pero requiere más recursos y una buena gestión de hilos para evitar cuellos de botella.
    
- **Node.js (event loop)** es ideal para servicios web que manejan muchas peticiones concurrentes con operaciones de entrada/salida, utilizando un modelo asincrónico muy eficiente con bajo consumo de CPU.
    

En lugar de elegir una tecnología por "rapidez de despliegue" o "curva de aprendizaje", debemos analizar el perfil de carga de nuestra aplicación: ¿consume más CPU o más E/S?