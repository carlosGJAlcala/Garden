---
title: "Paso 1: Añadir el repositorio de InfluxData (si no lo tienes ya)"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**Telegraf** es un agente de recolección de métricas de código abierto que es parte de la **Elastic Stack** (ahora más comúnmente conocido como **TICK Stack**, que incluye **Telegraf**, **InfluxDB**, **Chronograf** y **Kapacitor**). Su propósito principal es recopilar métricas de sistemas, aplicaciones y servicios y enviarlas a una base de datos, como **InfluxDB**, o a otras plataformas de almacenamiento y análisis de datos.

Telegraf se caracteriza por su capacidad de manejar **métricas en tiempo real**, ser altamente **configurable**, y su bajo impacto en los recursos del sistema, lo que lo hace ideal para infraestructuras grandes y dinámicas.

### Características Principales de Telegraf


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[02-Ciencias-Computacion/Redes/Grafana|Grafana]]. [[02-Ciencias-Computacion/Redes/InfluxDB|InfluxDB]].

1. **Recolección de Métricas**:
    
    - Telegraf se utiliza para **recolectar métricas** de una amplia gama de sistemas y servicios, como uso de CPU, memoria, almacenamiento, tráfico de red, y más.
        
    - Puede obtener métricas de sistemas locales (por ejemplo, **Linux**, **Windows**), aplicaciones (por ejemplo, **MySQL**, **Redis**, **Apache**), y también de servicios en la nube (como **AWS**, **Azure**, **Google Cloud**).
        
2. **Soporte de Plugins**:
    
    - **Telegraf** es muy flexible y se extiende mediante **plugins**. Existen más de 200 plugins disponibles que permiten recopilar métricas de diferentes fuentes, tales como:
        
        - **System**: Métricas del sistema operativo, como uso de CPU, memoria, y disco.
            
        - **Inputs**: Plugins para recolectar métricas de bases de datos, servidores web, y aplicaciones (por ejemplo, **Prometheus**, **SNMP**, **Kafka**, **Nginx**).
            
        - **Outputs**: Plugins para enviar los datos a diversos destinos, como **InfluxDB**, **Kafka**, **Graphite**, entre otros.
            
        - **Processors**: Plugins para procesar y transformar los datos recolectados.
            
        - **Aggregators**: Plugins para realizar agregaciones de datos, como promedios, sumas, etc.
            
3. **Bajo Consumo de Recursos**:
    
    - Telegraf está diseñado para ser ligero y eficiente, con bajo impacto en los recursos del sistema. Es ideal para su implementación en **entornos de producción** y en **infraestructuras grandes** que requieren la recolección de métricas sin consumir recursos excesivos.
        
4. **Configuración Sencilla**:
    
    - Telegraf es fácil de configurar mediante un archivo de configuración en formato **TOML**. La configuración de **plugins** se puede realizar de manera simple, especificando los **inputs**, **outputs**, **procesadores** y **agregadores** que deseas utilizar.
        
5. **Recolección de Datos en Tiempo Real**:
    
    - Telegraf está diseñado para recolectar métricas **en tiempo real** y transmitirlas a plataformas de almacenamiento o análisis como **InfluxDB**. Su enfoque eficiente le permite recolectar métricas sin una carga considerable en el rendimiento del sistema.
        

### Casos de Uso Comunes de Telegraf

1. **Monitoreo de Infraestructura**:
    
    - Telegraf es comúnmente usado para **monitorear servidores** y **sistemas** en tiempo real, recolectando métricas como uso de CPU, uso de memoria, carga de disco, tráfico de red, etc. Estas métricas se envían luego a una base de datos como **InfluxDB** o **Prometheus**, donde pueden ser visualizadas en **Grafana**.
        
2. **Monitoreo de Aplicaciones**:
    
    - Telegraf se puede usar para obtener métricas de aplicaciones específicas como bases de datos, servidores web, y servicios en la nube. Por ejemplo, puedes configurar Telegraf para recolectar métricas de un servidor **MySQL** o de un servicio **Nginx**.
        
3. **Recolección de Datos en IoT**:
    
    - En aplicaciones de **Internet de las Cosas (IoT)**, Telegraf es ideal para recolectar datos de sensores y dispositivos IoT, enviándolos a una base de datos como **InfluxDB** para análisis y visualización en tiempo real.
        
4. **Monitoreo de Sistemas en la Nube**:
    
    - Telegraf también se utiliza para recolectar métricas de **servicios en la nube** como **AWS**, **Google Cloud** o **Azure**. Esto permite monitorear los recursos y servicios que se ejecutan en plataformas de nube.
        

### Instalación de Telegraf

Aquí te dejo un ejemplo de cómo instalar **Telegraf** en un sistema basado en **Ubuntu**.

#### Paso 1: Añadir el repositorio de Telegraf

```bash
sudo apt-get update
sudo apt-get install -y software-properties-common
sudo add-apt-repository ppa:influxdata/influxdb
```

#### Paso 2: Instalar Telegraf

