---
title: "Volting System"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---
### Tema 2: Requisitos de Seguridad en Sistemas de Votación Electrónica


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

#### 1. Requisitos Fundamentales de Seguridad

En el diseño de sistemas de votación electrónica, se establecen varias propiedades de seguridad fundamentales que son clave para garantizar la integridad, confidencialidad y accesibilidad del proceso electoral. Los requisitos más importantes incluyen:

- **Secreto del Voto**: Solo el votante debe conocer su elección, asegurando que el contenido de cada voto sea confidencial.
- **Legitimidad**: Solo los votantes registrados tienen permitido emitir un voto, asegurando que cada voto proviene de una fuente autorizada.
- **Elegibilidad**: Un votante puede emitir su voto una sola vez, y todos los votos emitidos deben ser genuinos.
- **Verificabilidad Individual**: Cada votante debe poder verificar que su voto fue correctamente registrado para el conteo.
- **Verificabilidad Universal**: Cualquier observador externo debe poder verificar que el recuento final refleja los votos emitidos de manera precisa.
- **Exactitud (Integridad)**: Los resultados publicados deben reflejar el conteo verdadero de todos los votos válidos.
- **Ausencia de Recibo**: No debe ser posible que el votante demuestre a terceros cómo votó, lo cual previene el intercambio o venta de votos.
- **Resistencia a la Coacción**: El sistema debe permitir que el votante emita su voto libremente incluso si parece cooperar con un coaccionador.
- **Robustez**: El sistema debe ser capaz de generar un resultado preciso incluso si ocurren ciertos niveles de fallos o corrupción.
- **Disponibilidad**: El sistema debe estar completamente operativo y accesible para todos los usuarios durante el periodo de votación.

#### 2. Conflictos e Interrelaciones entre los Requisitos de Seguridad

Algunos de estos requisitos están en tensión o conflicto entre sí, lo que representa desafíos importantes en el diseño del sistema:

- **Secreto del Voto vs. Verificabilidad Individual**: Mantener el secreto del voto puede dificultar que un votante verifique públicamente la exactitud del registro de su voto. Mientras el secreto es fundamental para la privacidad, la verificabilidad es esencial para la confianza en el sistema.
- **Ausencia de Recibo vs. Resistencia a la Coacción**: La resistencia a la coacción implica que el votante no pueda probar cómo votó, lo cual también respalda la propiedad de ausencia de recibo. Sin embargo, esta resistencia es difícil de lograr en esquemas de votación remota donde el entorno no es controlado.
- **Legitimidad y Elegibilidad**: Para que la elección sea legítima, solo los votantes autorizados deben votar, y cada uno debe poder hacerlo una sola vez. Esto puede requerir métodos adicionales de autenticación que garanticen tanto la identificación como la exclusividad del voto. Enfoques para Lograr la Seguridad en el Sistema

Para cumplir con estos requisitos de seguridad, los sistemas de votación electrónica suelen dividirse en dos partes:

1. **Front-end (Interfaz de Votación)**: En esta fase, los votantes interactúan con el cliente de votación para generar su voto encriptado y enviarlo al sistema de votación.
   - En este punto, se debe asegurar que el voto esté correctamente cifrado y que no revele la intención del votante, incluso si él intenta demostrarlo a otros.
   
2. **Back-end (Tanteo de Votos)**: Una vez que los votos se reciben, se realiza el conteo y se publica el resultado final.
   - En esta fase, se utilizan técnicas como **mixnets** y **cifrado homomórfico** para desasociar los votos de los votantes, asegurando que el proceso de desencriptado y conteo mantenga la privacidad del voto individual.

Ambas fases están diseñadas para cumplir con las propiedades de privacidad, resistencia a la coacción y exactitud de los votos【4†sourceisos de Seguridad en los Sistemas de Votación

