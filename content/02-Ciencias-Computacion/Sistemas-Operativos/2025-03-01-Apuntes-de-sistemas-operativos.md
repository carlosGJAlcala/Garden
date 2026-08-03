---
title: "RESUMEN COMPLETO"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
---

# RESUMEN COMPLETO


> **Relacionado**: [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

## **1. GPT vs MBR: Esquema de particiones**

Cuando creamos o administramos discos, podemos usar dos tipos de esquemas de particiones:  
 **MBR (Master Boot Record)**  
 **GPT (GUID Partition Table)**

### ** Diferencias clave:**

|Característica|**MBR**|**GPT**|
|---|---|---|
|**Máximo de particiones**|4 primarias (o 3 + 1 extendida)|128 primarias|
|**Tamaño máximo de disco**|2 TB|Más de 9 ZB|
|**Compatibilidad**|BIOS y sistemas antiguos|UEFI y modernos|
|**Redundancia de datos**| No| Sí (tabla de particiones duplicada)|

### ** Comandos para verificar y cambiar entre MBR/GPT**

1. **Ver el esquema de partición actual**:
    
    ```bash
    sudo parted -l
    ```
    
2. **Convertir un disco a GPT** (️ Borra todo el disco):
    
    ```bash
    sudo parted /dev/sdX mklabel gpt
    ```
    
3. **Convertir un disco a MBR**:
    
    ```bash
    sudo parted /dev/sdX mklabel msdos
    ```
    

 **Si tu PC usa UEFI, usa GPT. Si es BIOS antiguo, usa MBR.**

---

## **2. Creación y gestión de un USB Live con Parrot OS**

Cuando se graba un **USB Live**, el sistema de archivos suele quedar en **ISO9660** (de solo lectura). Esto puede:  Permitir arrancar Parrot OS.  
 Bloquear la escritura en el USB y no usar todo el espacio disponible.

### ** Comandos para verificar el estado del USB**

1. **Ver particiones y sistemas de archivos**:
    
    ```bash
    lsblk -f
    ```
    
2. **Comprobar si el USB está en ISO9660**:
    
    ```bash
    mount | grep iso9660
    ```
    
3. **Ver detalles de las particiones**:
    
    ```bash
    sudo blkid
    ```
    

 **Si el USB está en ISO9660, no podrás escribir en él sin reformatearlo.**

---

## **3. Soluciones para recuperar el espacio del USB**

Si un **USB de 120 GiB solo usa 5 GiB**, es porque:

1. **Está en ISO9660** (modo de solo lectura).
2. **Tiene espacio sin particionar** que no se usa.

### ** Opción 1: Crear una partición sin borrar Parrot OS**

Si el USB tiene **espacio libre**, puedes crear una partición extra sin afectar el sistema Live.

1. **Abrir `parted`**:
    
    ```bash
    sudo parted /dev/sda
    ```
    
2. **Ver el espacio disponible**:
    
    ```bash
    print free
    ```
    
3. **Crear una partición nueva en FAT32 o ext4**:
    
    ```bash
    mkpart primary fat32 5GiB 100%
    ```
    
4. **Formatear la nueva partición**:
    
    ```bash
    sudo mkfs.vfat -F 32 /dev/sda2   # Para FAT32
    sudo mkfs.ext4 /dev/sda2         # Para ext4
    ```
    

 **Esto te permite seguir usando Parrot OS Live y aprovechar el resto del USB.**

---

### ** Opción 2: Borrar el USB y recuperar todo el espacio**

Si el USB está completamente en **ISO9660**, debes **eliminar la tabla de particiones y formatearlo**.

**️ Esto eliminará TODO el contenido del USB.**

1. **Borrar todas las particiones**:
    
    ```bash
    sudo wipefs --all /dev/sda
    sudo dd if=/dev/zero of=/dev/sda bs=1M count=10
    ```
    
2. **Crear una nueva tabla de particiones (GPT o MBR)**:
    
    ```bash
    sudo parted /dev/sda
    mklabel gpt    # Para UEFI
    mklabel msdos  # Para BIOS
    ```
    
3. **Crear una nueva partición y formatearla**:
    
    ```bash
    mkpart primary fat32 1MiB 100%
    sudo mkfs.vfat -F 32 /dev/sda1
    ```
    

 **Ahora el USB puede usarse como almacenamiento normal.**

---

## **4. Creacion de una particion de persistencia en USB Live**

Si quieres que Parrot OS **guarde cambios entre reinicios**, necesitas una partición de **persistencia**.

### ** Pasos para agregar persistencia**

1. **Crear una partición ext4 para la persistencia**:
    
    ```bash
    sudo parted /dev/sda
    mkpart primary ext4 4GiB 100%
    ```
    
2. **Formatear la partición**:
    
    ```bash
    sudo mkfs.ext4 /dev/sda3
    ```
    
3. **Montar la partición y crear `persistence.conf`**:
    
    ```bash
    sudo mkdir /mnt/usb_persistence
    sudo mount /dev/sda3 /mnt/usb_persistence
    echo "/ union" | sudo tee /mnt/usb_persistence/persistence.conf
    sudo umount /mnt/usb_persistence
    ```
    
4. **Reiniciar y seleccionar "Persistence" en el menú de GRUB**.
    

 **Ahora Parrot OS guardará los cambios y no se perderán al apagar.**

---

## **5. Comandos clave explicados**

|Comando|Explicación|
|---|---|
|`lsblk -f`|Muestra dispositivos y sistemas de archivos.|
|`parted -l`|Lista las particiones y tabla de particiones (GPT/MBR).|
|`blkid`|Muestra UUID y sistema de archivos de cada partición.|
|`mount|grep iso9660`|
|`wipefs --all /dev/sda`|Borra todas las firmas de partición en el USB.|
|`dd if=/dev/zero of=/dev/sda bs=1M count=10`|Borra completamente el inicio del USB.|
|`mkfs.vfat -F 32 /dev/sda1`|Formatea una partición en FAT32.|
|`mkfs.ext4 /dev/sda3`|Formatea una partición en ext4.|
|`mount /dev/sda2 /mnt/usb_storage`|Monta una partición manualmente.|

---

# ** CONCLUSIÓN**

 **Si el USB Live tiene espacio libre, puedes crear una nueva partición sin borrar Parrot OS.**  
 **Si el USB está bloqueado en ISO9660, debes eliminar la tabla de particiones y formatearlo.**  
 **Si quieres guardar cambios en Parrot OS Live, necesitas una partición de persistencia en ext4.**  
 **GPT es mejor para UEFI, mientras que MBR es mejor para BIOS Legacy.**

