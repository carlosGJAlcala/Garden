---
title: "Arp Spoofing"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---

El **ARP Spoofing** (o **ARP Poisoning**) es un ataque que explota vulnerabilidades del protocolo [[ARP. Address Resolution Protocol|ARP]] en el que un atacante envía mensajes ARP falsificados en una red local para asociar su propia dirección MAC con la dirección IP de otro dispositivo, como el router o la víctima, engañando a los dispositivos de la red para que redirijan el tráfico a través del atacante. Esto se utiliza, por ejemplo, para realizar ataques de **Man-in-the-Middle (MITM)**, donde el atacante puede interceptar, modificar o redirigir el tráfico de la víctima.

> **Ver también**: [[SSLTRIP]] para ataques MITM sobre HTTPS.

### Explicación detallada de los comandos


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]]. [[01-Ciberseguridad/Comunicaciones-Seguras/2024-12-19-REDES-WIFI|2024 12 19 REDES WIFI]]. [[01-Ciberseguridad/Comunicaciones-Seguras/La-Red-SARA|La Red SARA]].

Los comandos que mencionas son parte de un ataque de ARP Spoofing utilizando la herramienta **`arpspoof`**:

#### 1. **Envenenamiento de la tabla ARP en la víctima**:
   ```bash
   sudo arpspoof -t IP_víctima IP_router
   ```

   **¿Qué sucede aquí?**
   - **`-t IP_víctima`**: Esto especifica que el objetivo del ataque es la **IP de la víctima**.
   - **`IP_router`**: Esta es la dirección IP del **router** o puerta de enlace predeterminada, cuya dirección MAC debe ser asociada incorrectamente con la dirección MAC del atacante.

   Lo que ocurre cuando ejecutas este comando es que el atacante está enviando continuamente paquetes **ARP Reply** a la víctima, diciendo que la dirección MAC que corresponde a la IP del **router** (normalmente una IP estática) es en realidad la dirección MAC del **atacante**.

   - **Resultado**: La víctima actualiza su tabla ARP, asociando la dirección IP del router con la MAC del atacante. Ahora, cuando la víctima intente enviar paquetes a la puerta de enlace predeterminada (el router), esos paquetes serán enviados al atacante en lugar del router.

#### 2. **Envenenamiento de la tabla ARP en el router**:
   ```bash
   sudo arpspoof -t IP_router IP_victima
   ```

   **¿Qué sucede aquí?**
   - **`-t IP_router`**: El objetivo ahora es la **IP del router**.
   - **`IP_victima`**: Esta es la dirección IP de la víctima, cuya dirección MAC debe ser asociada incorrectamente con la dirección MAC del atacante.

   En este segundo comando, el atacante está enviando continuamente paquetes **ARP Reply** al router, indicando que la dirección MAC correspondiente a la **IP de la víctima** es en realidad la dirección MAC del atacante.

   - **Resultado**: El router actualiza su tabla ARP, asociando la dirección IP de la víctima con la dirección MAC del atacante. Ahora, cuando el router intente enviar paquetes a la víctima, esos paquetes serán enviados al atacante en lugar de a la víctima.

### ¿Por qué se hace esto de manera continua?

En redes locales, las tablas ARP de los dispositivos no son estáticas, sino que tienen un **tiempo de vida limitado** (TTL). Cada dispositivo de la red realiza consultas periódicas ARP para mantener actualizada su tabla ARP. Este comportamiento es natural para el funcionamiento del protocolo ARP.

- **El ciclo de consulta ARP**: Si un dispositivo necesita enviar un paquete a una IP específica, realiza una consulta ARP para saber qué dirección MAC corresponde a esa IP. El dispositivo que tiene esa IP responde con un **ARP Reply** que incluye su dirección MAC. 
- **Envenenamiento continuo**: En un ataque de ARP Spoofing, el atacante envía **continuamente ARP Replies falsificados** para sobrescribir las entradas en la tabla ARP de la víctima y del router. Esto se hace para asegurarse de que, aunque el router o la víctima realicen sus consultas ARP de forma periódica, las respuestas ARP del atacante continúen sobrescribiendo las respuestas legítimas.

