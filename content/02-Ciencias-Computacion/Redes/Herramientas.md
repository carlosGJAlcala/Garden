---
title: "Herramientas"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
En el documento se describen numerosas **herramientas de gestión de redes**, agrupadas por funciones. Aquí tienes un resumen organizado por tipo, con ejemplos y contexto práctico:

---

###  **1. Pruebas de capa física**


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[02-Ciencias-Computacion/Redes/LLDP|LLDP]]. [[02-Ciencias-Computacion/Redes/NETCONF|NETCONF]]. [[02-Ciencias-Computacion/Redes/NetFlow|NetFlow]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Estas herramientas diagnostican problemas **eléctricos o de señal** en cables y medios físicos.

- **Tester de cableado**: comprueba continuidad y polaridad.
    
- **Carrier sensor**: detecta señal en pines (mediante LED).
    
- **Reflectómetro (TDR/OTDR)**: localiza cortes y fallos en cables, indicando la distancia.
    
- **Certificador de cableado**: verifica que el cable cumple con normas (como diafonía o pérdida).
    
- **Tester Wi-Fi**: mide calidad de señal y detecta interferencias en el espectro.
    

---

###  **2. Alcanzabilidad y conectividad**

Comprobación de si un dispositivo está accesible.

- **Ping** (ICMP): mide latencia y pérdida.
    
    - Puede automatizarse con scripts.
        
    - Permite ajustar tamaño de paquetes y frecuencia de envío.
        

---

###  **3. Análisis de paquetes**

Herramientas para capturar y examinar el contenido de los paquetes de red.

- **Wireshark** (software): permite capturar, filtrar y analizar protocolos.
    
- **Sniffers hardware**: en entornos donde no se puede instalar software.
    

Se usa para:

- Diagnosticar fallos.
    
- Ver quién se comunica con quién.
    
- Extraer estadísticas por protocolo, host, etc.
    

---

###  **4. Descubrimiento de rutas**

Determina el camino que siguen los paquetes.

- **Traceroute / tracert**: revela los saltos intermedios y la latencia por salto.
    

---

### ️ **5. Descubrimiento de topología**

Reconstruye el mapa de red automáticamente.

- Protocolos: **LLDP**, **CDP**.
    
- Herramientas como **OPManager** muestran diagramas jerárquicos, por subred, con zoom.
    

---

###  **6. Interrogación de dispositivos**

Lectura del estado/configuración de los elementos de red.

- **CLI** (manual).
    
- **Interfaz web**.
    
- **Programación (SNMP, REST, XML)**: permite automatizar consultas y recolección de datos.
    

Ejemplo: `SNMP get` para ver estado de interfaces.

---

###  **7. Monitorización de eventos**

Detección de anomalías como:

- Interfaces caídas.
    
- Sobrecarga de CPU.
    
- Tráfico excesivo.
    

Modos:

- **Polling**: el sistema de gestión consulta cada cierto tiempo (por ejemplo vía SNMP).
    
- **Trap**: el dispositivo notifica cuando ocurre un evento.
    

Parámetros:

- Nivel de severidad (emergency, warning, notification).
    
- Visualización jerárquica y por colores.
    

---

###  **8. Monitorización de rendimiento**

Se centra en métricas cuantitativas:

- Utilización de interfaces (%).
    
- Tráfico (bps, paquetes/s).
    
- Conexiones/s.
    

Visualización:

- Temporal (línea de tiempo).
    
- Histograma (comparativa entre elementos).
    

---

###  **9. Análisis de flujo**

Estudia la naturaleza del tráfico entre extremos.

- Herramientas: **NetFlow**, **IPFIX**.
    
- Permite identificar:
    
    - Origen del tráfico pesado.
        
    - Tipos de conexiones (largas/cortas, frecuentes, por aplicación).
        
    - Cuellos de botella.
        

---

### ️ **10. Ingeniería de encaminamiento y tráfico**

Controla por dónde deben ir los flujos y cómo se gestionan los recursos.

- Definición de rutas preferentes y backup.
    
- Control de QoS.
    
- Manipulación de métricas de rutas (OSPF, BGP...).
    

---

### ️ **11. Herramientas de configuración**

Permiten cambiar parámetros de red.

- **CLI**: por consola.
    
- **NETCONF**: protocolo estructurado para configuración.
    
- **SNMP**: también permite escritura.
    
- **HTML scraping**: automatización web de interfaces gráficas.
    

Ejemplo (CLI):

```bash
Router# configure terminal
Router(config)# interface fastethernet 5/4
Router(config-if)# ip address 172.20.52.106 255.255.255.248
Router(config-if)# no shutdown
Router# end
```

---

###  **12. Aplicación de seguridad**

Incluye:

- **Firewalls**
    
- **IDS/IPS**
    
- **VPNs** (configuración y supervisión de túneles seguros)
    

Algunos routers lo integran directamente.

---

###  **13. Planificación de red**

Ayuda en el diseño de topologías, simulación y previsión.

- Ejemplo: **GNS3**, para emular redes reales y probar configuraciones antes de desplegar.
    

---

###  Conclusión

El documento recoge una **visión integral de las herramientas de gestión de red**, desde el plano físico hasta la monitorización, análisis y configuración. Saber elegir y combinar estas herramientas es clave para mantener redes **operativas, seguras y bien documentadas**. Si quieres, puedo ayudarte a agruparlas en una tabla comparativa o crear un mapa mental.