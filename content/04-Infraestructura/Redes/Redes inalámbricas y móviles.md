---
title: "Redes inalámbricas y móviles"
---

# Redes inalámbricas y móviles

Redes inalámbricas y móviles
Introducción
Características de las redes y enlaces inalámbricos
WiFi: redes LAN inalámbricas IEEE 802.11

## Índice

- 6.1 Introducción
- 6.2 Características de las redes y enlaces inalámbricos
- 6.3 WiFi: redes LAN inalámbricas IEEE 802.11

## Motivación

El número de teléfonos móviles supera al de fijos.

Variedad: Portátiles, tabletas, teléfonos… Acceso heterogéneo: "anytime, anywhere"

Desafíos:
- Medio de propagación inalámbrico
- Movilidad: los terminales cambian del punto de acceso a la red

## Elementos de una red inalámbrica

- Hosts inalámbricos: ejecutan aplicaciones. Pueden tener movilidad o no.
- Estaciones base / puntos de acceso (access point, AP): normalmente conectada a la red cableada. Reenvía los paquetes entre la red cableada y la inalámbrica. Poseen un área de cobertura.
- Enlace inalámbrico: conecta host inalámbrico con su punto de acceso. Protocolo de acceso múltiple al medio.

## Tecnologías inalámbricas

WxAN = Wireless x Area Network (término genérico)

| Tipo | Alcance | Tecnologías |
|---|---|---|
| WRAN: Regional | < 100km | IEEE 802.22 |
| WWAN: Wide | < 15km | MBWA |
| WMAN: Metropolitan | < 5km | WiMAX |
| WLAN: Local | < 150m | WiFi |
| WPAN: Personal | < 10m | Bluetooth, ZigBee |

## Tecnologías inalámbricas (continuación)

LTE Advanced (4G)

## Clasificación de las redes inalámbricas

En función de si poseen infraestructura:

- Redes de infraestructura: el AP interconecta toda la red inalámbrica. Comunicación a través del AP. Traspaso/handoff/handover: cambio de AP.
- Red ad hoc: no se emplean APs. Los hosts pueden transmitir a otros hosts que estén dentro de su radio de cobertura. Los nodos (hosts y routers) se organizan para formar una red: se encaminan paquetes entre ellos.

## Clasificación de las redes inalámbricas (continuación)

| | Sólo un salto | Múltiples saltos inalámbricos |
|---|---|---|
| **Infraestructura** | Hosts conectados a una estación base (WiFi, WiMAX, redes celulares) que se conecta a Internet | Los hosts pueden necesitar varios saltos para alcanzar a la estación base (wireless mesh networks) |
| **Sin infraestructura** | No hay estación base (Bluetooth, redes ad hoc) | No hay estación base y las comunicaciones pueden darse en varios saltos (ej. VANET Vehicle Ad-Hoc Network, MANET Mobile Ad-Hoc Network) |

## Índice

- 6.1 Introducción
- 6.2 Características de las redes y enlaces inalámbricos
- 6.3 WiFi: redes LAN inalámbricas IEEE 802.11
- 6.4 Acceso celular a Internet
- 6.5 Gestión de la movilidad: principios
- 6.6 IP móvil
- 6.7 Gestión de la movilidad en redes celulares
- 6.8 Tecnología inalámbrica y movilidad: impacto sobre los protocolos de las capas superiores

## Características de los enlaces inalámbricos

A diferencia de los enlaces cableados: intensidad decreciente de la señal, interferencias, propagación multicamino, más vulnerable frente a ataques.

El receptor recibe la señal original + ruido:
- SNR: relación señal ruido (Signal-to-Noise Ratio). Cociente entre la potencia de la señal y la potencia del ruido (se suele expresar en dB). Con un SNR mayor, es más fácil extraer la señal original.
- Incrementando la potencia de emisión: aumenta la SNR, pero también aumenta el consumo de potencia (valioso en terminales móviles) y la interferencia producida sobre otras fuentes.

→ El canal radioeléctrico es muy agresivo con la señal. → La tasa de error de bit (BER, Bit Error Rate) será mayor que la que se tiene en redes cableadas.

## Características de los enlaces inalámbricos (continuación)

