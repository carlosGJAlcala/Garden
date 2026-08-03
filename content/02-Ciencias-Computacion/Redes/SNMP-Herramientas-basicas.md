---
title: "Snmp Herramientas Basicas"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---

### Herramientas básicas de SNMP


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/OSPF|OSPF]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Telegraf|Telegraf]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

1. **Comandos principales:**
    
    - **snmpget**: Permite realizar consultas a un agente SNMP para obtener valores específicos de un OID (Object Identifier). Por ejemplo:
        
        ```bash
        snmpget -c public -v 1 <ip_dispositivo> system.sysName.0
        ```
        
        Este comando solicita el nombre del sistema (`sysName`) del dispositivo de destino.
        
    - **snmpset**: Permite modificar valores de configuración en el dispositivo gestionado mediante el protocolo SNMP. Se utiliza para establecer nuevos valores en los OIDs.
        
        ```bash
        snmpset -c public -v 1 <ip_dispositivo> sysName.0 s "nuevoNombre"
        ```
        
    - **snmpwalk**: Permite recorrer una rama completa de la MIB (Management Information Base) y obtener una lista de todos los valores disponibles bajo un OID determinado.
        
        ```bash
        snmpwalk -c public -v 1 <ip_dispositivo> system
        ```
        
    - **snmptranslate**: Traduce entre nombres y OIDs en la MIB, lo que facilita la interpretación de los valores o identificadores. Algunos ejemplos de su uso son:
        
        ```bash
        snmptranslate -On -IR system.sysName.0
        snmptranslate -Td -IR system.sysName.0
        ```
        
    - **snmpdelta**: Supervisión en tiempo real de ciertos valores de la MIB, como el tráfico de red. Se puede usar para ver cómo cambian los valores con el tiempo:
        
        ```bash
        snmpdelta -Cp 5 -c public -v 1 <ip_dispositivo> ip.ipInReceives.0
        ```
        
2. **Primitivas SNMP**: Los comandos de SNMP interactúan mediante diferentes tipos de primitivas. Algunas de las primitivas comunes incluyen:
    
    - **GetRequest**: Usada en `snmpget` para solicitar un valor.
        
    - **GetResponse**: Respuesta a una solicitud `GetRequest`.
        
    - **SetRequest**: Usada en `snmpset` para modificar un valor.
        
    - **GetNextRequest**: Usada en `snmpgetnext` para obtener el siguiente valor en una lista de OIDs.
        
    - **WalkRequest**: Usada en `snmpwalk` para recorrer todos los valores de un OID.
        
3. **Comunidad SNMP**: Las comunidades SNMP son una forma básica de control de acceso, que funcionan como contraseñas compartidas para determinar quién puede leer o modificar la MIB. Existen diferentes niveles de acceso, como "public" (lectura) y "private" (lectura y escritura). En algunos casos, también se pueden definir otras comunidades personalizadas.
    
4. **Activación y configuración de SNMP**: Para que un dispositivo pueda ser gestionado mediante SNMP, es necesario configurar un **agente SNMP**. En sistemas Linux, el archivo de configuración del agente es típicamente `/etc/snmp/snmpd.conf`. Este archivo define qué comunidades están habilitadas, qué versiones de SNMP se utilizan y qué objetos se pueden gestionar.
    
5. **Prácticas comunes**:
    
    - **Obtener datos de una MIB**: Usar comandos como `snmpwalk` o `snmpget` para recuperar información sobre un dispositivo.
        
    - **Modificar configuraciones**: Usar `snmpset` para cambiar valores de configuración de un dispositivo, como el nombre o la ubicación de un sistema.
        
    - **Supervisión en tiempo real**: Usar `snmpdelta` para monitorizar valores como el tráfico de red de manera continua.
        

### Resumen

En resumen, las herramientas básicas de gestión SNMP permiten interactuar con dispositivos de red mediante comandos que se comunican con el agente SNMP. Estas herramientas son esenciales para la administración y monitorización de redes, permitiendo a los administradores obtener información detallada sobre los dispositivos, modificar configuraciones y realizar un seguimiento del rendimiento a lo largo del tiempo.

