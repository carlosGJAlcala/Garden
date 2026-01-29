---
title: "Rmi"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
---
Perfecto, vamos a ampliar **RMI (Remote Method Invocation)** en el contexto del documento, porque aunque allí solo se menciona brevemente como tecnología que usa hilos, en realidad su funcionamiento interno depende fuertemente de la concurrencia en Java.

---

## **RMI y la concurrencia en Java**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/SAP_PI/STUB|STUB]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

**Java RMI** (Remote Method Invocation) es una tecnología que permite a una aplicación Java **invocar métodos de objetos que residen en otra JVM** (Java Virtual Machine), incluso si está en una máquina diferente y conectada a través de una red.

Desde el punto de vista de la **programación concurrente**, RMI es un ejemplo claro de cómo una tecnología puede **crear y gestionar hilos automáticamente en segundo plano** para atender múltiples clientes de forma simultánea, sin que el programador tenga que instanciarlos explícitamente.

---

### **Cómo RMI utiliza hilos**

Cuando un objeto remoto está registrado en el **RMI Registry** y un cliente realiza una llamada a uno de sus métodos:

1. El **servidor RMI** recibe la solicitud de forma asíncrona.
    
2. El _runtime_ de RMI **crea o asigna un hilo** para atender la petición.
    
3. Ese hilo ejecuta el método solicitado en el objeto remoto.
    
4. El resultado o excepción se envía de vuelta al cliente por la red.
    
5. El hilo queda disponible para atender otra petición.
    

Esto significa que un mismo objeto remoto puede ser invocado por múltiples clientes **al mismo tiempo** en diferentes hilos, lo que introduce el problema del **acceso concurrente a datos compartidos** dentro del objeto.

---

Consumir un servicio **RMI** en Java implica **conectarse al objeto remoto registrado en el servidor** y llamar a sus métodos como si fuera un objeto local.  
La gracia de RMI es que **oculta toda la complejidad de la comunicación por red** y convierte la llamada en algo transparente para el programador.

Te lo explico paso a paso con un ejemplo completo de **servidor + cliente**.

---

## **1. Definir la interfaz remota**

Esta interfaz define los métodos que estarán disponibles de forma remota.  
Debe **extender `java.rmi.Remote`** y **todos los métodos deben lanzar `RemoteException`**.

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface HolaMundo extends Remote {
    String saludar(String nombre) throws RemoteException;
}
```

---

## **2. Implementar el objeto remoto**

La implementación debe **extender `UnicastRemoteObject`** y proporcionar el comportamiento de los métodos.

```java
import java.rmi.server.UnicastRemoteObject;
import java.rmi.RemoteException;

public class HolaMundoImpl extends UnicastRemoteObject implements HolaMundo {

    public HolaMundoImpl() throws RemoteException {
        super();
    }