Relación entre BER y SNR:
- Aumentando potencia emisión → Aumenta SNR → Disminuye BER.
- Para una SNR, el empleo de una modulación de mayor tasa de bit tendrá una BER mayor.
- Por eso, según las características del canal es bueno cambiar la modulación dinámicamente. Adaptación dinámica de la velocidad para optimizar compromiso velocidad vs. robustez.

## Características de las redes inalámbricas

*(dos diagramas: pérdida de señal debido a un obstáculo, y pérdida de señal por la distancia)*

**Problema de la estación oculta**

A y B se escuchan. B y C se escuchan. Pero A y C no se escuchan. Si A está transmitiendo a B, C no lo sabe, por lo que C puede empezar a transmitir a B y provocar una interferencia.

## Índice

- 6.1 Introducción
- 6.2 Características de las redes y enlaces inalámbricos
- 6.3 WiFi: redes LAN inalámbricas IEEE 802.11
- 6.4 Acceso celular a Internet
- 6.5 Gestión de la movilidad: principios
- 6.6 IP móvil
- 6.7 Gestión de la movilidad en redes celulares
- 6.8 Tecnología inalámbrica y movilidad: impacto sobre los protocolos de las capas superiores

## Estándares WiFi

De entre todos los estándares para LAN inalámbricas (WLAN) ha vencido IEEE 802.11

| Estándar | Banda de frecuencia | Velocidad máxima | Velocidad efectiva |
|---|---|---|---|
| 802.11b | 2,4 GHz | 11 Mbps | 6 Mbps |
| 802.11a | 5 GHz | 54 Mbps | 31 Mbps |
| 802.11g | 2,4 GHz | 54 Mbps | 12 Mbps |
| 802.11n | 2,4 y 5 GHz | >200 Mbps | >200 Mbps |

## Aspectos generales

**Flexibilidad**
- Movilidad: salas de reuniones, aulas, campus, hogar,…
- Uso compartido: hot spots, cafés, aeropuertos, congresos,…
- No se requiere infraestructura adicional al añadir nuevos usuarios
- En edificios históricos, menos impacto de cableado
- Ancho de banda limitado: medio compartido
- Seguridad menor: red expuesta físicamente

**Aplicaciones**
- Ampliaciones de redes LAN
- Interconexión de edificios
- Acceso nómada
- Formación de redes ad hoc
- Cobertura de zonas sin infraestructuras

## Medios Físicos

- Infrarrojo: permite comunicaciones a 1-2 Mbps. Los elementos que se comunican deben tener visión directa. Es difícil que pinchen la señal.
- Radio: funciona en la banda de 2.4 Ghz y también en la de 5 Ghz, ambas bandas libres. Se consiguen velocidades de 1-2-5.5-11-55 e incluso >100 Mbps. Se usan varios canales que pueden cambiar de manera pseudoaleatoria (hay algo de seguridad).
- Empleando antenas direccionales conseguimos: minimizar interferencias; mayores alcances (enlaces punto a punto a decenas de kilómetros a bajo coste).

## Uniendo 802.11 con 802.3

*(diagrama de un punto de acceso uniendo una red 802.11 (inalámbrica) con una red 802.3 (Ethernet cableada); la imagen no sobrevivió a la extracción OCR)*

## Arquitectura

- IEEE 802.11 define las capas física y de enlace de datos.
- Tipos básicos de equipos:
  - Una o más estaciones inalámbricas
  - Una estación base → AP (puntos de acceso)
- Servicios:
  - BSS (Basic Service Set): forman una célula.
    - Estaciones sin punto de acceso: red ad hoc.
    - Estaciones con punto de acceso: red de infraestructura.
  - ESS (Extended Services Set): dos o más BSS con APs unidos mediante una red de distribución (habitualmente cableada, ej. Ethernet).

## Arquitectura (continuación)

*(diagramas ilustrando un BSS en modo Ad hoc, un BSS en modo Infraestructura, y un ESS formado por varios BSS de infraestructura; ejemplo: Eduroam)*

## Canales y asociación

Nos centramos en IEEE 802.11b/g. Al instalar un AP:

- Asignación de SSID (Identificador de Conjunto de Servicio – Service Set IDentifier): los SSID son los nombres de red que aparecen en la lista de redes WiFi accesibles por un dispositivo.
- Asignación de canal: en la banda de 2,4GHz-2,485GHz hay 11 canales parcialmente solapados. 2 canales no están solapados si están separados por 4 o más canales.

