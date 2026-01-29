---
title: "Técnicas de Ocultación y Manipulación en Seguridad Informática"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
# Técnicas de Ocultación y Manipulación en Seguridad Informática**


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/GanarAcceso/Rootkits|Rootkits]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

Los **rootkits** y el **hooking** son técnicas avanzadas utilizadas tanto por atacantes para mantener el control sobre un sistema comprometido como por herramientas de seguridad para monitorear actividades maliciosas.

---

## **1. ¿Qué es un Rootkit?**

Un **rootkit** es un tipo de software malicioso diseñado para **ocultarse en un sistema** y permitir el acceso persistente a un atacante. Su principal objetivo es **evadir la detección** de antivirus y herramientas de seguridad, garantizando control remoto sobre el sistema infectado.

### **Características de un Rootkit**

- **Oculta procesos, archivos y conexiones de red.**
- **Puede ejecutarse en espacio de usuario o de kernel.**
- **Es persistente**: Sobrevive reinicios del sistema y actualizaciones.
- **Puede deshabilitar herramientas de seguridad** (antivirus, firewalls).
- **Se instala mediante exploits, phishing o descargas maliciosas.**

---

## **2. Tipos de Rootkits**

### **1️⃣ Rootkits de Espacio de Usuario (User-mode, Ring 3)**

- Se ejecutan en **modo usuario** y modifican procesos normales del sistema.
- Utilizan técnicas como **DLL Injection y API Hooking** para ocultar su presencia.
- Son más fáciles de detectar porque operan con privilegios limitados.

Ejemplo: **Rootkit Hacker Defender**, que oculta procesos y conexiones en Windows.

### **2️⃣ Rootkits de Espacio de Kernel (Kernel-mode, Ring 0)**

- Se ejecutan con privilegios elevados en el **kernel del sistema operativo**.
- Pueden modificar estructuras internas como la **System Call Table**.
- Son más peligrosos porque pueden desactivar antivirus y firewalls.

Ejemplo: **Rootkit FU** en Windows, que oculta procesos modificando estructuras del kernel.

### **3️⃣ Rootkits de Firmware (BIOS/UEFI Rootkits)**

- Se instalan en el **firmware de la placa base o discos duros**.
- Persisten incluso tras formatear el disco y reinstalar el sistema operativo.
- Muy difíciles de detectar y eliminar.

Ejemplo: **LoJax**, el primer rootkit detectado en el firmware UEFI.

### **4️⃣ Rootkits de Modo Virtualización (Hypervisor Rootkits)**

- Se ejecutan en un nivel más bajo que el sistema operativo.
- Pueden interceptar y modificar todas las instrucciones del sistema.

Ejemplo: **Blue Pill**, un rootkit basado en virtualización para Windows.

---

## **3. Hooking: Manipulación de Llamadas del Sistema**

El **hooking** es una técnica utilizada tanto por **malware** como por herramientas de seguridad para interceptar y modificar el comportamiento de un sistema operativo o aplicación.

### **Tipos de Hooking**

### **1️⃣ API Hooking**

- Consiste en modificar funciones del sistema para alterar su ejecución.
- Se usa para ocultar procesos, archivos y conexiones de red.
- Se implementa con técnicas como **IAT Hooking y Detours** en Windows.

Ejemplo en Windows:

```cpp
BOOL WINAPI HookedCreateFile(LPCTSTR lpFileName, DWORD dwDesiredAccess, DWORD dwShareMode, LPSECURITY_ATTRIBUTES lpSecurityAttributes, DWORD dwCreationDisposition, DWORD dwFlagsAndAttributes, HANDLE hTemplateFile) {
    if (strstr(lpFileName, "malware.exe")) {
        SetLastError(ERROR_ACCESS_DENIED);
        return INVALID_HANDLE_VALUE;
    }
    return OriginalCreateFile(lpFileName, dwDesiredAccess, dwShareMode, lpSecurityAttributes, dwCreationDisposition, dwFlagsAndAttributes, hTemplateFile);
}
```

Este código modifica la API `CreateFile` para impedir que el sistema abra ciertos archivos.

### **2️⃣ System Call Hooking**

- Se usa en rootkits de kernel para modificar la **System Call Table**.
- Permite ocultar procesos, archivos y conexiones de red al modificar llamadas como `sys_open` o `sys_read`.

Ejemplo en Linux:

```c
asmlinkage int (*original_sys_open)(const char __user *, int, int);

asmlinkage int hooked_sys_open(const char __user *filename, int flags, int mode) {
    if (strstr(filename, "archivo_secreto")) {
        return -1;  // Evita la apertura del archivo
    }
    return original_sys_open(filename, flags, mode);
}
```

Este código intercepta `sys_open` para evitar la apertura de un archivo específico.

### **3️⃣ Inline Hooking**

- Modifica directamente el código en memoria de una función.
- Se usa en **malware avanzado y herramientas de seguridad**.

Ejemplo: Un keylogger puede **hookear GetAsyncKeyState** en Windows para capturar pulsaciones de teclas.

---

## **4. Diferencias entre Rootkit y Hooking**

|**Característica**|**Rootkit**|**Hooking**|
|---|---|---|
|**Objetivo**|Ocultar presencia y mantener persistencia|Interceptar y modificar llamadas de sistema|
|**Nivel de ejecución**|Puede ser en espacio de usuario o kernel|Puede ser en APIs o llamadas del sistema|
|**Uso principal**|Malware, persistencia, evasión de antivirus|Seguridad, depuración, modificación de software|
|**Ejemplo de uso malicioso**|Rootkit que oculta procesos de un malware|Keylogger que intercepta pulsaciones de teclas|

---

## **5. Cómo Detectar y Eliminar Rootkits y Hooking**

### **1️⃣ Herramientas de Detección de Rootkits**

- **Chkrootkit** (Linux):
    
    ```bash
    sudo apt install chkrootkit
    sudo chkrootkit
    ```
    
- **rkhunter (Rootkit Hunter)** (Linux):
    
    ```bash
    sudo apt install rkhunter
    sudo rkhunter --check
    ```
    
- **GMER** (Windows): Escanea procesos ocultos y hooks en el kernel.
- **Malwarebytes Anti-Rootkit**: Detecta y elimina rootkits en Windows.

### **2️⃣ Métodos de Eliminación**

- **Modo seguro y escaneo con herramientas especializadas**.
- **Restauración de archivos del sistema** con comandos como `sfc /scannow` en Windows.
- **Reinstalación del sistema operativo** en casos de rootkits persistentes.
- **Actualizar BIOS/UEFI** si el rootkit se encuentra en el firmware.

---

## **6. Conclusión**

- **Rootkits** son herramientas avanzadas de persistencia utilizadas por atacantes para ocultarse en un sistema.
- **Hooking** es una técnica de modificación de llamadas de sistema, utilizada tanto en ataques como en herramientas de seguridad.
- **Los rootkits de kernel y firmware son los más difíciles de detectar y eliminar**.
- **Usar herramientas de seguridad y mantener el sistema actualizado** es clave para prevenir infecciones.

Rootkits y hooking son técnicas poderosas que pueden usarse tanto para el **cibercrimen como para la seguridad informática**. Entender su funcionamiento es fundamental para proteger los sistemas frente a ataques avanzados.