---
title: "Partes Principales De Un Sistema Robotico"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---

### **Actuadores**


> **Relacionado**: [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

Son los dispositivos que ejecutan acciones físicas en el mundo real, basadas en las órdenes que reciben del sistema de control. Por ejemplo:

- Motores eléctricos → mueven ruedas, brazos, etc.
    
- Servomotores → permiten movimientos más precisos (posición angular controlada).
    
- Actuadores neumáticos o hidráulicos → usados en contextos industriales por su fuerza.
    

 **En ciberseguridad**, un atacante que logra comprometer el sistema de control podría generar comandos maliciosos para mover actuadores de forma peligrosa (por ejemplo, abrir una válvula, girar una rueda, etc.). Este tipo de amenaza está presente en ataques a infraestructuras críticas o fábricas automatizadas (ICS/SCADA).

---

### ️ **Sensores**

Son los "ojos" y "oídos" del sistema. Recogen información del entorno (externa) o del propio robot (interna):

- **Externos**: cámara, LIDAR, sensores ultrasónicos, sensores de proximidad, radar, sensores láser.
    
- **Internos**: encoders, giróscopos, acelerómetros, sensores de corriente o temperatura.
    

Los sensores se clasifican también como:

- **Activos**: emiten una señal (láser, ultrasonido, IR) y miden la respuesta.
    
- **Pasivos**: detectan el entorno sin emitir energía (cámara, micrófono, brújula).
    

 **En ataques**, los sensores pueden ser:

- Falsificados (spoofing): por ejemplo, enviar una señal de ultrasonido falsa.
    
- Cegados (blinding): usando luz láser contra cámaras o sensores ópticos.
    
- Saturados: enviando señales que los hagan responder erróneamente (DoS).
    

---

###  **Procesadores (Sistema de Control)**

Son el "cerebro". Reciben la información de los sensores, la procesan y generan comandos para los actuadores. Incluyen:

- Microcontroladores para tareas de bajo nivel (motores, lectura de sensores).
    
- Ordenadores con capacidad de planificación, navegación o visión.
    
- Software embebido o incluso sistemas operativos como ROS (Robot Operating System).
    

 **Vulnerabilidades típicas**:

- Firmware inseguro o desactualizado.
    
- Comunicación no cifrada entre sensores, actuadores y controladores.
    
- Interfaces de configuración (como CLI o HTTP) abiertas o sin autenticación.
    

---

###  En resumen:

|Componente|Función principal|Riesgo de ciberseguridad|
|---|---|---|
|Actuador|Ejecuta acciones físicas|Manipulación de movimientos o estados|
|Sensor|Detecta entorno o estado|Spoofing, blinding, DoS, lectura indebida|
|Procesador|Toma decisiones y coordina|Acceso al sistema de control y lógica|

---

