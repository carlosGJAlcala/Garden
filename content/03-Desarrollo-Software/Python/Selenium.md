---
title: "Guía Rápida: Selenium - El Titiritero de los Navegadores Web"
date: 2026-01-26
tags:
  - desarrollo-software
  - python
---
¡Excelente elección! Selenium es el motor principal de tu script para la parte web. Es una herramienta increíblemente poderosa y fundamental en la automatización moderna.

Aquí tienes la nota explicativa detallada en formato Markdown.

---

# Guía Rápida: Selenium - El Titiritero de los Navegadores Web


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Java/SELENIUM|SELENIUM]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]].

**Selenium** es un framework de código abierto para la **automatización de navegadores web**. En pocas palabras, te permite escribir código (en Python, Java, C#, etc.) que controla un navegador web (como Chrome, Firefox o Edge) exactamente como si una persona estuviera sentada frente a él: abriendo páginas, haciendo clic en botones, rellenando formularios y extrayendo información.

Piensa en Selenium como un **robot programable que usa un navegador real**.

## ¿Para Qué Sirve?

Aunque fue creado originalmente para **pruebas automatizadas** (verificar que un sitio web funciona correctamente después de hacer cambios), sus usos se han expandido enormemente:

1.  **Testing de Aplicaciones Web:** Su propósito original. Simula flujos de usuario para encontrar errores de forma automática.
2.  **Automatización de Tareas Repetitivas:** Justo lo que hace tu script. Rellenar formularios, subir archivos, generar reportes desde una intranet, etc.
3.  **Web Scraping:** Extraer datos de sitios web de manera estructurada. Es especialmente útil para sitios dinámicos que cargan contenido con JavaScript, donde librerías como `BeautifulSoup` o `requests` no son suficientes.

## ¿Cómo Funciona? La Arquitectura Clave

Entender esto es crucial para solucionar problemas. Selenium no es un solo programa, sino un sistema de tres partes:

1.  **Tu Script de Python:** Aquí es donde escribes los comandos (`driver.get()`, `driver.find_element()`, etc.).
2.  **WebDriver:** Este es el "traductor" o el "puente". Es un pequeño servidor **ejecutable e independiente** (`chromedriver.exe` para Chrome, `geckodriver.exe` para Firefox) que recibe los comandos de tu script y los traduce a un lenguaje que el navegador entiende. En tu script, lo configuras con la línea `service=Service(...)`.
3.  **El Navegador Web:** La aplicación real (Chrome, en tu caso) que recibe las instrucciones del WebDriver y las ejecuta, mostrando la página e interactuando con ella.

El flujo es: **Tu Script → WebDriver → Navegador**

## Conceptos Fundamentales en Tu Script

Tu código utiliza los conceptos más importantes de Selenium.

### 1. Iniciar una Sesión (`driver`)

Todo comienza creando un objeto `driver`, que representa la instancia del navegador que vas a controlar.

```python
# Configuras el servicio para decirle a Selenium dónde está chromedriver.exe
service = Service("C:/.../chromedriver.exe")
# Configuras opciones, como ejecutar en modo "headless" (sin ventana visible)
option = webdriver.ChromeOptions()
# Creas la instancia del navegador
driver = Chrome(service=service, options=option)
```

Al final, es vital cerrar la sesión para liberar recursos con `driver.quit()`.

### 2. Navegar y Encontrar Elementos

Una vez tienes el `driver`, las dos tareas más comunes son ir a una URL y encontrar elementos en la página.

```python
# Navegar a una URL
driver.get(url_of_list)

# Encontrar un elemento
# Sintaxis: driver.find_element(By.<LOCATOR>, "valor_del_locator")
button = driver.find_element(By.XPATH, "/html/body/div[1]/.../button[1]")
```

**"Localizadores" (Locators):** `By.XPATH` es un tipo de localizador. Es la estrategia que usa Selenium para encontrar un elemento. Las más comunes son:
*   `By.ID`: El más rápido y robusto. Usa el atributo `id` del elemento (ej: `id="username"`).
*   `By.NAME`: Usa el atributo `name` (ej: `name="password"`).
*   `By.CLASS_NAME`: Usa una de las clases CSS del elemento.
*   `By.CSS_SELECTOR`: Muy potente, usa selectores de CSS.
*   `By.XPATH`: El más flexible, pero puede ser lento y frágil.

> **️ Advertencia sobre tus XPaths:** Tu script usa **XPaths absolutos** (`/html/body/div[1]...`). Son extremadamente frágiles. Si el desarrollador de SharePoint añade un solo `<div>` en la página, todos tus XPaths se romperán.
> **Mejora:** Siempre que sea posible, utiliza **XPaths relativos** que busquen elementos por atributos únicos, como texto o un ID.
> *   **Malo:** `/html/body/div[6]/div/div/div/div[2]/div[2]/.../button`
> *   **Bueno:** `//button[text()='Guardar']` (Busca cualquier botón en la página cuyo texto sea 'Guardar').

### 3. Interactuar con Elementos

Una vez que tienes un elemento, puedes actuar sobre él.

```python
# Hacer clic en un botón o enlace
button.click()

# Escribir en un campo de texto
elemento.send_keys(valor)
```
Esto es el corazón de tu función `cargarDatosForm`.

### 4. Esperas: El Secreto para Scripts Robustos

Las páginas web modernas son dinámicas. Un elemento puede tardar un poco en aparecer.

*   **Mala Práctica (`time.sleep()`):** Pausa el script por un tiempo fijo. Si la red es lenta, puede no ser suficiente y el script fallará. Si es rápida, es una pérdida de tiempo. **Tu script abusa de `time.sleep()`**.

*   **Buena Práctica (Esperas Explícitas):** Le dicen a Selenium que espere **hasta que una condición se cumpla** (o hasta que se acabe un tiempo máximo). Es mucho más eficiente y fiable. Ya importas las herramientas para ello: `WebDriverWait` y `expected_conditions as EC`.

**Ejemplo de cómo mejorar tu código:**

```python
# En lugar de esto:
time.sleep(4)
button = driver.find_element(By.XPATH, "...")
button.click()

# Deberías hacer esto:
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Espera un máximo de 10 segundos hasta que el botón sea clickeable
wait = WebDriverWait(driver, 10)
button_xpath = "/html/body/div[1]/.../button[1]"
button = wait.until(EC.element_to_be_clickable((By.XPATH, button_xpath)))
button.click()
```

Este cambio haría tu script **infinitamente más robusto**.

En resumen, Selenium es la herramienta que te permite navegar a la lista de SharePoint, hacer clic en "Nuevo", encontrar cada campo del formulario usando el `XPATH_MAP` y rellenarlo con `send_keys` o `click`, para finalmente guardar el registro.