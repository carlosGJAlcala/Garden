---
title: "2025 03 10 Ingeneria Inversa"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
Aquí tienes una versión expandida con más detalles sobre cómo afectan los cambios en los binarios y cómo solucionarlos en Windows, Linux y macOS.

---

## **Windows (PE - Portable Executable)**


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

El formato PE (Portable Executable) se usa en Windows para archivos **EXE, DLL y SYS**. Su cabecera incluye información crítica como el tamaño del binario y un checksum opcional.

### **¿Dónde se define el tamaño del binario?**

- **`SizeOfImage` (Offset `0x50` en la cabecera PE/NT)**
    - Define el tamaño total del binario en memoria.
    - Si modificas el tamaño del binario pero no actualizas este valor, el sistema operativo puede rechazar la ejecución o producir errores en el mapeo de memoria.
- **`SizeOfHeaders` (Offset `0x54`)**
    - Indica el tamaño de todas las cabeceras combinadas.
    - Si el binario tiene nuevas secciones añadidas, esta sección debe actualizarse.

### **¿El PE usa checksum?**

- Sí, tiene un campo **`CheckSum` (Offset `0x58`)**.
- En la mayoría de los casos, **Windows ignora este checksum**, excepto en archivos de sistema críticos o controladores (`.sys`).
- Si necesitas recalcularlo, puedes usar:
    
    ```bash
    signtool /verify /dump binary.exe
    ```
    
    O herramientas como **PEChecksum**, **PE-bear** o **LIEF**.

### **¿Cómo solucionar problemas tras modificar un PE?**

1. **Si solo cambias instrucciones del mismo tamaño**, el binario debería seguir funcionando sin problemas.
2. **Si agregas código nuevo**, debes:
    - Buscar espacios libres en el binario (rellenos de `NOPs`).
    - Añadir una nueva sección con herramientas como `PE-bear`.
    - Actualizar `SizeOfImage` si el binario crece.
3. **Si Windows bloquea el binario por el checksum**, usa `LIEF` para recalcularlo.

---

## **Linux (ELF - Executable and Linkable Format)**

El formato **ELF** se usa en Linux para **binarios ejecutables, bibliotecas compartidas (`.so`) y módulos del kernel**.

### **¿Dónde se define el tamaño del binario?**

- **`p_filesz` y `p_memsz` en la tabla de segmentos (Program Header)**
    
    - `p_filesz`: Tamaño en disco del segmento.
    - `p_memsz`: Tamaño en memoria del segmento.
    - Si agregas código y no actualizas `p_filesz`, la parte extra puede ser ignorada al cargar el binario.
- **`e_shoff` y `e_shentsize * e_shnum`**
    
    - `e_shoff`: Indica la posición de la tabla de secciones.
    - `e_shentsize * e_shnum`: Define cuántas secciones tiene el ELF y su tamaño total.
    - Si modificas las secciones, estos valores deben actualizarse.

### **¿El ELF usa checksum?**

- **No tiene checksum obligatorio**, pero algunas distribuciones usan `strip` o `.gnu_debuglink` para detectar cambios.
- En kernels o binarios protegidos, herramientas como **SELinux o AppArmor** pueden detectar modificaciones.

### **¿Cómo solucionar problemas tras modificar un ELF?**

1. **Si solo cambias bytes del mismo tamaño, no hay problema.**
2. **Si agregas código, debes:**
    - Modificar `p_filesz` para reflejar el nuevo tamaño.
    - Asegurar que las secciones tengan el tamaño adecuado en `e_shoff`.
3. **Para modificar ELF de forma segura, usa `readelf` o `elfedit`**:
    
    ```bash
    readelf -l binary
    elfedit --output-type binary
    ```
    

---

## **macOS (Mach-O)**

El formato **Mach-O** se usa en macOS e iOS para **ejecutables, bibliotecas (`.dylib`) y binarios del kernel**.

### **¿Dónde se define el tamaño del binario?**

- **`__TEXT` y `__DATA` en la Load Command**
    - Estas secciones indican el tamaño del código y los datos en memoria.
    - Si modificas el código, debes actualizar estos valores.
- **LC_SEGMENT_64.nsects**
    - Define cuántas secciones tiene el binario.
    - Si agregas código, debes modificar este valor.

### **¿El Mach-O usa checksum?**

- No tiene checksum obligatorio, **pero requiere firma (`codesign`)**.
- Si editas un binario sin actualizar la firma, macOS puede bloquear su ejecución con errores como:
    
    ```
    code signature invalid
    ```
    

### **¿Cómo solucionar problemas tras modificar un Mach-O?**

1. **Si cambias instrucciones del mismo tamaño, no hay problema.**
2. **Si agregas código nuevo, debes:**
    - Ajustar `__TEXT` y `__DATA`.
    - Modificar `LC_SEGMENT_64.nsects` si creaste una nueva sección.
3. **Si macOS bloquea el binario, puedes eliminar la firma con:**
    
    ```bash
    sudo codesign --remove-signature binary
    ```
    

---

## **Conclusión**

Si modificas un binario, debes tener en cuenta:

- **Windows (PE)**: Debes actualizar `SizeOfImage` y, si es necesario, recalcular el checksum.
- **Linux (ELF)**: Si cambias el tamaño, modifica `p_filesz` y `p_memsz`.
- **macOS (Mach-O)**: Actualiza `__TEXT`, `__DATA` y elimina la firma si es necesario.

Si solo cambias bytes sin alterar el tamaño, el binario debería seguir funcionando. Pero si agregas código nuevo, necesitas ajustar la estructura para evitar fallos.