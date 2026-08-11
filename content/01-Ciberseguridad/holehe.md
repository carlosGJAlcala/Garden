**Holehe** es una herramienta de OSINT (*Open Source Intelligence*) que permite comprobar si una dirección de correo electrónico está registrada en diferentes plataformas o servicios en línea. Esto puede ser útil en investigaciones de ciberseguridad, como la recopilación de datos sobre un objetivo en pruebas de penetración, o para analizar posibles riesgos asociados con el uso de correos electrónicos en múltiples servicios.

### **Cómo usar Holehe**

#### 1. **Instalación**
Sigue estos pasos para instalar **Holehe** en tu sistema:

1. **Clonar el repositorio desde GitHub:**
   ```bash
   git clone https://github.com/megadose/holehe.git
   ```

2. **Cambiar al directorio de Holehe:**
   ```bash
   cd holehe
   ```

3. **Instalar las dependencias necesarias:**
   Holehe utiliza Python, así que asegúrate de tenerlo instalado, y luego ejecuta:
   ```bash
   pip install -r requirements.txt
   ```

#### 2. **Ejecutar Holehe**
La estructura básica del comando para usar Holehe es:

```bash
python3 holehe.py <correo> [opciones]
```

- **`<correo>`**: Especifica la dirección de correo electrónico que deseas investigar.

#### 3. **Ejemplos de Uso**

- **Búsqueda básica:**
  Verifica si la dirección de correo `example@gmail.com` está registrada en plataformas soportadas:
  ```bash
  python3 holehe.py example@gmail.com
  ```

- **Especificar servicios específicos:**
  Si quieres limitar la búsqueda a ciertas plataformas, puedes indicarlo:
  ```bash
  python3 holehe.py example@gmail.com --only facebook,instagram
  ```

- **Excluir plataformas específicas:**
  Puedes omitir ciertas plataformas en la búsqueda:
  ```bash
  python3 holehe.py example@gmail.com --exclude twitter,linkedin
  ```

- **Modo silencioso:**
  Si no deseas que se muestre información en pantalla, puedes activar el modo silencioso:
  ```bash
  python3 holehe.py example@gmail.com --quiet
  ```

#### 4. **Opciones Comunes**

- **`--only <servicios>`**: Limita la búsqueda a las plataformas especificadas.
- **`--exclude <servicios>`**: Excluye ciertas plataformas de la búsqueda.
- **`--help`**: Muestra todas las opciones y parámetros disponibles.
- **`--output <archivo>`**: Guarda los resultados en un archivo.

### **Ejemplo Completo**
Supongamos que quieres investigar si el correo `user@example.com` está registrado en todas las plataformas soportadas excepto Twitter y LinkedIn, y guardar los resultados en un archivo llamado `resultado.json`:

```bash
python3 holehe.py user@example.com --exclude twitter,linkedin --output resultado.json
```

### **Nota de Uso Ético**
Holehe debe utilizarse únicamente con propósitos legítimos, como investigaciones de seguridad autorizadas o análisis personales. El uso no autorizado puede violar leyes y políticas de privacidad.

### **Enlaces Relacionados**
- [Sitio oficial de Holehe (GitHub)](https://github.com/megadose/holehe)
- [OSINT (Open Source Intelligence)](https://es.wikipedia.org/wiki/Inteligencia_de_fuentes_abiertas)
- [Python](https://www.python.org/): Lenguaje en el que está desarrollado Holehe y necesario para ejecutarlo.
