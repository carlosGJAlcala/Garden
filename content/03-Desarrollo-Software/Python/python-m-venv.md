---
title: "Guía Rápida: `python -m venv` - Creando Entornos Virtuales"
date: 2026-01-26
tags:
  - desarrollo-software
  - python
---
¡Excelente idea! Aquí tienes una nota explicativa completa sobre `python -m venv`, lista para copiar y pegar en un archivo Markdown (`.md`).

---

# Guía Rápida: `python -m venv` - Creando Entornos Virtuales


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

Si alguna vez has trabajado en más de un proyecto de Python, es casi seguro que te has topado con este comando. `python -m venv` es una de las herramientas más fundamentales y esenciales en el ecosistema de Python moderno. Esta guía explica qué es, por qué es crucial y cómo usarlo.

## ¿Qué es un Entorno Virtual?

Imagina que un **entorno virtual** es una **caja de herramientas aislada y específica para un proyecto**.

Cuando instalas Python en tu sistema, tienes una instalación "global" con sus propias librerías (paquetes). Si instalas un paquete con `pip install <paquete>`, se instala en ese sitio global.

Un entorno virtual crea una carpeta en tu proyecto que contiene una copia de Python y su propio directorio de paquetes. Cuando "activas" este entorno, tu terminal pasa a usar esta versión aislada en lugar de la global. Cualquier paquete que instales se quedará **dentro de esa caja** y no afectará a otros proyectos ni a tu sistema.

## ¿Por Qué es Tan Importante?

Usar entornos virtuales no es una opción, es una **buena práctica indispensable**. Estas son las razones principales:

*   **Aislamiento de Dependencias:** El Proyecto A puede necesitar `requests==2.25.0` y el Proyecto B una versión más nueva, `requests==2.28.0`. Sin entornos virtuales, tendrías un conflicto constante. Con ellos, cada proyecto tiene su propia versión sin problemas.
*   **Reproducibilidad:** Puedes generar un archivo `requirements.txt` que lista exactamente qué paquetes y versiones usa tu proyecto. Otro desarrollador (o tú mismo en otro ordenador) puede recrear el entorno idéntico con un solo comando (`pip install -r requirements.txt`).
*   **Limpieza del Sistema:** Mantiene tu instalación global de Python limpia. Solo los paquetes que realmente usas en todos lados (como `pip` mismo) deberían estar allí.
*   **Permisos:** Evita la necesidad de usar `sudo` para instalar paquetes, ya que todo se instala en una carpeta local de tu proyecto sobre la que tienes control total.

## Uso Básico - Paso a Paso

El proceso es siempre el mismo: **Crear**, **Activar**, **Usar** y **Desactivar**.

### 1. Crear el Entorno Virtual

Navega a la carpeta raíz de tu proyecto en la terminal y ejecuta:

```bash
# Sintaxis: python -m venv <nombre-del-entorno>
# Por convención, se suele llamar "venv" o ".venv"
python -m venv venv
```

Esto creará una nueva carpeta llamada `venv` en tu proyecto.

> **¡Pro Tip!** Añade el nombre de tu entorno virtual (ej. `venv/` o `.venv/`) a tu archivo `.gitignore` para no subirlo a tu repositorio de código.

### 2. Activar el Entorno

La activación depende de tu sistema operativo.

*   **En Windows (PowerShell o CMD):**
    ```powershell
    # La ruta al script de activación
    .\venv\Scripts\activate
    ```

*   **En macOS y Linux (bash, zsh, etc.):**
    ```bash
    # La palabra clave "source" es importante
    source venv/bin/activate
    ```

Sabrás que el entorno está activo porque el prompt de tu terminal cambiará, mostrando el nombre del entorno entre paréntesis. Ejemplo: `(venv) C:\Users\TuUsuario\MiProyecto>`.

### 3. Usar el Entorno

Ahora que está activo:

*   Cualquier paquete que instales con `pip` se guardará dentro de la carpeta `venv`.
    ```bash
    (venv) $ pip install pandas requests numpy
    ```
*   Cuando ejecutes tu código con `python mi_script.py`, se usará el intérprete y los paquetes del entorno virtual.

### 4. Desactivar el Entorno

Cuando termines de trabajar, simplemente ejecuta:

```bash
(venv) $ deactivate
```

El prompt de la terminal volverá a la normalidad.

## Desglose del Comando `python -m venv`

Veamos qué significa cada parte:

*   `python`: Llama al intérprete de Python que está disponible en tu `PATH`.
*   `-m`: Es una bandera (flag) que le dice a Python: "No ejecutes un archivo, sino un **módulo** de la librería estándar como si fuera un script".
*   `venv`: Es el nombre del módulo que queremos ejecutar. El módulo `venv` está diseñado específicamente para crear entornos virtuales.

En resumen, el comando le pide a tu instalación de Python que use su herramienta interna `venv` para crear un nuevo entorno virtual.

---