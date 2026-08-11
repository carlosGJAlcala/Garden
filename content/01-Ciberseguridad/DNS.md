### DNS (Domain Name System) – Nota expandida

El **DNS** es uno de los pilares de Internet. Es el sistema que permite traducir **nombres de dominio legibles para humanos** (como `www.google.com`) en **direcciones IP** que las máquinas entienden (`142.250.184.100`). Funciona como la "guía telefónica" de Internet.

Sin DNS, necesitaríamos recordar direcciones IP para acceder a cualquier sitio web, lo que sería impráctico y propenso a errores.

---

### 📚 Arquitectura del sistema DNS

DNS tiene una **estructura jerárquica y distribuida**, diseñada para ser escalable:

#### Niveles:

1. **Root (raíz)**: Es el punto más alto. Hay 13 servidores raíz globales (`A` a `M`), pero distribuidos por miles de nodos mediante Anycast.
    
2. **TLD (Top-Level Domains)**: `.com`, `.org`, `.net`, `.es`, etc.
    
3. **Dominios secundarios**: `google.com`, `uc3m.es`, etc.
    
4. **Subdominios**: `www.google.com`, `mail.uc3m.es`, etc.
    

#### Tipos de servidores DNS:

- **Servidores raíz**
    
- **Servidores TLD**
    
- **Servidores autoritativos**: Tienen la información definitiva de un dominio.
    
- **Resolvers**: Son los que contactan con los demás en nombre del cliente. Los ofrecen los ISPs, empresas o servicios como Google DNS (8.8.8.8).
    

---

### 🔄 ¿Cómo se resuelve un dominio?

Cuando escribes `www.uc3m.es` en tu navegador, ocurre:

1. Tu equipo pregunta al **resolver local** (del ISP, por ejemplo).
    
2. Si no está en caché, el resolver contacta con un **servidor raíz**.
    
3. Este responde con la dirección del servidor del TLD `.es`.
    
4. Luego el resolver pregunta al servidor del TLD `.es`, que responde con el autoritativo de `uc3m.es`.
    
5. Finalmente, se resuelve `www.uc3m.es` con la IP correspondiente.
    

---

### 🗂️ Tipos de registros DNS comunes

|Tipo de registro|Descripción|
|---|---|
|**A**|Traduce nombre a dirección IPv4|
|**AAAA**|Traduce nombre a IPv6|
|**CNAME**|Alias de otro dominio|
|**MX**|Servidores de correo electrónico|
|**NS**|Servidores autoritativos|
|**TXT**|Información arbitraria (SPF, DKIM, etc.)|
|**PTR**|Resolución inversa (IP → nombre)|

---

#### 1. **DNS Spoofing / Cache Poisoning**

- El atacante **inyecta información falsa** en la caché del resolver.
    
- La víctima es redirigida a un sitio malicioso (sin saberlo).
    
- Ejemplo: `www.banco.com` apunta a una IP controlada por el atacante.
    

#### 2. **Intercepción o manipulación de respuestas**

- Si el tráfico DNS no está cifrado (UDP/53), un atacante en la misma red puede leerlo o modificarlo (ej. Wi-Fi pública).
    

#### 3. **Ataques de amplificación DDoS**

- DNS puede ser usado para amplificar ataques: un pequeño paquete malicioso genera una gran respuesta hacia la víctima (si el servidor permite recursion sin restricciones).
    

#### 4. **Dependencia excesiva del DNS**

- Muchas aplicaciones confían en que el nombre resuelto sea correcto para aplicar controles de seguridad. Si el DNS se manipula, se rompe esta suposición.
    

---

#### 1. **DNSSEC (Domain Name System Security Extensions)**

- Proporciona **integridad y autenticación** mediante firmas digitales.
    
- Introduce nuevos registros como:
    
    - `RRSIG`: firma digital del conjunto de registros.
        
    - `DNSKEY`: clave pública de la zona.
        
    - `DS`: hash de la clave en la zona superior.
        
    - `NSEC/NSEC3`: pruebas de inexistencia.
        
- No cifra, pero garantiza que la respuesta proviene de quien dice ser y no fue manipulada.
    

#### 2. **DANE (DNS-based Authentication of Named Entities)**

- Usa DNSSEC para almacenar certificados TLS (como alternativa a las CAs públicas).
    

#### 3. **Cifrado del tráfico DNS**

- **DoT (DNS over TLS)**: Cifra las consultas DNS entre cliente y resolver.
    
- **DoH (DNS over HTTPS)**: Usa HTTPS para consultas DNS, ocultando el tráfico DNS como tráfico web normal.
    
- Grandes resolvers como Google, Cloudflare (1.1.1.1) y Quad9 ofrecen estos servicios.
    

#### 4. **Políticas de TTL cortas y validación activa**

- Evitar que datos en caché duren demasiado y validar constantemente las rutas DNS.
    

---

### 🧪 Ejemplo de ataque: Envenenamiento de caché

```plaintext
1. Resolver realiza consulta por www.banco.com.
2. Atacante envía múltiples respuestas con IP falsa y QID aleatorio.
3. Si acierta con el QID antes que el verdadero, la respuesta se guarda en caché.
4. Todos los usuarios del resolver irán al sitio fraudulento hasta que expire el TTL.
```

---

### 🛡️ Otras medidas defensivas

- **HSTS (HTTP Strict Transport Security)**: asegura que el navegador solo use HTTPS tras la primera visita.
    
- **Certificate Pinning**: vincula un dominio a una clave pública específica.
    
- **Redundancia en resolvers**: usar múltiples servidores DNS y verificar consistencia.
    

---

### Conclusión

El DNS es fundamental pero fue diseñado sin seguridad en mente. Hoy en día, existen múltiples ataques que lo aprovechan para redirigir, interceptar o manipular tráfico. La adopción de **DNSSEC**, **DoH/DoT**, y herramientas de validación, junto con la vigilancia proactiva, son esenciales para mantener una infraestructura de Internet segura y confiable.

---

¿Quieres que te muestre cómo configurar DNSSEC para un dominio o cómo interceptar tráfico DNS con Wireshark para prácticas de auditoría?
