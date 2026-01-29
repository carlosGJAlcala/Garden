---
title: "Facturae"
date: 2025-01-01
tags:
  - desarrollo-software
---

## **1. Qué es Facturae**


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

**Facturae** es el **formato oficial de factura electrónica en España**, definido por la Administración General del Estado (AGE) y basado en un estándar **XML**.  
Su finalidad es garantizar que las facturas electrónicas tengan **un formato estructurado, interoperable y seguro**, especialmente para la comunicación con el sector público.

Se utiliza principalmente para:

- **B2G (Business to Government)**: facturación de empresas a administraciones públicas, donde su uso es obligatorio desde el **15 de enero de 2015** para la AGE, comunidades autónomas y muchos entes locales.
    
- **B2B**: aunque no es obligatorio en todas las transacciones privadas, puede usarse y se está impulsando con la nueva Ley “Crea y Crece”, que establece la obligatoriedad de la factura electrónica entre empresas en los próximos años.
    

---

## **2. Estructura técnica del formato**

Facturae es un **XML estructurado** que sigue un esquema XSD publicado por el Ministerio de Asuntos Económicos y Transformación Digital.  
Dentro del XML hay diferentes bloques de información:

- **Cabecera**: metadatos de la factura (versión, número, fecha, tipo de documento).
    
- **Datos del emisor y receptor**: NIF, razón social, direcciones, etc.
    
- **Líneas de detalle**: productos o servicios facturados, cantidades, precios unitarios, impuestos aplicados.
    
- **Totales**: importes brutos, bases imponibles, IVA, retenciones, importe total.
    
- **Forma de pago**: transferencia, domiciliación, etc.
    
- **Firma electrónica**: firma XAdES-BES integrada en el XML para garantizar integridad, autenticidad y no repudio.
    

---

## **3. Versiones más importantes**

Las más relevantes en los últimos años son:

- **Facturae 3.2.1**: muy utilizada, aunque está en proceso de sustitución.
    
- **Facturae 3.2.2**: la versión vigente y recomendada. Añade campos para:
    
    - Tipos de cambio y moneda extranjera.
        
    - Detalle de impuestos retenidos.
        
    - Mayor soporte para operaciones intracomunitarias.
        

---

## **4. Firma y validación**

La factura Facturae debe ir firmada electrónicamente con un **certificado digital reconocido** (FNMT, Camerfirma, etc.).

- Se utiliza una **[[Firma-XaDES]]** (XML Advanced Electronic Signatures – Basic Electronic Signature).
    
- Antes de enviarla, se valida el XML contra el esquema oficial y se comprueba la firma.
    

Existen herramientas como:

- **Programa Facturae** (oficial, gratuito).
    
- **Validador de FACe** (online).
    
- Bibliotecas de terceros para integrarlo en ERPs.
    

---

## **5. Envío a las Administraciones Públicas**

Cuando se factura a un organismo público, el XML Facturae se envía a través de **FACe** (Punto General de Entrada de Facturas Electrónicas) o la plataforma equivalente de la administración correspondiente (por ejemplo, FACeB2B o plataformas autonómicas).

**Datos clave en B2G**:

- **Código DIR3**: identifica el órgano administrativo de destino.
    
- **Registro y seguimiento**: FACe devuelve un número de registro y estados de tramitación (recibida, registrada, aceptada, rechazada, pagada).
    

---

## **6. Ventajas del Facturae**

- **Formato estructurado**: fácil de procesar por sistemas de gestión.
    
- **Seguridad jurídica**: integridad y autenticidad mediante firma digital.
    
- **Cumplimiento normativo**: obligatorio en facturación a la Administración.
    
- **Ahorro**: reduce papel, tiempos y costes de envío.
    
- **Interoperabilidad**: válido en todo el ámbito nacional y reconocido en entornos europeos (adaptable a EN16931).
    

---

## **7. Facturae en el futuro B2B**

La **Ley “Crea y Crece”** va a extender la factura electrónica obligatoria entre empresas. El borrador del Real Decreto establece que se podrán usar formatos estructurados como **Facturae**, **UBL**, **CII** o **EDIFACT**, y que las plataformas deberán ser interoperables.  
Esto significa que Facturae podría pasar de ser un formato centrado en la administración pública a convertirse en uno de los principales formatos estándar para **todas las relaciones comerciales en España**.

---

Si quieres, puedo prepararte **un ejemplo real de XML Facturae 3.2.2 comentado línea por línea**, para que entiendas qué significa cada etiqueta y cómo se construye una factura válida.  
¿Quieres que lo haga?