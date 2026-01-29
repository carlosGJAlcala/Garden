---
title: "2024 12 20 Evoting Y Historia Telefonia Movil"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

### eVoting


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

#### Sistema de Estonia

El sistema de voto electrónico de Estonia utiliza la autenticación mediante PKI (Infraestructura de Clave Pública) y firma digital. Los datos se cifran utilizando TLS. Para garantizar el anonimato, se emplea un sistema de doble sobre. Además, el sistema permite la verificación para comprobar si el voto ha sido emitido correctamente. El conteo de votos se realiza mediante técnicas de homomorfismo, y después de cada elección se lleva a cabo una auditoría independiente. Sin embargo, no se puede afirmar que el sistema sea totalmente seguro, ya que está expuesto a vulnerabilidades y al factor humano.

#### Sistema de Noruega

Introducido en 2011, este sistema se cerró en 2014 debido a crecientes preocupaciones sobre la seguridad y la confianza pública. Utilizaba una red de mezcla (mixnet) para garantizar el anonimato en lugar de un sistema de doble sobre. El resto de sus características eran similares al sistema de Estonia. Los algoritmos empleados incluían transporte TLS y firma digital. Aunque tenía ventajas, enfrentó una gran desconfianza pública, y su complejidad y vulnerabilidad ante ataques internos (insiders) contribuyeron a su declive.

#### Sistema de Brasil

Introducido en el año 2000, el sistema de Brasil combina hardware dedicado y software propietario desarrollado localmente. Utiliza autenticación múltiple, con RSA de 2048 bits para el cifrado y módulos HSM para almacenar las claves de autenticación de doble factor. Una ventaja destacada es la rapidez en comparación con el voto en papel. Sin embargo, carece de un sistema de verificación independiente del voto, lo que aumenta el riesgo de manipulación interna y dificulta las auditorías.

---

### Digivote y el incidente de Bélgica

El sistema de teatro DigiVote almacenaba votos en tarjetas digitales. En 2003, un rayo cósmico afectó el sistema de voto electrónico en Bélgica, lo que expuso la falta de controles de integridad y verificación física en el sistema.

---

### Historia de la telefonía móvil

#### Primera Generación (1G)

La 1G utilizaba canales únicos en un esquema de división celular. Era un sistema analógico donde las celdas podían reutilizar frecuencias no adyacentes. Se empleaba multiplexación FDMA y los sistemas AMPS y AMTS permitían comunicaciones básicas. Una gran vulnerabilidad era la facilidad con la que se podían clonar teléfonos.

#### Segunda Generación (2G)

Introdujo mejoras significativas con FDMA, TDMA y CDMA, permitiendo comunicación internacional. CDMA destacó por su eficiencia. Evolucionó a GPRS y EDGE, marcando el cambio de circuitos a paquetes y la integración de características multimedia.

#### Tercera Generación (3G)

Aumentó la eficiencia y mejoró los protocolos de cifrado, proporcionando mayor velocidad y seguridad.

#### Cuarta Generación (4G)

Mejoró la gestión de conexiones y enfrentó amenazas como intercepciones y ataques DDoS, implementando protocolos de anonimato como solución.

#### Quinta Generación (5G)

Introduce la virtualización de redes y mejora la seguridad con autenticación multifactor y cifrado avanzado como NEA y TLS. Permite comunicaciones VoIP, lo que abre la puerta a ataques de phishing y vishing, mientras que la configuración de firewalls se vuelve crítica. Las amenazas incluyen intercepción de llamadas y posibles fallos en la protección de datos.

---
La principal diferencia entre un **bit** clásico y un **qubit** (bit cuántico) radica en cómo representan y procesan la información:

### 1. **Bits clásicos**

- Los bits son la unidad básica de la información en los sistemas tradicionales.
- Representan un estado binario: 0 o 1.
- En los circuitos clásicos, se implementan mediante voltajes, niveles eléctricos, o señales digitales que representan claramente un estado fijo.

### 2. **Qubits**

- Los qubits son la unidad básica de la información en los sistemas cuánticos.
- Pueden representar simultáneamente 0, 1 o una **superposición** de ambos estados (una combinación lineal de 0 y 1).
- Su estado se describe por una función de onda y depende de principios cuánticos como la **superposición** y el **entrelazamiento**.
- Se implementan en sistemas cuánticos como electrones, átomos, o **fotones**.

---

### En el contexto del uso de fotones y bases en comunicación cuántica:

1. **Bases de medición**:
    
    - En un sistema cuántico, como el protocolo BB84 (una base común en criptografía cuántica), los fotones representan los qubits.
    - Las bases son como "referencias" para medir el estado del fotón. Las más comunes son:
        - **Base estándar (+)**: Estados rectilíneos (|0⟩ y |1⟩).
        - **Base diagonal (×)**: Estados en ángulo de 45° (|+⟩ y |−⟩).
