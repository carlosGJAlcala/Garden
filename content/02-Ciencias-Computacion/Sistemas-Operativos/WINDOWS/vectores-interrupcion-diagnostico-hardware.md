---
title: "Vectores de Interrupción y Diagnóstico de Hardware en Windows"
description: "Guía técnica profunda sobre IRQ, buses I2C, drivers y diagnóstico de fallos de arranque"
date: 2025-01-17
tags:
  - hardware
  - windows
  - drivers
  - interrupciones
  - i2c
  - bios
  - diagnóstico
  - cybersecurity
aliases:
  - IRQ
  - Vector de Interrupción
  - I2C
  - Serial IO
draft: false
---

# Vectores de Interrupción y Diagnóstico de Hardware en Windows


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

Esta nota documenta un caso real de diagnóstico donde un técnico "solucionó" un problema de pantalla negra deshabilitando el touchpad, alegando un conflicto de **vector de interrupción**. Analizo la arquitectura subyacente para entender qué ocurrió realmente y por qué la "solución" fue una chapuza.

---

## Arquitectura del Sistema de Interrupciones

### Qué es una interrupción (IRQ)

El procesador no puede estar preguntando constantemente a cada dispositivo si tiene datos. En su lugar, los dispositivos **interrumpen** al procesador cuando necesitan atención. Este mecanismo se llama **IRQ** (Interrupt Request).

```
┌─────────────────┐
│   Dispositivo   │
│ (touchpad, USB) │
└────────┬────────┘
         │ Señal IRQ
         ▼
┌─────────────────┐
│      APIC       │
│  (Controlador   │
│ de Interrupciones)│
└────────┬────────┘
         │ Interrupción
         ▼
┌─────────────────┐
│       CPU       │
│                 │
└────────┬────────┘
         │ Consulta IDT
         ▼
┌─────────────────┐
│  Vector de      │
│  Interrupción   │
│     (IDT)       │
└────────┬────────┘
         │ Salta a ISR
         ▼
┌─────────────────┐
│      Driver     │
│  (Rutina ISR)   │
└─────────────────┘
```

> [!info] IDT - Interrupt Descriptor Table
> Es una tabla que mapea cada número de interrupción a la dirección de memoria donde está el código (ISR - Interrupt Service Routine) que debe ejecutarse. Si dos dispositivos comparten el mismo vector y sus drivers no están preparados para compartirlo, el sistema se cuelga.

### Tipos de interrupciones

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Hardware (IRQ)** | Generadas por dispositivos físicos | Teclado, ratón, disco |
| **Software (INT)** | Generadas por instrucciones del programa | Llamadas al sistema |
| **Excepciones** | Errores del procesador | División por cero, page fault |

### APIC vs PIC

Los sistemas modernos usan **APIC** (Advanced Programmable Interrupt Controller) en lugar del antiguo PIC de 8 líneas:

```
PIC Legacy (8259):
- Solo 15 IRQs disponibles
- Sin soporte multicore
- Conflictos frecuentes

APIC Moderno:
- 256 vectores de interrupción
- Soporte SMP (múltiples cores)
- MSI/MSI-X para PCIe
- Gestión dinámica de IRQs
```

> [!warning] Conflicto de IRQ
> Aunque APIC permite compartir interrupciones, algunos drivers legacy o mal escritos no manejan correctamente el sharing. Cuando dos dispositivos disparan la misma IRQ y un driver no la "libera" correctamente, el sistema puede entrar en un **IRQ storm** (interrupciones infinitas que saturan la CPU).

---

## El Bus I2C y los Touchpads

### Qué es I2C

**I2C** (Inter-Integrated Circuit) es un bus de comunicación serie de baja velocidad que usa solo dos líneas:

| Línea | Función |
|-------|---------|
| **SDA** | Serial Data (datos) |
| **SCL** | Serial Clock (reloj) |

Se usa para dispositivos que no necesitan mucho ancho de banda: touchpads, sensores de temperatura, control de batería, controladores de retroiluminación, etc.

### Arquitectura del touchpad en un portátil

```
┌──────────┐    ┌─────────────────┐    ┌───────────┐    ┌────────────┐
│   CPU    │◄──►│ Intel Serial IO │◄──►│  Bus I2C  │◄──►│  Touchpad  │
│          │    │   Controller    │    │           │    │ ELAN/Synap │
└──────────┘    └─────────────────┘    └───────────┘    └────────────┘
```