No todos los sistemas de votación electrónica logran todos los requisitos de seguridad de manera absoluta. Dependiendo del contexto y de los recursos disponibles, algunos requisitos pueden priorizarse sobre otros:

- **Resistencia a la Coacción en Votación Remota**: En entornos de votación no supervisados (como el voto en línea), la resistencia a la coacción es más difícil de lograr ya que no existe control sobre el entorno en el que se emite el voto. En algunos casos, los administradores de votación pueden aceptar ciertos riesgos de coacción cuando se considera que estos no representan una amenaza significativa.
- **Accesibilidad vs. Secreto del Voto**: En sistemas diseñados para brindar accesibilidad a votantes con discapacidades, se pueden introducir ayudas adicionales (auditivas o visuales) que podrían comprometer parcialmente el secreto del voto. En estos casos, se deben implementar salvaguardas adicionales para minimizar el riesgo sin afectar la usabilidad del sistema.

La implementación de estos compromisos depende del contexto específico de cada elección, buscando siempre equilibrar la seguridad con la funcionalidad del sistema【4†source】 .
### Tema 3: Esquemas de Votación Verificables

Los esquemas de votación verificables están diseñados para garantizar la integridad y transparencia en el proceso electoral, permitiendo que tanto los votantes como observadores externos verifiquen que los votos se han emitido, registrado y contado correctamente. A continuación, se detallan los tipos de esquemas de votación verificables, sus componentes y técnicas de implementación.

#### 1. Componentes de Verificación en Esquemas de Votación

Los sistemas de votación verificables deben cumplir con tres componentes de verificación clave:

- **Verificación de intención (Cast-as-Intended)**: Asegura que el voto emitido representa fielmente la intención del votante. Esto permite que el votante verifique que el contenido cifrado del voto coincide con su elección.
- **Verificación de registro (Recorded-as-Cast)**: Permite que el votante confirme que su voto ha sido registrado en el sistema sin alteraciones.
- **Verificación de conteo (Counted-as-Recorded)**: Permite que cualquier persona (incluidos observadores externos) verifique que los votos registrados han sido correctamente contados en el resultado final de la elección.

#### 2. Esquemas Supervisados Verificables

Los **esquemas supervisados** se emplean en entornos controlados, como centros de votación, donde los votantes emiten su voto bajo supervisión. Algunos de los métodos de verificación más comunes en estos esquemas incluyen:

- **Método de "Cortar y Elegir" (Cut-and-Choose)**: Los votantes verifican la exactitud del proceso de encriptación auditando votos aleatorios antes de emitir el voto final. Este proceso probabilístico permite que el votante audite múltiples veces si lo desea, verificando la autenticidad del cifrado antes de emitir el voto real.
- **Pruebas Criptográficas Directas**: Estas pruebas permiten al sistema de votación generar un comprobante de que el cifrado del voto es correcto sin necesidad de auditorías adicionales. Ejemplo de este enfoque es el esquema **MarkPledge**, que genera una prueba criptográfica que permite al votante verificar que el sistema registró su intención de voto correctamente.

#### 3. Esquemas Remotos Verificables

Los **esquemas de votación remota** son utilizados en entornos no controlados, como en votaciones por Internet. Estos esquemas permiten al votante emitir su voto desde cualquier ubicación, lo cual facilita el voto a distancia pero introduce nuevos retos para la verificación y la privacidad del votante. Para estos casos, se han desarrollado métodos específicos:

- **Protección de Privacidad y Resistencia a la Coacción**: Dado que los entornos remotos son más susceptibles a la coacción, estos esquemas incluyen fases de registro en las que el votante obtiene credenciales únicas que le permiten proteger su voto.
- **Ejemplo de Sistema Helios**: Helios es un sistema de votación remota diseñado para entornos de bajo riesgo de coacción. Permite la verificación del registro y del conteo de los votos sin comprometer la privacidad. Sin embargo, en contextos de alto riesgo de coacción, puede no ser suficiente sin una infraestructura adicional.

