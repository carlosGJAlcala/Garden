---
title: "Uso de rlwrap en Linux"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
`rlwrap` es una herramienta útil en Linux que proporciona una interfaz de línea de comandos mejorada con funcionalidades como **historial**, **autocompletado** y **edición de línea** (como en `bash` o `zsh`). Es una herramienta especialmente valiosa cuando usas programas que no tienen estas características de forma predeterminada.

### ¿Qué es `rlwrap`?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Bases-Datos/MongoDB|MongoDB]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

`rlwrap` básicamente "envuelve" otros programas de línea de comandos, proporcionándoles una capa de **Readline** para que puedas aprovechar características como:

- **Historial de comandos**: guarda los comandos anteriores y permite navegar por ellos con las teclas de flecha.
- **Autocompletado**: sugerencias y autocompletado para comandos y archivos.
- **Edición de línea**: permite editar la línea de comando de forma más avanzada.

Esto es especialmente útil cuando estás trabajando con programas como `telnet`, `ssh`, `redis-cli`, `mongo` o cualquier otra aplicación que no tenga por defecto soporte para estas funcionalidades.

### ¿Cómo instalar `rlwrap`?

#### En **Debian/Ubuntu** y derivados:

```bash
sudo apt update
sudo apt install rlwrap
```

#### En **Fedora**:

```bash
sudo dnf install rlwrap
```

#### En **Arch Linux**:

```bash
sudo pacman -S rlwrap
```

#### En **macOS** (con Homebrew):

```bash
brew install rlwrap
```

### Uso básico de `rlwrap`

`rlwrap` es fácil de usar: simplemente anteponlo al comando que deseas ejecutar. Aquí te dejo algunos ejemplos prácticos:

### Ejemplo 1: Usar `rlwrap` con `redis-cli`

Si estás interactuando con una base de datos de Redis, puedes usar `rlwrap` para mejorar la experiencia de línea de comandos:

```bash
rlwrap redis-cli
```

Esto te permitirá tener historial de comandos, autocompletado y otras funcionalidades que Redis no ofrece por defecto.

### Ejemplo 2: Usar `rlwrap` con `ssh`

Si te conectas a una máquina remota a través de SSH, también puedes usar `rlwrap` para agregar autocompletado y historial:

```bash
rlwrap ssh usuario@servidor_remoto
```

### Ejemplo 3: Usar `rlwrap` con `mongo`

Para interactuar con MongoDB a través de su shell, puedes usar `rlwrap` para habilitar las funcionalidades mencionadas:

```bash
rlwrap mongo
```

### Ejemplo 4: Usar `rlwrap` con cualquier comando

En general, puedes usar `rlwrap` con cualquier comando de consola que quieras envolver para obtener estas características. Por ejemplo:

```bash
rlwrap python
```

Esto lanzará el intérprete de Python, pero con la capacidad de usar las teclas de flecha para navegar por el historial y editar la línea de comandos.

### Configuración de `rlwrap`

#### Usar `rlwrap` permanentemente con un comando

Si deseas que un comando específico siempre use `rlwrap` sin tener que escribirlo cada vez, puedes crear un alias en tu archivo de configuración de shell (por ejemplo, `~/.bashrc` o `~/.zshrc`):

```bash
alias redis-cli='rlwrap redis-cli'
```

Después de agregar esto a tu archivo de configuración, recuerda recargar el archivo de configuración para que el alias sea efectivo:

```bash
source ~/.bashrc   # o ~/.zshrc si usas Zsh
```

#### Configuración avanzada

`rlwrap` tiene algunas opciones interesantes que puedes usar para personalizar su comportamiento:

- **Especificar un archivo de historial personalizado**:

    Puedes configurar `rlwrap` para que use un archivo de historial personalizado, como `~/.redis_history`:

    ```bash
    rlwrap -H ~/.redis_history redis-cli
    ```

- **Desactivar el historial**:

    Si no deseas que se guarde el historial de comandos, puedes usar la opción `-n`:

    ```bash
    rlwrap -n redis-cli
    ```

- **Habilitar autocompletado**:

    `rlwrap` también admite el autocompletado de comandos si se le proporciona un archivo de autocompletado. Por ejemplo, para habilitar el autocompletado con `redis-cli`, puedes usar:

    ```bash
    rlwrap -f /usr/share/doc/redis/examples/redis-cli.autocompletion redis-cli
    ```

---

### `rlwrap` en un contexto de desarrollo

