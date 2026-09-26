---
title: "Funciones hash y códigos MAC"
---

# 3.3 Funciones resumen y códigos de autenticación

Máster en Ciberseguridad | Raúl Durán Díaz | Curso académico 2024–2025

## Contenidos

1. Funciones resumen
2. Códigos de autenticación de mensajes (MAC)
3. Cifrado autenticado

## 1. Funciones resumen

### Funciones resumen

**Definición 1:** Informalmente, una función resumen (en inglés, hash) toma una entrada de un tamaño cualquiera y produce una salida de tamaño fijo.

**Comentario 2:** Al resultado de la ejecución de la función resumen sobre una entrada lo solemos llamar resumen del mensaje. Si tenemos m ∈ {0,1}*, entonces:

```
H: {0,1}* → {0,1}^n
H: m ↦ h
```

donde h = H(m), y n es el tamaño (fijo) del resumen.

### Usos de las funciones resumen

- Comprobación de integridad.
- Autenticación de mensajes, datos o software (huella digital).
- Firmas digitales.
- Protocolos de acuerdo de claves.
- Protección de contraseñas.
- ...

### Seguridad de las funciones resumen

Para considerar segura una función resumen, se consideran las siguientes propiedades:

- Imprevisibilidad.
- Resistencia a la pre-imagen.
- Resistencia a la segunda pre-imagen.
- Resistencia a colisiones.

### Imprevisibilidad

El resumen de un mensaje debe depender de todos los bits, de modo que un cambio mínimo en la entrada debe causar un cambio máximo en la salida: en particular deben cambiar, en promedio, la mitad de los bits de la salida.

### Resistencia a la pre-imagen

Una función resumen debe ser unidireccional: dado un resumen, h, debe ser computacionalmente inabordable encontrar un mensaje m tal que H(m) = h.

**Definición 3:** Una función unidireccional f: X → Y tiene inversa f⁻¹, pero mientras que el coste computacional de evaluar f es bajo o muy bajo, el coste computacional de evaluar f⁻¹ es inaceptablemente alto.

### Resistencia a la segunda pre-imagen

Dado un mensaje m tal que su resumen es h = H(m₁), tiene que ser computacionalmente inabordable encontrar otro mensaje m₂, tal que se resuma en el mismo valor h, es decir, tal que h = H(m₁) = H(m₂).

Esta propiedad también se llama resistencia débil a colisiones.

### Resistencia a colisiones

Debe ser computacionalmente inabordable encontrar dos mensajes cualesquiera, m₁, m₂, tales que se resuman en el mismo, es decir, tales que H(m₁) = H(m₂).

Obsérvese que en este caso no se dispone de ningún resumen previo: basta ser capaz de encontrar dos mensajes, no importa cuáles, tales que se resuman en el mismo valor.

### Ataques sobre las funciones resumen

**Comentario 4:** Si tenemos ataque a la segunda pre-imagen, conseguimos atacar también la resistencia a la colisión. Dado el mensaje m₁, si soy capaz de encontrar m₂ tal que H(m₁) = H(m₂), obviamente tengo una colisión.

**Comentario 5:** Análogamente, si tenemos ataque a la pre-imagen, conseguimos atacar también la segunda pre-imagen. Supongamos que tomo un m' y calculo h = H(m'). Aplico el ataque a la pre-imagen sobre h y obtengo cierto m tal que H(m) = h. Con altísima probabilidad, m ≠ m', con lo que he conseguido la segunda pre-imagen.

### Definición formal de la resistencia a colisiones

Dada una función resumen, H, el experimento ColRes_H(n) para buscar colisiones lo expresamos así:

1. El adversario recibe el valor del parámetro de seguridad n.
2. El adversario emite x, x', distintos.
3. La salida del experimento se define como 1 (el adversario gana el ataque) si y solo si x ≠ x' y H(x) = H(x').

Si la salida es 1, decimos que ha encontrado una colisión.

### Definición formal de resistencia a colisiones (formal)

**Definición 6:** Una función resumen H: {0,1}* → {0,1}^n es resistente a colisiones si para cualquier adversario de tiempo polinómico probabilístico, existe una función insignificante ng tal que:

```
Pr[ColRes_H(n) = 1] ≤ ng(n)
```

donde n es el parámetro de seguridad.

### ¿Qué ocurre si se encuentra una colisión?

La firma digital de un documento se realiza sobre un resumen de tal documento, para hacer el proceso más seguro (y, de paso, más rápido).

Pero entonces... si alguien encuentra una colisión, puede hacer pasar un documento falso por el bueno, pues ambos verifican la firma ya que esta se hace sobre el resumen: y tendríamos dos documentos con el mismo resumen.

### Pigeon-hole principle

Si tienes 100 pichones pero solo 99 nidos para ellos, seguro que en al menos un nido habrá más de un pichón...

Por tanto, es imposible evitar las colisiones. Se trata de que no exista un método analítico para obtenerla y fracase en otros ataques, como el de fuerza bruta.

### ¿Qué tan difícil es encontrar colisiones?

Puesto que las funciones resumen tienen una salida de tamaño fijo, ello implica un número máximo de posibles resúmenes.

Pero el número de mensajes distintos por resumir puede alcanzar un valor arbitrariamente alto... así que hay más pichones que nidos.

### Paradoja del cumpleaños

Si el resumen es de n bits, parece que se necesitan 2^n pruebas para tener éxito en el ataque por fuerza bruta. Pero en realidad, a un atacante le bastaría con 2^(n/2), como consecuencia de un curioso resultado que se suele llamar la paradoja del cumpleaños.

### Paradoja del cumpleaños: dato

Si en una sala hay 23 personas, la probabilidad de que dos de ellas cumplan años el mismo día es mayor del 50%.

Ensayemos una justificación:

En primer lugar, observemos que si en la sala hay una persona y entra otra, la probabilidad de que el cumpleaños de la que entra no coincida con el de la que está allí es:

```
P(no colisión) = 364/365
```

