---
title: "Tailscale"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - gestionservidores
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[06-Infraestructura/Servidores/GestionServidores/Proxmox|Proxmox]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

Tailscale sobre WireGuard: VPN fácil de configurar y segura

Tailscale es una solución de VPN moderna que utiliza WireGuard como protocolo subyacente para crear redes privadas seguras entre dispositivos, pero con un enfoque simplificado y orientado al usuario. A continuación te explico cómo funciona y cómo puedes configurarlo en tu infraestructura.

1. ¿Qué es Tailscale?

Tailscale es una herramienta de VPN basada en el protocolo WireGuard, diseñada para crear una red privada virtual de manera fácil y sin necesidad de complicados procedimientos de configuración. WireGuard es un protocolo VPN conocido por ser seguro y eficiente, y Tailscale lo utiliza como base para crear redes privadas entre dispositivos, sin requerir configuración de enrutadores, firewalls o direcciones IP manuales.

Características de Tailscale:

Fácil configuración: Puedes conectar múltiples dispositivos en minutos sin necesidad de modificar la infraestructura de red ni abrir puertos manualmente.

Seguridad avanzada: Utiliza WireGuard, que es conocido por su alto rendimiento y seguridad.

Red privada global: Tailscale crea una red privada entre tus dispositivos, de forma que pueden comunicarse de forma segura entre sí, independientemente de la red local a la que estén conectados.

Acceso remoto: Puedes acceder de forma remota a tus dispositivos de forma segura sin necesidad de configuraciones complicadas.


2. ¿Cómo funciona Tailscale sobre WireGuard?

WireGuard es un protocolo de red que cifra el tráfico de red entre dispositivos para proteger la privacidad de las comunicaciones. Tailscale usa WireGuard para proporcionar una conexión privada entre los dispositivos, pero añade una capa de simplicidad y escalabilidad.

WireGuard en sí mismo requiere que configures las claves públicas y privadas de cada dispositivo y las configuraciones de las redes manualmente, lo cual puede ser complejo.

Tailscale simplifica este proceso gestionando automáticamente las claves y las conexiones, y utilizando NAT traversal para garantizar que los dispositivos se conecten entre sí incluso si están detrás de firewalls o redes NAT (como una red doméstica).


Tailscale agrega varias ventajas sobre el uso directo de WireGuard:

1. Facilidad de conexión: Al registrarse en Tailscale, cada dispositivo obtiene una identidad única y puede conectarse automáticamente con otros dispositivos de la red sin tener que configurar las direcciones IP ni claves manualmente.


2. Escalabilidad: Puedes conectar fácilmente cientos de dispositivos sin tener que gestionar manualmente cada uno.


3. Control centralizado: Tailscale gestiona las conexiones y configuraciones de red a través de un servidor de control centralizado, que simplifica la administración de la red privada.



4. Instalación de Tailscale en Proxmox (o cualquier sistema Linux)

Tailscale es compatible con muchos sistemas operativos, incluidos Linux, macOS, Windows, Android y iOS. Aquí te guiaré para instalar Tailscale en un servidor Linux (puede ser tu Proxmox o cualquier otra máquina basada en Linux).

Pasos para instalar Tailscale en Linux (Proxmox o cualquier distribución):

1. Instalar Tailscale:

En una máquina Linux (por ejemplo, una VM en Proxmox o un servidor físico), puedes instalar Tailscale usando los siguientes comandos:


Para Debian/Ubuntu:

curl -fsSL https://tailscale.com/install.sh | sh

Para CentOS/Fedora:

sudo yum install https://pkgs.tailscale.com/stable/tailscale_1.14.0_amd64.rpm


2. Iniciar el servicio Tailscale: Una vez que Tailscale esté instalado, inicia el servicio:

sudo systemctl enable --now tailscale


3. Autenticación con Tailscale: El siguiente paso es autenticarte en Tailscale. Esto se puede hacer con tu cuenta de Google, GitHub, o cualquier otro proveedor soportado.

sudo tailscale up

Esto abrirá un enlace en tu navegador para que inicies sesión y autorices el dispositivo. Después de autorizarlo, Tailscale se conectará a tu red privada.


4. Verificar la conexión: Para verificar que tu dispositivo está correctamente conectado a la red privada, puedes usar:

tailscale status

Esto mostrará los dispositivos conectados y sus direcciones IP dentro de la red privada Tailscale.



4. Conectar varios dispositivos a la red de Tailscale

Una vez que hayas instalado Tailscale en todos los dispositivos que quieres conectar, puedes comenzar a interactuar entre ellos de forma segura. Para hacerlo:

1. Instala Tailscale en los demás dispositivos (computadoras, teléfonos, otros servidores).


2. En la interfaz de Tailscale, verás una lista de todos los dispositivos conectados. Puedes acceder a ellos utilizando sus direcciones IP privadas asignadas por Tailscale.



3. Acceder a tu Proxmox de forma remota a través de Tailscale

Si tienes Proxmox corriendo y deseas acceder a la interfaz web de Proxmox de manera remota a través de Tailscale, simplemente sigue estos pasos:

1. Instala Tailscale en la máquina desde donde accederás (por ejemplo, tu laptop o dispositivo móvil).


2. Conecta Proxmox al grupo de red privada Tailscale.


3. Accede a la interfaz web de Proxmox a través de su IP privada Tailscale, por ejemplo:

https://<IP_de_tu_servidor_Tailscale>:8006



De esta manera, puedes acceder a la interfaz web de Proxmox o cualquier otro servicio interno de tu red privada de manera segura y encriptada, sin exponer las IPs públicas de tu red.

6. Configuraciones adicionales (opcional)

Acceso de dispositivos móviles: Puedes instalar Tailscale en tu teléfono móvil (disponible para iOS y Android) y acceder a los servicios internos de tu red privada sin importar en qué red estés.

Redes divididas por subredes: Tailscale te permite crear redes privadas virtuales (VPNs) entre dispositivos sin necesidad de definir manualmente las direcciones IP. De esta forma, no tienes que preocuparte de gestionar redes y direcciones IP internas.



---

Conclusión

Tailscale es una solución simple y eficiente para establecer redes privadas seguras entre tus dispositivos utilizando el protocolo WireGuard. Puedes usarlo para acceder de manera remota a tu infraestructura de Proxmox y otros servicios internos de forma segura, sin la complejidad de configuraciones tradicionales de VPN. Además, Tailscale maneja automáticamente las claves, la configuración de las redes y el enrutamiento, lo que te permite gestionar tu infraestructura de red de forma sencilla y segura.

Si necesitas más detalles sobre la configuración de Tailscale o tienes preguntas específicas, no dudes en pedírmelo. ¡Estoy aquí para ayudarte!