#### 4. Técnicas Criptográficas en Esquemas de Votación Verificables

Las técnicas criptográficas avanzadas son esenciales para proporcionar verificación en los sistemas de votación electrónica sin comprometer el secreto y la integridad de los votos:

- **Mixnets**: Los mixnets son redes que re-cifran y mezclan los votos para desasociar el contenido de cada voto de su votante. Esto asegura que, aunque los votos se cuenten, no es posible vincular un voto específico con un votante individual. Los mixnets pueden emplear diferentes métodos de verificación, como **Randomized Partial Checking (RPC)**, que permite auditar el proceso de mezcla sin revelar el contenido de los votos.
- **Cifrado Homomórfico**: El cifrado homomórfico permite realizar operaciones (como la suma) directamente sobre los votos cifrados sin necesidad de desencriptarlos. Esto es útil en sistemas de votación que solo requieren contar los votos, ya que permite sumar todos los votos cifrados para obtener el resultado final sin comprometer la privacidad de cada voto individual.
- **Pruebas de Conocimiento Cero (Zero-Knowledge Proofs)**: Estas pruebas permiten que los votantes y el sistema verifiquen la exactitud de ciertas operaciones sin revelar información sensible, como la elección del votante. Por ejemplo, el **Protocolo de Schnorr** permite a un votante demostrar que su voto ha sido encriptado correctamente sin revelar su contenido.

#### 5. Ejemplos Destacados de Esquemas de Votación Verificables

Existen varios esquemas de votación que emplean estas técnicas y que son ampliamente estudiados y utilizados en la literatura. Algunos de los más notables incluyen:

- **MarkPledge**: Este sistema utiliza pruebas criptográficas que permiten a los votantes verificar que sus votos han sido cifrados y registrados correctamente, brindando además resistencia a la coacción. El sistema incluye varias verificaciones internas para garantizar que el contenido del voto cifrado sea el correcto, y los votantes pueden auditar sus propios votos.
- **Scantegrity II**: Diseñado para sistemas de votación de escaneo óptico, Scantegrity II utiliza códigos secretos en las papeletas de voto. Estos códigos permiten a los votantes verificar que su voto fue correctamente registrado y contado en el sistema, sin revelar el contenido del voto.
- **JCJ/Civitas**: Este sistema utiliza técnicas avanzadas de registro y cifrado para asegurar la privacidad y verificar el recuento, resistiendo tanto la coacción como la manipulación del proceso de votación. Los votantes pueden obtener credenciales que se utilizan para emitir votos en entornos controlados, protegiendo así la integridad del sistema en situaciones de alto riesgo de coacción.

### Tema 4: Bloques Constructivos en Sistemas de Votación Verificable

Los bloques constructivos o "building blocks" son los componentes criptográficos fundamentales que permiten la implementación segura y verificable de sistemas de votación electrónica. Estos bloques incluyen técnicas de cifrado, mecanismos de verificación, y sistemas de mezcla (mixnets), entre otros. Su uso es clave para garantizar la privacidad, integridad y verificabilidad de cada voto en el proceso electoral.

#### 4.1 Esquemas de Cifrado

El cifrado es esencial para proteger la privacidad del voto, permitiendo que los votos se almacenen y manipulen de forma segura sin exponer su contenido. En sistemas de votación, se emplean varios tipos de cifrado:

##### Cifrado RSA
El cifrado RSA se basa en el uso de dos números primos grandes \( p \) y \( q \), y se calcula un módulo \( n = p \times q \) y el valor de Euler \( \phi = (p - 1)(q - 1) \).

