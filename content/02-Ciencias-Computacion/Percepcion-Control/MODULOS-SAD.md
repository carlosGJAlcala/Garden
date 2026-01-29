---
title: "Modulos Sad"
date: 2026-01-26
tags:
  - ciencias-computacion
  - percepcion-control
---
En el contexto de sistemas automáticos y robótica, los **módulos SAD** (Sistema Automático Digital) se refieren a la **descomposición funcional de un sistema de control digital** en **módulos interconectados**, donde cada módulo realiza una función específica dentro del lazo de control. Este enfoque modular es esencial para el diseño, implementación y análisis de sistemas complejos.

---

##  ¿Qué son los módulos SAD?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[03-Desarrollo-Software/Concurrencia/Timer|Timer]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Konversation/konversation|konversation]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/Instalacion-y-Configuracion-de-Splunk-Universal-Forwarder-con-Snort-en-Windows-y-Ubuntu|Instalacion y Configuracion de Splunk Universal Forwarder con Snort en Windows y Ubuntu]]. [[01-Ciberseguridad/Ingenieria-Inversa/2025-01-21-INGENIERIA-INVERSA|2025 01 21 INGENIERIA INVERSA]].

Un **Sistema Automático Digital (SAD)** está compuesto por **módulos funcionales** que interactúan entre sí para percibir, procesar y actuar sobre un entorno. Su estructura sigue típicamente el **modelo de lazo cerrado** y puede implementarse en microcontroladores, PLCs, SoCs, o sistemas embebidos con ROS.

---

##  Principales módulos de un SAD

Aquí tienes una descripción detallada y ampliada de cada módulo:

---

### 1. **Módulo Sensorial (Adquisición de datos)**

#### Función:

- Captura información del entorno físico y la convierte en una señal digital interpretable por el sistema.
    

#### Componentes típicos:

- **Sensores físicos** (temperatura, presión, velocidad, aceleración, corriente...).
    
- **Conversores A/D (ADC)** para señales analógicas.
    
- Filtros digitales para reducir ruido.
    

#### Ejemplo:

- Un sensor de posición lineal que convierte desplazamiento en voltaje, y este es digitalizado a través del ADC.
    

---

### 2. **Módulo de Tratamiento / Filtrado**

#### Función:

- Mejora la calidad de la señal digital, eliminando ruido o transformando datos para facilitar el análisis posterior.
    

#### Operaciones comunes:

- **Filtrado digital FIR/IIR**.
    
- **Normalización**.
    
- **Conversión de unidades**.
    
- **Estimación de velocidad por derivación numérica**.
    

#### Ejemplo:

- Filtrar una señal de encoder ruidosa con un filtro Butterworth de orden 2.
    

---

### 3. **Módulo de Decisión / Controlador**

#### Función:

- Compara la señal de referencia con la medida y calcula una **acción de control** para reducir el error.
    

#### Tipos comunes:

- **Controladores PID (Proporcional, Integral, Derivativo)**.
    
- Control por modos deslizantes, adaptativo, LQR, fuzzy logic.
    
- Puede incluir lógica de decisión, temporizadores, condiciones booleanas.
    

#### Ejemplo:

- Un PID digital calcula la señal de control u[k]u[k] para que la temperatura medida alcance el valor de consigna.
    

---

### 4. **Módulo de Actuación**

#### Función:

- Transforma la señal digital de control en una señal física que modifique el comportamiento del sistema.
    

#### Componentes típicos:

- **Conversores D/A (DAC)**.
    
- **Puentes H**, transistores, drivers PWM.
    
- **Actuadores**: motores, resistencias, válvulas, relés, servos.
    

#### Ejemplo:

- Controlar la corriente de un motor DC variando el ciclo de trabajo de una señal PWM generada digitalmente.
    

---

### 5. **Módulo de Interfaz Hombre-Máquina (HMI)**

#### Función:

- Permite al operador humano observar el estado del sistema y modificar parámetros.
    

#### Elementos:

- Pantallas, botones, LEDs.
    
- Comunicaciones por UART, I2C, CAN, Ethernet.
    
- Terminales táctiles o SCADA.
    

---

### 6. **Módulo de Comunicación / Supervisión**

#### Función:

- Permite la comunicación con sistemas externos, almacenamiento de datos o supervisión remota.
    

#### Tecnologías:

- CAN bus, Modbus, MQTT, TCP/IP.
    
- Wi-Fi, Bluetooth, ZigBee.
    
- ROS topics, serial USB, etc.
    

---

### 7. **Módulo de Temporización / Sincronización**

#### Función:

- Coordina el funcionamiento periódico de los módulos del SAD.
    
- Define frecuencias de muestreo y control.
    

#### Ejemplo:

- Un **timer** dispara una interrupción cada 10 ms para ejecutar el bucle de control.
    

---

##  Flujo típico en un SAD

```
[SENSOR] → [ADC] → [FILTRO] → [CONTROLADOR] → [DAC/PWM] → [ACTUADOR]
                                    ↑
                          [REFERENCIA / SETPOINT]
```

Cada uno de estos bloques puede ser un **módulo independiente**, con interfaces bien definidas (entrada/salida) que permiten diseño modular, depuración, y escalabilidad.

---

##  Ejemplo aplicado: control digital de temperatura

- **Sensor**: termopar.
    
- **ADC**: convierte mV en datos digitales (ej. 12 bits).
    
- **Filtro**: media móvil para estabilizar lectura.
    
- **Controlador**: PID digital con muestreo cada 100 ms.
    
- **DAC / PWM**: modula una resistencia calefactora.
    
- **Actuador**: elemento calefactor (resistencia).
    
- **HMI**: pantalla táctil para ver temperatura y ajustar consigna.
    

---

##  Ventajas del enfoque modular en SAD

- **Reusabilidad**: módulos como filtros o PID pueden usarse en diferentes sistemas.
    
- **Escalabilidad**: nuevos sensores o actuadores se integran fácilmente.
    
- **Facilidad de pruebas**: cada módulo puede ser testeado por separado.
    
- **Paralelización**: en sistemas con múltiples núcleos o hilos.
    

---

##  Conclusión

Los **módulos de un Sistema Automático Digital (SAD)** representan una arquitectura robusta y flexible que permite implementar lazos de control reales sobre hardware digital. Su diseño modular, basado en el flujo de información desde sensores hasta actuadores, permite abordar desde sistemas embebidos simples hasta robots cognitivos complejos.

Si lo deseas, puedo complementar esto con un **diagrama funcional**, **esquema de implementación en código** o **simulación en MATLAB/Simulink**. ¿Quieres alguno de esos ejemplos?