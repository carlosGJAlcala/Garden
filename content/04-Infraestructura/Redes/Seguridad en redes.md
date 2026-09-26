---
title: "Seguridad en redes"
---

# Seguridad en Redes

Cap 8. Seguridad en Redes

## Objetivos del tema 8

*(el número de diapositiva "22" en la fuente original no sigue la secuencia de numeración habitual del resto del capítulo, que reinicia en "3" en la siguiente diapositiva; se conserva sin alterar)*

Temas del capítulo: comprender los principios de la seguridad de la red:
- La criptografía y sus muchos usos: confidencialidad, autenticación, integridad de los mensajes.
- La seguridad en la práctica: «firewalls» y sistemas de detección de intrusiones.
- La seguridad en los niveles de aplicación, transporte, red y enlace.

## Índice capítulo 8

- 8.1 ¿Qué es la seguridad de la red?
- 8.2 Principios de la criptografía
- 8.3 Integridad de los mensajes
- 8.5 Asegurar las conexiones TCP: SSL
- 8.6 La seguridad en el nivel de red: IPsec
- 8.7 Asegurar las redes inalámbricas
- 8.8 Dispositivos: "firewalls" e IDS

## ¿Qué es la seguridad de la red?

- Confidencialidad: sólo el emisor y el destinatario deben entender el contenido del mensaje. El emisor encripta el mensaje; el receptor desencripta el mensaje.
- Autenticación: el emisor y el receptor quieren confirmar la identidad del otro.
- Integridad del mensaje: el emisor y el receptor quieren estar seguros que el mensaje no puede ser modificado (en el camino o en cualquier parte) sin que se detecte.
- Accesibilidad y disponibilidad: los servicios deben estar accesibles y disponibles a los usuarios.

## Amigos y enemigos: Alice, Bob, Trudy

Actores en el mundo de la seguridad de la red:
- Alice, Bob quieren comunicarse con seguridad.
- Trudy quiere interceptar, destruir o modificar los mensajes.

*(diagrama: Alice (emisor) y Bob (receptor) se comunican a través de un canal de datos/mensajes/control; Alice cifra el dato seguro que envía y Bob lo descifra; Trudy, en medio del canal, intenta interceptar la comunicación)*

## ¿Quiénes pueden ser Alice y Bob?

- Personas reales Alice y Bob
- Cliente/servidor web para transacciones electrónicas (ej., comercio en línea)
- Banco en línea cliente/servidor
- Servidores de DNS
- «Routers» comunicándose los cambios en las tablas de encaminamiento
- …

## ¡Existen atacantes!

P: ¿Qué puede hacer un atacante? R: ¡Muchas cosas!

- «Eavesdropping»: interceptar mensajes.
- Añadir mensajes en la conexión.
- Alteración de mensajes: puede modificar la dirección fuente (o cualquier campo del paquete).
- «Hijacking» (Secuestro): e.g. robar la conexión o sesión sustituyendo al emisor o receptor, colocándose él en su lugar.
- Denegación del servicio: evitar que los demás puedan utilizar el servicio (e.g. sobrecargando los recursos).

## Índice capítulo 8

- 8.1 ¿Qué es la seguridad de la red?
- 8.2 Principios de la criptografía
- 8.3 Integridad de los mensajes
- 8.5 Asegurar las conexiones TCP: SSL
- 8.6 La seguridad en el nivel de red: IPsec
- 8.7 Asegurar las redes inalámbricas.
- 8.8 Dispositivos: "firewalls" e IDS

## La terminología de la criptografía

*(diagrama: texto claro m → algoritmo de cifrado, usando la clave de cifrado de Alice K_A, → texto cifrado K_A(m) → algoritmo de descifrado, usando la clave de descifrado de Bob K_B, → texto claro m)*

- m: mensaje en claro
- K_A(m): mensaje cifrado con la clave K_A
- m = K_B(K_A(m)): mensaje descifrado con clave K_B

## Esquema de encriptación simple I

Sustitución: se sustituye una cosa por otra.

Cifrado de Julio César: se sustituye una letra del alfabeto por otra desplazada K posiciones.

```
K=3
Texto claro:   abcdefghijklmnopqrstuvwxyz
Texto cifrado: defghijklmnopqrstuvwxyzabc
```

