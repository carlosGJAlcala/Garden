---
title: "Servlets"
date: 2026-01-26
tags:
  - desarrollo-software
  - concurrencia
---
Vale, vamos a ampliar la parte de **servlets** que aparece en el documento, porque aunque en el texto original solo se menciona como ejemplo de tecnología que usa hilos, en realidad hay bastante profundidad detrás en cómo interactúan los servlets con la concurrencia en Java.

---

## **Servlets y concurrencia en Java**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Condiciones-de-Carrera|Condiciones de Carrera]]. [[05-Profesional/Cursos/Process-Mapping/2025-09-02-Gestion-por-procesos-y-BPMN|2025 09 02 Gestion por procesos y BPMN]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

En el contexto de programación concurrente de memoria común en Java, **los servlets son un ejemplo real y cotidiano de aplicaciones que se ejecutan en un entorno multihilo** sin que el desarrollador tenga que gestionar explícitamente la creación o destrucción de hilos.

Un **servlet** es un componente Java que se ejecuta en un servidor web o de aplicaciones (como Apache Tomcat, Jetty, JBoss/WildFly o GlassFish) y que **procesa peticiones HTTP** provenientes de clientes (normalmente navegadores web). El contenedor de servlets gestiona todo el ciclo de vida del servlet, desde su carga hasta su destrucción.

---

### **Concurrencia en servlets**

Por diseño, un contenedor de servlets:

- Crea **una única instancia** de cada servlet definido.
    
- Usa **un hilo diferente** para atender cada petición entrante al mismo servlet.
    
- Reutiliza la misma instancia para múltiples hilos concurrentes.
    

Esto significa que **todas las variables de instancia (atributos no estáticos)** de un servlet son **compartidas** por todos los hilos que lo atienden simultáneamente.

Ejemplo simplificado:

```java
@WebServlet("/contador")
public class ContadorServlet extends HttpServlet {
    private int contador = 0; // Variable compartida

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws IOException {
        contador++; // Posible condición de carrera
        resp.getWriter().println("Visitas: " + contador);
    }
}
```

En este código, si varios usuarios hacen peticiones casi al mismo tiempo, el incremento de `contador` no está protegido. Esto puede provocar resultados incorrectos debido a **condiciones de carrera**.

---

### **Implicaciones de la programación concurrente**

1. **No usar variables de instancia mutables sin protección**  
    Si se necesita un estado compartido, debe protegerse con sincronización (`synchronized`), `AtomicInteger`, `volatile` o utilizando estructuras de datos concurrentes (`ConcurrentHashMap`, etc.).
    
2. **Preferir variables locales a variables de instancia**  
    Las variables locales dentro de `doGet()` o `doPost()` son seguras por naturaleza porque cada hilo obtiene su propia copia en la pila de ejecución.
    
3. **Evitar estados globales**  
    Las variables `static` también son compartidas entre hilos y entre instancias de servlets, lo que incrementa el riesgo de inconsistencias.
    
4. **Sincronización explícita**  
    En caso de tener que modificar datos compartidos:
    
    ```java
    private final AtomicInteger contador = new AtomicInteger();
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws IOException {
        int valor = contador.incrementAndGet();
        resp.getWriter().println("Visitas: " + valor);
    }
    ```
    

---

### **Cómo el contenedor de servlets gestiona los hilos**

- El contenedor mantiene un **pool de hilos** (muy parecido a un `ThreadPoolExecutor`).
    
- Cada nueva petición HTTP se asigna a un hilo libre del pool.
    
- Si todos los hilos están ocupados, las nuevas peticiones esperan en una cola.
    
- El programador no ve directamente los hilos, pero su código se ejecuta en ellos.
    

Esto hace que **los servlets sean un caso práctico de programación concurrente de memoria común en Java**, donde los datos compartidos residen en el heap de la JVM y son accesibles por múltiples hilos simultáneamente.

---

### **Relación con Thread-safety**

En el documento original, los servlets se citan como ejemplo de tecnología que **crea hilos automáticamente en nombre del programador**.  
Esto implica que **aunque el desarrollador no haya escrito `new Thread()`**, su código ya está expuesto a un contexto multihilo y debe ser diseñado para ser **thread-safe**.

---

### **Buenas prácticas de concurrencia en servlets**

- **Hacer los servlets inmutables** siempre que sea posible.
    
- **Delegar el manejo de estados en sistemas externos** (base de datos, cachés distribuidas, etc.).
    
- **Utilizar sincronización de bajo nivel solo cuando sea estrictamente necesario**, prefiriendo estructuras concurrentes ya probadas de `java.util.concurrent`.
    
- **No bloquear el hilo innecesariamente**, ya que cada hilo bloqueado reduce la capacidad de respuesta global del servidor.
    
- Para tareas pesadas o de larga duración, **descargar el trabajo** a otro hilo gestionado por un `ExecutorService` en lugar de bloquear el hilo que atiende la petición.
    

---

Si quieres, puedo también **integrar esta explicación dentro de la parte de “Los hilos están por todas partes” (4.1.4)** del documento, para que tu versión ampliada quede cohesionada y con ejemplos prácticos de cada tecnología que se menciona ahí.  
¿Quieres que lo haga?