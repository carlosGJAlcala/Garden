---
title: "Elk"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**ELK** es un acrónimo que se refiere a un conjunto de tres herramientas de código abierto que se utilizan comúnmente para la **recolección, análisis y visualización de datos**. ELK está compuesto por **Elasticsearch**, **Logstash** y **Kibana**, y a menudo se utiliza en arquitecturas de monitoreo, gestión de logs y análisis en tiempo real.

### 1. **Elasticsearch** (E)


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Kibana|Kibana]]. [[02-Ciencias-Computacion/Redes/Logstash|Logstash]].

- **Elasticsearch** es un motor de búsqueda y análisis distribuido, diseñado para manejar grandes volúmenes de datos de manera rápida y eficiente. Se utiliza para almacenar, buscar y analizar datos en tiempo real. Es la base de **ELK** y proporciona la capacidad de indexar y almacenar grandes cantidades de datos, facilitando búsquedas complejas y análisis en tiempo real.
    
- **Características**:
    
    - **Indexación y búsqueda rápida**: Elasticsearch permite realizar consultas de búsqueda complejas sobre grandes volúmenes de datos en milisegundos.
        
    - **Escalabilidad**: Elasticsearch es distribuido, lo que significa que puede escalar horizontalmente, añadiendo más nodos para manejar mayores volúmenes de datos.
        
    - **Agregación de datos**: Permite realizar operaciones de agregación sobre los datos, como promedios, sumas, cuentas, etc.
        
    - **Tolerancia a fallos**: Los datos se replican en varios nodos, lo que garantiza alta disponibilidad y resistencia ante fallos.
        

### 2. **Logstash** (L)

- **Logstash** es una herramienta de procesamiento y transformación de datos. Su principal función es la de **ingestar, transformar y enviar datos a Elasticsearch** o a otros destinos. Logstash permite recoger datos de varias fuentes (como logs de servidores, bases de datos, aplicaciones, etc.), procesarlos, y luego enviarlos a **Elasticsearch** para su almacenamiento y análisis.
    
- **Características**:
    
    - **Ingestión de datos**: Logstash puede recibir datos de una variedad de fuentes, como archivos de log, bases de datos, colas de mensajes, y otros sistemas de monitoreo.
        
    - **Transformación de datos**: Con **filter plugins**, Logstash puede transformar los datos antes de enviarlos a Elasticsearch. Por ejemplo, puede convertir los registros de texto en un formato estructurado, como JSON.
        
    - **Enriquecimiento de datos**: Logstash puede agregar información adicional a los datos antes de enviarlos a Elasticsearch, como la geolocalización de direcciones IP o la categorización de eventos.
        

### 3. **Kibana** (K)

- **Kibana** es una herramienta de visualización de datos que se conecta a **Elasticsearch** para mostrar de manera gráfica los datos almacenados y procesados. Kibana proporciona una interfaz web interactiva que permite crear dashboards, gráficos y visualizaciones de los datos, facilitando el análisis y la interpretación de los mismos.
    
- **Características**:
    
    - **Dashboards interactivos**: Kibana permite crear dashboards interactivos que pueden mostrar métricas en tiempo real, gráficos de barras, líneas, tortas, mapas de calor, entre otros.
        
    - **Búsqueda y filtrado de datos**: Kibana permite realizar búsquedas complejas y aplicar filtros para analizar datos de manera más detallada.
        
    - **Alertas**: Puedes configurar alertas en Kibana que se disparan cuando los datos alcanzan ciertos umbrales, lo que es útil para monitoreo y notificación en tiempo real.
        

### ¿Por qué se dice que es "Elástica"?

Cuando se dice que **ELK es "elástica"**, se hace referencia a la capacidad de **Elasticsearch** para escalar de manera **elástica**. Esto significa que el sistema puede adaptarse de manera eficiente a cambios en la carga de trabajo, aumentando o disminuyendo recursos según sea necesario, sin afectar el rendimiento. Esto se logra por:

1. **Escalabilidad Horizontal**:
    
    - **Elasticsearch** es un sistema distribuido que permite añadir nodos adicionales para **ampliar la capacidad de procesamiento y almacenamiento**. Cuando se necesita manejar más datos o realizar más consultas, se pueden agregar más nodos al clúster de Elasticsearch. La información se divide en **shards** (fragmentos), y cada shard se puede replicar en varios nodos para mejorar la **disponibilidad** y **reducción de fallos**.
        
