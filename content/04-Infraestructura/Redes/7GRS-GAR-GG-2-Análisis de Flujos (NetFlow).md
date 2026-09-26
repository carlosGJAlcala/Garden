---
title: "7GRS-GAR-GG-2-Análisis de Flujos ( NetFlow)"
tags: [universidad, 4anyo, redes3]
date: 2026-08-12
lang: es
---

# 7GRS-GAR-GG-2-Análisis de Flujos ( NetFlow)

## Limitaciones del Análisis de Tráfico Tradicional

Análisis de tráfico: proceso de medida y valoración del tráfico de red para la identificación de patrones de interés. ( e.g. Matriz de tráfico de la semana pasada)

Ejemplo de análisis tradicional:

- Uso de SNMP y de la MIB de RMON ( o un analizador de paquetes)
  - Examinar los paquetes de los diferentes enlaces y sacar estadísticas
- Problema: el procesamiento se hace por paquete
  - Se examina un paquete y se actualizan estadísticas ( contadores…)
  - No se pueden detectar relaciones entre paquetes
    - ¿Iba el paquete al mismo destino que el anterior?
    - ¿Qué paquetes forman parte de una misma conversación?
    - 20% del tráfico son emails. Pero ¿cuántos emails se han enviado?
- Sólo permite estadísticas agregadas

## Solución: la abstracción de Flujo de Red

*Nota: las diapositivas siguientes usaban una pseudo-tabla del extractor de PDF con la frase repartida en celdas; se ha recompuesto en viñetas sin perder palabras.*

- Queremos poder valorar comunicaciones que vayan más allá del paquete individual
  - ¿Tamaño máximo de los emails enviados?
  - ¿Duración media de una llamada VoIP?
  - ¿Número máximo de conexiones TCP simultáneas en un enlace?
- Claramente, el análisis tradicional no permite responder a estas preguntas
- Solución: análisis basado en flujos de red
- Flujo: secuencia de paquetes relacionados
  - Definición genérica y flexible. Permite al administrador de red emplear la granularidad que crea oportuna
    - Un flujo por cada par de programas comunicándose
    - Un flujo para todos los paquetes que van hacia un servidor web

## Posibles usos del Análisis de Flujos

- Caracterización de tráfico: entender el tráfico de red, clasificándolo por protocolo, por aplicación, por destino…
- Estimación de rendimiento, asignando flujos específicos a la carga útil respecto del tráfico total
- Contabilidad y facturación de servicios, separando flujos por cliente y servicio.
- Comparación de entrada/salida de tráfico para dimensionamiento de enlaces, por ejemplo.
- Evaluación de calidad de servicio ( QoS), confirmando si se cumple lo pactado con proveedores o clientes
- Detección de anomalías como eventos o variaciones inesperadas en los flujos de red
- Análisis de seguridad, por ejemplo, para detectar ataques de denegación de servicio o propagación de malware ( virus, worms)
- Diagnóstico y solución de problemas en tiempo real, permitiendo la detección de problemas en el momento en que ocurren
- Análisis Forense, empleando datos históricos de flujos de red para identificar los eventos que dieron lugar a un problema
- Planificación de capacidad, usando la información de flujos para construir matrices de tráfico más avanzadas
- Dimensionamiento y planificación de aplicaciones, empleando flujos para monitorizar aplicaciones concretas de cara a su gestión específica

## Flujos unidireccionales y bidireccionales

- Flujos unidireccionales
  - Se corresponden con tráfico que fluye en una sola dirección
  - Muy populares
    - La mayoría de enlaces son full-duplex
    - Es habitual modelarlos como dos enlaces independientes
    - Permite modelar encaminamiento asimétrico
    - Más flexible
- Flujos bidireccionales
  - Capturan la interacción en ambos sentidos de la comunicación
  - Muy útiles en aplicaciones "simétricas"
    - Misma cantidad de datos en ambos sentidos
    - Mismo camino para ambos sentidos
    - Poco usual
- En ocasiones la propia aplicación restringe el tipo

## Niveles de agregación de flujos

