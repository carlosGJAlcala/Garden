---
title: "Que es init - El sistema de arranque de Linux"
date: 2024-11-21
tags:
  - linux
  - sistemas-operativos
source: https://www.genbeta.com/linux/que-init-sistema-arranque-linux-que-alternativas-existen-distribucion-que-uses
author: Marcos Merino
---

# Qué es init, el sistema de arranque de Linux (y qué alternativas existen según la distribución que uses)


> **Relacionado**: [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

> ## Excerpt
> Cuando encendemos un PC equipado con un sistema operativo Unix (como, por ejemplo, Linux) el kernel del mismo inicia, una vez está cargado en memoria, un...

---
Cuando encendemos un PC equipado con un sistema operativo Unix (como, por ejemplo, Linux) el kernel del mismo inicia, una vez está cargado en memoria, **un primer proceso responsable de iniciar directa o indirectamente todos los demás procesos** que se ejecutarán en el equipo hasta que lo apaguemos.

Este proceso recibe el nombre genérico de 'init' y es, como habrás podido suponer, **constituye una pieza clave del funcionamiento de Linux y similares**. Tanto, que si no es capaz de hallar su correspondiente script el arranque del sistema quedará abortado. Al fin y al cabo, resulta necesario para iniciar la consola, montar el sistema de archivos, configurar el hostname, iniciar los puertos o el firewall, etc.

Dicho script también determina el **cómo se inicia nuestro init, pues establece su 'nivel de ejecución'** o 'runlevel'. Según el runlevel indicado, init ejecutará un determinado grupo de procesos, permitiendo recurrir al nivel 0 para apagar el sistema y al 6 para reiniciarlo. El resto son los siguientes:

1.  Modo monousuario (generalmente para tareas de mantenimiento).
2.  Modo multiusuario sin soporte de red
3.  Modo multiusuario con soporte de red
4.  Se usa sólo para secuencias de inicio personalizadas.
5.  Modo multiusuario completo con entorno gráfico.

[![Qué es Linux y cómo funciona](https://i.blogs.es/ed64de/ian-parker-tlcldigmtke-unsplash/375_142.webp)](https://www.genbeta.com/a-fondo/que-linux-como-funciona)

Sin embargo, hablar de init es como hablar de 'procesador de textos' para referirnos a Word, **pues existen diversas implementaciones rivales**. Eso no significa que no haya estándares de facto: procedente de los vetustos Unix System V, **SysV** —o, más exactamente, su release SysV4— **fue durante mucho tiempo el software de init más usado en el mundo Linux**… hasta la llegada de systemd.

## El rey SysV ha muerto, viva el rey systemd

Creado por Lennart Poettering, creador también de PulseAudio, este desarrollador de Red Hat ha logrado situar su sistema de init como el más usado por las grandes distribuciones desde hace unos 7 años.

La comunidad de Debian (**distribución en que se basan Ubuntu y sus derivadas**) vivió con [especial polémica el cambio desde SysV](https://www.genbeta.com/linux/canonical-acata-la-decision-de-debian-y-ubuntu-abrazara-systemd), tanto que en 2017 se terminó lanzando un 'fork' de Debian ([Devuan](https://www.genbeta.com/linux/ya-disponible-devuan-1-0-la-primera-version-estable-del-debian-sin-systemd)) que usaba SysV por defecto y estaba abierto a otros init alternativos.

La polémica deriva del hecho de que se considera que este nuevo init incrementa enormemente la complejidad del sistema, **convirtiéndolo —según muchas voces de la comunidad— es una especie de 'segundo kernel'** que violenta la propia filosofía de funcionamiento de Unix ('haz una cosa y hazla bien') y que, por su dinámica de funcionamiento, dificulta que mucho software adaptado para systemd pueda ser usado sin cambios en otros init.

## Otras alternativas

Slackware fue una de las pocas distribuciones que **nunca adoptaron SysV** y ahora ha seguido sin dar el salto a systemd: **recurre a initscripts** basados en los que usan [los sistemas \*BSD](https://www.genbeta.com/sistemas-operativos/sistemas-operativos-bsd-primos-conocidos-linux-que-se-encuentra-mac-os-x). Otras distribuciones, como CRUX, hacen lo mismo.

[Void Linux](https://www.genbeta.com/linux/void-linux-linux-vieja-escuela-nacido-espana), una distribución aún más 'BSDiana' que Slackware, **hace uso de otro init** [llamado Runit](http://smarden.org/runit/), que ahora también podemos usar (aunque de forma no predeterminada) en Devuan.

Por su parte, **Gentoo y sus distribuciones derivadas hacen uso de su propio sistema** de init personalizado, [denominado OpenRC](https://wiki.gentoo.org/wiki/Project:OpenRC) (usada también por distribuciones como Alpine y Artix).

Imagen | [Eli Duke](https://www.flickr.com/photos/elisfanclub/2189150570)
