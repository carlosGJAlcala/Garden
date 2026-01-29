---
title: "Snmp Para Enumerarcion"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
En el contexto de ciberseguridad, un atacante podría intentar aprovechar el **protocolo SNMP** y las **MIBs** para comprometer dispositivos en una red, acceder a información sensible, manipular configuraciones o incluso causar interrupciones en los servicios de red. A continuación, te explico cómo un atacante podría utilizar los conceptos que hemos visto hasta ahora en un escenario de ataque.

### 1. **Exploración de dispositivos a través de SNMP**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

Los atacantes podrían usar herramientas como **snmpget**, **snmpwalk** y **snmpwalk -v1** para escanear redes en busca de dispositivos vulnerables que expongan información a través de SNMP. Si los dispositivos no están configurados correctamente o usan configuraciones predeterminadas (como la comunidad `public`), el atacante puede obtener fácilmente información valiosa sobre la infraestructura de red.

- **Comando de exploración**:
    
    ```bash
    snmpwalk -c public -v 1 <ip_dispositivo>
    ```
    
    Este comando puede ser utilizado para obtener información sobre dispositivos, como nombres de sistema, interfaces de red, tráfico, y más.
    

#### Riesgos:

- **Enumeración de dispositivos**: El atacante podría obtener una lista de dispositivos en la red.
    
- **Recolección de información sensible**: Información sobre la configuración del sistema, como el nombre de los dispositivos, ubicaciones, direcciones IP, y otros valores importantes podrían ser obtenidos.
    
- **Acceso a credenciales**: Algunos OIDs podrían contener configuraciones como contraseñas o comunidades predeterminadas.
    

### 2. **Explotación de configuraciones débiles o predeterminadas**

Una de las debilidades más comunes de SNMP es que muchos dispositivos están configurados con comunidades predeterminadas, como `public` para lectura y `private` para escritura. Si un atacante sabe que un dispositivo usa estas configuraciones por defecto, puede fácilmente consultar y modificar la configuración del dispositivo.

#### Ejemplo de ataque:

- **Comando de modificación**:
    
    ```bash
    snmpset -v 1 -c private <ip_dispositivo> sysName.0 s "NewName"
    ```
    

Un atacante podría modificar el nombre del dispositivo, cambiar la configuración de una interfaz de red o incluso apagar un servicio crítico de red.

#### Riesgos:

- **Modificación de configuración**: Un atacante podría cambiar parámetros del dispositivo, como los nombres del sistema, las configuraciones de red, o los parámetros de seguridad.
    
- **Interrupción de servicios**: El atacante podría deshabilitar interfaces de red, interrumpir el tráfico o incluso hacer que el dispositivo sea inaccesible.
    

### 3. **Falsificación de SNMP Traps**

Un atacante podría explotar las **notificaciones SNMP (traps)** enviando mensajes falsificados a un servidor de gestión SNMP. Esto podría permitirle manipular los eventos gestionados en la red y causar una reacción por parte del administrador de la red.

#### Ejemplo de ataque:

- Un atacante podría generar un **SNMP Trap** falso que simule un evento crítico (como un enlace caído) para engañar al administrador de la red y desviar su atención de una intrusión real.
    

#### Riesgos:

- **Manipulación de eventos**: El atacante podría hacer que el servidor de gestión reciba información falsa, alterando las alertas o haciendo que se tomen acciones incorrectas.
    
- **Desviación de atención**: El atacante podría generar eventos falsos para que el equipo de respuesta ante incidentes se enfoque en falsos positivos, mientras mantiene la intrusión real sin ser detectada.
    

### 4. **Acceso a información sensible mediante OIDs**

Algunos OIDs pueden contener información sensible, como configuraciones de seguridad, direcciones IP, contraseñas, o detalles internos de la red. Si un atacante obtiene acceso a estos OIDs, puede obtener información confidencial sobre la infraestructura de la red.

#### Ejemplo:

- Consultar el **OID sysLocation.0** podría revelar la ubicación física del dispositivo, lo que podría ser útil para un atacante en la fase de **reconocimiento**.
    

#### Riesgos:

- **Recopilación de información sensible**: Un atacante podría recopilar información crítica sobre la infraestructura de la red, facilitando la planificación de un ataque más profundo.
    
- **Enumeración de dispositivos y servicios**: Los atacantes pueden identificar dispositivos críticos y servicios expuestos en la red.
    

### 5. **Ataques de Denegación de Servicio (DoS) a través de SNMP**

Aunque SNMP no es típicamente un vector de ataque directo para denegación de servicio (DoS), un atacante podría intentar saturar un servidor SNMP con solicitudes masivas, lo que podría afectar el rendimiento o incluso causar la caída de los dispositivos de red si no están correctamente protegidos.

#### Ejemplo de ataque:

- Enviar un número masivo de **snmpget** o **snmpwalk** al dispositivo, consumiendo recursos o afectando su rendimiento.
    

#### Riesgos:

- **Interrupción del servicio**: Si un atacante genera una carga excesiva en los dispositivos, puede ralentizar o bloquear el servicio.
    
- **Saturación de recursos**: Los recursos del servidor SNMP o los dispositivos de red pueden agotarse, impidiendo el acceso legítimo o afectando el tráfico de red.
    

### 6. **Uso de SNMP para el desplazamiento lateral (lateral movement)**

Si un atacante ya tiene acceso a un dispositivo en la red, podría usar SNMP para moverse lateralmente a otros dispositivos. Por ejemplo, podría obtener los nombres de los sistemas de otras máquinas y sus direcciones IP y luego intentar conectarse a ellos utilizando el protocolo SNMP o explotando otras vulnerabilidades en esos dispositivos.

#### Ejemplo:

- Un atacante obtiene el nombre del sistema de un servidor y sus interfaces de red usando **snmpwalk** y luego usa esa información para atacar otros dispositivos de la red.
    

#### Riesgos:

- **Desplazamiento lateral**: El atacante puede moverse por la red utilizando la información obtenida de SNMP, explotando vulnerabilidades adicionales.
    
- **Acceso no autorizado a más sistemas**: Al obtener información de dispositivos adicionales, el atacante puede comprometer otros sistemas en la misma red.
    

### Prevención y mitigación

Para mitigar estos riesgos, se deben implementar prácticas de seguridad estrictas en relación con SNMP:

- **Deshabilitar SNMP si no es necesario**.
    
- **Configurar comunidades de SNMP seguras** (usando cadenas de comunidad personalizadas, no predeterminadas como `public` o `private`).
    
- **Usar SNMPv3**, que ofrece **autenticación y cifrado** para proteger las comunicaciones.
    
- **Limitar el acceso a SNMP** mediante **firewalls** y listas de control de acceso (ACL) para permitir que solo los servidores de gestión confiables puedan acceder al agente SNMP.
    
- **Monitorizar el tráfico SNMP** para detectar actividades sospechosas, como un uso excesivo de **snmpget** o **snmpwalk**.
    

En resumen, SNMP es una herramienta poderosa para la administración de redes, pero también puede ser un vector de ataque si no se configura adecuadamente. Los atacantes pueden explotar configuraciones débiles, recopilar información crítica, modificar configuraciones o incluso generar eventos falsos para desviar la atención de los administradores. La seguridad de SNMP debe ser una prioridad para prevenir estos tipos de ataques.