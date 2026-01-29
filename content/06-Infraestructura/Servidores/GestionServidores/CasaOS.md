---
title: "Casaos"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - gestionservidores
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[06-Infraestructura/Servidores/GestionServidores/Bitwarden|Bitwarden]].

CasaOS es un sistema operativo ligero y de código abierto diseñado para convertir cualquier ordenador (especialmente un mini-PC como una Raspberry Pi, Intel NUC o similares) en un servidor doméstico inteligente y personalizable. Su objetivo es proporcionar una alternativa fácil, visual y amigable para usuarios no técnicos que desean alojar servicios y aplicaciones en casa, al estilo de un “Google Drive”, “Netflix”, o centro multimedia privado”.


---

 ¿Qué es exactamente CasaOS?

CasaOS es una plataforma que se instala sobre sistemas basados en Linux (por ejemplo, Debian o Ubuntu) y proporciona una interfaz web sencilla y minimalista desde donde puedes gestionar fácilmente contenedores y aplicaciones, sin necesidad de aprender comandos complicados de Docker o Linux.


---

️ Características principales

Instalación sencilla (una sola línea de comando).

Interfaz web moderna y fácil de usar.

Basado en Docker, lo que permite ejecutar cientos de aplicaciones en contenedores (Nextcloud, Jellyfin, Home Assistant, Bitwarden, etc.).

Gestor de archivos tipo Google Drive, accesible por web.

Soporte para discos duros externos.

Gestión de red y almacenamiento local.

Acceso remoto (puedes conectarte desde cualquier lugar).

Seguridad básica con autenticación y HTTPS.



---

 Ejemplos de cosas que puedes montar con CasaOS

1. Tu propio Google Drive → con Nextcloud


2. Tu Netflix personal → con Jellyfin


3. Tu Spotify casero → con Navidrome


4. Tu gestor de contraseñas → con Bitwarden_rs / Vaultwarden


5. Tu consola de juegos retro → con RetroArch


6. Tu gestor de descargas torrent → con qBittorrent


7. Home Assistant para automatización del hogar.




---

 Instalación rápida

Puedes instalar CasaOS en una máquina con Debian/Ubuntu ejecutando:

curl -fsSL https://get.casaos.io | bash

Esto descargará y ejecutará el script que instala todos los servicios necesarios.


---

 Requisitos mínimos

Un equipo con arquitectura x86_64 o ARM64 (como Raspberry Pi 4).

Sistema operativo base: Debian/Ubuntu Server.

Docker instalado (el script lo instala automáticamente).

Acceso a Internet.



---

 Interfaz Web

Una vez instalado, puedes acceder desde el navegador con la IP de la máquina en el puerto 80:

http://<IP-de-tu-servidor>

Desde ahí puedes:

Ver el estado del sistema (CPU, RAM, disco, red).

Instalar apps desde una App Store visual.

Ver y gestionar archivos locales.

Añadir discos externos.

Administrar contenedores Docker sin saber Docker.



---

 Ampliación y comunidad

CasaOS tiene soporte para plugins y extensiones.

Puedes instalar cualquier contenedor Docker manualmente.

La comunidad es activa y hay múltiples tutoriales en su GitHub, Reddit y Discord.

Actualizaciones frecuentes y mejoras continuas.



---

 Seguridad

Aunque CasaOS es accesible por web, es recomendable:

Activar HTTPS.

Usar una contraseña segura.

No exponer el puerto 80 al exterior sin protección.

Usar una VPN (como Tailscale o WireGuard) si quieres acceder desde fuera de casa.



---

 ¿Para qué tipo de usuario es ideal CasaOS?

Usuarios sin experiencia en administración de servidores.

Entusiastas del DIY que quieren montar su propio servidor doméstico.

Gente que busca una alternativa privada a los servicios en la nube.

Quienes desean controlar sus propios datos sin depender de grandes empresas.



---

¿Quieres que te ayude a montar uno en tu Proxmox, VPS o Raspberry Pi? Puedo guiarte paso a paso según el entorno que tengas.

