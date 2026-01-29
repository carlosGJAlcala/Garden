---
title: "Iptables"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - redes
---
**`iptables`** es una herramienta en sistemas Linux que se utiliza para configurar y administrar las reglas de filtrado de paquetes en el **firewall** del sistema. Permite controlar el tráfico de red, estableciendo reglas que determinan qué paquetes pueden o no pueden llegar a tu sistema. Es una de las herramientas más poderosas para gestionar la seguridad en redes en sistemas basados en Linux.

En términos simples, **`iptables`** actúa como un **filtro de tráfico** que examina los paquetes de datos que llegan o salen del sistema, y decide si deben ser aceptados, rechazados o redirigidos según las reglas que le defines.

### Componentes clave de `iptables`


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

1. **Tablas**: 
   Las reglas de `iptables` se organizan en **tablas**. Cada tabla tiene un propósito diferente, y las reglas dentro de ellas determinan cómo se maneja el tráfico. Existen varias tablas, pero las más comunes son:

   - **`filter`**: Es la tabla por defecto y se utiliza para filtrar paquetes. Aquí se definen las reglas que permiten o bloquean el tráfico de red.
   - **`nat`**: Esta tabla se usa para realizar **traducción de direcciones de red** (NAT, por sus siglas en inglés). Aquí puedes modificar la dirección IP de los paquetes, lo que se usa comúnmente en routers para compartir la conexión a Internet.
   - **`mangle`**: Se utiliza para modificar los paquetes de manera más avanzada, como cambiar la prioridad del tráfico, marcar paquetes, etc.
   - **`raw`**: Se usa para configurar excepciones de seguimiento de conexión, es decir, para paquetes que no deben ser tratados por el mecanismo de seguimiento de conexiones.

2. **Cadenas (Chains)**: 
   Dentro de cada tabla, las reglas se organizan en **cadenas**, que son secuencias de reglas que se ejecutan en un orden específico. Las principales cadenas son:

   - **`INPUT`**: Esta cadena maneja los paquetes que van dirigidos al sistema local (es decir, al servidor o computadora que ejecuta `iptables`).
   - **`OUTPUT`**: Maneja los paquetes que salen del sistema local hacia la red.
   - **`FORWARD`**: Se utiliza cuando el tráfico está siendo **ruteado** a través del sistema, es decir, cuando el sistema está actuando como un router o puente entre otras redes.
   - **`PREROUTING`**: Esta cadena se utiliza antes de que los paquetes sean enrutados, generalmente se usa para cambiar la dirección de los paquetes (por ejemplo, en el caso de redirección de puertos).
   - **`POSTROUTING`**: Se utiliza después de que el paquete ha sido enrutado, por lo general se usa para hacer NAT, como en el caso de la traducción de direcciones de origen.

3. **Reglas**: 
   Cada **regla** en `iptables` especifica lo que debe hacer un paquete que coincida con ciertas condiciones (por ejemplo, una dirección IP o un puerto). Las acciones que se pueden tomar son principalmente:
   
   - **`ACCEPT`**: Permite que el paquete pase sin restricción.
   - **`DROP`**: Bloquea el paquete sin enviar ninguna notificación.
   - **`REJECT`**: Bloquea el paquete, pero envía una notificación al remitente.
   - **`SNAT`**: Realiza la traducción de la dirección IP de origen (usado principalmente en NAT).
   - **`DNAT`**: Realiza la traducción de la dirección IP de destino.
   - **`LOG`**: Registra el paquete (útil para auditorías).

### Ejemplo de comandos básicos de `iptables`

1. **Ver reglas actuales**:
   Para ver las reglas configuradas actualmente en el sistema, se utiliza el siguiente comando:

   ```bash
   sudo iptables -L
   ```

2. **Permitir tráfico HTTP (puerto 80)**:
   Para permitir todo el tráfico entrante en el puerto 80 (HTTP), puedes añadir la siguiente regla:

   ```bash
   sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
   ```

   - `-A INPUT`: Añade la regla a la cadena de entrada (paquetes que van hacia el sistema).
   - `-p tcp`: Especifica que estamos tratando con tráfico TCP.
   - `--dport 80`: Especifica que queremos que la regla se aplique a los paquetes dirigidos al puerto 80.
   - `-j ACCEPT`: Indica que los paquetes que coincidan con esta regla deben ser aceptados.

3. **Bloquear tráfico entrante de una IP específica**:
   Para bloquear todo el tráfico de una dirección IP específica, se puede usar el siguiente comando:

   ```bash
   sudo iptables -A INPUT -s 192.168.1.100 -j DROP
   ```

   - `-s 192.168.1.100`: Especifica que la regla se aplica a los paquetes que provienen de la IP `192.168.1.100`.
   - `-j DROP`: Indica que esos paquetes deben ser bloqueados.

4. **Redirigir tráfico de un puerto a otro**:
   Para redirigir el tráfico que llega al puerto 80 (HTTP) hacia el puerto 8080, puedes usar el siguiente comando (típico en ataques como **SSLStrip** o para proxies):

   ```bash
   sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
   ```

   - `-t nat`: Especifica que estamos trabajando con la tabla NAT (Traducción de direcciones de red).
   - `PREROUTING`: Indica que la regla se aplicará antes de que los paquetes sean enrutados.
   - `--dport 80`: Aplica la regla a los paquetes que lleguen al puerto 80.
   - `-j REDIRECT`: Indica que queremos redirigir el tráfico.
   - `--to-port 8080`: Especifica que el tráfico debe ser redirigido al puerto 8080.

5. **Eliminar una regla**:
   Si deseas eliminar una regla, por ejemplo, para bloquear una IP, puedes hacerlo con:

   ```bash
   sudo iptables -D INPUT -s 192.168.1.100 -j DROP
   ```

   - `-D INPUT`: Elimina la regla de la cadena de entrada.

### ¿Por qué usar `iptables`?

- **Seguridad**: `iptables` se utiliza para proteger los sistemas de accesos no deseados, bloqueando puertos o direcciones IP maliciosas.
- **NAT (Traducción de direcciones de red)**: Puedes usar `iptables` para compartir una conexión a Internet entre varios dispositivos (por ejemplo, en una red local con un solo punto de acceso a Internet).
- **Redirección de tráfico**: Puedes redirigir tráfico de un puerto a otro, útil en configuraciones de proxies o cuando necesitas realizar una auditoría de tráfico.

### Consejos adicionales:

- **Persistencia**: Las reglas de `iptables` no son persistentes por defecto (es decir, se pierden después de reiniciar). Para hacer que las reglas sean permanentes, puedes usar herramientas como **`iptables-save`** y **`iptables-restore`** o configurar un script que se ejecute al inicio del sistema.
  
- **Prueba y monitoreo**: Es recomendable probar las reglas de firewall en un entorno de pruebas antes de implementarlas en producción, y monitorear constantemente el tráfico para detectar comportamientos inusuales.

`iptables` es una herramienta poderosa, pero requiere cuidado al configurarla. Un error en las reglas puede bloquear el acceso a tu sistema o interrumpir servicios críticos.