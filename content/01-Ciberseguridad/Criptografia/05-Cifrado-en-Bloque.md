# 3.2 Criptografía simétrica: cifrado en bloque
Máster en Ciberseguridad | Raúl Durán Díaz | Curso académico 2024–2025
## Contenidos
1. Funciones y permutaciones pseudo-aleatorias
2. Cifrado en bloque
3. Cifrador DES
4. Cifrador AES
5. Modos de operación
## 1. Funciones y permutaciones pseudo-aleatorias
## # Funciones pseudo-aleatorias
Las funciones pseudo-aleatorias generalizan la idea de los generadores pseudo-aleatorios. Para fijar ideas, nos restringimos a {Func}_n, conjunto de todas las funciones que mapean cadenas de n bits a cadenas de n bits. Si f ∈ {Func}_n, entonces f: {0,1}^n : {0,1}^n.
El cardinal de {Func}_n es finito y vale:
```
|{Func}_n| = 2^( n·2^n)
```
**Ejemplo 1:** Si n = 3, el número de posibles funciones {0,1}³ : {0,1}³ es, en total, 2^( 3·2³) = 2²⁴ = 16777216.
## # Definición de función pseudo-aleatoria
Si extraigo de manera totalmente aleatoria una función f ∈ {Func}_n, puedo hablar de una "función aleatoria". Ahora imagino que tengo una forma de seleccionar funciones de {Func}_n que depende de un parámetro n, ξ: {0,1}^ℓ( n) : {Func}_n, donde ℓ( n) es polinómica en n.
Si ocurre que, cuando doy valores de manera aleatoria k ∈ {0,1}^ℓ( n), obtengo funciones F_k = ξ( k) de tal manera que esa selección parece aleatoria... entonces hablamos de funciones pseudo-aleatorias.
## # Formalizando las funciones pseudo-aleatorias
Vamos a suponer un discriminador D con acceso a un oráculo O, que es o bien una función f extraída aleatoriamente o bien una función F_k extraída pseudo-aleatoriamente mediante ξ. El discriminador pide al oráculo que evalúe valores x elegidos por él. Puede invocar al oráculo un número de veces polinómico en n.
## # Definición formal de la función pseudo-aleatoria
**Definición 2:** Una función F_k: {0,1}^n : {0,1}^n es pseudo-aleatoria si para cualquier discriminador D de tiempo polinómico ocurre que:
```
|Pr[D^( F_k (·))( 1^n) = 1] - Pr[D^( f (·))( 1^n) = 1]| ≤ ng ( n)
```
donde la primera probabilidad se toma sobre la elección uniformemente aleatoria de k ∈ {0,1}^n, la segunda sobre la elección uniformemente aleatoria de f ∈ {Func}_n y para ambas la aleatoriedad propia de D.
## # Funciones y generadores pseudo-aleatorios
Podemos usar las funciones pseudo-aleatorias para construir un generador pseudo-aleatorio que tenga una salida de tamaño fácilmente ajustable. Si F_k ( x) es una función pseudo-aleatoria con salida de n bits, podemos construir un generador G que produzca salidas múltiplos de n así:
```
G ( s) := F_s ( IV || ⟨0⟩) || F_s ( IV || ⟨1⟩) || F_s ( IV || ⟨2⟩) || ...
```
es decir, concatenamos las salidas de F_s evaluadas en valores arbitrarios pero distintos.
## # Propiedades del generador
El generador G así definido puede generar bloques de n bits hasta el agotamiento del contador. El vector IV permite controlar el comienzo de la sucesión generada. G es pseudo-aleatorio: de lo contrario, podríamos construir un discriminador para F_k, que dejaría de ser pseudo-aleatoria.
## # Permutaciones pseudo-aleatorias
Sea ahora {Perm}_n ⊂ {Func}_n el conjunto de las permutaciones de las cadenas de n bits, es decir, las funciones biyectivas. Puesto que existen 2^n posibles cadenas de n bits, el cardinal de ese conjunto será:
```
|{Perm}_n| = ( 2^n)!
```
## # Definición de permutación pseudo-aleatoria
Definimos ahora una permutación pseudo-aleatoria de la misma manera que en el caso de las funciones. Tenemos ahora funciones F_k ∈ {Perm}_n, es decir, permutaciones que dependen de una clave k.
Informalmente, F_k será una permutación pseudo-aleatoria si está seleccionada de su espacio muestral de tal manera que parece una selección uniformemente aleatoria.
**Comentario 3:** Observemos que, trivialmente, si F_k es una permutación pseudo-aleatoria, también es una función pseudo-aleatoria.
## # Algunas propiedades de las permutaciones
- Dependencia entre bits: cada bit de la permutación es una función compleja de todos los bits de la clave y todos los bits del bloque permutado.
- Un cambio de un bit del bloque de entrada produce un cambio del 50% de los bits del bloque permutado.
- Análogamente, un cambio de un bit de la clave produce un cambio del 50% de los bits del bloque permutado.
## 2. Cifrado en bloque
## # Definición de cifrado en bloque
**Definición 4:** Sistema en el que los símbolos se agrupan en bloques de tamaño dado y se cifran permutando cada bloque por otro con una permutación dependiente de la clave.
**Comentario 5:** Normalmente los símbolos son bits. Tamaños típicos de bloque son 64, 128 o 256 bits. Observemos que la permutación debe ser de las que consideramos pseudo-aleatorias. Curiosamente, el cifrado por transposición puede considerarse una forma de cifrado en bloque pues es una permutación de símbolos.
## # Seguridad del cifrado en bloque frente a CPA
De manera ingenua, podríamos fijar un tamaño de bloque n y definir la función de cifrado como una permutación, dependiente de una clave k, de los bits del mensaje:
```
E_k ( m) = F_k ( m)
```
**Comentario 6:** Claramente, así definido el cifrado en bloque no es CPA-seguro, pues cada mensaje da lugar a un único criptograma.
## # Fortaleciéndose el cifrado en bloque
Para lograr seguridad frente a CPA, introducimos el cifrado probabilístico, que consta de los siguientes algoritmos:
1. k ← Gen ( 1^n), que genera una clave uniforme k ∈ {0,1}^n.
2. c ← E_k ( m, r), donde m ∈ {0,1}^n es el mensaje, r ∈ {0,1}^n es un valor aleatorio y el criptograma se calcula:
```
s = F_k ( r) ⊕ m
```
El criptograma c es el par ( s, r).
3. Dado un criptograma c = ( s, r), el mensaje se recupera mediante:
```
m = F_k ( r) ⊕ s
```
## # Seguridad CPA del cifrado probabilístico
El esquema anterior es CPA-seguro si F_k es una función pseudo-aleatoria. El valor r está generado también aleatoriamente... y se usa solo una vez!
**Comentario 7:** La idea es que si un atacante tiene éxito, se podría usar como oráculo para distinguir si F_k es una función pseudo-aleatoria o es verdaderamente aleatoria. Pero esto no puede ocurrir si F_k es verdaderamente pseudo-aleatoria.
Observemos que F_k no necesita ser una permutación: basta que sea una función pseudo-aleatoria, pues no necesitamos invertirla.
## # Realización práctica del cifrado en bloque
Para el cifrado en bloque necesitamos en la práctica un par de "primitivas":
- Confusión:** Primitiva que trata de ofuscar la relación entre la clave y el criptograma.
- Difusión:** Primitiva que trata de distribuir la influencia del cambio de un solo símbolo del texto en claro sobre todos los símbolos del criptograma, para disimular las posibles propiedades estadísticas del texto claro.
## # Paradigma confusión-difusión de Shannon
Para implementar el paradigma confusión-difusión, se utiliza una idea de Shannon:
- Confusión: se construye una permutación ( pseudo-aleatoria) F con un bloque grande a base de combinar muchas permutaciones {f_i} de bloque pequeño.
- Difusión: se intercambian los bloques pequeños entre sí.
Ese esquema se repite varias veces ( lo que llamamos rondas), aplicando en cada ronda una clave distinta, derivada de la clave principal.
## # Ejemplo de confusión-difusión
Para fijar ideas, supongamos que F tiene una longitud de bloque de 128 bits y supongamos una familia de funciones {f_i} con longitud de bloque 8 bits.
Introducimos la confusión así:
```
F ( x) = f₁( x₁) || ... || f₁₆( x₁₆)
```
A continuación introducimos la difusión "barajando" los bloques x_i. Dicho más formalmente, tomamos una permutación σ ∈ S₁₆ de modo que:
```
x'₁ = x_σ( 1), x'₂ = x_σ( 2), ..., x'₁₆ = x_σ( 16)
```
Ahora los bloques x'_i son de nuevo sometidos a confusión, generando así nuevos bloques que serán "barajados" de nuevo. Cada repetición o ronda puede ser realizada de manera dependiente de una clave distinta, derivada de la clave principal.
## # Arquitectura práctica del cifrado en bloque
Lo dicho se puede resumir en estos pasos:
1. Transformación inicial.
2. Iteración de una función de cifrado ( no especialmente robusta).
3. Transformación final.
Además, necesitamos una función de derivación de sub-claves a partir de la clave del sistema.
```
K ( clave original)
 |
 Expansión de clave
 | | |
 k₁ ... kℓ
 | | |
m ---> Transf --> Cifrado --> Cifrado --> Transf --> c
 inicial vuelta 1 vuelta ℓ final
```
## # Etapas del cifrado en bloque
Las transformaciones inicial y final pueden no tener un significado criptográfico. La función que se itera es no lineal y no debe presentar ninguna estructura algebraica para evitar que la ejecución de las ℓ vueltas equivalga a una sola pasada con otros parámetros, lo que facilitaría el criptoanálisis.
## 3. Cifrador DES
## # Sistema DES
Ganador del concurso que el NIST propuso en los años 70 para definir un sistema criptográfico de clave simétrica. El sistema tenía que poder realizarse sobre un chip microelectrónico. La longitud de clave es de 56 bits.
## # Estructura del DES
La arquitectura del DES es de tipo Feistel, bloque de 64 bits y permutaciones inicial y final ( inversa de la inicial) fijas. Utiliza 16 vueltas, con un tamaño de sub-clave de 48 bits. En total necesita 16×48 = 768 bits de clave, que se derivan mediante una función de expansión de clave, de la clave inicial de 56 bits.
## # Cifrado múltiple
A día de hoy, el tamaño de clave de DES es demasiado pequeño. Para intentar aún así sacar partido:
**Definición 8:** El cifrado múltiple consiste en iterar el cifrado de un texto claro a través de varios cifradores de bloque ( iguales o distintos) aplicando una clave distinta en cada uno de ellos.
## # Seguridad del cifrado múltiple
Hay que asegurarse que la operación del cifrador no presenta alguna propiedad algebraica tal que, para cierto texto claro m y claves K₁ y K₂, se verifique que:
```
E_K₁( E_K₂( m)) = E_K₃( m)
```
lo que significaría que combinar dos claves equivale a una tercera, lo cual no aumentaría la seguridad.
**Comentario 9:** En el caso de DES, no se verifica esa propiedad algebraica.
## # Ataque por encuentro a medio camino
Este ataque provoca una disminución drástica del tamaño efectivo de la clave en un sistema múltiple. Supongamos dos bloques cifrantes E₁ y E₂ con claves K₁ y K₂ de L bits cada una.
```
m ---> E₁( K₁) ---> y ---> E₂( K₂) ---> c
```
Supongamos que tenemos la pareja ( m, c). Tomamos m y lo ciframos con todas las posibles claves de E₁ y hacemos una lista de parejas ( y[i], K₁[i]) para i = 1, 2, ..., 2^L.
Desciframos c con todas las posibles claves de E₂ y hacemos otra lista de parejas ( z[j], K₂[j]) para j = 1, 2, ..., 2^L.
Necesariamente habrá una pareja ( i, j) tal que y[i] = z[j]. La buscamos, por comparación, y cuando la encontremos, habremos determinado K₁ y K₂ como K₁[i] y K₂[j].
En total, si tenemos mala suerte, habremos realizado 2^L cifrados y 2^L descifrados, por lo que la seguridad pasa a ser... ¡L+1 bits!
## # Triple DES
El triple DES ( TDES) presenta la estructura que se ve abajo, y proporciona una seguridad efectiva de 2×56 = 112 bits, aceptable para aplicaciones de seguridad media.
```
m ---> DES ( K₁) ---> DES⁻¹( K₂) ---> DES ( K₃) ---> c
```
**Comentario 10:** Observemos que si el sistema decae a un DES simple de clave K, K₁ = K₂ = K₃ = K, compatible con el sistema antiguo.
## 4. Cifrador AES
## # Cifrador en bloque AES
A finales de los 90, el NIST solicitó propuestas para un nuevo cifrador en bloque, sustituto del DES, al que denominó genéricamente AES. Parte de los requisitos eran:
- Tamaño de bloque de 128 bits.
- Longitudes de clave de 128, 192, y 256 bits.
- Seguridad, eficiencia computacional, simplicidad de diseño, ausencia de patentes.
## # Andthewinneris...
En el año 2000, el NIST anunció que la propuesta ganadora era el Rijndael, un cifrador de bloque creado por dos jóvenes criptógrafos belgas, Vincent Rijmen y Joan Daemen.
El Rijndael presenta un tamaño de bloque y un tamaño de clave de 128, 192, y 256 bits. Sin embargo, el NIST solo aceptó como tamaño de bloque 128 bits. Con esa restricción, el Rijndael se convirtió en el AES, nuevo estándar de cifrado en bloque.
## # Detalles de AES
**Comentario 11:** La estructura interna responde también a la iteración de una operación de cifrado. El número de vueltas depende del tamaño de la clave según esta tabla:
```
Longitud de clave Número de vueltas
128 bits 10
192 bits 12
256 bits 14
```
## # Estado interno de AES
AES maneja un bloque entero de 128 bits en cada iteración. En cada momento el valor del bloque se conoce con el nombre de estado del algoritmo.
El bloque se organiza en cuatro filas y cuatro columnas de bytes, que podemos llamar A_i, con i = 0, 1, ..., 15:
```
A₀ A₄ A₈ A₁₂
A₁ A₅ A₉ A₁₃
A₂ A₆ A₁₀ A₁₄
A₃ A₇ A₁₁ A₁₅
```
El estado A se inicializa con el bloque de entrada y va evolucionando con las transformaciones que se le van aplicando hasta generar el bloque de salida.
## # Estructura de AES
```
Texto claro ( 128 bits) Clave de cifrado ( 128, 192, 256 bits)
 | |
 | Expansión de clave
 | |
 v k₀ |
 Ronda normal: | |
 ( vu <= nr - 1) v |
 - AddRoundKey kⱼ ( j=0..nr-1)
 - SubBytes
 - ShiftRows
 - MixColumns
 Ronda final:
 - AddRoundKey
 - SubBytes
 - ShiftRows
 - AddRoundKey k_nr
 |
 v
Criptograma ( 128 bits)
```
## # Transformaciones en cada vuelta
La transformación que se aplica en cada vuelta se compone en realidad de cuatro etapas:
1. **AddRoundKey:** suma módulo 2 del estado con la subclave correspondiente a la vuelta.
2. **SubBytes:** sustitución no lineal de bytes.
3. **ShiftRows:** desplazamiento cíclico de las filas del estado, aplicando diversos saltos.
4. **MixColumns:** mezcla de columnas.
## # Estructura de AES: detalles
La primera etapa consiste en aplicar una sub-clave, sumándola módulo 2 a la matriz de estado A.
La segunda etapa corresponde a una función fija, independiente de la clave, aplicada a cada byte de A ( fase de confusión).
Las dos últimas etapas corresponden a una permutación, también fija, ( de filas primero, de columnas después) de los bytes de A ( fase de difusión).
## # Última ronda especial
**Comentario 12:** Observemos que en la última ronda, se sustituye la etapa MixColumns por AddRoundKey. Así se evita que el atacante pueda deshacer las dos últimas transformaciones pues, como se ha dicho, son fijas.
## # Cuerpo de Galois GF ( 2⁸)
Matemáticamente, se considera cada A_i como un elemento del cuerpo de Galois GF ( 2⁸) visto como ℤ₂[x]/( p ( x)) y p ( x) = x⁸ + x⁴ + x³ + x + 1.
Definimos la biyección natural φ_ℓ que asigna a una cadena de ℓ bits un polinomio de grado ℓ en ℤ₂[x] ( y viceversa) de la siguiente manera:
```
φ_ℓ: {0,1}^ℓ ↪ ℤ₂[x]
( b_ℓ-1, b_ℓ-2, ..., b₁, b₀) ↦ b_ℓ-1·x^(ℓ-1) + b_ℓ-2·x^(ℓ-2) + ... + b₁·x + b₀
```
En nuestro caso, ℓ = 8.
## # Transformación SubBytes
La operación SubBytes se aplica byte a byte sobre la matriz de estado A. Podemos verla como una única caja S que también es no lineal, de modo que B_i = S ( A_i) para cada i = 0, ..., 15.
Para ello, calculamos A_i⁻¹, visto como un elemento del cuerpo de Galois GF ( 2⁸), lo expresamos como un vector de dimensión 8 sobre el cuerpo ℤ₂ y, finalmente, le aplicamos en ese cuerpo la siguiente transformación afín:
```
B_i = M × A_i⁻¹ + V
```
donde M y V son una matriz y un vector fijados de una vez por todas.
## # Transformación SubBytes en bits
En bits, la transformación se puede escribir así:
```
[b'₀] [1 0 0 0 1 1 1] [a'₀] [1]
[b'₁] [1 1 0 0 0 1 1] [a'₁] [1]
[b'₂] = [1 1 1 0 0 0 1] [a'₂] + [0]
[b'₃] [1 1 1 1 0 0 0] [a'₃] [0]
[b'₄] [0 1 1 1 1 0 0] [a'₄] [0]
[b'₅] [0 0 1 1 1 1 0] [a'₅] [1]
[b'₆] [0 0 0 1 1 1 1] [a'₆] [1]
[b'₇] [1 0 0 0 1 1 1] [a'₇] [0]
```
donde A_i⁻¹ = ( a'₇, ..., a'₀), B_i = ( b₇, ..., b₀).
## # Propiedades de SubBytes
Esta transformación es no lineal, es decir:
```
S ( A₁ + A₂) ≠ S ( A₁) + S ( A₂)
```
Pero es perfectamente invertible, para facilitar el descifrado. Como la matriz M tiene su inversa, se tiene:
```
A_i⁻¹ = M⁻¹ × ( B_i + V)
```
En la práctica no se hacen operaciones, sino se tienen unas tablas preparadas con todos los posibles valores de entrada.
## # Transformación SubBytes inversa
La matriz inversa de M es:
```
[0 0 1 0 0 1 0 1]
[1 0 0 1 0 0 1 0]
[0 1 0 0 1 0 0 1]
[1 0 1 0 0 1 0 0]
[0 1 0 1 0 0 1 0]
[0 0 1 0 1 0 0 1]
[1 0 0 1 0 1 0 0]
[0 1 0 0 1 0 1 0]
```
## # Tabla de inversas en GF ( 2⁸)
Para ayudar a calcular las inversas de los elementos de GF ( 2⁸), se tiene esta tabla ( valores en hexadecimal):
```
 0 1 2 3 4 5 6 7 8 9 A B C D E F
0: 00 01 8D F6 CB 52 7B D1 E8 4F 29 C0 B0 E1 E5 C7
1: 74 B4 AA 4B 99 2B 60 5F 58 3F FD CC FF 40 EE B2
2: 3A 6E 5A F1 55 4D A8 C9 C1 0A 98 15 30 44 A2 C2
3: 2C 45 92 6C F3 39 66 42 F2 35 20 6F 77 BB 59 19
4: 1D FE 37 67 2D 31 F5 69 A7 64 AB 13 54 25 E9 09
5: ED 5C 05 CA 4C 24 87 BF 18 3E 22 F0 51 EC 61 17
6: 16 5E AF D3 49 A6 36 43 F4 47 91 DF 33 93 21 3B
7: 79 B7 97 85 10 B5 BA 3C B6 70 D0 06 A1 FA 81 82
8: 83 7E 7F 80 96 73 BE 56 9B 9E 95 D9 F7 02 B9 A4
9: DE 6A 32 6D D8 8A 84 72 2A 14 9F 88 F9 DC 89 9A
A: FB 7C 2E C3 8F B8 65 48 26 C8 12 4A CE E7 D2 62
B: 0C E0 1F EF 11 75 78 71 A5 8E 76 3D BD BC 86 57
C: 0B 28 2F A3 DA D4 E4 0F A9 27 53 04 1B FC AC E6
D: 7A 07 AE 63 C5 DB E2 EA 94 8B C4 D5 9D F8 90 6B
E: B1 0D D6 EB C6 0E CF AD 08 4E D7 E3 5D 50 1E B3
F: 5B 23 38 34 68 46 03 8C DD 9C 7D A0 CD 1A 41 1C
```
## # Tabla de transformación S
Con la tabla anterior, se puede construir la tabla de la transformación S ( valores en hexadecimal):
```
 0 1 2 3 4 5 6 7 8 9 A B C D E F
0: 63 7C 77 7B F2 6B 6F C5 30 01 67 2B FE D7 AB 76
1: CA 82 C9 7D FA 59 47 F0 AD D4 A2 AF 9C A4 72 C0
2: B7 FD 93 26 36 3F F7 CC 34 A5 E5 F1 71 D8 31 15
3: 04 C7 23 C3 18 96 05 9A 07 12 80 E2 EB 27 B2 75
4: 09 83 2C 1A 1B 6E 5A A0 52 3B D6 B3 29 E3 2F 84
5: 53 D1 00 ED 20 FC B1 5B 6A CB BE 39 4A 4C 58 CF
6: D0 EF AA FB 43 4D 33 85 45 F9 02 7F 50 3C 9F A8
7: 51 A3 40 8F 92 9D 38 F5 BC B6 DA 21 10 FF F3 D2
8: CD 0C 13 EC 5F 97 44 17 C4 A7 7E 3D 64 5D 19 73
9: 60 81 4F DC 22 2A 90 88 46 EE B8 14 DE 5E 0B DB
A: E0 32 3A 0A 49 06 24 5C C2 D3 AC 62 91 95 E4 79
B: E7 C8 37 6D 8D D5 4E A9 6C 56 F4 EA 65 7A AE 08
C: BA 78 25 2E 1C A6 B4 C6 E8 DD 74 1F 4B BD 8B 8A
D: 70 3E B5 66 48 03 F6 0E 61 35 57 B9 86 C1 1D 9E
E: E1 F8 98 11 69 D9 8E 94 9B 1E 87 E9 CE 55 28 DF
F: 8C A1 89 0D BF E6 42 68 41 99 2D 0F B0 54 BB 16
```
## # Transformación ShiftRows
Esta transformación desplaza cíclicamente las filas de la matriz de estado:
```
Entrada: Salida:
B₀ B₄ B₈ B₁₂ B₀ B₄ B₈ B₁₂ ( sin cambios)
B₁ B₅ B₉ B₁₃ ⇐ B₅ B₉ B₁₃ B₁ ( una celda a la izquierda)
B₂ B₆ B₁₀ B₁₄ ⇐ B₁₀ B₁₄ B₂ B₆ ( dos celdas a la izquierda)
B₃ B₇ B₁₁ B₁₅ ⇐ B₁₅ B₃ B₇ B₁₁ ( tres celdas a la izquierda)
```
Esta transformación tiene por misión lograr la difusión. También es resistente al criptoanálisis diferencial porque no difunde las diferencias.
## # Transformación MixColumns
Es una transformación lineal que mezcla entre sí las columnas de la matriz de estado. Cada columna de la matriz de estado se multiplica ( siguiendo la aritmética del GF ( 2⁸)) por una matriz constante. La finalidad es conseguir maximizar la difusión.
## # Operación MixColumns
En concreto la operación que se realiza es la siguiente:
```
[s'₀,ⱼ] [02 03 01 01] [s₀,ⱼ]
[s'₁,ⱼ] = [01 02 03 01] [s₁,ⱼ]
[s'₂,ⱼ] [01 01 02 03] [s₂,ⱼ]
[s'₃,ⱼ] [03 01 01 02] [s₃,ⱼ]
```
donde s_i,j y s'_i,j representan los elementos de la matriz de estado, y el índice j recorre las cuatro columnas.
Es importante recordar que toda la aritmética se realiza en GF ( 2⁸).
## # Transformación MixColumns inversa
La operación anterior se puede invertir usando la siguiente matriz:
```
[0E 0B 0D 09]
[09 0E 0B 0D]
[0D 09 0E 0B]
[0B 0D 09 0E]
```
donde s_i,j y s'_i,j representan, a igual que antes, los elementos de la matriz de estado, y el índice j recorre las cuatro columnas.
De nuevo, toda la aritmética se realiza en GF ( 2⁸).
## # Transformación AddRoundKey
Esta transformación es simplemente una operación de suma módulo 2 de la matriz de estado con una de las sub-claves. Cada sub-clave tiene 16 bytes ( a igual que la matriz de estado) y se deriva, de acuerdo a un cierto esquema, a partir de la clave principal.
## # Función de derivación de sub-claves
La clave en AES puede ser de 128, 192 o 256 bits. A partir de ella es necesario generar n_r + 1 sub-claves ( donde n_r es el número de vueltas), cada una de 128 bits.
En la descripción del algoritmo, usaremos como unidad palabras de 32 bits indexadas en un vector W.
## # Ecuaciones para la derivación de sub-claves
Suponemos que usamos el vector W con elementos de 32 bits. Para el caso de una clave de tamaño 128, necesitamos generar n_r + 1 = 11 sub-claves, cada una de 128 bits, que supondremos almacenadas secuencialmente en el vector W.
Por tanto, los elementos de las sub-claves, k₀ ... k₁₀, son:
```
k₀: W[0], W[1], W[2], W[3]
k₁: W[4], W[5], W[6], W[7]
k₁₀: W[40], W[41], W[42], W[43]
```
## # Esquema de derivación de sub-claves para 128 bits
```
W[0] W[1] W[2] W[3] ⇒ k₀
 ↓ g () ↓
W[4] W[5] W[6] W[7] ⇒ k₁
 ↓ g () ↓
W[8] W[9] W[10] W[11] ⇒ k₂
```
## # Ecuaciones para la derivación de sub-claves ( continuación)
La primera sub-clave, k₀, se inicializa con la propia clave, K. El resto de sub-claves se computan como:
```
W[4i] = W[4 ( i-1)] ⊕ g ( W[4i-1])
W[4i+j] = W[4 ( i-1)+j] ⊕ W[4i+j-1]
para i = {1, ..., 10} y j = {1, 2, 3}
```
## # Función g ( W) para la derivación de sub-claves
```
[b₀ b₁ b₂ b₃]
 ↓ ( rotar)
[b₁ b₂ b₃ b₀]
 ↓ ( SubBytes S)
[S S S S]
 ↓ (⊕ Rc[j])
W'
```
## # Función S y vector Rc
La función S que aparece en g es simplemente la transformación SubBytes que se presentó más arriba. El vector Rc está fijado y tiene estos valores:
```
n 1 2 3 4 5
Rc[n] 0x01 0x02 0x04 0x08 0x10
n 6 7 8 9 10
Rc[n] 0x20 0x40 0x80 0x1B 0x36
```
## # Derivación de sub-claves para 192 bits
Para 192 bits, AES usa 12 vueltas y por tanto necesita 13 sub-claves, la original y 12 más. En los pasos de generación de cada sub-clave, AES maneja seis palabras del vector W. Por tanto, con dos vueltas genera 3 sub-claves. Para generar 12 sub-claves, le bastan 8 vueltas de generación.
## # Derivación de sub-claves para 256 bits
Para 256 bits, AES usa 14 vueltas y por tanto necesita 15 sub-claves, la original y 14 más. Ahora, en los pasos de generación de cada sub-clave, AES maneja ocho palabras del vector W. Por tanto, genera dos sub-claves por vuelta. Para generar 14 sub-claves, le bastan 7 vueltas de generación.
## # Descifrado en AES
AES no utiliza una red de Feistel, que es involutiva, sino que se han de invertir todos los pasos. Pero la derivación de sub-claves no es un proceso invertible: se generan todas en sentido directo y se almacenan para ser usadas en sentido inverso.
**Comentario 13:** El descifrado es ligeramente más lento que el cifrado pues antes de comenzar a hacer nada se ha de generar la lista completa de sub-claves.
## # Esquema de descifrado en AES
```
Criptograma ( 128 bits) Clave de cifrado ( 128, 192, 256 bits)
 | |
 | Expansión de clave
 | |
 Ronda inicial: k_nr |
 - AddRoundKey | |
 - InvShiftRows |
 - InvSubBytes |
 - AddRoundKey |
 |
 Ronda normal: kⱼ |
 ( j = nr-1 ... 0) | |
 - InvMixColumns |
 - InvShiftRows |
 - InvSubBytes |
 - AddRoundKey |
 |
 v
Texto claro ( 128 bits)
```
## # Resumen de seguridad de AES
- No se conocen ataques analíticos hasta la fecha.
- Tampoco han triunfado los ataques diferenciales, o de clave relacionada.
- Interesante: desde 2008 las CPUs de Intel incorporan instrucciones AES, que ejecutan una vuelta del algoritmo si se le proporciona la sub-clave correspondiente.
## 5. Modos de operación
## # Modos de operación
Los cifradores de bloque se puede usar con seguridad para cifrar pequeñas cantidades de datos: esencialmente, hasta un bloque.
Para cifrar en volumen hay que recurrir a los llamados modos de operación.
En todo caso la información para cifrar ha de tener un número de bits múltiplo del tamaño de bloque. Si no es así, se debe completar hasta alcanzarlo ( véase Apéndice).
**Definición 14:** Un modo de operación es un algoritmo que, utilizando un cifrador de bloque como pieza básica, construye una suerte de cifrador en flujo, apto para cifrar datos en volumen.
## # Modos disponibles
- Libro electrónico de códigos ( ECB: Electronic Code Book)
- Encadenado de bloques cifrados ( CBC: Cipher Block Chaining)
- Realimentación de la salida ( OFB: Output Feedback)
- Realimentación del criptograma ( CFB: Cipher Feedback)
- Contador ( CTR: Counter Mode)
## # Modo ECB: Libro electrónico de códigos
Cada bloque cifrado depende del bloque en claro y de la clave. Cada bloque se cifra independientemente y se pueden cifrar bloques en paralelo. El descifrado se puede hacer en paralelo. No hace falta descifrar bloques anteriores para descifrar un bloque en particular.
Dos bloques de texto claro iguales producen dos bloques cifrados idénticos: no es CPA-seguro.
Dada una clave K, y bloques de texto claro, m₁, ..., m_n, los bloques cifrados, c₁, ..., c_n se obtienen:
```
c_i = E_K ( m_i), i = 1, ..., n
```
Para descifrar:
```
m_i = E_K⁻¹( c_i), i = 1, ..., n
```
## # Modo ECB: advertencia
¡ECB es inseguro!
## # Modo CBC: Encadenado de bloques cifrados
Cada bloque se suma con el bloque cifrado anterior antes de cifrarlo. Para cifrar el primer bloque, se usa un bloque inicio aleatorio ( distinto cada vez). Por tanto, cada bloque depende de todos los anteriores ( y del bloque inicio aleatorio). Por ello, bloques iguales no se cifran en iguales criptogramas.
Para descifrar un criptograma, basta conocer el criptograma anterior.
Dada una clave K, IV un bloque inicial aleatorio, y bloques de texto claro, m₁, ..., m_n, los bloques cifrados, c₁, ..., c_n se obtienen:
```
c₁ = E_K ( IV ⊕ m₁)
c_i = E_K ( c_{i-1} ⊕ m_i), i = 2, ..., n
```
Para descifrar:
```
m₁ = E_K⁻¹( c₁) ⊕ IV
m_i = E_K⁻¹( c_i) ⊕ c_{i-1}, i = 2, ..., n
```
## # Modo CBC: diagrama
```
Cifrado:
IV/Bloque Texto claro Texto claro Texto claro
inicial 1 2 n
 | | | |
 +-------+ +-------+ +-------+ |
 v v v v
 E_K E_K E_K
 | | |
 Criptograma Criptograma Criptograma
 1 2 n
Descifrado:
IV/Bloque Criptograma Criptograma Criptograma
inicial 1 2 n
 | | | |
 +--+ +----+ +----+ |
 v v v v
 E_K⁻¹ E_K⁻¹ E_K⁻¹
 | | |
 Texto Texto Texto
 claro 1 claro 2 claro n
```
## # Modo OFB: Realimentación de la salida
Se trata de construir un cifrador en flujo basándose en cifradores de bloque. Se genera una secuencia de bloques que constituyen la secuencia cifrante ( extrayendo un número de bits s de cada uno).
Cada conjunto de s bits de entrada se cifra sumándolos módulo 2 con la secuencia cifrante.
El descifrado es totalmente análogo al cifrado.
Las operaciones son esencialmente secuenciales y no paralelizables.
Dada una clave K, un bloque inicial aleatorio IV, y los bloques de texto claro, m₁, ..., m_n, de tamaño s ( tal que 1 ≤ s ≤ b, donde b es el tamaño en bits del bloque) los bloques cifrados, c₁, ..., c_n ( también de tamaño s bits), se obtienen:
```
O = E_K ( IV), c₁ = O_{( b-1...b-s)} ⊕ m₁
O_i = E_K ( O), c_i = O_{( b-1...b-s)} ⊕ m_i, i = 2, ..., n
```
Para descifrar:
```
O = E_K ( IV), m₁ = O_{( b-1...b-s)} ⊕ c₁
O_i = E_K ( O), m_i = O_{( b-1...b-s)} ⊕ c_i, i = 2, ..., n
```
## # Modo OFB: diagrama de cifrado y descifrado
Similar a CFB pero generando la secuencia cifrante de forma independiente del criptograma.
## # Modo CFB: Realimentación del criptograma
En CFB, de nuevo se trata de generar una réplica de un cifrador en flujo.
Se elige un valor s tal que 1 ≤ s ≤ b, donde b es el tamaño de bloque.
Cada bloque cifrado depende de los criptogramas anteriores, de la clave y del texto claro. Se ha de hacer en serie.
El descifrado se puede hacer en paralelo.
Dada una clave K, un bloque inicial aleatorio IV, y los bloques de texto claro, m₁, ..., m_n, de tamaño s los bloques cifrados, c₁, ..., c_n se obtienen:
```
I = IV, c₁ = E_K ( I)_{( b-1...b-s)} ⊕ m₁
I = I_{( b-1...b-s)} || c_{i-1}, c_i = E_K ( I)_{( b-1...b-s)} ⊕ m_i, i = 2, ..., n
```
Para descifrar:
```
I = IV, m₁ = E_K ( I)_{( b-1...b-s)} ⊕ c₁
I = I_{( b-1...b-s)} || c_{i-1}, m_i = E_K ( I)_{( b-1...b-s)} ⊕ c_i, i = 2, ..., n
```
## # Modo CTR: Contador
Se construye también en este caso una secuencia cifrante que se suma módulo 2 al texto claro.
La secuencia cifrante se construye cifrando un valor que se va incrementando ( mediante diversas funciones) para cada bloque.
Es inherentemente paralelizable tanto en cifrado como en descifrado, lo que aconseja su uso cuando son necesarias velocidades altas.
Dada una clave K, un bloque inicial aleatorio IV, y los bloques de texto claro, m₁, ..., m_n, los bloques cifrados, c₁, ..., c_n se obtienen:
```
CTR = IV, c₁ = E_K ( CTR) ⊕ m₁
CTR = f ( CTR), c_i = E_K ( CTR) ⊕ m_i, i = 2, ..., n
```
Para descifrar:
```
CTR = IV, m₁ = E_K ( CTR) ⊕ c₁
CTR = f ( CTR), m_i = E_K ( CTR) ⊕ c_i, i = 2, ..., n
```
La función f puede ser tan sencilla como incrementar el valor del contador de uno en uno ( módulo 2^b).
## # Comparación cifrado en flujo vs cifrado en bloque
**Ventajas del cifrado en flujo:**
- Operación muy rápida.
- Sencillez de diseño.
- Apropiado para pequeños dispositivos.
**Inconvenientes del cifrado en flujo:**
- Condiciones de seguridad menos conocidas.
- Vulnerados más frecuentemente.
- Diseños "ad-hoc" realizados por "gurús".
**Ventajas del cifrado en bloque:**
- Sistemas muy estudiados.
- Condiciones de seguridad muy bien conocidas.
- Posibilidad de paralelización con rendimientos muy altos.
**Inconvenientes del cifrado en bloque:**
- Sistemas más complejos que necesitan más recursos.
- Poco adecuados para dispositivos de bajas capacidades.
## # Apéndice: relleno ( padding)
En todos los sistemas de cifrado en bloque, se necesita que el número de bytes para cifrar sea un múltiplo del tamaño de bloque. En caso contrario, se completa con el número de bytes suficientes para alcanzar un múltiplo del tamaño de bloque.
El relleno se suele realizar de acuerdo a varias posibilidades: una de ellas es el estándar PKCS#5.
## # Apéndice: relleno PKCS#5
Este estándar exige que el último byte del último bloque indique el número de bytes de relleno. El relleno consiste en bytes que indican justamente el número de bytes de relleno.
**Comentario 15:** Si por casualidad, el número de bytes para cifrar es múltiplo del tamaño de bloque, se añade un bloque adicional de puro relleno, donde todos los bytes llevan el valor del tamaño del bloque.
## # Apéndice: ejemplo de relleno PKCS#5
**Ejemplo 16:** Supongamos un tamaño de bloque de 8 bytes. Si se han de cifrar 12 bytes, cuyo valor es, por ejemplo, F0 para todos, necesitamos que los 4 últimos bytes del último bloque sean de relleno. Los bloques quedarían así:
```
F0 F0 F0 F0 F0 F0 F0 F0 : F0 F0 F0 F0 04 04 04 04
```
## # Apéndice: ejemplo de relleno PKCS#5 ( caso especial)
**Ejemplo 17:** Supongamos de nuevo un tamaño de bloque de 8 bytes. Si hemos de cifrar justamente 8 bytes ( de valor F0), el último bloque es de puro relleno y todos los bytes llevan el valor del tamaño del bloque:
```
F0 F0 F0 F0 F0 F0 F0 F0 : 08 08 08 08 08 08 08 08
```
