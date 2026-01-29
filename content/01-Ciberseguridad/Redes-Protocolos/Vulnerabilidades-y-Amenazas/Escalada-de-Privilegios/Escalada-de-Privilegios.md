---
title: "Escalada De Privilegios"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Escalada de Privilegios – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]]. [[01-Ciberseguridad/Herramientas/Hydra|Hydra]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/John-the-Ripper|John the Ripper]].

**Escalada de privilegios** es la fase de un ataque en la que un atacante que ha obtenido acceso limitado a un sistema (por ejemplo, como usuario sin privilegios) **intenta conseguir permisos más altos**, típicamente **privilegios de administrador o root**.

Es una fase crítica que suele ocurrir **después de haber conseguido una shell** y **antes de realizar acciones sensibles**, como extraer datos, desactivar protecciones o instalar malware persistente.

---

###  Tipos de escalada de privilegios

#### 1. **Escalada horizontal**

- Acceder a los recursos o cuentas de **otros usuarios del mismo nivel**.
    
- Ejemplo: un usuario común accede a carpetas de otro usuario.
    

#### 2. **Escalada vertical**

- Subir desde una cuenta limitada hasta una **con privilegios más altos** (root, SYSTEM, administrador).
    
- Es la forma más peligrosa y buscada.
    

---

###  Técnicas comunes de escalada de privilegios

####  1. **Fuerza bruta de contraseñas**

- Contra hashes de `/etc/shadow` o SAM de Windows.
    
- Herramientas: `John the Ripper`, `Hashcat`, `Hydra`.
    

####  2. **Errores de permisos en archivos**

- Archivos sensibles accesibles por usuarios comunes:
    
    - Ejemplo: `/etc/shadow` legible.
        
    - Archivos con permisos de escritura global (`777`).
        

```bash
find / -perm -0002 -type f 2>/dev/null
```

####  3. **Ficheros SUID mal configurados (Linux)**

- Archivos ejecutables que se ejecutan con los privilegios del **propietario**, no del usuario que los lanza.
    

```bash
find / -perm -4000 -type f 2>/dev/null
```

- Si un binario vulnerable tiene el bit SUID y pertenece a root → escalada garantizada.
    

####  4. **Exploit de vulnerabilidades locales**

- Desbordamientos en programas ejecutables por todos.
    
- Fallos en el kernel del sistema operativo.
    
- Vulnerabilidades conocidas con exploits públicos (CVE).
    

Ejemplo en Linux:

```bash
uname -a  # buscar versión del kernel
searchsploit Linux Kernel 4.15  # buscar exploits
```

####  5. **Abuso de servicios mal configurados**

- **Cron jobs** ejecutados con privilegios elevados y editables por el usuario.
    
- **Servicios systemd** que se lanzan como root con scripts modificables.
    
- **Tareas programadas (Windows Task Scheduler)** con comandos mal protegidos.
    

####  6. **Enumeración del sistema**

Antes de escalar, el atacante **analiza el entorno** para encontrar pistas:

- Usuarios actuales: `whoami`, `id`
    
- Archivos interesantes: `.bash_history`, `.ssh`, backups
    
- Procesos y servicios en ejecución
    
- Versiones de paquetes instalados
    

Herramientas:

- **Linux**: `LinPEAS`, `Linux Exploit Suggester`, `GTFOBins`, `sudo -l`
    
- **Windows**: `winPEAS`, `PowerUp`, `Seatbelt`
    

####  7. **Uso abusivo de sudo (Linux)**

```bash
sudo -l
```

- Si el usuario puede ejecutar algún comando como root, puede escalar.
    

Ejemplo:

```bash
sudo less /etc/shadow
```

→ Se puede invocar `!bash` desde dentro de `less`.

---

###  Ejemplo real: Escalada mediante archivo SUID vulnerable

1. Se encuentra un binario SUID:
    

```bash
-rwsr-xr-x 1 root root 123456 /usr/bin/vulnprog
```

2. El binario es vulnerable a buffer overflow o permite ejecutar comandos arbitrarios.
    
3. El atacante ejecuta:
    

```bash
/usr/bin/vulnprog  # y lanza shell
```

Resultado: shell con permisos de root (`id → uid=0(root)`)

---

###  Contramedidas para prevenir la escalada

|Área|Medida defensiva|
|---|---|
|Archivos|Revisar permisos, evitar SUID innecesarios|
|Usuarios|Aplicar principio de mínimo privilegio|
|Servicios|Aislar servicios y tareas programadas|
|Auditar|Buscar SUID, cron jobs, contraseñas débiles|
|Kernel / Software|Mantener el sistema actualizado|
|Detección|Monitorizar acciones sospechosas (IDS/HIDS, Sysmon)|
|Linux|Desactivar ejecución en stack y heap (`noexec`)|

---

###  Herramientas clave

|Sistema|Herramientas|
|---|---|
|Linux|`LinPEAS`, `sudo -l`, `GTFOBins`, `pspy`, `exploit-db`, `Linux Exploit Suggester`|
|Windows|`winPEAS`, `PowerUp`, `Seatbelt`, `AccessChk`, `SharpUp`, `PrivescCheck`|

---

### Conclusión

La **escalada de privilegios es lo que convierte a un atacante en administrador del sistema**. A menudo es el paso intermedio más difícil, pero más recompensante. Para los defensores, es una prioridad **detectar esta actividad rápidamente** y asegurar el sistema para que un acceso inicial no implique una toma total de control.

---

¿Quieres que prepare una demo paso a paso con `LinPEAS` o `winPEAS`, o cómo explotar un binario SUID en un entorno de laboratorio?