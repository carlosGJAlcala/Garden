---
title: "Seguridad Web Y Auditoria"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---

poner habilitados servicios 
servicios 
systmenctl enable
ospd-openvas
gvmd
gsad

contraseña  root/Lamp1278
2. Configuración de red del escenario.

Para el tema de la configuración he instalado las dos máquinas con virtual box y con configuración bridge para que tenga su propia ip y el kali es un ubuntu en dual bot

## PARTE I- AUDITORÍA WEB Y HARDENING

Primero veos en la máquina Lamp está levantado están los seguridad
![[Pasted-image-20241113164146.png]]Suponemos que no conocemos la ip, el primer paso sería hacer un nmap con la máscara de red.
nmap 172.22.0.0/16 
En nuestro caso lo haremos ya 