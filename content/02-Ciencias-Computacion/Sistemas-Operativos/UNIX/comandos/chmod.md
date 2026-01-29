---
title: "Chmod"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
El comando que mencionas, `chmod -r 600`, tiene como objetivo **cambiar los permisos de archivos y directorios de forma recursiva** en Linux. Sin embargo, hay un error en el uso de la opción. Vamos a desglosar lo que hace cada parte y corregirlo.

### Entendiendo el Comando `chmod -r 600`


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

- **`chmod`**: Es el comando usado para cambiar los permisos de archivos y directorios.
- **`-r`**: La opción `-r` no es válida para `chmod`. El parámetro correcto para aplicar permisos recursivamente es `-R` (con mayúscula).
- **`600`**: Especifica los permisos que queremos aplicar. En este caso:
  - `6` (lectura y escritura) para el **propietario**.
  - `0` (sin permisos) para **grupo** y **otros**.

Entonces, el comando correcto sería:

```bash
chmod -R 600 nombre_directorio
```

### Explicación de `chmod 600`

- **600**:
  - **Propietario**: Permiso de **lectura y escritura** (`rw-`).
  - **Grupo**: Sin permisos (`---`).
  - **Otros**: Sin permisos (`---`).

Esto significa que solo el propietario del archivo o directorio tendrá permisos para leer y escribir. Nadie más podrá acceder.

### Ejemplo Completo

```bash
chmod -R 600 /ruta/del/directorio
```

Este comando aplicará los permisos `600` a todos los archivos y subdirectorios dentro de `/ruta/del/directorio`, y se hará de forma recursiva, de modo que afectará todos los niveles.

### Importante

- **Precaución con directorios**: Si aplicas `600` a un directorio, solo el propietario podrá entrar al directorio y modificar archivos, pero nadie más tendrá acceso.
- **Recomendación**: Normalmente, para directorios, es preferible `700` en lugar de `600`, ya que el permiso de ejecución (`x`) es necesario para abrir y listar el contenido de los directorios.

Por ejemplo, para permitir que el propietario pueda acceder y modificar archivos en el directorio:

```bash
chmod -R 700 /ruta/del/directorio
```

Esto proporciona acceso completo solo al propietario.