---
title: "Arquitectura de Detección y Análisis de Ataques"
date: 2026-01-26
tags:
  - ciberseguridad
  - analisis-datos
---

# **Arquitectura de Detección y Análisis de Ataques**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/PFSENSE|PFSENSE]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[03-Desarrollo-Software/Bases-Datos/MongoDB|MongoDB]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

## **Componentes Principales**

### **Subsistemas de la Arquitectura**

1. **Subsistema de Detección de Eventos de Ataque (DEA)**
    
    - Responsable de identificar eventos sospechosos en la red.
2. **Subsistema de Modelado y Análisis de Patrones de Ataque (MAP)**
    
    - Analiza los eventos detectados y modela patrones de ataque.
3. **Subsistema de Visualización de Patrones de Ataque (VIAPA)**
    
    - Presenta visualmente los patrones identificados para facilitar su interpretación.

### **Infraestructura de la Honynet**

Para detectar y analizar ataques, se despliega una **honynet** con los siguientes elementos:

- **Honeypot T-Pot:** Captura tráfico malicioso y eventos de ataque.
- **SIEM Splunk:** Recibe los datos del honeypot para su correlación y análisis.
- **Firewall pfSense:** Controla y monitorea el tráfico de red.
- **EAD (Event Analysis and Detection):** Sistema de análisis de eventos con las siguientes tecnologías:
    - **MongoDB y Neo4j:** Bases de datos para almacenamiento y análisis de datos.
- **Jump Host:** Servidor intermedio (_bastion host_) que permite saltar entre redes. Se despliega como máquina virtual.
- **Neo4j:** Se utiliza para la representación y análisis de relaciones entre eventos, con cifrado aplicado para la seguridad de los datos.

---

## **Herramientas y Tecnologías Adicionales**

### **Simulación y Generación de Ataques**

- **Herramienta IDT o ID2T:** Se utiliza para generar ataques simulados y evaluar la respuesta del sistema.
- Se prioriza la simulación de ataques más fáciles de reproducir.

### **Bots en la Red**

- Los bots funcionan enviando _pings_ por toda la red para detectar hosts activos y mapear la infraestructura.

### **Plataformas y Software Utilizado**

- **Splunk MLKT:** Framework de aprendizaje automático para correlación de eventos.
- **MobXterm:** Herramienta para acceso remoto y administración de sistemas.
- **Base de datos Studio3:** Software para la gestión de bases de datos.

### **Análisis de Métricas en Splunk**

- **Jupyter Notebook:** Splunk permite la integración con Jupyter para análisis avanzado de datos.
- **Métricas más relevantes:**
    - _Accuracy_ (precisión del modelo).
    - _Área bajo la curva (AUC-ROC)_ o _F-score_ en caso de datos desbalanceados.

---

## **Otras Consideraciones**

- **Taxonomía CAPEC:** Se emplea para clasificar los ataques detectados en la red.
- **Beca INTA:** Posible relación con el proyecto de investigación o desarrollo en el Instituto Nacional de Técnica Aeroespacial (INTA).
- **Usuarios de contacto:**
    - [pdiagar@inta.es](mailto:pdiagar@inta.es)
    - [dlopabr@inta.es](mailto:dlopabr@inta.es)