pues la segunda persona tiene 364 días "sin ocupar".

### Paradoja del cumpleaños: continuación

Pero si entra una tercera:

```
P(no colisión) = (364/365) · (363/365)
```

pues ahora había dos días "ocupados".

Por tanto, la probabilidad que deseamos saber será para t personas:

```
P_t(colisión) = 1 - P_t(no colisión) =
                1 - (364/365) · (363/365) · (362/365) · ... · (365-t+1)/365
```

### Paradoja del cumpleaños: tabla

La siguiente tabla es interesante:

```
t       P_t(colisión)
5       2,71%
10      11,69%
20      41,14%
23      50,73%
40      89,12%
60      99,41%
```

### Paradoja en la función resumen

Podemos suponer que los mensajes son como "personas", a cada uno de los cuales le corresponde un resumen, que es como su "cumpleaños".

Nos hacemos la pregunta análoga: ¿cuántos mensajes necesito reunir para tener una determinada probabilidad de que dos de ellos "colisionen" (es decir, les corresponda el mismo resumen)?

### Paradoja en la función resumen (continuación)

Observemos que ahora el número posible de resúmenes, para una función con tamaño n bits es 2^n. Por tanto:

```
P_t(no colisión) = (2^n - 1)/(2^n) · (2^n - 2)/(2^n) · (2^n - 3)/(2^n) · ... · (2^n - t + 1)/(2^n)
                 = ∏(i=1 a t-1) (1 - i/(2^n))
```

### Aproximación de la probabilidad de colisión

Cuando x ≪ 1, se verifica que e^(-x) ≈ 1 - x, así que:

```
P_t(no colisión) ≈ ∏(i=1 a t-1) e^(-i/2^n) = e^(-(1+2+3+...+t-1)/2^n)
```

Pero:

```
1 + 2 + 3 + ... + t - 1 ≈ t²/2
```

lo que significa que:

```
P_t(no colisión) ≈ e^(-t²/2^(n+1))
```

### Aproximación de la probabilidad de colisión (fórmula final)

Si queremos una probabilidad de colisión λ_c, se tiene que:

```
λ_c ≈ 1 - e^(-t²/2^(n+1))
```

Despejando t para un valor fijado de λ_c, tenemos:

```
t ≈ 2^((n+1)/2) · (log(1/(1-λ_c)))^(1/2)
```

donde log es el logaritmo natural.

### Aproximación final

Observando la ecuación, si fijamos una probabilidad de colisión de λ_c = 0,5, el término bajo el radical vale aproximadamente 0,8326. Es claro, pues, que el término importante es el factor 2^((n+1)/2).

Contra la intuición, vemos que se necesitan del orden de 2^(n/2) resúmenes para que haya una probabilidad muy significativa de encontrar una colisión.

Dada la capacidad actual de cómputo, es imprescindible que n sea al menos de 192 bits.

### Panorámica de las funciones resumen

La estrategia general es dividir el mensaje original en trozos de tamaño fijo y procesar cada trozo iterativamente: esta estrategia se denomina resumen iterativo.

Posibles modos de realizar el resumen iterativo:

- Mediante el uso de funciones compresoras, que transforman una entrada en una salida de menor tamaño (construcción Merkle-Damgård).
- Mediante funciones esponja que esencialmente son permutaciones de la entrada.

### Construcción Merkle-Damgård

**Definición 7:** La transformación Merkle-Damgård es, esencialmente, un mecanismo para extender una función resumen (o función compresora) que sea resistente a colisiones y con entrada de tamaño fijado a otra función resumen genérica, que pueda recibir entradas de cualquier tamaño.

**Comentario 8:** La construcción Merkle-Damgård permite reducir el problema de encontrar una función resumen resistente a colisiones a encontrar una función compresora resistente a colisiones, lo que puede suponerse más sencillo, en principio.

### Algoritmo Merkle-Damgård

Supongamos una función compresora f: {0,1}^(n+r) → {0,1}^n, resistente a colisiones. Con ella construimos una función resumen H resistente a colisiones con estos pasos:

1. Dividir el mensaje de entrada, m, de longitud b (con b < 2^r), en bloques m₁, m₂, ..., m_t, de r bits, completando con ceros, si fuera necesario, el último bloque.

2. Definir un bloque final nuevo, m_(t+1) que recibe la representación binaria del valor b.

3. Definimos H(m) = h_(t+1), calculado como:

```
h₀ = IV; h_i = f(h_(i-1) || m_i), 1 ≤ i ≤ t + 1
```

El valor IV se supone fijado: típicamente IV = 0^n.

### Seguridad del esquema Merkle-Damgård

**Implicación:** Si la función compresora es resistente a colisiones, también lo es la construcción de Merkle-Damgård.

**Comentario 9:** Lo anterior es cierto porque podemos transformar cualquier ataque exitoso a la función resumen en un ataque exitoso a la función compresora.

### Ataque por extensión al esquema Merkle-Damgård

Dado un mensaje m, y su resumen H(m), el atacante siempre puede "inventarse" un bloque de mensaje adicional m_a, y añadirlo al mensaje original (aunque no lo conozca), recalculando el resumen así:

```
h_a = f(H(m) || m_a)
```

y haciendo creer que el nuevo resumen es H'(m || m_a) = h_a.

Este ataque no necesariamente invalida el esquema, pero no puede olvidarse que existe.

### Cómo construir una función de compresión

Existen dos estrategias principales:

- **Cifradores de bloque:** usando un cifrador de bloque para construir la función de compresión.
- **Funciones específicamente diseñadas:** con las características adecuadas para servir de función compresión/resumen.

### Funciones de compresión con cifradores de bloque

**Definición 10:** Definimos la función de compresión como un cifrador de bloque que cifra bloques de texto claro de n bits, produciendo un criptograma de n bits y utiliza una clave de r bits.

### Construcciones sobre cifradores de bloque

Hay tres esquemas básicos, nombrados por sus creadores:

1. Davies-Meyer
2. Matyas-Meyer-Oseas
3. Miyaguchi-Preneel

### Esquema Davies-Meyer

Este es el esquema más importante. Los pasos son:

1. Dividir el mensaje de entrada, m, de longitud b, en bloques m₁, m₂, ..., m_t, de r bits (completando el último bloque, si fuera necesario), donde r es el tamaño de la clave K.

2. Definir un valor constante inicial IV, de n bits.

3. Definimos H(m) = h_t, calculado como:

```
h₀ = IV;
h_i = E_m_i(h_(i-1)) ⊕ h_(i-1), 1 ≤ i ≤ t
```

### Esquema Matyas-Meyer-Oseas

1. Dividir el mensaje de entrada, m, de longitud b, en bloques m₁, m₂, ..., m_t, de n bits (completando el último bloque, si fuera necesario).

2. Definir un valor constante inicial IV, de n bits.

3. Definimos H(m) = h_t, calculado como:

```
h₀ = IV;
h_i = E_g(h_(i-1))(m_i) ⊕ m_i, 1 ≤ i ≤ t
```

**Comentario 11:** La función g simplemente mapea entradas de n bits a una clave K de tamaño adecuado para el cifrador de bloque E. Si las claves son también de tamaño n, bien puede ser la función identidad.

### Esquema Miyaguchi-Preneel

1. Dividir el mensaje de entrada, m, de longitud b, en bloques m₁, m₂, ..., m_t, de n bits (completando el último bloque, si fuera necesario).

2. Definir un valor constante inicial IV, de n bits.

3. Definimos H(m) = h_t, calculado como:

```
h₀ = IV; h_i = E_g(h_(i-1))(m_i) ⊕ m_i ⊕ h_(i-1), 1 ≤ i ≤ t
```

**Comentario 12:** La función g cumple el mismo papel que en el esquema de Matyas-Meyer-Oseas.

### Funciones esponja

**Definición 13:** Una función esponja es un algoritmo con estado interno finito, que toma una entrada de cualquier longitud y produce una salida de la longitud deseada.

### Funciones esponja: componentes

Una función esponja consta típicamente de:

1. un estado interno S, de b bits;
2. una función f: {0,1}^b → {0,1}^b que transforma biyectivamente el estado (se puede ver como una permutación pseudo-aleatoria de los 2^b posibles valores del estado interno);
3. y una función de relleno, L.

**Comentario 14:** La memoria de estado, S, se considera dividida en dos partes, R y C, de tamaños r y c bits respectivamente.

### Operación de la función esponja

La función esponja tiene dos fases:

1. fase de absorción
2. fase de explotación ("apretar" la esponja)

### Fase de absorción

1. El estado S se inicializa a 0^b.
2. Si es necesario, la entrada se completa mediante la función L de relleno para que su longitud sea múltiplo del tamaño r.
3. Para cada bloque B de tamaño r, repetir:
   - R ← R ⊕ B
   - S ← f(S)
   hasta agotar los bloques de entrada.

### Fase de explotación

A partir del estado actual, se generan tantos bits de salida como sigue:

1. Se emite la porción R de la memoria de estado, S.
2. Repetir:
   - S ← f(S)
   - extraer un máximo de r bits hacia la salida ← R
   hasta que el número deseado de bits haya sido emitido.

### Seguridad de las funciones esponja

Observemos que el estado tiene r + c bits. En cada paso, solo r bits se ven modificados.

El nivel de seguridad garantizado por estas funciones es c/2 bits.

La complejidad del ataque por colisión es el mínimo valor entre 2^(c/2) y 2^(n/2), donde n es la longitud del resumen.

**Ejemplo 15:** Si tengo bloques de mensajes de 128 bits y el resumen también es de 128 bits, puedo aspirar como mucho a una seguridad de 64 bits, por lo que el valor de c ha de ser 128 y el estado S ha de tener r + c = 128 + 128 = 256 bits.

### Implementaciones reales de resúmenes: funciones MD

Las funciones resumen más populares han sido las MD4 y MD5, diseñadas por Rivest en los años 90. En la actualidad se conocen ataques muy rápidos para generar colisiones en ambos sistemas.

MD5 procesa bloques de mensajes de 512 bits, actualiza una memoria de estado de 128 bits para producir un resumen de 128 bits, por lo que nos encontramos con una seguridad frente a colisiones de 64 bits.

### Implementaciones reales de resúmenes: funciones MD (seguridad)

En 2005 un grupo de investigación chino descubrió un método para generar colisiones con una complejidad de cómputo que no excede 2^39 operaciones. Con los recursos actuales, es cuestión de segundos, por lo que MD5 está completamente descartada.

El ataque no afecta a las preimágenes, por lo que MD5 se sigue usando a veces en aplicaciones donde no importa que existan colisiones.

### Implementaciones reales de resúmenes: funciones SHA

Como iniciativas del NIST, surgieron unas propuestas que recibieron el nombre de SHA-X.

Se desarrollaron el SHA-1, posteriormente ampliado a SHA-2. Estos se utilizan el algoritmo de Merkle-Damgård, con un esquema de tipo Davies-Meyer y una función de compresión basada en un cifrador especialmente diseñado para el SHA. Las distintas variantes se diferencian simplemente en el tamaño del bloque de mensaje y el resumen.

### SHA-1 en funcionamiento

SHA-1 trabaja con bloques de mensajes de 512 bits y bloques resumen de 160 bits.

Se aplica el esquema de Davies-Meyer:

```
h₀ = IV; h_i = E_m_i(h_(i-1)) + h_(i-1), 1 ≤ i ≤ t
```

pero, ¡cuidado!, la suma no es módulo 2 (bit a bit) sino que el bloque de 160 bits se considera dividido en 5 palabras de 32 bits que se suman independientemente.

### Seguridad del SHA-1

En principio, SHA-1 debiera dar una seguridad de 80 bits, pero, de nuevo, ataques llevados a cabo por investigadores, han rebajado su fortaleza a "tan solo" 69 bits.

