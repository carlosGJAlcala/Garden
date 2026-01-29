---
title: "Firma Xades"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema1principiosbasicossi
---
Perfecto. Vamos a desarrollar de forma clara qué es la **firma XAdES** (XML Advanced Electronic Signature), para qué se usa, cómo funciona y por qué es importante especialmente en **entornos administrativos, jurídicos y gubernamentales**.

---

##  ¿Qué es la firma XAdES?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema1PrincipiosBasicosSI/PAdES|PAdES]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**XAdES (XML Advanced Electronic Signature)** es un **formato de firma electrónica avanzada**, diseñado para firmar documentos electrónicos en formato **XML** de forma **legalmente vinculante**, cumpliendo con normativas europeas como **eIDAS** y leyes nacionales como la **Ley 39/2015** en España.

> Es una extensión del estándar **XMLDSig (XML Digital Signature)** con mejoras que garantizan **validez jurídica, integridad y autenticidad a largo plazo**.

---

##  ¿Qué añade XAdES sobre una firma digital básica?

- Información del **firmante** (nombre, certificado)
    
- **Marca temporal** para demostrar cuándo se firmó
    
- **Política de firma** aplicada
    
- **Referencias cruzadas** con los datos firmados
    
- Posibilidad de incluir **varias firmas** en un solo documento
    

---

##  Tipos de XAdES (perfiles)

|Perfil|Descripción|
|---|---|
|**XAdES-BES**|Firma básica con certificado, datos del firmante y referencia al documento|
|**XAdES-EPES**|Añade política de firma (como sello oficial de una entidad pública)|
|**XAdES-T**|Añade **marca de tiempo** (timestamp) para evitar repudio|
|**XAdES-C**|Añade referencias a los certificados y validaciones CRL/OCSP|
|**XAdES-X-L**|Añade los certificados de validación a largo plazo (archivable)|
|**XAdES-A**|Para **archivado legal a largo plazo**, actualizable con el tiempo|

 A mayor nivel, **más garantías legales y durabilidad**, aunque más complejidad técnica.

---

##  ¿Para qué se usa XAdES?

- Firmar documentos en procedimientos electrónicos oficiales
    
- **Intercambio de datos estructurados** firmados (como facturas electrónicas, expedientes administrativos, contratos)
    
- Garantizar la validez jurídica de documentos XML incluso **años después**
    
- Cumplir requisitos del **ENS (Esquema Nacional de Seguridad)** en España
    

---

##  Normativa relacionada

- **eIDAS (Reglamento UE 910/2014)**: regula la validez legal de las firmas electrónicas en Europa.
    
- **Ley 39/2015** y **Ley 40/2015**: regulan el procedimiento administrativo electrónico en España.
    
- **ENS**: exige el uso de firma electrónica avanzada o cualificada en trámites administrativos.
    

---

## ️ Herramientas y plataformas que usan XAdES

- **@firma y AutoFirma** (Ministerio de Hacienda y Función Pública)
    
- **Cl@ve firma**
    
- **VALIDe** (verificador de firma del gobierno de España)
    
- **Plataformas de tramitación electrónica** (SIA, GEISER, Notific@…)
    

---

##  Ventajas de XAdES

- Adaptado a **documentos XML estructurados**
    
- Permite firmar **datos parciales o múltiples nodos**
    
- Compatible con entornos de administración electrónica
    
- **Escalable y extensible** (firmas múltiples, sello de tiempo, custodia)
    

---

## ️ Consideraciones técnicas

- No es compatible con formatos PDF ni binarios (para eso se usa PAdES o CAdES)
    
- Requiere validadores especializados (no basta con Acrobat o visor de texto)
    
- Puede contener múltiples niveles de firma encadenados
    

---

##  Conclusión

> **XAdES es el estándar de firma electrónica avanzada para documentos XML** en la administración pública y muchos entornos jurídicos.  
> Garantiza **autenticidad, integridad, no repudio y validez legal**, incluso a largo plazo, y es una pieza clave en la **transformación digital del sector público** en España y Europa.

---

¿Quieres que te prepare un esquema visual de los niveles XAdES o un ejemplo práctico con XML firmado?