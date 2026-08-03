---
title: "Diseno Y Desarrollo De Sistema"
date: 2025-03-06
tags:
  - ciberseguridad
---

### CNN-CERT e INCIBE


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/LDAP|LDAP]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/suricata|suricata]].

CNN-CERT gestiona incidentes de ciberseguridad y responde a amenazas en el ámbito nacional. S2 Grupo, por su parte, colabora con Pilar en diversas iniciativas de ciberseguridad.  
INCIBE es similar a CNN-CERT, pero enfocado en el sector privado, ofreciendo servicios y asesoramiento a empresas.

### Anuncio de BlackBasta y respuesta a incidentes

La campaña **Stop Ransomware** ha identificado numerosos incidentes relacionados con grupos como **BlackBasta**.  
CISA (Cybersecurity & Infrastructure Security Agency) publica regularmente información sobre Indicadores de Compromiso (IOCs) en formato JSON, lo que facilita su integración en herramientas de seguridad.

El enfoque actual en seguridad está orientado a facilitar auditorías, gestionar respuestas a incidentes y analizar alertas como **BlackBasta**. Un aspecto clave en las auditorías es demostrar qué medidas de mitigación y respuesta han sido implementadas.

Un ejemplo de mala práctica en auditorías es limitarse a bloquear dominios sin realizar una evaluación real del impacto o la efectividad de estas acciones.

### Subdominios y listas de bloqueo

Los dominios deben analizarse en su formato **FQDN (Fully Qualified Domain Name)** para su correcta identificación y bloqueo. Se implementan listas de bloqueo tanto a nivel de proxy web como de C2, aunque estas medidas pueden ser ineficaces si el tráfico elude los mecanismos de filtrado.

Cuando se comparte un **Indicador de Compromiso (IOC)**, hay dos tareas clave:

1. **Descubrir:** Revisar registros históricos para determinar si ha habido una infección en el pasado.
2. **Detectar:** Monitorear en tiempo real para identificar coincidencias con indicadores activos.

### Carga de reglas y detección de tráfico

Para aplicar reglas de detección se utilizan soluciones como **EDR (Endpoint Detection & Response)** o **XEDR (Extended Endpoint Detection & Response)**. También se pueden emplear sistemas **IDS/IPS** como **Suricata**, que capturan tráfico de red para identificar anomalías y ataques.

### Limitaciones de IDS/IPS

Los **IDS/IPS** pueden ser efectivos en tráfico no cifrado, como consultas **DNS, LDAP** y otros protocolos sin cifrado. Sin embargo, con la adopción de **TLS 1.3** y el uso de **Client Hello Encryption (CLH)**, la visibilidad del tráfico se reduce drásticamente, lo que limita la utilidad de estos sistemas.

### BlackBasta y filtraciones de datos

El grupo **BlackBasta** ha sufrido un **leak** de información. Como respuesta, algunos actores han desarrollado modelos de IA personalizados para analizar los datos robados y obtener información estratégica.

### Análisis de amenazas y gestión de riesgos

Un enfoque eficaz en ciberseguridad implica **asumir que las intrusiones ocurrirán** y trabajar en reducir su impacto. Para ello, es esencial:

- **Entender a los actores de amenaza (Threat Actors).**
- **Analizar las técnicas, tácticas y procedimientos (TTPs) que emplean.**
- **Usar Indicadores de Compromiso (IOCs) para mejorar la detección y respuesta.**
- **Evaluar intrusiones pasadas y los grupos que las ejecutaron para ajustar las medidas de seguridad.**

La clave es definir **requisitos realistas y actualizados** para nuestros procesos de seguridad, con un enfoque basado en inteligencia de amenazas.

### ¿Qué papel juegan WAF y Cobalt Strike?

Los atacantes emplean herramientas avanzadas como **Cobalt Strike**, que les permite simular ataques avanzados para evadir defensas. Por otro lado, los **WAF (Web Application Firewalls)** pueden ayudar a mitigar ciertos tipos de ataques, pero deben configurarse adecuadamente según la infraestructura de la organización.