Ej. K=3:

```
Texto claro:   bob. te amo. alicia
Texto cifrado: ere. wh dpr. dolfld
```

Clave: el desplazamiento K.

## Esquema de encriptación simple II

Sustitución: se sustituye una cosa por otra.

Cifrado monoalfabeto: se sustituye una letra por otra.

```
Texto claro:   abcdefghijklmnopqrstuvwxyz
Texto cifrado: mnbvcxzasdfghjklpoiuytrewq
```

Ej.:

```
Texto claro:   bob. Te amo. alice
Texto cifrado: nkn. Uc mhk. mgsbx
```

Clave: aplicación (mapeado) de un conjunto de 26 letras en un conjunto de 26 letras.

## ¿Cómo se rompe un esquema de encriptación?

"El escarabajo de oro", de E.A. Poe:

```
53‡‡†305))6*;4826)4‡.)4‡);806*;48†8
¶60))85;1‡(;:‡*8†83 ( 88)5*†;46 (;88*96
*?;8)*‡(;485);5*†2:*‡(;4956*2 ( 5*—4)8
¶8*;4069285);)6†8)4‡‡;1 (‡9;48081;8:8‡
1;48†85;4)485†528806*81 (‡9;48;( 88;4
(‡?34;48)4‡;161;:188;‡?;
```

*(las tres diapositivas siguientes muestran, en una revelación progresiva típica de una animación de PowerPoint, cómo se rompe este criptograma mediante análisis de frecuencias)*

Análisis de frecuencias: permite establecer correspondencias.
- 8 → e

Análisis de digramas/trigramas:
- ;48 → the

