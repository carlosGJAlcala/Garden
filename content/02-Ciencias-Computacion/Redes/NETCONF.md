---
title: "Netconf"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**NETCONF** (Network Configuration Protocol) es un protocolo estándar para la **gestión y configuración de dispositivos de red**. Fue desarrollado por la **IETF** (Internet Engineering Task Force) y está diseñado para ser utilizado en redes **definidas por software (SDN)** y en **entornos de redes complejas**, permitiendo una forma más estructurada, eficiente y automatizada de gestionar dispositivos de red como routers, switches, firewalls, entre otros.

### Características Claves de NETCONF


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Ansible|Ansible]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

1. **Basado en XML**:
    
    - **NETCONF** usa **XML** (Extensible Markup Language) para codificar los datos de configuración y las respuestas, lo que permite un formato estructurado y fácilmente comprensible tanto para humanos como para máquinas.
        
2. **Comunicación a través de SSH**:
    
    - **NETCONF** se comunica de forma segura utilizando el **protocolo SSH** para establecer una conexión entre el cliente (herramienta de gestión) y el dispositivo de red. Esto garantiza que los datos de configuración estén protegidos durante la transmisión.
        
3. **Operaciones de Configuración**:
    
    - **NETCONF** soporta operaciones estándar como:
        
        - **get**: recuperar la configuración del dispositivo.
            
        - **edit-config**: realizar cambios en la configuración del dispositivo.
            
        - **commit**: confirmar los cambios realizados.
            
        - **rollback**: revertir los cambios a la configuración anterior.
            
        - **lock**: bloquear el dispositivo para evitar que otros usuarios realicen cambios simultáneamente.
            
        - **unlock**: liberar el bloqueo del dispositivo.
            
4. **Modelo de Datos YANG**:
    
    - **NETCONF** utiliza **YANG (Yet Another Next Generation)**, un modelo de datos para la definición de las configuraciones que pueden ser gestionadas a través de NETCONF. YANG proporciona una estructura estandarizada para representar las configuraciones de los dispositivos de red y sus estados.
        
5. **Automatización y Gestión Centralizada**:
    
    - **NETCONF** permite la **automatización** de la gestión de redes mediante **scripts** y herramientas de orquestación, proporcionando una solución más eficiente y centralizada para administrar dispositivos en grandes redes.
        
6. **Soporte para Transacciones Atómicas**:
    
    - **NETCONF** permite realizar **transacciones atómicas**, lo que significa que puedes hacer múltiples cambios en la configuración de un dispositivo y confirmar todos esos cambios de una sola vez. Si algo falla, puedes revertir los cambios completos sin afectar el estado anterior.
        

### Beneficios de NETCONF

1. **Automatización y Eficiencia**:
    
    - **NETCONF** permite la **automatización** de tareas de configuración, lo que reduce el trabajo manual y minimiza los errores humanos.
        
    - Es ideal para **gestionar grandes infraestructuras de red** de manera consistente y rápida.
        
2. **Gestión de Configuración Centralizada**:
    
    - Puedes gestionar **dispositivos de red** de manera centralizada desde un único controlador o sistema de gestión, sin tener que acceder manualmente a cada dispositivo.
        
3. **Mejor Seguridad**:
    
    - **NETCONF** utiliza **SSH** para las comunicaciones, lo que asegura la **autenticación** y **confidencialidad** de las configuraciones transmitidas.
        
4. **Escalabilidad**:
    
    - **NETCONF** está diseñado para ser escalable, permitiendo gestionar miles de dispositivos de red sin perder eficiencia, lo cual es esencial en redes de gran tamaño o distribuídas.
        
5. **Reversibilidad**:
    
    - Si algo sale mal durante una configuración, **NETCONF** permite revertir a configuraciones previas de forma sencilla con la operación **rollback**.
        

---

### Cómo Funciona NETCONF

