---
title: "Shred"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
El comando **`shred`** es una utilidad de línea de comandos en sistemas **Linux/Unix** que se utiliza para sobrescribir repetidamente un archivo con datos aleatorios antes de eliminarlo, con el propósito de dificultar (o imposibilitar) la recuperación de los datos eliminados mediante técnicas de recuperación forense.

### Sintaxis básica


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

```bash
shred [opciones] <archivo>
```

### ¿Cómo funciona?

1. **Sobrescritura**:
    
    - `shred` sobrescribe el contenido del archivo varias veces con datos aleatorios. Esto evita que herramientas de recuperación de datos puedan reconstruir los datos originales.
2. **Eliminación opcional**:
    
    - Después de sobrescribir, `shred` puede eliminar el archivo si se especifica la opción correspondiente.
3. **Reemplazo seguro**:
    
    - El proceso asegura que los bloques de datos en disco sean alterados, incluso en sistemas de archivos tradicionales.

### Opciones comunes

|**Opción**|**Descripción**|
|---|---|
|`-f`|Fuerza los permisos de escritura si es necesario para sobrescribir el archivo.|
|`-n N`|Realiza **N** pasadas (sobrescrituras) en lugar de las 3 por defecto.|
|`-u`|Después de sobrescribir, elimina el archivo (unlink).|
|`-v`|Muestra detalles (modo verboso) del progreso de sobrescritura.|
|`-z`|Sobrescribe con ceros al final, para que no parezca que el archivo ha sido manipulado.|

### Ejemplos de uso

1. **Sobrescribir un archivo con valores aleatorios (por defecto 3 pasadas)**:
    
    ```bash
    shred archivo.txt
    ```
    
2. **Sobrescribir y eliminar un archivo de forma segura**:
    
    ```bash
    shred -u archivo.txt
    ```
    
3. **Personalizar el número de sobrescrituras (5 pasadas)**:
    
    ```bash
    shred -n 5 archivo.txt
    ```
    
4. **Sobrescribir, eliminar y llenar con ceros en la última pasada**:
    
    ```bash
    shred -u -z archivo.txt
    ```
    
5. **Aplicar `shred` a múltiples archivos**:
    
    ```bash
    shred -u archivo1.txt archivo2.txt archivo3.txt
    ```
    

### Consideraciones importantes

1. **Limitaciones en ciertos sistemas de archivos**:
    
    - En sistemas de archivos modernos, como **ext4**, **btrfs**, o aquellos con soporte para **journaling** o **copia en escritura (COW)**, los datos originales pueden ser mantenidos en otras partes del disco, lo que podría comprometer la seguridad del proceso. Para estos casos, es recomendable utilizar herramientas específicas para limpiar bloques libres o discos enteros.
2. **No garantiza la eliminación en discos SSD**:
    
    - En discos sólidos (SSD), el mapeo lógico a físico realizado por el controlador del SSD puede dificultar que `shred` sobrescriba físicamente los bloques correctos. En estos casos, el comando **`blkdiscard`** o utilidades específicas del fabricante son más efectivas.
3. **No apto para nombres de archivo**:
    
    - `shred` no sobrescribe los nombres de archivo presentes en el sistema de archivos. Para garantizar la eliminación segura de nombres de archivo, considera usar **`wipe`** o técnicas adicionales.

### Resumen

El comando **`shred`** es útil para garantizar la destrucción segura de datos en muchos casos. Sin embargo, su efectividad depende del sistema de archivos y del medio de almacenamiento. En situaciones donde la seguridad total es crítica, considera herramientas complementarias o técnicas de destrucción física.