Incluso se han encontrado dos ejemplos de ficheros "pdf" que se resumen en el mismo valor usando la función SHA-1.

### Función SHA-2

Se trata en realidad de una familia de cuatro funciones: SHA-224, SHA-256, SHA-384, SHA-512.

El número representa el tamaño del resumen en bits, para cada una.

### Funciones SHA-256 y SHA-224

A igual que SHA-1, SHA-256 utiliza bloques de mensajes de 512 bits.

Sin embargo, los bloques resumen son de 256 bits, manejados en palabras de 32 bits, con un total de 8 palabras.

La función de compresión cambia ligeramente respecto a la de SHA-1.

SHA-224 es idéntico a SHA-256: simplemente se cambia el vector inicial, IV y, al finalizar el proceso, se extraen tan solo 224 bits.

### Funciones SHA-512 y SHA-384

Estas dos funciones manejan bloques de mensajes de 1024 bits.

Los bloques resumen son de 512 bits, manejados en palabras de 64 bits, con un total de 8 palabras.

La función de compresión cambia también ligeramente respecto a la de SHA-1, para tener en cuenta los mayores tamaños.

SHA-384 es idéntico a SHA-512: simplemente se cambia el vector inicial, IV y, al finalizar el proceso, se trunca la salida a tan solo 384 bits.

### Seguridad en SHA-2

Hasta la fecha, no se conocen ataques a esta familia de funciones resumen, por lo que ofrecen la seguridad estándar: 128 o 256 bits frente a colisiones, lo cual es un valor suficiente a día de hoy.

### Función SHA-3

En 2007 el NIST lanzó un concurso para un nuevo algoritmo de resumen, que fuera, por diseño, totalmente distinto a lo existente previamente.

El ganador de la competición para una nueva función resumen fue Keccak, con el nombre de SHA-3.

### Función SHA-3: características

El núcleo de Keccak es una función esponja, con un estado de 1600 bits.

Deglute bloques de mensajes de 1152, 1088, 832, o 576 bits, para dar lugar a resúmenes de 224, 256, 384, o 512 bits, respectivamente.

Keccak también da lugar a dos algoritmos, SHAKE128 y SHAKE256, que permiten producir resúmenes de longitud variable, con seguridades de 128 y 256 bits respectivamente.

### Seguridad de SHA-3

No se conoce ningún ataque a este algoritmo, por el momento.

Dado su historial, no parece probable que se encuentre ninguno en bastante tiempo.

## 2. Códigos de autenticación de mensajes (MAC)

### Códigos de autenticación de mensajes

Un código de autenticación de mensaje es una primitiva criptográfica que permite proteger la integridad y autenticar un mensaje. Un MAC funciona de manera análoga a una función resumen, donde el resumen depende no solo del mensaje sino también de una clave. Por ello, a veces hablamos también de un MAC como una función resumen con clave.

### Motivación para los MACs

Hay muchos momentos en que se necesita garantizar la integridad y autenticar un mensaje:

- Operaciones bancarias.
- Certificación de software.
- Gestiones telemáticas con la Administración Pública.

### ¡Importante!

La integridad/autenticación es totalmente independiente de la confidencialidad. Puede siempre haber una sin la otra, las dos o ninguna.

### Códigos de autenticación de mensajes: definición

**Definición 16:** Un MAC consiste en una triplete de algoritmos (GEN, MAC, VER) donde:

1. GEN es un algoritmo probabilístico que, tomando como entrada un parámetro de seguridad de n bits, devuelve una clave aleatoria k de tamaño al menos n bits.

2. MAC es un algoritmo probabilístico que toma como entrada un mensaje m y, para cierta clave k, devuelve una etiqueta t.

3. VER es un algoritmo determinista de verificación, tal que tomando una etiqueta t, una clave k y un mensaje m devuelve 1 si la etiqueta es correcta y 0 en caso contrario.

### Códigos de autenticación de mensajes: comentario

**Comentario 17:** Dado un mensaje y una clave k, se calcula una etiqueta a partir del par (m, k), t invocando la función MAC:

```
t ← MAC_k(m)
```

que puede ser probabilística.

La verificación se realiza invocando la función VER sobre un mensaje m y una etiqueta t, para cierta clave k:

```
VER_k(m, t) = { 1  si la verificación es correcta
              { 0  si la verificación es incorrecta
```

### Códigos de autenticación de mensajes: corrección

Para que el MAC sea correcto, se debe cumplir que:

```
Pr[VER_k(m, MAC_k(m)) = 1] = 1
```

### Integridad y autenticación

**Ejemplo 18:** Si dos usuarias, Alicia y Begoña, comparten una clave k, Alicia puede enviar a Begoña un mensaje m junto con la etiqueta t, generada como t = MAC_k(m).

### Integridad y autenticación: verificación

El receptor (Begoña) recibe m' y t', pues no puede estar segura si el mensaje o la etiqueta han sido modificados por el camino.

Pero Begoña conoce la clave k, y puede comprobar si:

```
VER_k(m', t') = 1
```

Si la verificación es correcta, es señal de que:

1. el mensaje se ha recibido íntegramente (integridad);
2. el mensaje procede de Alicia, con quien comparte k (autenticación).

### Propiedades de un MAC

- Admite mensajes de longitud arbitraria.
- Proporciona etiquetas de longitud fija.
- Es simétrico.
- Proporciona integridad de mensajes.
- Proporciona autenticación de emisores.

### Seguridad en un MAC

Intuitivamente, consideramos seguro un MAC si un adversario A (de tiempo polinómico en el parámetro de seguridad) no es capaz de falsificar una etiqueta para un "nuevo" mensaje (es decir, no autenticado previamente) si desconoce la clave k.

### Seguridad en un MAC: modelado

Modelamos el adversario con las siguientes capacidades:

- tener acceso a múltiples parejas de mensaje/etiqueta previamente transmitidas;
- tener acceso oracualar a la función MAC_k(·), de manera que pueda obtener (un número polinómico de) etiquetas correspondientes a mensajes de su elección.