Para una defensa efectiva, es necesario correlacionar **activos, actores de amenaza y contexto organizacional**, asegurando que la seguridad esté alineada con el riesgo real de la empresa.

---



**WiFi Hopping en una Universidad**  
El **WiFi Hopping** es una técnica que permite cambiar entre diferentes redes inalámbricas de forma automatizada o manual para evitar restricciones, mantener conexión en entornos con múltiples puntos de acceso o incluso evadir controles de seguridad. Sin embargo, su uso en una universidad puede estar **restringido por normativas internas** y políticas de uso aceptable de la red.

Algunas instituciones implementan medidas para prevenir este tipo de actividad, como la autenticación basada en MAC, segmentación de VLANs o detección de conexiones anómalas. Si el propósito es legítimo, como realizar pruebas de seguridad con autorización, se recomienda coordinar con el equipo de IT de la universidad.

---

### **Principios de Diseño en Seguridad**

1. **Las intrusiones ocurren**
    
    - Se debe asumir que cualquier sistema puede ser vulnerado en algún momento.
    - El diseño debe centrarse en la resiliencia y la capacidad de respuesta.
2. **Conocer a los atacantes y sus capacidades**
    
    - Identificar qué técnicas y herramientas emplean los adversarios.
    - Estudiar su **TTPs (Tácticas, Técnicas y Procedimientos)** para anticiparse a sus movimientos.
3. **Detección orientada a la amenaza**
    
    - No se trata de detectar cualquier anomalía, sino de centrar la detección en lo que **los atacantes realmente saben hacer**.
    - Implementar modelos de detección basados en inteligencia de amenazas y comportamiento en lugar de solo firmas estáticas.


### **Modelado de Intrusiones: Kill Chain**

La **Kill Chain** es un modelo que describe las fases de una intrusión. No se trata de una secuencia rígida, sino de un marco que ayuda a identificar y detener ataques en diferentes etapas. Cada fase representa una oportunidad para bloquear o mitigar la intrusión antes de que el atacante alcance su objetivo final.

#### **Fases de la Kill Chain**

1. **Intrusión = Punto de entrada + Vulnerabilidad**
    
    - Un atacante necesita encontrar una debilidad en el sistema para iniciar el ataque.
2. **Fases previas: Reconocimiento y preparación**
    
    - **Reconocimiento:** Identificación del perímetro de la red y recopilación de información sobre el objetivo.
        - Herramientas como **Intellx.io** permiten indexar filtraciones de datos y exponer información sensible que podría ser usada en el ataque.
    - **Weaponization:** Preparación del binario o payload malicioso para la explotación.
3. **Entrega**
    
    - Cómo se distribuye la amenaza (phishing, USBs infectados, explotación de servicios expuestos, etc.).
4. **Explotación**
    
    - Uso de la vulnerabilidad para ejecutar código malicioso en el sistema.
5. **Instalación**
    
    - Establecimiento de persistencia en la máquina comprometida para asegurar el control a largo plazo.
6. **Command and Control (C2)**
    
    - Comunicación del malware con el atacante para recibir órdenes y enviar datos robados.
    - Algunos C2 usan plataformas como **Telegram**, donde bots actúan como paneles de control ocultos.
7. **Actions on Objective**
    
    - Ejecución de los objetivos del atacante: robo de información, cifrado de archivos (ransomware), movimiento lateral, etc.

### **Enfoque de Seguridad Basado en la Kill Chain**

- **No es una secuencia obligatoria:** No todos los ataques siguen cada fase, pero **siempre pasan por algunas de ellas**.
- **Cada fase es una oportunidad de defensa:** Bloquear un ataque no significa solo parchear vulnerabilidades, sino interrumpir cualquier etapa del proceso.
- **Defensa en profundidad:** Aunque el atacante use un **0-day**, su actividad puede ser detectada en otras fases (como en la instalación, C2 o exfiltración de datos).