A partir de ahí pueden recomponerse frases:
- ;48;( 88 → the tree

Sólo sirve para cifrados "débiles".

## Cifradores de flujo

*(diagrama: un generador de flujo de clave (keystream) pseudoaleatorio combina de forma continua cada bit de un flujo de clave con el texto en claro para obtener el texto cifrado)*

- m(i) = i-ésimo bit del mensaje
- ks(i) = i-ésimo bit del flujo de clave (keystream)
- c(i) = i-ésimo bit del texto cifrado
- c(i) = ks(i) Å m(i) (Å = XOR)
- m(i) = ks(i) Å c(i)

**Cifrador de flujo RC4**
- RC4 es un cifrado de flujo popular. Muy analizado y considerado bueno, aunque en ocasiones su uso incorrecto lo hace inseguro.
- La clave puede ser de 1 a 256 bytes.
- Se usa en WEP para 802.11. También puede usarse en SSL.

**One time pad (OTP)**
- Clave de la misma longitud del mensaje, aleatoria, sólo utilizable una vez.
- Secreto perfecto. Muy poco práctico.

## Cifradores de bloques

El mensaje a cifrar se procesa en bloques de k bits (ej., bloques de 64-bit). Se realiza una aplicación 1-a-1 de un bloque de k-bits de texto en claro a un bloque de k-bits de texto cifrado.

Por ejemplo, con k=3:

| claro | cifrado | claro | cifrado |
|---|---|---|---|
| 000 | 110 | 100 | 011 |
| 001 | 111 | 101 | 010 |
| 010 | 101 | 110 | 000 |
| 011 | 100 | 111 | 001 |

¿Qué texto cifrado corresponde a 010110001111?

## Cifradores de bloques (continuación)

¿Cuántas aplicaciones diferentes existen con k=3?
- ¿Cuántas entradas con 3-bits? 2³=8
- ¿Cuál es el número de permutaciones para entradas de 3-bits? 8!
- Solución: 40320; ¡no son muchas! (de cara a romper cifrado)
- En general hay 2^k! aplicaciones; para k=64, ¡enorme!

Problema: la tabla de cifrado necesita 2⁶⁴ entradas, y cada entrada es de 64 bits. La tabla es demasiado grande: en su lugar se simula la tabla con una función aleatoria dependiente de la clave.

## La encriptación de mensajes largos

¿Por qué no vale dividir el mensaje en bloques de 64 bits, y encriptar cada bloque por separado? Porque si hay dos bloques en claro iguales, darán dos bloques cifrados iguales.

¿Cómo se opera?:
- Se genera un número aleatorio de 64-bits, r(i), para cada bloque de texto claro m(i).
- Se calcula c(i) = K_S(m(i) Å r(i))
- Se transmite c(i), r(i), i=1,2,…
- En el receptor se calcula: m(i) = K_S(c(i)) Å r(i)

Problema: es ineficiente, hay que enviar c(i) y r(i) (¡el doble de bits!!!). Solución: CBC.

## Cadena de bloques de cifrado (CBC)

Vector de inicialización (IV) de K bits: bloque aleatorio c(0) que se envía sin cifrar.

- Primer bloque: emisor envía c(1) = K_S(m(1) Å c(0)). El receptor calcula mensaje m(1) = K_S(c(1) Å c(0))
- Para el i-ésimo bloque: c(i) = K_S(m(i) Å c(i-1)); m(i) = K_S(c(i) Å c(i-1))

## Cadena de bloques de cifrado (CBC) (continuación)

*(diagrama comparando dos modos de cifrado por bloques)*

**Bloque de cifrado simple**: si el bloque de entrada se repite, se producirá el mismo texto cifrado:
- t=1: m(1) = "HTTP/1.1" → c(1) = "k329aM02"
- t=17: m(17) = "HTTP/1.1" → c(17) = "k329aM02"

**Cadena de bloques de cifrado (CBC)**: XOR del i-ésimo bloque de entrada, m(i), con el texto cifrado del bloque anterior, c(i-1), antes de cifrar. c(0) se transmite en claro.

¿Qué pasa con "HTTP/1.1" en el escenario anterior (con CBC)?

## Tipos de métodos criptográficos

Criptografía basada en las claves: el algoritmo lo conoce todo el mundo, lo único secreto es la clave.
- Criptografía de clave pública: utiliza dos claves.
- Criptografía de clave simétrica: utiliza una sola clave.

Funciones «hash»: no utiliza claves. Nada es secreto: ¿cómo puede ser útil?

## Criptografía de clave simétrica

*(diagrama: texto claro m → algoritmo de cifrado con K_S → texto cifrado K_S(m) → algoritmo de descifrado con K_S → texto claro m = K_S(K_S(m)))*

Clave simétrica: Alice y Bob comparten la misma clave (simétrica): K_S. Ej., conocen la clave de sustitución en el cifrado monoalfabeto.

P: ¿Cómo se ponen de acuerdo Alice y Bob en el valor de la clave?

## Criptografía de clave simétrica: ejemplos

**DES: «Data Encryption Standard»**

Estándar de encriptación en USA [NIST 1993]. Cifrador de bloques con bloques de cifrado en cadena. Clave simétrica de 56-bits, entrada de texto claro de 64-bits.

¿DES es seguro? Ataque a DES: una frase encriptada con una clave de 56-bits se puede desencriptar (por fuerza bruta) en menos de un día. No se conoce un ataque analítico bueno.

Para hacer DES más seguro: 3DES: se encripta 3 veces con 2 ó 3 claves diferentes (actualmente se encripta, se desencripta, se encripta).

**AES: «Advanced Encryption Standard»**

Estándar de clave simétrica NIST. Se presentó en (Nov. 2001) para substituir a DES. Procesa los datos en bloques de 128 bits. Claves de 128, 192, o 256 bits.

Tiempos estimados del ataque por fuerza bruta (obtener la clave): 1 seg para DES, 149 billones de años para AES.

## Criptografía de clave pública

Criptografía de clave simétrica: se necesita que el emisor y el receptor compartan la clave. Q: ¿Cómo acordar la clave la primera vez (en concreto, si nunca han contactado)?

Criptografía de clave pública: solución completamente diferente [Diffie-Hellman76, RSA78]. El emisor y el receptor no comparten la misma clave. La clave pública la conoce todo el mundo. La clave para descifrar sólo la conoce el receptor.

## Criptografía de clave pública (continuación)

*(diagrama: texto claro m → algoritmo de cifrado con la clave pública de Bob K_B⁺ → texto cifrado K_B⁺(m) → algoritmo de descifrado con la clave privada de Bob K_B⁻ → mensaje en claro m = K_B⁻(K_B⁺(m)))*

## Algoritmos de encriptación de clave pública

Requisitos:
1. Se necesitan K_B⁺() y K_B⁻() tales que K_B⁻(K_B⁺(m)) = m
2. Dada la clave pública K_B⁺, debe ser imposible obtener la clave privada K_B⁻

RSA: algoritmo de Rivest, Shamir, Adleman, basado en "función trampa" (factorización de números primos).

## RSA: Otra propiedad importante

La siguiente propiedad será muy útil más adelante:

K_B⁻(K_B⁺(m)) = m = K_B⁺(K_B⁻(m))

- Primero se usa la clave pública, después la privada.
- Primero se usa la clave privada, después la clave pública.

¡El resultado es el mismo!

## Claves de sesión

La exponenciación es computacionalmente intensiva. DES es al menos 100 veces más rápido que RSA.

Clave de sesión, K_S: Alice y Bob usan RSA para intercambiar una clave simétrica K_S. Una vez que ambos tienen K_S, ellos utilizan criptografía de clave simétrica.

## Índice capítulo 8

- 8.1 ¿Qué es la seguridad de la red?
- 8.2 Principios de la criptografía
- 8.3 Integridad de los mensajes
- 8.5 Asegurar las conexiones TCP: SSL
- 8.6 La seguridad en el nivel de red: IPsec
- 8.7 Asegurar las redes inalámbricas
- 8.8 Dispositivos: "firewalls" e IDS

## Integridad de los mensajes

En realidad, veremos autenticación e integridad.

Garantía de que los mensajes que se reciben son auténticos:
- Que el emisor es quien dice ser (autenticación)
- Que el contenido del mensaje no ha sido alterado
- Que el mensaje no ha sido reemplazado
- Que se mantiene el orden de los mensajes

Veremos, en primer lugar, los resúmenes (digest) de mensajes.

## Resumen de Mensaje

La función H() recibe un mensaje de longitud arbitraria y devuelve un mensaje de longitud fija: «firma del mensaje». H() es una función muchos a 1. H() se conoce como «función hash».

*(diagrama: mensaje largo m → función Hash H → H(m))*

Propiedades deseables:
- Fácil de calcular.
- Irreversible: que no se pueda obtener m a partir de H(m).
- Distribución uniforme: que sea computacionalmente difícil que existan m y m' que generen H(m) = H(m').
- Salida aparentemente aleatoria.

