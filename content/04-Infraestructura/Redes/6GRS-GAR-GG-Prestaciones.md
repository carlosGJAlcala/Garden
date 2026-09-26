---
title: "6GRS-GAR-GG-Prestaciones"
tags: [universidad, 4anyo, redes3]
date: 2026-08-12
lang: es
---
# 6GRS-GAR-GG-Prestaciones

Gestión de Prestaciones y Optimización
Gestión de Redes

## Prestaciones: Objetivo y Beneficios

Asegura que los recursos en la red permanecen accesibles para que los usuarios los utilicen eficientemente.

Beneficios:
- Mejor nivel de servicio (Calidad):
  - Ayuda a prevenir congestión
  - Aumenta el rendimiento
  - Mejora la disponibilidad
- Ayuda a planificar la futura capacidad necesaria de la red (Optimización).

## Técnicas

- Monitorización de datos: utilización de dispositivos y enlaces para determinar el comportamiento y nivel de servicio de la red.
  - → Poner umbrales de utilización que avisan antes de llegar a valores máximos.
- Generación de tráfico que permite observar el comportamiento de la red bajo cierto nivel de carga controlada.
- Análisis de datos: permite verificar si se sobrepasa la capacidad de la red y planificar la futura capacidad.
- Simulación de red permite determinar cómo la red puede ser modificada para optimizarla.

## Aspectos a Considerar

- ¿Qué medir?
  - Elementos, indicadores
- ¿Cómo obtener medidas?
- ¿Qué hacer con las medidas?

## ¿Qué Elementos Pueden Ser Medidos?

Enlaces de red
- Utilización del enlace en el tiempo
- Detectar anomalías (gestión de fallos)
- Planificación de capacidad

Elementos de red (router, conmutador)
- Paquetes procesados
- Algunos dispositivos incorporan herramientas específicas de análisis de rendimiento.

Servicios de red y Aplicaciones (DNS, VPN, LDAP, smtpd, HTTP, base de datos….)
- Medir las prestaciones desde el punto de vista del cliente
- Medir el tiempo de respuesta tanto para peticiones internas como externas

## ¿Cómo Medir?

Es sencillo tomar medidas de indicadores locales en cada elemento de un enlace.
- Ejemplo: retardo, paquetes perdidos, throughput…. en un router concreto.

El usuario final está interesado en medidas de indicadores extremo a extremo
- Ejemplo: retardo en obtener respuesta de un servidor web.

→ No es inmediato deducir medidas extremo a extremo a partir de medidas locales.

## Aproximaciones de Medidas en la Red

Observación Pasiva: obtiene medidas sobre el rendimiento de una forma no intrusiva.
- Medidas locales.

Pruebas Activas: tests que generan tráfico para tomar medidas, afectando al tráfico existente.
- Medidas extremo a extremo
- Intrusiva
- Resultados realistas

## Indicadores

### ¿Qué Parámetros Medir? – Indicadores

- Disponibilidad: tiempo que la red está disponible y tiempo de recuperación ante problemas.
- Tiempo de respuesta: tiempo que tarda el sistema en reaccionar a una entrada determinada.
- Fiabilidad: porcentaje de tiempo sin errores en la transmisión y entrega de información.
- Velocidad efectiva o Throughput: eventos/seg.
- Utilización: porcentaje de la capacidad que está siendo utilizada
- Latencia: retardo de un paquete al atravesar la red (ms).
- Jitter: varianza en el retardo de paquetes (importante para tráfico en tiempo real como es el de voz).
- Pérdida de paquetes: porcentaje de paquetes que la red pierden (%).

### Disponibilidad

Porcentaje de tiempo que un sistema de red, componente o aplicación está disponible para el usuario.

Medida de disponibilidad A:

```
A = MTBF / (MTBF + MTTR)
```

- MTBF: tiempo medio entre fallos.
- MTTR: tiempo medio de reparación.