El objetivo del modelo es organizar la seguridad en **capas**, de modo que si una barrera falla, existan otras que puedan frenar el ataque.

### **Fail2Ban y su función en la seguridad**

**Fail2Ban** es una herramienta de **rate limiting** que protege los sistemas contra ataques de fuerza bruta y otras actividades maliciosas bloqueando direcciones IP después de un número determinado de intentos fallidos. Funciona monitoreando los logs del sistema y aplicando reglas para bloquear IPs temporalmente cuando detecta un comportamiento sospechoso.

### **¿Cómo ayuda Fail2Ban?**

- **Evita ataques de descubrimiento tipo fuerza bruta**, como intentos reiterados de acceso por SSH, FTP o paneles web.
- **Reduce la superficie de ataque** limitando la cantidad de intentos que un atacante puede realizar en un periodo corto de tiempo.
- **Se basa en reglas predefinidas**, pero también permite personalizar filtros para detectar patrones específicos en los logs.

### **Limitaciones de Fail2Ban y detección de ataques válidos**

- **No detecta ataques más sofisticados**: Si un atacante distribuye sus intentos entre varias IPs (ataque distribuido), Fail2Ban puede no ser efectivo.
- **No distingue entre actividad legítima y maliciosa**: Si alguien legítimamente olvida su contraseña y realiza varios intentos fallidos, también puede ser bloqueado.
- **Se puede complementar con detección de anomalías**, que permite identificar patrones sospechosos más allá del simple número de intentos fallidos.

### **Detección de anomalías para identificar ataques reales**

Para mejorar la seguridad, se puede implementar **detección de anomalías** con técnicas más avanzadas, como:

- **Análisis de comportamiento**: Comparar la actividad del usuario con patrones históricos para detectar accesos inusuales.
- **Modelos de machine learning**: Identificar intentos de acceso con características sospechosas (IP, horario, ubicación, velocidad de intentos).
- **Correlación con otros eventos**: Si un intento de acceso va acompañado de exploración de vulnerabilidades o actividad en múltiples servicios, podría indicar un ataque real.

En resumen, **Fail2Ban es una buena primera barrera**, pero **para detectar ataques válidos** es recomendable combinarlo con detección de anomalías y monitoreo en tiempo real.

### **Pirámide de Esfuerzo en Seguridad**

La **Pirámide de Esfuerzo** representa el nivel de dificultad que tiene un atacante para cambiar ciertos indicadores y evadir detecciones. Cuanto más arriba en la pirámide, más difícil es modificar el indicador sin afectar la operatividad del ataque.

|Nivel|Descripción|Dificultad de Cambio|
|---|---|---|
|**Hashes**|Modificar el hash de un archivo es trivial (agregar bytes, recompilar).|**Muy fácil**|
|**Direcciones IP**|Cambiar una IP es sencillo con VPNs, proxies o botnets.|**Fácil**|
|**Nombres de Dominio**|Cambiar un dominio es posible, pero requiere modificar la infraestructura.|**Sencillo**|
|**Artefactos de Host o Red**|Cambiar configuraciones específicas en endpoints o tráfico es más molesto.|**Moderado**|
|**Herramientas**|Si la herramienta usada para el ataque es bloqueada, el atacante debe desarrollar o adaptar otra.|**Retador**|
|**TTPs (Técnicas, Tácticas y Procedimientos)**|Cambiar la metodología completa del ataque requiere entrenamiento y reestructuración operativa.|**Difícil**|

### **Fuzzy Hashing**

El **Fuzzy Hashing** (hash difuso) es una técnica que permite comparar archivos similares aunque no sean idénticos. A diferencia de los hashes criptográficos tradicionales (como SHA-256 o MD5), que cambian drásticamente con una pequeña modificación, los fuzzy hashes detectan similitudes parciales entre archivos.

#### **Ejemplos de usos de Fuzzy Hashing en seguridad**

