---
title: "Scp Copia De Archivos De Forma Remota"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
### Comando SCP (Secure Copy): Transferencia Segura de Archivos entre Sistemas


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

**SCP** (Secure Copy Protocol) es una herramienta de línea de comandos que permite copiar archivos y directorios de manera segura entre dos ubicaciones. Utiliza el protocolo **SSH** (Secure Shell) tanto para la autenticación como para la encriptación, lo que garantiza que los archivos y las contraseñas estén protegidos durante la transferencia. SCP es comúnmente utilizado para transferir datos entre sistemas locales y remotos, o entre dos sistemas remotos, con el beneficio adicional de la encriptación para evitar accesos no autorizados durante la transferencia.

Este tutorial explica cómo usar el comando SCP con ejemplos prácticos y detalla las opciones más comunes de este comando.

---

### **Sintaxis Básica del Comando SCP**

La sintaxis básica del comando SCP es la siguiente:

```bash
scp [OPCIÓN] [usuario@]SRC_HOST:]archivo1 [usuario@]DEST_HOST:]archivo2
```

- **OPCIÓN**: Opciones para modificar el comportamiento de SCP (como compresión, puerto SSH, copia recursiva, etc.).
- **[usuario@]SRC_HOST:]archivo1**: Ruta al archivo fuente. Se debe incluir el nombre de usuario y la dirección IP (o el nombre de host) del sistema de origen cuando el archivo esté en una máquina remota.
- **[usuario@]DEST_HOST:]archivo2**: Ruta al archivo destino. Se debe incluir el nombre de usuario y la dirección IP (o el nombre de host) del sistema de destino cuando el archivo esté en una máquina remota.

Los archivos locales pueden especificarse usando una ruta absoluta o relativa, mientras que los archivos remotos requieren el nombre de usuario y la dirección del host.

---

### **Opciones Comunes de SCP**

SCP proporciona varias opciones que controlan diversos aspectos de su comportamiento. Algunas de las más comúnmente utilizadas son:

- **`-P`**: Especifica el puerto SSH del host remoto (nota que el `P` es mayúscula).
- **`-p`**: Preserva los tiempos de modificación y acceso de los archivos.
- **`-q`**: Suprime el medidor de progreso y los mensajes no relacionados con errores (modo silencioso).
- **`-C`**: Habilita la compresión durante la transferencia de datos, útil para archivos grandes.
- **`-r`**: Copia directorios de manera recursiva, asegurando que todos los archivos y subdirectorios se incluyan.
- **`-i`**: Especifica una clave privada para la autenticación (si se usa autenticación por clave SSH).

---

### **Ejemplos Básicos del Comando SCP**

#### **1. Copiar un Archivo Local a un Sistema Remoto**

Para copiar un archivo desde tu máquina local a un servidor remoto:

```bash
scp archivo.txt usuario_remoto@10.10.0.2:/directorio/remoto
```

Donde:
- **archivo.txt** es el archivo que deseas copiar.
- **usuario_remoto** es el nombre de usuario en el servidor remoto.
- **10.10.0.2** es la dirección IP del servidor remoto.
- **/directorio/remoto** es la ruta en el sistema remoto donde quieres copiar el archivo.

Si no especificas un directorio remoto, el archivo se copiará al directorio home del usuario remoto.

#### **2. Copiar un Archivo desde un Sistema Remoto a tu Sistema Local**

Para copiar un archivo desde un servidor remoto a tu máquina local:

```bash
scp usuario_remoto@10.10.0.2:/directorio/remoto/archivo.txt /directorio/local
```

Donde:
- **usuario_remoto@10.10.0.2:/directorio/remoto/archivo.txt** es la ruta al archivo en el servidor remoto.
- **/directorio/local** es el directorio en tu sistema local donde se copiará el archivo.

Se te pedirá la contraseña del usuario remoto, a menos que tengas configurada una autenticación sin contraseña mediante claves SSH.