La disponibilidad de un sistema depende de la disponibilidad de sus componentes. El fallo de un componente puede ocasionar:
- Que el sistema no funcione: serie.
- Que el sistema siga funcionando igual: paralelo (redundancia).
- Que el sistema funcione con una reducción de la capacidad: el cálculo se hace más complejo al tener en cuenta la carga.

### Disponibilidad – Ejemplos

Sistema disponible si ambos elementos lo están: A*A = A²
Sistema indisponible si ambos elementos lo están: (1-A)²
Entonces: 1-(1-A)² = 2A-A²

### Disponibilidad – Ejercicio

Dos enlaces en paralelo con disponibilidad A.
- En periodos de carga normal (40% de peticiones de servicio) cualquiera de los enlaces puede absorber todo el tráfico (100%).
- En periodos de picos de carga un solo enlace absorbe el 80% del tráfico.

Calcule la disponibilidad total

### Disponibilidad – Solución

*(Las siguientes fórmulas tenían los subíndices esparcidos en celdas de tabla por el extractor de PDF; se han recompuesto con la notación de subíndice más plausible según el contexto, sin alterar el contenido matemático.)*

Disponibilidad Funcional para una situación de carga:

```
Af = C₁*Pr₁ + C₂*Pr₂
```

- Cᵢ es la capacidad con i enlaces.
- Probabilidad de que funcionen los dos enlaces: Pr₂ = A²
- Probabilidad de que funcione un enlace: Pr₁ = A(1-A)+(1-A)A = 2A-2A²

- En situaciones de carga normal: C₁ = C₂ = 1; Afₙ = 1*Pr₁ + 1*Pr₂
- En situaciones de pico de carga: C₁ = 0.8, C₂ = 1; Afₚ = 0.8*Pr₁ + 1*Pr₂

Disponibilidad total:

```
Af = 0.4*Afₙ + 0.6*Afₚ
```

### Tiempo de Respuesta

Tiempo que tarda el sistema en reaccionar a una entrada determinada.

Un mejor tiempo de respuesta aumenta la productividad pero tiene un coste que hay que evaluar:
- Mayores requisitos hardware: cpu, memoria...
- Competencia entre procesos: penaliza a otros procesos.

Medidas de tiempo de respuesta se pueden utilizar para:
- Corregir problemas y dimensionar adecuadamente la red.
- Identificar cuellos de botella (estudio más detallado).

### Fiabilidad

Porcentaje de tiempo sin errores en la transmisión y entrega de información.

Es un parámetro dependiente de la tecnología usada y por lo tanto no controlable por el usuario.

La tasa de errores que deben ser corregidos es un indicador de:
- Fallos intermitentes en la línea.
- Existencia de fuentes de ruido o interferencias.

### Fiabilidad – Ejemplos

Indicador de fiabilidad de la red (rechazos de conexión):
- tcpAttemptFails: nº de intentos fallidos para abrir una conexión.
- tcpEstabResets: nº de resets para una conexión establecida.
- tcpRetransSegs: número de segmentos retransmitidos.
- tcpInErrs: número de segmentos recibidos con error.
- tcpOutRsts: nº de intentos de hacer reset en una conexión indica un problema que afecta a la fiabilidad.

### Fiabilidad – Ejercicio

Los paquetes descartados y los errores en un interfaz indican problemas en el interfaz o el medio.

Ocasionan pérdida de rendimiento.

Medir el porcentaje de descartes y de errores en la transmisión y recepción de un interfaz de comunicación.

### Fiabilidad – Solución (descartes)

Porcentaje de paquetes descartados en un interfaz:

```
% in_Discards  = ifInDiscards / (ifInUcastPkt + ifInNUcastPkts)
% out_Discards = ifOutDiscards / (ifOutUcastPkt + ifOutNUcastPkts)
```

- ifInDiscards: paquetes descartados de entrada.
- ifOutDiscards: paquetes descartados de salida.
- ifIn(Out)UcastPkts: paquetes unicast
- ifIn(Out)NUcastPkts: paquetes no unicast

Si ifInDiscard crece al mismo ritmo que ifInUnknownProtos. Los paquetes se descartan por protocolo desconocido. El problema no es del interfaz.

