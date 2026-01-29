---
title: "Locate"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---
El comando **`locate`** se utiliza en sistemas Unix y Linux para buscar archivos en el sistema de archivos de manera rápida. A diferencia de otros comandos de búsqueda como **`find`**, que realizan la búsqueda en tiempo real, **`locate`** utiliza una base de datos previamente indexada, lo que permite realizar búsquedas mucho más rápidas.

### ¿Cómo funciona **`locate`**?


> **Relacionado**: [[00-Inicio/HOME|HOME]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

**`locate`** consulta una base de datos que contiene información sobre los archivos del sistema (incluyendo sus rutas completas). Esta base de datos no se actualiza en tiempo real, por lo que puede estar desactualizada si se han agregado o movido archivos después de la última actualización del índice.

### Cómo usar **`locate`**:

#### 1. **Buscar un archivo o directorio**:

Para buscar un archivo o directorio específico, simplemente ejecuta el comando seguido del nombre o patrón que quieres encontrar. Por ejemplo, para buscar archivos que contienen la palabra **`documento`** en su nombre:
```bash
locate documento
```
Esto te mostrará una lista de todos los archivos y directorios que contienen "documento" en su nombre, mostrando las rutas completas.

#### 2. **Actualizar la base de datos**:

La base de datos de **`locate`** no se actualiza automáticamente en tiempo real. Para asegurarte de que la base de datos esté actualizada, puedes ejecutar el comando **`updatedb`**. Este comando generalmente requiere privilegios de superusuario (root) para ejecutarse:

```bash
sudo updatedb
```

Este comando actualizará la base de datos de **`locate`** con los archivos actuales del sistema, lo que permitirá una búsqueda precisa y actualizada.

#### 3. **Buscar usando expresiones o patrones**:

Puedes usar patrones de texto con comodines para refinar tu búsqueda. Por ejemplo:

- Para buscar todos los archivos con extensión **`.txt`**:
  ```bash
  locate "*.txt"
  ```
- Para buscar todos los archivos que contengan la palabra **`config`**:
  ```bash
  locate config
  ```

#### 4. **Ignorar mayúsculas y minúsculas**:

Si quieres que la búsqueda ignore las diferencias entre mayúsculas y minúsculas, puedes usar la opción `-i`. Por ejemplo, para buscar archivos que contengan "documento" independientemente de si están en mayúsculas o minúsculas:
```bash
locate -i documento
```

#### 5. **Limitar el número de resultados**:

Puedes limitar el número de resultados que **`locate`** muestra utilizando la opción `-n`. Por ejemplo, para mostrar solo los primeros 5 resultados:
```bash
locate -n 5 documento
```

#### 6. **Mostrar solo coincidencias completas (filtrar por ruta exacta)**:

Si quieres filtrar los resultados y ver solo coincidencias completas, puedes usar el parámetro `-b`. Este filtro se usa para buscar la coincidencia solo en el nombre del archivo, no en todo el path. Ejemplo:
```bash
locate -b documento
```

#### 7. **Mostrar resultados más detallados**:

Puedes usar la opción `-l` para mostrar la lista de archivos y sus rutas de una forma más legible y completa.

```bash
locate -l
```

### Ejemplos de uso comunes:

- **Buscar archivos con "config" en el nombre**:
  ```bash
  locate config
  ```

- **Buscar todos los archivos `.jpg` en el sistema**:
  ```bash
  locate "*.jpg"
  ```

- **Buscar un archivo en una ubicación específica** (por ejemplo, dentro de `/home`):
  ```bash
  locate /home/documento
  ```

- **Actualizar la base de datos de `locate`**:
  ```bash
  sudo updatedb
  ```

### Consideraciones importantes:

- **Base de datos no actualizada**: Si el comando **`locate`** no muestra archivos recientemente creados o modificados, es porque la base de datos no se ha actualizado. Puedes actualizarla manualmente con **`updatedb`**.
  
- **Rendimiento**: **`locate`** es mucho más rápido que **`find`** porque utiliza una base de datos indexada, pero ten en cuenta que los resultados pueden estar desactualizados si no has actualizado la base de datos recientemente.

### Instalación de **`locate`**:

En algunos sistemas, **`locate`** no viene instalado por defecto. Si no tienes **`locate`** en tu sistema, puedes instalarlo de la siguiente manera:

- **Ubuntu/Debian**:
  ```bash
  sudo apt install mlocate
  ```

- **CentOS/RHEL**:
  ```bash
  sudo yum install mlocate
  ```

- **Arch Linux**:
  ```bash
  sudo pacman -S mlocate
  ```

Una vez instalado, asegúrate de ejecutar **`updatedb`** para crear la base de datos inicial de archivos.

### Resumen de opciones útiles:

- **`locate [patrón]`**: Buscar archivos que coincidan con el patrón dado.
- **`updatedb`**: Actualizar la base de datos de archivos.
- **`locate -i [patrón]`**: Buscar sin distinguir entre mayúsculas y minúsculas.
- **`locate -n [número] [patrón]`**: Limitar el número de resultados a mostrar.
- **`locate -b [patrón]`**: Buscar solo coincidencias en el nombre del archivo.

Si tienes alguna duda más o necesitas ejemplos adicionales, no dudes en preguntar. ¡Estoy aquí para ayudarte!