## Algoritmos para funciones Hash

- MD5: función Hash muy extendida (RFC 1321). A partir del mensaje calcula un resumen de 128 bits. Desde 2004, considerado inseguro ("facilidad" para encontrar colisiones).
- SHA-1: es otra función muy utilizada. Es un estándar USA [NIST, FIPS PUB 180-1]. La longitud del resultado es de 160-bits. También inseguro (2007).
- Hashes seguros (de momento): SHA-3, RIPEMD-128/256, RIPEMD-320.

## Message Authentication Code (MAC)

Permite:
- Autenticar al emisor.
- Verificar la integridad del mensaje.

No utiliza cifrado. También se denomina "hash con clave".

Notación: MD_m = H(s|m); se envía m|MD_m

s = clave secreta compartida

*(diagrama: el emisor calcula H(s|mensaje) y lo envía junto al mensaje; el receptor recalcula H(s|mensaje) con su propia copia de s y compara el resultado con el MD recibido)*

## Autenticación de origen

Queremos estar seguros del origen del mensaje – autenticación de origen. Asumimos que Alice y Bob tienen una clave secreta compartida, entonces MAC provee autenticación de origen.

Nosotros sabemos que Alice creó el mensaje. Pero ¿lo envió ella?

## Ataque de repetición

MAC = f(msg,s)

*(ejemplo: un atacante repite un mensaje interceptado "Transferir $1M de Bob a Trudy" junto con su MAC original, reenviándolo de nuevo — ya que el MAC sigue siendo válido, el receptor no detecta que es una repetición)*

## Protección frente a ataque de repetición

"Yo soy Alicia": R (un valor aleatorio/nonce)

MAC = f(msg,s,R)

*(al incluir el nonce R en el cálculo del MAC, cada mensaje "Transferir $1M de Bob a Trudy" produce un MAC distinto, impidiendo que un mensaje repetido sea aceptado de nuevo)*

## Firma digital