> [!important] Cadena de dependencias
> Para que el touchpad funcione, **todos** estos componentes deben estar operativos:
> 
> 1. **ACPI** - Gestión de energía y enumeración de hardware
> 2. **Intel Chipset Driver** - Comunicación básica con el chipset
> 3. **Intel Serial IO Driver** - Controlador del bus I2C
> 4. **Driver HID I2C** - Driver genérico de Windows para dispositivos I2C
> 5. **Driver específico** - Synaptics o ELAN con funcionalidad completa
> 
> Si cualquier eslabón falla, el touchpad no funciona o funciona parcialmente.

### Por qué el driver genérico no sirve

Windows detecta el dispositivo I2C y carga el driver genérico **"HID I2C Device"**. Pero este driver solo sabe:

- Hay un dispositivo I2C en la dirección X
- Cumple el estándar HID (Human Interface Device)

**No sabe:**
- Resolución del touchpad
- Número de dedos soportados
- Gestos disponibles
- Cómo interpretar los datos raw

El driver de Synaptics/ELAN tiene toda esa información específica del modelo.

---

## Secuencia de Arranque de Windows

### Fases del arranque

```
┌─────────────────────────────────────────────────────────┐
│ 1. POST (BIOS/UEFI)                                     │
│    - Inicialización de hardware básico                  │
│    - Carga del bootloader                               │
├─────────────────────────────────────────────────────────┤
│ 2. Windows Boot Manager                                 │
│    - Selección del SO                                   │
│    - Carga de winload.exe                               │
├─────────────────────────────────────────────────────────┤
│ 3. Kernel (ntoskrnl.exe)                                │
│    - Inicialización del kernel                          │
│    - Carga del HAL                                      │
├─────────────────────────────────────────────────────────┤
│ 4. Drivers BOOT_START                                   │
│    - Drivers críticos para el arranque                  │
│    - Controladores de disco, filesystem                 │
├─────────────────────────────────────────────────────────┤
│ 5. Drivers SYSTEM_START  ◄─── AQUÍ SE PRODUCE EL FALLO │
│    - Drivers de hardware secundario                     │
│    - Serial IO, touchpad, audio...                      │
├─────────────────────────────────────────────────────────┤
│ 6. Servicios                                            │
│    - Session Manager                                    │
│    - Servicios de Windows                               │
├─────────────────────────────────────────────────────────┤
│ 7. Winlogon y escritorio                                │
│    - Pantalla de login                                  │
│    - Shell de usuario                                   │
└─────────────────────────────────────────────────────────┘
```

### Start Types de los drivers

Los drivers tienen un valor **Start** en el registro que determina cuándo se cargan:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<driver>
```

| Valor | Tipo | Descripción |
|-------|------|-------------|
| 0 | BOOT_START | Antes de que el kernel arranque completamente |
| 1 | SYSTEM_START | Durante la inicialización del kernel |
| 2 | AUTO_START | Después de que el kernel esté listo |
| 3 | DEMAND_START | Solo cuando se necesita (manual) |
| 4 | DISABLED | No se carga nunca |

> [!tip] Diagnóstico
> Si cambias el valor Start de un driver problemático a **4 (DISABLED)**, el driver no se cargará y puedes arrancar el sistema para investigar.

---

## Cómo un Conflicto de IRQ Causa Pantalla Negra

### Escenario del fallo

```
1. Windows inicia fase SYSTEM_START
         │
         ▼
2. Carga Intel Serial IO Driver
         │
         ▼
3. Driver solicita IRQ al sistema (vía ACPI)
         │
         ▼
4. ACPI asigna IRQ conflictivo o mal configurado
         │
         ▼
5. Driver intenta inicializar hardware
         │
         ▼
┌────────┴────────┬─────────────────┐
▼                 ▼                 ▼
Deadlock      IRQ Storm      Excepción
(espera       (interrupciones  no manejada
infinita)     infinitas)       en ISR
         │
         ▼
6. Sistema congelado ANTES del escritorio
         │
         ▼
