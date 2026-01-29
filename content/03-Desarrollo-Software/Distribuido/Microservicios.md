---
title: "Microservicios"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
---
# Microservicios

> **Relacionado**: Ver [[SOA]] para arquitectura orientada a servicios. [[KAFKA]] para mensajería. [[GraphQL]] y REST para APIs. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]] para contenedores. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH2.0|OAuth 2.0]] para seguridad de APIs.

Vamos a verlo de forma clara y conectándolo con lo que ya sabes de **SOA**, **SAP PI** y la **programación distribuida**.

---

## **1. Qué son los microservicios**

Los **microservicios** son un estilo arquitectónico para sistemas distribuidos donde la aplicación se divide en **múltiples servicios pequeños, independientes y autónomos**, cada uno ejecutando una función de negocio específica y comunicándose con los demás mediante **interfaces ligeras** (normalmente APIs REST/JSON o mensajería).

---

## **2. Comparación rápida con SOA**

|Característica|SOA (ej. SAP PI)|Microservicios|
|---|---|---|
|**Tamaño de servicio**|Más grande, orientado a procesos o funciones amplias.|Muy pequeño, enfocado a una única responsabilidad.|
|**Middleware**|ESB central (ej. SAP PI) que orquesta y transforma.|No hay un único bus central, cada servicio gestiona su lógica.|
|**Comunicación**|SOAP, REST, JMS, protocolos diversos.|REST/JSON, gRPC, mensajería ligera (Kafka, RabbitMQ).|
|**Despliegue**|Integrado en plataforma central.|Independiente, con despliegue aislado por servicio (contenedores, Kubernetes).|
|**Escalado**|Escala toda la aplicación o el middleware.|Escala solo el microservicio que lo necesita.|

---

## **3. Características clave**

- **Independencia**: cada microservicio se puede desarrollar, desplegar y escalar por separado.
    
- **Comunicación distribuida**: mediante HTTP/REST, gRPC o mensajería asíncrona (Kafka, RabbitMQ).
    
- **Resiliencia**: un fallo en un microservicio no debe tumbar todo el sistema.
    
- **Poliglotismo**: cada servicio puede usar el lenguaje y la tecnología que prefiera, mientras respete la interfaz.
    
- **Automatización DevOps**: integración continua, despliegue continuo (CI/CD).
    

---

## **4. Ejemplo de microservicios**

En lugar de un SAP PI orquestando todo, podrías tener:

- **Servicio de Inventario** → expone `GET /stock/{producto}`.
    
- **Servicio de Pedidos** → expone `POST /pedido`.
    
- **Servicio de Facturación** → expone `POST /factura`.
    
- **Servicio de Notificaciones** → envía email/SMS.
    

Estos servicios se comunican entre sí vía API REST o mediante eventos publicados en Kafka.

---

## **5. Ventajas**

- Escalabilidad granular.
    
- Despliegue independiente.
    
- Mejor resiliencia y aislamiento de fallos.
    
- Adaptación rápida a cambios en partes específicas del negocio.
    

---

## **6. Retos y ciberseguridad**

En microservicios, la **superficie de ataque crece** porque:

- Hay más **endpoints expuestos** (cada servicio tiene su API).
    
- Hay más **tráfico interno** (service-to-service) que puede ser interceptado si no se protege.
    
- Es más fácil perder el control de autenticación/autorización si no hay **gobernanza central**.
    

**Controles típicos:**

- **Service mesh** (Istio, Linkerd) para cifrar tráfico interno (mTLS) y aplicar políticas.
    
- API Gateway (Kong, Apigee, NGINX) para controlar acceso externo.
    
- Escaneo de imágenes de contenedores y configuración segura en Kubernetes/Docker.
    
- Monitoreo y trazabilidad distribuida (OpenTelemetry, Jaeger).
    

---

## **7. Relación con SAP PI**

- SAP PI es más típico en **arquitecturas SOA tradicionales** con un bus central.
    
- Los microservicios evitan un bus central, pero **pueden integrarse con PI** si necesitas comunicar microservicios con sistemas SAP legacy.
    
- En entornos híbridos, PI puede actuar como **puente** entre microservicios y sistemas monolíticos.
    

---

Si quieres, puedo prepararte **un cuadro comparativo entre SOA, Microservicios y Event-Driven (Kafka)** para que veas claramente cuándo usar cada uno y cómo encajan en ciberseguridad.  
¿Quieres que lo haga?