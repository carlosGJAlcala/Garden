---
title: "Timer"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
---
Perfecto, vamos a ampliar la explicación de **Timer** que aparece en el documento, para que quede mucho más detallada y con ejemplos prácticos, porque en el texto original solo se menciona como ejemplo de tecnología que crea hilos de forma implícita.

---

## **Timer en Java y su relación con la concurrencia**


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Malware/Mutex-nombrados-como-IOC-en-ciberseguridad|Mutex nombrados como IOC en ciberseguridad]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Monitores|Monitores]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Semaforos|Semaforos]]. [[05-Profesional/Cursos/Process-Mapping/2025-09-02-Gestion-por-procesos-y-BPMN|2025 09 02 Gestion por procesos y BPMN]].

En el contexto de **4.1.4 Los hilos están por todas partes**, el **`java.util.Timer`** es un mecanismo integrado en Java para programar la ejecución diferida o periódica de tareas. Aunque su uso es sencillo, es importante entender que internamente **utiliza hilos** y que, por tanto, puede introducir problemas de concurrencia si no se diseña correctamente.

---

### **Funcionamiento básico**

Un objeto `Timer` mantiene internamente **un único hilo en segundo plano** (background thread) que se encarga de ejecutar las tareas programadas (`TimerTask`) en los momentos establecidos.

- Si se programa una tarea para ejecutarse una vez, el hilo del `Timer` la ejecuta en el momento indicado.
    
- Si se programa una tarea periódica, el hilo se encarga de reprogramarla automáticamente según el intervalo definido.
    

Ejemplo básico:

```java
import java.util.Timer;
import java.util.TimerTask;

public class EjemploTimer {
    public static void main(String[] args) {
        Timer timer = new Timer();

        // Tarea que se ejecuta después de 2 segundos
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println("Tarea ejecutada en: " + Thread.currentThread().getName());
            }
        }, 2000);
    }
}
```

Salida esperada:

```
Tarea ejecutada en: Timer-0
```

Aquí, `Timer-0` es el hilo interno que el `Timer` ha creado para ejecutar la tarea.

---

### **Implicaciones de concurrencia**

1. **Un único hilo para todas las tareas**  
    El `Timer` usa un solo hilo por instancia, por lo que si una tarea tarda demasiado en completarse, retrasará la ejecución de las siguientes.  
    Esto significa que **no hay paralelismo real** entre tareas dentro del mismo `Timer`.
    
2. **Sin manejo nativo de excepciones no controladas**  
    Si una `TimerTask` lanza una excepción en tiempo de ejecución y no la captura, el hilo del `Timer` se detiene y **ninguna otra tarea se ejecutará**.  
    Por ejemplo:
    
    ```java
    timer.schedule(new TimerTask() {
        @Override
        public void run() {
            throw new RuntimeException("Error crítico");
        }
    }, 1000);
    ```
    
    Después de este error, el `Timer` dejará de funcionar.
    
3. **Thread-safety**  
    Si las tareas (`TimerTask`) acceden a datos compartidos, es responsabilidad del programador **sincronizar el acceso** usando `synchronized`, `Lock`, variables atómicas o estructuras concurrentes.
    

---

### **Alternativas modernas**

A partir de Java 5, se recomienda usar **`ScheduledExecutorService`** (parte de `java.util.concurrent`) en lugar de `Timer`, ya que:

- Permite múltiples hilos de ejecución para las tareas.
    
- Tolera excepciones en una tarea sin detener la ejecución de las demás.
    
- Ofrece una API más flexible para programar tareas repetitivas.
    

Ejemplo equivalente con `ScheduledExecutorService`:

```java
import java.util.concurrent.*;

public class EjemploScheduler {
    public static void main(String[] args) {
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);

        scheduler.schedule(() -> {
            System.out.println("Tarea ejecutada en: " + Thread.currentThread().getName());
        }, 2, TimeUnit.SECONDS);

        scheduler.shutdown();
    }
}
```

---

### **Buenas prácticas al usar Timer**

- Usar **una instancia de `Timer` por grupo de tareas relacionadas** para evitar interferencias entre tareas de naturaleza diferente.
    
- Manejar todas las excepciones dentro de la `TimerTask` para evitar que el hilo principal del `Timer` muera.
    
- Cancelar el `Timer` con `timer.cancel()` cuando ya no sea necesario, para liberar recursos.
    
- Considerar **`ScheduledExecutorService`** para aplicaciones críticas o con alta concurrencia.
    

---

Si quieres, puedo hacer lo mismo con **RMI**, que es otra de las tecnologías mencionadas junto a Timer en esa sección y que también tiene implicaciones importantes en programación concurrente. ¿Quieres que continúe con RMI?