---
title: "Wpscan"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
**WPScan** es una herramienta de seguridad popular diseñada específicamente para escanear sitios web basados en **WordPress**. Es de código abierto y se utiliza principalmente para identificar vulnerabilidades en la instalación de WordPress, en los temas, plugins y la configuración de la página. WPScan es una herramienta esencial para profesionales de la seguridad, administradores de sitios web y auditores que buscan mejorar la seguridad de sus instalaciones de WordPress.

### Características principales de WPScan:


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

1. **Base de datos de vulnerabilidades**: WPScan mantiene una base de datos de vulnerabilidades conocida, que incluye vulnerabilidades conocidas en el núcleo de WordPress, temas y plugins. Esta base de datos se actualiza regularmente, lo que permite a los administradores identificar versiones obsoletas o inseguras de los componentes instalados.

2. **Enumeración de plugins y temas**: WPScan puede enumerar todos los plugins y temas instalados en un sitio de WordPress. Esto es útil para detectar plugins o temas vulnerables, ya que WPScan puede comparar las versiones con su base de datos de vulnerabilidades.

3. **Enumeración de usuarios**: La herramienta puede enumerar los usuarios registrados en un sitio WordPress, lo cual es útil para identificar cuentas de usuario que pueden ser débiles o que no deberían estar allí. Esta función también es útil en pruebas de contraseñas y en la realización de ataques de fuerza bruta.

4. **Ataque de fuerza bruta**: WPScan soporta ataques de fuerza bruta sobre el formulario de inicio de sesión de WordPress, utilizando una lista de palabras (wordlist) para intentar adivinar contraseñas de usuarios.

5. **Detección de problemas de configuración**: WPScan puede identificar configuraciones inseguras, como permisos de archivos débiles, datos sensibles expuestos o cabeceras HTTP innecesarias que podrían poner en riesgo el sitio web.

6. **Opciones de escaneo personalizables**: La herramienta permite personalizar los escaneos para buscar vulnerabilidades específicas, como la búsqueda de un plugin o tema en particular, o bien para centrarse en ciertos tipos de vulnerabilidades, como las de inyección SQL o XSS.

### Ejemplo básico de uso:

Para usar WPScan, generalmente se ejecuta un comando desde la línea de comandos (CLI) con la siguiente sintaxis:

```bash
wpscan --url http://tusitio.com
```

Este comando realiza un escaneo básico en el sitio web `tusitio.com`.

Si deseas realizar un escaneo más específico, como por ejemplo buscar vulnerabilidades de un plugin específico, puedes usar:

```bash
wpscan --url http://tusitio.com --plugins-detection mixed
```

### Instalación:

1. **En Linux (Ubuntu/Debian)**:
   Puedes instalar WPScan utilizando el siguiente comando:

   ```bash
   sudo apt install wpscan
   ```

2. **Usando Docker**:
   Si prefieres usar Docker, puedes ejecutar WPScan con el siguiente comando:

   ```bash
   docker run --rm wpscanteam/wpscan --url http://tusitio.com
   ```

### Consideraciones importantes:
- **Uso ético**: WPScan debe ser utilizado de manera ética. Solo debes escanear sitios web para los que tienes permiso explícito. El escaneo de sitios sin autorización es ilegal y puede ser considerado un ataque.
- **Actualización de la base de datos**: Para aprovechar las últimas mejoras y vulnerabilidades conocidas, es importante actualizar la base de datos de vulnerabilidades de WPScan regularmente.

### Conclusión:
WPScan es una herramienta poderosa para auditar la seguridad de sitios WordPress. Ofrece una forma eficaz de detectar vulnerabilidades antes de que los atacantes puedan explotarlas. Sin embargo, es crucial usar la herramienta de forma responsable y legal.