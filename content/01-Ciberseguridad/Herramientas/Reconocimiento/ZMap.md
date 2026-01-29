---
title: "Zmap"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---
###  ZMap (ZM)


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Censys|Censys]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/Naabu|Naabu]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

- **Nombre completo:** **ZMap**
    
- **Símbolo en la tabla:** **ZM**
    
- **Categoría:**  **Reconnaissance**
    
- **Tipo:** Herramienta de escaneo masivo de red a nivel de internet
    
- **Desarrollador:** University of Michigan (Censys.io)
    
- **Repositorio oficial:** [https://github.com/zmap/zmap](https://github.com/zmap/zmap)
    
- **Sitio oficial:** [https://zmap.io](https://zmap.io/)
    

---

##  ¿Qué es ZMap?

**ZMap** es una herramienta de código abierto diseñada para realizar **escaneos de red a gran escala**, extremadamente rápido, eficiente y optimizado para analizar grandes porciones del espacio IPv4 público. Puede escanear **todo Internet (4 mil millones de IPs)** en menos de una hora desde un único equipo bien configurado.

Su principal ventaja es la **velocidad sin comprometer fiabilidad**, ideal para investigaciones a escala global, detección de servicios abiertos, exposición de puertos vulnerables o recolección masiva de inteligencia sobre la superficie de ataque en Internet.

---

## ️ Características principales

-  **Velocidad extrema**: hasta 14 millones de paquetes por segundo.
    
-  **Escaneo de puertos específico**: escanea un solo puerto por ejecución (ideal para análisis tipo censo).
    
-  **Salida limpia y configurable**: permite exportar en JSON, CSV, listas simples, etc.
    
-  **Soporte para IPv4** (no soporta IPv6 por diseño).
    
-  Compatible con módulos extendidos: escaneo de banners, certificados, DNS, etc.
    
-  Integración con **ZGrab** para inspección profunda de servicios (TLS, HTTP, SSH...).
    

---

##  ¿Para qué sirve ZMap?

|Aplicación|Ejemplo de uso|
|---|---|
| Recolección de inteligencia|Identificar servidores web abiertos en el mundo.|
| Investigación académica|Estudios sobre el uso de servicios inseguros (telnet).|
| Ciberdefensa global|Análisis de exposición pública de sistemas.|
| Vigilancia de vulnerabilidades|Detectar hosts expuestos tras CVEs críticas.|
| Estadísticas globales|Ej. ¿cuántos servidores con TLS 1.0 siguen activos?|

---

##  Ejemplo básico

### Escanear el puerto 80 en toda una red

```bash
sudo zmap -p 80 192.168.1.0/24 -o resultados.txt
```

Este comando enviará paquetes SYN a todos los hosts del rango `/24` para ver cuáles tienen el puerto 80 abierto.

---

### Escaneo de todo Internet (️ requiere justificación legal y técnica)

```bash
sudo zmap -p 443 0.0.0.0/0 -o https_hosts.csv
```

Esto escaneará todo el espacio IPv4 buscando hosts con HTTPS activo.

️ **IMPORTANTE:** Esto **puede considerarse actividad maliciosa** si no se hace con consentimiento explícito y propósito académico, de investigación o bajo un programa de divulgación autorizado. ZMap no es para uso ofensivo sin permiso.

---

##  Instalación en Linux

### Ubuntu/Debian

```bash
sudo apt install zmap
```

### Fedora

```bash
sudo dnf install zmap
```

### Desde código fuente (recomendado para última versión):

```bash
git clone https://github.com/zmap/zmap.git
cd zmap
cmake .
make
sudo make install
```

---

##  Integración con ZGrab

ZMap se puede usar junto con **ZGrab**, una herramienta de **recolección de banner e información de protocolos**. Ejemplo:

```bash
zmap -p 443 -o - | ztee open443.txt | zgrab --port 443 --tls --output=zgrab_tls.json
```

Esto escanea hosts con HTTPS y luego analiza el certificado TLS de cada uno.

---

##  Consideraciones de defensa (Blue Team)

Desde la perspectiva defensiva:

- Un escaneo de ZMap puede delatarse por su **frecuencia de paquetes muy alta**.
    
- IDS/IPS deben estar configurados para detectar **escaneos SYN masivos**.
    
- Se puede usar ZMap en entornos internos para detectar dispositivos no autorizados o servicios abiertos sin conocimiento del administrador.
    

---

##  Comparativa con otras herramientas

|Herramienta|Velocidad|Alcance|Precisión|Ideal para|
|---|---|---|---|---|
|Nmap|Media|Local/global|Alta|Análisis detallado|
|Masscan|Muy alta|Masivo|Alta|Escaneo rápido global|
|ZMap|Extremadamente alta|Global IPv4|Alta (solo un puerto a la vez)|Recolección masiva de datos|
|Naabu|Alta|Dominios/IPs|Media|Recon semi-pasivo web|

---

##  Conclusión

**ZMap** es una herramienta de escaneo extremadamente potente y rápida, diseñada para quienes necesitan analizar grandes volúmenes de direcciones IP. Es una herramienta indispensable para **analistas de ciberseguridad a gran escala, investigadores, Blue Teams nacionales, universidades, CERTs y CSIRTs**.

---

### ️ Advertencia Legal

ZMap debe utilizarse **solo en redes bajo tu control** o con permiso expreso. Escanear Internet sin justificación y autorización **puede constituir delito** en muchas jurisdicciones.

---

¿Quieres que prepare un ejemplo de escaneo masivo con filtrado por ASN o país? ¿O prefieres una guía completa de ZMap + ZGrab para levantar un informe de exposición TLS en una organización?