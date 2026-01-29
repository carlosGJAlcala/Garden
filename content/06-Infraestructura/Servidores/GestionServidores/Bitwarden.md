---
title: "Guía para Instalar Bitwarden Gratuito en Proxmox"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - gestionservidores
---
Tu guía para instalar Bitwarden gratuito en Proxmox está bastante completa, pero contiene algunos errores y omisiones que pueden dificultar su seguimiento, especialmente para usuarios menos experimentados. A continuación, corregiré y mejoraré los pasos, aclararé conceptos, optimizaré el proceso y expandiré la información para hacerlo más claro y detallado, manteniendo la esencia de tu propuesta. También corregiré errores técnicos y gramaticales, y añadiré recomendaciones de seguridad y mejores prácticas.

---

# Guía para Instalar Bitwarden Gratuito en Proxmox


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/DHCP|DHCP]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]].

Bitwarden es un gestor de contraseñas de código abierto que permite almacenar y gestionar contraseñas de forma segura. Al instalarlo en Proxmox, un hipervisor basado en Debian para gestionar máquinas virtuales (VM) y contenedores LXC, puedes tener un servidor privado y controlado. La implementación más ligera y recomendada para entornos autohospedados es **Vaultwarden** (anteriormente Bitwarden_RS), ya que es más eficiente en recursos que la versión oficial de Bitwarden, especialmente para servidores pequeños.

**Nota**: Vaultwarden es una alternativa no oficial escrita en Rust, compatible con las aplicaciones oficiales de Bitwarden, pero usa menos recursos. La versión oficial de Bitwarden requiere más dependencias y es más pesada, por lo que Vaultwarden es ideal para Proxmox.

---

## 1. Requisitos Previos

Antes de comenzar, asegúrate de tener:

- Un servidor con **Proxmox VE** instalado (versión recomendada: 7.x o superior).
- Acceso a la interfaz web de Proxmox (por defecto en `https://<IP_PROXMOX>:8006`).
- Conexión a internet para descargar paquetes y Vaultwarden.
- Conocimientos básicos de Linux y comandos de terminal.
- Recursos mínimos sugeridos:
  - **Contenedor LXC**: 1 vCPU, 512 MB-1 GB de RAM, 10 GB de almacenamiento.
  - **Máquina virtual**: 1 vCPU, 1-2 GB de RAM, 20 GB de almacenamiento.
- Opcional: Un dominio o subdominio (ej. `vaultwarden.tudominio.com`) para acceso remoto y configuración de HTTPS.

---

## 2. Opciones de Despliegue en Proxmox

Puedes instalar Vaultwarden en Proxmox de dos formas principales:

1. **Contenedor LXC**: Más ligero, eficiente y recomendado para servidores pequeños.
2. **Máquina virtual (VM)**: Más aislada, pero consume más recursos.

**Recomendación**: Usa un contenedor LXC para Vaultwarden, ya que es más eficiente. Una VM es útil si necesitas aislamiento completo o planeas instalar otras aplicaciones en el mismo sistema.

---

## 3. Instalación de Vaultwarden en un Contenedor LXC

### 3.1. Crear un Contenedor LXC en Proxmox

1. **Accede a la interfaz web de Proxmox** (`https://<IP_PROXMOX>:8006`).
2. Ve a **Datacenter > Tu nodo > Create CT**.
3. Configura el contenedor:
   - **Template**: Selecciona una plantilla de Ubuntu (recomendado: Ubuntu 22.04 LTS).
   - **Hostname**: Por ejemplo, `vaultwarden-ct`.
   - **Recursos**:
     - CPU: 1 núcleo.
     - RAM: 512 MB (1 GB para mejor rendimiento).
     - Disco: 10 GB (ajusta según necesidades).
   - **Red**: Asigna una IP estática o usa DHCP.
   - Habilita **Nesting** (en la pestaña Options) para soporte de Docker, si planeas usarlo.
4. Finaliza la creación y arranca el contenedor.

### 3.2. Configurar el Contenedor

1. Accede al contenedor desde la consola de Proxmox o vía SSH:
   ```bash
   ssh <usuario>@<IP_CONTENEDOR>
   ```
   Por defecto, el usuario es `root` y la contraseña la estableciste al crear el contenedor.

2. Actualiza el sistema:
   ```bash
   apt update && apt upgrade -y
   ```

