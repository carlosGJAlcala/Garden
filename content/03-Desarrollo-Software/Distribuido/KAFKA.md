---
title: "Apache Kafka"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
---

# Apache Kafka

> **Relacionado**: Ver [[Microservicios]] para arquitectura. [[SOA]] para comparación. [[02-Ciencias-Computacion/Redes/Kafka|Kafka en redes]]. [[03-Desarrollo-Software/Concurrencia/CONCEPTOS-SOBRE-PROGRAMACION-CONCURRENTE|Concurrencia]] para fundamentos.

## **1. Qué es Apache Kafka**

Apache Kafka es una **plataforma distribuida de mensajería y streaming** que implementa un modelo **publicador–suscriptor** (_pub/sub_) y almacenamiento distribuido de mensajes.  
Está diseñada para manejar **altos volúmenes de datos** con baja latencia y tolerancia a fallos.

---

## **2. Rol en programación distribuida**

Kafka encaja perfectamente en el modelo de **paso de mensajes asíncrono**:

- **Productores** (_producers_) publican mensajes en **tópicos**.
    
- **Consumidores** (_consumers_) se suscriben a tópicos y procesan mensajes a su ritmo.
    
- Los mensajes se almacenan de forma **persistente** y replicada entre múltiples **brokers** (nodos de Kafka).
    
- No hay acoplamiento directo entre productores y consumidores → **desacoplamiento temporal y espacial**.
    

---

## **3. Componentes clave**

- **Broker** → nodo del clúster Kafka que almacena y sirve mensajes.
    
- **Topic** → canal lógico de comunicación, dividido en **particiones**.
    
- **Partición** → unidad de almacenamiento/consumo; los mensajes tienen un **offset**.
    
- **ZooKeeper** (en versiones antiguas) → coordinaba el clúster, ahora reemplazado por KRaft en versiones recientes.
    
- **Producer API** → para enviar mensajes.
    
- **Consumer API** → para leer mensajes.
    
- **Kafka Connect** → framework para integrar Kafka con sistemas externos (BD, sistemas de ficheros, etc.).
    
- **Kafka Streams** → librería para procesar datos directamente desde tópicos.
    

---

## **4. Funcionamiento distribuido**

- Cada **partición** se replica en varios brokers (configurable) para **alta disponibilidad**.
    
- Un **líder** por partición recibe escrituras y réplicas (**followers**) mantienen copias.
    
- Los **consumidores** se agrupan en _consumer groups_, y Kafka reparte las particiones entre ellos para **procesamiento paralelo**.
    
- La comunicación es siempre **binaria sobre TCP**, usando un protocolo propio de Kafka.
    

---

## **5. Ejemplo simple de uso**

### Productor:

```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

Producer<String, String> producer = new KafkaProducer<>(props);
producer.send(new ProducerRecord<>("mi-topico", "clave1", "mensaje de prueba"));
producer.close();
```

### Consumidor:

```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "grupo1");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList("mi-topico"));

while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        System.out.printf("offset = %d, clave = %s, valor = %s%n",
                          record.offset(), record.key(), record.value());
    }
}
```

---

## **6. Relación con la teoría**

- **Paso de mensajes asíncrono**: productores no esperan a que los consumidores reciban el mensaje.
    
- **Canal tipado**: cada tópico tiene un tipo de datos esperado (normalmente definido por un esquema: Avro, JSON Schema, Protobuf).
    
- **Escalabilidad horizontal**: más particiones → más consumidores en paralelo.
    
- **Tolerancia a fallos**: replicación y _failover_ automático.
    
- **Persistencia**: mensajes almacenados en disco durante un período configurado, independientemente de si se consumen.
    

---

## **7. Casos de uso**

- Integración de microservicios.
    
- Procesamiento de eventos en tiempo real.
    
- Pipelines ETL distribuidos.
    
- IoT (ingestión masiva de datos de sensores).
    
- Sistemas de _logging_ centralizado.
    
