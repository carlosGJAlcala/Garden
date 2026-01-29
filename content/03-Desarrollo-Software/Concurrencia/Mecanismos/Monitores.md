---
title: "Monitores"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
  - mecanismos
---
Perfecto, te preparo el apartado de **Monitores** en **formato Markdown**, ampliado, con teoría, funcionamiento en Java y ejemplos prácticos, enlazando con lo que ya vimos de RC y RCC.

---


# Monitores


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Malware/Mutex-nombrados-como-IOC-en-ciberseguridad|Mutex nombrados como IOC en ciberseguridad]]. [[03-Desarrollo-Software/Concurrencia/Mecanismos/Semaforos|Semaforos]].

Los **monitores** son un mecanismo de sincronización de alto nivel introducido por **C.A.R. Hoare** y **Per Brinch Hansen** en los años 70.  
Son una **abstracción** que encapsula:
- Variables compartidas.
- Procedimientos que las manipulan.
- Mecanismos para garantizar **exclusión mutua** y **sincronización condicional**.

En Java, **todo objeto** puede actuar como un monitor.

---

## 1. Características de un monitor

1. **Exclusión mutua automática**:
   - Solo un hilo puede ejecutar un procedimiento del monitor a la vez.
   - El resto de hilos queda bloqueado hasta que el monitor se libere.

2. **Variables de condición**:
   - Permiten suspender y reanudar hilos dentro del monitor.
   - Operaciones típicas:
     - `wait()` → libera el monitor y bloquea el hilo hasta recibir señal.
     - `notify()` → despierta un hilo bloqueado.
     - `notifyAll()` → despierta todos los hilos bloqueados.

3. **Control estructurado**:
   - Las variables compartidas solo pueden ser manipuladas desde dentro del monitor.

---

## 2. Tipos de monitores

- **Monitores de Hoare**:
  - Cuando un hilo hace `signal`, el hilo que recibe la señal entra **inmediatamente** en el monitor y el que hizo `signal` sale.
- **Monitores de Mesa** (implementación en Java):
  - Cuando un hilo hace `notify`, el hilo que recibe la señal pasa a la **cola de entrada** y solo entra cuando el monitor esté libre.

---

## 3. Monitores en Java

En Java, un monitor se implementa con:
- `synchronized` para garantizar exclusión mutua.
- `wait()`, `notify()` y `notifyAll()` para sincronización condicional.

**Reglas de uso**:
- `wait()`, `notify()` y `notifyAll()` **solo se pueden llamar** desde un contexto sincronizado.
- `wait()` libera el monitor y suspende el hilo.
- `notify()` despierta **uno** de los hilos en espera.
- `notifyAll()` despierta **todos** los hilos en espera.

---

## 4. Ejemplo – Productor–Consumidor con monitores

```java
public class Buffer {
    private Object[] buf;
    private int in = 0, out = 0, numElem = 0, max;

    public Buffer(int max) {
        this.max = max;
        buf = new Object[max];
    }

    public synchronized void insertar(Object obj) throws InterruptedException {
        while (numElem == max) {
            wait(); // Variable de condición: buffer lleno
        }
        buf[in] = obj;
        in = (in + 1) % max;
        numElem++;
        notifyAll(); // Señal para consumidores
    }

    public synchronized Object extraer() throws InterruptedException {
        while (numElem == 0) {
            wait(); // Variable de condición: buffer vacío
        }
        Object obj = buf[out];
        buf[out] = null;
        out = (out + 1) % max;
        numElem--;
        notifyAll(); // Señal para productores
        return obj;
    }
}
```

 Aquí:

- El objeto `Buffer` es el **monitor**.
    
- Los métodos `insertar` y `extraer` son **métodos monitor** (RC).
    
- `wait()` y `notifyAll()` gestionan la **sincronización condicional** (RCC).
    

---

## 5. Diferencias clave entre RC, RCC y Monitores

|Mecanismo|Exclusión mutua|Espera condicional|Encapsulación|
|---|---|---|---|
|RC||||
|RCC||||
|Monitor||| (variables y métodos dentro del monitor)|

---

## 6. Ventajas y limitaciones de monitores

**Ventajas**:

- Encapsulan datos y sincronización en una sola estructura.
    
- Eliminan errores comunes de manejo manual de semáforos.
    
- Legibles y mantenibles.
    

**Limitaciones**:

- No permiten que varios hilos ejecuten métodos distintos del monitor simultáneamente (aunque accedan a datos independientes).
    
- No son adecuados para ciertas aplicaciones de muy alto rendimiento.
    

---

## 7. Buenas prácticas en Java

- Usar `while` y no `if` antes de `wait()` para volver a verificar la condición al despertar.
    
- Usar `notifyAll()` en lugar de `notify()` si hay múltiples condiciones posibles.
    
- Encapsular todas las variables compartidas dentro del monitor.
    
- Evitar operaciones largas dentro de métodos sincronizados para reducir la espera de otros hilos.
    

---

```

---

Si quieres, puedo seguir con el **apartado de Ejemplos** y después con **Interbloqueo**, así ya tendrías todo el tema 4 completo y listo para tu apunte final.  
¿Quieres que lo continúe así?
```