---
title: "Xdocreport"
date: 2026-01-26
tags:
  - desarrollo-software
  - java
---
Te lo explico a fondo, porque **XDocReport** es de esas librerías en Java que parecen sencillas, pero bien usadas son muy potentes cuando quieres trabajar con **plantillas de Word u OpenDocument** y rellenarlas con datos dinámicos.

---

## 1. Qué es XDocReport


> **Relacionado**: [[03-Desarrollo-Software/Java/JASPER|JASPER]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

Es una librería Java open source diseñada para **fusionar datos con plantillas** en formatos:

- **DOCX** (Microsoft Word)
    
- **ODT** (OpenDocument Text de LibreOffice/OpenOffice)
    

La idea es:

- Diseñas la plantilla **directamente** en Word o LibreOffice (con todo el formato, estilos, imágenes, tablas…).
    
- En esa plantilla insertas **placeholders** (marcadores) como `${nombre}`, `${fecha}`, `${items.descripcion}` usando sintaxis de motor de plantillas.
    
- Desde Java, cargas la plantilla y le pasas un mapa de datos o un objeto Java (bean).
    
- XDocReport reemplaza los placeholders y genera el documento final.
    

---

## 2. Motores de plantillas soportados

XDocReport no se inventa su propia sintaxis, sino que usa **motores de plantillas** ya conocidos:

- **Freemarker**
    
- **Velocity**
    

La sintaxis de `${campo}` o `${objeto.propiedad}` dependerá del motor que elijas.  
Esto permite que puedas hacer incluso condicionales (`#if`, `#foreach`) y bucles dentro del documento.

---

## 3. Flujo típico de uso

1. **Diseñar la plantilla**  
    Abres Word o LibreOffice, escribes tu documento con formato corporativo y, donde quieras datos dinámicos, escribes `${nombre}`, `${fecha}`, etc.  
    Si tienes listas o tablas repetitivas, usas la sintaxis de bucle de Freemarker o Velocity:
    
    ```
    #foreach($item in $items)
    - $item.descripcion ($item.precio)
    #end
    ```
    
2. **Cargar la plantilla en Java**
    
    ```java
    InputStream in = new FileInputStream("plantilla.docx");
    IXDocReport report = XDocReportRegistry.getRegistry()
        .loadReport(in, TemplateEngineKind.Freemarker);
    ```
    
3. **Definir los metadatos si hay listas**
    
    ```java
    FieldsMetadata metadata = report.createFieldsMetadata();
    metadata.addFieldAsList("items");
    ```
    
4. **Pasar los datos**
    
    ```java
    IContext context = report.createContext();
    context.put("nombre", "Mario");
    context.put("fecha", "2025-08-14");
    context.put("items", Arrays.asList(
        new Producto("Camiseta", 15.99),
        new Producto("Pantalón", 35.50)
    ));
    ```
    
5. **Generar el documento final**
    
    ```java
    OutputStream out = new FileOutputStream("salida.docx");
    report.process(context, out);
    ```
    

---

## 4. Ventajas frente a JasperReports

- **Diseño 100% en Word/LibreOffice**: los usuarios no técnicos pueden editar la plantilla sin aprender JRXML.
    
- **Fidelidad de formato**: el documento final es un DOCX/ODT completamente editable, sin “artefactos” de exportación.
    
- **Curva de aprendizaje baja**: si sabes usar Freemarker o Velocity, ya puedes hacer plantillas.
    
- Ideal para **cartas, contratos, certificados** o documentos narrativos con datos dinámicos.
    

---

## 5. Limitaciones

- No tiene motor de informes como Jasper (no hay bandas, paginación, agrupaciones automáticas, charts integrados).
    
- Si quieres gráficos o tablas dinámicas complejas, tendrás que generarlas antes e insertarlas como imagen o tabla en Word.
    
- No es tan bueno para listados largos paginados o cálculos agregados en el propio motor.
    

---

## 6. Cuándo elegirlo

- Si tu plantilla **ya existe** en Word y quieres automatizarla.
    
- Si el equipo de negocio quiere editar el formato sin pasar por un desarrollador.
    
- Si la salida final debe ser **editable** en Word sin perder formato.
    
- Si los datos ya vienen preparados desde la aplicación (JSON, objetos Java).
    

---

Si quieres, puedo prepararte **un ejemplo funcional con XDocReport usando una plantilla Word con bucles y campos simples**, para que veas cómo desde Java se sustituyen los datos y obtienes el `.docx` listo para enviar.  
Así podrías compararlo directamente con el flujo que te mostré antes de Jasper.