---
title: "MONA - Asistente para Explotación en Immunity Debugger"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
# MONA - Asistente para Explotación en Immunity Debugger


> **Relacionado**: [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|2025 04 20 Computacion Cuantica y Criptografia Post Cuantica]].

## Descripción
**Mona.py** es un script de Python diseñado para facilitar y automatizar tareas relacionadas con la explotación de vulnerabilidades en **Immunity Debugger**. Ayuda a los analistas a identificar patrones, calcular compensaciones, buscar gadgets para Return-Oriented Programming (ROP), y automatizar tareas complejas en el desarrollo de exploits.

Desarrollado por Corelan Team, Mona es una herramienta fundamental para analistas de seguridad y pentesters que trabajan en entornos Windows.

## Características
- **Identificación de Patrones**: Genera y encuentra patrones únicos para calcular compensaciones.
- **Búsqueda de Gadgets ROP**: Encuentra gadgets para construir cadenas ROP.
- **Identificación de Direcciones Seguras**: Busca direcciones en módulos con protecciones específicas (DEP, ASLR).
- **Automatización de Explotación**: Facilita tareas como encontrar badchars, generar cadenas de payload y mucho más.
- **Compatibilidad con Immunity Debugger**: Totalmente integrado en este entorno de depuración.

## Usos Comunes
- **Desarrollo de Exploits**: Automatiza tareas repetitivas durante la creación de exploits.
- **Análisis de Binarios**: Identifica vulnerabilidades en programas y módulos.
- **Pruebas de Penetración**: Evalúa la seguridad de aplicaciones Windows.
- **Entrenamiento en Explotación**: Usada en laboratorios y cursos para aprender técnicas de explotación.

---

## Instalación

### Requisitos
- **Immunity Debugger** instalado en un sistema Windows.
- **Python 2.7**, que Immunity Debugger utiliza de manera predeterminada.

### Instalación de Mona
1. Descarga Mona.py desde el repositorio oficial:
   [Mona.py - Corelan](https://github.com/corelan/mona)
2. Copia el archivo `mona.py` al directorio de scripts de Immunity Debugger:
   ```plaintext
   C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands\
   ```
3. Reinicia Immunity Debugger para cargar el script.

---

## Comandos Básicos

### 1. **Generar un Patrón Único**
Genera un patrón único para calcular compensaciones:
```plaintext
!mona pattern_create 500
```
- `500`: Longitud del patrón a generar.

### 2. **Encontrar la Compensación**
Encuentra la posición de un valor dentro del patrón:
```plaintext
!mona pattern_offset <valor>
```
Ejemplo:
```plaintext
!mona pattern_offset 39654138
```

### 3. **Buscar Gadgets ROP**
Busca gadgets en módulos específicos:
```plaintext
!mona rop
```
Opciones avanzadas para filtrar gadgets:
```plaintext
!mona rop -m <nombre_modulo>
```

### 4. **Identificar Badchars**
Detecta caracteres problemáticos en un exploit:
```plaintext
!mona compare -f badchars.bin -a <dirección>
```
- `badchars.bin`: Archivo con posibles badchars.
- `<dirección>`: Dirección de memoria donde empieza el análisis.

### 5. **Buscar Direcciones en Módulos**
Lista direcciones de interés en módulos con protecciones específicas:
```plaintext
!mona modules
```
Resultados útiles para encontrar módulos sin ASLR y DEP.

---

## Ejemplo Completo de Uso

1. **Generar un Patrón para Sobrescribir EIP**:
   En tu script de prueba, coloca un patrón generado con:
   ```plaintext
   !mona pattern_create 400
   ```
   Usa este patrón en tu payload y ejecuta el programa objetivo.

2. **Calcular la Compensación**:
   Cuando el programa crashea, encuentra el valor en EIP usando:
   ```plaintext
   !mona pattern_offset <valor_en_eip>
   ```

3. **Identificar Gadgets ROP**:
   Busca gadgets para construir una cadena ROP:
   ```plaintext
   !mona rop -m kernel32.dll
   ```

4. **Detectar Badchars**:
   Genera un archivo con posibles badchars y compáralo:
   ```plaintext
   !mona compare -f badchars.bin -a 0x0012FF50
   ```

5. **Buscar Módulos sin Protecciones**:
   Identifica módulos útiles para redirigir la ejecución:
   ```plaintext
   !mona modules
   ```

---

## Opciones Avanzadas

### Configuración del Directorio de Salida
Cambia el directorio donde Mona guarda los resultados:
```plaintext
!mona config -set workingfolder C:\ExploitResults\
```

### Generación de Payloads
Crea una cadena de payload con Mona:
```plaintext
!mona jmp -r esp
```

### Análisis de Protección de Módulos
Lista los módulos junto con sus protecciones:
```plaintext
!mona modules -n DEP,ASLR
```

---

## Relevancia en Ciberseguridad

**Mona.py** es esencial para:
- **Automatizar Tareas de Explotación**: Reduce el tiempo necesario para realizar análisis complejos.
- **Identificar Vulnerabilidades**: Facilita la búsqueda de puntos débiles en aplicaciones.
- **Entrenamiento y Educación**: Proporciona una plataforma práctica para aprender técnicas de explotación.

---

## Contramedidas

1. **Implementar Protecciones Modernas**:
   - Asegúrate de que los módulos tengan **ASLR** (Address Space Layout Randomization) y **DEP** (Data Execution Prevention) habilitados.

2. **Actualización de Software**:
   - Mantén las aplicaciones y librerías actualizadas para mitigar vulnerabilidades conocidas.

3. **Análisis de Binarios**:
   - Realiza revisiones de seguridad en el código fuente y en binarios críticos.

4. **Uso de Seguridad en Compilación**:
   - Configura compiladores con opciones como **/GS** (Buffer Security Check) y **SEHOP** (Structured Exception Handling Overwrite Protection).

---

## Recursos Adicionales
- [Repositorio Oficial de Mona.py](https://github.com/corelan/mona)
- [Guía Oficial de Corelan](https://www.corelan.be/index.php/introduction-to-mona-py/)
- [[Immunity-Debugger-Depuracion-y-Explotacion]]
- [[ROP-Return-Oriented-Programming]]

---

## Notas Relacionadas
- [[Exploit-Development]]
- [[Buffer-Overflow]]
- [[Gadgets-ROP-Busqueda-y-Uso]]
- [[Protecciones-de-Memoria-en-Windows]]