### **Proceso completo del ataque ARP Spoofing**

1. **El atacante envía ARP Replies falsificados a la víctima**:
   - La víctima está configurada para enviar paquetes a su **router** (puerta de enlace predeterminada). El atacante le dice que la IP del **router** corresponde a su propia dirección MAC. La víctima ahora enviará el tráfico destinado al router al atacante.

2. **El atacante envía ARP Replies falsificados al router**:
   - Al mismo tiempo, el atacante también envía ARP Replies falsificados al router, diciéndole que la IP de la **víctima** corresponde a su propia dirección MAC. El router, ahora engañado, enviará los paquetes destinados a la víctima al atacante.

3. **Resultado**: El tráfico entre la víctima y el router ahora pasa por el atacante, que puede interceptarlo, modificarlo o incluso redirigirlo.

### **¿Qué es lo que permite al atacante controlar el tráfico?**

- **Envenenamiento de la tabla ARP**: Al sobrescribir continuamente las entradas en las tablas ARP de ambos dispositivos (víctima y router), el atacante consigue controlar cómo se enruta el tráfico. La víctima y el router ahora creen que la dirección MAC del atacante es la dirección MAC del otro dispositivo.
  
- **El flujo de tráfico**: El atacante se convierte en el "hombre en el medio" (MITM). Todos los paquetes destinados al router desde la víctima y viceversa pasan por el atacante, quien puede modificarlos o redirigirlos a otros destinos.

### ¿Cómo funciona ARP Spoofing de forma continua?

- **El protocolo ARP es un protocolo sin autenticación**: ARP no tiene ningún mecanismo para verificar si una respuesta ARP es auténtica o no. Cualquier dispositivo en la red puede enviar un mensaje ARP diciendo que tiene la dirección MAC correspondiente a una determinada dirección IP.
  
- **Ciclo de ARP**: La víctima y el router realizan consultas ARP periódicas para mantener actualizadas sus tablas ARP. Esto es lo que permite al atacante seguir enviando respuestas ARP falsificadas y mantener el envenenamiento de las tablas.

- **Ataque persistente**: Debido a que las entradas ARP tienen un tiempo de vida limitado (TTL) y se actualizan periódicamente, el atacante debe continuar enviando respuestas ARP falsas de manera continua para asegurar que las tablas ARP de la víctima y del router sigan apuntando a la dirección MAC del atacante.

### Herramientas para detectar y mitigar ARP Spoofing

- **Herramientas de monitoreo ARP**: Herramientas como **`arpwatch`** permiten detectar cambios inusuales en las tablas ARP, lo que podría indicar un ataque de ARP Spoofing.
  
- **Uso de ARP estático**: Una forma de mitigar este tipo de ataque es configurando entradas **ARP estáticas** en los dispositivos, lo que previene que las tablas ARP se actualicen de forma dinámica y asegura que las direcciones IP estén asociadas a direcciones MAC específicas.

- **Segmentación de redes y encriptación**: El uso de técnicas como **VPNs** o redes segmentadas también ayuda a protegerse contra ataques de **Man-in-the-Middle** (MITM), ya que cifran el tráfico, dificultando que el atacante pueda leer o modificar los datos.

### Conclusión

El ataque de **ARP Spoofing** aprovecha la falta de seguridad en el protocolo ARP para interceptar o redirigir el tráfico de red. Al enviar respuestas ARP falsificadas al router y a la víctima, el atacante puede hacer que ambos dispositivos crean que la dirección MAC del atacante corresponde a la dirección IP del otro, convirtiéndose en un "hombre en el medio" (MITM). El envenenamiento de la tabla ARP se mantiene de forma continua enviando ARP Replies falsificados, lo que permite al atacante mantener el control sobre el tráfico de la red local.****