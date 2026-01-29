---
title: "Dnsenum"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  DNSEnum (Dum)

> **Relacionado**: Ver [[TheHarvester]] para OSINT general. [[Nslookup-y-dig]] para consultas manuales. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|Nmap]] para escaneo de puertos. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/DNS|Protocolo DNS]].

- **Nombre completo:** **DNSEnum**
    
- **Símbolo:** **Dum**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de enumeración de DNS
    
- **Repositorio oficial:** [https://github.com/fwaeytens/dnsenum](https://github.com/fwaeytens/dnsenum)
    

---

##  ¿Qué es DNSEnum?

**DNSEnum** es una herramienta de código abierto escrita en Perl cuyo propósito es **recolectar toda la información DNS disponible sobre un dominio objetivo**. Esta técnica, llamada **enumeración DNS**, es clave en la fase de reconocimiento de un test de penetración, ya que permite descubrir servidores, subdominios, registros públicos y configuraciones mal hechas.

Su enfoque es **automatizar múltiples técnicas de recolección DNS** en una sola herramienta, ahorrando tiempo y mejorando la profundidad del análisis.

---

## ️ Funcionalidades principales de DNSEnum

DNSEnum realiza una amplia gama de tareas de reconocimiento DNS, entre las que destacan:

1.  **Resolución directa e inversa** (A y PTR records).
    
2.  **Enumeración de subdominios** mediante diccionario.
    
3.  **Transferencias de zona DNS (AXFR)** si el servidor está mal configurado.
    
4.  **Consulta de registros DNS**:
    
    - A (IPv4)
        
    - AAAA (IPv6)
        
    - MX (correo)
        
    - NS (servidores de nombre)
        
    - TXT (incluyendo SPF/DKIM)
        
    - SOA (Start of Authority)
        
    - CNAME (alias)
        
5.  **Búsqueda WHOIS** para obtener datos del registrante.
    
6.  **Brute force de subdominios** (opcional).
    
7.  **Escaneo recursivo** (buscar subdominios dentro de subdominios).
    

---

##  Casos de uso en pentesting

- Identificar **subdominios ocultos** que podrían estar expuestos a Internet.
    
- Detectar **malas configuraciones DNS**, como servidores que permiten **transferencias de zona**.
    
- Obtener información sobre **infraestructura de correo** (por ejemplo, MX sin protección).
    
- Descubrir posibles vectores de ataque: staging sites, paneles de administración, entornos de desarrollo (ej: `dev.empresa.com`, `test.api.empresa.com`).
    
- **Ampliar la superficie de ataque** antes de la fase de explotación.
    

---

##  Ejemplo de uso básico

```bash
dnsenum ejemplo.com
```

Esto lanzará la enumeración básica sobre el dominio `ejemplo.com`.

###  Con opciones personalizadas:

```bash
dnsenum --enum -f diccionario.txt -r -n 8.8.8.8 ejemplo.com
```

- `--enum`: realiza una enumeración completa (brute force, WHOIS, etc.)
    
- `-f diccionario.txt`: usa un archivo de diccionario para buscar subdominios.
    
- `-r`: realiza resolución inversa de IPs.
    
- `-n`: especifica el servidor DNS a utilizar (en este caso, Google).
    

---

##  ¿Qué puede revelar DNSEnum?

|Tipo de dato|Riesgo asociado|
|---|---|
|Subdominios|Superficie de ataque no protegida|
|Transferencias AXFR|Filtración total del esquema DNS interno|
|Registros TXT|Configuración débil de SPF/DKIM|
|IPs públicas|Servidores expuestos directamente|
|WHOIS|Correos, teléfonos, nombres de contacto|

---

##  Seguridad y defensa

Desde el punto de vista del **Blue Team**, DNSEnum pone en evidencia por qué es importante:

- **Restringir transferencias de zona** DNS solo a IPs autorizadas.
    
- No exponer subdominios sensibles.
    
- Configurar correctamente los registros **TXT** para evitar suplantaciones.
    
- Minimizar la información expuesta en **registros WHOIS** (uso de privacidad).
    

---

##  Herramientas alternativas o complementarias

|Herramienta|Características|
|---|---|
|**Fierce**|Enumeración DNS con enfoque en redes internas|
|**dnsrecon**|Similar a DNSEnum, pero en Python|
|**Amass**|OSINT avanzado + subdomain enumeration|
|**Sublist3r**|Enumeración rápida de subdominios por OSINT|
|**Dig**|Herramienta manual para consultas específicas|

---

##  Integración con otros pasos

DNSEnum puede usarse como **paso previo a Nmap o a ataques de ingeniería social**, ya que ayuda a descubrir activos o correos. También puede alimentar herramientas de escaneo como **Nuclei**, si se descubren nuevos endpoints.

---

¿Te gustaría que prepare una **plantilla de automatización** que combine `dnsenum`, `nmap` y `ffuf` para reconocimiento inicial de un dominio? ¿O quieres que analice un dominio específico con DNSEnum y te muestre cómo interpretar los resultados?