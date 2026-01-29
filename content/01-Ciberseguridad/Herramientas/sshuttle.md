---
title: "Uso de sshuttle para crear una VPN"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
`sshuttle` es una herramienta útil para crear una **VPN** (Virtual Private Network) de forma sencilla a través de un túnel SSH. A diferencia de otras herramientas, no requiere instalación de software adicional en el servidor remoto; simplemente necesitas acceso SSH y Python.

A continuación, te mostraré cómo usar `sshuttle` para redirigir todo tu tráfico de red (o solo tráfico específico) a través de un servidor remoto.

## ¿Qué es `sshuttle`?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

`sshuttle` es una herramienta de "VPN transparente" que redirige el tráfico de tu red local a través de un servidor remoto usando una conexión SSH. Funciona de manera similar a un túnel SSH, pero también maneja las rutas y el tráfico de red a través del servidor remoto.

### ¿Cómo funciona?
- Utiliza el túnel SSH para crear un proxy a nivel de red.
- Redirige todo o parte del tráfico de red de tu máquina local a través del servidor remoto, lo que te permite navegar como si estuvieras en la red remota (por ejemplo, como si estuvieras dentro de una red corporativa o accediendo a contenido bloqueado geográficamente).

## Instalación de `sshuttle`

### En Linux
Puedes instalar `sshuttle` desde el repositorio de tu distribución. Para las distribuciones basadas en Debian/Ubuntu:

```bash
sudo apt update
sudo apt install sshuttle
```

En distribuciones basadas en Red Hat/CentOS (o Fedora):

```bash
sudo dnf install sshuttle
```

En **Arch Linux**:

```bash
sudo pacman -S sshuttle
```

### En macOS
Si usas macOS y tienes Homebrew instalado, puedes instalar `sshuttle` con el siguiente comando:

```bash
brew install sshuttle
```

### En Windows
En Windows, necesitarás tener un entorno que soporte herramientas de línea de comandos como **Windows Subsystem for Linux (WSL)** o **Cygwin** para usar `sshuttle`, ya que no está disponible de manera nativa. Una vez que hayas instalado uno de esos entornos, puedes seguir las instrucciones de Linux.

## Uso básico de `sshuttle`

Una vez que hayas instalado `sshuttle`, puedes crear un túnel SSH para redirigir todo el tráfico o solo el tráfico de ciertas redes a través de un servidor remoto.

### Ejemplo 1: Redirigir todo el tráfico a través del servidor remoto

```bash
sshuttle -r usuario@servidor_remoto 0.0.0.0/0
```

- `-r usuario@servidor_remoto`: La dirección del servidor remoto (debe ser accesible a través de SSH).
- `0.0.0.0/0`: Significa que todo el tráfico IP será redirigido a través del servidor remoto.

### Ejemplo 2: Redirigir solo tráfico hacia una red específica

Si solo deseas redirigir el tráfico hacia una red en particular, puedes especificar esa red en lugar de `0.0.0.0/0`. Por ejemplo, para redirigir solo el tráfico hacia la red `192.168.1.0/24`:

```bash
sshuttle -r usuario@servidor_remoto 192.168.1.0/24
```

### Ejemplo 3: Usar una contraseña SSH (sin autenticación de clave)

Si prefieres usar una contraseña SSH en lugar de una clave SSH para autenticarte:

```bash
sshuttle -r usuario@servidor_remoto 0.0.0.0/0 --ssh-cmd 'sshpass -p "tu_contraseña" ssh'
```

Esto te permitirá autenticarte sin tener que usar una clave SSH.

### Ejemplo 4: Usar un puerto SSH personalizado

Si el servidor remoto utiliza un puerto SSH personalizado (por ejemplo, el puerto `2222` en lugar del predeterminado `22`), puedes especificarlo con la opción `-p`:

```bash
sshuttle -r usuario@servidor_remoto:2222 0.0.0.0/0
```

## Otras opciones útiles

- `-D` o `--dns`: Redirige también las consultas DNS a través del túnel.
- `-v` o `--verbose`: Modo verbose, para ver información detallada sobre lo que está haciendo `sshuttle`.
- `-x` o `--exclude`: Excluir ciertas direcciones IP o subredes del túnel.

Por ejemplo, para redirigir todo el tráfico excepto el de la red local `192.168.1.0/24`, usarías:

```bash
sshuttle -r usuario@servidor_remoto 0.0.0.0/0 -x 192.168.1.0/24
```

## Finalización de la conexión

Para detener el túnel de `sshuttle`, puedes usar `Ctrl+C` en el terminal donde lo ejecutaste. Esto terminará la sesión de `sshuttle` y restablecerá las rutas de red originales.

---

## Ejemplo práctico en Markdown

Aquí tienes un ejemplo práctico documentado en formato Markdown para usar en un archivo de documentación o README:

```markdown
# Uso de sshuttle para crear una VPN

## Instalación

### En Ubuntu/Debian

```bash
sudo apt update
sudo apt install sshuttle
```

### En macOS (usando Homebrew)

```bash
brew install sshuttle
```

## Usar sshuttle para redirigir tráfico

### Redirigir todo el tráfico a través de un servidor remoto

```bash
sshuttle -r usuario@servidor_remoto 0.0.0.0/0
```

### Redirigir tráfico solo hacia una red específica

```bash
sshuttle -r usuario@servidor_remoto 192.168.1.0/24
```

### Usar un puerto SSH personalizado

Si el servidor remoto usa un puerto SSH personalizado (por ejemplo, el puerto 2222):

```bash
sshuttle -r usuario@servidor_remoto:2222 0.0.0.0/0
```

### Redirigir DNS también

Si quieres que las consultas DNS pasen por el túnel:

```bash
sshuttle -r usuario@servidor_remoto 0.0.0.0/0 --dns
```

## Detener la conexión

Para finalizar el túnel, presiona `Ctrl+C`.
```

Este ejemplo cubre las configuraciones básicas y algunos casos más específicos para que puedas documentar o utilizar `sshuttle` según tus necesidades.