2. **Generación de la clave**:
    
    - **Alice** envía fotones en estados aleatorios y selecciona bases aleatorias para codificarlos.
    - **Bob**, al recibir los fotones, usa también bases aleatorias para medirlos.
    - Solo las mediciones hechas con la misma base que usó Alice serán útiles. Alice y Bob descartan los resultados de bases distintas y conservan los coincidentes para generar una clave compartida.
3. **Verificación de seguridad**:
    
    - Para detectar si un tercero (un espía) intenta interceptar los fotones, Alice y Bob comparan una fracción de los resultados para verificar la tasa de error. Si es alta, puede haber una intervención externa.
    - Esto se basa en el principio de **no clonación cuántica**, que impide que un observador copie exactamente el estado de un qubit sin alterarlo.
4. **Limitaciones actuales**:
    
    - Aunque los canales cuánticos son muy prometedores, las implementaciones reales enfrentan problemas:
        - **Ruido en el canal**: Afecta la fidelidad de los fotones.
        - **Modelado de los fotones**: Las imperfecciones en la preparación o detección de los estados cuánticos pueden permitir ataques.
    - La criptografía cuántica actualmente sirve como **inicialización** para un futuro en el que las redes cuánticas sean más robustas y seguras.
- la clave  es un cuarto  porque una mitad se va eliguiendo y la otra mita se va detectar entonces se queda en cuarto

El contenido sobre **SUCI** y **SUPI** en redes 5G trata temas fundamentales de seguridad y cómo la arquitectura 5G soluciona problemas de generaciones anteriores. Aquí tienes una versión corregida, organizada y explicada para mayor claridad:

---

### Redes 5G y Identificadores: SUPI y SUCI

#### Problema en redes previas (4G)

En las redes 4G, el **IMSI** (Identificador Internacional de Suscriptor Móvil) se transmite en texto plano al conectarse el dispositivo al eNodeB (la estación base). Esto lo hace vulnerable a ataques como el **IMSI Catcher**, donde un atacante puede interceptar el identificador y rastrear o suplantar al usuario.

#### Solución en 5G

En redes 5G, se introducen los conceptos de **SUPI** y **SUCI** para solucionar este problema:

1. **SUPI (Subscription Permanent Identifier)**:
    
    - Es un identificador único internacional de usuario.
    - Formato típico para dispositivos móviles:
        - **IMSI**: Que incluye:
            - **MCC (Mobile Country Code)**: Código de país.
            - **MNC (Mobile Network Code)**: Código del operador.
            - **MSIN (Mobile Subscription Identifier Number)**: Identificador del usuario.
        - Ejemplo: `IMSI-MCC-MNC-MSIN`.
    - Aunque es único y útil, el **SUPI** no se transmite directamente por la red para evitar vulnerabilidades.
2. **SUCI (Subscription Concealed Identifier)**:
    
    - Es el **SUPI cifrado**, diseñado para proteger la privacidad del usuario.
    - Basado en el esquema de cifrado **ECIES (Elliptic Curve Integrated Encryption Scheme)**.
    - Cada **SUCI** es único para cada sesión, lo que dificulta su reutilización o análisis por parte de atacantes.

---

### Esquema de ECIES y Cifrado del SUCI

El **SUCI** se construye cifrando el **SUPI** con una clave pública de la red de origen, utilizando el esquema **ECIES**. Este proceso incluye:

- **Input del SUPI**:
    - Tipo de SUPI.
    - Identificador de red local (**Home Network Identifier**).
    - Indicador de enrutamiento (**Routing Indicator**).
    - Esquema de protección utilizado (**Protection Scheme ID**).
    - Identificador de la clave pública de la red (**Home Network Public Key ID**).
- **Cifrado**:
    - Se utiliza la clave pública de la red para cifrar el identificador, generando un **SUCI** que solo puede ser descifrado por la red autorizada.

---

### Seguridad en 5G y Protocolo AKA

1. **Protocolo de Autenticación AKA**:
    
    - Permite autenticación mutua entre el dispositivo y la red, además de un acuerdo de claves.
    - La **USIM** verifica si los datos son correctos y genera una respuesta de autenticación (**Authentication Response**).
    - El sistema detecta inconsistencias (como ataques de sincronización fallida) y reacciona.
2. **Ataques en 5G**:
    
    - **SUCI Cracker**:
        - Aparece cuando la arquitectura es **standalone** (combinación de 4G y 5G), donde algunos componentes no son completamente 5G y persisten vulnerabilidades heredadas.
    - **Ataques de repetición**:
        - Para mitigarlos, se usa:
            - **SQN (Sequence Number)**: Número secuencial para detectar datos reutilizados.
            - **Temporizadores estrictos**: Limitan la validez de valores como **RAND** y **AUTN**, evitando que los atacantes reutilicen información capturada.

---

