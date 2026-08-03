---
title: "Sockets Java"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
---
---

## **1. Qué es un socket en Java**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

Un **socket** es un **punto de comunicación** que conecta dos procesos (pueden estar en la misma máquina o en máquinas distintas) a través de la red.  
En Java, los sockets implementan el modelo de **paso de mensajes** que vimos en la teoría, pero usando APIs de **entrada/salida de streams** o **paquetes datagrama**.

---

## **2. Tipos principales**

En Java tienes dos familias base:

|Tipo|Clase en Java|Características|
|---|---|---|
|**TCP** (orientado a conexión)|`Socket` (cliente) / `ServerSocket` (servidor)|Fiable, ordenado, orientado a flujo de bytes, requiere establecer conexión.|
|**UDP** (no orientado a conexión)|`DatagramSocket`, `DatagramPacket`|No fiable, sin control de orden, orientado a mensajes, más rápido.|

---

## **3. Ciclo básico TCP**

**Servidor**:

```java
ServerSocket servidor = new ServerSocket(5000); // escucha en puerto 5000
Socket socket = servidor.accept(); // espera conexión (bloqueante)
InputStream entrada = socket.getInputStream();
OutputStream salida = socket.getOutputStream();
// trabajar con DataInputStream/DataOutputStream para datos tipados
socket.close();
servidor.close();
```

**Cliente**:

```java
Socket socket = new Socket("localhost", 5000);
InputStream entrada = socket.getInputStream();
OutputStream salida = socket.getOutputStream();
socket.close();
```

Aquí:

- El **ServerSocket** espera (`accept()`) hasta que llega un cliente.
    
- El **Socket** representa la conexión punto a punto y da acceso a streams.
    

---

## **4. Ciclo básico UDP**

**Servidor**:

```java
DatagramSocket socket = new DatagramSocket(5000);
byte[] buffer = new byte[1024];
DatagramPacket paquete = new DatagramPacket(buffer, buffer.length);
socket.receive(paquete); // bloquea hasta recibir
String mensaje = new String(paquete.getData(), 0, paquete.getLength());
```

**Cliente**:

```java
DatagramSocket socket = new DatagramSocket();
byte[] datos = "Hola".getBytes();
InetAddress destino = InetAddress.getByName("localhost");
DatagramPacket paquete = new DatagramPacket(datos, datos.length, destino, 5000);
socket.send(paquete);
```

---

## **5. Relación con la teoría**

En el temario de **Programación distribuida**:

- Un **socket TCP** sería un **canal síncrono** orientado a conexión: emisor y receptor deben estar conectados, y los mensajes (bytes) llegan en orden.
    
- Un **socket UDP** sería un **canal asíncrono** orientado a datagramas: no garantiza orden ni entrega, pero el emisor no bloquea esperando confirmación.
    
- Los datos que viajan por el socket pueden estar:
    
    - En formato binario puro (bytes, `DataOutputStream`/`DataInputStream`).
        
    - En texto (`PrintWriter`/`BufferedReader`).
        
    - Serializados (Java Object Serialization, JSON, Protobuf…).
        

---

## **6. Concurrencia en servidores con sockets**

Un **servidor concurrente** en TCP usa normalmente un hilo por cliente o un pool:

```java
while (true) {
    Socket cliente = servidor.accept();
    new Thread(() -> manejarCliente(cliente)).start();
}
```

O con **ExecutorService**:

```java
ExecutorService pool = Executors.newFixedThreadPool(10);
while (true) {
    Socket cliente = servidor.accept();
    pool.execute(() -> manejarCliente(cliente));
}
```

Esto evita que un cliente lento bloquee a los demás.

---

## **7. Buenas prácticas**

- Cerrar siempre **primero streams y luego sockets**.
    
- Manejar excepciones (`IOException`, `SocketTimeoutException`).
    
- Evitar puertos reservados (<1024) para tus propios servicios.
    
- Para comunicación entre distintos lenguajes/plataformas, acordar un **protocolo** y codificación (UTF-8, binario fijo, JSON, etc.).
    
- Usar **buffers** para eficiencia (`BufferedInputStream`, `BufferedOutputStream`).
    

---

