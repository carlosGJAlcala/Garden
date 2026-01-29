---
title: "Ps"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
El comando `ps aux` en Linux se utiliza para mostrar información detallada sobre todos los procesos que se están ejecutando en el sistema. Vamos a desglosarlo:

### Explicación de `ps aux`


> **Relacionado**: [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

- **`ps`**: Es el comando para mostrar información sobre los procesos en ejecución.
- **`a`**: Muestra los procesos de todos los usuarios, no solo los del usuario actual.
- **`u`**: Muestra información adicional en formato de usuario, como el usuario que ejecuta el proceso y la cantidad de memoria y CPU utilizada.
- **`x`**: Muestra también procesos que no tienen una terminal asociada (procesos en segundo plano, servicios del sistema, etc.).

### Salida de `ps aux`

Cuando ejecutas `ps aux`, obtienes una tabla con las siguientes columnas:

1. **USER**: El usuario que inició el proceso.
2. **PID**: El ID del proceso.
3. **%CPU**: El porcentaje de CPU que está utilizando el proceso.
4. **%MEM**: El porcentaje de memoria física que está usando el proceso.
5. **VSZ**: El tamaño virtual del proceso en kilobytes.
6. **RSS**: La cantidad de memoria residente en kilobytes que el proceso está utilizando (el uso real de memoria).
7. **TTY**: La terminal asociada al proceso. Si el proceso no tiene una terminal asociada, verás un `?`.
8. **STAT**: El estado del proceso:
   - `R`: Ejecutándose (Running).
   - `S`: Durmiendo (Sleeping).
   - `D`: Durmiendo ininterrumpidamente (no se puede interrumpir).
   - `T`: Detenido (Stopped).
   - `Z`: Zombie (un proceso que ha terminado, pero aún no ha sido eliminado).
9. **START**: La hora a la que se inició el proceso.
10. **TIME**: El tiempo total de CPU que ha usado el proceso.
11. **COMMAND**: El comando completo que inició el proceso.

### Ejemplo

```bash
ps aux
```

Este comando puede devolver una salida como esta:

```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  16960  1352 ?        Ss   10:20   0:00 /sbin/init
user       101  0.2  1.5 242484 31520 ?        S    10:22   0:02 /usr/bin/python3 myscript.py
user       200  0.0  0.3 101200  8304 pts/0    Ss   10:25   0:00 /bin/bash
```

### Ejemplo de uso útil

Para encontrar un proceso específico, puedes combinar `ps aux` con `grep`. Por ejemplo, para encontrar todos los procesos que contienen "apache":

```bash
ps aux | grep apache
```

### Otras opciones útiles

- **`ps aux --sort=-%mem`**: Ordena los procesos por el uso de memoria, de mayor a menor.
- **`ps aux --sort=-%cpu`**: Ordena los procesos por el uso de CPU, de mayor a menor.

Este comando es muy útil para monitorear y diagnosticar procesos, revisar el consumo de recursos y entender el estado general del sistema.