---
title: "Redes Privadas Virtuales Vpn"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - protocolos-de-internet
---
### Redes Privadas Virtuales (VPN) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]]. [[01-Ciberseguridad/Comunicaciones-Seguras/2024-12-19-REDES-WIFI|2024 12 19 REDES WIFI]].

Una **VPN (Virtual Private Network)** permite crear un **canal cifrado y seguro** entre dos puntos a través de una red insegura como Internet. Se utiliza para **proteger la confidencialidad, integridad y autenticidad** de las comunicaciones, como si los equipos conectados estuvieran en la misma red local, aunque estén físicamente dispersos.

---

###  Objetivos principales de una VPN

1. **Confidencialidad**: El tráfico viaja cifrado y no puede ser leído por terceros.
    
2. **Autenticación**: Las partes deben comprobar que son quienes dicen ser.
    
3. **Integridad**: Se evita que los datos sean modificados en tránsito.
    
4. **Privacidad**: Se oculta la dirección IP y la localización del usuario final.
    
5. **Acceso remoto**: Permite a empleados conectarse de forma segura desde casa o el extranjero.
    

---

###  Componentes básicos de una VPN

- **Cliente VPN**: el software o dispositivo que inicia la conexión.
    
- **Servidor VPN**: el punto de entrada que gestiona la conexión y canaliza el tráfico.
    
- **Túnel VPN**: canal virtual cifrado por donde pasan los datos.
    
- **Protocolos de túnel y cifrado**: los encargados de proteger la comunicación.
    

---

###  Tipos de uso de VPNs

1. **Acceso remoto (Remote Access VPN)**  
    Usuarios se conectan desde fuera de la red corporativa, por ejemplo, trabajadores en casa.
    
2. **VPN site-to-site (punto a punto)**  
    Conecta dos oficinas distantes como si estuvieran en la misma red LAN.
    
3. **VPN interna (intra-LAN)**  
    Se usa dentro de una misma red para aislar departamentos o segmentos sensibles.
    

---

###  Protocolos comunes usados en VPNs

|Protocolo|Capa|Características principales|
|---|---|---|
|**PPTP** (obsoleto)|Capa 2|Fácil de configurar, pero inseguro. Hoy se desaconseja.|
|**L2TP/IPsec**|Capa 2 + 3|Combina L2TP para túnel y IPsec para cifrado. Robusto, pero más lento.|
|**IPsec**|Capa 3|Alta seguridad. Cifra directamente los paquetes IP.|
|**OpenVPN**|Capa 4/7|Basado en TLS. Muy seguro, flexible, y ampliamente adoptado.|
|**WireGuard**|Capa 3|Moderna, rápida y más eficiente que IPsec y OpenVPN. Código muy ligero.|

---

### ️ Modos de operación de IPsec (usado en VPNs)

1. **Modo transporte**:
    
    - Solo se cifra la carga útil del paquete IP.
        
    - Útil para comunicaciones entre hosts específicos.
        
    - La cabecera IP original se mantiene (visible a routers).
        
2. **Modo túnel**:
    
    - Se cifra todo el paquete IP original (cabecera + datos).
        
    - Se añade una **nueva cabecera IP** para el encaminamiento.
        
    - Ideal para VPN site-to-site o acceso remoto.
        

---

### ️ Vulnerabilidades y riesgos en VPNs

1. **Falsificación de servidor**:
    
    - Un atacante puede simular ser el servidor VPN si no hay autenticación mutua sólida.
        
2. **Filtración de DNS o tráfico fuera del túnel**:
    
    - Algunos sistemas operativos pueden enviar consultas DNS fuera del túnel (DNS leak).
        
3. **Conexiones sin cifrar**:
    
    - Algunos proveedores o configuraciones erróneas pueden usar algoritmos débiles o no cifrar correctamente.
        
4. **Dependencia de CA públicas** (en VPNs basadas en TLS):
    
    - Si una CA confiable es comprometida, se podrían emitir certificados falsos.
        
5. **Privacidad limitada por el proveedor**:
    
    - Algunas VPNs registran y venden datos del usuario.
        

---

###  Buenas prácticas y mecanismos de seguridad

- Usar **certificados digitales** para autenticación.
    
- Configurar **cifrado fuerte** (AES-256, TLS 1.3, etc.).
    
- Habilitar **firewall y reglas estrictas** en el servidor VPN.
    
- Evitar PPTP. Usar preferentemente **WireGuard**, **OpenVPN** o **IPsec/IKEv2**.
    
- Utilizar **kill switch** en clientes: bloquea todo el tráfico si se cae la conexión VPN.
    
- Verificar que no haya **leaks de IP/DNS/WebRTC**.
    

---

### ️ Aplicaciones típicas de una VPN

- **Empresarial**: conectar teletrabajadores a redes internas.
    
- **Protección personal**: navegar de forma segura en redes Wi-Fi públicas.
    
- **Evasión de censura**: acceder a servicios bloqueados en ciertos países.
    
- **Protección contra rastreo**: ocultar IP y ubicación ante anunciantes o atacantes.
    

---

###  Comparación entre protocolos VPN modernos

|Protocolo|Seguridad|Rendimiento|Facilidad de configuración|Estado|
|---|---|---|---|---|
|OpenVPN|Alta|Media|Media|Muy usado|
|IPsec/IKEv2|Alta|Alta|Alta (con herramientas)|Estándar|
|WireGuard|Muy alta|Muy alta|Muy fácil|En crecimiento|

---

### Conclusión

Las VPNs son fundamentales para asegurar comunicaciones privadas y confiables en entornos tanto corporativos como personales. Aunque son potentes, su eficacia depende de **una buena configuración, elección del protocolo adecuado, y conciencia de sus límites**. Con el auge del teletrabajo y la movilidad, su uso se ha convertido en una **pieza esencial de la ciberseguridad moderna**.

---

¿Quieres que te prepare un ejemplo de configuración de VPN con WireGuard o OpenVPN en Linux o Windows?