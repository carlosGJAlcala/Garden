---
title: "Reconocimiento De Directorios Y Archivo"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
`dirb`, `feroxbuster` y `ffuf` son tres herramientas muy populares en el ámbito de s** durante pruebas de penetración o **pentesting**. Estas herramientas se utilizan para realizar ataques de "fuerza bruta" o para descubrir rutas ocultas y archivos en un servidor web que no están fácilmente accesibles.

A continuación te doy un resumen de cada una de estas herramientas, cómo funcionan y cómo puedes usarlas para realizar pruebas de seguridad en un servidor web:

---

### 1. **DIRB**

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

**`dirb`** es una herramienta sencilla que realiza un escaneo de directorios y archivos en un servidor web. Utiliza un diccionario de palabras para probar rutas y encontrar directorios o archivos ocultos.

#### Instalación:
Si usas **Kali Linux**, `dirb` ya viene instalado. Si no es así, puedes instalarlo de la siguiente forma:

```bash
sudo apt install dirb
```

#### Uso básico:
```bash
dirb http://example.com
```

- `http://example.com`: La URL del sitio web donde deseas buscar directorios y archivos.

También puedes usar un diccionario personalizado:

```bash
dirb http://example.com /ruta/al/diccionario.txt
```

#### Opciones comunes:
- `-w`: Especifica el tamaño del `wordlist` (diccionario) a usar.
- `-o`: Guardar los resultados en un archivo de salida.
- `-r`: Hacer un "retry" o reintentar solicitudes fallidas.

Ejemplo con diccionario personalizado y guardado de salida:
```bash
dirb http://example.com /usr/share/dirb/wordlists/common.txt -o resultados.txt
```

---

### 2. **FEROXBUSTER**
**`feroxbuster`** es una herramienta escrita en Rust que es mucho más rápida que herramientas más antiguas como `dirb`. También es una excelente opción para realizar pruebas de directorios y archivos, y ofrece varias funcionalidades avanzadas como la capacidad de detectar redirecciones o realizar búsquedas recursivas.

#### Instalación:
Puedes instalar `feroxbuster` desde GitHub:

1. **Con `cargo` (gestor de paquetes de Rust)**:
   Si tienes `cargo` instalado, simplemente usa el siguiente comando:
   ```bash
   cargo install feroxbuster
   ```

2. **Instalar con `apt` en Kali Linux**:
   ```bash
   sudo apt install feroxbuster
   ```

#### Uso básico:
```bash
feroxbuster -u http://example.com
```

- `-u`: Especifica la URL a escanear.
- `-w`: Especifica un diccionario de palabras a usar.

#### Ejemplo de uso:
```bash
feroxbuster -u http://example.com -w /usr/share/wordlists/dirb/common.txt
```

#### Opciones comunes:
- `-t`: Especifica el número de hilos (threads) que se utilizarán para realizar el escaneo en paralelo.
- `-x`: Para especificar extensiones de archivo (por ejemplo, `.php`, `.html`).
- `-e`: Realiza una búsqueda recursiva (si encuentra directorios, entra a buscar dentro de ellos).

Ejemplo con múltiples extensiones y hilos:
```bash
feroxbuster -u http://example.com -w /usr/share/wordlists/dirb/common.txt -t 50 -x php,html
```

---

### 3. **FFUF (Fuzz Faster U Fool)**
**`ffuf`** es una herramienta rápida y flexible de "fuzzing" o fuerza bruta para detectar directorios y archivos en servidores web. Es similar a `feroxbuster`, pero más ligera y flexible, permitiendo un alto grado de personalización.

#### Instalación:
Si usas Kali Linux:
```bash
sudo apt install ffuf
```

Si no lo tienes en tu distribución, puedes instalarlo desde el repositorio oficial de GitHub:

```bash
go install github.com/ffuf/ffuf@latest
```

#### Uso básico:
```bash
ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

- `-u`: La URL donde se reemplaza la palabra `FUZZ` por las entradas del diccionario.
- `-w`: Especifica el diccionario a usar.

#### Ejemplo con diccionario:
```bash
ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

#### Opciones comunes:
- `-w`: Diccionario a usar.
- `-u`: La URL de destino, con `FUZZ` como marcador de posición.
- `-t`: Número de hilos.
- `-e`: Extensiones de archivos.
- `-mc`: Especifica el código de estado HTTP que deseas capturar (por ejemplo, `-mc 200` para obtener solo respuestas HTTP 200).
- `-s`: Filtra los resultados mostrando solo aquellos con un tamaño de respuesta mayor o igual que el especificado.

Ejemplo con filtros y extensiones:
```bash
ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.html,.bak -mc 200
```

---

### Comparativa Rápida:

| Herramienta        | Velocidad | Características principales                                              |
|--------------------|-----------|---------------------------------------------------------------------------|
| **dirb**           | Baja      | Simple, menos opciones, ideal para principiantes.                         |
| **feroxbuster**    | Alta      | Rápido, utiliza hilos, recursivo, manejo de redirecciones.                |
| **ffuf**           | Muy Alta  | Muy rápido, flexible, permite múltiples filtros y configuraciones avanzadas. |

---

### Resumen

- **`dirb`**: Es más simple y fácil de usar, adecuado para escaneos rápidos, pero con menos funcionalidades avanzadas.
- **`feroxbuster`**: Es más rápido y flexible que `dirb`, soporta hilos y es capaz de hacer búsquedas recursivas.
- **`ffuf`**: Es extremadamente rápido, altamente configurable, y permite filtros más detallados y controlados sobre los resultados.

Estas herramientas son esenciales para el **reconocimiento web** y pueden ayudarte a descubrir rutas y archivos ocultos en un servidor web durante un test de penetración. ¡Asegúrate de usarlas de manera ética y legal!

si acaba en númro es de base de datos