2. **Automatización de la Gestión de Clústeres**:
    
    - Elasticsearch automáticamente **distribuye los datos** entre nodos y realiza **equilibrio de carga**. Si un nodo falla, los datos y las solicitudes se reconfiguran dinámicamente sin interrupciones.
        
3. **Alta Disponibilidad**:
    
    - Gracias a la **replicación** de los datos entre nodos, si un nodo se cae, otro nodo replica los datos, lo que garantiza que el sistema siga funcionando incluso en caso de fallos de hardware.
        
4. **Elasticidad en la Administración de Recursos**:
    
    - **Kibana** y **Logstash**, aunque no tan distribuidos como Elasticsearch, pueden aprovechar la elasticidad de **Elasticsearch**. Esto significa que la infraestructura general que administra el análisis de logs y métricas puede escalar sin problemas.
        

### Casos de Uso de ELK

1. **Monitoreo de Logs**:
    
    - ELK es muy popular en el análisis y visualización de **logs de aplicaciones**, **servidores web**, **bases de datos**, y **sistemas operativos**. Los logs se procesan con **Logstash**, se almacenan en **Elasticsearch**, y luego se visualizan con **Kibana** para detectar errores, alertas y patrones.
        
2. **Monitoreo de Infraestructura y Aplicaciones**:
    
    - A través de la recopilación de métricas de sistemas y aplicaciones, ELK permite monitorear la **salud** y el **rendimiento** de infraestructuras TI en tiempo real. Por ejemplo, se pueden visualizar métricas como uso de CPU, memoria, tráfico de red y más, todo a través de los dashboards de Kibana.
        
3. **Análisis de Datos en Tiempo Real**:
    
    - ELK es ideal para sistemas que requieren procesamiento de **eventos en tiempo real**, como aplicaciones de IoT o análisis de datos financieros. Los eventos y métricas se almacenan en **Elasticsearch** y se visualizan en tiempo real en **Kibana**.
        
4. **Seguridad y Cumplimiento**:
    
    - ELK se usa en soluciones **SIEM** (Security Information and Event Management) para analizar los logs de seguridad y detectar patrones anómalos, como intentos de acceso no autorizados o ataques DDoS (Distributed Denial of Service). Kibana se utiliza para crear alertas y realizar auditorías de seguridad.
        
5. **Análisis de Datos de Series Temporales**:
    
    - ELK, especialmente **Elasticsearch**, es una herramienta poderosa para analizar **datos de series temporales**. Esto se aplica a aplicaciones como monitoreo de infraestructuras, análisis financiero y más.
        

### Arquitectura de ELK

La arquitectura de **ELK** se compone de tres componentes principales:

1. **Logstash** (Ingesta y procesamiento de datos).
    
2. **Elasticsearch** (Almacenamiento y análisis de datos).
    
3. **Kibana** (Visualización y análisis de datos).
    

Estos componentes están diseñados para trabajar juntos de manera eficiente y escalable, lo que permite a las organizaciones recolectar, procesar, almacenar, y visualizar grandes volúmenes de datos en tiempo real.

### Integración de ELK con Otros Sistemas

- **Beats**: Son agentes ligeros que recopilan datos de máquinas y aplicaciones y los envían a **Elasticsearch** o a **Logstash** para su procesamiento.
    
- **Filebeat**: Agente para recopilar y enviar logs de archivos a **Elasticsearch** o **Logstash**.
    
- **Metricbeat**: Recopila métricas del sistema (como uso de CPU, memoria, etc.) y las envía a **Elasticsearch**.
    
- **Heartbeat**: Para monitorear la disponibilidad de servicios.
    

### Conclusión

**ELK** (Elasticsearch, Logstash, Kibana) es una poderosa plataforma para el procesamiento, almacenamiento, y visualización de grandes volúmenes de datos en tiempo real. La elasticidad de Elasticsearch es clave en la capacidad de ELK para manejar la carga de trabajo de manera eficiente y escalar según las necesidades. Con su capacidad para indexar, buscar y visualizar datos rápidamente, ELK es ampliamente utilizado para el análisis de logs, métricas de infraestructura, seguridad y más.