    @Override
    public String saludar(String nombre) throws RemoteException {
        return "Hola, " + nombre + " desde el servidor RMI";
    }
}
```

---

## **3. Crear el servidor RMI**

Este código **registra el objeto remoto en el RMI Registry** para que los clientes puedan localizarlo.

```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class ServidorRMI {
    public static void main(String[] args) {
        try {
            HolaMundo objeto = new HolaMundoImpl();

            // Crear el registro RMI en el puerto 1099
            Registry registry = LocateRegistry.createRegistry(1099);

            // Registrar el objeto remoto con un nombre
            registry.rebind("HolaMundoService", objeto);

            System.out.println("Servidor RMI listo y esperando conexiones...");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## **4. Consumir el RMI desde un cliente**

En el cliente, se localiza el objeto remoto y se llama a sus métodos **como si fuera un objeto local**, pero en realidad se ejecutan en el servidor.

```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class ClienteRMI {
    public static void main(String[] args) {
        try {
            // Conectarse al RMI Registry del servidor (localhost y puerto 1099)
            Registry registry = LocateRegistry.getRegistry("localhost", 1099);

            // Buscar el objeto remoto por su nombre
            HolaMundo stub = (HolaMundo) registry.lookup("HolaMundoService");

            // Invocar un método remoto
            String respuesta = stub.saludar("Carlos");
            System.out.println("Respuesta del servidor: " + respuesta);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## **5. Ejecución**

1. Compilar todas las clases (`javac *.java`).
    
2. Iniciar el servidor RMI ejecutando `ServidorRMI`.
    
3. Ejecutar el cliente (`ClienteRMI`).
    
4. Ver la comunicación cliente-servidor a través de RMI.
    

---

## **Notas importantes**

- Si cliente y servidor están en máquinas distintas, en `LocateRegistry.getRegistry()` se debe poner la IP o el nombre del servidor.
    
- En versiones antiguas de Java (< 5) había que usar `rmic` para generar _stubs_, pero hoy la generación es dinámica y no hace falta.
    
- RMI funciona sobre TCP, por lo que hay que asegurarse de que el puerto (por defecto 1099) esté abierto en el firewall.
    

---


---

### **Características relevantes para la concurrencia**

- **Un objeto remoto es compartido**: Todas las invocaciones concurrentes de distintos clientes se dirigen al mismo objeto en memoria, a menos que se haya diseñado para crear una nueva instancia por cliente.
    
- **Los métodos deben ser thread-safe**: El desarrollador debe garantizar la consistencia de datos compartidos.
    
- **El runtime de RMI usa un pool de hilos**: Esto permite atender múltiples peticiones simultáneamente.
    
- **No hay sincronización automática**: RMI no bloquea el acceso concurrente; esto es responsabilidad del programador.
    

---

### **Buenas prácticas en RMI con concurrencia**

1. **Usar sincronización explícita** en los métodos que modifican estado compartido (`synchronized`, `ReentrantLock`, etc.).
    
2. **Diseñar objetos remotos inmutables** cuando sea posible, eliminando la necesidad de sincronización.
    
3. **Evitar operaciones bloqueantes largas** en métodos remotos, ya que cada hilo ocupado en una llamada larga reduce la capacidad de respuesta global.
    
4. **Considerar el uso de `ExecutorService`** dentro de la implementación para descargar tareas pesadas a un pool separado, evitando saturar los hilos internos de RMI.
    

---

### **Ventajas de RMI en entornos concurrentes**

- Permite **paralelismo natural** al atender múltiples clientes en paralelo.
    
- Se integra bien con otras APIs concurrentes de Java (`ExecutorService`, `Future`, `Callable`).
    
- Simplifica la comunicación remota ocultando los detalles de la red, centrándose en la lógica de negocio.
    
Cuando un cliente llama a un método de un objeto **RMI**, **no se envía un texto plano ni un binario "crudo"**, sino que **la JVM convierte automáticamente los argumentos y el resultado en un formato binario siguiendo el protocolo Java RMI (JRMP)**.

Te explico el flujo interno paso a paso:

---

## **1. Qué protocolo usa**

- El transporte por defecto de RMI es **JRMP** (Java Remote Method Protocol).
    
- JRMP funciona **sobre TCP**.
    
- JRMP **no usa JSON, XML ni texto plano**; usa un **formato binario propietario de Java** que incluye metadatos de clases, tipos y valores.
    
- También puede configurarse para usar **IIOP** (para interoperar con CORBA), pero por defecto es JRMP.
    

---

## **2. Cómo se codifican los datos**

- Java usa un mecanismo llamado **Object Serialization** para convertir los argumentos y resultados en un flujo de bytes.
    
- Este flujo binario contiene:
    
    1. **Metadatos de clase** (nombre, serialVersionUID, etc.).
        
    2. **Estructura del objeto** (campos y tipos).
        
    3. **Valores de los campos**.
        
- Todo se hace usando **Java Object Serialization Stream Protocol**, que es **binario** y con una codificación propia, no legible como texto.
    

---

## **3. Ejemplo conceptual**

Supongamos que llamamos:

```java
String respuesta = stub.saludar("Carlos");
```

Internamente ocurre esto:

1. El _stub_ (objeto proxy en el cliente) **serializa** el String `"Carlos"` en un flujo binario.
    
2. Ese flujo se envía vía TCP al servidor RMI.
    
3. El _skeleton_ del servidor **deserializa** el flujo binario, obtiene `"Carlos"` como `String` y llama al método real `saludar()`.
    
4. El valor de retorno (`String`) se **serializa** de nuevo a binario.
    
5. El cliente recibe el flujo y lo **deserializa** para obtener el `String respuesta`.
    

---

## **4. Codificación interna**

- Aunque un `String` en Java internamente usa **UTF-16** en memoria, cuando se serializa se transforma en un flujo binario que guarda los caracteres usando una variante de **modified UTF-8** definida por el protocolo de serialización de Java.
    
- Los tipos primitivos (`int`, `boolean`, `double`, etc.) se codifican en su representación binaria directa (big-endian).
    
- Objetos complejos se recorren recursivamente y se codifican según el mismo formato binario.
    

---

## **5. Ejemplo real de serialización**

Si serializamos un String `"Hola"` en Java:

```java
import java.io.*;

public class Test {
    public static void main(String[] args) throws Exception {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(baos);
        oos.writeObject("Hola");
        oos.close();

        byte[] bytes = baos.toByteArray();
        for (byte b : bytes) {
            System.out.printf("%02X ", b);
        }
    }
}
```

Salida (ejemplo):

```
AC ED 00 05 74 00 04 48 6F 6C 61
```

Aquí:

- `AC ED 00 05` → cabecera de stream de objetos de Java.
    
- `74` → indica tipo String.
    
- `00 04` → longitud (4 caracteres).
    
- `48 6F 6C 61` → "Hola" en UTF-8 modificado.
    

Esto mismo es lo que pasa dentro de un RMI, pero empaquetado junto con metadatos de la invocación.

---

## **6. Resumen**

- **Se envía un flujo binario** siguiendo el protocolo de serialización de Java.
    
- **Está codificado** usando **Java Object Serialization** (no es JSON, XML, ni texto plano).
    
- Los Strings usan **UTF-8 modificado** dentro de esa codificación.
    
- Todo esto se transporta sobre **TCP mediante JRMP**.
    

---

Si quieres, puedo prepararte **un diagrama de red** donde se vea cómo el RMI convierte parámetros en binario, los envía por TCP, y los vuelve a convertir en objetos en el otro extremo.  
¿Quieres que lo haga?