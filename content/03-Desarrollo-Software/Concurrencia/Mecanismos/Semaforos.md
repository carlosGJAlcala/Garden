---
title: "Semáforos"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
  - mecanismos
---
# Semáforos

> **Relacionado**: Ver [[Monitores]] para alternativa de alto nivel. [[Regiones-Criticas-y-RCC|Regiones Críticas]]. [[03-Desarrollo-Software/Concurrencia/CONCEPTOS-SOBRE-PROGRAMACION-CONCURRENTE|Concurrencia]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Condiciones-de-Carrera|Condiciones de carrera]].

Los **semáforos** son un **Tipo Abstracto de Datos (TAD)** introducido por Edsger W. Dijkstra como mecanismo de **sincronización y exclusión mutua** en sistemas concurrentes.  
Permiten controlar el acceso de múltiples hilos o procesos a recursos compartidos, garantizando un uso ordenado y evitando condiciones de carrera.

---

## 1. Concepto básico

Un semáforo es esencialmente:
- Un **contador** que indica cuántos permisos hay disponibles para acceder a un recurso.
- Una **cola de espera** para los procesos/hilos que no pueden acceder de inmediato.

---

## 2. Operaciones fundamentales

Dijkstra definió dos operaciones atómicas:

### `wait(s)` o `P(s)` (*proberen* = probar)
- Si el contador del semáforo `s` es mayor que 0:
  - Decrementa el contador en 1.
  - El hilo puede continuar.
- Si es 0:
  - El hilo se **bloquea** y se añade a la cola de espera.

Pseudocódigo:
```text
PROCEDURE wait(s: SEMAPHORE);
BEGIN (* Operación Atómica *)
    IF (s.contador > 0) THEN
        s.contador := s.contador - 1;
    ELSE
        suspende_en(s.cola);
END;
````

---

### `signal(s)` o `V(s)` (_verhogen_ = incrementar)

- Si hay hilos bloqueados en la cola:
    
    - Se despierta a uno de ellos.
        
- Si no hay hilos bloqueados:
    
    - Incrementa el contador en 1.
        

Pseudocódigo:

```text
PROCEDURE signal(s: SEMAPHORE);
BEGIN (* Operación Atómica *)
    IF vacia(s.cola) THEN
        s.contador := s.contador + 1;
    ELSE
        activar_desde(s.cola);
END;
```

---

## 3. Propiedades e invariantes

- **Atomicidad**: `wait` y `signal` son indivisibles.
    
- **Invariantes**:
    
    S≥0S \geq 0 S=S0+#signal−#waitS = S_0 + \#signal - \#wait
    
    Donde:
    
    - SS = valor actual del contador.
        
    - S0S_0 = valor inicial.
        
    - #signal\#signal = número de operaciones `signal` realizadas.
        
    - #wait\#wait = número de operaciones `wait` realizadas.
        

---

## 4. Tipos de semáforos

- **Binarios**: El contador solo puede ser 0 o 1 (equivalentes a un **mutex**).
    
- **De conteo**: El contador puede ser un valor entero mayor o igual a 0.
    

---

## 5. Usos de los semáforos

1. **Exclusión mutua**  
    Controlar el acceso a zonas críticas (un semáforo binario inicializado a 1).
    
2. **Sincronización**  
    Asegurar que un hilo espere a que otro complete una tarea (semaforo inicializado a 0).
    
3. **Comunicación sincronizada**  
    Coordinar productores y consumidores.
    

---

## 6. Implementación en Java

Java proporciona la clase `Semaphore` en `java.util.concurrent`.

### Constructores:

```java
Semaphore(int permits)               // No justo
Semaphore(int permits, boolean fair) // Justo (FIFO)
```

- **Justo** (`fair = true`): otorga permisos en orden FIFO.
    
- **No justo**: más rápido, pero no garantiza orden.
    

### Operaciones principales:

- `acquire()` / `acquire(n)`: intenta obtener permisos, bloqueando si no hay disponibles.
    
- `release()` / `release(n)`: libera permisos, potencialmente desbloqueando hilos.
    
- `tryAcquire()`: intenta adquirir permisos sin bloquear.
    

---

### Ejemplo en Java – Exclusión mutua

```java
import java.util.concurrent.Semaphore;

public class Secuencia {
    private int valor = 0;
    private Semaphore sem = new Semaphore(1);

    public int getSiguiente() {
        try {
            sem.acquire();
            valor++;
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        } finally {
            sem.release();
        }
        return valor;
    }
}
```

---

### Ejemplo – Productor/Consumidor con semáforos

```java
import java.util.concurrent.Semaphore;

class Buffer {
    private Object[] buf;
    private int in = 0, out = 0, max;
    private Semaphore lleno;
    private Semaphore vacio = new Semaphore(0);
    private Semaphore em = new Semaphore(1); // Exclusión mutua

    public Buffer(int max) {
        this.max = max;
        buf = new Object[max];
        lleno = new Semaphore(max);
    }

    public void insertar(Object obj) throws InterruptedException {
        lleno.acquire();
        em.acquire();
        buf[in] = obj;
        in = (in + 1) % max;
        em.release();
        vacio.release();
    }

    public Object extraer() throws InterruptedException {
        vacio.acquire();
        em.acquire();
        Object obj = buf[out];
        buf[out] = null;
        out = (out + 1) % max;
        em.release();
        lleno.release();
        return obj;
    }
}
```

---

## 7. Diferencia Semáforo vs Lock

- **Semáforo**: Un hilo bloqueado puede ser liberado por otro.
    
- **Lock**: Solo el hilo que adquirió el lock puede liberarlo.
    

---

## 8. Ventajas y limitaciones

**Ventajas**:

- Muy versátiles: sirven para exclusión mutua y sincronización.
    
- Permiten control de recursos con múltiples permisos.
    

**Limitaciones**:

- Más complejos que `synchronized` o `Lock` para casos simples.
    
- Mal uso puede llevar a interbloqueos o inanición.
    

---


