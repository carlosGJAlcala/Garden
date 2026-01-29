---
title: "Netflow"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**NetFlow** y **IPFIX** son dos tecnologías de análisis de flujo de tráfico que se utilizan para **monitorear** y **analizar** el tráfico de red, proporcionando información detallada sobre cómo los datos circulan a través de la red. Ambas son esenciales para obtener visibilidad sobre el tráfico, identificar cuellos de botella, gestionar la carga de tráfico y solucionar problemas en la red.

### **1. NetFlow**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/SolarWinds|SolarWinds]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Kibana|Kibana]].

**NetFlow** es un protocolo desarrollado por **Cisco** para recopilar y almacenar información sobre el tráfico de red que pasa a través de un dispositivo de red, como un router o switch. Es uno de los protocolos más populares utilizados en el análisis de flujo de tráfico.

#### **Características de NetFlow**:

- **Flujos de tráfico**: NetFlow recopila datos sobre flujos de tráfico, los cuales son definidos como una secuencia de paquetes que comparten ciertas características, como la dirección IP de origen y destino, el puerto de origen y destino, el protocolo de capa 4 (TCP, UDP), y otros parámetros.
    
- **Generación de informes**: Los dispositivos de red generadores de flujos (como routers o switches) envían información sobre los flujos a un colector NetFlow. Este colector almacena y analiza los flujos de tráfico.
    
- **Análisis de tráfico**: Ayuda a obtener información sobre el **tipo de tráfico**, la **utilización del ancho de banda**, las **conexiones más frecuentes**, y los **top usuarios**.
    
- **Monitoreo de la red**: Facilita el monitoreo y la gestión de la red, ayudando a identificar cuellos de botella, anomalías, y tráfico no deseado.
    

#### **Ejemplo de parámetros que NetFlow recopila**:

- Dirección IP de origen y destino.
    
- Puertos de origen y destino.
    
- Protocolo (por ejemplo, TCP o UDP).
    
- Número de paquetes y bytes transferidos.
    
- Tiempo de inicio y fin de la comunicación.
    
- Identificación del flujo (ID de flujo).
    

#### **Cómo funciona NetFlow**:

- **Paso 1**: Un dispositivo de red como un **router** o **switch** recopila información sobre los flujos de tráfico que pasan a través de él.
    
- **Paso 2**: Este dispositivo envía los **flujos** a un colector NetFlow que almacena los datos.
    
- **Paso 3**: Los analistas de red pueden usar herramientas para analizar los datos recolectados, identificar patrones de tráfico y tomar decisiones para optimizar la red.
    

#### **Herramientas comunes con NetFlow**:

- **SolarWinds NetFlow Traffic Analyzer**.
    
- **PRTG Network Monitor**.
    
- **ManageEngine NetFlow Analyzer**.
    

---

### **2. IPFIX (Internet Protocol Flow Information Export)**

**IPFIX** es una extensión del protocolo NetFlow, que fue **normalizado** por el **IETF** (Internet Engineering Task Force) para proporcionar una versión más abierta y flexible del protocolo NetFlow. IPFIX se basa en NetFlow, pero tiene mejoras clave que lo hacen más versátil y adaptable a diferentes necesidades de monitoreo.

#### **Características de IPFIX**:

- **Estándar abierto**: A diferencia de NetFlow, que fue inicialmente desarrollado por Cisco, IPFIX es un estándar abierto que puede ser implementado por cualquier fabricante de equipos de red.
    
- **Mayor flexibilidad**: IPFIX permite definir más parámetros de **información de flujo** y personalizar cómo se recopilan, exportan y almacenan los datos.
    
- **Mejor soporte para redes grandes**: IPFIX puede manejar una mayor cantidad de flujos y proporciona un mejor soporte para el monitoreo de **redes distribuidas** y de gran escala.
    

#### **Diferencias entre NetFlow e IPFIX**:

1. **Estándares**:
    
    - **NetFlow** es propietario de Cisco, mientras que **IPFIX** es un estándar abierto.
        
