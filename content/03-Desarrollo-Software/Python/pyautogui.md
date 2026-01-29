---
title: "Guía Rápida: `pyautogui` - Controla tu Ratón y Teclado con Python"
date: 2026-01-26
tags:
  - desarrollo-software
  - python
---
¡Perfecto! `pyautogui` es la primera herramienta que usaste en tu script para interactuar con el diálogo de Windows. Es muy útil conocerla bien.

Aquí tienes la nota explicativa en formato Markdown.

---

# Guía Rápida: `pyautogui` - Controla tu Ratón y Teclado con Python


> **Relacionado**: [[03-Desarrollo-Software/Java/SELENIUM|SELENIUM]]. [[03-Desarrollo-Software/Python/Selenium|Selenium]]. [[03-Desarrollo-Software/Python/pywinauto|pywinauto]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

`pyautogui` es una librería de Python que te permite **simular programáticamente los movimientos del ratón, los clics y las pulsaciones del teclado**. En esencia, le das a tus scripts de Python el poder de controlar la interfaz gráfica de usuario (GUI) de tu ordenador como si fuera una persona.

Es una herramienta de **automatización de GUI multiplataforma** (funciona en Windows, macOS y Linux) y es increíblemente útil para automatizar tareas repetitivas en cualquier aplicación.

## ¿Cuál es su Superpoder?

Su principal ventaja es su **simplicidad**. No necesita conocer la estructura interna de una aplicación (como hace `pywinauto`). En su lugar, opera de una de estas dos maneras:

1.  **Control por Coordenadas:** Le dices "mueve el ratón a la posición X=800, Y=400 y haz clic".
2.  **Control por Teclado:** Le dices "pulsa la tecla 'Alt', luego la 'F', y luego suelta 'Alt'".

En tu script, utilizaste el segundo método en la función `seleccionar_en_dialogo_windows` para interactuar con el diálogo de subida de archivos:

```python
# 1) Atajo para ir al campo File name: Alt+F (o Alt+N en español)
pyautogui.keyDown('alt')    # Simula mantener pulsada la tecla Alt
pyautogui.press("f")        # Simula pulsar y soltar la tecla 'f'
pyautogui.keyUp('alt')      # Simula soltar la tecla Alt
time.sleep(0.2)

# 2) Pegar la ruta
pyautogui.hotkey('ctrl', 'v') # Simula la combinación Ctrl+V
time.sleep(0.2)

# 3) Confirmar con Enter
pyautogui.press('enter')
```
Este es un caso de uso clásico y muy inteligente de `pyautogui`.

## Casos de Uso Comunes

*   Automatizar clics en botones de una página web que son difíciles de manejar con Selenium.
*   Rellenar formularios en aplicaciones de escritorio antiguas.
*   Realizar tareas repetitivas en software de diseño gráfico o edición de vídeo.
*   Crear bots para juegos sencillos (¡con cuidado!).
*   Interactuar con diálogos del sistema operativo, como en tu script.

## Funciones Más Importantes

### Control del Ratón

```python
import pyautogui

# Obtener el tamaño de la pantalla
screenWidth, screenHeight = pyautogui.size()

# Mover el ratón a una coordenada (x, y) durante 0.5 segundos
pyautogui.moveTo(100, 150, duration=0.5)

# Mover el ratón relativamente a su posición actual
pyautogui.move(0, 50)  # Mover 50 píxeles hacia abajo

# Clics del ratón
pyautogui.click()               # Clic izquierdo en la posición actual
pyautogui.click(200, 220)       # Mueve a (200, 220) y hace clic
pyautogui.rightClick()          # Clic derecho
pyautogui.doubleClick()         # Doble clic

# Arrastrar y soltar
pyautogui.dragTo(300, 400, duration=1) # Arrastra el ratón a una nueva posición
```

### Control del Teclado

```python
# Escribir texto (letra por letra, como un usuario)
pyautogui.write('¡Hola, mundo!', interval=0.1) # interval es la pausa entre teclas

# Pulsar teclas individuales
pyautogui.press('enter')
pyautogui.press('f1')
pyautogui.press('left')

# Mantener teclas pulsadas (keyDown y keyUp)
pyautogui.keyDown('shift')
pyautogui.press('4')
pyautogui.keyUp('shift') # Esto escribiría el símbolo '$' en un teclado US

# Combinaciones de teclas (atajos)
pyautogui.hotkey('ctrl', 'c') # Copiar
pyautogui.hotkey('ctrl', 'v') # Pegar
```

### Mensajes y Capturas de Pantalla

```python
# Mostrar un cuadro de diálogo simple
pyautogui.alert('Este es un mensaje de alerta.')

# Tomar una captura de pantalla
im = pyautogui.screenshot()

# Guardar la captura en un archivo
pyautogui.screenshot('mi_captura.png')
```

## Ventajas y Desventajas

### Ventajas 
*   **Universal:** Funciona con cualquier cosa que veas en la pantalla.
*   **Sencillo:** Muy fácil de aprender y usar para tareas rápidas.
*   **Multiplataforma:** El mismo script puede funcionar en Windows, macOS y Linux con pequeños ajustes.

### Desventajas 
*   **Muy Frágil (Breakable):** Es su mayor debilidad. Tu script se romperá si:
    *   La ventana de la aplicación no está en el lugar esperado.
    *   La resolución de la pantalla cambia.
    *   La aplicación se actualiza y un botón cambia de posición.
    *   El script se ejecuta en un ordenador donde los atajos de teclado son diferentes (ej. `Alt+N` vs `Alt+F`).
*   **"Ciego":** `pyautogui` no sabe si el botón en el que va a hacer clic está realmente ahí o si es visible. Simplemente mueve el ratón a una coordenada y hace clic.
*   **Requiere Foco:** La ventana con la que quieres interactuar debe estar activa y en primer plano. Si el usuario hace clic en otro sitio mientras el script se ejecuta, el script interactuará con la ventana equivocada.

**En resumen:** `pyautogui` es como un robot que ha memorizado una secuencia de movimientos. Es increíblemente rápido y eficiente si las condiciones son exactamente las mismas cada vez, pero se confunde fácilmente si algo cambia. Es una herramienta fantástica para prototipos rápidos y automatizaciones personales, pero para sistemas robustos y profesionales en Windows, `pywinauto` suele ser una mejor opción.