- **Detección de variantes de malware**: Si un atacante recompila un binario malicioso para cambiar su hash, un fuzzy hash aún puede reconocer similitudes con versiones anteriores.
- **Análisis forense**: Comparar archivos sospechosos con bases de datos de muestras conocidas.
- **Detección de evasión**: Comparar logs, documentos o ejecutables que han sido levemente modificados para evitar detección.

Una herramienta común para fuzzy hashing es **ssdeep**, que genera y compara hashes difusos de archivos.


### **Emulación de Adversarios y Uso de MITRE ATT&CK**

Desde la **Comisión Europea** se está promoviendo la **emulación de adversarios** como un enfoque para mejorar la resiliencia cibernética, alineándose con prácticas avanzadas como las pruebas de seguridad ofensivas y la inteligencia de amenazas. Un ejemplo es la emulación del grupo **Lazarus**, replicando sus tácticas y técnicas para evaluar la efectividad de los controles defensivos.

MITRE ATT&CK es un marco ampliamente utilizado que documenta técnicas de ataque reales utilizadas por grupos **APT (Advanced Persistent Threats)**. No solo sirve para documentación, sino que es una herramienta esencial para:

- **Mejorar las capacidades de detección.**
- **Estandarizar y operacionalizar la inteligencia de amenazas.**
- **Emular adversarios en entornos controlados.**
- **Priorizar la defensa y evaluar capacidades.**
- **Guiar las decisiones de ingeniería para mejorar detección, respuesta y prevención.**
[[MITRE-ATTCK]]
### **APT y la Emulación de Adversarios**

Algunos grupos conocidos que han sido emulados para pruebas de defensa incluyen:

- **APT3 (Pirates of the Three Kingdoms)**: Utilizado para evaluar herramientas de detección avanzada.
- **APT41**: Conocido por sus campañas de espionaje y cibercrimen financiero.

### **BlackBasta y su Modelo de Ataque**

BlackBasta no es un único grupo de actores de amenazas, sino un **ransomware-as-a-service (RaaS)** con varias células operando bajo el mismo nombre.

- **Initial Access Techniques**:
    
    - Phishing con documentos maliciosos.
    - Explotación de accesos remotos no asegurados.
    - Uso de credenciales robadas.
- **Double Extortion Model**:
    
    - Cifran archivos y exfiltran datos.
    - Exigen pago no solo para descifrar, sino también para evitar la filtración de la información.
- **Notas de rescate**:
    
    - Proporcionan a la víctima un código único con instrucciones para contactar con los atacantes.
    - Suelen dar un plazo de **10 a 12 días** para pagar antes de publicar los datos robados.

---

### **Kill Chain aplicada a BlackBasta**

Para responder ante ataques de **BlackBasta**, podemos mapear su actividad en la **Kill Chain** y analizar qué defensas pueden interrumpir cada fase:

1. **Reconocimiento**
    
    - **Acción defensiva**: Monitorear accesos inusuales, implementar inteligencia de amenazas, proteger información expuesta en internet.
2. **Weaponization**
    
    - **Acción defensiva**: Implementar restricciones en la ejecución de macros y binarios desconocidos.
3. **Entrega**
    
    - **Acción defensiva**: Filtrado de correos, sandboxing de archivos sospechosos, detección de patrones de spear-phishing.
4. **Explotación**
    
    - **Acción defensiva**: Aplicación de parches, hardening de sistemas, segmentación de red para limitar movimientos laterales.
5. **Instalación**
    
    - **Acción defensiva**: Restricción de privilegios, detección de anomalías en la instalación de software, EDR/XDR para identificar ejecución de payloads.
6. **Command and Control (C2)**
    
    - **Acción defensiva**: Bloqueo de dominios maliciosos, inspección de tráfico saliente, detección de conexiones persistentes inusuales.
7. **Actions on Objective**
    
    - **Acción defensiva**: Monitorización de movimientos laterales, backups protegidos contra cifrado, mitigación de exfiltración de datos.

### **Conclusión**