7. PANTALLA NEGRA
```

### Por qué específicamente pantalla negra

La GPU probablemente inicializó el modo gráfico correctamente, pero el sistema se colgó **antes** de que `winlogon.exe` pudiera dibujar la pantalla de login.

La pantalla está técnicamente "encendida" (no hay señal de error), pero no hay contenido porque el proceso responsable de dibujarlo nunca llegó a ejecutarse.

---

## Métodos de Diagnóstico

### Método 1: Modo Seguro

El modo seguro carga solo drivers marcados como críticos. Si el sistema arranca en modo seguro pero no en modo normal, el problema es un driver no esencial.

```powershell
# Habilitar modo seguro desde cmd admin
bcdedit /set {current} safeboot minimal

# Volver a modo normal después
bcdedit /deletevalue {current} safeboot
```

### Método 2: Boot Logging

Windows puede generar un log de qué drivers se cargan y si fallan:

```powershell
# Habilitar boot logging
bcdedit /set {current} bootlog yes
```

Después del arranque, revisar:
```
C:\Windows\ntbtlog.txt
```

Ejemplo de salida:
```
Loaded driver \SystemRoot\System32\drivers\intelppm.sys
Loaded driver \SystemRoot\System32\drivers\iaStorV.sys
Did not load driver \SystemRoot\System32\drivers\SerialIO.sys  ← FALLO
```

### Método 3: Visor de Eventos

Después de un arranque exitoso (ej: modo seguro), revisar:

```
Visor de eventos → Registros de Windows → Sistema
```

Filtrar por:
- Origen: **Kernel-PnP**
- Origen: **Service Control Manager**
- Nivel: **Error** o **Advertencia**

### Método 4: Deshabilitación selectiva

Desde modo seguro o usando `msconfig`:

```
msconfig → Servicios → Ocultar servicios de Microsoft → Deshabilitar todo
msconfig → Inicio → Abrir Administrador de tareas → Deshabilitar todo
```

Ir habilitando de uno en uno hasta encontrar el culpable.

### Método 5: Driver Verifier

Herramienta avanzada para detectar drivers problemáticos:

```powershell
# Configurar verificación de todos los drivers no-Microsoft
verifier /standard /all

# Ver resultados
verifier /query

# Desactivar después del diagnóstico
verifier /reset
```

> [!danger] Precaución
> Driver Verifier puede causar BSODs frecuentes mientras está activo. Usar solo para diagnóstico y desactivar después.

---

## Formas de Deshabilitar un Dispositivo

### Nivel 1: Administrador de dispositivos (visible)

```
Administrador de dispositivos → Clic derecho → Deshabilitar
```

- Fácil de revertir
- Se resetea con reinstalación de Windows
- **No es lo que hizo el técnico** (el dispositivo aparecía sin flecha)

### Nivel 2: Registro de Windows

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<driver>
```

Cambiar `Start` de su valor normal a `4` (DISABLED).

- Sobrevive reinicios
- Se resetea con reinstalación limpia
- **Posiblemente lo que hizo**, pero el reset debería haberlo revertido

### Nivel 3: Política de grupo

```
gpedit.msc → Configuración del equipo → Plantillas administrativas →
Sistema → Instalación de dispositivos → Restricciones de instalación
```

Puede bloquear dispositivos por Hardware ID:
```
"Impedir la instalación de dispositivos que coincidan con estos ID"
ACPI\ELAN1200
```

- Sobrevive actualizaciones
- **Podría explicar** por qué el driver no se aplica

### Nivel 4: UEFI/NVRAM (oculto)

Las BIOS InsydeH2O tienen opciones ocultas no accesibles desde el menú normal. Herramientas como **H2OUVE** (Insyde UEFI Variable Editor) permiten modificar variables NVRAM.

```
Variable: I2C0_ENABLE
Value: 0x00 (disabled)
```

> [!danger] Esto es lo más probable
> Las variables NVRAM **no se resetean** con "Load Defaults" porque están en memoria no volátil separada de la configuración visible. Explicaría por qué nada funciona.

### Nivel 5: Hardware/Firmware

- Desconexión física del flex cable
- Flash de firmware corrupto al touchpad
- Daño en el conector ZIF

---

## Análisis del Caso: Qué Hizo el Técnico

### El problema original
Pantalla negra al arrancar.

### Su proceso probable

