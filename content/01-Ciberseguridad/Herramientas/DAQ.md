---
title: "Daq"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **DAQ (Data Acquisition) en Blue Team y Seguridad Informática**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/ZEEK|ZEEK]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]].

En el contexto de **Blue Team** y **seguridad informática**, **DAQ (Data Acquisition o Adquisición de Datos)** se refiere a la recopilación y procesamiento de información de diferentes fuentes dentro de una infraestructura de TI para **detectar, analizar y responder a amenazas**.

---

## **1. ¿Qué son los DAQ en Seguridad Informática?**

Los **DAQ** en el ámbito de Blue Team se centran en la **captura y análisis de datos de seguridad**, como registros de eventos, tráfico de red, cambios en el sistema y actividad de usuarios. Estos datos son utilizados para:

- **Monitoreo y detección de amenazas** en tiempo real.
- **Respuesta a incidentes** con información detallada de ataques.
- **Forense digital** para analizar ataques después de que ocurren.
- **Análisis de comportamiento** de usuarios y procesos sospechosos.

---

## **2. Tipos de DAQ en Seguridad**

### **1️⃣ DAQ en Monitoreo de Red (Network DAQ)**

- Captura y analiza tráfico de red en tiempo real.
- Usa herramientas como **Snort, Suricata o Zeek (Bro IDS)** para detectar ataques.
- Puede implementarse en **IDS/IPS, firewalls y SIEMs**.

Ejemplo de captura de tráfico con **tcpdump**:

```bash
tcpdump -i eth0 -w captura.pcap
```

### **2️⃣ DAQ en Seguridad de Sistemas (Host DAQ)**

- Analiza registros de eventos en sistemas Windows y Linux.
- Captura cambios en archivos, procesos y privilegios de usuario.
- Se usa en **EDR (Endpoint Detection and Response)** y HIDS (Host-based Intrusion Detection Systems).

Ejemplo de monitoreo con **auditd** en Linux:

```bash
auditctl -w /etc/passwd -p wa -k passwd_changes
```

Este comando registra cambios en el archivo `/etc/passwd`.

### **3️⃣ DAQ en Seguridad en la Nube (Cloud DAQ)**

- Recopila registros de servicios en la nube como **AWS CloudTrail, Azure Sentinel y Google Security Command Center**.
- Permite detectar accesos no autorizados y anomalías en entornos cloud.

Ejemplo de búsqueda de eventos en AWS CloudTrail:

```bash
aws cloudtrail lookup-events --lookup-attributes AttributeKey=EventName,AttributeValue=ConsoleLogin
```

---

## **3. DAQ y su Relación con SIEM y SOC**

Los sistemas **SIEM (Security Information and Event Management)** usan DAQ para recopilar y correlacionar eventos de seguridad en una organización.

Un **SOC (Security Operations Center)** usa DAQ para:

1. **Monitorear ataques en tiempo real**.
2. **Realizar análisis forense** en caso de incidentes.
3. **Correlacionar eventos sospechosos** entre múltiples fuentes.

Ejemplo de uso en SIEM (con ELK Stack - Elastic, Logstash y Kibana):

```bash
filebeat -e -c filebeat.yml
```

Este comando envía logs al sistema de SIEM para análisis.

---

## **4. Herramientas de DAQ para Blue Team**

|**Herramienta**|**Uso Principal**|**Tipo de DAQ**|
|---|---|---|
|**Wireshark**|Captura y análisis de paquetes de red|Network DAQ|
|**Zeek (Bro IDS)**|Detección de intrusos en red|Network DAQ|
|**OSSEC**|Monitoreo de archivos y registros|Host DAQ|
|**Sysmon**|Registro detallado en Windows|Host DAQ|
|**AWS CloudTrail**|Registro de eventos en AWS|Cloud DAQ|
|**Splunk**|SIEM para correlación de eventos|Integrado|

---

## **5. Conclusión**

Los **DAQ en Blue Team** son esenciales para **monitoreo, detección y respuesta a incidentes** en seguridad informática. Se utilizan en sistemas de detección de intrusos, análisis forense y plataformas SIEM para garantizar la protección de redes y servidores. Un equipo de **Blue Team eficaz** debe saber configurar y analizar datos de múltiples fuentes para prevenir ataques y responder rápidamente a amenazas.