### Seguridad en un MAC: experimento

Diseñamos el experimento (que llamamos FalsifMAC(n)) donde interviene el atacante:

1. Se genera una clave k ejecutando el algoritmo GEN(1^n).

2. El adversario A recibe acceso oracualar a la función MAC_k(·).

3. El adversario A puede invocar el oráculo un número polinómico de veces en el parámetro de seguridad n sobre mensajes de su elección, que se almacenan en el conjunto.

4. El adversario A gana el juego (y el experimento devuelve valor 1) si es capaz de generar una pareja (m*, t*) tal que:

```
VER_k(m*, t*) = 1
```

y m* ∉ (conjunto de mensajes previamente consultados).

### Seguridad en un MAC: definición formal

**Definición 19:** Un código de autenticación de mensajes Π = (GEN, MAC, VER) se denomina existencialmente infalsificable bajo el ataque del mensaje elegido si para cualquier adversario A de tiempo polinómico se tiene que:

```
Pr[FalsifMAC,Π(n) = 1] ≤ ng(n)
```

### Creando MACs a partir de funciones resumen

Para construir un MAC, una estrategia común es apoyarse en las funciones resumen. La idea es aplicar una función resumen H sobre el mensaje concatenado con la clave.

Tenemos dos posibilidades:

1. MACs con prefijo secreto:
   ```
   MAC_k(m) = H(k || m)
   ```

2. MACs con sufijo secreto:
   ```
   MAC_k(m) = H(m || k)
   ```

Ambas tienen potencialmente debilidades.

### Falsificando MACs con prefijo secreto

Si la función resumen H responde al esquema de Merkle-Damgård (como, por ejemplo, las funciones SHA-2), se puede realizar el ataque por extensión.

Un atacante intercepta el mensaje m y su MAC, t. Puede, entonces, añadir un nuevo bloque (en realidad tantos como quiera) al mensaje original, sea m_a, y calcular un nuevo (y válido) MAC:

```
m' ← m || m_a
t' ← H(t || m_a)
```

y enviar al destinatario las falsificaciones m' y t'.

### Falsificando MACs con prefijo secreto: validación

Observemos que, por construcción y aunque ignora la clave, las falsificaciones verifican correctamente:

```
t' = H(k || m')
```

y el receptor acepta como íntegro y auténtico el mensaje falsificado.

### Falsificando MACs con sufijo secreto

A la vista de la experiencia, parece obvio que... ¡mejor usamos el sufijo secreto!

Aunque así, existe una debilidad: supongamos que el atacante encuentra una colisión en la función resumen, de modo que existen dos posibles mensajes, m₁ y m₂, tales que H(m₁) = H(m₂).

### Falsificando MACs con sufijo secreto: colisión

En tal caso, por la manera iterativa en que se genera un resumen en el esquema de Merkle-Damgård, se verifica que:

```
H(m₁ || k) = H(m₂ || k)
```

para cualquier valor de k.

**Comentario 20:** Queda claro, entonces, que un MAC con sufijo secreto queda protegido por la dificultad de encontrar una colisión en la función resumen H que se esté usando.

### Mejorando: HMAC

Para paliar esos problemas, se propuso en 1996 un sistema más sofisticado que combina funciones resumen internas y externas.

Dado una función resumen, H, un mensaje, m, y una clave k, el HMAC se calcula de la siguiente manera:

```
HMAC_k(m) = H(S_O || H(S_I || m))
```

### Parámetros en el HMAC

Los valores S_I y S_O (interno y externo) se calculan así:

```
S_I = k+ ⊕ RI
```

donde k+ es la clave a la que se agregan suficientes ceros por la izquierda hasta completar la longitud del bloque de mensaje. El valor RI (relleno interno) está fijado al valor (en hexadecimal) 36363636... repetido tantas veces como sea necesario hasta alcanzar la longitud del bloque de mensaje.

### Parámetros en el HMAC: continua

Análogamente se procede con el valor S_O:

```
S_O = k+ ⊕ RO
```

donde k+ tiene el mismo significado y el relleno externo, RO, es la repetición del valor hexadecimal 5c5c5c...

**Comentario 21:** Se puede decir que el resumen "interno" genera un resumen del mensaje; mientras que el resumen "externo" equivale a un MAC aplicado al resumen "interno": es el paradigma HMAC, es decir, hash-and-MAC.

### Seguridad del HMAC

Los mismos autores del esquema muestran que la seguridad del esquema es esencialmente la de la función resumen subyacente.

Si aparecen ataques (por ejemplo, colisiones) en la función resumen, se puede armar un ataque contra el HMAC.

### MAC derivados de un cifrador de bloque

También llamados CMAC, se trata de una autenticación de mensajes que usa directamente un cifrador de bloque como función resumen.

### Un predecesor: CBC-MAC

Las primeras propuestas datan de los años 70: usar DES como un cifrador de bloque base, y un mecanismo iterativo similar al modo CBC.

Dado un mensaje m y una clave k, dividimos el mensaje en r bloques m₁, m₂, ..., m_r y definimos el CBC-MAC t como t = CBC-MAC(k, m) = h_r, calculándolo como sigue:

```
h₀ = IV; h_i = E_k(h_{i-1} ⊕ m_i), 1 ≤ i ≤ r
```

donde IV es públicamente conocido.

### Un predecesor: CBC-MAC (observación)

Observemos que los valores intermedios, h_j, no son visibles externamente, ni se transmiten al receptor.

El receptor comprueba la validez del código aplicando el mismo algoritmo (no hay que descifrar nada) siempre, obviamente, que conozca la clave k.

E puede ser cualquier cifrador de bloque.

### ¿Es seguro el CBC-MAC?

No, porque en ciertos casos, se puede falsificar una pareja etiqueta mensaje a partir de dos parejas etiqueta/mensaje conocidas, aunque sin conocer la clave.

