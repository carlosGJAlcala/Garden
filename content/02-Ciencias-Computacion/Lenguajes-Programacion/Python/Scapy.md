---
title: "Scapy"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - python
---
### **¿Qué es Scapy?**


> **Relacionado**: [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/ARP-SPOOFING|ARP SPOOFING]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

**Scapy** es una poderosa herramienta de manipulación y análisis de paquetes de red escrita en Python. Permite la creación, envío y captura de paquetes de red, lo que la hace útil para tareas como análisis de redes, pruebas de penetración y experimentación con protocolos de comunicación. Scapy tiene una interfaz simple y permite trabajar con muchos protocolos de red a nivel de capa de enlace, red, transporte y aplicación.

### **Funcionalidades principales de Scapy:**
1. **Creación de paquetes**: Puedes construir paquetes desde cero, especificando los campos y parámetros del protocolo.
2. **Envío y captura de paquetes**: Permite enviar paquetes a la red y capturar respuestas o tráfico.
3. **Manipulación de protocolos**: Es posible modificar fácilmente campos de protocolos específicos como IP, TCP, UDP, ARP, ICMP, entre otros.
4. **Escaneo y exploración de redes**: Scapy se usa ampliamente para realizar escaneos de redes, como escaneos ARP, escaneos de puertos, etc.
5. **Análisis de tráfico**: Puedes analizar el tráfico capturado y extraer información útil, como IPs, puertos, y más.

### **Explicación del código que mencionas:**

Este código utiliza Scapy para realizar un escaneo ARP en una red local, identificando las direcciones MAC y las IPs de los dispositivos conectados en la red. A continuación, te explico el código línea por línea:

```python
import scapy
from scapy.all import srp, Ether, ARP, conf
```
- **Importación de módulos:**  
   Aquí importamos el módulo `scapy` y desde `scapy.all` se importan varias clases y funciones que se utilizarán en el código:
   - `srp`: Es una función que se utiliza para enviar y recibir paquetes a nivel de enlace de datos (Ethernet) y red (ARP).
   - `Ether`: Representa la capa de enlace de datos Ethernet.
   - `ARP`: Representa el protocolo ARP (Address Resolution Protocol), que se utiliza para mapear direcciones IP a direcciones MAC.
   - `conf`: Es un objeto de configuración en Scapy, que se utiliza para ajustar configuraciones globales, como la cantidad de información que se muestra en la terminal.

```python
conf.verb = 0
```
- **Desactivar la verbosidad:**  
   La opción `conf.verb = 0` desactiva los mensajes de información detallada que Scapy normalmente imprime durante el envío y la recepción de paquetes. En este caso, `0` significa "sin verbosidad". Si quisieras más detalles, podrías cambiar el valor a `1` o `2` para obtener más información.

```python
ans, unans = srp(Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(pdst="192.168.0.0/24"), timeout=2)
```
- **Envío de paquetes ARP:**  
   Aquí estamos enviando un paquete ARP en la red local para descubrir las direcciones IP y MAC de los dispositivos conectados. Vamos a desglosarlo:

   - **`Ether(dst="ff:ff:ff:ff:ff:ff")`**:  
     Crea un paquete Ethernet con la dirección de destino configurada como `ff:ff:ff:ff:ff:ff`, que es la dirección MAC de difusión (broadcast). Esto significa que el paquete se enviará a todos los dispositivos de la red local.
     
   - **`ARP(pdst="192.168.0.0/24")`**:  
     Aquí creamos un paquete ARP que está buscando la dirección MAC de todos los dispositivos en el rango de direcciones IP `192.168.0.0/24`, es decir, todas las direcciones IP en la subred `192.168.0.0` hasta `192.168.0.255`. Este paquete ARP pregunta a cada dispositivo "¿quién tiene esta IP?".

   - **`timeout=2`**:  
     Define el tiempo de espera en segundos para recibir una respuesta. En este caso, esperamos 2 segundos para obtener respuestas ARP.

   - El resultado de la función `srp()` es que `ans` contendrá los paquetes de respuesta ARP recibidos y `unans` contendrá los paquetes que no obtuvieron respuesta.

```python
for snd, rcv in ans:
    print(rcv.sprintf(r"%Ether.src%, en la IP %ARP.psrc%"))
```
- **Procesar las respuestas ARP:**  
   Este ciclo recorre las respuestas almacenadas en `ans`. Cada respuesta ARP tiene dos partes: `snd` (el paquete enviado) y `rcv` (el paquete recibido). Solo nos interesa la parte de la respuesta (`rcv`).

   - **`rcv.sprintf(r"%Ether.src%, en la IP %ARP.psrc%")`**:  
     Aquí usamos el método `sprintf()` de Scapy para formatear la salida y extraer los valores de los campos relevantes:
     - `%Ether.src%`: Extrae la dirección MAC del dispositivo que ha respondido (la fuente del paquete Ethernet).
     - `%ARP.psrc%`: Extrae la dirección IP que el dispositivo está asociando con su dirección MAC (la IP fuente del paquete ARP).

   El resultado será una línea por cada dispositivo que respondió al paquete ARP, mostrando su dirección MAC y la dirección IP correspondiente.

---

### **¿Cómo funciona este código?**
1. **El script envía un paquete ARP de difusión (broadcast)** a la red `192.168.0.0/24` preguntando por las direcciones MAC de todos los dispositivos en esa red.
2. **Los dispositivos en la red responden con un paquete ARP** que contiene su dirección MAC asociada con su dirección IP. Esta es la información que buscamos.
3. **El script recibe las respuestas ARP** y las procesa para mostrar la dirección MAC (`Ether.src`) y la IP asociada (`ARP.psrc`) de cada dispositivo que ha respondido al paquete ARP.
4. **El resultado es una lista de direcciones IP y MAC** de todos los dispositivos activos en la red local.

### **Aplicaciones del código**
Este tipo de escaneo ARP es muy útil para descubrir dispositivos activos en una red. A menudo se utiliza en el contexto de:
- **Escaneos de red**: Para identificar dispositivos activos.
- **Ataques ARP Spoofing**: Para llevar a cabo ataques de suplantación de dirección MAC.
- **Análisis de redes locales**: Para mapear la infraestructura de una red.

---

### **Resumen**
- **Scapy** es una herramienta poderosa y flexible para manipular paquetes de red.
- El código enviado realiza un escaneo ARP para descubrir dispositivos en la red local (`192.168.0.0/24`) y muestra las direcciones IP y MAC de los dispositivos que responden a la consulta ARP.
- **`srp`** se utiliza para enviar paquetes a nivel de enlace de datos (Ethernet) y recibir respuestas.
- **`Ether` y `ARP`** permiten construir y manejar los paquetes a nivel de enlace de datos y red, respectivamente.

Este script es solo un ejemplo básico de cómo se puede usar Scapy para hacer un escaneo ARP, pero Scapy es muy versátil y puede usarse para muchos otros tipos de pruebas y manipulaciones de paquetes en redes.

```python
import scapy

from scapy.all import srp,Ether,ARP,conf

  

conf.verb =0

ans,unans=srp(Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(pdst="192.168.0.0/24"),timeout=2)

  

for snd,rcv in ans:

    print rcv.sprintf(r"%Ether.src%, en la IP %ARP.psrc%")
```
