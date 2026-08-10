
**theHarvester** es una herramienta de recopilación de información (OSINT, *Open Source Intelligence*) diseñada para recolectar datos relacionados con nombres de dominio, como direcciones de correo electrónico, subdominios, direcciones IP, puertos abiertos y nombres de empleados de una organización. Es ampliamente utilizada en auditorías de seguridad y pruebas de penetración para recopilar información que puede ser útil durante la fase de reconocimiento.

La herramienta utiliza diversos motores de búsqueda y servicios públicos para obtener esta información, tales como Google, Bing, Shodan, VirusTotal y más. theHarvester es una herramienta esencial para profesionales de la ciberseguridad que buscan identificar posibles vulnerabilidades mediante la recopilación de datos accesibles públicamente.

### Enlaces relacionados:
- [OSINT (Open Source Intelligence)](https://es.wikipedia.org/wiki/Inteligencia_de_fuentes_abiertas): Marco más amplio dentro del cual opera theHarvester.
- [Kali Linux](https://www.kali.org/): Una distribución de Linux que incluye theHarvester como una de sus herramientas de pruebas de penetración.
- [Sitio oficial de theHarvester](https://github.com/laramies/theHarvester): Repositorio de GitHub para descargar y consultar el código fuente de la herramienta.

Si quieres más información sobre alguna de estas conexiones, avísame.

**theHarvester** es relativamente fácil de usar, especialmente si tienes experiencia en la línea de comandos. Aquí tienes una guía básica sobre cómo usarlo:

---

### **Pasos para usar theHarvester:**

#### 1. **Instalación:**
Si no tienes **theHarvester** instalado, puedes hacerlo fácilmente. A menudo, ya está incluido en distribuciones como **Kali Linux**. Si no, puedes instalarlo manualmente:

```bash
# Clona el repositorio desde GitHub
git clone https://github.com/laramies/theHarvester.git

# Cambia al directorio de theHarvester
cd theHarvester

# Instala las dependencias
pip install -r requirements.txt
```

---

#### 2. **Ejecutar theHarvester:**
Una vez instalado, puedes ejecutarlo desde la línea de comandos. La estructura básica del comando es:

```bash
python3 theHarvester.py -d <dominio> -l <límite> -b <motor>
```

- **`-d <dominio>`**: Especifica el dominio objetivo, por ejemplo, `example.com`.
- **`-l <límite>`**: Define la cantidad de resultados a obtener (opcional, dependiendo del motor).
- **`-b <motor>`**: Indica el motor de búsqueda a utilizar, como `google`, `bing`, `shodan`, etc.

---

#### 3. **Ejemplos de Uso:**

- **Búsqueda básica:**
  ```bash
  python3 theHarvester.py -d example.com -b google
  ```
  Esto buscará información sobre el dominio `example.com` usando Google.

- **Buscar usando múltiples motores de búsqueda:**
  ```bash
  python3 theHarvester.py -d example.com -b google,bing,shodan
  ```
  Esto combinará resultados de varios motores de búsqueda.

- **Exportar resultados a un archivo:**
  Puedes guardar los resultados en un archivo HTML para visualización posterior:
  ```bash
  python3 theHarvester.py -d example.com -b google -f resultado.html
  ```

---

#### 4. **Parámetros Adicionales Útiles:**

- **`-h`**: Muestra la ayuda y todas las opciones disponibles.
  ```bash
  python3 theHarvester.py -h
  ```

- **`-v`**: Muestra más detalles durante la ejecución.

- **`-f <archivo>`**: Especifica un archivo de salida.

---

### **Ejemplo Completo:**

Si deseas recopilar datos sobre el dominio `example.com`, usando los motores `google` y `bing`, y guardar los resultados en un archivo llamado `example_output.html`:

```bash
python3 theHarvester.py -d example.com -b google,bing -f example_output.html
```

---

### **Nota de Uso Ético:**
Utiliza **theHarvester** únicamente para auditorías de seguridad en dominios sobre los que tienes permiso. El uso no autorizado puede ser ilegal y contravenir normas éticas de ciberseguridad.