Dos formas de asociarse con un AP: exploración pasiva o exploración activa. Puede existir autenticación. Típicamente emplea DHCP para obtener una dirección IP.

## Exploración pasiva

*(la diapositiva original etiqueta erróneamente esta sección como "Tema 3: Redes inalámbricas y móviles" en vez de Tema 6, como el resto de la presentación)*

AP emite tramas baliza (beacon) que contienen dirección MAC y SSID. Host inalámbrico recorre los 11 canales buscando las tramas baliza.

Pasos:
1. AP envían tramas baliza
2. H1 envía una trama de solicitud de asociación al AP seleccionado
3. AP envía a H1 una trama de respuesta de asociación

## Exploración activa

Host inalámbrico difunde una trama de sondeo que reciben los AP.

Pasos:
1. Difusión desde H1 de una trama de solicitud de sondeo
2. Envío de tramas de respuesta de sondeo desde los AP
3. H1 envía una trama de solicitud de asociación al AP seleccionado
4. AP envía a H1 una trama de respuesta de asociación

## Capa MAC IEEE 802.11

- Protocolo de acceso múltiple: CSMA/CA (Collision Avoidance).
- Utilización de RTS (Request to Send) y CTS (Clear to Send).
- CSMA: cada estación sondea el canal antes de transmitir y se abstiene cuando está ocupado. Las tramas se transmiten en su totalidad.
- No se implementa CSMA/Collision Detect (CSMA/CD) porque:
  - La señal puede tener potencias tan diferentes que no es fácil detectar una colisión.
  - Pueden no detectarse colisiones debido al problema de la "estación oculta" (hidden station).

## Capa MAC

Dos subcapas MAC:
- DCF: Distributed Coordination Function (función de coordinación distribuida). Es la usada habitualmente de facto.
- PCF: Point Coordination Function (función de coordinación puntual) (No se usa). Opcional (sólo se puede usar en red de infraestructura) para datos con requerimientos temporales especiales o de alta prioridad. Se hacen consultas (polling) a cada estación. PCF tiene prioridad sobre DCF. Para que las estaciones que usen DCF no se queden sin acceso se establecen periodos para PCF y DCF.

*(diagrama de pila de protocolos: capa de enlace de datos con IEEE 802.2 LLC arriba, y la subcapa MAC —PCF y DCF— debajo; capa física con FHSS, DSSS, infrarrojo, OFDM,…)*

## Capa MAC: DCF

Pasos:
1. Si canal inactivo, transmite la trama después de un tiempo DIFS (Distributed InterFrame Space).
2. Si canal ocupado, pone un temporizador (backoff) aleatorio que efectúa una cuenta atrás mientras el canal esté libre y se congela mientras el canal esté ocupado.
3. Cuando vence el temporizador (sólo pasa cuando el canal libre) se transmite la trama completa y se espera un ACK.
4. Si se recibe ACK: trama enviada correcta. Si tiene otra trama, vuelta a 1.
5. Si no se recibe ACK, vuelta a 2, pero con backoff doble al anteriormente usado.

Nota: un ACK se envía siempre tras un tiempo SIFS (Short InterFrame Space) después de recibir una trama de datos. SIFS<DIFS.

## Capa MAC: DCF con RTS/CTS

Para tratar el problema de la estación oculta se introducen las tramas:
- RTS (Request to Send): solicitud de transmisión.
- CTS (Clear to Send): preparado para enviar.

Funcionamiento:
1. H1 transmite RTS: la escuchan todas las estaciones en su área de cobertura.
2. AP responde con CTS: la escuchan todas las estaciones en su área de cobertura.
3. H2 (que ocasionaba el problema de la estación oculta) se abstiene de transmitir el tiempo que se indica en CTS.

## Capa MAC: DCF con RTS/CTS — Puntualizaciones

- RTS puede colisionar con trama transmitida por estación oculta. Mal menor ya que su longitud es pequeña; tiempo desperdiciado de Tx pequeño.
- Configuración RTS/CTS depende del canal, nº de nodos, estaciones ocultas… Valores óptimos difíciles de saber a priori.

*(diagrama indicando que tanto RTS como CTS se transmiten en "Broadcast" y que "todas las estaciones reciben CTS"; la disposición exacta no se pudo recuperar de la extracción OCR)*

## Modo DCF: ejemplo de transmisión

