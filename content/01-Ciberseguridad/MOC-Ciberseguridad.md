---
title: "MOC - Ciberseguridad"
date: 2026-01-26
tags:
  - ciberseguridad
---
# MOC - Ciberseguridad


> **Relacionado**: [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

> Mapa de contenido del área de ciberseguridad. Incluye notas del Máster y recursos adicionales.

[[00-Inicio/HOME|← Volver al inicio]]

---

## Fundamentos
Conceptos base de seguridad informática.

- [[Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos básicos de seguridad]]
- [[Fundamentos/Ciclo-de-Vida-del-Desarrollo-del-Software-SDLC|SDLC]]
- [[Fundamentos/owasp|OWASP]]

### Vulnerabilidades Web
- [[Fundamentos/SSRF|SSRF]]
- [[Fundamentos/XXE|XXE]]
- [[Fundamentos/SQLMap|SQL Injection]]
- [[Fundamentos/Request-Smuggling|HTTP Request Smuggling]]
- [[Fundamentos/OptionsBleed|OptionsBleed]]

### Ataques de Red
- [[Fundamentos/ARP-SPOOFING|ARP Spoofing]]
- [[Fundamentos/SSLTRIP|SSL Strip]]
- [[Fundamentos/Ataque-Rudy|Ataque Rudy (DoS)]]

---

## Herramientas de Hacking
Herramientas esenciales para pentesting y auditoría.

### Reconocimiento
- [[Herramientas/Nikto|Nikto]]
- [[Herramientas/owasp-zap|OWASP ZAP]]
- [[Herramientas/WPScan|WPScan]]
- [[Herramientas/Reconocimiento-de-directorios-y-archivo|Fuzzing de directorios]]

### Explotación
- [[Herramientas/Burp-suite|Burp Suite]]
- [[Herramientas/Hydra|Hydra]]
- [[Herramientas/Netcat|Netcat]]
- [[Herramientas/Cobalt-Strike|Cobalt Strike]]

### IDS/IPS
- [[Herramientas/IDS-IPS/SNORT|Snort]]
- [[Herramientas/IDS-IPS/suricata|Suricata]]
- [[Herramientas/IDS-IPS/ZEEK|Zeek]]

### SIEM
- [[Herramientas/SIEM/SPLUNK|Splunk]]

---

## Criptografía
Fundamentos y aplicaciones de criptografía.

- [[Criptografia/AES256|AES-256]]
- [[Criptografia/OpenSSL|OpenSSL]]
- [[Criptografia/Dropbear-SSH|Dropbear SSH]]
- [[Criptografia/Encriptacion-homomorfica|Cifrado homomórfico]]
- [[Criptografia/SWEET32|SWEET32]]
- [[Criptografia/2025-04-20-Computacion-Cuantica-y-Criptografia-Post-Cuantica|Criptografía post-cuántica]]

---

## Análisis de Malware
Técnicas de análisis estático y dinámico.

- [[Malware/2025-01-13-ANALISIS-DE-MALWARE|Introducción al análisis]]
- [[Malware/2025-02-17-Binwalk-dd-strings-y-analisis-de-binarios|Binwalk y strings]]
- [[Malware/2025-02-24-Formatos-ejecutables-PE-y-ELF|Formatos PE y ELF]]
- [[Malware/2025-03-10-APIs-Windows-y-DLL-Hijacking|DLL Hijacking]]
- [[Malware/2025-03-17-Anti-Debugging-y-PAFish|Anti-Debugging]]
- [[Malware/Gusano-de-Morris|Gusano de Morris]]
- [[Malware/njRAT|Análisis de njRAT]]

---

## Ingeniería Inversa
Reversing de binarios y exploits.

- [[Ingenieria-Inversa/2025-01-14-Tipos-de-analisis-en-binarios-PE|Análisis de PE]]
- [[Ingenieria-Inversa/2025-03-11-Radare2|Radare2]]
- [[Ingenieria-Inversa/2025-03-18-Parcheo-de-binario|Parcheo de binarios]]
- [[Ingenieria-Inversa/2025-03-25-exploit|Desarrollo de exploits]]
- [[Ingenieria-Inversa/Ghidra|Ghidra]]
- [[Ingenieria-Inversa/x64dbg|x64dbg]]

---

## Forense Digital
Análisis forense y respuesta a incidentes.

- [[Forense/guia/Conceptos-base|Conceptos base forense]]
- [[Forense/guia/Acceso-y-analisis-de-memoria-en-Linux-y-Windows|Análisis de memoria]]
- [[Fundamentos/Autopsy|Autopsy]]
- [[Fundamentos/LABORATORIO-2-volatility|Volatility]]

---

## Gestión de Seguridad
SGSI, normativas y gestión de riesgos.

- [[Gestion-Seguridad/Tema1PrincipiosBasicosSI/GRC|GRC]]
- [[Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/ENS|ENS]]
- [[Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/RGPD|RGPD]]
- [[Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/NIS2|NIS2]]
- [[Gestion-Seguridad/Tema4Auditoria/COBIT|COBIT]]

---

## Comunicaciones Seguras
Protocolos y seguridad en comunicaciones.

- [[Comunicaciones-Seguras/Protocolos-de-comunicaciones-seguras|Protocolos seguros]]
- [[Comunicaciones-Seguras/2024-11-29-Ratchet-y-E3DH-SIGNAL|Signal Protocol]]
- [[Comunicaciones-Seguras/HOTP-Y-TOTP|TOTP/HOTP]]
- [[Comunicaciones-Seguras/Heartbleed-bug|Heartbleed]]
- [[Comunicaciones-Seguras/2024-12-19-REDES-WIFI|Seguridad WiFi]]

---

## Desarrollo Seguro
SSDLC y programación segura.

- [[Desarrollo-Seguro/2025-01-23-DISENO-DE-APLICACIONES-modelado-de-amenazas|Modelado de amenazas]]
- [[Desarrollo-Seguro/2025-01-30-Arbol-de-ataque|Árboles de ataque]]
- [[Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|TPM y UEFI]]
- [[Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH2.0|OAuth 2.0]]

---

## Prácticas
Ejercicios y laboratorios.

- [[Practicas/Hacking-WordPress|Hacking WordPress]]
- [[Comunicaciones-Seguras/WIFICHALLENGE/|WiFi Challenge]]
