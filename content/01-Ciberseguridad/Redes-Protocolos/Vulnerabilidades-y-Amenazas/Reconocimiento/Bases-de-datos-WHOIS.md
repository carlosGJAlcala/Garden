---
title: "Bases De Datos Whois"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Bases de datos WHOIS – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

**WHOIS** es un protocolo y una base de datos pública que permite consultar **quién es el responsable de un nombre de dominio o de una dirección IP**. Es una herramienta fundamental en la fase de **footprinting (reconocimiento pasivo)** durante una auditoría o ciberataque, ya que proporciona información valiosa sobre el objetivo **sin necesidad de interactuar con sus sistemas**.

---

###  ¿Qué información proporciona WHOIS?

Una consulta WHOIS puede devolver:

- **Nombre del propietario del dominio**
    
- **Organización a la que pertenece**
    
- **Emails de contacto (técnico, administrativo, abuso)**
    
- **Fechas de creación, expiración y última modificación**
    
- **Servidores DNS asociados**
    
- **Estado del dominio (bloqueado, activo, transferible, etc.)**
    
- En algunos casos: dirección postal, número de teléfono, etc.
    

---

###  ¿Qué se puede consultar?

#### 1. **Dominios**

Ejemplo de consulta para `example.com`:

```bash
whois example.com
```

Devuelve:

```text
Registrar: XYZ Registrar Inc.
Registrant Name: John Smith
Registrant Organization: Example Corp
Email: john.smith@example.com
Creation Date: 2000-01-01
Expiration Date: 2030-01-01
Name Servers: ns1.example.com, ns2.example.com
```

#### 2. **Direcciones IP y bloques IP**

Ejemplo con una IP:

```bash
whois 8.8.8.8
```

Devuelve información como:

```text
NetName: GOOGLE
OrgName: Google LLC
CIDR: 8.8.8.0/24
Country: US
```

---

###  Principales registros WHOIS

|Región|Registro|Web oficial|
|---|---|---|
|Global (gTLDs como .com, .net)|ICANN / Verisign|[whois.verisign-grs.com](https://whois.verisign-grs.com/)|
|Europa|RIPE NCC|[ripe.net](https://www.ripe.net/)|
|Norteamérica|ARIN|[arin.net](https://www.arin.net/)|
|Asia-Pacífico|APNIC|[apnic.net](https://www.apnic.net/)|
|Latinoamérica|LACNIC|[lacnic.net](https://www.lacnic.net/)|
|África|AFRINIC|[afrinic.net](https://www.afrinic.net/)|

---

###  Herramientas WHOIS

#### CLI (Línea de comandos)

- **whois** (paquete estándar en Linux):
    
    ```bash
    whois ejemplo.com
    whois 192.168.1.1
    ```
    
- **dig** y **nslookup** también ofrecen datos parciales sobre DNS.
    

#### Webs y servicios gráficos

- [https://whois.domaintools.com](https://whois.domaintools.com/)
    
- [https://centralops.net/co/](https://centralops.net/co/)
    
- [https://who.is](https://who.is/)
    
- [https://dnslytics.com](https://dnslytics.com/)
    

---

### ️ Consideraciones de privacidad y seguridad

1. **Protección WHOIS (Privacy/Proxy Services)**:
    
    - Muchos registradores permiten ocultar datos personales.
        
    - En su lugar, se muestra un servicio intermediario.
        
2. **RGPD y WHOIS**:
    
    - Desde la aplicación del RGPD en Europa, muchos datos personales se ocultan en dominios registrados por personas físicas.
        
3. **Limitaciones y bloqueos**:
    
    - El acceso masivo a WHOIS puede estar limitado por captchas, cuotas, o bloqueos automáticos.
        

---

###  Uso ofensivo y defensivo en ciberseguridad

#### Uso ofensivo (atacante):

- Localizar puntos de contacto, posibles emails que se puedan usar para **phishing o spear phishing**.
    
- Determinar la **estructura de dominio** y servidores DNS para posibles **zone transfers**.
    
- Asociar dominios entre sí por sus propietarios.
    
- Encontrar **IPs de redes enteras** pertenecientes a una organización.
    

#### Uso defensivo (analista de ciberseguridad):

- Atribuir un dominio malicioso a una organización o país.
    
- Investigar campañas de phishing o malware por sus registros.
    
- Verificar si un dominio sospechoso está vinculado a dominios conocidos maliciosos.
    
- Comprobar la **legitimidad** de sitios externos antes de permitir el acceso o intercambio de datos.
    

---

###  Ejemplo práctico de uso en pentesting

```bash
whois banco-falso.com
```

```text
Registrar: OffshoreDomains Ltd.
Registrant Name: John Anonymous
Email: contacto@correo.ru
Creation Date: Hace 2 semanas
Name Servers: ns1.hackdns.biz, ns2.hackdns.biz
```

 _Conclusión rápida:_ dominio sospechoso recién creado, con nombres de servidores poco confiables → posible phishing.

---

### Conclusión

La base de datos WHOIS es una herramienta poderosa para **reconocer, rastrear y atribuir** tanto activos legítimos como maliciosos. Aunque su alcance ha sido limitado por cuestiones legales y de privacidad, **sigue siendo esencial en auditorías, análisis de amenazas y ciberinteligencia**.

---

¿Quieres que te prepare un script en Python para automatizar consultas WHOIS y correlacionarlas con reputación de dominios o feeds de amenazas?