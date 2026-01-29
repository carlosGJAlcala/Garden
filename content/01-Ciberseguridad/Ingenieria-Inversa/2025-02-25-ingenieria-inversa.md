---
title: "2025 02 25 Ingenieria Inversa"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---

### **Herramientas para Análisis de Binarios en Windows**


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

#### **Wrestool: Extracción de Recursos en Binarios de Windows**

`wrestool` es una herramienta que permite extraer recursos de binarios de Windows, como iconos, imágenes y otros elementos embebidos en archivos `.exe` o `.dll`.

 Instalación en Linux (Debian/Ubuntu):

```bash
sudo apt install icoutils
```

 Uso básico para extraer iconos de un ejecutable:

```bash
wrestool -x --output-dir=./icons archivo.exe
```

---

### **Bilkwak: Análisis de Binarios Empaquetados**

`bilkwak` es una herramienta que permite visualizar la información de binarios empaquetados, útil para detectar _packers_ o compresiones en archivos ejecutables.

---

### **Evasión de Análisis: Dificultar el Rastreo**

Una técnica utilizada en la cibercriminalidad consiste en **dificultar el seguimiento de transacciones** mediante el uso de múltiples monederos de criptomonedas.  
Esto complica la trazabilidad de fondos ilícitos, especialmente en esquemas de **blanqueo de dinero** o _ransomware_.

---

### **Vacunas para Malware: Bloqueo con Mutex**

Una estrategia para generar **vacunas contra malware** consiste en analizar las condiciones utilizadas por el código malicioso para ejecutarse.

 **Uso de Mutex como condición de ejecución**  
Muchos malware utilizan **mutex** para asegurarse de que solo una instancia del programa se ejecute a la vez.  
Si creamos **manualmente** un mutex con el mismo nombre antes de que el malware se ejecute, este podría **abortar su ejecución**.

Ejemplo de creación de un mutex en Windows con PowerShell:

```powershell
[System.Threading.Mutex]::new($false, "NombreDelMutex")
```

Este método es útil para impedir la ejecución de malware que dependa de un mutex específico.

---

### **Estado Actual del Análisis (Current Status)**

- Se tiene la **muestra original** del malware.
- Se ha identificado una **URL que el malware consulta** para verificar si está activa.
- Existe la posibilidad de que el malware **se haya filtrado fuera del laboratorio**, si ha sido ejecutado en un entorno con conexión a Internet.

---

### **Creación de Servicios Maliciosos**

El malware puede registrar un servicio en Windows para **mantener persistencia**.  
Ejemplo de un servicio que puede ser creado por un malware:

```powershell
sc create msecsvc binPath= "C:\ruta\malicioso.exe" start= auto
```

Este comando crea un servicio llamado `msecsvc` que se ejecutará automáticamente en cada inicio de Windows.

---

### **Contraseñas en Binarios**

En algunos casos, la **contraseña para descomprimir un archivo** puede estar embebida dentro del binario.  
Para extraer información sensible, se pueden utilizar herramientas como:

- **`strings`** (en Linux) para buscar texto en binarios:
    
    ```bash
    strings archivo.bin | grep "password"
    ```
    
- **`rabin2` (radare2)**
    
    ```bash
    rabin2 -z archivo.exe
    ```
    
- **Análisis con `Ghidra` o `IDA Pro`** para extraer cadenas codificadas.
