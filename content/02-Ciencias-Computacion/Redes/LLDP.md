---
title: "Lldp"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**LLDP** (Link Layer Discovery Protocol) es un protocolo de descubrimiento de red basado en la capa de enlace (capa 2 del modelo OSI). Es un estándar abierto, definido en el **IEEE 802.1AB**, utilizado principalmente para obtener información sobre los dispositivos conectados a una red Ethernet. LLDP permite a los dispositivos de red **descubrirse mutuamente** y compartir información sobre sus capacidades, topología y detalles de conexión.

### Características Claves de LLDP


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/SolarWinds|SolarWinds]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

1. **Protocolo de Capa 2**:
    
    - LLDP funciona a nivel de **capa de enlace (Layer 2)**, lo que significa que se utiliza para recopilar información sobre los dispositivos directamente conectados a través de enlaces Ethernet o similares.
        
2. **Descubrimiento de dispositivos**:
    
    - LLDP permite a los dispositivos de red, como switches, routers, y puntos de acceso, **intercambiar información de manera automática** para conocer detalles sobre los dispositivos cercanos sin la intervención manual.
        
3. **Intercambio de información estructurada**:
    
    - LLDP permite que los dispositivos compartan una variedad de información, como:
        
        - **Nombre del dispositivo**.
            
        - **Dirección IP**.
            
        - **Capacidades de red** (por ejemplo, si el dispositivo es un switch, un router, un punto de acceso, etc.).
            
        - **Puerto de conexión** (la interfaz a la que está conectado el dispositivo).
            
        - **Información de VLAN**.
            
        - **Dirección MAC**.
            
        - **Información de capacidad de energía (PoE)**, entre otros.
            
4. **Automatización de la red**:
    
    - LLDP facilita el **descubrimiento automático** de la red, lo que puede ser útil para mapear topologías de red y para tareas de administración de red, como la planificación de capacidad o la resolución de problemas.
        
5. **Interoperabilidad**:
    
    - LLDP está diseñado para ser interoperable entre diferentes fabricantes, lo que significa que dispositivos de diferentes marcas pueden usar LLDP para compartir información entre sí.
        
6. **Actualización periódica**:
    
    - Los dispositivos que utilizan LLDP envían actualizaciones de información de manera periódica (por defecto, cada 30 segundos). Si un dispositivo deja de enviar actualizaciones, los dispositivos cercanos eliminarán la información después de un tiempo determinado.
        

### Funcionamiento de LLDP

LLDP funciona enviando **paquetes de descubrimiento** a través de la red de manera periódica. Estos paquetes son llamados **TLVs** (Type-Length-Value) y contienen la información estructurada que los dispositivos de red intercambian.

1. **Paquetes LLDP**:
    
    - Los dispositivos envían **frames LLDP** en el medio de la red. Estos **frames** contienen la información sobre el dispositivo que está enviando el paquete.
        
    - LLDP no requiere que la información sea entregada de manera confiable (es decir, no hay confirmación de recepción). Sin embargo, la red debe estar configurada para permitir el paso de estos paquetes entre dispositivos.
        
2. **Interfaz de administración**:
    
    - Los administradores de red pueden usar herramientas de administración para **ver la información recopilada por LLDP**. Por ejemplo, un administrador puede consultar la **topología de red** descubierta por LLDP, como qué dispositivos están conectados entre sí, qué puertos están en uso, etc.
        

### Ejemplos de Uso de LLDP

1. **Detección de Topología**:
    
    - LLDP se utiliza para construir una vista detallada de la **topología de red**. Un administrador puede ver la **jerarquía de switches**, los puertos a los que están conectados los dispositivos, e identificar dispositivos que podrían no ser visibles directamente.
        
2. **Planificación de Red**:
    
    - LLDP puede ser útil para **planificar la capacidad de la red**, asegurando que las conexiones se utilicen de manera eficiente y detectando cuellos de botella o posibles problemas de rendimiento.
        
3. **Resolución de Problemas**:
    
    - Si hay **problemas de conectividad** o **rendimiento** en la red, el protocolo LLDP puede ser útil para identificar en qué dispositivos o puertos está ocurriendo el fallo, ayudando a los administradores a **aislar problemas** rápidamente.
        
4. **Integración con otras herramientas**:
    
    - Herramientas como **SolarWinds**, **OpManager** o **PRTG Network Monitor** pueden utilizar LLDP para **descubrir la topología de la red** y proporcionar información visual sobre los dispositivos conectados y su estado.
        

### Comandos de LLDP

Si tu dispositivo de red es compatible con LLDP (como la mayoría de los switches y routers modernos), puedes utilizar varios comandos en la CLI (Command Line Interface) para ver la información que LLDP ha recolectado:

#### 1. **Ver la información LLDP en un Switch Cisco**:

```bash
show lldp neighbors
```

Este comando muestra una lista de dispositivos conectados que han enviado paquetes LLDP, incluyendo detalles como el nombre del dispositivo, el puerto de conexión y la dirección IP.

#### 2. **Ver la información LLDP en un Router Cisco**:

```bash
show lldp neighbors detail
```

Esto proporciona una vista más detallada de los vecinos, mostrando la información completa sobre cada dispositivo cercano, incluidos los puertos y capacidades.

#### 3. **Ver la información LLDP en un dispositivo Juniper**:

```bash
show lldp neighbors
```

En dispositivos Juniper, el comando es muy similar a los de Cisco y proporciona detalles sobre los dispositivos vecinos y las conexiones entre ellos.

#### 4. **Habilitar LLDP en un dispositivo Cisco**:

```bash
conf t
lldp run
```

Este comando habilita LLDP en el dispositivo para que comience a enviar y recibir información de descubrimiento.

---

### Aplicaciones Prácticas de LLDP

1. **Creación Automática de Mapas de Red**:
    
    - Las herramientas de monitoreo pueden usar LLDP para crear automáticamente un **mapa de la red** y visualizar cómo están conectados los dispositivos, lo que facilita la planificación y administración de redes.
        
2. **Detección de Dispositivos**:
    
    - Si un dispositivo nuevo se conecta a la red, **LLDP** permite que otros dispositivos en la red lo descubran automáticamente, obteniendo detalles como su nombre, dirección IP, y puerto de conexión.
        
3. **Seguridad y Auditoría**:
    
    - LLDP también se puede usar para asegurarse de que los dispositivos no autorizados no estén conectados a la red, ya que puedes verificar la información sobre los dispositivos que están en tu infraestructura.
        

---

### Conclusión

**LLDP** es un protocolo de **descubrimiento de dispositivos** en la red muy útil para la **gestión de redes** y la **monitorización**. Su capacidad para proporcionar información detallada sobre la topología de red y los dispositivos conectados es valiosa para los administradores de redes que necesitan comprender y gestionar sus infraestructuras de manera eficiente. Al ser un estándar abierto, su implementación es compatible entre diferentes fabricantes de equipos de red.


Un **atacante** puede utilizar **LLDP (Link Layer Discovery Protocol)** durante la fase de **reconocimiento y enumeración** para obtener información detallada sobre la infraestructura de red, lo que facilita el diseño de un ataque. LLDP es un protocolo de **capa 2** que permite a los dispositivos compartir información de **topología** y **conexiones** a través de la red. Si no se protege adecuadamente, un atacante puede aprovechar esta información para **mapear** la red y planificar el ataque con mayor precisión.

### **Cómo un atacante utiliza LLDP**

#### 1. **Descubrimiento de dispositivos de red**

LLDP permite a los dispositivos compartir información acerca de su **identidad** y **conexiones**, lo que ayuda a un atacante a obtener detalles sobre los dispositivos de red en una red. Esta información incluye:

- **Dirección MAC**: Identificación del dispositivo.
    
- **Nombre del dispositivo**: Nombre o identificador del dispositivo conectado.
    
- **Puerto de conexión**: El puerto físico o lógico al que está conectado el dispositivo.
    
- **Dirección IP**: Algunos dispositivos también pueden compartir su dirección IP.
    
- **Información de capacidades**: ¿Es un router, switch, servidor, punto de acceso, etc.?
    

El atacante puede utilizar herramientas como **snmpwalk** o **snmpget** para realizar consultas SNMP sobre dispositivos que soportan LLDP y obtener esta información.

**Ejemplo**:  
Si un atacante tiene acceso a un switch o router y puede ejecutar `snmpwalk`, puede obtener la siguiente información:

```bash
snmpwalk -v 2c -c public 192.168.1.1 LLDP-MIB::lldpRemTable
```

Este comando le devolvería la información de los dispositivos conectados, como **nombres**, **direcciones IP** y **puertos de conexión**.

#### 2. **Mapeo de la topología de red**

Una vez que el atacante tiene acceso a la información LLDP de varios dispositivos, puede construir un **mapa de la red** para ver cómo se conectan los dispositivos entre sí. Este mapeo puede mostrar:

- Qué dispositivos están conectados a qué puertos de switch o router.
    
- La ubicación de servidores clave, como servidores DNS, servidores de bases de datos, y sistemas críticos.
    
- El camino que toman los datos a través de la red.
    

Con esta información, el atacante puede identificar **dispositivos vulnerables** o **puntos de entrada** que puede atacar, y planificar el movimiento lateral dentro de la red.

#### 3. **Identificación de dispositivos de red críticos**

Un atacante puede utilizar LLDP para identificar dispositivos de red críticos que pueden ser utilizados para:

