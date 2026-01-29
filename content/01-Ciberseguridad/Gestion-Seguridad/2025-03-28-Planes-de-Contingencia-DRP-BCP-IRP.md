---
title: "Tipos de incidentes de seguridad"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
---
## Incidentes


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

---

No se castiga fallar, **se castiga no intentarlo**.  
Si se produce un compromiso habiendo actuado correctamente e intentado prevenirlo, la lectura es distinta y puede considerarse como una situación gestionada de buena fe.

---

### Planificación ante contingencias

En el ámbito de la seguridad de la información y la gestión de la continuidad operativa, existen tres planes clave que forman la base de cualquier estrategia de resiliencia:

- **Plan de recuperación ante desastres (DRP)**: establece cómo restaurar sistemas críticos y servicios tras un desastre tecnológico o físico grave.
    
- **Plan de continuidad de negocio (BCP)**: define cómo asegurar la continuidad de las funciones esenciales de la organización durante y después de una interrupción significativa.
    
- **Plan de respuesta a incidentes (IRP)**: detalla los procedimientos para identificar, gestionar y resolver incidentes de seguridad, limitando daños y acelerando la recuperación.
    

---

### Bases de estos planes

El problema más grave que puede afrontar una organización es aquel que compromete la **continuidad del negocio**.  
En algunos casos, **es preferible afrontar sanciones regulatorias antes que una parada total de la operación**, que podría tener un impacto mucho mayor en términos económicos y reputacionales.

Para diseñar planes eficaces es fundamental:

- **Conocer y priorizar las amenazas importantes**.
    
- Desarrollar un **plan de actuación claro y bien estructurado**.
    
- **Reducir la probabilidad de incidentes graves** fortaleciendo la seguridad y resiliencia de los sistemas, minimizando así el impacto cuando sea inevitable activar estos planes.
    

Cabe recordar que un **incidente de seguridad puede afectar a los tres pilares fundamentales de la seguridad de la información (CID)**:

- **Confidencialidad**
    
- **Integridad**
    
- **Disponibilidad**
    

---

### Tipos de incidentes

El **INCIBE** (Instituto Nacional de Ciberseguridad) establece una clasificación de los incidentes utilizada habitualmente en el ámbito público y privado en España.

Cada incidente debe ser analizado considerando:

- **Clasificación**: qué tipo de incidente es (ej. malware, phishing, fuga de datos, etc.).
    
- **Severidad**: nivel de impacto potencial o real sobre la organización.
    
- **Categoría o “caja”**: encuadre dentro de las categorías definidas en los planes de gestión y respuesta a incidentes.
    

---

### Intervinientes en la gestión de incidentes

La respuesta efectiva ante un incidente requiere la participación de diferentes perfiles y roles dentro de la organización, entre ellos:

- **Equipo técnico**: encargado de contener, erradicar y recuperar los sistemas afectados.
    
- **Responsable de seguridad**: coordina las tareas y asegura que se cumplen las políticas y procedimientos establecidos.
    
- **Responsable legal**: analiza las implicaciones legales y asegura el cumplimiento de las obligaciones regulatorias (ej. notificación de brechas a autoridades como la AEPD).
    
- **Departamento de comunicación**: gestiona la comunicación interna y externa para proteger la imagen de la organización y transmitir mensajes adecuados a clientes, proveedores y medios.
    
- **Alta dirección**: proporciona apoyo estratégico, toma decisiones clave y asegura los recursos necesarios para la gestión de la crisis.
    

---

Si quieres puedo añadir ejemplos concretos de tipos de incidentes definidos por **INCIBE** o un esquema de cómo se relacionan estos tres planes (BCP, DRP, IRP). Solo dime. 

---

# Tipos de incidentes de seguridad

## ¿Qué hace un equipo de gestión de incidentes?

Ante un ataque de tipo **DDoS**, el equipo de gestión de incidentes no puede hacer mucho directamente, ya que **la respuesta corresponde principalmente al equipo de redes**.

