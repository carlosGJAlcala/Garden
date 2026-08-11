---
title: "Estrella Optica"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - dispositivosot
---
Basándome en la imagen del rack, la **"estrella óptica"** es el **dispositivo físico** que implementa la topología de red óptica que te expliqué anteriormente.

## **Estrella Óptica - Dispositivo Físico**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

### **¿Qué veo en la imagen?**
Un **rack de comunicaciones** con varios equipos, donde la **estrella óptica** sería uno de estos dispositivos (probablemente con múltiples puertos de fibra óptica).

### **Características del dispositivo:**
- **Switch/Hub óptico** con múltiples puertos
- **Puertos de fibra óptica** (conectores SC, LC o ST)
- **LEDs de estado** por cada puerto
- **Fuente de alimentación** redundante
- **Gestión SNMP** para monitoreo

### **Función específica:**
1. **Concentra** todas las conexiones de fibra óptica
2. **Distribuye** las comunicaciones a todos los equipos de campo
3. **Convierte** señales ópticas a eléctricas cuando es necesario
4. **Gestiona** el tráfico de datos del SCADA

### **En tu instalación conecta:**
- **Inversores fotovoltaicos**
- **Medidores** de campo
- **Estaciones meteorológicas**
- **Relés de protección** (como el ZIV y RED670)
- **UCS-1** (que veo etiquetado en el rack)
- **Cámaras de seguridad**

### **Ventajas operativas:**
- **Punto único** de gestión de comunicaciones
- **Monitoreo centralizado** del estado de enlaces
- **Fácil identificación** de problemas de comunicación
- **Expansión modular** de la red

Este dispositivo es el **corazón** de las comunicaciones de tu planta fotovoltaica, permitiendo que el SCADA pueda supervisar todos los equipos distribuidos en el campo.