2. **Flexibilidad**:
    
    - **IPFIX** ofrece una mayor flexibilidad en la recolección de datos de tráfico, ya que permite que los administradores personalicen el tipo de datos que se recopilan.
        
3. **Compatibilidad**:
    
    - **IPFIX** soporta flujos más complejos y mayores volúmenes de datos, siendo más adecuado para redes **grandes** o **distribuidas**.
        

#### **Ejemplo de parámetros adicionales que IPFIX puede recopilar**:

- Información detallada de la **red de acceso**.
    
- Soporte de **flujos multidimensionales**, como los relacionados con la calidad de servicio (QoS).
    
- **Metadatos de aplicaciones** (por ejemplo, protocolos de capa 7 como HTTP, FTP, DNS).
    

#### **Cómo funciona IPFIX**:

- **Paso 1**: Al igual que con NetFlow, los dispositivos de red recopilan información sobre los flujos de tráfico.
    
- **Paso 2**: Esta información es exportada a un colector IPFIX, que la almacena y analiza.
    
- **Paso 3**: El análisis de los datos recolectados permite identificar patrones de tráfico, utilizar los datos para informes detallados y tomar decisiones sobre la gestión de la red.
    

#### **Herramientas comunes con IPFIX**:

- **Wireshark** (para capturar y analizar flujos IPFIX).
    
- **ntopng** (monitorización y análisis de flujos en tiempo real).
    
- **Elastic Stack (Elasticsearch y Kibana)** con plugins para IPFIX.
    

---

### **Beneficios del análisis de flujo con NetFlow/IPFIX**

1. **Visibilidad completa de la red**: Te permite observar cómo fluye el tráfico a través de la red, qué aplicaciones consumen más ancho de banda, qué usuarios están generando más tráfico, y mucho más.
    
2. **Detección de anomalías**: Puedes detectar tráfico inusual, como **ataques DDoS**, **anomalías en el uso de ancho de banda** o tráfico no autorizado.
    
3. **Optimización de recursos**: Al identificar cuellos de botella, puedes mejorar la **gestión de la red** y tomar decisiones sobre la optimización de los recursos.
    
4. **Planificación de capacidad**: Ayuda a identificar **picos de tráfico** y **tendencias** que pueden indicar la necesidad de aumentar la capacidad de la red.
    
5. **Solución de problemas**: Proporciona información valiosa para **aislar problemas de red** y obtener detalles precisos sobre el comportamiento del tráfico.
    

---

### **Ejemplo de cómo usar NetFlow/IPFIX en una red**

Supongamos que eres el administrador de una red corporativa y deseas monitorear el tráfico entre diferentes sucursales para asegurarte de que el ancho de banda no esté siendo utilizado de forma excesiva por ciertas aplicaciones.

1. **Configurar NetFlow en los routers**: Configuras NetFlow en los routers entre las sucursales para que recojan y exporten información de los flujos de tráfico.
    
2. **Configurar un colector**: Configuras un **colector NetFlow/IPFIX** (como **SolarWinds** o **PRTG**) para recibir los datos exportados.
    
3. **Análisis de datos**: Usas las herramientas de análisis para observar qué aplicaciones están consumiendo más ancho de banda y si existen **picos anómalos** de tráfico.
    
4. **Alertas y optimización**: Configuras alertas para cuando el tráfico supere ciertos umbrales y realizas cambios en la configuración de la red para optimizar el uso del ancho de banda.
    

---

### **Conclusión**

**NetFlow** y **IPFIX** son herramientas esenciales para **monitorear y analizar el tráfico de red** de forma detallada. Mientras que NetFlow es un protocolo ampliamente utilizado en entornos Cisco, **IPFIX** es un estándar abierto que ofrece más flexibilidad y escalabilidad para redes grandes o distribuidas. Ambos permiten la **visualización de patrones de tráfico**, la **detección de problemas de rendimiento** y la **optimización de la red** en tiempo real. La integración con herramientas de análisis y visualización, como **Wireshark**, **Elastic Stack** y **ntopng**, facilita la recopilación, procesamiento y visualización de los datos, proporcionando una visión completa de la red.