Si eres un desarrollador o administras bases de datos y servidores, **`rlwrap`** es una herramienta bastante útil que te puede ayudar a mejorar tu flujo de trabajo cuando trabajas con aplicaciones de línea de comandos que carecen de las características estándar que ofrecen shells como `bash` o `zsh`.

---

## Ejemplo en Markdown

Aquí te dejo un ejemplo de cómo documentar el uso de `rlwrap` en un archivo de Markdown:

```markdown
# Uso de rlwrap en Linux

`rlwrap` es una herramienta que envuelve comandos de línea de comandos y les proporciona características como historial de comandos, autocompletado y edición de línea. Es útil cuando trabajas con programas que no tienen estas funcionalidades de forma predeterminada.

## Instalación

### En Ubuntu/Debian:

```bash
sudo apt update
sudo apt install rlwrap
```

### En Fedora:

```bash
sudo dnf install rlwrap
```

### En Arch Linux:

```bash
sudo pacman -S rlwrap
```

### En macOS (con Homebrew):

```bash
brew install rlwrap
```

## Uso Básico

### Usar `rlwrap` con `redis-cli`

```bash
rlwrap redis-cli
```

### Usar `rlwrap` con `mongo`

```bash
rlwrap mongo
```

### Usar `rlwrap` con cualquier otro comando

```bash
rlwrap python
```

## Opciones avanzadas

### Especificar un archivo de historial personalizado

```bash
rlwrap -H ~/.redis_history redis-cli
```

### Desactivar el historial

```bash
rlwrap -n redis-cli
```

### Habilitar autocompletado

```bash
rlwrap -f /usr/share/doc/redis/examples/redis-cli.autocompletion redis-cli
```
```

Con `rlwrap`, puedes mejorar significativamente la experiencia de uso de herramientas que normalmente no tienen soporte para características tan comunes como el historial de comandos o autocompletado.



La principal diferencia entre **`rlwrap`** y **`zsh`** radica en el **alcance** y el **propósito** de ambas herramientas. Mientras que `rlwrap` es una herramienta **externa** para agregar características a aplicaciones de línea de comandos que no las tienen, **`zsh`** es un **shell interactivo completo** con muchas características avanzadas de por sí. Aquí te doy una comparación más detallada:

## 1. **Propósito y Alcance**

### **`rlwrap`**:
- **Propósito**: `rlwrap` es una herramienta que envuelve programas de línea de comandos para proporcionarles funcionalidades de **edición de línea** y **historial de comandos** (gracias a la librería `Readline`), **autocompletado** y otras características.
- **Alcance**: `rlwrap` no es un **shell** en sí mismo. Es más bien una herramienta que se utiliza para mejorar la experiencia de línea de comandos de **otros programas** que no incluyen estas características de manera predeterminada.  
    Por ejemplo, puedes usar `rlwrap` con herramientas como `redis-cli`, `mongo`, `ssh`, `telnet`, o cualquier programa de consola que no tenga un mecanismo interno de edición de línea y autocompletado.
  
### **`zsh`**:
- **Propósito**: `zsh` (Z shell) es un **shell interactivo** completo y potente. Es un reemplazo más avanzado y configurable de `bash` (el shell predeterminado en muchas distribuciones de Linux). `zsh` incluye soporte nativo para muchas características avanzadas, como **historial de comandos**, **autocompletado**, **edición de línea** y **completado dinámico**, todo de manera integrada y muy configurable.
- **Alcance**: `zsh` es un shell completo que puedes usar para interactuar con tu sistema operativo. No solo proporciona características de autocompletado y edición de línea, sino que también ofrece:
  - **Plugins** y **temas** personalizables.
  - Soporte para **expansión de glóbulos** (glob expansion), **programación avanzada** en el shell, y mucho más.
  - Funciones de **historial avanzado** y **control de versiones** para el historial de comandos.

## 2. **Características**

### **`rlwrap`**:
- **Autocompletado**: Permite autocompletar comandos, archivos y opciones para cualquier programa que no tenga estas características por sí mismo.
- **Historial de comandos**: Guarda y navega a través de los comandos ejecutados en el contexto del programa envuelto.
- **Edición de línea**: Añade las teclas de edición de línea (como `Ctrl+A`, `Ctrl+E`, etc.) para editar el texto de manera eficiente.
- **Uso**: Ideal para usar con programas que no están diseñados para ser interactivos o no tienen un editor de línea potente integrado.

