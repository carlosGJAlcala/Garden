---
title: "Foca"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  FOCA (Fo)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Metagoofil|Metagoofil]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Recon-ng|Recon ng]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Escalada-de-Privilegios|Escalada de Privilegios]].

- **Nombre completo:** **FOCA** (Fingerprinting Organizations with Collected Archives)
    
- **Símbolo en la tabla:** **Fo**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de análisis de metadatos y footprinting OSINT
    
- **Desarrollador:** ElevenPaths (Telefónica)
    
- **Sitio oficial:** [https://www.elevenpaths.com](https://www.elevenpaths.com/labstools/foca.html)
    

---

##  ¿Qué es FOCA?

**FOCA** es una herramienta de **reconocimiento pasivo** diseñada para **extraer y analizar metadatos de documentos públicos**, como PDFs, DOCX, XLSX, PPT, etc., que estén disponibles en sitios web o repositorios accesibles públicamente. Es especialmente útil para **obtener información interna de una organización**, como:

- Nombres de usuarios y dispositivos
    
- Rutas de sistema de archivos
    
- Versiones de software
    
- Estructura de red o dominio interno
    

Es ampliamente usada en auditorías de seguridad y Red Team por su capacidad de recopilar datos sensibles **sin interactuar directamente con los sistemas**.

---

## ️ Funcionalidades principales

1. **Descubrimiento de documentos públicos**
    
    - Realiza búsquedas en Google, Bing o directamente desde el dominio.
        
    - Busca documentos con extensiones como `.pdf`, `.docx`, `.ppt`, `.xls`, etc.
        
2. **Extracción de metadatos**
    
    - Autor del documento.
        
    - Software usado para crearlo (ej: Microsoft Word 2016).
        
    - Sistema operativo.
        
    - Ruta local de creación (`C:\Users\Juan\Documents\...`).
        
    - Fechas de creación/modificación.
        
    - Nombres de dominio, nombres de equipo, usuarios.
        
3. **Análisis de estructura de red**
    
    - Deducción de **nombres internos de máquinas**.
        
    - Posible mapeo de **nombres de dominio** internos y subredes.
        
4. **Resolución DNS automática**
    
    - FOCA puede tomar nombres descubiertos y resolverlos.
        
    - Intenta hacer **transferencias de zona DNS** si encuentra configuraciones débiles.
        
5. **Mapas gráficos de red interna**
    
    - Representa visualmente lo descubierto (máquinas, relaciones, subdominios).
        
6. **Exportación de resultados**
    
    - Informes detallados en formatos como XML o HTML.
        
    - Mapas de red interactivos.
        

---

##  Casos de uso real en pentesting

- **Descubrir infraestructura interna** sin escaneo activo.
    
- **Obtener usuarios de Active Directory** para ataques de diccionario o fuerza bruta.
    
- **Detectar software vulnerable** (versiones obsoletas de Office, Adobe, etc.).
    
- **Identificar rutas de archivos** que pueden usarse para escalada de privilegios o LFI.
    
- **Recolección de inteligencia previa a ingeniería social**.
    

Ejemplo: Un documento público con metadatos podría mostrar esto:

```text
Author: Juan Pérez
Last Modified By: IT\JGarcia
Application: Microsoft Word 2013
Company: EmpresaSegura S.A.
Document Path: C:\Users\JGarcia\Documents\Proyectos\AuditoriaInterna.docx
```

Esto puede revelar que:

- El usuario `JGarcia` existe.
    
- La máquina probablemente es parte del dominio `IT`.
    
- Se usa Word 2013 → versión vulnerable.
    
- Hay una carpeta “AuditoríaInterna” que puede existir en la red compartida.
    

---

## ️ Cómo usar FOCA

1. **Instalación (Windows)**  
    Descarga desde el sitio oficial de ElevenPaths. Solo funciona en Windows.
    
2. **Nuevo proyecto**  
    Crea un nuevo proyecto y añade el dominio o URL objetivo.
    
3. **Descargar documentos**  
    FOCA usará Google, Bing y otros motores para recopilar documentos públicos.
    
4. **Extraer metadatos**  
    Analiza los documentos descargados y lista los metadatos obtenidos.
    
5. **Enumeración y resolución DNS**  
    Intenta identificar nombres de hosts y resolverlos.
    
6. **Exportar informe o mapa**  
    Puedes guardar todo para presentación o análisis posterior.
    

---

##  Consideraciones de defensa (Blue Team)

FOCA expone el riesgo de:

- Subir documentos sin limpiar metadatos (Word, PDF, etc.).
    
- Configuraciones débiles en DNS (permitir AXFR).
    
- Software desactualizado incrustado en los metadatos.
    

###  Buenas prácticas:

- Usar herramientas como `exiftool` para limpiar metadatos antes de publicar documentos.
    
- Aplicar DLP (Data Loss Prevention) en servidores públicos.
    
- Bloquear transferencias de zona DNS a IPs no autorizadas.
    

---

##  Herramientas relacionadas

|Herramienta|Función similar|
|---|---|
|`exiftool`|Extracción manual de metadatos|
|`metagoofil`|Similar a FOCA, pero en consola|
|`strings`|Extracción de texto de binarios|
|`recon-ng`|Puede usar fuentes para documentos|
|`SpiderFoot`|OSINT y metadatos entre otras cosas|

---

##  Conclusión

FOCA es una herramienta **esencial para la recolección pasiva de información en pruebas de intrusión**. Su interfaz amigable y enfoque gráfico la hacen ideal para pentesters que deseen explorar estructuras internas de una empresa **sin realizar ningún escaneo activo**.

¿Te gustaría que prepare un caso práctico completo usando un dominio real o una guía paso a paso para analizar metadatos con FOCA y complementarlo con `exiftool`?