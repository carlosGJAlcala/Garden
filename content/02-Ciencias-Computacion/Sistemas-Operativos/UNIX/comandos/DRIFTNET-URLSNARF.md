---
title: "Driftnet Urlsnarf"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
### Driftnet: Herramienta para Esnifar Imágenes


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

**Driftnet** es una herramienta que se utiliza para esnifar imágenes que están siendo transmitidas en una red. Principalmente, su función es interceptar y capturar las imágenes que se envían en el tráfico HTTP. Este tipo de herramientas son comúnmente empleadas por pentesters o atacantes en entornos de redes no seguras para obtener información visual de lo que está siendo transmitido.

#### **¿Cómo Funciona Driftnet?**
Driftnet escucha el tráfico de la red y captura cualquier imagen que pase por las conexiones de red. Esto puede incluir imágenes de sitios web, correos electrónicos, redes sociales y más. Funciona a nivel de red, es decir, detecta el tráfico sin necesidad de interacción directa con las aplicaciones.

Una de las características interesantes de Driftnet es que no solo captura imágenes estáticas, sino que también puede identificar y mostrar imágenes en tiempo real. Esto es útil en ataques de man-in-the-middle (MITM), donde un atacante puede capturar imágenes que pasan a través de una red local o pública.

#### **Instalación y Uso Básico de Driftnet**
1. **Instalar Driftnet**:
   
   En sistemas basados en Linux, puedes instalar Driftnet usando un gestor de paquetes como **apt** (en distribuciones Debian/Ubuntu):

   ```bash
   sudo apt-get install driftnet
   ```

2. **Ejecutar Driftnet**:
   
   Para comenzar a capturar imágenes, basta con ejecutar Driftnet en la terminal. Debes tener privilegios de root para interceptar el tráfico de la red:

   ```bash
   sudo driftnet -i eth0
   ```

   Aquí, **eth0** es la interfaz de red que deseas monitorear (puede ser diferente según tu sistema).

3. **Ver las Imágenes**:
   
   Driftnet abrirá una ventana en tu sistema que mostrará las imágenes que se están capturando en tiempo real. Si estás escaneando un tráfico HTTP donde se transmiten imágenes, las verás reflejadas.

#### **Precauciones Legales**
Es importante recordar que el uso de herramientas como Driftnet para interceptar el tráfico de una red ajena sin permiso es **ilegal** en muchas jurisdicciones. Solo debes utilizar este tipo de herramientas en entornos controlados, como en tus propias redes o con el permiso explícito de los propietarios de las redes.

---

### Urlsnarf: Captura de Peticiones HTTP en la Terminal

**Urlsnarf** es una herramienta de sniffing centrada exclusivamente en el tráfico HTTP. Es una herramienta similar a **Wireshark**, pero mucho más simple y especializada, ya que se enfoca solo en interceptar las solicitudes HTTP, es decir, las peticiones que hacen los navegadores web a los servidores para obtener recursos como HTML, imágenes, scripts, etc.

Urlsnarf captura las URLs que pasan por la red y las imprime en la terminal. Esta herramienta es útil en auditorías de seguridad para analizar las solicitudes HTTP que los usuarios hacen en la red, o en un ataque de **man-in-the-middle** para espiar el tráfico web.

#### **Características Clave de Urlsnarf**
- **Captura HTTP**: Específicamente captura todas las solicitudes HTTP realizadas en la red, lo que incluye URLs, parámetros de consulta, cabeceras y más.
- **Interfaz de Línea de Comandos**: Funciona completamente desde la terminal, lo que la hace ligera y rápida para usar en entornos de pruebas.
- **Facilidad de Uso**: Si bien no tiene la complejidad de herramientas como Wireshark, su simplicidad permite a los usuarios concentrarse solo en las peticiones HTTP.

#### **Instalación de Urlsnarf**
1. **Instalar en sistemas basados en Debian/Ubuntu**:

   ```bash
   sudo apt-get install dsniff
   ```

   Urlsnarf viene incluido en el paquete **dsniff**, que incluye varias herramientas de análisis de red.

2. **Uso básico de Urlsnarf**:
   
   Para empezar a capturar las solicitudes HTTP en la red, simplemente ejecuta Urlsnarf desde la terminal:

   ```bash
   sudo urlsnarf -i eth0
   ```

   Aquí, **eth0** es la interfaz de red que deseas monitorear. Puedes sustituirla por la interfaz que estés usando, como **wlan0** para redes Wi-Fi.

3. **Ver el tráfico HTTP**:
   
   Urlsnarf comenzará a mostrar todas las URLs que se capturan en la red en tiempo real. Las peticiones HTTP serán mostradas de forma clara, permitiéndote ver qué sitios están visitando los usuarios en la red.

#### **Usos de Urlsnarf**
- **Monitoreo de tráfico**: Es útil para monitorear las solicitudes HTTP de una red local, por ejemplo, para ver qué sitios web son visitados en una red corporativa o en un entorno de pruebas.
- **Análisis forense**: Se puede usar en análisis de tráfico para ayudar a investigar incidentes de seguridad, identificando solicitudes HTTP sospechosas.
- **Ataques Man-in-the-Middle**: Al igual que con Driftnet, esta herramienta también puede ser utilizada en un ataque de MITM para interceptar el tráfico HTTP y espiar las actividades web de los usuarios.

#### **Precauciones Legales**
Al igual que con cualquier herramienta de sniffing, el uso de **Urlsnarf** sin autorización en una red ajena es ilegal. Solo debes utilizarla en redes en las que tengas permiso para realizar auditorías o análisis de seguridad.

---

### **Conclusión**

Ambas herramientas, **Driftnet** y **Urlsnarf**, son poderosas en la categoría de análisis y esnifado de tráfico de red, pero cada una tiene un enfoque diferente:

- **Driftnet** se especializa en capturar imágenes transmitidas en la red, lo que puede ser útil en auditorías de seguridad o como parte de pruebas de penetración.
- **Urlsnarf** es una herramienta ligera para capturar solicitudes HTTP, ideal para monitorear el tráfico web en tiempo real desde la terminal.

Ambas herramientas requieren un conocimiento básico de redes y deben ser usadas de forma ética y legal en entornos controlados.