*(secuencia de 5 diapositivas mostrando la animación paso a paso de un ejemplo de transmisión en modo DCF entre cuatro estaciones —A, B, C, D—, incluyendo una nota sobre que las tramas "llevan el tiempo de transmisión"; el contenido visual de esos pasos no sobrevivió a la extracción OCR)*

## Modo DCF (Cont.)

¿Cómo se evita que otras estaciones ocupen el canal?

- Cuando C detecta que A quiere enviar algo: se inhibe y marca su canal virtual como ocupado. ¿Cuánto? Tanto como dura CTS+Datos+ACK.
- Cuando D detecta que B está listo para recibir (problema estación oculta): hace lo mismo que C, inhibiéndose. ¿Cuánto? Tanto como dura Datos+ACK.

Las señales NAV (Network Allocation Vector) no son señales reales, sino que son marcas que utilizan las estaciones.

## Modo DCF: tasa de error

Problema con la alta tasa de error que hay en sistemas de Tx por radio.

Si la probabilidad de error en un bit es p, la probabilidad de recibir correctamente una trama de N bits es (1-p)^N.

- Si p=10⁻⁶ y N=18768: probabilidad de trama correcta = 0.98
- Si p=10⁻⁴, con el mismo valor de N: prob. de trama correcta = 0.15. Incluso en el primer caso, un 2% de las tramas tendrían errores, lo que supone muchas retransmisiones.

En 802.11 se permite enviar tramas largas en paquetes más pequeños, cada uno con su CRC, de manera que, si hay un error, sólo se retransmite ese sub-paquete.

## Modo DCF: tasa de error (Cont.)

*(diagrama de la fragmentación de una trama y su NAV inicial; la imagen no sobrevivió a la extracción OCR)*

## Modo DCF: tasa de error (Cont. II)

En este caso, el NAV inicial se produce como en el caso anterior, pero con la duración de uno de los fragmentos.

Después, las estaciones C y D van autogenerándose NAV's a medida que leen que hay más fragmentos (se va indicando mediante bits de control si es el último fragmento o si vienen más).

Hay unos números de secuencia dentro de esta partición de tramas, para poder controlar las pérdidas de un sub-paquete.

## Formato trama MAC

*(diagrama de la trama MAC 802.11, con campos medidos en bytes y bits)*

Duración: tiempo que se va a ocupar el canal (en tramas de datos, RTS y CTS).

4 direcciones que habitualmente son:
1. Dirección del Receptor (Rx)
2. Dirección del Transmisor (Tx)
3. Dirección del servidor
4. Dirección del cliente (sólo en modo puente, Wireless Distribution System, WDS)

Secuencia: para numerar fragmentos e identificación.

CRC-32 para detección de errores.

## Formato trama MAC (continuación)

Control de trama, con 11 subcampos:
- Versión: permite que 2 versiones de protocolo funcionen en la misma celda.
- Tipo: gestión (00), control (01) o datos (10).
- Subtipo: Ej. tramas de control: RTS (1011), CTS (1100) o ACK (1101).
- Hacia AP y Desde AP: indican si la trama va o viene de la red troncal que comunica celdas.
- MF: indica si hay más fragmentos.
- Retransmisión: indica que esta trama ha sido retransmitida de nuevo.
- Gestión de Potencia: usado para hibernar o sacar de hibernación a un terminal.
- Más datos: el emisor tiene más tramas para el receptor.
- WEP: indica que el cuerpo de la trama está codificado con WEP.
- Rsvd: tramas deben procesarse en orden estricto de llegada. No usado.

## Direccionamiento en 802.11

DA = DestinationAddress, SA = SourceAddress

*(diagrama mostrando una estación origen (SA) enviando a través de AP-A (tráfico "ToAP") hasta AP-B, que reenvía al destino (DA) como tráfico "FromAP")*

| Función | ToAP | FromAP | Address1 (Rx) | Address2 (Tx) | Address3 |
|---|---|---|---|---|---|
| ToAP | 1 | 0 | AP-A | SA | DA |
| FromAP | 0 | 1 | DA | AP-A | SA |

## Direccionamiento en 802.11 (continuación)

DA = DestinationAddress, SA = SourceAddress

*(diagrama mostrando una estación origen (SA) enviando a través de un único Access Point hasta un Server (DA))*