- Concepto intuitivo de flujo
  - Comunicación única entre dos puntos finales
- En la práctica, la definición es más flexible
  - En general, se basa en campos de las cabeceras de los paquetes
    - e.g. paquetes con una determinada IP de destino y puerto TCP destino
  - A veces también restricciones temporales
    - e.g. que no estén separados más de 30 segundos entre sí
- Agregación de flujos
  - Agrupación de comunicaciónes individuales en una misma medida
- Nivel de agregación: granularidad

## Ejemplos de agregación de flujos

- Por dirección IP
  - origen ( e.g. número de hosts contribuyendo a una congestión)
  - destino ( e.g. número de hosts externos con los que interaccionamos)
  - Origen y destino ( pares de máquinas comunicándose)
- Por interfaz de red
  - e.g. para analizar el tráfico de salida de un router
- Por protocolo de transporte ( UDP, TCP, ICMP…)
  - Para analizar cada protocolo por separado
- Por tipo de aplicación
  - Agregando por número de puerto
  - E.g. ¿Qué porcentaje de tráfico es Web y cuál email?
- Por el contenido del paquete
  - Deep packet inspection
  - E.g. Flujos para secciones específicas de una web
- Por extremos finales a nivel de aplicación
  - Clasificando por tupla ( IP origen, IP destino, puerto origen, puerto destino, protocolo)

### Ejemplo: flujo unidireccional por IP origen y destino ( ssh)

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
% ssh 192.168.0.2
respuesta
192.168.1.1
192.168.0.2
```

Flujos activos:

| Flujo | IP Origen | IP Destino |
| --- | --- | --- |
| 1 | 192.168.1.1 | 192.168.0.2 |
| 2 | 192.168.0.2 | 192.168.1.1 |

### Ejemplo: flujo unidireccional por IP origen y destino ( telnet + ping)

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
% telnet 192.168.0.2
% ping 192.168.0.2
login:
192.168.1.1
192.168.0.2
Respuesta eco ICMP
```

Flujos activos:

| Flujo | IP Origen | IP Destino |
| --- | --- | --- |
| 1 | 192.168.1.1 | 192.168.0.2 |
| 2 | 192.168.0.2 | 192.168.1.1 |

### Ejemplo: flujo unidireccional por IPs, puertos y protocolo

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
% telnet 192.168.0.2
% ping 192.168.0.2
192.168.1.1 192.168.0.2
```

Flujos activos:

| Flujo | IP Origen | IP Destino | Prot | srcPort | dstPort |
| --- | --- | --- | --- | --- | --- |
| 1 | 192.168.1.1 | 192.168.0.2 | TCP | 32000 | 23 |
| 2 | 192.168.0.2 | 192.168.1.1 | TCP | 23 | 32000 |
| 3 | 192.168.1.1 | 192.168.0.2 | ICMP | 0 | 0 |
| 4 | 192.168.0.2 | 192.168.1.1 | ICMP | 0 | 0 |

### Ejemplo: flujo bidireccional por IPs, puertos y protocolo

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
% telnet 192.168.0.2
% ping 192.168.0.2
192.168.1.1 192.168.0.2
```

Flujos activos:

| Flujo | IP Origen | IP Destino | Prot | srcPort | dstPort |
| --- | --- | --- | --- | --- | --- |
| 1 | 192.168.1.1 | 192.168.0.2 | TCP | 32000 | 23 |
| 2 | 192.168.1.1 | 192.168.0.2 | ICMP | 0 | 0 |

## Análisis de Flujos Online y Offline

- Análisis online
  - Los flujos se analizan en tiempo real
    - Se envían los datos al analizador en cuanto se recogen
    - Retardos entre el evento y la visualización
    - Por la velocidad del análisis
    - Por el nivel de agregación
    - Por el retardo en el transporte de los datos desde recogida a análisis
- Análisis offline
  - Se analizan los flujos después de que los datos se han recogido y almacenado
    - e.g. cada noche se analizan los datos de las últimas 24 horas
  - Útil para análisis forense o cuando no se sabe a priori qué analizar
  - Ventaja principal: no hay restricciones de tiempo de cómputo

