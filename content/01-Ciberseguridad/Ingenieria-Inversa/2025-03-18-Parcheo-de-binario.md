---
title: "Parcheo de binario"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
conseguir un windows xp  con service pack 0 con  con un ftp
conseguir un inteprete  para la semana que viene 
python instalad
# Parcheo de binario


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

El parcheo de binarios consiste en modificar un archivo ejecutable para actualizarlo o corregirlo sin acceso al código fuente. Este proceso se realiza directamente sobre el archivo binario, lo que significa que no se tiene conocimiento previo de su código fuente ni su estructura interna. El objetivo es realizar cambios sin alterar la funcionalidad general del programa, a menudo corrigiendo errores o aplicando mejoras.

En el parcheo de binarios, es posible modificar varios aspectos del ejecutable, como el flujo de ejecución del programa o el valor de ciertas variables e instrucciones. Sin embargo, se debe tener cuidado al realizar estos cambios, ya que no se pueden hacer modificaciones que alteren el tamaño del binario ni que afecten su estructura de manera que cause su mal funcionamiento.

**Tipos de modificaciones comunes:**

1. **Modificación del flujo de ejecución:** Alterar la secuencia de instrucciones para cambiar cómo se ejecutan las funciones o procesos dentro del programa.
2. **Modificación de valores de variables o instrucciones:** Cambiar el valor de ciertas variables o de las instrucciones dentro del código compilado.

### Riesgos del parcheo de binarios

Al realizar un parcheo incorrecto, pueden surgir varios problemas, tales como:

1. **Rotura del flujo de ejecución:** Si los cambios no son cuidadosamente implementados, el flujo de ejecución puede interrumpirse o desorganizarse, causando que el programa deje de funcionar correctamente.
2. **Corrupción del ejecutable:** Un parcheo mal realizado puede dañar el archivo binario, lo que puede llevar a errores irreparables o fallos del sistema.
3. **Violación de segmento:** Saltar a secciones no permitidas del ejecutable, como áreas protegidas de memoria, puede provocar una violación de segmento y cerrar el programa inesperadamente.
4. **Modificación del hash del archivo:** El parcheo puede alterar el valor hash del archivo, lo que puede afectar la autenticidad del software. Técnicas como el uso de malware a veces incluyen mecanismos para evitar que estas alteraciones sean detectadas.

### Ejemplos históricos

Un ejemplo famoso de parcheo es el caso de **Rainbow Six Vegas**, que fue denunciado por **Ubisoft** debido a la modificación no autorizada de su software. En este caso, se utilizaban técnicas de parcheo para alterar el comportamiento del juego, lo que violaba las leyes de propiedad intelectual.

Otro caso ampliamente conocido es el de **Sublime Text**, un software de edición de texto que fue parcheado repetidamente. Los usuarios podían borrar ciertas listas mediante un editor hexadecimal, lo que permitía eludir restricciones de la aplicación.

### Consideraciones legales

Es importante destacar que modificar un software sin el permiso del titular de los derechos es ilegal. El acto de **reverse engineering** o ingeniería inversa también ha sido considerado un delito en muchas jurisdicciones, ya que implica el análisis de un binario para entender su funcionamiento interno y, en algunos casos, modificarlo.

### Herramientas necesarias para parchear un binario

Para realizar un parcheo de binarios de forma adecuada, se requieren herramientas especializadas. Una de las más comunes es un depurador que permita leer y escribir en la memoria del binario, lo que se denomina un **depurador RW/RW**. Este tipo de depuradores facilita la modificación del contenido binario en tiempo de ejecución, permitiendo modificar variables, instrucciones o incluso el flujo de ejecución del programa sin necesidad de recompilar el código.

En resumen, el parcheo de binarios es una técnica avanzada que debe realizarse con precaución, pues puede acarrear riesgos de corrupción del archivo y violaciones legales si no se lleva a cabo de manera ética y con el debido consentimiento.



---


Abrimos el binario `./func1` y lo modificamos utilizando **GHex** para editar su contenido en formato hexadecimal.

**Reparar (reapear) un binario** consiste en reducir su tamaño optimizando su estructura, eliminando secciones innecesarias o comprimiendo datos sin afectar su funcionalidad.

Las vulnerabilidades pueden **concatenarse**, permitiendo la explotación encadenada de fallos de seguridad para alcanzar un objetivo más complejo. En este contexto, se suelen utilizar técnicas como **ROP (Return-Oriented Programming)**, que permite ejecutar código arbitrario mediante gadgets en la memoria. Como mínimo, se requiere una secuencia de ROP bien estructurada para lograr la explotación efectiva.

El comando:

```bash
watch -n 1 <comando>
```

Ejecuta `<comando>` automáticamente cada segundo, lo que permite monitorear cambios en tiempo real. Puede ser útil para observar la salida de herramientas de análisis forense, depuración o seguridad.

---
