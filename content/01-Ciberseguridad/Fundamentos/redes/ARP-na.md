---
title: "Arp Na"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - redes
---
El comando **`arp -na`** es una variación del comando `arp` en sistemas Linux y otros sistemas operativos Unix-like. La opción **`-n`** en `arp` hace que las direcciones IP se muestren en formato numérico, es decir, sin intentar resolver o traducir las direcciones IP a nombres de host. Esto es útil si quieres ver las direcciones IP en formato de número sin que el sistema intente hacer una consulta DNS para resolver el nombre de la máquina correspondiente a esa IP.

La opción **`-a`**, por otro lado, muestra todas las entradas de la tabla ARP, tanto dinámicas como estáticas, de todas las interfaces de red de tu sistema.

### Explicación del comando


> **Relacionado**: [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]]. [[01-Ciberseguridad/Comunicaciones-Seguras/2024-12-19-REDES-WIFI|2024 12 19 REDES WIFI]].

```bash
arp -na
```

- **`-n`**: Muestra las direcciones IP en formato numérico (sin intentar resolver los nombres de host).
- **`-a`**: Muestra todas las entradas ARP (por lo general, en todas las interfaces de red).

### ¿Qué hace este comando?

Cuando ejecutas **`arp -na`**, obtendrás una lista de todas las entradas de la **tabla ARP** de tu sistema, mostrando las direcciones IP en formato numérico y las direcciones MAC correspondientes, sin tratar de resolver nombres de host. Esto te proporciona una vista rápida de todas las direcciones IP y sus direcciones MAC asociadas, que tu sistema ha aprendido en la red local.

### Ejemplo de salida

El comando **`arp -na`** podría generar una salida similar a esta:

```
? (192.168.1.1) at 00:14:22:01:23:45 [ether] on eth0
? (192.168.1.100) at 00:11:22:33:44:55 [ether] on eth0
? (192.168.1.101) at 00:11:22:33:44:56 [ether] on eth0
```

En este ejemplo:
- **`192.168.1.1`**, **`192.168.1.100`** y **`192.168.1.101`** son las direcciones IP en formato numérico.
- **`00:14:22:01:23:45`**, **`00:11:22:33:44:55`** y **`00:11:22:33:44:56`** son las direcciones MAC correspondientes.
- **`[ether]`** indica que las direcciones son para redes Ethernet.
- **`on eth0`** muestra que estas entradas se han aprendido a través de la interfaz de red **`eth0`**.

### ¿Cuándo usar `arp -na`?

Este comando es útil cuando:
1. Quieres obtener una lista rápida de todas las direcciones IP y MAC en tu red local.
2. Necesitas verificar las direcciones IP de los dispositivos que tu sistema ha encontrado en la red.
3. No te interesa obtener nombres de host, sino solo las direcciones IP y MAC numéricas.

### Resumen

El comando **`arp -na`** muestra todas las entradas de la tabla ARP de tu sistema, con las direcciones IP en formato numérico, sin intentar resolver los nombres de host, y las direcciones MAC correspondientes, lo que te permite ver cómo están mapeadas las IP a las MAC en tu red local.