Utilizar frameworks como **MITRE ATT&CK** y la **Kill Chain** nos permite estructurar una defensa efectiva contra adversarios como **BlackBasta**. La clave está en diseñar una estrategia de seguridad por capas, donde cada fase del ataque represente una oportunidad para detenerlo antes de que cumpla su objetivo.

### **BlackBasta y su Evolución en Técnicas de Ataque**

BlackBasta ha ido **evolucionando** y adaptando sus tácticas, integrando herramientas previamente utilizadas en otros tipos de malware, como **Aakbot**, que originalmente era un troyano bancario.

---

### **Métodos de Distribución**

- **Spearphishing**:
    
    - BlackBasta utiliza correos dirigidos con ingeniería social para engañar a empleados y obtener acceso inicial.
    - Puede incluir archivos adjuntos maliciosos o enlaces a sitios falsos para robar credenciales.
- **Explotación de Vulnerabilidades (MITRE ATT&CK - T1190)**:
    
    - En algunos casos, los afiliados de BlackBasta explotan vulnerabilidades en servicios expuestos para obtener acceso a la red.
    - **Técnica T1190 (Exploiting Public-Facing Applications)**: Ataques dirigidos contra aplicaciones accesibles desde internet (como servidores VPN, RDP sin seguridad, o sistemas CMS vulnerables).
- **Obtención de Credenciales Válidas**:
    
    - Algunas intrusiones se han realizado con credenciales legítimas obtenidas a través de phishing o bases de datos filtradas.
    - Esto permite acceso sin levantar sospechas en los sistemas de defensa.

---

### **Uso de CMDB en la Gestión de Activos y su Impacto en Seguridad**

- **CMDB (Configuration Management Database)** es una base de datos utilizada para gestionar activos y su configuración dentro de una organización.
- Una **CMDB mal gestionada** puede convertirse en un problema de seguridad si:
    - No se actualizan los activos correctamente (software sin mantenimiento, sistemas obsoletos).
    - No se documentan correctamente accesos y configuraciones, lo que dificulta la detección de cambios sospechosos.
    - No se protegen adecuadamente, permitiendo que atacantes obtengan información útil para el reconocimiento.

---

### **Estrategias de Defensa ante BlackBasta**

Para contrarrestar los ataques de BlackBasta, se pueden aplicar contramedidas en cada fase de su **Kill Chain**:

1. **Prevención de Spearphishing:**
    
    - Implementar **filtros avanzados de correo** para detectar archivos adjuntos sospechosos y enlaces maliciosos.
    - **Autenticación multifactor (MFA)** para evitar acceso con credenciales robadas.
2. **Protección contra T1190 (Exploitation of Public-Facing Applications):**
    
    - **Parcheo continuo** de sistemas expuestos a internet.
    - **Reducción de la superficie de ataque**, limitando accesos externos solo a direcciones IP de confianza.
3. **Detección de uso de credenciales válidas:**
    
    - **Monitorización de accesos inusuales**, como inicios de sesión desde ubicaciones inesperadas.
    - Implementación de **reglas de detección en SIEM**, analizando el comportamiento de los usuarios.
4. **Refuerzo de la CMDB:**
    
    - **Mantener un inventario actualizado** de software y hardware en la organización.
    - Implementar **control de cambios**, verificando qué activos han sido modificados o accedidos recientemente.
    - **Restringir el acceso a la CMDB**, ya que puede ser utilizada por atacantes para planear movimientos laterales.
5. **Detección y Respuesta ante BlackBasta y Aakbot:**
    
    - **EDR/XDR** para detectar patrones de ejecución anómalos.
    - **Monitorización de tráfico de red**, identificando conexiones con servidores de C2 sospechosos.
    - **Implementación de listas de bloqueo dinámicas**, basadas en inteligencia de amenazas actualizada.

---

### **Conclusión**

BlackBasta no solo emplea **ransomware**, sino que utiliza tácticas avanzadas para el acceso inicial, persistencia y movimiento lateral. Su uso de **Aakbot, spearphishing y explotación de vulnerabilidades (T1190)** requiere una **defensa en profundidad**, combinando detección proactiva con una buena gestión de activos.