## Captura de Datos Activa y Pasiva

- Captura de datos pasiva
  - El hardware que captura información está separado del que procesa o reencamina los paquetes
    - sonda conectada a un hub en una subred
    - Mirror port en un switch
    - optical splitter en redes de fibra
  - No interfiere en el tráfico de la red
  - Normalmente se restringe a un solo enlace o VLAN
- Captura de datos activa
  - Un elemento de la red incluye hardware/software para la captura
    - e.g. Añadir una tarjeta de análisis de flujos en un router
  - Permite analizar todo el tráfico que pasa por el elemento de red
  - Permite emplear la información de flujo para la operación
  - Hace los routers más complejos

### Diagrama: captura de datos pasiva

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
Estación A Estación B
Sonda de Flujos conectada a un puerto
del switch en modo de "repetidor" ( mirror)
```

### Diagrama: captura de datos activa

*Diagrama de la diapositiva, texto linealizado en el orden extraído:*

```
LAN
LAN
LAN
Internet
```

Módulo colector de flujos registra todos los flujos procesados por el router.

## Inspección y clasificación de paquetes

Imaginemos una paquete que lleva una petición HTTP:

```
Cabecera   Cabecera  Cabecera   Mensaje
Ethernet   IP        TCP        HTTP Request
           Tipo      Protocolo  Puerto destino
```

- Cada cabecera tiene un campo que indica de qué tipo es la PDU encapsulada
  - ( 0x0800, 6, 80) è IP, TCP, HTTP ( probablemente)
  - Consultando estos tres campos "sabemos" que es un flujo web.
- Clasificación: proceso de chequeo selectivo de campos para ver a qué flujo pertenece un paquete
  - Mucho más rápido que inspeccionar el paquete completo
  - Puede optimizarse por hardware
- El "esfuerzo" es proporcional al número de cabeceras

### Inspección y clasificación de paquetes ( II)

¿Y si queremos mucho más control?:

```
Cabecera   Cabecera  Cabecera   Mensaje
Ethernet   IP        TCP        HTTP Request
                                 GET /products HTTP/1.0
           Tipo      Protocolo  Puerto destino  URL
