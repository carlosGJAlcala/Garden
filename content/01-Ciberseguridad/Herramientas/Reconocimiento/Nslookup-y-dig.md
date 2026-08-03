---
title: "Nslookup Y Dig"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

## Nslookup / Dig


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

####  **¿Qué son?**

 Ambas son herramientas que permiten **consultar registros DNS**, es decir, preguntar a los servidores DNS para obtener información sobre nombres de dominio, direcciones IP y mucho más:

- **`nslookup`:**  
    Herramienta clásica incluida en prácticamente todos los sistemas operativos (Windows y Unix-like).  
    Sencilla pero con menos opciones avanzadas.
    
- **`dig` (Domain Information Groper):**  
    Herramienta más avanzada y flexible, especialmente popular en entornos Unix/Linux.
    

---

####  **Uso en pentesting**

 Son clave en la fase de **reconocimiento** para:

- Obtener direcciones IP de objetivos (A/AAAA records).
- Descubrir subdominios y zonas.
- Consultar registros importantes:
    - **MX (Mail Exchange)**
    - **NS (Name Server)**
    - **TXT (incluye registros SPF/DKIM)**
    - **SOA (Start of Authority)**
- Intentar **zone transfer (`AXFR`)** → si está mal configurada, puede revelar todo el contenido DNS del dominio objetivo (grave vulnerabilidad).

---

####  **Comandos básicos con `nslookup`**

-  Resolver dominio:
    
    ```bash
    nslookup www.ejemplo.com
    ```
    
-  Consultar tipo específico de registro:
    
    ```bash
    nslookup -query=MX ejemplo.com
    ```
    
-  Consultar usando un servidor DNS concreto:
    
    ```bash
    nslookup www.ejemplo.com 8.8.8.8
    ```
    
-  Intentar zone transfer (si el servidor lo permite):
    
    ```bash
    nslookup
    > server ns1.ejemplo.com
    > ls -d ejemplo.com
    ```
    

---

####  **Comandos básicos con `dig`**

-  Resolver dominio:
    
    ```bash
    dig www.ejemplo.com
    ```
    
-  Consultar registros MX:
    
    ```bash
    dig MX ejemplo.com
    ```
    
-  Consultar usando un servidor DNS concreto:
    
    ```bash
    dig @8.8.8.8 www.ejemplo.com
    ```
    
-  Consultar registros NS:
    
    ```bash
    dig NS ejemplo.com
    ```
    
-  Intentar zone transfer:
    
    ```bash
    dig AXFR ejemplo.com @ns1.ejemplo.com
    ```
    

---

####  **Comparativa rápida**

|Herramienta|Ventajas|Limitaciones|
|---|---|---|
|**nslookup**|Fácil de usar, integrada en Windows|Menos detallada y flexible|
|**dig**|Salida detallada, opciones avanzadas, más precisa|No siempre está instalada por defecto en Windows|

---

####  **Impacto en pentesting**

- Información que puedes obtener:
    - IPs de sistemas.
    - Estructura de subdominios.
    - Servidores de correo → posible vector de ataque (ej: phishing).
    - Servidores autoritativos → prueba de configuración (ej: zone transfer mal configurado).

---

####  **Mitigaciones para protegerse**

 **Hardening DNS corporativo:**

- Bloquear **zone transfers no autorizadas** (`AXFR` debe permitirse solo a servidores secundarios autorizados).
- Revisar registros DNS públicos para evitar filtraciones innecesarias (subdominios sensibles).
- Usar configuraciones adecuadas de registros SPF/DKIM para evitar abusos.

---

 **Resumen rápido para recordar:**

>  **`nslookup` y `dig`: herramientas fundamentales de reconocimiento DNS.**  
> Permiten consultar registros, descubrir información sensible y detectar configuraciones incorrectas (como zone transfer abierto).  
> Clave en la **fase de reconocimiento en pentesting**.