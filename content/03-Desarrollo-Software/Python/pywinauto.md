---
title: "Guía Rápida: `pywinauto` - El Robot para tus Aplicaciones de Windows"
date: 2026-01-26
tags:
  - desarrollo-software
  - python
---
¡Claro! `pywinauto` es una de las librerías más potentes que usaste en tu script (aunque la función que la usaba estaba sin llamar). Es la herramienta "profesional" para la automatización de escritorios en Windows.

Aquí tienes una nota explicativa completa, perfecta para tu documentación en Markdown.

---

# Guía Rápida: `pywinauto` - El Robot para tus Aplicaciones de Windows


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[03-Desarrollo-Software/Java/SELENIUM|SELENIUM]]. [[03-Desarrollo-Software/Python/Selenium|Selenium]]. [[03-Desarrollo-Software/Python/pyautogui|pyautogui]]. [[02-Ciencias-Computacion/IA/Notas|Notas]].

`pywinauto` es una librería de Python que te permite **automatizar la interfaz gráfica de usuario (GUI) de aplicaciones de Windows**. Piénsalo como un Selenium, pero en lugar de controlar un navegador web, controla aplicaciones nativas como el Bloc de Notas, la Calculadora, SAP, o incluso los diálogos de "Abrir" y "Guardar archivo" de Windows.

## ¿Para Qué Sirve?

Su propósito principal es interactuar con aplicaciones como si fueras un usuario humano, pero de forma programática:
*   Hacer clic en botones.
*   Escribir texto en campos de entrada.
*   Seleccionar elementos de menús desplegables.
*   Obtener texto de etiquetas.
*   Mover y redimensionar ventanas.

Es la solución ideal cuando necesitas automatizar un proceso en una aplicación que **no tiene una API** (una interfaz de programación).

## `pywinauto` vs. `pyautogui`

En tu script, tienes dos funciones para manejar el diálogo de Windows. Una usa `pyautogui` y la otra `pywinauto`. Esta es la diferencia clave:

| Característica | `pyautogui` (El Autómata Ciego) | `pywinauto` (El Robot Inteligente) |
| :--- | :--- | :--- |
| **Método** | Controla el ratón y el teclado de forma **"ciega"**. Le dices "mueve el ratón a la coordenada (x, y) y haz clic" o "pulsa la tecla Alt". | Interactúa con los **componentes internos** de la aplicación. Le dices "busca el botón que se llama 'Guardar'" o "escribe en el campo de texto con el ID '1148'". |
| **Robustez** | **Muy frágil**. Si la ventana se mueve, la resolución cambia, o un atajo de teclado es diferente (por idioma), el script falla. | **Mucho más robusto**. No depende de coordenadas ni de la posición de la ventana. Encuentra los controles por sus propiedades (título, clase, ID). |
| **Complejidad** | Más simple para tareas muy básicas. | Requiere un poco más de configuración inicial para "conectar" con la aplicación, pero es mucho más potente. |
| **Plataforma** | Multiplataforma (Windows, macOS, Linux). | **Solo Windows**. |

**Conclusión:** `pyautogui` es bueno para scripts rápidos y sencillos, pero `pywinauto` es la elección correcta para una automatización fiable y profesional en Windows.

## ¿Cómo Funciona? Los "Backends"

`pywinauto` no "ve" la pantalla. Utiliza las APIs de accesibilidad que Microsoft integra en Windows para entender la estructura de una aplicación. Principalmente usa dos "backends" (motores):

1.  **`win32` (por defecto):** Es el más antiguo y rápido. Funciona muy bien con aplicaciones más viejas (tecnología Win32, MFC).
2.  **`uia` (UI Automation):** Es el más moderno y potente. Es necesario para aplicaciones nuevas (WPF, WinForms, Qt, e incluso apps de la Tienda de Microsoft).

En tu función `seleccionar_en_dialogo_windows1`, especificaste `backend="uia"`, que es la elección correcta para interactuar con los diálogos modernos de Windows.

```python
# Así se especifica el backend al conectar
app = Desktop(backend="uia").connect(...)
```

## Ejemplo Práctico: Automatizar el Bloc de Notas

Este ejemplo abre el Bloc de Notas, escribe un texto, y lo guarda.

```python
from pywinauto import Application

# 1. Iniciar la aplicación que queremos controlar
app = Application(backend="uia").start("notepad.exe")

# 2. Conectar con la ventana principal. Podemos buscarla por su título.
#    Usamos 'title_re' para que coincida con "Sin título - Bloc de notas" o similar.
dlg = app.window(title_re=".*Bloc de notas")

# 3. Esperar a que la ventana esté lista
dlg.wait('ready')

# 4. Interactuar con los controles (widgets) de la ventana.
#    - Escribimos en el editor de texto.
#    - El editor es un control de tipo "Edit".
dlg.child_window(class_name="Edit").type_keys("¡Hola, mundo desde pywinauto!", with_spaces=True)

# 5. Interactuar con los menús
dlg.menu_select("Archivo->Guardar como...")

# 6. Se abre una nueva ventana de "Guardar como". La seleccionamos.
save_as_dlg = app.window(title="Guardar como")
save_as_dlg.wait('ready')

# 7. Escribimos el nombre del archivo en el campo "Nombre:"
save_as_dlg.child_window(title="Nombre:", auto_id="1001", control_type="Edit").set_text("mi_archivo.txt")

# 8. Hacemos clic en el botón "Guardar"
save_as_dlg.child_window(title="Guardar", auto_id="1", control_type="Button").click()

print("¡Archivo guardado con éxito!")
```

### Herramientas útiles

Para descubrir las propiedades de los controles (como `title`, `auto_id`, `control_type`) y poder usarlas en tu script, necesitas una herramienta de "inspección". La más común es **`Inspect.exe`**, que viene con el SDK de Windows. Te permite hacer clic en cualquier elemento de una ventana y ver todos sus detalles.