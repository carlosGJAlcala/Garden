---
title: "Pades"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema1principiosbasicossi
---
Perfecto. Vamos a explicar en profundidad qué es la **firma PAdES (PDF Advanced Electronic Signature)**, cómo funciona, sus ventajas, tipos y en qué se diferencia de otras firmas como XAdES y CAdES.

---

##  ¿Qué es PAdES?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/LSSI|LSSI]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**PAdES** es un estándar de **firma electrónica avanzada** para documentos **PDF**, definido por la norma europea **ETSI EN 319 142**.  
Su objetivo es **firmar digitalmente archivos PDF**, asegurando su **autenticidad, integridad y validez legal a largo plazo**, según el reglamento europeo **eIDAS**.

> Es el formato de firma **más usado en entornos administrativos, jurídicos y corporativos**, cuando el documento a firmar es un PDF.

---

##  ¿Qué añade PAdES?

- Certificado digital del firmante (ej. DNIe, FNMT, ACCV…)
    
- Fecha y hora de la firma (con o sin sello de tiempo)
    
- Información del firmante
    
- Política de firma electrónica aplicada
    
- Posibilidad de **firma visible en el documento**
    
- Soporte para múltiples firmas acumulativas
    

---

##  ¿Por qué es tan usado?

- No requiere herramientas especiales para su visualización: **Adobe Reader** u otros lectores PDF ya soportan validación de firmas.
    
- Compatible con procedimientos como:
    
    - Firma de contratos
        
    - Presentación de escritos
        
    - Tramitación electrónica en AAPP
        
    - Procesos judiciales o notariales
        

---

##  Tipos o niveles de firma PAdES

|Nivel|Descripción|
|---|---|
|**PAdES-BES**|Firma básica con certificado digital y datos del firmante|
|**PAdES-EPES**|Igual que BES pero incluye política explícita de firma|
|**PAdES-T**|Añade **marca de tiempo confiable** para evitar repudio|
|**PAdES-LTV**|_Long-Term Validation_: permite validar la firma incluso después de expirar el certificado, incluyendo OCSP/CRL|

 En España, muchas firmas PDF emitidas con **AutoFirma** o **Cl@ve Firma** utilizan PAdES-T o PAdES-LTV.

---

## ️ Cumplimiento legal

- Totalmente **válida legalmente según eIDAS**
    
- **Admitida en procedimientos administrativos** (Ley 39/2015)
    
- Admite firmas de personas físicas, jurídicas o sellos de entidad
    

---

##  Herramientas comunes para firmar PAdES

- **AutoFirma** (Gobierno de España)
    
- **Adobe Acrobat Pro**
    
- **Cl@ve Firma**
    
- **Firmadores corporativos** (LSSI, ValidE, etc.)
    
- **APIs de firma electrónica en la nube** (Signaturit, DocuSign, Lleida.net…)
    

---

##  Diferencias entre PAdES, XAdES y CAdES

|Formato|Para qué tipo de documentos|Estándar base|Soporte visible|Usos comunes|
|---|---|---|---|---|
|**PAdES**|PDF|PDF + CMS| (firma visible)|Firmas administrativas, contratos, justicia|
|**XAdES**|XML|XMLDSig||Facturas electrónicas, trámites estructurados|
|**CAdES**|Binarios (no PDF/XML)|CMS/PKCS#7||Firmas de software, ficheros ZIP, multimedia|

---

##  Conclusión

> **PAdES** es el estándar más usado para firmar digitalmente documentos PDF con **validez legal plena en Europa**.  
> Es sencillo de validar, flexible, soporta múltiples niveles de firma y es el **preferido por las Administraciones Públicas y empresas privadas** para tramitar documentación de forma segura.

---

¿Quieres que te prepare un ejemplo paso a paso de cómo firmar un PDF con AutoFirma o cómo validar una firma PAdES con Adobe Acrobat? ¿O una tabla comparativa entre PAdES y XAdES para justificar su uso en licitaciones?