### **`zsh`**:
- **Autocompletado avanzado**: `zsh` ofrece un autocompletado altamente configurable, que incluye la capacidad de autocompletar comandos, archivos, variables y otros elementos del sistema.
- **Historial avanzado**: `zsh` tiene un historial de comandos mejorado que se puede usar entre sesiones, búsqueda interactiva de comandos anteriores y más.
- **Edición de línea avanzada**: Al igual que `bash` y otros shells, `zsh` soporta la edición de línea con atajos de teclado (`Ctrl+A`, `Ctrl+E`, etc.), pero con más opciones de personalización.
- **Plugins y temas**: Gracias a su ecosistema, `zsh` permite el uso de **frameworks** como **Oh My Zsh** que proporcionan temas y plugins para mejorar aún más la funcionalidad del shell.
- **Expansión de glóbulos**: Ofrece potentes características como el **globing avanzado**, que permite seleccionar archivos de manera más precisa.
- **Compatibilidad**: `zsh` puede ejecutar scripts escritos para `bash` y es más flexible en términos de configuración.

## 3. **Uso y Aplicaciones**

### **`rlwrap`**:
- Se usa para mejorar programas que no ofrecen características avanzadas de consola. Ejemplos típicos incluyen clientes como:
  - **`redis-cli`** (cliente para Redis)
  - **`mongo`** (cliente para MongoDB)
  - **`ssh`** (para sesiones SSH)
  - **`telnet`**
  
  Si un programa no tiene soporte para edición de línea y autocompletado, puedes envolverlo con `rlwrap` para hacerlo más amigable.

### **`zsh`**:
- `zsh` se usa como **shell interactivo** para trabajar en el terminal de tu sistema operativo.
  - Puedes usarlo como reemplazo de `bash` o `fish`.
  - Perfecto para usuarios que necesitan un entorno de línea de comandos más avanzado y personalizable.
  - Ideal para desarrolladores que prefieren un shell potente con autocompletado avanzado y soporte para plugins.

## 4. **Configuración**

### **`rlwrap`**:
- **Configuración mínima**: Solo necesitas ejecutar el comando deseado con `rlwrap` antepuesto:
  ```bash
  rlwrap redis-cli
  ```
- Si deseas, puedes configurar un archivo de historial o modificar el comportamiento de `rlwrap` usando opciones como `-H` para definir un archivo de historial o `-n` para desactivar el historial.

### **`zsh`**:
- **Configuración avanzada**: `zsh` tiene una amplia gama de opciones de configuración, que pueden ser personalizadas editando archivos como `~/.zshrc`.
  - Se pueden agregar **plugins** como **zsh-users/zsh-autosuggestions** para autocompletado predictivo, o **zsh-users/zsh-history-substring-search** para búsquedas avanzadas en el historial.
  - Los usuarios de `zsh` a menudo usan **Oh My Zsh**, un framework que hace que la configuración de `zsh` sea más fácil con temas y una gran cantidad de plugins.

## 5. **Ejemplo Comparativo**

### **`rlwrap` con `redis-cli`**:
```bash
rlwrap redis-cli
```
Aquí, `rlwrap` simplemente envuelve el cliente de Redis (`redis-cli`) y le añade características como **historial de comandos**, **autocompletado** y **edición de línea**.

### **`zsh`** con **`redis-cli`**:
Si usas `zsh` como tu shell, puedes disfrutar de características similares directamente en el shell, sin necesidad de envolver el comando con `rlwrap`:
```bash
zsh
redis-cli
```
En este caso, `zsh` ofrece autocompletado, edición de línea y un historial de comandos mucho más avanzado **sin necesidad de herramientas adicionales**.

---

## Resumen de Diferencias

| Característica          | **`rlwrap`**                                      | **`zsh`**                                         |
|-------------------------|---------------------------------------------------|---------------------------------------------------|
| **Propósito**            | Proporcionar características de Readline a programas externos | Shell interactivo completo con muchas características avanzadas |
| **Alcance**              | Se utiliza para envolver otros programas como `redis-cli`, `mongo`, `ssh`, etc. | Es un **shell completo** que reemplaza a `bash` |
| **Autocompletado**       | Solo para los programas que se envuelven con `rlwrap` | Integrado nativamente en el shell y personalizable |
| **Historial de comandos**| Añade historial para el programa envuelto | Historial avanzado, búsqueda interactiva y persistente |
| **Edición de línea**     | Añade edición de línea (gracias a `Readline`) | Edición de línea avanzada con muchas opciones configurables |
| **Configuración**        | Configuración mínima a través de opciones de línea de comandos | Configuración altamente personalizable mediante `~/.zshrc` y plugins |

---

### En resumen:
- **`rlwrap`** es útil cuando quieres agregar características de shell a programas que no las tienen, mientras que **`zsh`** es un **shell completo** con soporte nativo para esas características y muchas otras.