- **Clave Pública**: Se define como \( (n, e) \), donde \( e \) es un exponente de cifrado.
- **Clave Privada**: Calculada como \( d \), donde \( e \times d \equiv 1 \ (\text{mod } \phi) \).
- **Cifrado**: Para cifrar un mensaje \( m \), se calcula \( c = m^e \ (\text{mod } n) \).
- **Descifrado**: La recuperación del mensaje se realiza con \( m = c^d \ (\text{mod } n) \).
- **Propiedad Homomórfica**: RSA permite realizar multiplicaciones en el dominio cifrado. Si \( E(m_1) \) y \( E(m_2) \) son dos mensajes cifrados, se cumple que \( E(m_1) \cdot E(m_2) = E(m_1 \cdot m_2) \), lo que facilita la verificación de ciertas operaciones sin descifrar los votosifrado ElGamal
El esquema ElGamal es un sistema de cifrado probabilístico que utiliza operaciones de grupo en números primos. En este esquema, se selecciona un grupo cíclico \( G \) de orden \( q \) y un generador \( g \).

- **Clave Pública**: Es el valor \( y = g^x \ (\text{mod } p) \), donde \( x \) es el secreto del sistema.
- **Clave Privada**: Es \( x \).
- **Cifrado**: Para cifrar un mensaje \( m \), se elige un valor aleatorio \( r \) y se calcula el par cifrado \( (c_1, c_2) = (g^r, m \times y^r) \).
- **Descifrado**: El sistema descifra obteniendo \( m = c_2 / c_1^x \), aprovechando que el valor \( c_1^x = g^{xr} \) es conocido por la clave privada.
- **Propiedad Homomórfica**: ElGamal también permite operaciones homomórficas multiplicativas en el dominio cifrado, útil para el conteo seguro de votos cifrados sin desencriptarlos .

##### Paillier
El cifrado Paillier ofrece una propiedad homomórfica aditiva, lo cual es útil para sumar votos cifrados en sistemas de votación sin comprometer la privacidad del contenido de cada voto.

- **Configuración**: El sistema define un módulo \( n = p \times q \), y selecciona un número \( g \) de orden múltiplo de \( n \) en el espacio \( n^2 \).
- **Cifrado**: Para un mensaje \( m \), el cifrado se calcula como \( c = g^m \times r^n \ (\text{mod } n^2) \), donde \( r \) es un valor aleatorio.
- **Propiedad Homomórfica Aditiva**: La propiedad aditiva permite sumar los valores cifrados directamente. Si \( E(m_1) \) y \( E(m_2) \) son dos mensajes cifrados, \( E(m_1 + m_2) = E(m_1) \times E(m_2) \), lo que permite obtener el total de votos sin desencriptar cada voto individual .

### Aplicación dmas de Cifrado en Sistemas de Votación Verificable

Los esquemas de cifrado RSA, ElGamal y Paillier permiten construir sistemas de votación en los que:

1. **Privacidad**: La elección del votante permanece confidencial gracias al cifrado, y no puede ser revelada sin la clave privada.
2. **Verificación de Votos**: Las propiedades homomórficas de estos esquemas permiten realizar verificaciones de la suma o el producto de votos cifrados sin comprometer el secreto de cada voto individual.
3. **Eficiencia**: Cada esquema se adapta a distintos requisitos del sistema de votación. ElGamal, por ejemplo, permite operaciones probabilísticas y es útil para entornos donde el anonimato debe mantenerse durante el proceso de mezcla de votos.



### Tema 4.2: Técnicas de Compartición de Secretos y Umbrales

Las técnicas de **secret sharing** y **umbral** son esenciales en sistemas de votación verificables, donde la clave secreta (por ejemplo, la clave de descifrado) se distribuye entre múltiples participantes. Este enfoque permite que un subconjunto específico (quórum) de participantes coopere para recuperar el secreto sin que ninguna de las partes individuales tenga acceso completo a él. A continuación, se presentan los métodos y técnicas clave de esta categoría:

#### 4.2.1 Shamir's Secret Sharing

El esquema de Shamir es un método de compartición de secretos basado en la interpolación de polinomios, que divide un secreto en múltiples partes de modo que solo un número mínimo de ellas permite reconstruir el secreto:

1. **Polinomio Secreto**: Para dividir un secreto \( m \), se genera un polinomio de grado \( k-1 \), \( f(z) = f_0 + f_1z + \dots + f_{k-1}z^{k-1} \), donde \( f(0) = m \).
2. **Distribución de Partes**: Cada participante recibe un punto \( (z_i, f(z_i)) \) del polinomio, que representa una parte del secreto.
3. **Recomposición del Secreto**: Con al menos \( k \) puntos, se puede reconstruir el secreto \( m \) usando **interpolación de Lagrange**:
   \[
   m = \sum_{i=1}^k m_i L_i
   \]
   Donde \( L_i \) son los coeficientes de interpolación definidos como:
   \[
   L_i = \prod_{\substack{1 \leq j \leq k \\ j \neq i}} \frac{z - z_j}{z_i - z_j}
   \]
   Este esquema asegura que cualquier subconjunto de \( k-1 \) partes es insuficiente para recuperar el secreto.2.2 Verifiable Secret Sharing (VSS)

El **Verifiable Secret Sharing** añade una capa de verificación para garantizar que el secreto compartido sea válido, permitiendo a cada participante comprobar que su parte fue generada correctamente. Este esquema es particularmente útil en sistemas de votación donde la confianza es clave:

1. **Distribución del Secreto con Verificación**: El secreto \( x \) se representa como el término constante \( f_0 \) de un polinomio de grado \( k-1 \) generado por una autoridad.
2. **Pruebas Públicas**: La autoridad publica valores \( F_i = g^{f_i} \), que permiten a cualquier participante verificar su parte mediante una ecuación pública. Para una parte \( x_j \) asignada, el participante puede verificar que:
   \[
   g^{x_j} = \prod_{l=0}^{k-1} F_j^{j^l}
   \]
   Esto asegura que la compartición es correcta y previene fraudes en la distribución del secreto .

#### Threshold ElGamal

El **Threshold ElGamal** es una variante del cifrado ElGamal en la cual la clave secreta de descifrado está distribuida entre múltiples participantes. Solo un subconjunto de ellos (el umbral) es necesario para realizar el descifrado:

1. **Distribución de la Clave**: Cada participante \( P_i \) selecciona una clave parcial \( x_i \) y publica \( y_i = g^{x_i} \). La clave pública total se calcula como \( y = \prod y_i \), y la clave privada es la suma \( x = \sum x_i \).
2. **Verificación entre Participantes**: Cada participante construye y verifica partes usando polinomios de compartición de secretos y pruebas públicas para asegurar la consistencia de las claves compartidas.
3. **Proceso de Descifrado Umbral**: Solo se requiere que un subconjunto de participantes coopere para descifrar un mensaje cifrado sin necesidad de reconstruir la clave completa, garantizando tanto la seguridad como la eficiencia .

Estos métodos ición y umbral son fundamentales en el contexto de la votación verificable, ya que protegen el acceso a la clave de descifrado y aseguran que el sistema pueda operar incluso si algunos participantes no están disponibles o son comprometidos.
### Tema 4.3: Pruebas de Conocimiento Cero (Zero-Knowledge Proofs)

Las pruebas de conocimiento cero permiten a un **proponente** demostrar un hecho al **verificador** sin revelar la información secreta subyacente. Estas pruebas son cruciales en sistemas de votación verificables, ya que permiten la verificación de propiedades de los votos sin comprometer su privacidad. Una prueba de conocimiento cero debe cumplir con las siguientes propiedades:

- **Completitud**: Si ambos, el proponente y el verificador, son honestos, el protocolo se completa con éxito casi con certeza.
- **Solidez**: Es improbable que un proponente deshonesto logre convencer al verificador de un hecho falso.
- **Conocimiento Cero**: No se revela información adicional sobre el secreto, y es posible simular la prueba sin interacción con el proponente3.1 Pruebas Interactivas y Heurística de Fiat-Shamir