| Función | ToAP | FromAP | Address1 (Rx) | Address2 (Tx) | Address3 |
|---|---|---|---|---|---|
| ToAP | 1 | 0 | AP | SA | DA |
| FromAP | 0 | 1 | DA | AP | SA |

## Direccionamiento en 802.11 — Ejemplo

*(diagrama de una red con H1 (host inalámbrico) → AP → R1 (router) → Internet)*

- AP → R1: trama 802.3 — Dirección destino: R1 MAC addr; Dirección origen: H1 MAC addr
- H1 → AP: trama 802.11 — Dirección 1: AP MAC addr; Dirección 2: H1 MAC addr; Dirección 3: R1 MAC addr

## Direccionamiento en 802.11 (WDS)

*(diagrama mostrando un Client (SA) conectado a AP-A y un Server (DA) conectado a AP-B, comunicándose a través de un enlace WDS entre AP-A y AP-B)*

| Función | ToAP | FromAP | Address1 (Rx) | Address2 (Tx) | Address3 | Address4 |
|---|---|---|---|---|---|---|
| WDS | 1 | 1 | AP-B | AP-A | DA | SA |

## Direccionamiento en 802.11 (continuación II)

En Ad-hoc las estaciones usan un BSSID (Basic Service Set IDentifier) generado a partir de su MAC.

En infraestructura se usa para identificar tramas de un BSSID y permitir varios AP en una misma zona (tramas de difusión).

## Movilidad dentro de una subred IP

Al seguir dentro de la subred (cambio de capa 2) → mantiene dirección IP. Sin embargo, los conmutadores deben aprender la nueva localización.

H1 detecta que la señal de AP1 se debilita y la de AP2 llega con más intensidad. H1 se desasocia de AP1 y se asocia con AP2:
- Mantiene dirección IP
- Mantiene sesiones TCP activas
- Muy posible pérdida de datos en el proceso de cambio de AP

## Gestión de la potencia en 802.11

Potencia: recurso valioso en dispositivos móviles. Los nodos no siempre tienen que estar activos.

La estación inalámbrica indica al AP que va a pasar al estado dormido hasta la siguiente trama baliza:
- Poniendo a 1 el bit "Gestión de potencia".
- Pone un temporizador que vence justo antes de la baliza (requiere 250µs para despertar).

El AP sabe que no puede enviar tramas a ese nodo hasta que despierte:
- Almacena en un buffer las tramas que le llegan para ese nodo.
- La trama baliza indica los nodos para los cuales tiene tramas que han llegado mientras dormía.
- Si no tiene tramas, vuelve a dormir. Si tiene tramas, las solicita al AP mediante un mensaje de sondeo.

## Bluetooth

Bluetooth es una tecnología para WPAN. Forma redes ad hoc. Diseñada para comunicaciones entre PCs, periféricos, agendas electrónicas, electrodomésticos, auriculares, teléfonos móviles etc.

Bluetooth fue ideado por Ericsson a finales de los 90. Ahora, la tecnología Bluetooth es la implementación de IEEE 802.15.

## Bluetooth (continuación)

El nombre Bluetooth viene del rey danés Harold Bluetooth, quien gobernó entre 940 y 981 a daneses y noruegos.

Ventajas:
- Bajo consumo
- Bajo coste
- Pequeño tamaño

Las redes Bluetooth pueden conectarse a Internet si uno de los dispositivos tiene esta capacidad.

## Arquitectura de Bluetooth

Características principales:
- 1Mbps (725 kbps en la práctica)
- Funciona en la banda 2.4GHz. Interferencia con IEEE 802.11.
- Alcance: 10m aprox.

Se definen dos tipos de redes:
- Piconets: un maestro, varios esclavos. TDD.
- Scatternets (unión de piconets)

## Arquitectura de Bluetooth: piconets

Puede tener hasta 8 dispositivos: 1 maestro (sólo puede haber uno), el resto son esclavos. Las comunicaciones dentro de una piconet son entre maestro-esclavo (no posible comunicaciones directas esclavo-esclavo).

*(diagrama de una piconet con un nodo Primario y varios nodos Secundario)*

## Arquitectura de Bluetooth: piconets (continuación)

Dentro de una piconet, el canal se comparte empleando TDD, donde el maestro emplea un protocolo de sondeo para asignar ranuras temporales a los nodos esclavos.
- El maestro puede transmitir en cada slot impar. Un esclavo sólo puede transmitir cuando el maestro se haya comunicado con él en el slot anterior.