- **Ataques a routers o switches**: Los dispositivos de red como **routers** o **switches** son esenciales en la infraestructura de red, y comprometerlos puede permitir al atacante **redirigir el tráfico**, **interrumpir la conectividad** o incluso **interceptar datos**.
    
- **Ataques a servidores**: Un atacante también podría identificar **servidores importantes** (por ejemplo, servidores DNS, servidores de bases de datos) y atacarlos directamente.
    

#### 4. **Ataques de MITM (Man-in-the-Middle)**

Si el atacante obtiene acceso a la información de la topología y sabe qué dispositivos están conectados a qué puertos, puede intentar realizar un ataque de **MITM** (Man-in-the-Middle). Esto puede incluir:

- **Envenenamiento de ARP** para redirigir el tráfico a través de su dispositivo y **capturar** o **alterar** los datos.
    
- **Secuestro de conexiones**: Si el atacante sabe qué dispositivos están en la red y cómo se interconectan, puede manipular la **tabla de enrutamiento** o **configurar un dispositivo** como proxy para interceptar el tráfico entre dispositivos.
    

#### 5. **Ingeniería social dirigida**

Un atacante también puede usar la información de LLDP para realizar **ingeniería social** más efectiva. Por ejemplo:

- Si sabe que un servidor crítico está conectado a un **puerto específico** o a un **switch específico**, puede enviar un correo electrónico de **phishing** o realizar un ataque a un **usuario en esa área**, haciéndolo más dirigido y eficiente.
    

#### 6. **Evitar detección** mediante el uso de técnicas de evasión

Si un atacante está dentro de una red protegida, puede usar el protocolo **LLDP** para obtener información sobre las conexiones de la red y **ocultar su actividad**. Por ejemplo:

- Si el atacante sabe que los dispositivos de red envían regularmente paquetes LLDP, puede configurar su dispositivo para enviar **traps LLDP falsos** o manipular los datos enviados para **confundir los sistemas de monitoreo**.
    
- También podría usar la información LLDP para **camuflarse como un dispositivo legítimo**, dificultando la detección durante un ataque.
    

#### 7. **Acceder a dispositivos a través de puertos vulnerables**

LLDP puede revelar **información sobre los puertos** a los que están conectados los dispositivos, lo que puede ser útil para un atacante si los dispositivos o puertos tienen **configuraciones débiles**. Por ejemplo:

- Si un dispositivo tiene un puerto **sin asegurar** o configurado con credenciales predeterminadas, el atacante podría acceder a él para obtener más información de la red o comprometerlo.
    

#### 8. **Enumeración de dispositivos IoT**

En una red que tiene dispositivos **IoT** (como cámaras, termostatos inteligentes, impresoras, etc.), LLDP puede ser usado para obtener rápidamente información sobre estos dispositivos sin necesidad de explorarlos uno a uno. Estos dispositivos a menudo tienen **seguridad débil** o están desactualizados, lo que los convierte en **objetivos fáciles** para un atacante.

---

### ️ **Mitigación de riesgos con LLDP**

Para reducir los riesgos asociados con el uso de LLDP por parte de un atacante, considera implementar las siguientes estrategias:

1. **Desactivar LLDP en dispositivos no esenciales**:
    
    - Si no necesitas que un dispositivo participe en el descubrimiento de topología, **desactiva LLDP** en ese dispositivo.
        
2. **Segmentación de la red**:
    
    - Asegúrate de que **dispositivos críticos** como routers, switches y servidores estén aislados en segmentos de red seguros, dificultando el acceso a ellos.
        
3. **Filtrar el tráfico LLDP**:
    
    - En los dispositivos de red de borde, **filtra el tráfico LLDP** para evitar que se difunda información innecesaria a los atacantes.
        
4. **Utilizar autenticación SNMP**:
    
    - Si LLDP está habilitado en los dispositivos, asegúrate de que el acceso SNMP esté **autenticado** y protegido con contraseñas fuertes.
        
5. **Monitorización activa**:
    
    - Implementa un sistema de **monitorización de red** para detectar **anomalías en el tráfico LLDP**. Por ejemplo, una cantidad inusualmente alta de paquetes LLDP podría indicar que un dispositivo malintencionado está intentando obtener información sobre la red.
        

---

###  **Conclusión**

LLDP es una herramienta útil para **gestionar redes** y obtener información sobre dispositivos conectados, pero también representa un **riesgo de seguridad** si no se controla adecuadamente. Un atacante puede usar LLDP para **mapear la red**, descubrir dispositivos vulnerables, planificar ataques dirigidos y manipular el tráfico. Es crucial implementar **políticas de seguridad** que incluyan el **filtrado de LLDP**, **aislamiento de dispositivos críticos** y **monitoreo activo** para mitigar estos riesgos.