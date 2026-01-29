---
title: "Clonar el repositorio desde GitHub"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - osint
---


**Sherlock** es una herramienta de código abierto diseñada para buscar nombres de usuario en múltiples plataformas y redes sociales. Su objetivo principal es ayudar a localizar perfiles en sitios web donde un nombre de usuario esté registrado, lo cual es útil en investigaciones OSINT (*Open Source Intelligence*), auditorías de seguridad o simplemente para verificar la disponibilidad de un nombre de usuario.

---

### **Cómo usar Sherlock**


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

#### 1. **Instalación**
Puedes instalar **Sherlock** en sistemas que tengan Python instalado. Sigue estos pasos:

```bash
# Clonar el repositorio desde GitHub
git clone https://github.com/sherlock-project/sherlock.git

# Cambiar al directorio de Sherlock
cd sherlock

# Instalar las dependencias necesarias
pip install -r requirements.txt
```

Opcionalmente, también puedes instalarlo usando **pipx** si deseas ejecutarlo de forma aislada:

```bash
pipx install sherlock
```

---

#### 2. **Ejecutar Sherlock**
La herramienta se ejecuta desde la línea de comandos. La estructura básica del comando es:

```bash
python3 sherlock <nombre_de_usuario>
```

Esto buscará el nombre de usuario en las plataformas soportadas.

---

#### 3. **Ejemplos de Uso**

- **Búsqueda básica de un nombre de usuario:**
  ```bash
  python3 sherlock john_doe
  ```
  Esto buscará el nombre de usuario `john_doe` en todas las plataformas compatibles.

- **Guardar los resultados en un archivo:**
  Puedes exportar los resultados a un archivo de texto o JSON para análisis posterior:
  ```bash
  python3 sherlock john_doe --output output.txt
  ```

- **Especificar el tiempo de espera:**
  Puedes ajustar el tiempo de espera entre solicitudes para evitar restricciones por parte de algunas plataformas:
  ```bash
  python3 sherlock john_doe --timeout 5
  ```

- **Modo silencioso:**
  Si no quieres mostrar la salida en tiempo real en la terminal:
  ```bash
  python3 sherlock john_doe --quiet
  ```

---

#### 4. **Opciones Adicionales**

- **Ver todas las opciones disponibles:**
  Usa el parámetro `--help` para listar todas las opciones de configuración:
  ```bash
  python3 sherlock --help
  ```

- **Buscar múltiples nombres de usuario:**
  Sherlock permite buscar varios nombres de usuario en una sola ejecución. Crea un archivo de texto con los nombres de usuario y utiliza:
  ```bash
  python3 sherlock --usernames-from-file usernames.txt
  ```

---

### **Ejemplo Completo:**
Para buscar el nombre de usuario `john_doe` en todas las plataformas, establecer un tiempo de espera de 10 segundos entre solicitudes y guardar los resultados en un archivo JSON:

```bash
python3 sherlock john_doe --timeout 10 --output resultados.json
```

---

### **Nota de Uso Ético:**
Sherlock debe ser utilizado únicamente para propósitos legítimos y éticos, como investigaciones de seguridad en las que tengas permiso o fines personales. El uso indebido podría violar las políticas de privacidad y ser ilegal en algunos contextos.

---

### **Enlaces Relacionados**
- [Sitio oficial de Sherlock (GitHub)](https://github.com/sherlock-project/sherlock)
- [OSINT (Open Source Intelligence)](https://es.wikipedia.org/wiki/Inteligencia_de_fuentes_abiertas)
- [Documentación de Python](https://docs.python.org/3/): Es útil para solucionar posibles problemas durante la instalación o ejecución.