```bash
sudo apt-get update
sudo apt-get install telegraf
```

#### Paso 3: Iniciar y habilitar el servicio Telegraf

```bash
sudo systemctl start telegraf
sudo systemctl enable telegraf
```

#### Paso 4: Configuración de Telegraf

El archivo de configuración de **Telegraf** se encuentra en `/etc/telegraf/telegraf.conf`. Puedes editar este archivo para ajustar las fuentes de datos (inputs), destinos (outputs), y cualquier otro parámetro.

```bash
sudo nano /etc/telegraf/telegraf.conf
```

### Configuración Básica de Telegraf

Telegraf se configura principalmente a través de su archivo de configuración (`telegraf.conf`). Este archivo está dividido en secciones que definen:

- **Inputs**: Especifica las fuentes de datos de donde Telegraf recolectará las métricas. Ejemplos incluyen:
    
    - `cpu` para recolectar métricas de la CPU.
        
    - `mem` para recolectar métricas de memoria.
        
    - `net` para recolectar métricas de red.
        
    
    Ejemplo de configuración de inputs:
    
    ```toml
    [[inputs.cpu]]
      percpu = true
      totalcpu = true
      fielddrop = ["time_*"]
    ```
    
- **Outputs**: Define a dónde se enviarán los datos recolectados. El destino más común es **InfluxDB**, pero también puede configurarse para otros destinos como **Kafka**, **Graphite**, etc.
    
    Ejemplo de configuración de outputs:
    
    ```toml
    [[outputs.influxdb]]
      urls = ["http://localhost:8086"]
      database = "telegraf"
      retention_policy = ""
      write_consistency = "any"
    ```
    
- **Processors**: Puedes utilizar procesadores para transformar o modificar los datos antes de que se envíen al destino.
    
    Ejemplo de configuración de un processor:
    
    ```toml
    [[processors.rename]]
      [processors.rename.replace]
        measurement = "cpu_usage"
        field = "value"
    ```
    
- **Aggregators**: Permiten la agregación de métricas, por ejemplo, para obtener promedios, sumas, máximos, etc.
    
    Ejemplo de configuración de un aggregator:
    
    ```toml
    [[aggregators.min]]
      interval = "10s"
    ```
    

### Ejemplo de Uso de Telegraf con InfluxDB y Grafana

En un escenario típico donde se usa **Telegraf** junto con **InfluxDB** y **Grafana**:

1. **Telegraf** recolecta métricas del sistema (por ejemplo, uso de CPU, memoria, red).
    
2. Estas métricas se envían a **InfluxDB**, que las almacena en una base de datos de series temporales.
    
3. **Grafana** se conecta a **InfluxDB** como fuente de datos y crea dashboards para visualizar las métricas recolectadas.
    
4. Las alertas se configuran en **Grafana** basadas en las métricas de **InfluxDB**.
    

**Telegraf** es un agente de recolección de métricas que se utiliza para obtener datos de diversos sistemas y aplicaciones, y enviarlos a plataformas de almacenamiento como **InfluxDB**, **Prometheus**, o **Kafka**, entre otros. Está diseñado para ser ligero, eficiente y flexible, soportando una gran variedad de **plugins de entrada (inputs)** para recolectar métricas y **plugins de salida (outputs)** para enviarlas a diferentes destinos.

### ¿Cómo se usa Telegraf?

Telegraf se configura a través de un archivo de configuración, generalmente en formato **TOML** (`/etc/telegraf/telegraf.conf`), donde puedes definir los **inputs**, **outputs**, **processors**, y **aggregators**. A continuación, te explico cómo usar **Telegraf** en un escenario común de monitoreo de infraestructura.

### Pasos para Usar Telegraf

#### 1. **Instalación de Telegraf**

En una máquina basada en **Ubuntu**, puedes instalar **Telegraf** utilizando los siguientes pasos:

```bash
# Paso 1: Añadir el repositorio de InfluxData (si no lo tienes ya)
wget -qO- https://repos.influxdata.com/influxdb.key | sudo apt-key add -

# Paso 2: Añadir el repositorio de InfluxDB a las fuentes de apt
echo "deb https://repos.influxdata.com/ubuntu focal stable" | sudo tee /etc/apt/sources.list.d/influxdata.list

# Paso 3: Actualizar el índice de paquetes
sudo apt-get update

# Paso 4: Instalar Telegraf
sudo apt-get install telegraf
```

#### 2. **Configuración de Telegraf**

El archivo de configuración de **Telegraf** se encuentra en `/etc/telegraf/telegraf.conf`. Aquí se definen las fuentes de datos (**inputs**), los destinos (**outputs**), y otras configuraciones de procesamiento y agregación.

##### Ejemplo de un archivo de configuración básico:

```toml
# Configuración de entrada: Recolecta datos de las métricas del sistema
[[inputs.cpu]]
  percpu = true
  totalcpu = true
  fielddrop = ["time_*"]

[[inputs.mem]]
  # Recolecta estadísticas de memoria

[[inputs.disk]]
  # Recolecta estadísticas de discos

[[inputs.net]]
  # Recolecta estadísticas de red

# Configuración de salida: Enviar datos a InfluxDB
[[outputs.influxdb]]
  urls = ["http://localhost:8086"]  # Dirección de InfluxDB
  database = "telegraf"  # Nombre de la base de datos donde se almacenarán las métricas
  retention_policy = ""
  write_consistency = "any"
  timeout = "5s"
```

##### Explicación de la configuración:

- **inputs**: Aquí defines los **plugins de entrada**, que son las fuentes de datos. En el ejemplo anterior, se están usando plugins para recolectar métricas de **CPU**, **memoria**, **discos** y **red**. Puedes añadir más plugins de entrada según el tipo de datos que deseas recolectar.
    
- **outputs**: En este caso, se está enviando las métricas recolectadas a **InfluxDB**. Puedes configurar otros destinos de salida como **Kafka**, **Prometheus**, o **Graphite**.
    

#### 3. **Iniciar el servicio de Telegraf**

Una vez configurado Telegraf, puedes **iniciar** el servicio con los siguientes comandos:

```bash
# Iniciar el servicio de Telegraf
sudo systemctl start telegraf

# Habilitar el servicio para que arranque automáticamente con el sistema
sudo systemctl enable telegraf

# Verificar el estado de Telegraf
sudo systemctl status telegraf
```

#### 4. **Verificar la Recolección de Métricas**

Puedes verificar que Telegraf esté recolectando y enviando datos correctamente mediante los siguientes comandos:

1. **Consultar las métricas en InfluxDB**:  
    Si configuraste Telegraf para enviar datos a **InfluxDB**, puedes usar la CLI de InfluxDB para verificar que los datos están siendo almacenados:
    
    ```bash
    influx
    SHOW DATABASES;  # Ver las bases de datos
    USE telegraf;    # Usar la base de datos telegraf
    SHOW MEASUREMENTS;  # Ver las métricas almacenadas
    ```
    
2. **Ver los logs de Telegraf**:  
    Puedes revisar los logs para verificar que no haya errores:
    
    ```bash
    sudo journalctl -u telegraf
    ```
    

#### 5. **Usar Telegraf con Grafana**

Una vez que **Telegraf** esté enviando métricas a **InfluxDB**, puedes integrar **InfluxDB** con **Grafana** para visualizar las métricas de manera gráfica.

1. **Conectar Grafana con InfluxDB**:
    
    - En **Grafana**, ve a la configuración de fuentes de datos y agrega **InfluxDB** como fuente de datos.
        
    - Ingresa la URL de tu servidor de **InfluxDB** y selecciona la base de datos (por ejemplo, `telegraf`).
        
2. **Crear Dashboards**:
    
    - Crea dashboards en **Grafana** donde puedas visualizar las métricas recolectadas, como el uso de la CPU, memoria, disco, etc.
        

#### 6. **Personalización de Telegraf**

Telegraf es altamente **personalizable** a través de sus plugins. A continuación te menciono algunos de los plugins más comunes que puedes configurar:

- **Plugins de Entrada**:
    
    - `inputs.cpu`: Métricas de la CPU.
        
    - `inputs.mem`: Métricas de memoria.
        
    - `inputs.disk`: Métricas de disco.
        
    - `inputs.net`: Métricas de red.
        
    - `inputs.http`: Para recolectar datos de una API HTTP.
        
    - `inputs.snmp`: Para recolectar métricas de dispositivos SNMP.
        
- **Plugins de Salida**:
    
    - `outputs.influxdb`: Para enviar datos a **InfluxDB**.
        
    - `outputs.kafka`: Para enviar datos a **Kafka**.
        
    - `outputs.prometheus`: Para enviar datos a **Prometheus**.
        

#### 7. **Configuración de Alertas en Telegraf**

Aunque **Telegraf** no tiene un sistema de alertas propio, puedes usar **InfluxDB** o **Grafana** para configurar alertas basadas en las métricas recolectadas por Telegraf. Por ejemplo, en **Grafana** puedes configurar alertas para recibir notificaciones si, por ejemplo, el uso de la CPU supera un umbral determinado.

### Ejemplo Completo de Uso de Telegraf

Aquí hay un ejemplo de cómo podrías usar Telegraf para monitorear el uso de la CPU y la memoria, y enviar estos datos a InfluxDB:

1. **Instalación y configuración básica de Telegraf**.
    
2. **Recolección de métricas de CPU y memoria** con los plugins `cpu` y `mem`.
    
3. **Envío de estas métricas a InfluxDB**.
    
4. **Visualización de las métricas en Grafana** para monitorear el rendimiento de tus sistemas.
    

### Conclusión

**Telegraf** es una herramienta ligera y flexible para la recolección de métricas, ideal para escenarios de monitoreo en tiempo real. Su facilidad de configuración y su capacidad de integrarse con plataformas como **InfluxDB** y **Grafana** lo convierten en una solución poderosa para monitorear y visualizar métricas de sistemas, aplicaciones y servicios.