### Fiabilidad – Solución (errores)

Porcentaje de errores en un interfaz:

```
% input errors  = ifInError / (ifInUcastPkts + ifInNUcastPkts)
% output errors = ifOutError / (ifOutUcastPkt + ifOutNUcastPkts)
```

- ifIn(Out)Errors: paquetes con error
- ifIn(Out)UcastPkts: paquetes unicast
- ifIn(Out)NUcastPkts: paquetes no unicast

Las medidas se pueden tomar en un periodo de tiempo (j-i):

```
valor = valorⱼ – valorᵢ
```

### Velocidad Efectiva (o Throughput)

Velocidad a la que ocurren eventos.

Ejemplos:
- Transmisión o procesamiento de datos: bps, pkts/seg…
- Nº de llamadas a un servicio en un periodo de tiempo.
- Nº de conexiones en periodo de tiempo.

Su monitorización permite:
- Conocer la demanda de un determinado servicio (planificación).
- Localización de problemas de prestaciones.

### Velocidad Efectiva – Ejemplos

Velocidad de segmentos:
- Segmentos recibidos (tcpInSegs) o enviados (tcpOutSegs).
- Medir la velocidad: nº de segmentos procesados en un periodo de tiempo entre los instantes i y j.

```
Vef = [(tcpInSegsⱼ + tcpOutSegsⱼ) - (tcpInSegsᵢ + tcpOutSegsᵢ)] / (j-i)
```

### Utilización

Porcentaje de la capacidad teórica del recurso que está siendo utilizada.

Es una medida más fina que la velocidad efectiva.

Se aplica a localización de potenciales cuellos de botella y áreas de congestión (t. respuesta crece exponencialmente con la utilización).

### Utilización – Reparto de Carga Justo

Una aplicación práctica: comparar la utilización de varios enlaces de una red.
- La carga de cada enlace nos permite comprobar el grado de utilización de cada enlace comparándolo con su capacidad.
- La relación %carga/%capacidad nos permite comprobar si el reparto de carga es justo:
  - Medimos la carga de cada enlace (Kbps) en relación (%) con la carga total (suma de todas las cargas).
  - Medimos la capacidad de cada enlace (Kbps) en relación (%) con la capacidad total (suma de todas las capacidades).
  - En cada enlace se calcula: % de carga/% capacidad.

### Relación Retardo-Utilización

La utilización U toma valores entre 0 y 1.

Si aumenta la utilización aparece congestión.

Una estimación de la relación Retardo-utilización:
- D: Retardo o Latencia efectiva
- D₀: Retardo o Latencia en ausencia de tráfico
- U: utilización

```
D ≈ D₀ / (1 − U)
```

### Utilización – Ejercicio (Cálculo Utilización Interfaz)

Utilización de un interfaz:

Total de bytes que pasan por el interfaz por segundo:

```
Bytes/s = [(ifInOctectsⱼ – ifInOctectsᵢ) + (ifOutOctectsⱼ – ifOutOctectsᵢ)] / (j-i)
```

Donde j e i son dos instantes de tiempo.

```
Utilización = (Bytes/s * 8) / ifSpeed
```

### Extra: Indicadores IP Aplicados a Prestaciones (I)

Medidas de prestaciones:
1. Porcentaje de datagramas IP recibidos: B/A
   - A: Suma: ifInNUcastPkts + ifInUcastPkts por cada interfaz
   - B: ipSystemStatsInReceives
2. Porcentaje de tráfico snmp o icmp (control).
3. Velocidad de reenvío: dos medidas en instantes i y j.
   ```
   Ip-forwarding-rate = (ipSystemStatsForwDatagramⱼ - ipSystemStatsForwDatagramᵢ) / (j-i)
   ```
4. Velocidad de paquetes recibidos: dos medidas en instantes i y j.
   ```
   Ip-input-rate = (ipSystemStatsInReceivesⱼ - ipSystemStatsInReceivesᵢ) / (j-i)
   ```

Si Ip-forwarding-rate es similar a Ip-input-rate, buenas prestaciones.

