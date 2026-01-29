---
title: "Proxmox"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - gestionservidores
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]].

Proxmox es una plataforma de virtualización de código abierto que utiliza una arquitectura híbrida, es decir, virtualización de máquinas virtuales (VM) y contenedores LXC (Linux Containers). Proxmox está diseñado para facilitar la gestión de servidores virtualizados, y se usa tanto en entornos de producción como en desarrollo para gestionar máquinas virtuales y contenedores. Ahora bien, para responder a tus preguntas sobre Proxmox y LXC:

¿Qué es Proxmox?

Proxmox VE (Virtual Environment) es una plataforma de virtualización de código abierto que permite la gestión de máquinas virtuales y contenedores a través de una interfaz web centralizada. Proxmox soporta KVM (Kernel-based Virtual Machine) para la virtualización de máquinas virtuales y LXC (Linux Containers) para la virtualización a nivel de contenedor.

¿Qué tipo de virtualización usa Proxmox?

Máquinas Virtuales (VMs): Utiliza KVM como hipervisor de tipo 1 para la virtualización completa de máquinas virtuales. Esto significa que cada máquina virtual tiene su propio sistema operativo completo (incluido el kernel), como si fuera un servidor físico.

Contenedores LXC: Utiliza LXC para virtualización ligera a nivel de sistema operativo. Los contenedores LXC comparten el kernel del sistema host, pero tienen sus propios entornos de usuario aislados. Son más ligeros en términos de recursos que las máquinas virtuales.


¿Qué son los contenedores LXC?

LXC (Linux Containers) es una tecnología de virtualización a nivel de sistema operativo, lo que significa que los contenedores comparten el mismo kernel que el host, pero están aislados entre sí. Los contenedores LXC proporcionan una forma eficiente y ligera de ejecutar aplicaciones y servicios, pero no proporcionan el mismo nivel de aislamiento que las máquinas virtuales completas.

Diferencia entre LXC y otros tipos de contenedores

1. LXC (Linux Containers)

Virtualización a nivel de sistema operativo: Los contenedores LXC son un tipo de virtualización a nivel de sistema operativo. Comparten el mismo kernel que el host, pero están aislados entre sí. Esto los hace más ligeros en comparación con las máquinas virtuales, pero también limita la flexibilidad en términos de la variedad de sistemas operativos que se pueden ejecutar dentro de los contenedores.

Aislamiento: LXC proporciona un buen aislamiento de los espacios de usuario (por ejemplo, archivos y procesos), pero no tiene el mismo nivel de aislamiento que las máquinas virtuales. Sin embargo, es adecuado para aplicaciones ligeras que no requieren un kernel independiente.

Uso eficiente de recursos: Debido a que los contenedores LXC no requieren un sistema operativo completo para cada instancia, son más eficientes en términos de recursos (memoria, almacenamiento, etc.) en comparación con las máquinas virtuales.

Uso en Proxmox: En Proxmox, los contenedores LXC se gestionan de manera eficiente, permitiendo ejecutar varios contenedores en una sola máquina física sin la sobrecarga que normalmente tendrías al usar máquinas virtuales completas.


2. Otros tipos de contenedores (Docker, etc.)

Docker: Docker es otra tecnología de contenedores, pero con un enfoque diferente. Docker también utiliza la virtualización a nivel de sistema operativo (al igual que LXC), pero tiene un enfoque más centrado en la portabilidad y la gestión de aplicaciones. Docker utiliza imágenes de contenedor que contienen el software y sus dependencias, lo que hace que sea fácil mover contenedores entre diferentes sistemas. Docker también utiliza LXC en sus versiones iniciales, pero más recientemente, ha implementado su propio sistema de contenedores.

Diferencias clave:

Docker está diseñado principalmente para gestionar aplicaciones y su entorno, mientras que LXC es más adecuado para contener sistemas operativos completos.

Docker tiene su propio ecosistema de herramientas para crear, gestionar y distribuir contenedores, mientras que LXC se basa más en herramientas estándar de Linux para crear contenedores.



3. Contenedores en la nube (Kubernetes, OpenShift)

Kubernetes y OpenShift son sistemas de orquestación de contenedores que gestionan clústeres de contenedores. A menudo utilizan Docker o containerd para ejecutar contenedores en nodos. Estos sistemas están diseñados para gestionar contenedores distribuidos y garantizar la disponibilidad, escalabilidad y recuperación ante fallos.

Diferencias clave:

Kubernetes se utiliza para gestionar clústeres de contenedores a gran escala, mientras que LXC y Docker son tecnologías de contenedores más centradas en el aislamiento y ejecución de aplicaciones a nivel de máquina individual.



Diferencias clave entre LXC y máquinas virtuales

1. Aislamiento:

Máquinas virtuales (VMs): Cada VM tiene su propio kernel y sistema operativo, lo que proporciona un aislamiento total entre ellas.

LXC: Los contenedores LXC comparten el mismo kernel del host, por lo que el aislamiento es más liviano. A pesar de esto, LXC sigue ofreciendo un buen nivel de aislamiento de recursos y procesos.



2. Uso de recursos:

Máquinas virtuales (VMs): Tienen una sobrecarga mayor ya que cada VM ejecuta un sistema operativo completo, lo que implica más uso de memoria y almacenamiento.

LXC: Son mucho más ligeros en comparación con las VMs. Como los contenedores LXC comparten el kernel del sistema host, no requieren sistemas operativos completos para cada instancia.



3. Rendimiento:

Máquinas virtuales (VMs): El rendimiento de las VMs es generalmente menor que el de los contenedores, debido a la sobrecarga de la virtualización completa.

LXC: El rendimiento de los contenedores LXC es mucho más cercano al del host, ya que no tienen que gestionar un sistema operativo completo.



4. Flexibilidad:

Máquinas virtuales (VMs): Son más flexibles en cuanto a la ejecución de diferentes sistemas operativos. Puedes ejecutar sistemas operativos Windows, Linux, etc., en la misma infraestructura.

LXC: Los contenedores LXC están limitados a sistemas Linux y no pueden ejecutar otros sistemas operativos como Windows.




¿Cuándo usar LXC en Proxmox?

Aislamiento ligero: Si necesitas ejecutar aplicaciones ligeras o servidores con un aislamiento moderado y un uso eficiente de recursos, LXC es ideal.

Entornos de pruebas o desarrollo: Si estás construyendo un entorno de desarrollo o pruebas en el que las máquinas virtuales completas son innecesarias, los contenedores LXC te ofrecen una alternativa más eficiente.

Escalabilidad: Si necesitas ejecutar múltiples instancias de una aplicación o servicio sin mucha sobrecarga, LXC puede ser más adecuado que las máquinas virtuales.


Conclusión

Proxmox te permite usar tanto máquinas virtuales como contenedores LXC, lo que te da flexibilidad para elegir la opción más adecuada según tus necesidades. Los contenedores LXC son más ligeros y eficientes en términos de recursos, pero las máquinas virtuales proporcionan un mayor aislamiento y flexibilidad al poder ejecutar sistemas operativos completos. LXC es excelente para tareas que no requieren un kernel independiente o un sistema operativo completo, como servidores web, bases de datos o contenedores de aplicaciones.

Si tienes más dudas sobre cómo usar LXC en Proxmox o cómo configurar algún entorno, no dudes en preguntar. ¡Estoy aquí para ayudarte!