```

- Podemos utilizar la URL ( o parte de ella) para definir flujos para diferentes secciones del sitio web
  - Desde el punto de vista del administrador, prácticamente igual
  - Desde el punto de vista del clasificador, muy diferente
    - La URL no se encuentra en una posición fija
    - Requiere procesar el paquete a nivel de aplicación
- Deep packet inspection
  - Requiere muchos más recursos computacionales
  - El clasificador será más lento ( tiempo real è menos paquetes/s)

## Flujos y reenvío optimizado

- Dos funciones diferenciadas en un router "avanzado"
  - Reenvío de paquetes y Captura de información de flujos
  - Ambas suponen una clasificación de paquetes
    - Reenvío: cabeceras è siguiente salto
    - Flujos: cabeceras è flujo
- Pueden combinarse para optimizar el reenvío
  - Creamos una memoria caché para los flujos activos
    - Asociando ID de flujo con siguiente salto
    - Menos flujos que posibles destinos
    - Memoria más pequeña è acceso más rápido
  - Los paquetes de flujos conocidos se reenvían mirando la caché
    - Sólo se mira la tabla de reenvío para el primer paquete de cada flujo
  - Útil si es probable que se repitan paquetes de un flujo
    - Localidad temporal de referencia è normalmente elevada

## Exportación de Datos de Flujo

- Comunicación de los datos de flujo desde el punto donde se originan hasta el punto de análisis
  - Típicamente, router è máquina de gestión
- Formato de datos de exportación
  - Compromiso entre cantidad de información y eficiencia
    - Más información implica mejores posibilidades de análisis
    - Pero consume ancho de banda y almacenamiento
  - Metadatos
    - Timestamp de cada registro
    - ID del equipo que capturó los datos
- Protocolo
  - De nuevo, compromiso entre eficiencia y efectividad
    - e.g. ¿nivel de enlace o de transporte?

## NetFlow

- La tecnología de flujos más usada actualmente
  - Desarrollada por CISCO para mejorar el rendimiento de los routers ( con cachés de flujos)
  - Definieron un formato de exportación de datos de flujo para monitorizar el rendimiento
  - Fueron los usuarios los que se dieron cuenta del potencial de esos datos y desarrollaron herramientas de análisis
- Formato de datos de exportación
  - Recogido en el RFC 3954 ( versión 9)
- Arquitectura distribuida
  - Exportadores
  - Colectores
  - Analizadores

### Características básicas

- Paradigma de captura activa
  - El router registra información sobre los flujos y la exporta a un colector externo
- Flujos de datos unidireccionales
- Permite al administrador controlar la captura de datos
  - E.g. Frecuencia de muestreo de paquetes
- En versiones previas, campos de exportación fijos
  - IP origen/destino
  - Puerto origen/destino
  - Interfaz de entrada /salida
  - …
- Versión 9: más flexible
  - Permite elegir qué datos usar para definir los flujos

### Extensibilidad y plantillas

- NetFlow envía información descriptiva con los datos
  - Campos de datos enviados
  - Longitud de cada campo
  - …
- Con esa información ( plantilla), el colector ya sabe cómo procesar los datos
  - Sólo es necesario configurar los exportadores
- Las plantillas tienen un ID asignado, por lo que sólo se envían la primera vez
- El formato de paquete permite incluso añadir nuevos campos sin necesidad de crear una versión nueva

### Configuración de Netflow

- Campos que se incluyen en cada plantilla
  - Pueden definirse plantillas diferentes para cada flujo
- Tasa de muestreo de paquetes
  - Básicamente, permite muestrear un paquete de cada N
    - No necesariamente muestreo determinista
  - Permite balancear la precisión y el volumen de datos
- Tamaño de caché
  - Se exportan flujos completos è necesario almacenamiento
  - El tamaño de caché limita el número de flujos simultáneos
    - ¡¡¡Si la caché se llena, se exportan los flujos incompletos!!!
- ¿Cómo sabe el exporter cuando el flujo está completo?
  - TCP: muy simple è cuando se libera la conexión
  - ¿IP, UDP? è temporizador de flujo
    - Configurable; puede afectar al funcionamiento

### Transporte de datos en Netflow

- Se emplea UDP para enviar datos desde los exporters a los collecters
  - Se pueden perder o reordenar paquetes
  - No hay control de flujo ni de congestión
- A partir de la versión 2, Netflow emplea números de secuencia en sus mensajes
  - Si los mensajes llegan antes que su plantilla, se almacenan hasta que esta llegue
  - Periódicamente se reenvía la plantilla ( por si acaso)
- El tráfico de Netflow puede congestionar la red
  - ¿Cómo evitarlo? Netflow no lo hace
  - Soluciones a nivel de administrador
    - Enviar el tráfico Netflow por una red separada
    - Limitar la cantidad de tráfico que genera Netflow

## Consideraciones finales

- Herramientas de análisis de datos para Netflow
  - Existen múltiples, y algunas de código abierto
  - http://www.splintered.net/sw/flow-tools/
- Información adicional por parte de CISCO
  - http://www.cisco.com/en/US/products/ps6601/products_ios_protocol_group_home.html
- IETF Internet Protocol Flow Information eXport ( IPFIX)
  - Protocolo basado en Netflow versión 9
  - Incluye seguridad y soporte de control de congestiones
  - http://tools.ietf.org/wg/ipfix/

## Bibliografía

- Douglas E. Comer "Automated Network Managemet Systems", Capítulo 11
- Recursos adicionales:
  - http://sourceforge.net/projects/netfltools/
  - http://ws.edu.isoc.org/
- Más recursos adicionales
  - http://www.splintered.net/sw/flow-tools/docs/flow-tools-examples.html
  - http://nfdump.sourceforge.net/
  - http://flow-tools.sourcearchive.com/
  - http://www.cisco.com/en/US/docs/ios/12_2/switch/configuration/guide/xcfnfc.html

## Anexos – Uso de Netflow

Vale, ¿pero qué pinta tiene esto en la práctica?

### Cabecera y registro Netflow ( versión 5)

- Cabecera netflow ( versión 5)
- Registro netflow ( versión 5)
  - No necesariamente conveniente ( e.g. Tiempo de inicio)

*(estas dos diapositivas incluyen una imagen de la cabecera y del registro netflow v5 no extraída como texto)*

### Configurar dispositivo "exportador" ( e.g. router Cisco)

```bash
configure terminal
interface serial 3/0/0
ip route-cache flow exit
ip flow-export 1.1.15.1 12345 version 5 peer-as
exit
clear ip flow stats
```

### Caché de Netflow en el router

```
Router# show ip cache flow
IP packet size distribution ( 230151 total packets):
   1-32    64   96  128  160  192  224  256  288  320  352  384  416  448  480
    .999 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000
    512   544  576 1024 1536 2048 2560 3072 3584 4096 4608
    .000 .000 .000 .000 .000 .000 .000 .000 .000 .000 .000
