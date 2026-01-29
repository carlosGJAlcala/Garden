---
title: "Kiil"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
El comando `kill` en Linux se usa para **terminar** procesos en ejecución. Permite enviar señales a un proceso, siendo la más común la señal `SIGTERM`, que le pide al proceso que termine de manera segura, o `SIGKILL`, que fuerza su finalización.

### Sintaxis Básica de `kill`


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

```bash
kill [señal] PID
```

- **PID**: Es el ID del proceso que quieres terminar. Puedes obtenerlo con `ps aux`, `top`, o `pgrep`.

### Ejemplo Básico

```bash
kill 1234
```

Este comando envía la señal por defecto `SIGTERM` (señal 15) al proceso con el ID 1234, solicitándole que termine.

### Señales Comunes de `kill`

- **SIGTERM (15)**: Es la señal predeterminada, solicita al proceso que termine de forma ordenada. No garantiza que el proceso termine inmediatamente, ya que depende de si el proceso puede manejar esta señal y terminar correctamente.
  
  ```bash
  kill -15 1234
  ```

- **SIGKILL (9)**: Mata el proceso inmediatamente sin darle la oportunidad de realizar limpieza o liberación de recursos. Úsalo solo si `SIGTERM` no funciona.

  ```bash
  kill -9 1234
  ```

- **SIGHUP (1)**: Reinicia el proceso. A veces es útil para actualizar la configuración de un servicio sin detenerlo.

  ```bash
  kill -1 1234
  ```

### Otros Comandos Relacionados

- **`pkill`**: Mata procesos por nombre en lugar de por PID.

  ```bash
  pkill nombre_proceso
  ```

- **`killall`**: Mata todos los procesos con el nombre especificado.

  ```bash
  killall nombre_proceso
  ```

- **`xkill`**: En sistemas con interfaz gráfica, permite cerrar aplicaciones gráficas haciendo clic en la ventana.

### Ejemplo Completo

1. Encuentra el PID del proceso con `ps aux` o `pgrep`.

   ```bash
   ps aux | grep nombre_proceso
   ```

2. Mata el proceso.

   ```bash
   kill -9 1234
   ```

> ️ **Precaución**: Utilizar `kill -9` puede causar pérdida de datos o estados no guardados, así que úsalo solo si es necesario.