En muchos casos, **la clave no es tanto la parte técnica, sino saber cómo actuar y coordinarse** adecuadamente.

### Algunos tipos de incidentes frecuentes:

- **Abuso de cuentas**
    
- **Intrusión en un ordenador o red**
    
- **Robo y exposición de información**
    
- **Infección por malware**
    
- **Ataques DDoS**
    

---

# Taxonomía del CCN-STIC 817 (ENS)

Esta taxonomía clasifica los tipos de incidentes en función de su naturaleza. Algunos ejemplos clave:

### **Contenido abusivo**

Ataques orientados a manipular la opinión pública o a propagar contenido ilegal o inadecuado. Ejemplo: campañas de influencia política (como las atribuidas a Rusia).

> _El profesor asegura que este tipo de campañas irá a más._

- **Spam**
    
- **Delitos de odio**
    
- **Contenidos inapropiados**
    

---

### **Contenido dañino**

Ataques que comprometen sistemas, servidores o redes.

- **Sistema infectado**
    
- **Servidor de Comando y Control (C2)**
    
- **Distribución de malware**
    
- **Configuraciones maliciosas (backdoors, troyanos, etc.)**
    

---

### **Obtención de información**

Actividades previas a un ataque para mapear y recolectar datos sobre una organización.

- **Escaneo de redes**
    
    > A veces se declara como incidente por lo que puede venir después.
    

---

### **Intento de intrusión**

Acciones activas para acceder sin autorización pero sin lograr éxito.

---

### **Intrusión**

Acceso no autorizado con robo de información o manipulación de sistemas.

---

### **Disponibilidad**

Ataques que buscan **interrumpir el servicio**, como los **DDoS** o **DoS**.

---

### **Fraude**

Engaños para obtener información sensible (phishing, vishing, ingeniería social, etc.).

---

### **Vulnerabilidades**

Problemas de seguridad, como:

- **Criptografía débil** no es el mayor problema.
    
- **Amplificadores de DDoS**:
    
    - Uso de **servidores DNS recursivos** abiertos
        
    - **Petición de volcados de memoria** para explotar configuraciones inseguras
        

---

### **Otros**

Cualquier otro tipo de incidente que no entre en las categorías anteriores.

- **APT (Amenazas Persistentes Avanzadas)**: ataques dirigidos, sigilosos y prolongados en el tiempo, normalmente atribuidos a actores estatales o grupos muy organizados.

---

# Categorías del CCN

El **Centro Criptológico Nacional (CCN)** establece categorías para clasificar y priorizar los incidentes de seguridad, lo que permite una gestión más eficaz y proporcional al impacto potencial sobre los activos afectados. Entre las categorías más relevantes destacan:

- **Incidentes prioritarios**: relacionados con **información clasificada**, donde el compromiso puede suponer un riesgo crítico para la seguridad nacional.
    
- **Ciberespionaje**: actividades dirigidas a acceder a información sensible o estratégica sin autorización.
    
- **Exfiltración de datos**: robo de información confidencial o sensible.
    
- **Servicios comprometidos**: ataques que afectan la disponibilidad o integridad de servicios esenciales.
    
- **Toma de control**: obtención de acceso y control total sobre sistemas o redes.
    
- **Robo y publicación de datos**: extracción y difusión no autorizada de información sensible.
    
- **Ciberdelito**: delitos comunes cometidos utilizando medios tecnológicos (fraude, estafas, etc.).
    
- **Suplantación de identidad**: uso fraudulento de credenciales o datos personales para acceder o realizar acciones en nombre de otro individuo.
    

La **clasificación de la información** también determina cómo se gestiona el acceso a los datos y qué requisitos deben cumplir las personas para manejarlos, por ejemplo, mediante la **habilitación personal de seguridad (HPS)**.

---

# Fases de la respuesta a incidentes