Además de los 8 dispositivos, pueden haber hasta 255 en estado aparcado: sincronizados pero sin comunicarse. Pueden pasar a activos si alguno de los 8 activos pasan a aparcados.

## Arquitectura de Bluetooth: scatternets (I)

Combinación de piconets. Un dispositivo puede pertenecer a dos piconets; un dispositivo secundario en una piconet puede ser primario en otra.

Todas las piconets emplean el mismo espectro: colisiones entre piconets; para disminuirlas se emplean saltos de frecuencia.

*(diagrama de dos piconets combinadas —scatternet—, cada una con un nodo Primario y varios Secundario, y un nodo Primario/Secundario compartido entre ambas)*

## Arquitectura de Bluetooth: scatternets (II)

Comunicación entre piconets: se recomienda que se haga a través de un esclavo que pertenezca a las 2 piconet, actuando como puente. Si lo hace el maestro se bloquean las comunicaciones interiores el tiempo que esté desunido a la red.

Al reenviar una trama:
1. Recibe la trama por la red 1
2. Desunirse de la red 1
3. Unirse a la red 2
4. Retransmitir la trama

## Capa física de Bluetooth

Dispositivos de baja potencia: alcance 10m aprox. Banda de 2.4GHz: se divide en 79 canales de 1MHz.

Los secundarios sincronizan su reloj y la secuencia de saltos de frecuencia (frequency hopping) con el maestro.

FHSS: Frequency-Hopping Spread Spectrum. Para minimizar interferencias de otras piconets u otras redes como IEEE 802.11. 1600 saltos de frecuencia por segundo (1/1600 = 625µs en cada frecuencia).

## Alternativas a Bluetooth

**ZigBee**
- Muy bajo consumo
- 2¹⁶ nodos
- Velocidad < 256 kbps
- Distancia de 70 m
- Usos: control remoto, redes de sensores

**Ultra-wide band**
- Velocidad 500 Mbps
- Usos: transmisión de imágenes sin cable

**DLNA (Digital Living Network Alliance)**
- Velocidad 500 Mbps
- Usos: transmisión de imágenes sin cable

## WiMAX

WiMAX: Worldwide Interoperability for Microwave Access. Tecnología WMAN (podría llegar a WWAN).

WiMAX Forum: asociación sin ánimo de lucro formada por decenas de empresas comprometidas con el cumplimiento de IEEE 802.16.

Ventajas competitivas:
- Relativo bajo coste de implantación
- Gran alcance
- Altas velocidades
- No necesaria visión directa
- Puede transportar IP, TDM, T1/E1, ATM, FR,…

Aplicaciones:
- Redes metropolitanas de acceso a Internet
- Banda ancha a áreas rurales
- Comunicaciones internas en el mundo empresarial

IEEE 802.16e permite la movilidad de los terminales.

## WiMAX (continuación)

Al igual que 802.11 y las redes celulares:
- Estación base coordina transmisión en ambos sentidos point-to-multipoint (BS→hosts, y hosts→BS). Utiliza antenas omnidireccionales para esto.
- Comunicación punto a punto entre estaciones base.

## WiMAX (continuación II)

Emplea TDM (aunque también tiene la opción de FDM).

- DL (Down Link): Descendentes. Informa a qué estación está dirigida cada ráfaga posterior y sus propiedades físicas: modulación, codificación,… Se pueden emplear parámetros diferentes para ráfagas diferentes → optimizado para cada receptor en cada momento.
- UL (Up Link): Ascendentes. Informa de la cantidad de tiempo que se le permite transmitir a cada estación y cuándo.

## Referencias

- J. Kurose & K.W. Ross, "Redes de Computadoras: un Enfoque Descendente" (5ª Ed.), Pearson Educación, 2010.
- A.S. Tanenbaum "Redes de ordenadores, cuarta edición". Editorial Prentice-Hall, 2003.
- J. Berrocal et al. "Redes de acceso de Banda Ancha", Ministerio de Ciencia y Tecnología, 2003.
- R. Flickenger "Building Wireless Community Networks" Editorial O'reilly, 2002.
- M. Gast "Redes Wireless 802.11" Editorial O'Really, 2005.

## Trabajo personal

- Preparación Prueba Parcial 2
- PS3 (S7,S8,S9)