### **Delito Inducido y Ciberseguridad**

El concepto de **delito inducido** implica incitar o facilitar la comisión de un delito. En ciberseguridad, se ve en situaciones donde actores maliciosos crean un **mercado de credenciales robadas**, donde:

1. **Atacantes roban credenciales** y las venden en foros clandestinos.
2. **Empresas de dudosa ética compran esas credenciales** y luego ofrecen servicios de "protección" a las víctimas, obligándolas a pagar para recuperar acceso.

Esto crea un **ciclo perverso**, similar a la frase: _“tomar droga para hacer música sobre tomar droga”_, donde la propia existencia del servicio depende de alimentar el problema que supuestamente mitiga.

Lo único que **las organizaciones pueden controlar directamente** en este tipo de situaciones es **el tiempo de respuesta en parchear y mitigar vulnerabilidades**, minimizando la ventana de oportunidad para los atacantes.

---

### **Gestión de Riesgos en Seguridad**

Cuando el equipo de gestión presenta una tabla de **probabilidad e impacto de riesgos**, el objetivo de seguridad es **reducir los riesgos críticos (color rojo)**.

#### **Cómo mitigar un riesgo sin seguir ciegamente la evaluación de gestión:**

- **Reducir la probabilidad**
    
    - Analizar el número real de atacantes con capacidad para explotar la vulnerabilidad.
    - Revisar si hay **evidencia real** de que el exploit se esté usando en ataques activos.
- **Reducir el impacto**
    
    - Implementar **hardening** (endurecimiento de sistemas para minimizar la explotación).
    - Usar un **WAF (Web Application Firewall)** para bloquear ataques en aplicaciones web antes de que lleguen al sistema.

---

### **Acceso Inicial: Identificación y Evaluación de Vulnerabilidades**

Para gestionar vulnerabilidades, se utilizan varios sistemas de clasificación y priorización:

| **Concepto**                                   | **Descripción**                                                                                                            |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **CVE (Common Vulnerabilities and Exposures)** | Identificador único de cada vulnerabilidad publicada.                                                                      |
| **CVSS (Common Vulnerability Scoring System)** | Puntuación de la gravedad de una vulnerabilidad en función de su impacto y facilidad de explotación.                       |
| **CPE (Common Platform Enumeration)**          | Identifica qué software y versiones están afectados por una vulnerabilidad.                                                |
| **CWE (Common Weakness Enumeration)**          | Clasifica los tipos de fallos de seguridad subyacentes (por ejemplo, buffer overflow, inyección SQL).                      |
| **EPSS (Exploit Prediction Scoring System)**   | Basado en análisis de datos históricos, predice la probabilidad de que una vulnerabilidad sea explotada en ataques reales. |
| **KEV (Known Exploited Vulnerabilities List)** | Lista de vulnerabilidades que **ya han sido explotadas activamente** en ataques reales.                                    |

---

### **Priorización de Parches y Respuesta a Vulnerabilidades**

1. **Si una vulnerabilidad está en KEV**, se **debe priorizar inmediatamente**, porque ya ha sido explotada en el mundo real.
2. **Si tiene un EPSS alto**, hay un alto riesgo de que pueda ser explotada pronto.
3. **Si afecta a software crítico (CPE) y tiene un CVSS alto**, la corrección debe hacerse lo antes posible.

El objetivo no es **parchear todo inmediatamente**, sino **priorizar inteligentemente** para reducir el riesgo de manera eficiente.

---

### **Conclusión**

El delito inducido en ciberseguridad se refleja en mercados ilegales de credenciales y modelos de negocio que **aprovechan la inseguridad** en lugar de solucionarla. La clave para la defensa efectiva es **reducir la probabilidad y el impacto de ataques**, priorizando la mitigación de vulnerabilidades con datos de **KEV, EPSS y CVSS**, y aplicando medidas como **hardening y WAFs** para minimizar el daño en caso de explotación.
