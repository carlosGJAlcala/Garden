---
title: "Seguridad dispositivo de red"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---


# Seguridad dispositivo de red


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

Si encuentras una vulnerabilidad, lo haces a través de intermediarios con varios dispositivos. Una botnet puede hacer ataques de contraseña.
	
- Watchtower
- Router + VPN
- 1 user + password stealer
- 2 RCE / auth bypass


---

## FortiManager y vulnerabilidad FortiJump (CVE-2024-47575)

**FortiManager** es una plataforma de administración centralizada que permite gestionar, configurar y actualizar múltiples dispositivos Fortinet, como firewalls, routers y dispositivos VPN. Es una solución ampliamente utilizada en entornos empresariales y de operadores para garantizar consistencia y eficiencia en la gestión de la infraestructura de seguridad.

---

### FortiJump (CVE-2024-47575): Vulnerabilidad crítica

Recientemente se ha descubierto la vulnerabilidad **CVE-2024-47575**, apodada **FortiJump**, que afecta al servicio **FGFM** (FortiGate-FortiManager Protocol). Esta vulnerabilidad permite que un atacante remoto y no autenticado pueda ejecutar código arbitrario o comandos maliciosos en dispositivos afectados, obteniendo control completo sobre ellos.

La raíz del problema reside en que, aunque FGFM usa **TLS con autenticación mutua**, la confianza total en los certificados Fortinet fue un supuesto equivocado. Los atacantes lograron obtener dispositivos que contenían certificados válidos y, tras realizar ingeniería inversa sobre el protocolo, pudieron explotar la funcionalidad de ejecución remota de comandos disponible en FGFM.

---

### Características técnicas del entorno Fortinet

- **Routers y dispositivos VPN de Fortinet** están basados en sistemas operativos derivados de Linux, pero modificados y adaptados específicamente para los fines de filtrado, gestión de tráfico y provisión de servicios VPN.
    
- Estos dispositivos permiten acceso remoto y funcionalidades avanzadas que, si no están correctamente protegidas y actualizadas, pueden convertirse en vectores críticos de ataque.
    

---

### Entornos operativos relacionados

El **NOC (Centro de Operaciones de Red)** es el área encargada de monitorizar, gestionar y mantener la infraestructura de red, incluyendo dispositivos como los administrados por FortiManager.

Fortinet **no es la única empresa que ha sufrido ataques de este tipo**:

- Las vulnerabilidades en dispositivos de red y seguridad perimetral se han convertido en objetivos prioritarios para atacantes avanzados.
    
- Investigadores como **Orange Tsai** han documentado múltiples vulnerabilidades en este tipo de equipos, contribuyendo significativamente al conocimiento y divulgación de fallos críticos.
    

---

### Prioridades de las empresas ante vulnerabilidades

Aunque estos ataques también pueden implicar espionaje y robo de información confidencial, en la práctica, **las empresas suelen priorizar la mitigación de riesgos relacionados con ransomware**, ya que:

- El ransomware genera impacto económico inmediato y directo.
    
- La indisponibilidad de sistemas y la pérdida de datos puede tener consecuencias devastadoras a corto plazo.
    
- La reputación de la empresa y su relación con clientes y partners puede verse gravemente afectada.
    


---

## FortiJump: análisis de vulnerabilidad y contexto

**FGFM** (FortiGate-FortiManager Protocol) es el demonio responsable de gestionar la comunicación entre **FortiGate** y **FortiManager**, utilizando un protocolo propietario no documentado públicamente, lo que representa un caso clásico de **"seguridad por oscuridad"**.

El diseño original asumía que la opacidad del protocolo y el uso de certificados propietarios Fortinet serían suficientes para proteger la comunicación, pero esto no resultó así.

---

### Características del protocolo FGFM

- **Protocolo propietario basado en texto**: aunque propietario, su estructura en texto permitió que herramientas como **Wireshark** lo analizaran con relativa facilidad, una vez identificado el formato.
    
- **Seguridad a través de TLS**: para proteger la confidencialidad y la autenticación de las comunicaciones, FGFM se basa en **TLS con autenticación mutua (mTLS)**.
    
    - La sesión solo se establece si **ambas partes presentan certificados válidos emitidos por Fortinet**.
        
    - En principio, se asumía que ningún atacante podría disponer de un certificado válido.
        
- **Funcionalidad de tunelización**: el protocolo **permite tunelizar servicios**, de forma similar a lo que permite un túnel SSH.
    
    - Uno de estos servicios críticos es un **RSH (Remote Shell)** que acepta como parámetro la ruta de un archivo y lo ejecuta directamente con privilegios **root**.
        

---

### Vector de ataque

El ataque denominado **FortiJump (CVE-2024-47575)** surgió tras un trabajo de ingeniería inversa:

- El atacante **obtuvo acceso a dispositivos Fortinet que contenían certificados válidos de FortiManager**, rompiendo el supuesto de que estos certificados no podían ser obtenidos.
    
- Una vez en posesión de estos certificados, el atacante pudo autenticarse legítimamente ante el protocolo FGFM.
    
- Gracias al conocimiento detallado del protocolo, obtenido mediante ingeniería inversa (por ejemplo, utilizando herramientas como **Ghidra**), el atacante logró ejecutar comandos arbitrarios como **root**, explotando la funcionalidad RSH del protocolo.
    
- Se reveló que el protocolo carecía de validaciones adicionales que limitaran la ejecución de comandos incluso después de la autenticación mutua.
    

---

### Respuesta y mitigación

- Fortinet publicó un **parche que introducía un mecanismo adicional de autorización denominado “human task”**:
    
    - Aunque autenticado, el atacante tendría que ser autorizado manualmente por un operador antes de ejecutar comandos.
        
    - Sin embargo, este mecanismo podría ser susceptible a ingeniería social: **si el atacante conseguía convencer al operador legítimo, podría volver a ejecutar sus acciones**.
        
- **El parche no resolvía completamente la vulnerabilidad en FortiJump**, porque no abordaba el problema de fondo: la confianza implícita total otorgada tras la autenticación mutua.
    

---

### Implicaciones de la vulnerabilidad

Esta vulnerabilidad tiene implicaciones críticas:

- **Acceso root a dispositivos FortiGate y FortiManager**:  
    Los atacantes pueden obtener control total del dispositivo comprometido.
    
- **Robo de información sensible**:  
    Pueden exfiltrar datos de configuración, credenciales y políticas de seguridad de la organización.
    
- **Persistencia y backdoors**:  
    Pueden instalar puertas traseras que permitan accesos futuros y discretos a las redes protegidas.
    

---

### Lecciones y medidas recomendadas

 **Principio clave: defensa en profundidad**  
La vulnerabilidad demostró que **no basta con confiar en autenticaciones criptográficas si después no existen controles adicionales sobre las acciones permitidas**.

Medidas recomendadas:

- **Revisión del diseño del protocolo**: introducir controles a nivel funcional y validar exhaustivamente las operaciones incluso después de la autenticación.
    
- **Seguridad basada en contexto y autorización adicional para operaciones críticas**.
    
- **Auditoría constante de dispositivos y certificados utilizados en producción**.
    
- **Monitoreo activo de logs y comportamiento anómalo en dispositivos de red y seguridad**.
    

---

Si quieres puedo incluir:

- **Una cronología detallada de FortiJump**
    
- **Resumen técnico de la vulnerabilidad CVE-2024-47575**
    
- **Buenas prácticas específicas para proteger dispositivos Fortinet frente a este tipo de fallos**
    

Solo dime. 