```

*( la diapositiva "Caché de Netflow en el router ( cont.)" continúa con una captura de pantalla no extraída como texto)*

### Configurar un "colector" ( Linux con flow-tools)

```
# flow-capture -p /var/run/flow-capture.pid
-n 287 -w /var/netflow/sensorXY \
-S 5 1.1.15.1/1.1.15.2/12345
```

### Examinar datos en un "analizador" ( Linux con flow-tools)

Definir filtros ( no imprescindible, pero conveniente):

```
filter-primitive tcp_only
type ip-protocol
permit 6
filter-definition tcp_only
match ip-protocol tcp_only
```

```bash
$ flow-cat ./data | flow-nfilter -f filters -F tcp_only | flow-stat -f9 –S1
#
#
#
#
130.49.72.0 30415 6881695 36110
128.223.216.0 28716 540202269 427566
130.49.88.0 24267 10770631 32186
```

### Más posibilidades ( flow-report)

```bash
root@server:~# flow-cat /var/flows/2008/2008-11/2008-11-13/ft-v05.2008-11-13.113001-0430 | flow-report -Sst3 | flow-rptfmt -fascii
ip-destination-port flows octets packets
http 1966 1380162 15390
telnet 11 334734 8016
imaps 12 277522 3284
https 169 219010 1092
48492 2 141779 1357
60280 2 141739 1356
ssh 53 114556 1281
34498 3 75666 1244
43607 3 74334 1243
40282 2 72953 1236
1863 65 57043 607
cfengine 4 17877 182
55641 3 3458 15
55636 2 2598 10
```

### Más posibilidades ( nfdump)

```bash
ip/flows -s dstport/pps/packets/bytes -s record/bytes
```

### Más posibilidades ( exportación a PostgreSQL / Excel)

- Exportación de los flujos a tablas en un servidor PostgreSQL
  - PervasiveTechnologies at Indiana University
- Permite exportarlo luego a Excel para sacar gráficas, estadísticas, etc.

*(la diapositiva siguiente, también titulada "Más posibilidades", sólo contiene una captura de pantalla no extraída como texto)*

### Aún más posibilidades ( herramientas comerciales)

- ICmyNet.Flow
  - http://www.icmynet.com/products/icmynet.flow/overview.html
  - Libre para uso académico ( y tryout de 30 días)

*(las tres diapositivas siguientes repiten el mismo título y "ICmyNet.Flow" con capturas de pantalla adicionales no extraídas como texto)*

### Ejemplo práctico

Monitorización de una red académica mediante Netflow

### Más herramientas

- Netflow analyzer
  - https://www.manageengine.com/products/netflow/?utm_source=capterra&utm_medium=ppc&utm_campaign=NetFlow
- Vigilar los IP SLA
  - https://www.manageengine.com/products/netflow/ipsla-monitor.html
- NFsens
  - https://sourceforge.net/projects/nfsen/
