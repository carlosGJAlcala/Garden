---
title: "2025 02 04 Ingenieria Inversa"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---


La máquina virtual de .NET es el **Common Language Infrastructure (CLI)**, que permite la ejecución de código escrito en múltiples lenguajes compatibles con la plataforma.

Para determinar el tipo de un fichero en sistemas Unix/Linux, se puede utilizar el comando `file`. Este comando analiza la estructura del archivo y devuelve información sobre su formato, lo que es útil en análisis forenses o para identificar ejecutables ofuscados.

Si se desea visualizar el contenido de un archivo en formato hexadecimal, se puede utilizar `xxd`. Este comando convierte un archivo en una representación hexadecimal legible, facilitando el análisis de binarios o la búsqueda de patrones dentro del archivo.

En el contexto de seguridad, ha habido exploits que utilizan `strings` para detectar fragmentos de código sospechoso en binarios. `strings` extrae secuencias de caracteres imprimibles de un archivo, lo que puede revelar información sensible o pistas sobre el comportamiento de un malware.

Si un malware utiliza **carga dinámica de librerías**, puede evadir el análisis de antivirus basado en escaneo estático, ya que el motor de detección no sabrá qué componentes se cargarán en tiempo de ejecución. La técnica más común para esto es el **enlazado dinámico**, que permite a un programa cargar librerías externas solo cuando las necesita.

El uso del enlazado dinámico tiene varias ventajas, como reducir el tamaño del binario final. Si un ejecutable ha sido **strippeado** (es decir, se le ha eliminado la información de depuración y símbolos), pero usa enlace dinámico, aún es posible recuperar información relevante analizando las librerías dinámicas utilizadas, ya que estas no suelen estar strippeadas. En Windows, las librerías dinámicas que exportan funciones se llaman **DLLs (Dynamic Link Libraries)**.

### Ejecución simbólica


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

La **ejecución simbólica** es una técnica utilizada en análisis de seguridad y depuración para evaluar todas las posibles ejecuciones de un programa sin ejecutarlo realmente. Se basa en representar las entradas como variables simbólicas y analizar los caminos de ejecución posibles, lo que permite detectar vulnerabilidades como desbordamientos de buffer o condiciones lógicas inseguras.

### Desarrollo de un desempaquetador de malware

Programar un **desempaquetador de malware** implica desarrollar una herramienta capaz de detectar y extraer payloads ocultos dentro de binarios ofuscados o empaquetados. Esto puede implicar el uso de técnicas de instrumentación dinámica, depuración y análisis de memoria.

### Herramientas y compilación

Para compilar y ejecutar programas en C, es necesario instalar las herramientas adecuadas. En entornos Linux, si se trabaja con aplicaciones de 32 bits en un sistema de 64 bits, se deben instalar los paquetes de compatibilidad:

```bash
sudo apt install gcc-multilib g++-multilib
```

Para compilar un programa en 32 bits, se usa:

```bash
gcc -m32 archivo.c -o archivo
```

En análisis de binarios, el **peor caso posible** es encontrarse con un ejecutable que haya sido **linkeado estáticamente y strippeado**, ya que en este escenario no se pueden recuperar funciones ni referencias de librerías externas, dificultando el análisis.

### Radare2 y análisis en Unix

`radare2` es una potente herramienta de análisis de binarios utilizada en entornos Unix/Linux. Permite la ingeniería inversa de ejecutables, incluyendo depuración, análisis estático y ejecución simbólica.

### Otros conceptos

- `glibc-devel`: Es un paquete de desarrollo que proporciona las cabeceras y bibliotecas necesarias para compilar programas que usen la **GNU C Library (glibc)**. Es esencial para el desarrollo de software en C en entornos Linux.
- `ALF`: Posiblemente te refieras a **Address Layout Randomization (ASLR)**, que es una técnica de seguridad que aleatoriza las direcciones de memoria donde se cargan ejecutables y librerías para dificultar la explotación de vulnerabilidades.
- `idum`: No está claro a qué te refieres con esto. Si puedes dar más contexto, puedo ayudarte a precisar su significado.