```
1. Intentó arrancar normalmente → Pantalla negra
         │
         ▼
2. Arrancó en modo seguro → Funcionó
         │
         ▼
3. Conclusión: Un driver no esencial causa el fallo
         │
         ▼
4. Revisó logs/eventos → Identificó Serial IO / I2C
         │
         ▼
5. Deshabilitó el touchpad a nivel UEFI/NVRAM
         │
         ▼
6. Arrancó normalmente → Funcionó
         │
         ▼
7. "Arreglado" 
```

### Por qué es una chapuza

**Lo que debería haber hecho:**

1. Identificar el conflicto específico (IRQ, ACPI, driver corrupto)
2. Actualizar/reinstalar el driver Intel Serial IO correctamente
3. Actualizar BIOS si era un bug conocido de ACPI
4. Verificar que no hubiera malware tocando drivers
5. Devolver el portátil **funcionando al 100%**

**Lo que hizo:**

1. Identificó que el touchpad/Serial IO causaba el cuelgue
2. Lo deshabilitó a nivel profundo (UEFI)
3. Cobró por "arreglarlo"
4. Dio una explicación técnica ("vector de interrupción") para parecer profesional

### Resultado

El portátil arranca, pero con **menos funcionalidad** que antes. Y la "solución" es tan profunda que ni reinstalar Windows, ni actualizar BIOS, ni resetear configuración la revierte.

---

## Cómo Revertirlo (Opciones)

### Opción 1: Linux Live USB (diagnóstico)

Arrancar Ubuntu desde USB sin instalar:

- Si el touchpad **funciona** → El problema es 100% Windows/drivers/UEFI config
- Si **no funciona** → Hardware dañado o firmware corrupto

### Opción 2: Herramientas UEFI

Usar **H2OUVE** o **UEFI Tool** para:

1. Extraer la imagen BIOS actual
2. Buscar variables relacionadas con I2C, Serial IO, Touchpad
3. Restaurar valores por defecto
4. Re-flashear

> [!warning] Riesgo
> Modificar NVRAM incorrectamente puede brickear el equipo. Solo para usuarios avanzados.

### Opción 3: Flash completo de BIOS

No actualizar, sino **borrar NVRAM y flashear desde cero**:

1. Descargar el ejecutable de BIOS de Acer
2. Extraer el archivo .fd
3. Usar un programador SPI para flashear directamente el chip
4. O usar herramientas de crisis recovery de Insyde

### Opción 4: Servicio técnico oficial

Llevar a servicio técnico autorizado de Acer que pueda:
- Acceder a herramientas de diagnóstico del fabricante
- Flashear BIOS/NVRAM con herramientas oficiales
- Verificar hardware físicamente

---

## Lecciones Aprendidas

> [!note] Para usuarios
> - Pregunta siempre **qué** se va a hacer y **por qué**
> - Pide explicación de los cambios realizados
> - Verifica que todo funciona antes de pagar
> - Guarda una imagen de disco antes de llevar a reparar

> [!note] Para técnicos
> - Deshabilitar no es arreglar
> - Una solución que reduce funcionalidad no es solución
> - Documenta los cambios para que sean reversibles
> - Si no sabes arreglarlo bien, sé honesto

> [!note] Para profesionales de seguridad
> - El acceso físico permite modificaciones profundas
> - Las variables UEFI/NVRAM son un vector de persistencia
> - "Vector de interrupción" suena técnico pero puede ser humo
> - Verificar la integridad del firmware es parte del hardening

---

## Referencias

- [Intel Serial IO Driver Documentation](https://www.intel.com/content/www/us/en/download/18235/intel-serial-io-driver-for-windows-10.html)
- [InsydeH2O UEFI BIOS Documentation](https://www.insyde.com/)
- [Windows Driver Start Types - Microsoft Docs](https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/specifying-driver-load-order)
- [I2C Bus Specification - NXP](https://www.nxp.com/docs/en/user-guide/UM10204.pdf)
- [ACPI Specification](https://uefi.org/specifications)

---

## Metadatos

- **Caso**: Acer Nitro AN515-54 con touchpad deshabilitado
- **BIOS**: InsydeH2O
- **Touchpad**: ELAN o Synaptics (I2C)
- **Síntoma original**: Pantalla negra al arrancar
- **"Solución" del técnico**: Deshabilitar touchpad a nivel UEFI
- **Estado actual**: Touchpad aparece en Windows pero no funciona
