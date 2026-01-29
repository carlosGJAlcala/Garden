---
title: "Configuracion Router"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
Aquí tienes un ejemplo básico de cómo configurar un **router** utilizando la **interfaz de línea de comandos (CLI)**, como en el caso de un dispositivo Cisco. Este ejemplo muestra los pasos fundamentales para configurar una interfaz de red, asignar una dirección IP y habilitar la interfaz para que funcione en una red.

### **Ejemplo de configuración de un router con CLI**


> **Relacionado**: [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

#### 1. **Acceder al router**

Primero, debes acceder al router a través de la **CLI**. Esto generalmente se hace mediante una consola física o de forma remota (SSH o Telnet). Una vez que accedas, verás el prompt del router, como este:

```bash
Router>
```

Para comenzar a configurar el router, necesitas ingresar al **modo privilegiado**:

```bash
Router> enable
Router#
```

#### 2. **Entrar al modo de configuración global**

Para realizar cambios en la configuración del router, debes ingresar al **modo de configuración global**:

```bash
Router# configure terminal
Router(config)#
```

#### 3. **Configurar una interfaz de red**

Imagina que necesitas configurar una interfaz de red Ethernet (por ejemplo, `FastEthernet0/1`). Para ello, sigue estos pasos:

```bash
Router(config)# interface FastEthernet0/1
Router(config-if)#
```

En este modo, puedes configurar diversas opciones para la interfaz seleccionada. Por ejemplo, **asignar una dirección IP** y **habilitarla**.

#### 4. **Asignar una dirección IP y máscara de subred**

En el modo de configuración de la interfaz (`config-if`), asigna la dirección IP y la máscara de subred para la interfaz:

```bash
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)#
```

- **192.168.1.1** es la dirección IP que se asigna a la interfaz.
    
- **255.255.255.0** es la máscara de subred.
    

#### 5. **Habilitar la interfaz**

Por defecto, las interfaces en los routers de Cisco pueden estar deshabilitadas. Para habilitarla, usa el siguiente comando:

```bash
Router(config-if)# no shutdown
Router(config-if)#
```

Este comando activa la interfaz de red **FastEthernet0/1**.

#### 6. **Configurar una ruta estática (opcional)**

Si deseas configurar una **ruta estática** para que el router pueda alcanzar otras redes, puedes hacerlo con el siguiente comando. Supongamos que quieres enviar el tráfico a una red **192.168.2.0/24** a través de un router de siguiente salto (puerta de enlace) con la dirección IP **192.168.1.254**.

```bash
Router(config)# ip route 192.168.2.0 255.255.255.0 192.168.1.254
Router(config)#
```

Este comando le indica al router cómo alcanzar la red **192.168.2.0/24** a través de la puerta de enlace **192.168.1.254**.

#### 7. **Guardar la configuración**

Una vez que hayas terminado de configurar el router, es crucial **guardar los cambios** para que no se pierdan al reiniciar el dispositivo:

```bash
Router(config)# exit
Router# write memory
```

O alternativamente:

```bash
Router# copy running-config startup-config
```

Este comando guarda la configuración actual (`running-config`) en la configuración de inicio (`startup-config`), lo que asegura que los cambios se mantendrán después de un reinicio.

#### 8. **Verificar la configuración**

Puedes verificar que la interfaz esté correctamente configurada y funcionando con el siguiente comando:

```bash
Router# show ip interface brief
```

Este comando te mostrará un resumen de las interfaces del router y su estado (si están habilitadas o no, la IP asignada, etc.).

Ejemplo de salida:

```bash
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
FastEthernet0/1        192.168.1.1     YES manual up                    up
```

---

### **Resumen de Comandos**

Aquí tienes un resumen de los comandos clave utilizados en este ejemplo de configuración de un router:

1. **Acceder al modo privilegiado**:
    
    ```bash
    enable
    ```
    
2. **Entrar al modo de configuración global**:
    
    ```bash
    configure terminal
    ```
    
3. **Seleccionar la interfaz de red**:
    
    ```bash
    interface FastEthernet0/1
    ```
    
4. **Asignar la dirección IP y máscara de subred**:
    
    ```bash
    ip address 192.168.1.1 255.255.255.0
    ```
    
5. **Habilitar la interfaz**:
    
    ```bash
    no shutdown
    ```
    
6. **Configurar una ruta estática**:
    
    ```bash
    ip route 192.168.2.0 255.255.255.0 192.168.1.254
    ```
    
7. **Guardar la configuración**:
    
    ```bash
    write memory
    ```
    
8. **Verificar la configuración**:
    
    ```bash
    show ip interface brief
    ```
    

### **Conclusión**

La **configuración de un router con CLI** es una habilidad fundamental para cualquier administrador de red. Usando comandos simples, puedes asignar direcciones IP, configurar rutas, y activar interfaces para asegurar que la red funcione correctamente. La **CLI** proporciona un control total sobre el dispositivo, permitiendo configuraciones detalladas que no siempre están disponibles a través de interfaces gráficas.