### Extra: Indicadores IP Aplicados a Prestaciones (II)

Problemas de prestaciones
- Indicador de falta de recursos:
  - ipSystemStatsInDiscard, ipSystemStatsOutDiscard
- Carga del sistema si se produce un gran porcentaje de errores o fragmentaciones:

```
% errorsIN = (ipSystemStatsInDiscards + ipSystemStatsInHdrErrors + ipSystemStatsInAddrErrors) / ipSystemStatsInReceives
% fragmetsIN = ipSystemStatsReasmReqds / ipSystemStatsInReceives
```

Elegir el indicador más apropiado es complicado.

### Extra2: ¿Cómo Procesar Varios OIDs?

Podemos usar librerías: por ejemplo en Python

<https://pypi.org/project/pysnmp/>

## Calidad

### Percepción de Calidad de la Red

Diferentes aproximaciones
- Cuantificación de uno o más indicadores:
  - Latencia
  - Throughput
  - Jitter
  - Pérdida de paquetes
  - Disponibilidad
  - ……….
- Nº de reclamaciones de usuarios

### Dependencias de la Calidad

EXTREMOS: depende de los enlaces extremo a extremo
- Cada camino puede pasar por diferentes dispositivos con diferentes características y estado (nivel de congestión)
- No tiene la misma calidad las comunicaciones entre los extremos A y B que entre los extremos C y D

APLICACIONES: cada tipo de aplicación tiene unos requisitos diferentes de calidad.

| | Remote Login | File Transfer | VoIP |
| --- | --- | --- | --- |
| Throughput | - | High | Low |
| Latency | Low | High | Low |
| Jitter | High | - | Low |

### Degradación del Servicio

Un servicio se degrada cuando algunos de sus indicadores tienen valores menores que los esperados.

Causas:
- Fallos: hardware que funciona mal y tira paquetes.
- Problemas de rendimiento (principal causa):
  - Rutas no óptimas en routers
  - Cambios continuos de rutas en routers
  - Enlace de un conmutador saturado
  - ……….

*(Diagrama de red con dos hosts A y B conectados a un servidor mediante enlaces de 1 Gbps.)*

### Congestión y sus Consecuencias

Buffers de paquetes en elementos de red (router, conmutadores…) permiten que estos elementos soporten ráfagas de tráfico.

Si el buffer se llena se produce congestión que influye en:
- Aumento de pérdida de paquetes: descarte de paquetes
- Aumento de latencia: mayor retardo
- Reducción del throughput: menor velocidad efectiva

### Ejercicio: Congestión en Interfaz

Varios indicadores:
- La longitud de la cola de salida permanece con un valor elevado.
- El nº de paquetes descartados a la salida de un interfaz es alto y por el interfaz salen pocos octetos.

¿Cómo puedo detectar la congestión?

### Solución I

¿La longitud de la cola de salida permanece con un valor elevado?

Monitorizar en intervalos de tiempo j-i la evolución de ifOutQLen (Syntax Gauge32)

- Valor cola interfaz salida en instante j: A = ifOutQLenⱼ
- Evolución de la cola: B = ifOutQLenⱼ – ifOutQLenᵢ

Congestión → Si A elevado y B bajo

### Solución II

¿El nº de paquetes descartados a la salida de un interfaz es alto y por el interfaz salen pocos octetos?

Monitorizar en intervalos de tiempo j-i:

```
A = ifOutDiscardⱼ - ifOutDiscardᵢ
B = ifOutOctetsⱼ - ifOutOctetsᵢ
```

Congestión → Si A elevado y B bajo

## Planificación y Optimización

### Optimización y Cuellos de Botella

Objetivo:
- Optimizar el rendimiento
- Para ello hay que identificar cuellos de botella en la red

Cuellos de botella: elementos o subsistemas con respuesta lenta
- Enlaces saturados
- Routers/servidores al límite de su capacidad

Optimización actual:
- Identificar cuellos de botella que se resuelvan con configuración o gestión de fallos

