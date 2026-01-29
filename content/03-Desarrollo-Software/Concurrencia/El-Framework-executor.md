---
title: "El Framework Executor"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
---
Perfecto, vamos a desarrollar **4.6.2 El Framework Executor** con un nivel técnico más profundo, ampliando los conceptos del documento y añadiendo contexto, ventajas, problemas y ejemplos de uso reales.

---

## **4.6.2 El Framework Executor**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Malware/Mutex-nombrados-como-IOC-en-ciberseguridad|Mutex nombrados como IOC en ciberseguridad]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Monitores|Monitores]].

En Java, la programación concurrente tradicionalmente se ha basado en la creación y gestión manual de hilos mediante la clase `Thread` o la interfaz `Runnable`. Sin embargo, este enfoque presenta varios problemas cuando el número de tareas crece o cuando se requieren políticas avanzadas de ejecución y gestión de recursos.

El **Framework Executor**, introducido en Java 5 como parte del paquete `java.util.concurrent`, abstrae el manejo de hilos y proporciona una infraestructura robusta para **ejecutar tareas de forma asíncrona**, gestionar su ciclo de vida y aplicar políticas de ejecución específicas.

En este modelo:

- **La tarea** se encapsula en un objeto (`Runnable` o `Callable`).
    
- **El executor** decide cuándo y cómo se ejecutará la tarea.
    
- El desarrollador ya no necesita preocuparse por la creación, sincronización o destrucción manual de hilos.
    

---

### **Conceptos clave**

- **Separación de responsabilidades**: La lógica de negocio se concentra en la tarea (`Runnable`/`Callable`), mientras que la gestión de recursos queda en manos del executor.
    
- **Reutilización de hilos**: En lugar de crear un hilo por tarea, se usan _thread pools_ que permiten reciclar hilos ya existentes, reduciendo la sobrecarga de creación y destrucción.
    
- **Políticas de ejecución configurables**: Se puede decidir cómo se asignan los hilos, cuántos hilos usar, cómo manejar tareas pendientes y cómo actuar cuando no haya recursos disponibles.
    

---

### **Interfaz base**

El núcleo del framework es la interfaz:

```java
public interface Executor {
    void execute(Runnable command);
}
```

Esta interfaz define un único método que acepta una tarea `Runnable`. La implementación concreta decidirá cómo y cuándo se ejecuta.

---

### **ExecutorService**

La interfaz `ExecutorService` extiende `Executor` y añade:

- Métodos para **controlar el ciclo de vida** del executor (`shutdown()`, `shutdownNow()`).
    
- Métodos para **gestionar tareas con retorno de resultados** (`submit()`, `invokeAll()`, `invokeAny()`).
    
- Posibilidad de trabajar con **`Future`** para consultar el estado de ejecución o cancelar tareas.
    

Ejemplo básico:

```java
ExecutorService executor = Executors.newFixedThreadPool(4);

for (int i = 0; i < 10; i++) {
    executor.submit(() -> {
        System.out.println(Thread.currentThread().getName() + " ejecutando tarea");
    });
}

executor.shutdown();
```

---

### **Políticas de ejecución**

La política de ejecución define cómo se manejan las tareas:

- **Número máximo de hilos concurrentes**.
    
- **Orden de ejecución** (FIFO, prioridad, etc.).
    
- **Comportamiento ante saturación** (rechazo, ejecución en el hilo llamador, descarte).
    

Estas políticas se implementan principalmente a través de `ThreadPoolExecutor`, que permite configurar:

- `corePoolSize`: número de hilos básicos que siempre permanecen activos.
    
- `maximumPoolSize`: límite superior de hilos que puede crear.
    
- `keepAliveTime`: tiempo que un hilo inactivo permanece vivo antes de ser destruido.
    
- `workQueue`: cola donde se almacenan tareas pendientes.
    
- `RejectedExecutionHandler`: política a aplicar cuando no se puede aceptar una nueva tarea.
    

---

### **Ventajas frente al modelo Thread manual**

1. **Control centralizado** del ciclo de vida de los hilos.
    
2. **Mejora del rendimiento** gracias a la reutilización de hilos.
    
3. **Mayor escalabilidad** en entornos de alta concurrencia.
    
4. **Facilidad de mantenimiento**: la lógica de ejecución está desacoplada del código de negocio.
    
5. **Compatibilidad con `Callable` y `Future`** para obtener resultados de las tareas.
    

---

### **Ejemplo práctico: Servidor concurrente**

Un servidor que atiende múltiples conexiones simultáneamente podría gestionarse así:

```java
ExecutorService pool = Executors.newFixedThreadPool(50);

while (true) {
    Socket clientSocket = serverSocket.accept();
    pool.execute(() -> atenderCliente(clientSocket));
}
```

En este escenario:

- El _thread pool_ limita el número de hilos simultáneos, evitando la saturación del sistema.
    
- Cada conexión es atendida por un hilo del pool.
    
- El servidor sigue aceptando nuevas conexiones sin bloquearse por tareas largas.
    

---

### **Relación con otras utilidades de `java.util.concurrent`**

El Framework Executor se integra de forma natural con:

- **`ScheduledExecutorService`** para tareas periódicas o retrasadas.
    
- **`CompletionService`** para procesar resultados a medida que están disponibles.
    
- **`ForkJoinPool`** para tareas que pueden dividirse en subtareas recursivamente.
    

---

### **Buenas prácticas**

- Elegir el tipo de executor en función del patrón de carga:
    
    - `newFixedThreadPool(n)` para carga constante.
        
    - `newCachedThreadPool()` para tareas cortas y número variable.
        
    - `newSingleThreadExecutor()` para garantizar orden de ejecución.
        
- Cerrar el executor con `shutdown()` al terminar, para evitar fugas de recursos.
    
- Manejar adecuadamente las excepciones dentro de las tareas para que no afecten al resto de hilos.
    
- No abusar de `newCachedThreadPool()` en sistemas con recursos limitados, ya que puede crear demasiados hilos.
    

---

Si quieres, puedo continuar y **ampliar el apartado “Threads pools”** que está directamente ligado a este, ya que es el núcleo operativo del Executor en entornos concurrentes.  
¿Quieres que lo desarrolle a continuación?