Técnica criptográfica análoga a la firma manual. Emisor (Bob) firma digitalmente un documento, para indicar que él es su dueño/creador. El objetivo es similar al de MAC, excepto que ahora se usa criptografía de clave pública.

Verificable, no falsificable: el receptor (Alice) puede probar que Bob y nadie más (ni siquiera Alice), ha firmado el documento.

## Firma digital: esquema simple

Firma digital simple para un mensaje m: Bob firma m cifrándolo con su clave privada K_B⁻ y genera el mensaje firmado, K_B⁻(m).

*(diagrama: mensaje de Bob, m ("Querida Alice", texto del mensaje) → algoritmo de cifrado con la clave privada de Bob K_B⁻ → mensaje de Bob, m, firmado (cifrado) con su clave privada, K_B⁻(m))*

## Firma digital = resumen del mensaje firmado

Bob envía el mensaje firmado digitalmente:

*(diagrama: mensaje largo m → función hash H → resumen del mensaje H(m) → cifrado con la clave privada de Bob K_B⁻ → firma digital K_B⁻(H(m)); la firma digital se adjunta al mensaje completo m, formando el mensaje firmado)*

Alice verifica la firma y la integridad del mensaje firmado digitalmente:

*(diagrama: Alice recibe el mensaje completo m y la firma digital K_B⁻(H(m)); por un lado calcula H(m) directamente a partir del mensaje recibido; por otro lado descifra la firma con la clave pública de Bob K_B⁺ para obtener H(m); compara ambos resultados — ¿igual?)*

## Firma digital (II)

Suponga que Alice recibe el mensaje m, firmado digitalmente K_B⁻(m).

Alice comprueba que m está firmado por Bob, aplicando la clave pública de Bob K_B⁺ a K_B⁻(m) y comprobando que K_B⁺(K_B⁻(m)) = m. Si K_B⁺(K_B⁻(m)) = m, significa que m ha tenido que ser firmada con la clave privada de Bob.

De esta forma Alice verifica que:
- ✓ Bob firmó m. Nadie más pudo firmar m → Autenticación.
- ✓ Bob firmó m y no m' (otro mensaje distinto) → Integridad.
- ✓ No-repudio: Alice puede tomar m, y la firma K_B⁻(m), para probar que Bob firmó m.

## Certificado de clave pública

Ejemplo: Trudy pide unas pizzas cargándoselas a Bob.

- Trudy crea una petición por e-mail: "Querida pizzería, haga el favor de enviarme 4 pizzas pepperoni. Gracias, Bob"
- Trudy firma la orden con su clave privada.
- Trudy envía la orden a la pizzería.
- Trudy envía a la pizzería su clave pública, pero dice que es la clave pública de Bob.
- La pizzería comprueba la firma; y le envía las 4 pizzas a Bob.

A Bob no le gustan las Pepperoni...

## Autoridades de certificación (aka PKI)

Autoridad de certificación (CA): asigna claves públicas a entidades particulares, E.
- E (persona, router) registra su clave pública en la CA. E provee «prueba de identificación» al CA.
- CA crea el certificado asociado a la clave pública de E. Certifica que es de E lo firmado digitalmente con la clave pública CA – CA dice «esta es la clave pública de E».

*(diagrama: la clave pública de Bob K_B⁺, junto con información identificada como de Bob, se cifra con la clave privada de la CA K_CA⁻ para producir el certificado de Bob, firmado digitalmente por la CA)*

## Autoridades de certificación (continuación)

Cuando Alice quiere la clave pública de Bob:
- Pide el certificado de Bob (a la CA, al propio Bob…).
- Aplica la clave pública CA (K_CA⁺) al certificado de Bob, obtiene la clave pública de Bob (K_B⁺).

*(diagrama: el certificado firmado digitalmente —cifrado con K_CA⁻— se descifra con la clave pública de la CA K_CA⁺, recuperando la clave pública de Bob K_B⁺)*

## Trabajo Personal

- Estudio de los apartados 8.1, 8.2, 8.3 y 8.4
- Estudio del apartado 8.5, SSL.

*(la nota final "Redes multimedia" queda suelta al final del documento original, sin más contenido asociado — probablemente el inicio de una diapositiva o sección que no llegó a extraerse)*
