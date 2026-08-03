---
title: "Seguridad Web Y Auditoria"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - seguridadwebyauditoria
---
<<<<<<< HEAD:ASIGNATURAS_MASTER/Fundamentos de la seguridad en el sofware y en los componentes/seguridadWebYAuditoría/seguridad web y auditoria.md


contraseña kali kali/kali
contraseña owasp root/owaspbwa
contraseña  root/Lamp1278


poner habilitados servicios 
servicios 
systmenctl enable
ospd-openvas
gvmd
gsad


Para crear una red nat entre ellos usamos el siguiente comando:
VBoxManage natnetwork add --netname <nombre_red> --network "<rango_IP>" --enable


VBoxManage list natnetworks

2. Configuración de red del escenario.

Para el tema de la configuración he instalado las dos máquinas con virtual box y con configuración bridge para que tenga su propia ip y el kali es un ubuntu en dual bot

## PARTE I- AUDITORÍA WEB Y HARDENING


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/OpenVAS|OpenVAS]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

Primero veos en la máquina Lamp está levantado están los seguridad
![[Pasted-image-20241113164146.png]]Suponemos que no conocemos la ip, el primer paso sería hacer un nmap con la máscara de red.
nmap 172.22.0.0/16 
En nuestro caso lo haremos ya 