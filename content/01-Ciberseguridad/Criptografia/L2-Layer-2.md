---
title: "L2 Layer 2"
date: 2026-01-26
tags:
  - ciberseguridad
  - criptografia
---
Perfecto, vamos a expandirlo en ambos sentidos: **criptografía pura** y **blockchain**, porque aunque se usan en contextos distintos, se relacionan.

---

### 1. **En criptografía pura (teoría de seguridad en capas)**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]].

Cuando hablamos de **L2 (Layer 2)** en un sentido general dentro de criptografía, se refiere a un **nivel adicional de seguridad o abstracción** que se coloca sobre la capa base.

- La **L1** es el nivel fundamental: algoritmos básicos de cifrado, hash o firma digital.
    
- La **L2** añade una segunda capa que encapsula, optimiza o asegura aún más los datos.
    

Ejemplo:

- **L1:** AES (cifrado simétrico).
    
- **L2:** TLS/SSL, que usa AES junto con firmas y hashes para garantizar confidencialidad, integridad y autenticidad.
    

En otras palabras, en criptografía clásica “L2” no es un estándar fijo, sino una forma de hablar de **seguridad multicapa**. Cada capa se apoya en la anterior: la de más bajo nivel ofrece primitivas, la de más alto integra esas primitivas en protocolos seguros.

---

### 2. **En blockchain (uso más común de L2)**

Aquí el término **Layer 2** está mucho más definido. Se trata de protocolos que **se construyen sobre una blockchain principal (L1)** para resolver el famoso _trilema de blockchain_:

- **Seguridad** (no se puede comprometer la solidez de la red).
    
- **Descentralización** (que no dependa de unos pocos nodos).
    
- **Escalabilidad** (poder manejar millones de transacciones).
    

La capa 1 como Ethereum es segura y descentralizada, pero poco escalable. Ahí entra la L2.

**Mecanismos de L2 más importantes:**

- **State channels:** los usuarios abren un canal en la L1, transaccionan infinitas veces “off-chain”, y solo cierran el resultado en la L1. Ejemplo: Lightning Network (Bitcoin).
    
- **Rollups:** agrupan miles de transacciones fuera de la L1 y publican una única prueba en ella.
    
    - _Optimistic Rollups:_ suponen que las transacciones son válidas y solo se corrigen si alguien demuestra lo contrario. Ejemplo: Arbitrum, Optimism.
        
    - _zk-Rollups:_ usan **pruebas de conocimiento cero** (zk-SNARKs o zk-STARKs) para demostrar que el lote de transacciones es válido sin mostrar cada transacción. Ejemplo: zkSync, StarkNet.
        
- **Sidechains:** cadenas paralelas que procesan operaciones a gran velocidad y luego sincronizan con la L1. Ejemplo: Polygon PoS.
    

---

### 3. **Analogía práctica**

Piensa en una **carretera principal (L1)**: ancha, segura, con peajes caros. Todos los coches pasan por ahí.  
Una **L2** sería una autopista secundaria rápida y barata, que cada cierto tiempo envía un informe a la principal para que quede registrado oficialmente.

---

### 4. **Ejemplo en la práctica**

- En Ethereum L1, una transferencia puede costar 5–20 USD en comisiones.
    
- En zkSync (L2), la misma transacción cuesta céntimos y queda registrada en segundos.
    
- Pero al final, zkSync publica en Ethereum una **prueba criptográfica** que garantiza que todo lo que pasó en la L2 es válido.
    

---

 Resumen:

- **En criptografía:** L2 significa “segunda capa de seguridad/protocolo” construida sobre primitivas básicas.
    
- **En blockchain:** L2 son soluciones que heredan la seguridad de la capa 1, pero procesan transacciones fuera de ella para mejorar escalabilidad y costo.
    

---

¿Quieres que te prepare una explicación enfocada en **zk-STARKs y tu TFM** (cómo se aplican en L2 y autenticación), o prefieres algo más **general de seguridad multicapa** para entender la idea de L2 en cualquier contexto criptográfico?