Optimización futura:
- Identificar cuellos de botella por incremento de solicitud de servicio para planificar futuro crecimiento de la red
- Adquisición de nuevo hardware adaptado a las necesidades

### Planificación de Capacidad

- Medir el uso actual: tráfico
- Predecir el uso futuro: estimar tráfico futuro
- Elegir los componentes de red para que soporten la demanda estimada

Posibles escenarios para mejorar los recursos de red según las estimaciones.
- Incrementar el número de puertos de un elemento de red.
- Añadir nuevos elementos de red.
- Añadir nuevos enlaces.
- Incrementar la capacidad de los enlaces.
- ……..

Elegir una solución que tenga una relación de compromiso entre rendimiento, fiabilidad y coste.

### Planificación de Capacidad de Elementos de Red

Conmutador
- Nº de conexiones necesarias (puertos)
- Velocidad de cada conexión (10/100/1000 Mbps)
- Configuración automática en el conmutador.

Router
- Varios servicios: encaminamiento, DHCP, IPv6, VPN…
- Capacidad de cada conexión
- Capacidad depende del entorno en el que el router se instale

Conexión a Internet
- Medir utilización del enlace con ISP por sencillez.
- Otros indicadores: latencia, pérdidas de paquetes, throughput o jitter.
- Tráfico variable: elegir compromiso entre coste del enlace y calidad

### Medir Tráfico de un Enlace

Utilización máxima (pico) y media durante la semana

Dividir semana en intervalos
- Intervalos grandes (15 min):
  - Menos recursos
  - Válido para la mayoría de los casos. Recomendado normalmente.
  - 672 valores a la semana
- Intervalos cortos (5 min, 1 min): mayor precisión en detección de ráfagas

Crear una base repitiendo la medida durante sucesivas semanas (hasta un mes, un año…).

El tráfico normalmente es asimétrico, si es necesario medir en ambas direcciones:
- Utilización subida: empresa-ISP
- Utilización bajada: ISP-empresa (normalmente mayor)

### Cálculo Absoluto de Picos de Utilización

¿Qué tenemos?
- Estadísticas de utilización media y pico durante varias semanas en ambas direcciones.

¿Cómo lo uso para determinar si necesito aumentar la capacidad? Para prevenir pérdida de paquetes.
- Actualizar capacidad antes de que picos de utilización lleguen a 100%.
- Es necesario medir utilización absoluta máxima.
- Seleccionamos el máximo valor de los obtenidos en la serie de medidas de 15 minutos.

### Estimación Suave de Picos de Tráfico

Eventos puntuales en routers pueden provocar cortos picos en utilización no indicativos de tráfico normal.
- Condiciones de error
- Cambio de rutas
- ….

Queremos filtrar estos picos suavizándolos

Calcular picos de utilización usando 95º percentil.
- Medimos tráfico en intervalos de 15 minutos
- Ordenamos la serie de valores de utilización en cada intervalo
- Eliminamos el 5% de valores más altos
- Seleccionamos el valor más alto del resto (95%)

Estimación realista de picos usando 95º percentil

### Relación entre Utilización Media y de Pico

Experiencia en observación del tráfico de grandes organizaciones, en su enlace a Internet
- Observación en enlaces con fuerte carga
- No hay cambios bruscos en el tiempo
- No es necesaria una observación precisa
- Existe una relación aproximada entre la utilización media y pico

```
Pico_Utilización_Estimado / Utilización_Media ≈ 1.3
```

El valor estimado de la relación depende de la organización

Se puede evitar el cálculo de picos

### Regla 50/80

Aplicable a enlaces con fuerte carga

El gestor mide la utilización media y hace estimaciones:

| Utilización media | Pico | Estado del enlace |
| --- | --- | --- |
| 40% | 52% | Infrautilizado |
| 50% | 65% | Normal |
| 60% | 78% | Muy utilizado |
| 70% | 91% | Saturado |
| 80% | 100% | Completamente saturado |

Utilización media durante los periodos de actividad.

La utilización media se debe mantener entre el 50% y 80% de la capacidad del enlace.
