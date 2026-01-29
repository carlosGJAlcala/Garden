---
title: "The Linux Command Line"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
## Contenido


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

- [El Intérprete de Línea de Comandos](#el-int%C3%A9rprete-de-l%C3%ADnea-de-comandos)
- [Cómo Obtener Ayuda](#c%C3%B3mo-obtener-ayuda)
- [El Sistema de Archivos](#el-sistema-de-archivos)
- [Navegación en el Sistema de Archivos](#navegaci%C3%B3n-en-el-sistema-de-archivos)
- [Manipulación de Archivos y Directorios](#manipulaci%C3%B3n-de-archivos-y-directorios)
- [Permisos de Acceso](#permisos-de-acceso)
- [Trabajando con Comandos](#trabajando-con-comandos)
- [Control de Trabajos](#control-de-trabajos)
- [Entrada/Salida](#entradasalida)
- [Redirecciones y Tuberías](#redirecciones-y-tuber%C3%ADas)
- [Ejercicios Propuestos](#ejercicios-propuestos)

---

## El Intérprete de Línea de Comandos

- Es un programa que permite lanzar comandos para que el sistema operativo los ejecute.
- Ejemplos de comandos: `date`, `cal`, `df`, `exit`.
- Mantiene un historial de comandos y permite autocompletado con la tecla `TAB`.

## Cómo Obtener Ayuda

- Usa `man` para obtener ayuda de comandos:

 `$ man df`
 
 ## El Sistema de Archivos

- El árbol de directorios empieza en `/`, con directorios como `/boot`, `/etc`, `/bin`, `/usr`, `/home`, `/root`, `/dev`, `/proc`, `/mnt`, `/var`, y `/tmp`.
- El directorio de inicio (`~`) es donde un usuario comienza su sesión, usualmente `/home/usuario`.

## Navegación en el Sistema de Archivos

- Cambiar de directorio:
    
    bash
    

    
    `$ cd /ruta/absoluta $ cd ../ruta/relativa`
    
- Visualizar el directorio actual:
    
    bash
    
    
    `$ pwd`
    
- Listar archivos:
    
    bash
    
    
    `$ ls -a     # Archivos ocultos $ ls -l     # Vista detallada`
    

## Manipulación de Archivos y Directorios

- Comandos básicos:
    
    bash
    
    Copiar código
    
    `$ cp archivo1 archivo2    # Copiar archivo $ mkdir directorio        # Crear directorio $ rm archivo              # Eliminar archivo $ rmdir directorio        # Eliminar directorio vacío $ mv archivo destino      # Mover o renombrar archivo`
    
- Inspección de archivos:
    
    bash
    
    Copiar código
    
    `$ file archivo            # Tipo de archivo $ cat archivo             # Contenido completo $ less archivo            # Navegación en contenido`
    
- Enlaces:
    
    bash
    
    Copiar código
    
    `$ ln archivo enlace_fuerte       # Enlace fuerte $ ln -s archivo enlace_simbolico # Enlace simbólico`
    

## Permisos de Acceso

- Cambiar permisos de archivo:
    
    bash
    
    Copiar código
    
    `$ chmod 755 archivo`
    
- Visualización de permisos y tipos:
    
    bash
    
    Copiar código
    
    `$ ls -l`
    

## Trabajando con Comandos

- Tipos de comandos:
    - Archivos ejecutables.
    - Comandos internos.
    - Scripts y aliases.
- Ejecución en segundo plano:
    
    bash
    
    Copiar código
    
    `$ comando &`
    
- Gestión de trabajos:
    
    bash
    
    Copiar código
    $ jobs      # Mostrar trabajos en segundo plano 
    $ fg %1     # Llevar trabajo al primer plano 
    $ bg %1     # Enviar trabajo al fondo``
    

## Entrada/Salida

- Redirección de entrada:
    
    bash
    
    Copiar código
    
    `$ comando < archivo`
    
- Redirección de salida y errores:
    
    bash
    
    Copiar código
    
    `$ comando > salida.txt $ comando 2> errores.txt`
    
- Uso de tuberías:
    
    bash
    
    Copiar código
    
    `$ ls | wc -l`
    

## Ejercicios Propuestos

1. Mostrar la fecha en formato `dd-mm-aaaa`.
2. Copiar `/etc/passwd` al directorio actual usando rutas absolutas y relativas.
3. Guardar el espacio de disco actual en un archivo con el nombre `diskreport-{mes}-{día}-{hora}-{min}-{sec}`.
4. Contar el número de imágenes en `https://www.uah.es` usando `curl`, `grep`, y `wc`.

## Bibliografía

- Sánchez Prieto, S., & García Población, Ó. _Unix y Linux, guía práctica_. Ra-Ma, 3ra Ed., 2004.
- [The Linux Command Line](http://linuxcommand.org/lc3_learning_the_shell.php)