Consideremos dos mensajes monobloque, m₁ y m₂, y sus correspondientes etiquetas CBC-MAC, t₁, t₂. En tal caso, resulta que t₂ también es la etiqueta del CBC-MAC correspondiente al mensaje:

```
m₁ ⊕ m₂ ⊕ t₁ ⊕ IV
```

### ¿Es seguro el CBC-MAC? (prueba)

En efecto, por el carácter iterativo del proceso, se tiene que:

```
h₁ = E_k(h₀ ⊕ m₁) = t₁
h₂ = E_k(h₁ ⊕ (m₂ ⊕ t₁ ⊕ IV))
   = E_k(t₁ ⊕ m₂ ⊕ t₁ ⊕ IV)
   = E_k(h₀ ⊕ m₂) = t₂
```

**Comentario 22:** De ordinario, se escoge IV como el vector 0, con lo que en la anterior expresión no es necesario sumarlo.

### Arreglando el CBC-MAC: CMAC

Para arreglar el CBC-MAC, se utiliza la estrategia de cambiar de clave justo para el último bloque.

Para ello, derivamos dos claves, k₁ y k₂ a partir de k:

```
L = E_k(0^n)

k₁ = { L ≪ 1              si MSB(L) = 0
     { (L ≪ 1) ⊕ 0x87    si MSB(L) = 1

k₂ = { k₁ ≪ 1             si MSB(k₁) = 0
     { (k₁ ≪ 1) ⊕ 0x87   si MSB(k₁) = 1
```

### Proceso del CMAC

CMAC funciona igual que CBC-MAC, excepto con relación al último bloque.

1. Si el último bloque tiene exactamente el tamaño de bloque del cifrador, entonces suponiendo r bloques para un mensaje m, con clave k:
   ```
   CMAC(k, m) = E_k(h_{r-1} ⊕ m_r ⊕ k₁)
   ```

2. Si el último bloque m_r tiene menos bits que el tamaño de bloque del cifrador, se completa por la derecha con un 1 y suficientes 0s, es decir, m'_r = m_r || (10...0) y:
   ```
   CMAC(k, m) = E_k(h_{r-1} ⊕ m'_r ⊕ k₂)
   ```

## 3. Cifrado autenticado

### Seguridad CCA

Afrontamos ahora la creación de sistemas criptográficos resistentes frente a un adversario CCA.

Tal adversario es activo y puede distorsionar a su antojo los criptogramas que circulen por el canal público.

En este tipo de ataque, que llamamos CCA, modelamos al adversario como alguien con acceso oracualar tanto a la función de cifrado como de descifrado, en un número de veces polinómico en el parámetro de seguridad n.

### Modelo de seguridad CCA

Sea el siguiente experimento (que llamamos IndisCCA(n) o de la indistinguibilidad) donde interviene el adversario y un retador:

1. Se genera una clave k ejecutando Gen(1^n).
2. A genera dos mensajes de igual longitud, m₀, m₁ y los envía al retador.
3. El retador elige un bit b ∈ {0,1} aleatoriamente, calcula c ← E_k(m_b) y envía c a A.
4. A puede hacer uso de los oráculos tanto cuanto quiera (con la consabida restricción polinómica), excepto que no puede pedir el descifrado de c.
5. A devuelve un bit b' y gana el juego si b' = b, con lo que el experimento devuelve 1.

### Formalizando la seguridad CCA

**Definición 23:** Decimos que un criptosistema Π con parámetro de seguridad n es indistinguible bajo el ataque del criptograma elegido (CCA-seguro) si para cualquier adversario de tiempo polinómico, existe una función insignificante, ng(n), tal que:

```
Pr[IndisCCA,Π(n)] ≤ 1/2 + ng(n)
```

**Comentario 24:** Esta seguridad se abrevia con las siglas IND-CCA y es el tipo de seguridad que se exige a día de hoy.

### Inseguridad CCA de esquemas anteriores

Recordemos el esquema CPA-seguro que construimos con una función aleatoria, F, y una clave k. La función cifrado E_k(m) se define como:

```
c = E_k(m) = (r, s)
```

donde r es un valor aleatorio y s = F_k(r) ⊕ m. El descifrado es:

```
m = D_k(r, s) = F_k(r) ⊕ s
```

**Hecho 25:** Este esquema no es CCA-seguro.

### Inseguridad CCA de esquemas anteriores: ataque

Consideremos este ataque:

1. El adversario elige mensajes m₀ = 0^n y m₁ = 1^n.
2. El retador envía al adversario uno de ellos cifrado, c = (r, s).
3. El adversario crea un c' = (r, s'), donde s' es igual a s con el primer bit invertido y se lo manda al retador para que se lo descifre (es legítimo pues c ≠ c').
4. El retador contesta con dos posibles textos claros: o bien 10^(n-1), con lo que b = 0; o bien 01^(n-1), con lo que b = 1.

### Un paso más: cifrado autenticado

Necesitamos primitivas más seguras, que ofrezcan seguridad CCA. Entre ellas está la siguiente, que es CCA-segura (y más):

**Definición 26:** La primitiva criptográfica que ofrece simultáneamente confidencialidad (cifrado de la información) e integridad de datos se denomina cifrado autenticado, o AE por sus siglas en inglés.

### Definiendo el cifrado autenticado

Vamos a diseñar un experimento (FalsifCript(n)) que permita asegurar la integridad del cifrado: lo llamamos infalsificabilidad existencial. Consideremos este juego:

1. Se genera una clave k ejecutando Gen(1^n) y recibe acceso al oráculo de cifrado, E_k(·).
2. A pide al oráculo el cifrado de todos los mensajes que quiera (un número polinómico en n de ellos) y estos los guarda en el conjunto. Finalmente emite un criptograma c*, que envía al retador. Este lo descifra calculando, m* = D_k(c*).
3. A gana el reto (y el resultado del experimento es 1) si m* es válido y m* ∉ (conjunto de mensajes).

### Definiendo el cifrado autenticado: formal

