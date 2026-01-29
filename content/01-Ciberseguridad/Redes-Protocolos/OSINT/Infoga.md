---
title: "Infoga"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - osint
---

**Infoga** es una herramienta OSINT (*Open Source Intelligence*) utilizada para recopilar información sobre direcciones de correo electrónico. Ayuda a identificar detalles como servidores relacionados con el correo electrónico, información de dominio, y otros datos útiles que pueden ser empleados en auditorías de seguridad o investigaciones.

Infoga es especialmente efectiva durante la fase de reconocimiento en pruebas de penetración, ya que permite descubrir posibles vectores de ataque basados en información pública.

---

### **Cómo usar Infoga**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

#### 1. **Instalación**

Puedes instalar **Infoga** desde su repositorio oficial en GitHub. A continuación, los pasos para configurarlo:

1. **Clonar el repositorio desde GitHub:**
   ```bash
   git clone https://github.com/m4ll0k/Infoga.git
   ```

2. **Cambiar al directorio de Infoga:**
   ```bash
   cd Infoga
   ```

3. **Instalar las dependencias necesarias:**
   Infoga depende de Python, por lo que es necesario instalar las dependencias:
   ```bash
   pip install -r requirements.txt
   ```

---

#### 2. **Ejecutar Infoga**
Infoga tiene una interfaz de línea de comandos y se ejecuta con el script `infoga.py`.

La estructura básica del comando es:
```bash
python3 infoga.py --domain <dominio> --source <fuente>
```

---

#### 3. **Opciones Comunes**

- **`--domain <dominio>`**: Especifica el dominio del cual deseas recolectar información (por ejemplo, `example.com`).
- **`--source <fuente>`**: Define la fuente de búsqueda. Algunas opciones son `all`, `google`, `bing`, `yahoo`, `virustotal`, entre otras.
- **`--help`**: Muestra todas las opciones disponibles.

---

#### 4. **Ejemplos de Uso**

- **Búsqueda básica:**
  Busca correos electrónicos relacionados con el dominio `example.com` utilizando todas las fuentes disponibles:
  ```bash
  python3 infoga.py --domain example.com --source all
  ```

- **Búsqueda con una fuente específica:**
  Busca correos electrónicos utilizando Google como fuente:
  ```bash
  python3 infoga.py --domain example.com --source google
  ```

- **Exportar resultados a un archivo:**
  Puedes guardar los resultados en un archivo de texto:
  ```bash
  python3 infoga.py --domain example.com --source all --output resultados.txt
  ```

---

### **Ejemplo Completo**
Supongamos que quieres recopilar todos los correos relacionados con el dominio `example.com`, usando todas las fuentes y guardando los resultados en un archivo llamado `info_example.txt`:

```bash
python3 infoga.py --domain example.com --source all --output info_example.txt
```

---

### **Nota de Uso Ético**
Infoga está diseñado para fines éticos, como investigaciones legítimas de seguridad o auditorías con permiso del propietario. Usarlo sin autorización puede ser ilegal y podría violar políticas de privacidad.

---

### **Enlaces Relacionados**
- [Sitio oficial de Infoga (GitHub)](https://github.com/m4ll0k/Infoga)
- [OSINT (Open Source Intelligence)](https://es.wikipedia.org/wiki/Inteligencia_de_fuentes_abiertas)
- [Kali Linux](https://www.kali.org/): Distribución que incluye herramientas similares para investigaciones OSINT.