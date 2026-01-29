---
title: "Winget"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - windows
---

##  **`winget`: el gestor de paquetes oficial de Windows**


> **Relacionado**: [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

`winget` (Windows Package Manager) es la herramienta oficial de Microsoft para instalar, actualizar, configurar y desinstalar aplicaciones desde la terminal en Windows. Funciona a partir de **Windows 10 versión 1809** y en **Windows 11**, siempre que se tenga instalada la app **App Installer** desde la Microsoft Store.

Con `winget`, Microsoft ofrece por fin una alternativa nativa a gestores de paquetes de terceros como **Chocolatey** o **Scoop**, muy similar a lo que `apt` es en Debian/Ubuntu o `brew` en macOS.

---

### **Ventajas de `winget` frente a Chocolatey**

1. **Integración nativa**
    
    - No necesitas instalar software de terceros.
        
    - Está soportado oficialmente por Microsoft y recibe actualizaciones a través de Windows Update o la Microsoft Store.
        
2. **Repositorio oficial y seguro**
    
    - Usa el repositorio mantenido por Microsoft.
        
    - Permite instalar desde Microsoft Store, GitHub Releases y enlaces directos.
        
    - Validación de integridad y firmas digitales.
        
3. **Comodidad y simplicidad**
    
    - Sintaxis clara y directa.
        
    - Permite instalar, actualizar y eliminar apps en segundos.
        
    - Puede actualizar todas las apps compatibles con un solo comando.
        
4. **Compatibilidad empresarial**
    
    - Soporte para scripts de automatización en PowerShell.
        
    - Integración con políticas de seguridad y control en entornos corporativos.
        

---

### **Cuándo seguir usando Chocolatey**

Aunque `winget` cubre la mayoría de casos, Chocolatey sigue teniendo ventajas en algunos escenarios:

- **Catálogo más amplio**: incluye aplicaciones y utilidades que aún no están en el repositorio oficial de Microsoft.
    
- **Instalaciones más personalizadas**: permite ejecutar scripts antes, durante y después de la instalación.
    
- **Integración con DevOps y CI/CD**: muy usado en pipelines de automatización.
    
- **Compatibilidad con versiones antiguas de Windows**: funciona desde Windows 7.
    

---

### **Ejemplos de uso de `winget`**

- **Buscar aplicación**
    
    ```powershell
    winget search vlc
    ```
    
- **Instalar aplicación**
    
    ```powershell
    winget install VideoLAN.VLC
    ```
    
- **Actualizar todo**
    
    ```powershell
    winget upgrade --all
    ```
    
- **Listar instaladas**
    
    ```powershell
    winget list
    ```
    
- **Desinstalar aplicación**
    
    ```powershell
    winget uninstall VideoLAN.VLC
    ```
    

---

 **Conclusión**: Hoy en día, `winget` es el gestor de paquetes recomendado para la mayoría de usuarios y entornos corporativos que usen Windows 10 o 11. Chocolatey sigue siendo relevante si necesitas paquetes fuera del repositorio oficial o integraciones muy específicas, pero ya no es la única opción sólida.

---



---

### Sitios web recomendados para explorar catálogos de `winget`

- **[winstall.app](https://winstall.app/)**  
    Un portal muy visual que te permite buscar entre más de 9 500 aplicaciones. Puedes seleccionarlas y generar una única línea de comando `winget install …` lista para copiar y pegar ([winstall.app](https://winstall.app/?utm_source=chatgpt.com "winstall: Browse the winget repository"), [Trailhead Technology Partners](https://trailheadtechnology.com/manage-your-windows-applications-with-winget/?utm_source=chatgpt.com "Manage Your Windows Applications With Winget")).
    
- **[winget.run](https://winget.run/)**  
    Otro sitio que facilita la búsqueda y descubrimiento de paquetes. Muestra los ID de los paquetes y los comandos correspondientes para su instalación ([GitHub](https://github.com/microsoft/winget-cli?utm_source=chatgpt.com "WinGet is the Windows Package Manager. ...")).
    

---

- También puedes consultar directamente el repositorio oficial de **manifests de Microsoft** en GitHub (`microsoft/winget-pkgs`), donde están todos los archivos de descripción (YAML, JSON…) de los paquetes disponibles en el catálogo comunitario ([GitHub](https://github.com/microsoft/winget-pkgs?utm_source=chatgpt.com "microsoft/winget-pkgs: The Microsoft community Windows ...")).
    

---

### Cómo usar estos sitios

- En **winstall.app**, simplemente busca la aplicación que te interesa (ej. _Firefox_), la seleccionas y la web te mostrará algo como:
    
    ```
    winget install Mozilla.Firefox
    ```
    
- En **winget.run**, podrás visualizar datos como el nombre, la versión, y el comando de instalación preciso.
    

---

### Vista rápida

|Plataforma|Lo que ofrece|
|---|---|
|**winstall.app**|Interfaz visual, seleccionar múltiples apps y generar comando compuesto|
|**winget.run**|Búsqueda y comando directo por paquete|
|**GitHub `winget-pkgs`**|Inspección manual de manifiestos en bruto (ideal para scripting)|

---

¿Te gustaría que te prepare una sección con tus comandos favoritos listos para usar, o una pequeña guía en PowerShell para automatizar instalaciones usando `winget export` e `import`?