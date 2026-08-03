---
title: "Protocolos De Comunicaciones Seguras"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---
	1*
En esta versión se utiliza el "I am Alice" para que bob sepa que clave pública usar

![[Excalidraw/01PrimerDiagrama-Alice-2024-11-21-125910.excalidraw]]


La T es un timestamp sirve para evitar ataque de repetición

Las preguntas son las siguientes:


A. Alice sabe que Bob es Bob. 
B. Bob sabe que Alice es Alice.
C. Trudy no puede hacer un ataque de replay. 
D. Hay una clave de sesión segura. E. Ninguna es cierta

A. Lo sabe debido a que es capaz de desencriptar el primer mensaje con su clave privada.
B. No, porque sin la marca de tiempo Trudy puede haber reenviado el mensaje de Alice entero. “Alice” nunca desencripta el mensaje encriptado con su clave pública, por lo que no hay demostración de que sea ella.
C. Sí, porque sin las marcas del tiempo no hay ninguna comprobación de que la solicitud de Alice no haya sido la misma de otra ocasión.
D. La comunicación se ve comprometida por el ataque de replay.


### Pregunta Supuesto 1.1

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

**Si se repitiesen los números aleatorios, ¿qué número debería adivinar Trudy para suplantar a Bob? ¿Y a Alice?**

#### Solución Supuesto 1.1
- Para suplantar a **Bob** le hace falta **Ra**.
- Para suplantar a **Alice** le hace falta **Rb**.

### Pregunta Supuesto 1.2
**¿Cómo de grandes deben ser los números para que no se repitan?**

#### Solución Supuesto 1.2
Esto se contesta utilizando el **problema del cumpleaños**.
### Ejercicio 2

#### **PREGUNTA EJERCICIO 2**

T es una marca de tiempo. Los relojes de los ordenadores Alice y Bob están sincronizados.  
Alice y Bob están estableciendo una clave simétrica K. Esto se hace porque, aunque la clave asimétrica es más segura, la simétrica es más rápida. Por lo tanto, la comunicación se establece con una asimétrica y se continúa con la simétrica.
![[Excalidraw/02.0segundoDiagramaAlice]]
- A. Alice sabe que Bob es Bob.
- B. Bob sabe que Alice es Alice.
- C. Trudy no puede hacer un ataque de replay.
- D. Hay una clave de sesión segura.
- E. Ninguna es cierta.

#### **SOLUCIÓN EJERCICIO 2**

- **A.** Es cierto porque Alice firma con su clave privada que solo ella posee y nadie más.
- **B.** Es cierto por lo mismo: Bob firma con su clave personal.
- **C.** En principio no podría porque las marcas de tiempo cumplen la misma función que los números aleatorios RaR_a y RbR_b en el anterior ejercicio. Pero hay una ligera excepción.
- **D.** Sí, porque los mensajes encriptados con las claves públicas solo los puede desencriptar el dueño de la privada correspondiente.

---

#### **PREGUNTA SUPUESTO 2.1**

Se cambia el escenario de manera que ya no usan las marcas de tiempo.

- A. Alice sabe que Bob es Bob.
- B. Bob sabe que Alice es Alice.
- C. Trudy no puede hacer un ataque de replay.
- D. Hay una clave de sesión segura.
- E. Ninguna es cierta.
![[Excalidraw/021Alice2024-11-21-233615.excalidraw]]
#### **SOLUCIÓN SUPUESTO 2.1**

- **A.** Lo sabe debido a que es capaz de desencriptar el primer mensaje con su clave privada.
- **B.** No, porque sin la marca de tiempo, Trudy puede haber reenviado el mensaje de Alice entero. “Alice” nunca desencripta el mensaje encriptado con su clave pública, por lo que no hay demostración de que sea ella.
- **C.** Sí, porque sin las marcas del tiempo no hay ninguna comprobación de que la solicitud de Alice no haya sido la misma de otra ocasión.
- **D.** La comunicación se ve comprometida por el ataque de replay.

---

#### **PREGUNTA SUPUESTO 2.2**

¿Qué manera tiene Trudy de hacer un ataque de replay y comprometer la clave al mismo tiempo?

