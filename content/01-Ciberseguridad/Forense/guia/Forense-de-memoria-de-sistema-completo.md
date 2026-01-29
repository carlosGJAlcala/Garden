---
title: "Forense De Memoria De Sistema Completo"
date: 2025-01-01
tags:
  - ciberseguridad
---

## **Forense de memoria de sistema completo**

El análisis forense de memoria permite inspeccionar el estado **completo** de un sistema en un momento dado: procesos, código cargado, conexiones de red, artefactos de malware y objetos de sincronización como mutex o pipes. El objetivo es replicar la **visión total** que tendría un programa en ring 0, pero sin escribir uno, usando herramientas ya existentes y seguras.

> **Relacionado**: Ver [[01-Ciberseguridad/Fundamentos/LABORATORIO-2-volatility|Laboratorio Volatility]] para práctica. [[01-Ciberseguridad/Malware/2025-02-24-Formatos-ejecutables-PE-y-ELF|Formatos PE/ELF]] para entender binarios. [[01-Ciberseguridad/Malware/Mutex-nombrados-como-IOC-en-ciberseguridad|Mutex como IOC]].

---

### **1. Adquisición en caliente**

La adquisición “en caliente” (_live memory acquisition_) se realiza con el sistema en ejecución, capturando el contenido de la RAM. Esto preserva:

- Procesos activos.
    
- Datos en memoria volátil.
    
- Conexiones de red abiertas.
    
- Artefactos que desaparecerían en un apagado.
    

**En Linux:**

- **LiME** (_Linux Memory Extractor_): módulo de kernel para volcar memoria a un archivo.
    
    ```bash
    insmod lime.ko "path=/ruta/dump.lime format=lime"
    ```
    
- **AVML** (_Azure Virtual Machine Forensics Tool_): no requiere compilar módulo, ideal para entornos cloud.
    
    ```bash
    sudo avml dump.lime
    ```
    

**En Windows:**

- **WinPMEM** (parte de Rekall): controlador firmado que permite volcar memoria física.
    
    ```cmd
    winpmem.exe --output dump.raw
    ```
    

 **Buenas prácticas**:

- Realizar la adquisición desde un medio confiable (USB con toolkit forense).
    
- Guardar el volcado en un disco externo o almacenamiento seguro.
    
- Documentar fecha, hora y hash del archivo para cadena de custodia.
    

---

### **2. Análisis fuera de línea**

El análisis “offline” evita alterar la máquina original, trabajando sobre una copia del volcado. Esto garantiza integridad y permite repetir análisis.

**Herramientas recomendadas:**

- **Volatility** (versión 2) o **Volatility3** (reescrita en Python 3).
    
- Soportan Windows, Linux y macOS.
    
- Basan su análisis en perfiles de sistema o símbolos para interpretar estructuras de memoria.
    

---

### **3. Ejemplos de análisis con Volatility/Volatility3**

- **Procesos activos**:
    
    ```bash
    volatility3 -f dump.raw windows.pslist
    ```
    
- **Módulos del kernel**:
    
    ```bash
    volatility3 -f dump.raw windows.modules
    ```
    
- **Regiones de memoria mapeadas**:
    
    ```bash
    volatility3 -f dump.raw windows.vadinfo
    ```
    
- **Cadenas de texto**:
    
    ```bash
    volatility3 -f dump.raw strings | grep "keyword"
    ```
    
- **Handles (objetos abiertos por procesos)**:
    
    ```bash
    volatility3 -f dump.raw windows.handles
    ```
    

---

### **4. Relevancia de IOCs de memoria**

Artefactos como:

- **Mutex/Mutants** → identificadores únicos que usa un malware para saber si ya está en ejecución.
    
- **Secciones** → regiones de memoria compartida entre procesos.
    
- **Pipes con nombre** → canales de comunicación internos que un malware puede usar para C2.
    
- **DLLs inyectadas** → bibliotecas cargadas que no forman parte del binario original.
    

Estos IOCs son **potentes** porque:

- No dependen de archivos en disco.
    
- Pueden identificar familias de malware aunque cambien su hash o empaquetado.
    
- Son detectables incluso si el malware intenta ocultar su presencia en el sistema de archivos.
    

---

### **5. Flujo de trabajo recomendado**

1. **Preparar herramienta y medio** para adquisición (LiME, AVML, WinPMEM).
    
2. **Capturar memoria** y verificar integridad con hash.
    
3. **Transferir volcado** a un entorno de análisis (máquina forense).
    
4. **Analizar con Volatility/Volatility3**, siguiendo un checklist (procesos, módulos, conexiones, handles, strings).
    
5. **Documentar hallazgos**, extrayendo IOCs relevantes para reportar o alimentar una plataforma de Threat Intelligence.
    

---