3. Instala dependencias básicas:
   ```bash
   apt install -y curl wget sudo nano
   ```

---

## 4. Instalación de Vaultwarden

**Nota**: Tu guía menciona una versión antigua de Bitwarden_RS (`v1.21.0`). Desde 2021, Bitwarden_RS se renombró como **Vaultwarden**, y se recomienda usar la última versión. Además, el método de instalación directa con un binario descargado no es el más común; Vaultwarden se instala frecuentemente con **Docker** para simplificar actualizaciones y gestión.

### 4.1. Instalación con Docker (Método Recomendado)

Docker es la forma más práctica de instalar Vaultwarden, ya que gestiona dependencias y facilita actualizaciones. Si prefieres evitar Docker, consulta la sección 4.2 para instalación manual.

#### 4.1.1. Instalar Docker

1. Instala Docker en el contenedor:
   ```bash
   apt install -y docker.io
   systemctl enable docker
   systemctl start docker
   ```

2. Verifica que Docker esté corriendo:
   ```bash
   docker --version
   ```

#### 4.1.2. Desplegar Vaultwarden con Docker

1. Crea un directorio para los datos de Vaultwarden:
   ```bash
   mkdir /opt/vaultwarden
   ```

2. Ejecuta el contenedor de Vaultwarden:
   ```bash
   docker run -d \
     --name vaultwarden \
     -v /opt/vaultwarden:/data \
     -p 80:80 \
     --restart unless-stopped \
     vaultwarden/server:latest
   ```

   - **Explicación**:
     - `-d`: Ejecuta el contenedor en segundo plano.
     - `-v /opt/vaultwarden:/data`: Persiste los datos en el host.
     - `-p 80:80`: Mapea el puerto 80 del contenedor al puerto 80 del host.
     - `--restart unless-stopped`: Reinicia el contenedor automáticamente salvo que se detenga manualmente.
     - `vaultwarden/server:latest`: Imagen oficial de Vaultwarden.

3. Verifica que el contenedor esté corriendo:
   ```bash
   docker ps
   ```

4. Accede a Vaultwarden desde un navegador:
   - URL: `http://<IP_CONTENEDOR>:80`
   - Crea una cuenta de administrador para empezar a usar Vaultwarden.

#### 4.1.3. Configuración Avanzada (Opcional)

- **Variables de entorno**: Puedes personalizar Vaultwarden añadiendo variables al comando `docker run`. Por ejemplo:
  ```bash
  docker run -d \
    --name vaultwarden \
    -v /opt/vaultwarden:/data \
    -p 80:80 \
    -e ROCKET_PORT=80 \
    -e ADMIN_TOKEN=tu_token_secreto \
    --restart unless-stopped \
    vaultwarden/server:latest
  ```
  - `ADMIN_TOKEN`: Habilita el panel de administración en `/admin`. Usa un token seguro.
  - `ROCKET_PORT`: Cambia el puerto interno si es necesario.

- **Actualizaciones**: Para actualizar Vaultwarden:
  ```bash
  docker pull vaultwarden/server:latest
  docker stop vaultwarden
  docker rm vaultwarden
  # Vuelve a ejecutar el comando docker run anterior
  ```

---

### 4.2. Instalación Manual (Sin Docker)

Si no deseas usar Docker, puedes instalar Vaultwarden directamente. Este método es menos común pero válido.

1. Descarga la última versión de Vaultwarden:
   ```bash
   wget https://github.com/dani-garcia/vaultwarden/releases/latest/download/vaultwarden -O /usr/local/bin/vaultwarden
   chmod +x /usr/local/bin/vaultwarden
   ```

2. Crea un directorio para datos y configuración:
   ```bash
   mkdir /opt/vaultwarden
   ```

3. Crea un archivo de configuración (opcional):
   ```bash
   nano /opt/vaultwarden/.env
   ```
   Ejemplo de contenido:
   ```env
   DATA_FOLDER=/opt/vaultwarden
   ROCKET_PORT=80
   ADMIN_TOKEN=tu_token_secreto
   ```

4. Ejecuta Vaultwarden:
   ```bash
   vaultwarden
   ```