1. **Cliente y Servidor**:
    
    - **NETCONF** funciona en un modelo cliente-servidor. El **servidor** es el dispositivo de red que se va a configurar (router, switch, firewall, etc.), y el **cliente** es la herramienta de gestión que se usa para enviar las configuraciones, como **Cisco Network Services Orchestrator (NSO)**, **Ansible** con su módulo NETCONF, o herramientas propias.
        
2. **Transacciones**:
    
    - Las **operaciones NETCONF** son transacciones que se ejecutan de manera **atómica**. Esto significa que todas las configuraciones y cambios realizados en un dispositivo deben completarse con éxito; si algo falla, el sistema puede revertir a su configuración original.
        
3. **Intercambio de Datos**:
    
    - Cuando se realiza una consulta con **get** o se actualiza la configuración con **edit-config**, los datos se estructuran en **XML** y se intercambian entre el cliente y el servidor de manera segura a través de SSH.
        
4. **Interacción con YANG**:
    
    - **YANG** es el modelo de datos utilizado por **NETCONF** para definir la estructura de la configuración que se intercambia entre los dispositivos de red y las herramientas de gestión. YANG permite representar configuraciones de dispositivos como **interfaces de red**, **rutas**, **políticas de seguridad**, entre otras.
        

---

### Ejemplo de Comandos de NETCONF

#### 1. **Conexión a un dispositivo NETCONF**

Para comenzar a interactuar con un dispositivo de red mediante **NETCONF**, se utiliza una **herramienta cliente** como **ncclient** (en Python) o **NetConfClient** en otros entornos. Aquí tienes un ejemplo de cómo se establece una conexión:

```python
from ncclient import manager

with manager.connect(host='192.168.1.1', port=830, username='admin', password='admin', hostkey_verify=False) as m:
    print(m.get_config(source='running').xml)
```

#### 2. **Recuperar Configuración Actual (get)**

```xml
<rpc xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
  <get>
    <filter type="subtree">
      <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
        <interface>
          <name>eth0</name>
        </interface>
      </interfaces>
    </filter>
  </get>
</rpc>
```

Este comando **get** recupera la configuración de la interfaz **eth0** en el dispositivo de red.

#### 3. **Editar Configuración (edit-config)**

```xml
<rpc xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
  <edit-config>
    <target>
      <running/>
    </target>
    <config>
      <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
        <interface>
          <name>eth0</name>
          <type xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">iana-if-type:ethernetCsmacd</type>
          <enabled>true</enabled>
          <ipv4 xmlns="urn:ietf:params:xml:ns:yang:ietf-ip">
            <address>
              <ip>192.168.1.1</ip>
              <netmask>255.255.255.0</netmask>
            </address>
          </ipv4>
        </interface>
      </interfaces>
    </config>
  </edit-config>
</rpc>
```

Este comando **edit-config** configura una dirección **IP estática** en la interfaz **eth0** del dispositivo.

---

### Herramientas de NETCONF

- **ncclient** (Python): Es una biblioteca de cliente para interactuar con dispositivos NETCONF.
    
- **Ansible**: Ansible tiene un módulo `netconf` para configurar dispositivos de red a través de NETCONF.
    
- **Cisco NSO**: Una plataforma de orquestación para redes que utiliza NETCONF como base.
    
- **YANG Tools**: Herramientas para trabajar con modelos YANG y generar configuraciones basadas en NETCONF.
    

---

### Conclusión

**NETCONF** es un protocolo extremadamente potente y flexible para **gestionar dispositivos de red**. Su capacidad para trabajar de manera estructurada con **YANG**, utilizar **SSH** para garantizar la seguridad, y soportar **transacciones atómicas** lo hace adecuado para redes **definidas por software (SDN)** y entornos de redes automatizadas. Su **interoperabilidad** entre diferentes fabricantes y su enfoque en la **configuración centralizada** lo convierte en una opción ideal para **gestionar grandes infraestructuras de red** de manera eficiente.