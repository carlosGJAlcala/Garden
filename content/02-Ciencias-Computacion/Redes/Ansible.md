---
title: "Ansible"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---

### 1. **Instalación y configuración del entorno Ansible**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Bases-Datos/MongoDB|MongoDB]]. [[02-Ciencias-Computacion/Redes/Grafana|Grafana]]. [[02-Ciencias-Computacion/Redes/VAGRANT|VAGRANT]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

En este ejercicio, se comienza instalando Ansible en una máquina **manager** (en este caso, una máquina virtual dentro de un entorno gestionado por Vagrant). Luego, se establece una conexión SSH con los servidores **host1** y **host2** para permitir que Ansible ejecute tareas en estos.

- **Instalación de Ansible**:  
    Para instalar Ansible en el **manager**, se realiza el proceso de configuración según las instrucciones de un tutorial (como en el caso del tutorial de DigitalOcean). Posteriormente, Ansible es configurado para usar claves privadas RSA para las conexiones SSH.
    
- **Configuración del inventario**:  
    Se configura el archivo de inventario de Ansible (`/etc/ansible/hosts`) para incluir los **host1** y **host2** bajo el grupo `servers`.
    
- **Comprobación con el módulo `ping`**:  
    Ansible permite ejecutar comandos a través de módulos. Se verifica que la conexión funciona correctamente con el módulo **ping**:
    
    ```bash
    ansible servers -m ping
    ```
    

### 2. **Uso básico de Ansible**

Ansible se utiliza para ejecutar comandos o tareas de configuración en múltiples máquinas de forma simultánea. Los módulos más comunes incluyen:

- **Shell**: Ejecuta comandos en las máquinas objetivo. Por ejemplo, el siguiente comando obtiene el estado de los procesos en ejecución en los servidores:
    
    ```bash
    ansible servers -m shell -a 'ps -aux'
    ```
    
- **Copy**: Copia archivos desde la máquina de control (en este caso, **manager**) hacia los hosts de destino (**host1** y **host2**).
    
    ```bash
    ansible servers -m copy -a "src=/etc/hosts dest=/tmp/hosts"
    ```
    
- **Comando `ansible-console`**: Permite interactuar de manera interactiva con los hosts a través de una consola, facilitando la ejecución de comandos sin tener que escribirlos todos en una sola línea.
    

### 3. **Configuración de servicios con Ansible**

Ansible permite realizar configuraciones complejas y repetitivas de manera automatizada mediante **playbooks**. En el caso de la práctica, se configura **SNMPv3** en los dispositivos **host1** y **host2**.

- **Playbook para SNMPv3**: El playbook `snmpv3.yml` es creado para realizar tareas específicas, como:
    
    - Copiar el archivo de configuración `snmpd.conf` en los hosts.
        
    - Reiniciar el servicio **snmpd** en los hosts para aplicar la configuración.
        

Este tipo de tareas son definidas en el playbook, donde cada tarea se ejecuta en los hosts definidos en el inventario.

### 4. **Instalación de servicios con Ansible**

En la parte final de la práctica, se aprende cómo **instalar y configurar servicios** en los hosts utilizando playbooks. Ejemplos de servicios incluyen servidores web como **Node.js** o **MongoDB**, o sistemas de monitoreo como **Nagios** o **Grafana**.

La idea es usar **roles**, **variables**, **handlers** y **templates** de Ansible para gestionar la instalación, configuración y puesta en marcha de estos servicios de manera automatizada.

### Conclusión

Ansible es una herramienta poderosa para la automatización de tareas de configuración, implementación y mantenimiento de sistemas. En esta práctica, se aprende cómo usar Ansible para automatizar la configuración de servidores, utilizando módulos para ejecutar tareas remotas, playbooks para configuraciones complejas y la posibilidad de gestionar servicios a gran escala. La capacidad de Ansible para gestionar múltiples servidores simultáneamente y su enfoque sin agente lo hace muy adecuado para ambientes de infraestructura dinámica y escalable.

Si necesitas ayuda adicional con los detalles específicos de la práctica o los playbooks de Ansible, no dudes en preguntar.