5. Para ejecutarlo como servicio, crea un archivo systemd:
   ```bash
   nano /etc/systemd/system/vaultwarden.service
   ```
   Contenido:
   ```ini
   [Unit]
   Description=Vaultwarden Password Manager
   After=network.target

   [Service]
   ExecStart=/usr/local/bin/vaultwarden
   WorkingDirectory=/opt/vaultwarden
   EnvironmentFile=/opt/vaultwarden/.env
   Restart=always
   User=nobody
   Group=nogroup

   [Install]
   WantedBy=multi-user.target
  
```` 
```

```
6. Habilita e inicia el servicio:
   ```bash
   systemctl enable vaultwarden
   systemctl start vaultwarden
   ```

7. Accede a `http://<IP_CONTENEDOR>:80`.

---

## 5. Configuración de HTTPS (Altamente Recomendado)

Para proteger las comunicaciones, configura HTTPS usando un proxy inverso como **Caddy** o **Nginx** con un certificado SSL de **Let's Encrypt**.

### 5.1. Usar Caddy (Método Simple)

1. Instala Caddy:
   ```bash
   apt install -y debian-keyring debian-archive-keyring apt-transport-https
   curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | apt-key add -
   curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | tee /etc/apt/sources.list.d/caddy-stable.list
   apt update
   apt install -y caddy
   ```

2. Configura Caddy para Vaultwarden:
   ```bash
   nano /etc/caddy/Caddyfile
   ```
   Contenido:
   ```caddy
   vaultwarden.tudominio.com {
       reverse_proxy localhost:80
   }
   ```

3. Asegúrate de que tu dominio apunte a la IP de tu servidor (configura DNS en tu proveedor).
4. Reinicia Caddy:
   ```bash
   systemctl restart caddy
   ```

Caddy obtendrá automáticamente un certificado SSL de Let's Encrypt.

---

## 6. Acceso Remoto y Seguridad

- **Acceso remoto**: Para acceder a Vaultwarden desde fuera de tu red local:
  - Configura un dominio o subdominio (ej. `vaultwarden.tudominio.com`) y abre el puerto 80 (o 443 para HTTPS) en tu router.
  - Usa una VPN (como WireGuard en Proxmox) para acceso seguro sin exponer puertos.
  
- **Medidas de seguridad**:
  - Habilita un **ADMIN_TOKEN** para el panel de administración.
  - Usa contraseñas fuertes para la cuenta de administrador.
  - Configura un firewall en Proxmox (o en el contenedor) para limitar el acceso a puertos específicos (ej. 80, 443).
  - Realiza copias de seguridad regulares del directorio `/opt/vaultwarden`.
  - Mantén Vaultwarden y el sistema actualizados.

---

## 7. Comparación: Vaultwarden vs. Bitwarden Oficial

| **Característica**           | **Vaultwarden**                          | **Bitwarden Oficial**                   |
|------------------------------|------------------------------------------|-----------------------------------------|
| **Código**                   | Código abierto (Rust)                   | Código abierto (C#)                     |
| **Recursos**                 | Ligero (~100 MB RAM)                   | Pesado (~2 GB RAM)                     |
| **Dependencias**             | Mínimas (Docker o binario)             | Muchas (SQL Server, etc.)              |
| **Soporte oficial**          | Comunidad                              | Bitwarden, Inc.                        |
| **Funcionalidades**          | 95% de las funciones de Bitwarden       | 100% de las funciones                  |
| **Ideal para**               | Servidores pequeños, autohospedado     | Entornos empresariales                 |

**Recomendación**: Vaultwarden es ideal para Proxmox debido a su bajo consumo de recursos y facilidad de instalación.

---

## 8. Conclusión

Instalar Vaultwarden en Proxmox te permite gestionar contraseñas de forma segura y privada, con control total sobre tus datos. El uso de un contenedor LXC con Docker es el método más eficiente y escalable. Configurar HTTPS y medidas de seguridad es crucial para proteger tu instancia, especialmente si la expones a internet. Si necesitas más detalles sobre configuraciones avanzadas (como backups automáticos, monitoreo o integración con otras herramientas), no dudes en pedírmelo.

**Recursos adicionales**:
- Documentación oficial de Vaultwarden: [https://github.com/dani-garcia/vaultwarden](https://github.com/dani-garcia/vaultwarden)
- Foro de Proxmox: [https://forum.proxmox.com](https://forum.proxmox.com)
- Guía de Let's Encrypt: [https://letsencrypt.org](https://letsencrypt.org)

¿Necesitas ayuda con algún paso específico o quieres que profundice en algo, como la configuración de un dominio o una VPN?