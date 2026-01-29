---
title: "Liveness"
date: 2025-01-01
tags:
  - desarrollo-software
---

## **4.10 Evitando problemas de bloqueo indefinido (Liveness)**


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

En el ámbito de la programación concurrente, **liveness** hace referencia a la capacidad de un sistema o conjunto de hilos para seguir progresando en la ejecución de sus tareas, evitando quedarse en un estado de espera indefinida. Un sistema con problemas de liveness puede “colgarse” o quedarse bloqueado sin completar su trabajo, a pesar de que no haya fallos de hardware o software evidentes.

Cuando hablamos de _liveness_ no solo nos referimos a **deadlocks** (interbloqueos), sino también a otros problemas como **livelocks** (bloqueos vivos, donde los hilos están activos pero sin avanzar) y **starvation** (inanición, cuando uno o más hilos nunca obtienen acceso a los recursos necesarios). Aunque el apartado original se centra principalmente en el deadlock, en ingeniería de software se considera buena práctica contemplar los tres.

### **4.10.1 Interbloqueos (Deadlocks)**

El interbloqueo es la forma más grave de pérdida de liveness. Se produce cuando un conjunto de hilos queda esperando indefinidamente a que otros liberen recursos que nunca serán liberados. Es una condición en la que cada hilo del grupo está bloqueado esperando que otro hilo libere un recurso, generando una dependencia circular que impide cualquier progreso.

#### **Ejemplo clásico: La cena de los filósofos**

Este ejemplo, planteado por Edsger Dijkstra, ilustra de forma didáctica el problema:

- Cinco filósofos se sientan en una mesa redonda.
    
- Cada filósofo alterna entre pensar y comer.
    
- Para comer, cada filósofo necesita dos tenedores (o palillos), el de su izquierda y el de su derecha.
    
- Todos intentan coger primero el tenedor de su derecha y luego el de su izquierda.
    
- Si todos cogen el primer tenedor al mismo tiempo, ninguno podrá coger el segundo. Todos quedarán esperando indefinidamente.
    

Este escenario provoca un **deadlock** perfecto: ninguno de los hilos (filósofos) podrá avanzar porque todos esperan un recurso que otro hilo mantiene.

En términos de Java, este patrón se puede reproducir fácilmente con código que adquiera bloqueos (synchronized) sobre objetos en distinto orden, como en el ejemplo `LeftRightDeadlock`:

```java
public class LeftRightDeadlock {
    private final Object left = new Object();
    private final Object right = new Object();

    public void leftRight() {
        synchronized (left) {
            synchronized (right) {
                doSomething();
            }
        }
    }

    public void rightLeft() {
        synchronized (right) {
            synchronized (left) {
                doSomethingElse();
            }
        }
    }
}
```

En este caso, si un hilo ejecuta `leftRight()` y otro `rightLeft()`, se puede formar una espera circular: el primero tiene el bloqueo sobre `left` y espera `right`, mientras que el segundo tiene el bloqueo sobre `right` y espera `left`.

---

### **Estrategias para evitar el deadlock**

Existen múltiples enfoques para reducir la probabilidad o eliminar la posibilidad de un interbloqueo:

1. **Orden global de adquisición de recursos**  
    Establecer un orden fijo para adquirir bloqueos y asegurarse de que todos los hilos respeten ese orden.  
    Ejemplo: siempre bloquear primero `left` y luego `right`.
    
2. **Evitar bloqueos anidados**  
    Diseñar el código para que un hilo adquiera solo un bloqueo a la vez. Esto elimina la dependencia circular.
    
3. **Uso de temporizadores y reintentos**  
    Utilizar métodos como `tryLock()` de `java.util.concurrent.locks.Lock` con un tiempo de espera.  
    Si no se obtiene el bloqueo en un intervalo razonable, liberar los recursos adquiridos y volver a intentarlo.
    
4. **Asignación controlada de recursos (patrón del portero)**  
    Limitar el número de hilos que pueden intentar adquirir recursos simultáneamente. Por ejemplo, permitir solo `n-1` filósofos en la mesa garantiza que al menos uno pueda comer.
    
5. **Soluciones basadas en colas**  
    Poner a los hilos en una cola para cada recurso y atenderlos de manera controlada, evitando la competición directa.
    

---

### **Otros problemas de Liveness** (no incluidos explícitamente en el texto original pero relevantes)

- **Starvation (inanición)**  
    Un hilo nunca obtiene acceso a un recurso porque otros hilos monopolizan su uso o siempre tienen prioridad más alta.  
    Solución: políticas de planificación justas (_fair scheduling_), como las implementaciones de `ReentrantLock` con parámetro `fair=true`.
    
- **Livelock (bloqueo vivo)**  
    Ocurre cuando los hilos están activos pero se están cediendo recursos entre sí continuamente sin avanzar en el trabajo real.  
    Ejemplo: dos hilos detectan una posible colisión y ambos retroceden y vuelven a intentarlo al mismo tiempo, repitiendo indefinidamente.
    

---

En resumen, **garantizar el liveness** en aplicaciones concurrentes implica más que prevenir deadlocks: requiere diseñar políticas de bloqueo, adquisición de recursos y planificación de tareas que aseguren que todos los hilos tengan la oportunidad de progresar y que el sistema no quede atrapado en estados de espera indefinida.

---

Si quieres, puedo seguir y **expandir el apartado 4.11 "Rendimiento y escalabilidad"** con el mismo estilo técnico y detallado para que el capítulo quede completo y cohesionado. ¿Quieres que lo haga?