![[Excalidraw/022segundo-ataque-trudy-2024-11-21-170607.excalidraw]]
#### **SOLUCIÓN SUPUESTO 2.2**

Suponiendo que Bob es un servidor cualquiera, le da igual contestar a Alice que a Trudy; para él, ellas dos son clientes cualesquiera.

1. Alice manda su mensaje como sigue.
2. Trudy intercepta el mensaje y lo manda al mismo instante TT que Alice.
    - Esto lo hace desencriptándolo con la clave pública de Alice y firmándolo como si fuese suyo.
3. Bob lo desencriptará como si fuese un mensaje legítimo de otro cliente que quiere acceder a su servidor.
![[Excalidraw/023segundo-32024-11-21-171010.excalidraw]]
![[Excalidraw/024-Ataque-trudy-2024-11-21-171435.excalidraw]]
**Impacto:**  
Tras Alice establecer su clave simétrica con Bob, las conversaciones con Trudy tendrán la misma clave KK.

**Solución:**  
Para evitar este caso, Bob no debe devolver la clave KK de manera que Trudy pueda descubrirla.

---

### Ejercicio 3

#### **PREGUNTA EJERCICIO 3**

¿Qué se almacena en un certificado?

#### **SOLUCIÓN EJERCICIO 3**

En un certificado se almacena:

- La clave pública del sujeto certificado.
- Sus datos, ambos firmados por la CA.

Ejemplo:  
“Bob”,Kb+“Bob”, K^+_b_{ca}  
**Nota:** No se almacena nada privado.

---

#### **PREGUNTA SUPUESTO 3.1**

¿Qué pasaría si los datos del certificado no estuviesen firmados y solo su clave pública? Es decir, “Bob”, Kb+K^+_b_{ca}.

#### **SOLUCIÓN SUPUESTO 3.1**

Trudy podría modificar la entrada y poner sus datos en vez de los de Bob.

---

### Ejercicio 4

#### **PREGUNTA EJERCICIO 4**
![[Excalidraw/041Drawing-2024-11-21-171659.excalidraw]]
Tenemos a un cliente, Alice, estableciendo una clave de sesión con el servidor, Bob.

- Ra,RbR_a, R_b y SS: números aleatorios lo suficientemente grandes para que sean seguros.
- CLNTCLNT y SRVRSRVR: constantes públicas.
- K=h(Ra,Rb,S)K = h(R_a, R_b, S).

Opciones:

- A. Alice sabe que Bob es Bob.
- B. Bob sabe que Alice es Alice.
- C. Trudy no puede hacer un ataque de replay.
- D. Hay una clave de sesión segura.
- E. Ninguna es cierta.

#### **SOLUCIÓN EJERCICIO 4**

- **A.** Sí, porque el certificado da credibilidad a la clave pública Kb+K^+_b. Alice usa dicha clave y Bob es capaz de descifrar {S}_b, lo que significa que es el dueño de la clave privada correspondiente.
- **B.** No, porque nada de Alice es privado ni indica que sea ella.
- **C.** Sí, los números aleatorios lo impiden.
- **D.** Sí, gracias a la frescura y aleatoriedad que proporcionan Ra,RbR_a, R_b y SS a KK. Además, existe un control mutuo sobre la clave: ambos extremos influyen en su creación.

---

#### **PREGUNTA SUPUESTO 4.1**

¿Cómo se autentica Alice entonces?

#### **SOLUCIÓN SUPUESTO 4.1**

Alice se autentica tras entrar en la web del servidor Bob. Gracias a la clave de sesión segura, Alice puede:

- Rellenar y enviar un formulario con su usuario y contraseña de manera confidencial.

Aunque este método es más arcaico e inseguro, es preferido por:

- Su eficiencia y rapidez.
- La falta de necesidad de certificar oficialmente a Alice.

---

#### **PREGUNTA SUPUESTO 4.2**

¿Qué pasa si Alice envía en el tercer mensaje {S}_b, E(SRVR, K) en vez de {S}_b, E(CLNT, K)?

#### **SOLUCIÓN SUPUESTO 4.2**

Bob dejaría de estar autenticado, ya que el reto que debe resolver para autenticarse, encriptar la constante SRVRSRVR, sería resuelto.