### Ventajas de 5G frente a 4G

- **Privacidad mejorada**: El **SUPI** ya no se transmite en texto plano gracias al cifrado del **SUCI**.
- **Resiliencia a ataques**: Con mecanismos como SQN y tiempos de expiración, los ataques de repetición son mucho más difíciles.
- **Cifrado robusto**: ECIES proporciona seguridad avanzada, dificultando la intercepción y descifrado de identificadores.

Aquí tienes una descripción organizada y mejorada de los conceptos que planteaste, incluyendo los **ataques laterales**, **métodos de sonido** y la introducción a la **criptografía de posicionamiento cuántica (QPV)**:

---

### **Ataques Laterales (Side-Channel Attacks)**

Los ataques laterales son técnicas que explotan características físicas o indirectas de un sistema, en lugar de vulnerar el algoritmo criptográfico en sí. A continuación, se detallan dos ejemplos destacados:

#### 1. **Ataques basados en tiempo**

- **Descripción**:
    - Algunos sistemas de validación (como la introducción de un PIN bancario) comparan entrada por entrada para verificar la clave. Dependiendo del tiempo que tarda en responder, un atacante puede deducir el carácter o bit correcto en cada paso.
- **Cómo funciona**:
    - Si el sistema verifica el PIN carácter por carácter:
        - Un tiempo de respuesta más rápido sugiere que los primeros caracteres fueron correctos.
        - Un tiempo más largo indica que el proceso llegó a un error en la comparación.
    - Los atacantes pueden medir estas diferencias utilizando herramientas de alta precisión (cronómetros digitales o software).
- **Mitigación**:
    - Comparaciones constantes en tiempo (independientemente de la entrada correcta o incorrecta).
    - Introducir retardos artificiales para evitar que el tiempo de respuesta revele información.

#### 2. **Ataques por sonido**

- **Descripción**:
    - Los teclados físicos emiten sonidos específicos dependiendo de las teclas presionadas. Un atacante puede grabar estos sonidos, procesarlos con herramientas como la **Transformada de Fourier**, y deducir qué teclas se pulsaron.
- **Cómo funciona**:
    - El sonido de cada tecla tiene una frecuencia y amplitud únicas.
    - Con suficientes datos, se pueden mapear estas frecuencias a caracteres específicos.
    - Ejemplo: Capturar el sonido de alguien escribiendo una contraseña en un teclado físico.
- **Desafíos**:
    - Requiere un micrófono de alta calidad cercano al objetivo.
    - Es complicado asociar sonidos a teclas, ya que depende del tipo de teclado y su acústica.
- **Mitigación**:
    - Uso de teclados silenciosos o mecanismos físicos que reduzcan el ruido.
    - Generar ruido de fondo para dificultar la captura de sonidos específicos.

---

### **Criptografía de Posicionamiento Cuántica (Quantum Position Verification - QPV)**

La **criptografía cuántica de posicionamiento** es una rama emergente de la criptografía que aprovecha los principios de la física cuántica para verificar la posición de un usuario o dispositivo en el espacio.

#### Conceptos clave:

1. **Objetivo**:
    
    - Garantizar que un usuario está físicamente en un lugar específico, utilizando principios cuánticos como la superposición y el entrelazamiento.
    - Ejemplo: Probar que un usuario está en una ubicación exacta para acceder a un servicio.
2. **Funcionamiento**:
    
    - Basado en protocolos donde un dispositivo receptor mide propiedades cuánticas (como el estado de los fotones) que solo pueden generarse desde un lugar específico.
    - La información cuántica (qubits) no puede copiarse debido al principio de **no clonación cuántica**, lo que garantiza la autenticidad.
3. **Ejemplo de protocolo**:
    
    - **Protocolo de tiempo-cuántico**:
        - Una señal cuántica se envía al dispositivo receptor.
        - El tiempo que tarda la señal en regresar (round-trip time) se utiliza para verificar la distancia y la posición.
        - Si un atacante intenta interceptar la señal y reenviarla, alterará los estados cuánticos, haciendo que el intento sea detectable.
4. **Ventajas**:
    
    - Resistente a ataques de interceptación.
    - Basado en principios físicos fundamentales, lo que lo hace muy difícil de vulnerar.
5. **Desafíos actuales**:
    
    - Requiere equipos avanzados, como detectores y emisores de fotones precisos.
    - Vulnerabilidades en implementaciones prácticas (ruido o limitaciones de los canales cuánticos).

---

### **Relación con Fedora y Subatomic**

El uso de **Fedora** y herramientas como **Subatomic Editor** puede relacionarse con la implementación y análisis de criptografía o simulación de protocolos cuánticos. Si estás interesado en proyectos específicos, herramientas o ejemplos relacionados con este entorno, puedo ayudarte a explorarlos.

scure chat aplicacion hecha por misiego que utiliza rsa