**Definición 27:** Un esquema criptográfico Π con parámetro de seguridad n es existencialmente infalsificable si para cualquier atacante de tiempo polinómico probabilístico existe una función insignificante ng(n) tal que:

```
Pr[FalsifCript,Π(n) = 1] ≤ ng(n)
```

### Definiendo el cifrado autenticado: final

**Definición 28:** Un esquema de cifrado de clave secreta es un esquema de cifrado autenticado si y solo si es CCA-seguro y además es existencialmente infalsificable.

### Servicios de seguridad esperables de la AE

Capacidad de soportar los más fuertes ataques tanto a la confidencialidad (ha de comportarse como un cifrador robusto) como a la integridad (ha de comportarse como un MAC robusto).

Deseables también son criterios de desempeño o eficiencia:

- que sea paralelizable;
- que pueda funcionar en modo flujo;
- que su implementación sea barata en términos de recursos: necesidad de cómputo y memoria.

### Construyendo primitivas AE: una combinación genérica

La primera idea para crear una primitiva AE es combinar un cifrador robusto con un MAC robusto. Consideramos tres posibles combinaciones:

1. Cifrado y MAC (en paralelo).
2. MAC y después cifrar.
3. Cifrar y después MAC.

En lo que sigue, K_C será la clave de cifrado para el cifrador E, K_I será la clave para el MAC S.

### Cifrado y MAC

Dado un mensaje, m, se tiene C = E_K_C(m) y T = S_K_I(m).

El emisor envía el par (C, T) al receptor.

En este esquema, el cifrado y el MAC se calculan independientemente y, por tanto, son paralelizables.

### Seguridad en Cifrado y MAC

El receptor recibe (C', T'), descifra C' y obtiene m'.

