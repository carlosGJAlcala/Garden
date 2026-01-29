---
title: "Ansible Playbook"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
Un **playbook** de Ansible es un archivo que contiene una serie de **tareas** y **configuraciones** que Ansible debe ejecutar en los sistemas de destino. Estos archivos son escritos en formato YAML (YAML Ain't Markup Language), que es un lenguaje legible por humanos, y describen las acciones que deben realizarse en los equipos administrados.

### Estructura básica de un Playbook


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Ansible|Ansible]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Un **playbook** de Ansible tiene una estructura jerárquica definida que incluye los siguientes elementos clave:

1. **Hosts**: Define en qué grupos o máquinas se va a ejecutar el playbook. Los hosts son especificados en el archivo de inventario de Ansible (usualmente `/etc/ansible/hosts`).
    
2. **Tareas (Tasks)**: Son las acciones que Ansible ejecutará. Cada tarea está asociada con un módulo que realiza una función específica, como copiar un archivo, instalar un paquete o ejecutar un comando.
    
3. **Módulos**: Son las herramientas que realiza Ansible para ejecutar tareas, como `apt`, `yum`, `copy`, `file`, `command`, entre otros.
    
4. **Variables**: Se utilizan para almacenar valores que se pueden reutilizar a lo largo del playbook, lo que permite hacer el playbook más dinámico.
    
5. **Roles**: Son una forma de organizar el código dentro de un playbook en unidades reutilizables. Los roles permiten que la configuración y las tareas relacionadas estén contenidas en una estructura de directorios.
    
6. **Handlers**: Son tareas especiales que se ejecutan solo si se detecta un cambio en alguna tarea anterior. Son útiles para reiniciar servicios después de aplicar configuraciones, por ejemplo.
    

### Ejemplo de un Playbook Simple

Aquí te presento un ejemplo básico de un playbook en Ansible que instala y configura un servicio web (por ejemplo, **nginx**) en varias máquinas.

```yaml
---
- name: Configurar servidor web Nginx
  hosts: web_servers  # Se ejecutará en el grupo "web_servers"
  become: yes         # Indica que se deben usar privilegios de superusuario
  tasks:
    - name: Instalar Nginx
      apt: 
        name: nginx
        state: present    # Asegura que el paquete esté instalado
      notify:
        - Reiniciar Nginx  # Llama al handler para reiniciar el servicio

    - name: Copiar archivo de configuración
      copy:
        src: /local/path/to/nginx.conf
        dest: /etc/nginx/nginx.conf
      notify:
        - Reiniciar Nginx  # Llama al handler para reiniciar el servicio

  handlers:
    - name: Reiniciar Nginx
      service:
        name: nginx
        state: restarted  # Asegura que el servicio de Nginx se reinicie
```

### Explicación del Playbook

1. **Hosts**:
    
    ```yaml
    hosts: web_servers
    ```
    
    Esto significa que el playbook se ejecutará en todas las máquinas que estén definidas en el grupo `web_servers` dentro del archivo de inventario de Ansible.
    
2. **Become**:
    
    ```yaml
    become: yes
    ```
    
    Esto indica que las tareas deben ejecutarse con privilegios de superusuario (es decir, utilizando `sudo`).
    
3. **Tareas**:
    
    - **Instalar Nginx**: Usa el módulo `apt` para instalar el paquete **nginx** en las máquinas de destino. Se asegura de que el paquete esté presente (o lo instala si no lo está).
        
    - **Copiar archivo de configuración**: Utiliza el módulo `copy` para transferir un archivo de configuración desde el controlador (máquina que ejecuta Ansible) a las máquinas de destino.
        
4. **Notificar Handlers**:  
    La directiva `notify` se utiliza para llamar a un handler después de que una tarea se ejecute. En este caso, después de instalar **nginx** o copiar el archivo de configuración, se notificará al handler `Reiniciar Nginx` para que se reinicie el servicio de **nginx** si hay cambios.
    
5. **Handlers**:
    
    - **Reiniciar Nginx**: Este handler reinicia el servicio **nginx** si alguna de las tareas anteriores hizo un cambio (como instalar el paquete o modificar su archivo de configuración).
        

### Beneficios de usar Playbooks

1. **Automatización**: Ansible permite automatizar tareas repetitivas de administración de sistemas de forma sencilla y eficiente, lo que ahorra tiempo y esfuerzo.
    
2. **Escalabilidad**: Puedes aplicar configuraciones a múltiples servidores a la vez, haciendo que la gestión de infraestructuras grandes sea mucho más fácil.
    
3. **Idempotencia**: Ansible asegura que los cambios se apliquen solo cuando sea necesario. Si un servidor ya está configurado correctamente, Ansible no realizará cambios innecesarios, lo que significa que puedes ejecutar el playbook repetidamente sin riesgo de causar inconsistencias.
    
4. **Modularidad**: Los playbooks son modulares y pueden ser reutilizados. Puedes escribir tareas de configuración generales en playbooks que luego puedes usar en diferentes entornos o máquinas.
    
5. **Simplicidad**: Ansible usa YAML, que es fácil de leer y escribir, lo que lo hace accesible incluso para personas sin experiencia previa en programación o automatización.
    

### Ejemplo de Uso de Variables

Las **variables** en Ansible permiten que los playbooks sean más flexibles y reutilizables. Un ejemplo con variables podría ser:

```yaml
---
- name: Instalar Nginx y configurar un sitio web
  hosts: web_servers
  become: yes
  vars:
    web_package: nginx
    site_name: example.com
  tasks:
    - name: Instalar el servidor web
      apt:
        name: "{{ web_package }}"
        state: present

    - name: Copiar archivo de configuración para el sitio web
      copy:
        src: "/templates/{{ site_name }}.conf"
        dest: "/etc/nginx/sites-available/{{ site_name }}.conf"
```

En este caso, las variables `web_package` y `site_name` son definidas en el playbook y luego utilizadas en las tareas, lo que hace que sea más fácil cambiar la configuración sin tener que modificar cada tarea individualmente.

### Conclusión

Los **playbooks de Ansible** son fundamentales para automatizar la configuración de sistemas de forma eficiente y consistente. A través de tareas definidas en YAML, los administradores pueden controlar la configuración de múltiples sistemas de manera centralizada y en paralelo, lo que facilita la gestión de infraestructuras grandes o dinámicas. Los playbooks son idempotentes, lo que asegura que las tareas se realicen solo cuando sea necesario, evitando configuraciones erróneas por ejecuciones repetidas.