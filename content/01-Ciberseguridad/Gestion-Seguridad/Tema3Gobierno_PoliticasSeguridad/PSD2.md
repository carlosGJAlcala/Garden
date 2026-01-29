--- 
title: PSD2
---

**PSD2** es la segunda Directiva Europea sobre Servicios de Pago:

> **Payment Services Directive 2 – Directiva (UE) 2015/2366**

Entró en vigor en **enero de 2018**, y su objetivo es **modernizar, abrir y hacer más segura la banca y los servicios de pago** en Europa.

---

##  Objetivos principales de PSD2


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

1. **Fomentar la innovación**: obliga a los bancos a abrir su infraestructura (Open Banking).
    
2. **Aumentar la seguridad** de los pagos digitales y operaciones online.
    
3. **Proteger al consumidor** frente al fraude.
    
4. **Facilitar la aparición de nuevos actores** (fintechs) en el ecosistema financiero europeo.
    

---

##  ¿A quién aplica?

- **Entidades bancarias tradicionales** (bancos, cajas, etc.)
    
- **Proveedores de servicios de pago** (TPP – Third Party Providers)
    
- **Comercios electrónicos y pasarelas de pago**
    
- **Usuarios y consumidores finales**
    

---

##  Principales novedades de PSD2

###  1. **Open Banking – Acceso a cuentas**

Los bancos están obligados a **dar acceso a terceros autorizados** (TPPs) a las cuentas de los clientes, mediante **APIs seguras**.

Los TPP se dividen en:

- **AISP (Account Information Service Providers)**: pueden consultar tus movimientos (por ejemplo, apps de finanzas personales).
    
- **PISP (Payment Initiation Service Providers)**: pueden iniciar pagos en tu nombre (por ejemplo, para pagar en Amazon sin tarjeta).
    

 Siempre con tu **consentimiento explícito**.

---

###  2. **SCA – Strong Customer Authentication**

PSD2 obliga a aplicar **autenticación fuerte** para operaciones electrónicas:

>  Mínimo **2 de 3 factores**:

- Algo que sabes (contraseña, PIN)
    
- Algo que tienes (móvil, token)
    
- Algo que eres (biometría)
    

 Por ejemplo: **contraseña + SMS**, o **huella + código temporal**.

SCA se aplica en:

- Inicios de sesión en banca online
    
- Pagos electrónicos (excepto ciertas exenciones)
    
- Acceso a información de cuenta
    

---

###  3. **Responsabilidades legales**

- Las **entidades financieras son responsables de los fraudes** si no se aplica correctamente la SCA.
    
- Se debe notificar a las autoridades en caso de **fallos de seguridad**.
    
- Los TPP deben **estar registrados y supervisados** por el Banco Central correspondiente (en España, el **Banco de España**).
    

---

##  Impacto en ciberseguridad

- Refuerza el uso de **MFA (autenticación multifactor)**
    
- Requiere **encriptación, protección de APIs y tokens seguros**
    
- Aumenta la necesidad de:
    
    - **Gestión de riesgos**
        
    - **Monitoreo de fraude**
        
    - **Auditoría de accesos y logs**
        

---

## ️ Relación con otras normativas

|Norma|Relación con PSD2|
|---|---|
|**RGPD**|PSD2 exige consentimiento explícito → debe cumplir con protección de datos personales.|
|**eIDAS**|Uso de certificados electrónicos y firmas digitales.|
|**ENS**|Si la entidad trabaja con AAPP o en España.|

---

##  Conclusión

> **PSD2 transforma el sistema financiero europeo**, obligando a bancos y fintechs a **compartir datos con seguridad, habilitar pagos más abiertos, y proteger mejor a los usuarios mediante autenticación fuerte**.  
> Es una directiva **tecnológica, legal y de seguridad** que ha marcado un antes y un después en la **ciberseguridad bancaria**.

---

¿Quieres que te prepare un resumen visual de PSD2 con sus actores, flujos y medidas de seguridad? ¿O una comparativa entre PSD2, RGPD y eIDAS para un trabajo académico o presentación profesional?