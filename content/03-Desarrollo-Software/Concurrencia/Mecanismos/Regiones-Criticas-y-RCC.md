---
title: "Regiones Criticas Y Rcc"
date: 2025-01-01
tags:
  - desarrollo-software
---

# Regiones Críticas y Regiones Críticas Condicionales (RCC)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

Las **Regiones Críticas (RC)** son un mecanismo de sincronización que garantiza que solo **un hilo o proceso** pueda acceder a una sección de código donde se manipulan **variables compartidas** en un momento dado.  
Fueron propuestas por **Per Brinch Hansen** como una forma estructurada de conseguir **exclusión mutua**.

---

## 1. Concepto de Región Crítica

Una **Región Crítica** está asociada a una o más **variables compartidas**.  
Cuando un proceso/hilo entra en la RC:
- Se asegura **exclusión mutua**: solo un hilo a la vez puede acceder a la variable protegida.
- Se garantiza que la entrada en la RC se produzca en un **tiempo finito** (sin espera infinita injustificada).
- Varias RC pueden ejecutarse en paralelo si protegen **variables diferentes**.

Ejemplo en **Concurrent Pascal**:
```pascal
VAR v: SHARED INTEGER;

PROCEDURE P1;
BEGIN
    ...
    REGION v DO
        v := v + 2;
    ...
END;
````

---

## 2. Propiedades de una RC

1. **Exclusión mutua**: solo un hilo accede a la variable compartida en cada momento.
    
2. **Progreso**: si ningún hilo está en la RC, uno que quiera entrar lo hará en un tiempo finito.
    
3. **Tiempo limitado en la RC**: ningún hilo permanece indefinidamente en la región.
    

---

## 3. Regiones Críticas en Java

En Java, las RC se implementan con el **bloqueo implícito** que proporciona la palabra clave `synchronized`.

### Ejemplo 1 – Bloque sincronizado

```java
public class VarComp {
    private int v = 0;

    public void incrementar(int i) {
        synchronized (this) {
            v = v + i;
        }
    }
}
```

### Ejemplo 2 – Método sincronizado

```java
public class VarComp {
    private int v = 0;

    public synchronized void incrementar(int i) {
        v = v + i;
    }
}
```

En ambos casos:

- El **objeto** sobre el que se sincroniza actúa como **monitor implícito**.
    
- Todos los métodos/bloques `synchronized` que usan el mismo monitor forman **una única RC**.
    

---

## 4. Limitación: Espera Activa

Si se utilizan RC para **sincronización por condiciones** (ej. esperar que un buffer no esté vacío):

- El hilo podría entrar en un **bucle de espera activa** comprobando la condición continuamente.
    
- Esto **consume CPU innecesariamente**.
    

---

## 5. Regiones Críticas Condicionales (RCC)

Una **Región Crítica Condicional** es una extensión de la RC que permite a un hilo:

1. Entrar en la RC.
    
2. **Comprobar una condición**.
    
3. Si no se cumple, **salir temporalmente** y esperar.
    
4. Volver a entrar cuando otro hilo haya modificado la condición.
    

### Ventajas

- Evitan espera activa.
    
- El hilo solo se despierta cuando hay una señal relevante.
    

---

## 6. Funcionamiento de las RCC

- Dentro de la RCC, se usa una **operación de espera condicional** (`AWAIT`) para liberar la RC y bloquear el hilo hasta que la condición cambie.
    
- Cuando otro hilo modifica la condición, realiza una **señal** para despertar a los hilos bloqueados.
    

---

## 7. Implementación en Java

Java **no tiene una implementación directa** de RCC, pero se puede lograr usando:

- `wait()` → libera el monitor y bloquea el hilo.
    
- `notify()` → despierta a un hilo en espera.
    
- `notifyAll()` → despierta a todos los hilos en espera.
    

### Ejemplo – Buffer productor/consumidor con RCC

```java
public class Buffer {
    private Object[] buf;
    private int in = 0, out = 0, numElem = 0, maximo;

    public Buffer(int max) {
        this.maximo = max;
        buf = new Object[max];
    }

    public synchronized void insertar(Object obj) throws InterruptedException {
        while (numElem == maximo) {
            wait(); // Espera condicional
        }
        buf[in] = obj;
        numElem++;
        in = (in + 1) % maximo;
        notifyAll(); // Señal para consumidores
    }

    public synchronized Object extraer() throws InterruptedException {
        while (numElem == 0) {
            wait(); // Espera condicional
        }
        Object obj = buf[out];
        buf[out] = null;
        numElem--;
        out = (out + 1) % maximo;
        notifyAll(); // Señal para productores
        return obj;
    }
}
```

---

## 8. Diferencia RC vs RCC

|Característica|RC|RCC|
|---|---|---|
|Exclusión mutua|||
|Espera activa|Sí (si no se usa condición)|No (usa `wait`)|
|Despertar hilos|No aplica|Sí (`notify` / `notifyAll`)|
|Sincronización condicional|No|Sí|

---

## 9. Resumen

- **RC**: Garantiza exclusión mutua en acceso a datos compartidos.
    
- **RCC**: Añade sincronización condicional y evita espera activa.
    
- En **Java**, ambas se implementan con `synchronized`, pero las RCC requieren además `wait` y `notify`.
    

---