En una prueba de conocimiento cero interactiva, el proponente y el verificador se comunican en varias rondas:

1. **Compromiso**: El proponente envía un compromiso como prueba inicial al verificador.
2. **Desafío**: El verificador responde con un desafío (como un número aleatorio).
3. **Respuesta**: El proponente responde usando el compromiso, el desafío y el secreto, demostrando así la veracidad de su afirmación.

La heurística de **Fiat-Shamir** convierte pruebas interactivas en no interactivas. En este enfoque, el proponente utiliza una función hash en lugar del desafío del verificador, generando así una transcripción verificable sin interacción continua .

#### algoritmo de Identificación de Schnorr

Este algoritmo permite que el proponente demuestre conocer una clave secreta de ElGamal sin revelarla. Funciona de la siguiente manera:

1. **Compromiso**: El proponente elige un número aleatorio \( c \) y calcula \( w = g^c \).
2. **Desafío**: El verificador envía un desafío aleatorio \( e \) al proponente.
3. **Respuesta**: El proponente calcula \( s = c + xe \) (donde \( x \) es el secreto) y envía \( s \) al verificador.
4. **Verificación**: El verificador comprueba que \( g^s = w \cdot y^e \), donde \( y = g^x \).

Este protocolo permite verificar que el proponente conoce el secreto \( x \) sin revelarlo, y también se puede aplicar en sistemas de votación para probar la autenticidad de un voto cifrado  .

#### 4.3.3 Protn

Este protocolo demuestra la igualdad de logaritmos discretos, es decir, que un par de valores tiene el mismo logaritmo en diferentes bases. Por ejemplo, si el proponente tiene \( y = g^x \) y quiere probar que \( (m, n) \) cumple \( \log_g(y) = \log_m(n) \):

1. **Compromiso**: El proponente elige \( c \) y envía \( U = g^c \) y \( V = m^c \).
2. **Desafío**: El verificador envía un desafío \( e \).
3. **Respuesta**: El proponente envía \( s = c + xe \).
4. **Verificación**: El verificador comprueba que \( g^s = U y^e \) y \( m^s = V n^e \).

Este protocolo también permite verificar que un voto cifrado ha sido correctamente desencriptado sin exponer su contenido  .

#### 4.3.4 Protocolo Cramer-Damgårdl protocolo CDS permite al proponente demostrar que conoce la solución a uno o más problemas entre un conjunto, sin revelar cuál. Es útil en sistemas de votación para verificar que un voto pertenece a un conjunto válido de opciones sin revelar la elección específica:

1. **Preparación**: El proponente crea "pruebas falsas" para los problemas que no conoce y una prueba genuina para el problema que sí conoce.
2. **Desafío**: El verificador elige un desafío global y el proponente ajusta las pruebas para que el desafío sea válido para el conjunto completo.
3. **Verificación**: El verificador verifica todas las pruebas sin poder distinguir cuál es la prueba genuina.

Este protocolo asegura que un voto es válido sin que se revele por quién o qué opción se votó .

---
### Tema 4.3 - 4.5: Técnicas de Conocimiento Cero, Mixnets y Otras Técnicas Útiles en Sistemas de Votación Verificable

### 4.3 Pruebas de Conocimiento Cero (Zero-Knowledge Proofs)

Las pruebas de conocimiento cero permiten al proponente demostrar al verificador que conoce un secreto sin revelar información adicional. Son fundamentales para la privacidad y seguridad en sistemas de votación. Deben cumplir las propiedades de completitud (el verificador acepta si el proponente es honesto), solidez (un proponente deshonesto no debería convencer al verificador) y conocimiento cero (no se revela nada sobre el secreto).

- **Pruebas Interactivas y Fiat-Shamir**: Las pruebas interactivas requieren múltiples interacciones entre el proponente y el verificador. La heurística de Fiat-Shamir convierte estas pruebas en no interactivas usando funciones hash, lo cual permite verificar sin interacción continua.