Calcula la etiqueta S_K_I(m') y comprueba si coincide con T' para verificar la coincidencia.

**Comentario 29:** En teoría, el mecanismo podría tener problemas si el MAC no tiene el suficiente carácter de "aleatoriedad". Si el MAC es determinista, no tenemos ni siquiera seguridad CPA. Aún así, se ha empleado en algunos protocolos reales, como SSH.

### MAC y después cifrar

Dado m, el emisor calcula T = S_K_I(m).

A continuación, concatena el mensaje y la etiqueta T, dando lugar a m' = m || T.

Por último, genera el cifrado C = E_K_C(m') y lo envía al receptor.

### Seguridad en MAC y después cifrar

El receptor descifra C' y separa el mensaje, m', de la etiqueta T'. Después comprueba si T' = S_K_I(m').

**Comentario 30:** En este esquema, la etiqueta queda oculta a la vista del atacante y eso es ventajoso. Aún así, el receptor se ve obligado a descifrar lo que le llegue y comprobar después si lo obtenido es realmente un mensaje válido o no, lo cual da pie a los llamados ataques oraculares al relleno (padding-oracle attacks). El protocolo SSL los ha sufrido y ha terminado siendo sustituido por TLS.

### Cifrar y después MAC

Para un mensaje, m, el emisor calcula primero C = E_K_C(m).

Después calcula T = S_K_I(C) y envía al receptor el par (C, T).

### Seguridad en Cifrar y después MAC

El receptor recibe (C', T') y comprueba la integridad de C', es decir, si T' = S_K_I(C').

- En caso afirmativo, acepta el cifrado y procede a recuperar el mensaje.
- En caso negativo, descarta el mensaje sin intentar descifrarlo.

**Comentario 31:** Este sistema es el más ventajoso pues un receptor solo intentará descifrar cuando el criptograma se revele íntegro. Por tanto, el atacante ha de quebrantar en primer lugar el MAC para poder acceder a la máquina de descifrado. Este mecanismo es usado por IPsec, un protocolo de seguridad de capa red.

### Cifrado autenticado... de verdad

Hasta ahora hemos visto combinaciones que podrían valer, pero...

- lo que queremos realmente es una verdadera primitiva, AE, tal que:

```
(C, T) = AE(K, m)
```

es decir, dada una clave K y un mensaje m, AE nos debe devolver atómicamente el cifrado del mensaje y un código MAC de integridad.

### Cifrado autenticado... de verdad (continua)

Y, recíprocamente, debe existir también la primitiva AD, inversa de la anterior, tal que:

```
m = AD(K, C, T)
```

si todo es correcto, o bien un mensaje de error (que llamamos el token '⊥').

### Un paso más: datos asociados

Dando un paso más, resulta sumamente útil en la práctica poder autenticar un conjunto de datos pero cifrando solamente una parte de ellos.

**Ejemplo 32:** Si, por ejemplo, queremos cifrado autenticado de un datagrama IP, obviamente no debemos cifrar la cabecera IP: ¡el datagrama nunca se sería enrutado a su destino!

Pero, al mismo tiempo, deseamos una autenticación de todo el datagrama, incluyendo cabeceras, para asegurarnos de que llega al destinatario pretendido.

### Cifrado autenticado con datos asociados, AEAD

Para satisfacer esas necesidades, creamos AEAD.

Sea un mensaje m (que queremos cifrar), unos datos asociados a (que queremos tan solo autenticar) y una clave K, la nueva primitiva funciona así:

```
(C, T, a) = AEAD(K, m, a)
```

donde C es el criptograma correspondiente a m y T es el código de autenticación de todo, es decir, de m y de a.

### Cifrado autenticado con datos asociados, AEAD (continua)

**Comentario 33:** Observemos en passant que, si a está vacío, tenemos un cifrado autenticado ordinario; si m está vacío, tenemos un puro MAC.

**Comentario 34:** Para descifrar, tenemos la primitiva recíproca, ADAD, tal que:

```
(m, a) = ADAD(K, C, T, a)
```

que devolverá ⊥ si alguno de los parámetros de entrada es espurio.

### Condición de corrección de AEAD

La condición de corrección exige que:

```
Pr[(m, a) = ADAD(K, AEAD(K, m, a))] = 1
```

Además, para ofrecer seguridad CPA, el esquema AEAD debe manejar internamente ciertos valores aleatorios, que se suelen llamar nonces (por que no deben repetirse).

### Caso de estudio: GCM (contador de Galois)

Se trata de un AEAD basado en nonces y estandarizado por el NIST en 2007.

GCM responde al modelo Cifrar y después MAC.

Utiliza un cifrador de bloque (en la práctica, siempre AES) con bloques de 128 bits, en modo contador.

El MAC está construido usando una función específica llamada GHASH, que necesita también del cifrador en bloque.

### Descripción del GCM

Tomamos como entrada una clave K, un mensaje m (completado con suficientes ceros para que su longitud sea múltiplo de 128), unos datos asociados, AD (completados del mismo modo) y un nonce, n ∈ {0,1}^96.

Generamos la clave para GHASH:

```
K_A ← E_K(0^128)
```

Calculamos el valor inicial del contador:

```
x ← (n || 0^31 1) ∈ {0,1}^128
x' ← x + 1
```

valor inicial para el contador.

### Parte de cifrado

El cifrado se hace en modo contador; por tanto, cada bloque del mensaje, m_j, se cifra independientemente usando el valor del contador x' + j:

```
c_j = E_K((x' + j)) ⊕ m_j
```

para dar el bloque de criptograma c_j. Llamemos C al criptograma completo.

**Comentario 35:** Por construcción, el contador incrementa solamente los 32 bits menos significativos. Esto significa que podemos cifrar mensajes que tengan, como máximo, 2^32 bloques.

### Parte de autenticado

Para el autenticado, además de la suma, usaremos la operación de multiplicación en el cuerpo de Galois GF(2^128), visto como el cociente ℤ_2[x]/(p(x)), con p(x) = x^128 + x^7 + x^2 + x + 1.

Como en el caso del AES, definimos la inyección natural φ_ℓ que asigna a una cadena de ℓ bits un polinomio de grado ℓ en ℤ_2[x] (y viceversa) de la siguiente manera:

```
φ_ℓ: {0,1}^ℓ ↪ ℤ_2[x]
(b_ℓ-1, b_ℓ-2, ..., b₁, b₀) ↦ b_ℓ-1·x^(ℓ-1) + b_ℓ-2·x^(ℓ-2) + ... + b₁·x + b₀
```

En nuestro caso, ℓ = 128.

### Parte de autenticado (continua)

Formamos ahora la concatenación:

```
AAD = (AD || C || (long(AD)||long(C)))
```

Obviamente AAD es una lista de, digamos t, bloques de 128 bits, que indexaremos como AAD_j.

### Parte de autenticado (continua 2)

Ahora realizamos en el GF(2^128) la evaluación de este polinomio:

```
M = Σ(j=0 a t-1) φ_128(AAD_j) · (φ_128(K_A))^(t-j)
```

### Parte de autenticado (final)

Comentario 36: M es un elemento del GF(2^128) que, una vez convertido en un bloque de bits (aplicando φ_128^{-1}) constituye el resultado de la función GHASH, y podemos escribir como:

```
GHASH(K_A, C, AD) = φ_128^{-1}(M)
```

Observemos que, en efecto, M depende de K_A, C, y AD, luego GHASH también.

### Parte de autenticado (GMAC)

Con esto ya estamos en disposición de calcular el MAC, que llamaremos en nuestro caso GMAC:

```
GMAC(K, x) ⊕ GHASH(K_A, C, AD) = E_K(x)
```

### Arquitectura GMAC

```
Diagrama de la arquitectura GMAC con contadores, cifrado y GHASH.
```

### Seguridad en GCM: atacando la confidencialidad

El GCM es muy sensible a usar nonces repetidos (¡nunca debiera hacerse!).

Sea un GCM con cierta clave K para cifrar y autenticar dos mensajes m y m', con sus respectivos datos asociados AD y AD', pero repetimos el mismo nonce. El valor del contador x será el mismo para los dos, y:

```
c_j = E_K((x' + j)) ⊕ m_j
c'_j = E_K((x' + j)) ⊕ m'_j
```

### Seguridad en GCM: atacando la confidencialidad (continua)

Pero de lo anterior se deduce que:

```
c_j ⊕ c'_j = m_j ⊕ m'_j
```

con lo que la confidencialidad queda destruida.

### Seguridad en GCM: calculando K_A

Además, la clave K_A queda comprometida. En efecto, tendríamos:

```
GMAC(K, m, AD) = E_K(x) ⊕ GHASH(K_A, C, AD)
GMAC(K, m', AD') = E_K(x) ⊕ GHASH(K_A, C', AD')
```

Pero, a igual que antes:

```
GMAC(K, m, AD) ⊕ GMAC(K, m', AD') = GHASH(K_A, C, AD) ⊕ GHASH(K_A, C', AD')
```

### Seguridad en GCM: calculando K_A (continua)

**Comentario 37:** Como el adversario conoce C, C', AD y AD' y la operación GHASH es esencialmente lineal, puede averiguar el valor K_A.

### Seguridad en GCM: claves débiles

Recordemos que:

```
GHASH(K_A, C, AD) = φ_128^{-1}(M)
```

y:

```
M = Σ(j=0 a t-1) φ_128(AAD_j) · (φ_128(K_A))^(t-j)
```

### Seguridad en GCM: claves débiles (continuación)

Hay casos particularmente muy malos:

1. si K_A = 0, obviamente M = 0, GHASH = 0, y GMAC(K, m, AD) = E_K(x) para no importa qué m, AD.

2. si K_A = 1, GHASH = ⊕ c_j, sin que el orden de los bloques del criptograma altere el valor del GMAC.

3. a veces ocurre que las potencias de K_A en el GF(2^128) forman un subgrupo cíclico muy pequeño, es decir (φ_128(K_A))^ℓ = φ_128(K_A), para un valor ℓ pequeño. Esto destruye la seguridad del GMAC.

### Seguridad en GCM: claves débiles (final)

**Comentario 38:** Estas claves se denominan débiles y deben ser evitadas.
