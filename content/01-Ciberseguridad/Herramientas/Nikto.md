---
title: "Nikto"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
	**Nikto** es una herramienta de escaneo de vulnerabilidades de código abierto diseñada para realizar auditorías de seguridad en servidores web. Su objetivo principal es identificar una amplia gama de problemas de seguridad en servidores web, incluyendo vulnerabilidades en la configuración, software desactualizado, directorios y archivos sensibles expuestos, entre otros.

Nikto es muy popular entre los profesionales de la seguridad y pentesters (probadores de penetración) debido a su simplicidad, velocidad y la amplia base de datos de vulnerabilidades que tiene integrada.

### Características principales de **Nikto**:


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

1. **Escaneo de vulnerabilidades conocidas**: Nikto tiene una base de datos extensa con más de 6,700 vulnerabilidades conocidas. Esto incluye problemas como configuraciones incorrectas, versiones antiguas de software con fallos de seguridad, y archivos y directorios expuestos.
   
2. **Detección de software desactualizado**: Nikto puede identificar versiones antiguas de servidores web, como Apache, Nginx, y otros, y alertar sobre vulnerabilidades conocidas en esas versiones.

3. **Verificación de configuraciones inseguras**: La herramienta busca configuraciones incorrectas en los servidores web, como permisos inapropiados, métodos HTTP no seguros (como `TRACE` o `DELETE` habilitados), y otros problemas comunes que pueden representar riesgos de seguridad.

4. **Exploración de directorios y archivos sensibles**: Nikto busca directorios y archivos que no deberían ser accesibles desde la web pública, como archivos de configuración, archivos de backup, y otros recursos privados o sensibles.

5. **Soporte para autenticación**: Nikto puede trabajar con autenticación HTTP básica o autenticación mediante cookies, lo que permite escanear sitios web que requieren iniciar sesión o que están protegidos de alguna otra forma.

6. **Soporte para proxies**: Nikto puede configurarse para utilizar proxies, lo que es útil cuando se realizan pruebas de penetración de forma anónima o a través de redes privadas.

7. **Generación de informes**: Los resultados de los escaneos pueden exportarse en diferentes formatos, como HTML, XML, o CSV, lo que facilita la documentación y la presentación de los hallazgos.

8. **Escaneo de múltiples URLs**: Puedes configurar Nikto para escanear varios dominios o rutas específicas en un servidor, lo que es útil para realizar auditorías de aplicaciones web completas.

### Cómo usar **Nikto**:

El uso básico de Nikto es bastante sencillo. El comando más básico para realizar un escaneo de vulnerabilidades en un servidor web sería:

```bash
nikto -h http://ejemplo.com
```

Aquí, `-h` indica la URL o dirección IP del servidor web que se desea escanear.

### Algunos parámetros comunes de **Nikto**:

- `-h <url>`: Especifica la URL o dirección IP del servidor que se va a escanear.
- `-p <puerto>`: Especifica el puerto del servidor. Si no se especifica, Nikto escaneará el puerto 80 por defecto.
- `-Tuning <valor>`: Permite ajustar el nivel de pruebas que se realizarán. Los valores van de 1 a 5 (1 es el escaneo más rápido y 5 el más exhaustivo).
- `-o <archivo>`: Especifica el archivo donde se guardarán los resultados del escaneo.
- `-Format <formato>`: Permite especificar el formato de salida (HTML, CSV, XML, etc.).
- `-id <usuario:contraseña>`: Usado para especificar las credenciales de autenticación HTTP (en caso de que el sitio esté protegido por contraseña).

### Ejemplo de escaneo más detallado:

Para realizar un escaneo completo, con una salida en formato HTML y guardarlo en un archivo, podrías usar algo como esto:

```bash
nikto -h http://ejemplo.com -o resultados.html -Format htm
```

Este comando escanea el servidor web en `http://ejemplo.com`, genera un informe en formato HTML y lo guarda en un archivo llamado `resultados.html`.

### Instalación de **Nikto**:

1. **En Linux (Debian/Ubuntu)**:

   Nikto puede instalarse fácilmente a través de `apt`:

   ```bash
   sudo apt update
   sudo apt install nikto
   ```

2. **Desde el repositorio de GitHub**:

   También puedes clonar el repositorio oficial de Nikto desde GitHub:

   ```bash
   git clone https://github.com/sullo/nikto.git
   cd nikto
   perl nikto.pl
   ```

   Si decides instalarlo de esta manera, asegúrate de tener **Perl** instalado en tu sistema, ya que Nikto está escrito en Perl.

### Consideraciones y uso ético:

- **Uso responsable**: Al igual que con otras herramientas de seguridad, es importante utilizar Nikto de manera ética y legal. Nunca debes realizar un escaneo de vulnerabilidades en un sitio web o servidor sin obtener el permiso explícito del propietario.
- **Evitar escaneos agresivos**: Los escaneos de Nikto pueden generar una gran cantidad de tráfico, lo que podría afectar el rendimiento del servidor. Siempre realiza las pruebas de manera controlada y preferiblemente en entornos de prueba.

### Conclusión:

Nikto es una herramienta poderosa y fácil de usar para realizar auditorías de seguridad en servidores web. Ayuda a identificar rápidamente vulnerabilidades y configuraciones inseguras que podrían ser explotadas por atacantes. Sin embargo, como cualquier herramienta de seguridad, debe ser utilizada de manera responsable y con el permiso adecuado.