Aquí tienes ejemplos concretos de cómo **monitorizar conexiones WAN usando SNMP**, centrados en interfaces de red y rutas IP. Utilizaremos comandos con `snmpwalk` y `snmpget`, y mostraremos qué parámetros clave puedes extraer.

---

###  Requisitos previos

Para ejecutar estos comandos:

- Tener **instalado `snmp`** (cliente) en tu máquina de monitorización.
    
- Conocer:
    
    - La **IP del router/dispositivo WAN**.
        
    - La **versión de SNMP** usada (v2c o v3).
        
    - La **comunidad** SNMP (si usas v2c), o los credenciales de usuario (v3).
        

---

##  EJEMPLOS CON SNMP

---

###  1. Estado de una interfaz WAN

####  Ver si una interfaz está administrativamente y operativamente activa

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifAdminStatus.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifOperStatus.2
```

- `ifAdminStatus`: indica si está habilitada en la config.
    
- `ifOperStatus`: si está _realmente_ operativa.
    

Valores posibles:

- `1` = up
    
- `2` = down
    
- `3` = testing
    

####  Obtener nombre y descripción de la interfaz

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifDescr.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifName.2
```

Útil para identificar que estás viendo la interfaz correcta (por ejemplo, `GigabitEthernet0/1`).

---

###  2. Uso de ancho de banda

####  Bytes entrantes y salientes

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifInOctets.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifOutOctets.2
```

Puedes hacer dos consultas con diferencia de tiempo (por ejemplo, 1 minuto) y calcular:

- Bytes/s
    
- Tráfico en bits/s
    

####  Velocidad nominal de la interfaz

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifSpeed.2
```

Esto te dice la capacidad teórica máxima (por ejemplo, `1000000000` para 1 Gbps).

---

###  3. Errores y descartar paquetes

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifInErrors.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifOutErrors.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifInDiscards.2
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifOutDiscards.2
```

Estos valores te ayudan a detectar:

- Colisiones.
    
- Fallos físicos (cables, módulos, interfaz defectuosa).
    
- Congestión.
    

---

###  4. Tiempo desde el último cambio de estado

```bash
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifLastChange.2
```

Este valor es un contador de _TimeTicks_ desde que cambió de estado. Si ves cambios frecuentes, puede haber **intermitencias** o problemas de línea.

---

###  5. Rutas IP relevantes

####  Mostrar tabla de rutas IP

```bash
snmpwalk -v2c -c public 192.168.1.1 IP-MIB::ipRouteTable
```

Esta tabla incluye:

- `ipRouteDest`: red de destino.
    
- `ipRouteNextHop`: siguiente salto.
    
- `ipRouteType`: tipo de ruta (`3` = indirecta).
    
- `ipRouteMetric1`: prioridad.
    
- `ipRouteIfIndex`: qué interfaz la gestiona.
    

Puedes buscar, por ejemplo, qué ruta usa el router para llegar a `0.0.0.0` (la salida a Internet):

```bash
snmpwalk -v2c -c public 192.168.1.1 IP-MIB::ipRouteDest | grep 0.0.0.0
```

---

###  6. Traps por cambios de estado (pasivo)

Si configuras **traps SNMP** en tu router, puedes recibir notificaciones automáticas cuando:

- Una interfaz cambia a _down_.
    
- Se pierde la conectividad con un vecino BGP, OSPF, etc.
    
- Aparecen errores.
    

Para recibir traps necesitas:

- Un **servidor SNMP trap receiver** (como `snmptrapd`, Zabbix o Nagios).
    
- Configurar el **router** para enviar traps al host monitor.
    

---

##  Conclusión

Usando SNMP puedes monitorizar cualquier aspecto técnico de una **conexión WAN**, desde si está activa hasta si hay errores, congestión o rutas anómalas. Con `snmpget` y `snmpwalk` puedes hacer pruebas manuales, y con herramientas como **Telegraf + SNMP input**, **Zabbix**, **LibreNMS** o **Nagios**, puedes automatizar esta supervisión y generar alertas si algo falla.