#### **3. Copiar un Directorio Recursivamente**

Para copiar un directorio completo y su contenido, utiliza la opción **`-r`** (recursiva):

```bash
scp -r /directorio/local usuario_remoto@10.10.0.2:/directorio/remoto
```

La opción **`-r`** asegura que todos los archivos y subdirectorios dentro del directorio sean copiados.

#### **4. Copiar un Archivo entre Dos Sistemas Remotos**

Puedes copiar archivos directamente entre dos sistemas remotos sin necesidad de iniciar sesión en uno de ellos. Por ejemplo:

```bash
scp usuario1@host1.com:/archivos/archivo.txt usuario2@host2.com:/archivos
```

En este caso:
- El archivo **archivo.txt** se copiará desde **host1.com** a **host2.com**.
- Se te pedirá ingresar las contraseñas para ambas cuentas remotas.

#### **5. Especificar un Puerto SSH Personalizado**

Si el servidor SSH del sistema remoto está utilizando un puerto diferente al puerto predeterminado (22), puedes especificarlo utilizando la opción **`-P`** (mayúscula):

```bash
scp -P 2322 archivo.txt usuario_remoto@10.10.0.2:/directorio/remoto
```

Donde **2322** es el puerto SSH personalizado.

#### **6. Preservar los Metadatos de los Archivos**

Para preservar los metadatos de los archivos, como la fecha de modificación y la propiedad, utiliza la opción **`-p`**:

```bash
scp -p archivo.txt usuario_remoto@10.10.0.2:/directorio/remoto
```

Esto asegura que se mantengan las marcas de tiempo y los permisos del archivo original al llegar al destino.

#### **7. Usar Comodines para Copiar Múltiples Archivos**

Puedes usar caracteres comodín (como `*` o `?`) para coincidir con archivos o directorios específicos. Para evitar la expansión del shell, encierra el patrón en comillas:

```bash
scp "~Proyectos/*.txt" usuario_remoto@10.10.0.2:/home/usuario/Proyectos/
```

Esto copia todos los archivos `.txt` del directorio local **Proyectos** al directorio **Proyectos** en el sistema remoto.

---

### **Antes de Comenzar: Requisitos Previos para Usar SCP**

- **Autenticación SSH**: SCP depende de SSH para la transferencia de datos, por lo que necesitas una clave SSH o una contraseña para la autenticación.
- **Permisos**: Necesitas tener permisos de lectura sobre el archivo de origen y permisos de escritura en el sistema de destino.
- **Cuidado con Sobrescribir Archivos**: SCP sobrescribirá archivos en el destino sin advertencia si el nombre y la ubicación del archivo coinciden.
- **Archivos Grandes**: Para transferir archivos grandes, se recomienda ejecutar SCP dentro de una sesión **screen** o **tmux** para evitar interrupciones.

---

### **Conclusión**

SCP es una forma rápida, segura y confiable de copiar archivos entre sistemas Linux y Unix. Al usar la encriptación SSH, garantiza la privacidad e integridad de tus datos. La simplicidad de SCP lo convierte en una excelente opción para transferir archivos a través de redes.

Si buscas una solución más eficiente, puedes configurar autenticación basada en claves SSH para evitar ingresar contraseñas repetidamente, especialmente si te conectas regularmente a los mismos sistemas. También puedes simplificar tu flujo de trabajo definiendo tus conexiones comunes en el archivo de configuración de SSH.

### Puntos Clave:
- **SCP** garantiza la transferencia segura de archivos utilizando el protocolo **SSH**.
- La opción **`-r`** se usa para copiar directorios de manera recursiva.
- La opción **`-P`** se usa para especificar un puerto SSH personalizado.
- Se pueden preservar los metadatos del archivo utilizando la opción **`-p`**.
- Es posible transferir archivos directamente entre dos sistemas remotos sin necesidad de iniciar sesión en ninguno de ellos.

LInk :
https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/