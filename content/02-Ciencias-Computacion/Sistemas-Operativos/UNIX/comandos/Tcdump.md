---
title: "Tcdump"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---


### ¿Qué es **`tcpdump`**?


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/Pila-de-protocolos-TCPIP|Pila de protocolos TCPIP]].

**`tcpdump`** es una herramienta de línea de comandos utilizada para capturar y analizar paquetes de red en tiempo real. Es muy útil para diagnosticar problemas de red, inspeccionar el tráfico o incluso hacer auditorías de seguridad. Es una de las herramientas más populares en entornos Linux/Unix para monitoreo de tráfico de red.

### Cómo usar **`tcpdump`**:

#### 1. **Captura básica de paquetes**:
Para capturar paquetes en la interfaz de red predeterminada (generalmente `eth0` o `wlan0`), puedes ejecutar el siguiente comando:
```bash
sudo tcpdump
```
Este comando comenzará a capturar todos los paquetes de la interfaz predeterminada y mostrará información sobre cada uno de ellos.

#### 2. **Especificar una interfaz de red**:
Si deseas capturar en una interfaz de red específica, puedes usar la opción `-i`. Por ejemplo, para capturar en la interfaz `eth0`:
```bash
sudo tcpdump -i eth0
```

#### 3. **Filtrar por protocolo**:
Puedes filtrar la captura para centrarse en protocolos específicos, como TCP, UDP, ICMP, entre otros. Ejemplo, para capturar solo paquetes TCP:
```bash
sudo tcpdump -i eth0 tcp
```
Si solo deseas capturar paquetes ICMP (usados por ejemplo por el comando `ping`):
```bash
sudo tcpdump -i eth0 icmp
```

#### 4. **Guardar las capturas en un archivo**:
Para guardar los paquetes capturados en un archivo para su análisis posterior, usa la opción `-w`:
```bash
sudo tcpdump -i eth0 -w captura.pcap
```
Esto guardará los paquetes en un archivo con extensión `.pcap`, que luego puedes abrir con herramientas como **Wireshark**.

#### 5. **Leer un archivo de captura**:
Si tienes un archivo de captura previamente guardado y deseas analizarlo, usa la opción `-r`:
```bash
sudo tcpdump -r captura.pcap
```

#### 6. **Limitar el número de paquetes capturados**:
Si solo deseas capturar un número determinado de paquetes y detener la captura automáticamente después de alcanzarlo, utiliza la opción `-c`:
```bash
sudo tcpdump -i eth0 -c 10
```
Este comando capturará solo 10 paquetes.

#### 7. **Ver información detallada**:
Si quieres ver más detalles sobre los paquetes capturados, puedes aumentar el nivel de detalle con las opciones `-v`, `-vv`, o `-vvv`:
```bash
sudo tcpdump -i eth0 -vv
```
La opción `-vvv` muestra la mayor cantidad de detalles posibles.

#### 8. **Filtrados avanzados con expresiones**:
**`tcpdump`** tiene una sintaxis para crear filtros complejos, lo que te permite capturar solo el tráfico que te interesa. Algunos ejemplos:

- Capturar tráfico de un **IP específico**:
  ```bash
  sudo tcpdump -i eth0 host 192.168.1.1
  ```

- Capturar tráfico entre dos direcciones IP:
  ```bash
  sudo tcpdump -i eth0 src 192.168.1.1 and dst 192.168.1.2
  ```

- Capturar tráfico en una **puerta específica** (por ejemplo, HTTP en el puerto 80):
  ```bash
  sudo tcpdump -i eth0 port 80
  ```

- Capturar solo tráfico **UDP** en un puerto específico:
  ```bash
  sudo tcpdump -i eth0 udp and port 53
  ```

#### 9. **Ver los paquetes en formato más simple**:
Si prefieres ver los paquetes de forma más sencilla, en formato hexadecimal y ASCII, usa la opción `-X`:
```bash
sudo tcpdump -i eth0 -X
```

### Ejemplos comunes de comandos:

- **Capturar paquetes TCP en una interfaz específica**:
  ```bash
  sudo tcpdump -i eth0 tcp
  ```

- **Capturar paquetes de un host específico**:
  ```bash
  sudo tcpdump -i eth0 host 192.168.1.1
  ```

- **Capturar tráfico en el puerto 443 (HTTPS)**:
  ```bash
  sudo tcpdump -i eth0 port 443
  ```

- **Capturar tráfico entre dos direcciones IP**:
  ```bash
  sudo tcpdump -i eth0 src 192.168.1.1 and dst 192.168.1.2
  ```

### Consejos importantes:

- **Permisos**: Para usar `tcpdump`, generalmente necesitas privilegios de superusuario (root) para acceder a las interfaces de red y capturar paquetes.
  
- **Uso de recursos**: La captura de paquetes puede consumir muchos recursos, especialmente si el tráfico de red es elevado. Si planeas capturar durante mucho tiempo, es recomendable guardar los paquetes en un archivo (`-w`) y analizarlos después para evitar el consumo excesivo de memoria.

- **Análisis posterior**: Después de guardar los paquetes, puedes usar herramientas como **Wireshark** para un análisis más interactivo y detallado de los datos capturados.

### Instalación:

Si **`tcpdump`** no está instalado en tu sistema, puedes instalarlo con el siguiente comando:

- **Ubuntu/Debian**:
  ```bash
  sudo apt install tcpdump
  ```

- **CentOS/RHEL**:
  ```bash
  sudo yum install tcpdump
  ```

- **Arch Linux**:
  ```bash
  sudo pacman -S tcpdump
  ```