- **Algoritmo de Identificación de Schnorr**: Permite demostrar conocimiento de una clave secreta de ElGamal. El proponente envía un compromiso, recibe un desafío aleatorio, y responde calculando una solución basada en el desafío y el secreto.

- **Protocolo de Chaum-Pedersen**: Prueba la igualdad de logaritmos discretos en dos bases diferentes, útil para verificar que un voto cifrado ha sido correctamente desencriptado sin exponer su contenido.

- **Protocolo CDS (Cramer-Damgård-Schoenmakers)**: Permite demostrar que un valor cifrado pertenece a un conjunto de opciones sin revelar cuál. Es útil en votaciones donde solo interesa verificar que el voto es válido sin revelar la elección.

### 4.4 Mixnets

Los **mixnets** son estructuras que reordenan y, según el tipo de mixnet, re-cifran o descifran votos para romper la conexión entre cada voto y su emisor. Esto preserva la privacidad al evitar la asociación entre el voto original y su salida procesada. Existen dos tipos de mixnets:

- **Mixnets de Descifrado**: Cada servidor descifra parcialmente los votos y luego los permuta. El resultado final es una lista de valores en texto plano.
- **Mixnets de Re-cifrado**: Cada servidor re-cifra los votos y los permuta, manteniendo el contenido cifrado. Los mixnets de re-cifrado son más versátiles, ya que solo requieren información pública para funcionar.

**Métodos de Verificación en Mixnets**:

- **Cut-and-Choose (Cortar y Elegir)**: Se abren aleatoriamente algunas conexiones en la mezcla para verificar la corrección, aunque no revela toda la permutación. Sin embargo, requiere múltiples rondas de auditoría para aumentar la detección de errores.
  
- **Pruebas Eficientes**: Los servidores generan pruebas de que no se han alterado los votos durante el proceso de mezcla, lo que permite una verificación pública y reduce la necesidad de múltiples auditorías.

Ejemplo de implementación: **Mixnet de Chaum con Randomised Partial Checking (RPC)**, en el cual se auditan enlaces aleatorios entre cada par de servidores, dando una probabilidad de 50% de detectar manipulación en cada ronda.

### 4.5 Otras Técnicas Útiles en Sistemas de Votación

Existen otras técnicas que complementan la seguridad y verificación en sistemas de votación:

#### 4.5.1 Firma Ciega (Blind Signature)
Permite que un firmante autentique un mensaje sin conocer su contenido. Se utiliza en votación para que la autoridad firme los votos sin ver la elección del votante, manteniendo así la privacidad del voto.

- **Proceso**: El votante "ciega" el mensaje aplicando una operación matemática y lo envía a la autoridad, que lo firma sin ver el contenido. El votante puede entonces "des-cegar" la firma y usarla como prueba sin revelar su voto a la autoridad.

#### 4.5.2 Prueba de Verificación Designada (Designated Verifier Proof)
Permite probar una afirmación solo a un verificador específico. Así, el verificador no puede convencer a otros sobre la validez de la prueba, útil en sistemas donde solo ciertos actores necesitan verificación confidencial.

#### 4.5.3 Prueba de Equivalencia de Texto Plano (Plaintext Equivalence Test)
Permite verificar si dos cifrados contienen el mismo valor en texto plano sin desencriptarlos, una técnica útil para detectar duplicados o valores inconsistentes sin violar la privacidad del voto.

#### 4.5.4 Re-cifrado por Proxy (Proxy Re-encryption)
Permite transformar un cifrado bajo una clave pública a otro cifrado bajo una clave diferente sin revelar el texto plano. En votación, es útil para transferir votos a una autoridad de recuento sin exponer el contenido del voto.

Estas técnicas amplían las capacidades de verificación y privacidad en sistemas de votación, permitiendo construir un proceso electoral seguro, transparente y resistente a coacción.