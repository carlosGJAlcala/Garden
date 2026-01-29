---
title: "Logstash"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---
**Logstash** es una herramienta de **procesamiento de datos en tiempo real** que forma parte del **Elastic Stack** (antes conocido como ELK Stack: **Elasticsearch**, **Logstash** y **Kibana**). Su función principal es **recoger datos desde múltiples fuentes**, **procesarlos** o transformarlos, y **enviarlos a un destino**, comúnmente **Elasticsearch**.

---

### ¿Qué hace Logstash?


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Distribuido/KAFKA|KAFKA]]. [[02-Ciencias-Computacion/Redes/Kafka|Kafka]]. [[02-Ciencias-Computacion/Redes/Kibana|Kibana]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

**Logstash** actúa como una **tubería (pipeline)** de datos compuesta por tres etapas:

1. **Input**: recibe datos desde archivos, sockets, APIs, bases de datos, Kafka, Beats, syslog, etc.
    
2. **Filter**: transforma, limpia, interpreta, estructura o enriquece los datos. Aquí se pueden usar filtros como:
    
    - `grok`: para analizar logs no estructurados.
        
    - `mutate`: para renombrar, convertir, borrar o modificar campos.
        
    - `date`: para interpretar timestamps.
        
    - `geoip`: para añadir ubicación a IPs.
        
3. **Output**: envía los datos procesados a destinos como Elasticsearch, Kafka, otro archivo, stdout (terminal), etc.
    

---

### Ejemplo básico de configuración

Archivo: `/etc/logstash/conf.d/apache.conf`

```plaintext
input {
  file {
    path => "/var/log/apache2/access.log"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
  date {
    match => [ "timestamp", "dd/MMM/yyyy:HH:mm:ss Z" ]
  }
}

output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "apache-logs-%{+YYYY.MM.dd}"
  }
}
```

Esto toma logs de Apache, los interpreta con `grok`, ajusta su fecha, y los envía a Elasticsearch en un índice por día.

---

### Casos de uso típicos

- **Análisis de logs**: recolectar y estructurar logs de servidores, aplicaciones, contenedores, etc.
    
- **Seguridad**: análisis de eventos para SIEM.
    
- **Métricas e IoT**: recolección y limpieza de datos de sensores o dispositivos.
    
- **Flujos Kafka**: recibir eventos desde Kafka, transformarlos y reenviarlos.
    

---

###  Integración en el Elastic Stack

- **Logstash**: procesa datos.
    
- **Elasticsearch**: los indexa y almacena.
    
- **Kibana**: los visualiza.
    

Muchos entornos también integran **Beats** (como Filebeat o Metricbeat), que recogen datos y los envían a **Logstash** (para procesarlos) o directamente a Elasticsearch.

---

###  Ventajas

- Modular: puedes combinar múltiples inputs, filtros y outputs.
    
- Potente: puede interpretar, enriquecer y transformar datos complejos.
    
- Escalable: se usa en entornos de alto volumen (por ejemplo, logs de toda una red corporativa).
    
- Comunidad: gran soporte y plugins oficiales.
    

---

###  Verifica Logstash

```bash
sudo systemctl status logstash
sudo tail -f /var/log/logstash/logstash-plain.log
```

---

###  Conclusión

**Logstash** es una herramienta clave para **centralizar, interpretar y canalizar datos** antes de almacenarlos o visualizarlos. Si tienes múltiples fuentes de datos, distintos formatos y necesitas estructurar todo antes de enviarlo a Elasticsearch o similar, **Logstash es la pieza intermedia ideal**.