El proceso de respuesta a incidentes incluye varias fases clave que aseguran una gestión sistemática y eficiente:

1. **Planificación**: preparación previa a la aparición del incidente; incluye procedimientos, herramientas y equipos definidos.
    
2. **Detección**: identificación temprana de posibles incidentes; aquí juegan un papel central los **Security Operations Centers (SOC)** y las herramientas de monitorización.
    
3. **Análisis**: evaluación técnica del incidente para determinar su naturaleza, alcance e impacto.
    
4. **Contención**: acciones para limitar la propagación y daños del incidente.
    
5. **Erradicación y recuperación**: eliminación de la amenaza y restauración de sistemas a un estado seguro.
    
6. **Documentación y lecciones aprendidas**: registro detallado de las acciones realizadas para mejora continua.
    

---

# El papel del director en la respuesta a incidentes

Si la respuesta a incidentes depende únicamente de decisiones improvisadas del director, el resultado puede ser un **fracaso organizativo**. La clave está en que la respuesta esté:

- **Indicada y documentada previamente** en procedimientos normalizados.
    
- **Aprobada (homologada)**, para que cualquier miembro del equipo pueda ejecutarla conforme al estándar definido.
    
- **Independiente de las personas concretas**, garantizando continuidad aunque haya rotación de personal.
    

El nivel de madurez de estos procesos puede evaluarse según modelos como **CMMI-DEV**:

- Inicial.
    
- Repetible.
    
- Definido.
    
- Gestionado.
    
- Optimizado.
    

Todo debe ser **medible y mejorable continuamente**.

---

# Recursos técnicos clave

Para la respuesta efectiva a incidentes, son fundamentales:

- **Recopilación y análisis de logs**: herramientas como **ElasticSearch** o **Splunk** permiten centralizar y analizar registros de eventos de los sistemas.
    
- **Playbooks**: guías de actuación detalladas para los escenarios más comunes.
    
- **Simulacros**: permiten probar la preparación real del equipo y ajustar procedimientos antes de que ocurra un incidente real.
    

Aunque el **análisis de riesgos debería ser la base de la seguridad**, en la práctica los incidentes reales suelen ser los que determinan **dónde se debe priorizar la inversión y los recursos**.

---

# Roles en la gestión de incidentes

- **El escribiente**: documenta cada acción y decisión tomada durante la respuesta.
    
- **El investigador**: analiza técnicamente las causas y efectos del incidente.
    
- **El gestor**: organiza y coordina la respuesta.
    

---

# Caso específico: Phishing

El phishing es uno de los incidentes más comunes y debe gestionarse de forma sistemática:

- **Cómo llegan**: principalmente por correo electrónico, aunque también mediante SMS (smishing) o mensajería instantánea.
    
- **Cómo se reporta**: es útil establecer **formularios o botones específicos para que los usuarios puedan reportar correos sospechosos fácilmente**.
    

Acciones recomendadas en la gestión de un phishing:

 **Identificación de objetivos**:

- ¿Cuántos usuarios han recibido el mensaje?
    
- ¿A quiénes específicamente? (detectando posibles spear phishing).
    

 **Medidas de respuesta**:

- Avisar a los usuarios afectados.
    
- Eliminar el correo malicioso de buzones internos.
    
- Bloquear el asunto, remitente y enlaces relacionados.
    
- Notificar formalmente el phishing al proveedor de correo y a autoridades si corresponde.
    

 **Limitaciones**:

- En el caso de **SMS**, es más difícil actuar: no se pueden bloquear centralizadamente y la actuación se limita a advertir y sensibilizar a los usuarios.
    

 **Otros enfoques técnicos**:

- **Canarios o honeypots**: cuentas de correo monitorizadas para detectar ataques de phishing dirigidos antes de que afecten a empleados reales.
    
- **Obtención de la IP del atacante**: para ayudar a identificar la infraestructura empleada y contribuir a investigaciones posteriores.
    

