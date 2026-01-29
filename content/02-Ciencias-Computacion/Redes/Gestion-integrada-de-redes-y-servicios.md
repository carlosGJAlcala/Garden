---
title: "Gestion Integrada De Redes Y Servicios"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
La **gestión integrada de redes y servicios** se centra en la centralización y unificación de las distintas herramientas y protocolos utilizados para la administración de una red. El objetivo de esta práctica es aprender a integrar diversas tecnologías de gestión, como SNMP, Grafana, InfluxDB, Telegraf, Nagios, entre otros, para proporcionar una visión unificada del estado de la red.

### Resumen de la práctica


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Ansible|Ansible]]. [[02-Ciencias-Computacion/Redes/Grafana|Grafana]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/InfluxDB|InfluxDB]].

#### 1. **Introducción**

En entornos complejos, como los de empresas y organismos públicos, los equipos informáticos deben gestionar una variedad de sistemas que a menudo utilizan diferentes protocolos y herramientas de monitorización. Esto puede generar una **dispersión en la supervisión** de la red. Para mitigar este problema, se utilizan herramientas que centralizan la gestión, recolectando datos de todos los sistemas y presentándolos en un único panel. Este proceso facilita el análisis y la reacción ante cualquier incidente.

En esta práctica, se integrarán herramientas de monitorización como **Grafana**, **Nagios**, y **Prometheus** para crear un sistema completo de gestión de redes y servicios.

#### 2. **Objetivo de la práctica**

El propósito es desplegar tres máquinas virtuales utilizando **Ansible** o **Vagrant** y configurar los sistemas de monitoreo. Estas máquinas serán:

- **Servidor de Visualización (Grafana)**: Para visualizar los datos de la red a través de gráficos e interacciones.
    
- **Host1**: Un sistema con SNMPv3 configurado para enviar datos al servidor de monitoreo.
    
- **Host2**: Un sistema con **Nagios** instalado para gestionar y monitorizar servicios.
    

La práctica involucra la instalación y configuración de **Grafana**, **InfluxDB**, **Telegraf**, y **Nagios**, y la integración de estos componentes para centralizar la monitorización y visualización de la red.

#### 3. **Flujo de trabajo y herramientas**

- **Grafana**: Herramienta para visualizar datos de métricas y eventos. Se conecta a **InfluxDB** para almacenar datos de series temporales y generar gráficos interactivos.
    
- **InfluxDB**: Base de datos optimizada para almacenar series temporales, como las métricas de rendimiento de sistemas.
    
- **Telegraf**: Agente que recolecta métricas y eventos de los sistemas monitorizados y los envía a **InfluxDB**.
    
- **Nagios**: Sistema de monitoreo para detectar problemas en la infraestructura de la red y generar alertas.
    

#### 4. **Configuración de la práctica**

La práctica se divide en partes:

- **Parte 1: Sistema Visualizador**: Instalación de **Grafana**, **InfluxDB**, y **Telegraf** en el servidor de visualización. Configuración inicial de Grafana para mostrar métricas locales.
    
- **Parte 2: Host1**: Instalación de **SNMPv3** y **Telegraf** en el host1. Recolección de métricas y su envío al servidor de visualización.
    
- **Parte 3: Host2**: Instalación de **Nagios** en el host2 para monitorizar la red. Integración con el servidor de visualización.
    

#### 5. **Métricas de monitoreo**

Durante la práctica se podrán monitorear diversos parámetros del sistema, como:

- Utilización de **disco**, **memoria**, y **red**.
    
- Monitoreo de eventos de **Syslog**, como fallos de autenticación de usuarios, para generar alertas en el sistema de visualización.
    

### Herramientas utilizadas

1. **Grafana**:
    
    - Es una plataforma de visualización que permite crear **dashboards interactivos**. Se conecta con bases de datos como **InfluxDB** para mostrar las métricas en gráficos y alertas. En esta práctica, se configura para mostrar datos recolectados de los sistemas.
        
2. **InfluxDB**:
    
    - Base de datos diseñada para manejar **series temporales**. Almacena métricas de monitoreo que luego son visualizadas en Grafana.
        
3. **Telegraf**:
    
    - Es un agente de recolección de datos que obtiene métricas de sistemas y aplicaciones, y las envía a **InfluxDB**. En esta práctica, Telegraf se configura para recopilar métricas como uso de CPU, memoria, y red.
        
4. **Nagios**:
    
    - Herramienta de **monitorización de red** que permite detectar fallos o anomalías en los sistemas y servicios. En esta práctica, se utiliza para monitorizar el estado de los sistemas y generar alertas.
        

### Configuración y despliegue

El proceso de configuración de la infraestructura de la práctica se lleva a cabo usando **Ansible** o **Vagrant**, que facilita la creación y gestión de máquinas virtuales de manera automatizada.

1. **Acceso de los servidores web**: Para permitir el acceso a los servidores desde el host, es necesario configurar una red privada en **Vagrant**.
    
2. **Instalación y configuración de Grafana**: Grafana se instala en el servidor de visualización para mostrar métricas y alarmas de los sistemas monitorizados.
    
3. **Configuración de SNMPv3 en Host1**: El host1 se configura con **SNMPv3** y **Telegraf** para enviar métricas a **InfluxDB**.
    
4. **Integración de Nagios en Host2**: **Nagios** se instala para monitorear los servicios y sistemas de la red, y se configura para enviar métricas al servidor central.
    

### Conclusión

Esta práctica tiene como objetivo integrar distintas herramientas de gestión y monitorización de red en un entorno unificado, utilizando **Grafana**, **InfluxDB**, **Telegraf**, y **Nagios**. El uso de herramientas como **Vagrant** o **Ansible** para automatizar el despliegue y la configuración de los sistemas ayuda a gestionar infraestructuras más grandes y complejas de manera eficiente. Al final de la práctica, los participantes habrán implementado un sistema completo de monitoreo y visualización de red que incluye métricas de rendimiento y alertas en tiempo real.