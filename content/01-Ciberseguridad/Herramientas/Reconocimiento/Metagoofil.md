---
title: "Metagoofil"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  Metagoofil (mt)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Recon-ng|Recon ng]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

- **Nombre completo:** **Metagoofil**
    
- **Símbolo en la tabla:** **mt**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta OSINT para extracción de metadatos desde documentos públicos
    
- **Lenguaje:** Python
    
- **Repositorio oficial (archivado):** [https://github.com/laramies/metagoofil](https://github.com/laramies/metagoofil)
    
- **Estado del proyecto:** No actualizado desde 2013, pero aún útil en entornos controlados
    

---

##  ¿Qué es Metagoofil?

**Metagoofil** es una herramienta de recolección de información (OSINT) que **busca, descarga y analiza documentos públicos publicados en sitios web**, extrayendo de ellos **metadatos incrustados** que pueden contener información sensible.

Está enfocada en documentos comunes como:

- `.pdf` (Adobe Acrobat)
    
- `.doc/.docx` (Microsoft Word)
    
- `.ppt/.pptx` (PowerPoint)
    
- `.xls/.xlsx` (Excel)
    
- `.odt`, `.ods`, `.odp` (LibreOffice)
    

Metagoofil se apoya en motores de búsqueda (especialmente Google) para **descubrir archivos públicos**, y luego utiliza herramientas como `exiftool` o `strings` para **extraer los metadatos** incrustados.

---

##  ¿Qué puede revelar Metagoofil?

|Metadato extraído|Posible información sensible|
|---|---|
|Autor del documento|Nombres y apellidos de empleados|
|Organización|Nombre exacto interno de la empresa|
|Ruta del archivo|Directorio local de creación del documento (ej: `C:\Users\Admin`)|
|Fecha de creación/modificación|Cronología de trabajo interno|
|Nombre de la máquina|Hostnames, posibles targets para LLMNR, NetBIOS o AD|
|Versión del software|Indicios de software desactualado o vulnerable|

---

## ️ Flujo de trabajo de Metagoofil

1. **Buscar documentos públicos**:
    
    - Realiza consultas Google personalizadas como:  
        `site:empresa.com filetype:pdf`
        
2. **Descargar los documentos**:
    
    - Guarda copias locales en un directorio temporal.
        
3. **Extraer metadatos automáticamente**:
    
    - Usa herramientas embebidas o externas como `pdfinfo`, `exiftool`, `strings`, etc.
        
4. **Generar informe**:
    
    - Lista los autores, rutas, software, hostnames y patrones repetidos.
        

---

##  Ejemplo de uso

```bash
python metagoofil.py -d ejemplo.com -t pdf,doc,xls,ppt -l 100 -n 20 -o resultados -f informe.html
```

- `-d`: dominio a buscar (ej: ejemplo.com)
    
- `-t`: tipos de archivo (pdf, doc, xls, etc.)
    
- `-l`: número máximo de resultados en Google
    
- `-n`: máximo de archivos a descargar
    
- `-o`: carpeta de salida
    
- `-f`: nombre del informe generado
    

---

##  Casos de uso reales

- En un pentest interno, Metagoofil descubre que todos los documentos de `empresa.com` fueron creados por `j.santos@empresa.local`, y contienen rutas como `C:\Users\JSantos\Documents\Confidencial\...`.
    
- Esta información sugiere:
    
    - Un nombre de usuario de Active Directory (`JSantos`)
        
    - Una posible ruta compartida en red
        
    - Un sistema con Word 2007 (software desactualizado)
        
- La combinación de estos datos permite construir ataques más dirigidos (ingeniería social, spear phishing, brute force, etc.).
    

---

##  Requisitos y dependencias

Metagoofil fue creado para Python 2.7, lo cual significa que hoy en día:

- Puede requerir entorno virtual o Docker para ejecutarlo correctamente.
    
- Es recomendable **usar una VM de análisis con herramientas forenses** (REMnux, Kali, FLARE) si se quiere ejecutar de forma moderna.
    
- Alternativamente, puedes replicar su funcionalidad usando `Google Dorking + wget + exiftool`.
    

---

##  Alternativas más modernas

|Herramienta|Características destacadas|
|---|---|
|**FOCA**|GUI en Windows, más moderna, integrada|
|`exiftool`|CLI potente para extracción manual|
|`pdfinfo`|Información básica de documentos PDF|
|`strings`|Búsqueda rápida de texto incrustado|
|`SpiderFoot`|Framework OSINT automatizado con módulos|
|`Recon-ng`|Puede descargar y analizar documentos|

---

##  Relevancia para Blue Team

Desde una perspectiva defensiva, Metagoofil demuestra la importancia de:

- **Eliminar metadatos de documentos públicos** antes de su publicación.
    
- Usar herramientas como `exiftool -all= archivo.pdf` para limpiar datos.
    
- Configurar DLP para evitar filtraciones por documentos.
    
- Mantener control sobre qué empleados tienen permiso de publicación.
    

---

##  Conclusión

**Metagoofil** es una herramienta clásica, pero aún útil, para obtener **información estructural interna de una organización** a través de documentos publicados en Internet. Su utilidad está en la fase de **reconocimiento pasivo**, especialmente cuando se combina con ingeniería social, spear phishing o enumeración interna posterior.

---

¿Quieres que prepare un ejemplo completo con búsqueda, descarga y análisis de metadatos desde un dominio real? ¿O una alternativa moderna en Python 3 que replique las funciones de Metagoofil con herramientas actuales como `googlesearch`, `wget` y `exiftool`?