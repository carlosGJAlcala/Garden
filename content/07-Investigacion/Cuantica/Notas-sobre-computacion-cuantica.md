---
title: "Puertas cuánticas"
date: 2026-01-26
tags:
  - investigacion
  - cuantica
---



Los **computadores cuánticos** no utilizan transistores convencionales como los ordenadores clásicos. En lugar de usar transistores, los ordenadores cuánticos emplean **qubits** (bits cuánticos), que pueden representar tanto el estado 0 como el estado 1 al mismo tiempo, gracias al principio de la **superposición cuántica**. Esto les permite procesar una gran cantidad de información de manera simultánea, lo que, en teoría, les da una ventaja significativa sobre los ordenadores tradicionales en ciertas tareas.

### Teoría de la Computación Cuántica


> **Relacionado**: [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

David Deutsch, uno de los pioneros en la computación cuántica, formuló una **teoría formal** sobre cómo se podrían construir computadores cuánticos. Su trabajo fue fundamental para sentar las bases de lo que hoy entendemos como la **computación cuántica universal**, que, al igual que los ordenadores clásicos, puede realizar cualquier tipo de cálculo, pero aprovechando las propiedades cuánticas como la superposición y el entrelazamiento.

### Criptografía Híbrida

En el campo de la **criptografía**, la **criptografía híbrida** se refiere a un enfoque que combina la criptografía clásica con la cuántica. Con la computación cuántica, los algoritmos criptográficos tradicionales pueden volverse inseguros debido a la capacidad de los ordenadores cuánticos para resolver ciertos problemas de manera exponencialmente más rápida que los ordenadores clásicos. La criptografía cuántica, por ejemplo, mediante el uso de **llaves cuánticas**, promete ofrecer una forma de comunicación segura que podría ser resistente incluso ante los ataques de ordenadores cuánticos.

### La Teoría de la Información Cuántica de Schumacher

Una de las figuras clave en la **información cuántica** es **Benjamin Schumacher**, quien desarrolló una teoría formal sobre la **codificación cuántica**. Schumacher demostró que es posible representar y transmitir información cuántica de manera eficiente utilizando sistemas cuánticos. Su trabajo mostró que la cantidad de información que puede ser contenida en un sistema cuántico no está limitada por las mismas restricciones que la información clásica, lo que permite nuevos avances en áreas como la computación cuántica y la criptografía cuántica.

### El Entrelazamiento Cuántico

Uno de los conceptos más fascinantes de la computación cuántica es el **entrelazamiento cuántico**. Este fenómeno ocurre cuando dos o más partículas cuánticas (como qubits) se encuentran en un estado en el que el estado de una de ellas está directamente relacionado con el estado de las otras, sin importar la distancia entre ellas.

El entrelazamiento cuántico permite realizar **operaciones en paralelo**. Gracias al principio de superposición, un qubit puede estar en un estado de 0 y 1 simultáneamente. Sin embargo, por sí sola, esta propiedad no sería suficiente para obtener ventajas significativas sobre los ordenadores clásicos, ya que los bits cuánticos se comportarían solo como "bits difusos". Es aquí donde el entrelazamiento cuántico se convierte en una herramienta esencial: al entrelazar qubits, se pueden realizar operaciones que aprovechan las correlaciones entre ellos, lo que permite la paralelización de los cálculos y una mejora significativa en la eficiencia de los algoritmos cuánticos.

### Superando a los Ordenadores Tradicionales

Una de las demostraciones más emblemáticas del poder de la computación cuántica fue realizada mediante un **problema de caja negra**, en el cual un ordenador cuántico debe determinar si una función es **balanceada** o **constante**. Un ordenador clásico necesita realizar dos operaciones, una con un valor de 1 y otra con 0, para determinar de qué tipo es la función. En cambio, un ordenador cuántico puede resolver este problema con solo **un qubit**, ya que puede estar en una superposición de ambos estados (0 y 1), y al realizar una sola medición puede obtener ambas respuestas al mismo tiempo, lo que le permite determinar el tipo de función de manera mucho más rápida.

Este tipo de tareas, donde un ordenador cuántico puede superar a uno clásico, es solo una de las muchas áreas en las que la computación cuántica promete tener un impacto significativo, especialmente en problemas de optimización, simulación y criptografía.

---

### El Algoritmo de Shor para la Factorización Cuántica

La computación cuántica comenzó a mostrar su potencial real cuando **Peter Shor** propuso un **algoritmo cuántico** para la **factorización de números** grandes. Este algoritmo es famoso porque, en teoría, puede factorizar números en tiempo polinómico, lo cual es significativamente más rápido que los mejores algoritmos clásicos conocidos. La importancia de este algoritmo radica en que la factorización de números grandes es la base de la seguridad de muchos sistemas criptográficos clásicos, como el algoritmo RSA. En criptografía, la dificultad de factorizar grandes números compuestos es un problema que se asume computacionalmente intratable, pero el algoritmo de Shor puede romper esta suposición al hacerlo mucho más eficiente.

Shor utilizó una técnica cuántica denominada **reducción** para transformar el problema de la factorización en un problema más sencillo. Específicamente, la reducción implica encontrar patrones en los **residuos** de divisiones sucesivas. En la parte clásica del algoritmo, se realiza una división de manera tradicional, pero la parte cuántica juega un papel crucial al utilizar las propiedades cuánticas de **superposición** y **entrelazamiento cuántico**. Estos efectos cuánticos permiten la paralelización de los cálculos y la identificación de patrones que, en el caso de los algoritmos clásicos, tomarían mucho más tiempo en encontrar.

El algoritmo de Shor es uno de los ejemplos más claros de cómo la computación cuántica puede ofrecer una ventaja significativa en áreas que antes eran intratables para las computadoras clásicas, especialmente en el campo de la **criptografía**.

### El Primer Ordenador Cuántico: MIT y Resonancia Magnética Nuclear

El **primer ordenador cuántico** operativo fue desarrollado en 1998 por un equipo de investigadores del **MIT (Massachusetts Institute of Technology)** y científicos de la Universidad de Oxford. Este dispositivo utilizaba **resonancia magnética nuclear (RMN)** para manipular **moléculas líquidas**, lo que representaba un sistema cuántico en el que se podía controlar el estado cuántico de átomos dentro de las moléculas.

En este experimento, los investigadores se centraron en **el espín de los núcleos atómicos**. El espín es una propiedad cuántica fundamental que describe el momento angular intrínseco de una partícula subatómica, como un electrón o un núcleo atómico. En términos simples, el espín puede ser visualizado como una especie de "imán cuántico" que tiene dos posibles orientaciones: una hacia arriba (representada por 1) y otra hacia abajo (representada por 0).

Para manipular el espín, se utiliza un **campo electromagnético** extremadamente fuerte. Además, se aplican **pulsos de ondas calibrados** con una frecuencia y duración específicas para alterar la dirección del espín, de manera similar a cómo una brújula cambia su orientación al aplicar un campo magnético. Este proceso es crucial para manipular los estados cuánticos, permitiendo que los investigadores puedan controlar el espín de los núcleos atómicos y, por ende, los estados cuánticos de las moléculas.

Una vez que los pulsos electromagnéticos han manipulado los espines, los núcleos emiten señales débiles que pueden ser medidas. Esto se realiza utilizando una técnica llamada **eco cuántico**, que permite detectar el estado de los qubits (en este caso, los núcleos atómicos) y determinar si están en el estado 0 o 1. El eco cuántico es un método que ayuda a recuperar la información cuántica que se ha perdido debido a la interacción con el entorno, un problema común en la computación cuántica debido a la **decoherencia cuántica**.

Este avance representó un hito en la historia de la computación cuántica, demostrando que era posible manipular estados cuánticos de forma controlada, lo que abrió el camino para el desarrollo de ordenadores cuánticos más sofisticados en el futuro.

### Avances en la Computación Cuántica

**2001: IBM y la Factorización del Número 15**  
En 2001, **IBM** consiguió un hito importante en la computación cuántica al factorizar el número 15 utilizando una máquina cuántica de **7 qubits**. Este logro se alcanzó con la técnica de **resonancia magnética nuclear (RMN)**, que permitía manipular átomos en un estado cuántico controlado. Aunque este avance no marcó el inicio de la computación cuántica universal, sí representó una primera muestra de que era posible realizar cálculos cuánticos en un sistema relativamente simple.

**D-Wave: Primera Computadora Cuántica Comercial (2011)**  
En 2011, **D-Wave** lanzó la **primera computadora cuántica comercial**. Esta máquina se especializaba en resolver problemas de **optimización** cuántica, utilizando qubits superconductores. Sin embargo, a pesar de su capacidad para resolver ciertos tipos de problemas, no era una **computadora cuántica universal**. En lugar de ser un sistema general, estaba diseñada para abordar casos muy específicos, como encontrar la mejor solución en espacios de soluciones complejos. Este enfoque se centraba en optimizar ciertas tareas, pero no abarcaba todo el espectro de la computación cuántica.

**IBM Quantum Experience y Qiskit SDK**  
El desarrollo de la computación cuántica no se detuvo ahí. **IBM** presentó el **IBM Quantum Experience**, una plataforma basada en la nube que permitía a los usuarios acceder a computadoras cuánticas y experimentar con algoritmos cuánticos. Esta plataforma fue acompañada por **Qiskit**, un kit de herramientas de **código abierto** desarrollado por IBM. Qiskit está basado en **Python** y permite programar computadoras cuánticas desde cero. Gracias a esta plataforma, los desarrolladores pueden crear y ejecutar algoritmos cuánticos de manera accesible y experimentar con diversos tipos de qubits, todo a través de la nube.

**Sycamore y la Supremacía Cuántica de Google (2019)**  
En 2019, **Google** logró un hito que se conoció como **supremacía cuántica** con su procesador cuántico **Sycamore**. Este chip cuántico, compuesto por **53 qubits superconductores**, logró realizar una tarea en un tiempo significativamente más rápido que el que tomaría a un supercomputador clásico. El problema resuelto fue la generación y verificación de una secuencia de números aleatorios, un proceso que Sycamore completó en solo 200 segundos. En comparación, un supercomputador clásico habría tardado **más de 10.000 años** en realizar esta tarea. Aunque IBM refutó algunas de las estimaciones de Google, sugiriendo que podría tomar "solo" unos pocos días en lugar de milenios, este evento marcó un paso importante en la demostración de la potencia de la computación cuántica.

**Qubits Superconductores y sus Propiedades**  
El uso de **materiales superconductores** es fundamental en muchos ordenadores cuánticos, como los utilizados en Sycamore. Estos materiales tienen la capacidad única de transmitir electricidad sin resistencia, lo que permite construir circuitos cuánticos donde las corrientes pueden fluir en **dos direcciones simultáneamente**. Este fenómeno se aprovecha para representar qubits, que pueden estar en una superposición de 0 y 1 a la vez. Esta propiedad es la base de la computación cuántica, donde se pueden realizar cálculos mucho más rápidamente que en los sistemas clásicos.

**Meta a Largo Plazo: 1000 Qubits**  
Una de las metas más ambiciosas de la computación cuántica es alcanzar **1000 qubits**. Esto permitiría resolver problemas aún más complejos que no son factibles para los ordenadores cuánticos actuales, abriendo la puerta a nuevas aplicaciones en áreas como la simulación de materiales, la criptografía cuántica, y la optimización de procesos en diversos campos. Aunque todavía estamos lejos de lograr esta meta, los avances en la corrección de errores cuánticos y en la estabilidad de los qubits continúan, lo que hace que este objetivo sea cada vez más alcanzable.


### Aplicaciones de la Computación Cuántica

Los **computadores cuánticos** están siendo utilizados en una variedad de sectores para resolver problemas complejos que no pueden ser tratados eficazmente por las computadoras tradicionales. Algunas de las aplicaciones más prometedoras incluyen:

1. **Prueba de Nuevos Algoritmos**: Los algoritmos cuánticos, como el famoso **algoritmo de Shor**, que puede factorizar números grandes de manera exponencialmente más rápida que los algoritmos clásicos, tienen el potencial de revolucionar áreas como la **criptografía**. Con el avance de la computación cuántica, se están probando y desarrollando nuevos algoritmos para una variedad de problemas complejos, lo que podría cambiar la forma en que abordamos la computación y la seguridad digital.
    
2. **Farmacéutica y Desarrollo de Nuevas Moléculas**: En el campo de la **farmacia**, la computación cuántica puede utilizarse para **simular el comportamiento de moléculas** y materiales a nivel cuántico. Esto permite acelerar el descubrimiento de nuevos fármacos, diseñando medicamentos más efectivos y seguros en menos tiempo. **ScienceDirect** y otros centros de investigación están trabajando con simulaciones cuánticas para analizar reacciones químicas complejas que serían imposibles de modelar con computadoras tradicionales.
    
3. **Simulación de Materiales y Reacciones Químicas Complejas**: Los centros de investigación utilizan ordenadores cuánticos para simular materiales con propiedades específicas, como superconductores o materiales para baterías más eficientes. Estas simulaciones son esenciales para la **investigación de nuevos materiales** que podrían revolucionar industrias como la energética, la electrónica, y la manufactura avanzada.
    
4. **Inteligencia Artificial y Optimización**: En el campo de la **inteligencia artificial (IA)**, la computación cuántica tiene el potencial de mejorar significativamente los algoritmos de aprendizaje automático y optimización. Los ordenadores cuánticos pueden resolver problemas complejos de optimización, como la **optimización de rutas en logística**, la **predicción del clima** y la **optimización de portafolios de inversión**, todo esto en cuestión de segundos, en lugar de horas o días como se haría con computadoras tradicionales.
    

### Plataformas para Operar Computadoras Cuánticas

Varios proveedores están ofreciendo acceso a **computadoras cuánticas** a través de la **nube**, lo que permite a los investigadores y desarrolladores operar y programar estos sistemas sin necesidad de tener acceso físico a los mismos. Algunas de las principales plataformas incluyen:

- **Cirq de Google**: Esta es una biblioteca de código abierto diseñada específicamente para interactuar con los procesadores cuánticos de Google, como **Sycamore**. Cirq permite crear, simular y ejecutar algoritmos cuánticos en hardware cuántico real.
    
- **Qiskit de IBM**: Qiskit es el kit de herramientas de código abierto basado en **Python** desarrollado por IBM, que permite a los usuarios diseñar, simular y ejecutar algoritmos cuánticos en computadoras cuánticas reales a través de la nube. Con Qiskit, los desarrolladores pueden crear sus propios programas cuánticos y probarlos en hardware cuántico.
    
- **Forest de Rigetti**: Similar a Qiskit, **Forest** es una plataforma desarrollada por **Rigetti Computing** para operar con ordenadores cuánticos, permitiendo a los usuarios programar y ejecutar algoritmos cuánticos a través de la nube.
    

### Desafíos Actuales: Corrección de Errores Cuánticos

Uno de los mayores retos actuales en la computación cuántica es la **corrección de errores cuánticos**. Los qubits, debido a su naturaleza extremadamente sensible, son propensos a errores causados por la **decoherencia cuántica** y otras perturbaciones. Actualmente, los investigadores están trabajando en técnicas avanzadas de corrección de errores para garantizar que los cálculos cuánticos sean precisos y fiables.

Se espera que, en los próximos 10 a 20 años, veamos avances significativos en la **corrección de errores cuánticos**, lo que permitirá a la computación cuántica ser más estable y eficiente en aplicaciones reales.

### Modelos Híbridos: Combinación de Computación Cuántica y Clásica

A medida que los ordenadores cuánticos se siguen desarrollando, es probable que veamos una combinación de **computación cuántica y clásica** en lo que se denomina **modelos híbridos**. En este enfoque, algunas partes del cálculo se delegan a un **ordenador cuántico**, aprovechando las ventajas de la computación cuántica para resolver problemas complejos, mientras que otras tareas menos intensivas se realizan con ordenadores clásicos. Este enfoque permitirá aprovechar lo mejor de ambos mundos, sin tener que esperar a que los ordenadores cuánticos sean completamente desarrollados para todos los tipos de problemas.

computación cuántica uno de los pilares es la interferencia
La computación cuántica se basa en lógica booleana mientras que la computación cuántica se fundamenta en el algebra lineal.

# Puertas cuánticas

![[Pasted image 20250513132649.png]]
### **H – Hadamard**

- **Símbolo**: H
    
- **Función**: Crea superposición.
    
- **Ejemplo**: Convierte `|0⟩` en `(|0⟩ + |1⟩)/√2`, y `|1⟩` en `(|0⟩ - |1⟩)/√2`.
    
- **Uso común**: Punto de partida para entrelazamiento y algoritmos cuánticos.
    

---
### **HC**

Una puerta compuesta que aplica primero una Hadamard (H) y luego una CNOT controlada
Es decir, **es un atajo visual para crear estados entrelazados**, típicamente un estado de **Bell** cuando partes de qubits en ∣0⟩|0⟩∣0⟩.
→ Esto crea **entrelazamiento perfecto** entre dos qubits.

---
### **X – Pauli-X (NOT cuántico)**

- **Símbolo**: X
    
- **Función**: Cambia `|0⟩` ↔ `|1⟩`.
    
- **Es como**: Una puerta NOT clásica.
    

---

###  **Z – Pauli-Z**

- **Símbolo**: Z
    
- **Función**: Cambia el signo del estado `|1⟩`.
    
    - `|0⟩ → |0⟩`
        
    - `|1⟩ → -|1⟩`
        
- **Uso**: Manipula la **fase cuántica**, esencial para algoritmos como Grover o Fourier cuántico.
    

---

### **Y – Pauli-Y**

- **Símbolo**: Y
    
- **Función**: Combinación de X y Z, con cambio de signo complejo.
    
- **Transforma**:
    
    - `|0⟩ → i|1⟩`
        
    - `|1⟩ → -i|0⟩`
        
- **Uso**: Menos intuitiva, pero útil para rotaciones complejas.
    

---

### **S – Fase**

- **Símbolo**: S
    
- **Función**: Añade una fase de `i` al estado `|1⟩`.
    
    - `|0⟩ → |0⟩`
        
    - `|1⟩ → i|1⟩`
        
- **Uso**: Alinea fases; usada con Z, H y T.
    

---

###  **CTRL – Puerta controlada**

- **Símbolo**: CTRL
    
- **Función**: Controla otra puerta (por ejemplo, una **CNOT**, cuando se usa con `X`).
    
- **Uso**:
    
    - Si el qubit de control es `|1⟩`, la puerta se activa en el objetivo.
        
    - Muy usada para crear **entrelazamiento** (como en las puertas CNOT o Toffoli


** dos puertas S  equivalen a  una puerta z , dos puertas seguidas es como multiplicar  ambas señales, teoria de señales un sistema que pasa por otro se multiplica

** el orden no es comutativo en la computación cuantica no en todas la operzaciones la x es comutativa y la dos puertas idéntivas si so ncomutativas , porque toda puerta sigue la ecuación de Schrödinger que debe ser reversible  y son pulso
Cuando tienes más de tre qubit los cambios de fase afectan al sistema global de forma compleja 
** la logica booleana la haces con puertas de control cnot y ccnot donde dos qubits control interactuan con uno objetivo

Muy buena pregunta. Parece contradictorio a primera vista: **¿cómo puede ser reversible una ecuación que describe evolución en el tiempo?**

La clave está en **cómo** depende del tiempo y **qué tipo de ecuación** es. Vamos paso a paso:

---

##  1. La ecuación de Schrödinger es **determinista y unitaria**

La forma general de la ecuación es:

iℏddt∣ψ(t)⟩=H^∣ψ(t)⟩i\hbar \frac{d}{dt} |\psi(t)⟩ = \hat{H} |\psi(t)⟩

Esto se parece a una ecuación diferencial ordinaria. Y como tal, **tiene solución única** si conoces el estado inicial ∣ψ(0)⟩|\psi(0)⟩. Es decir:

> Si conoces el estado en un momento t0t_0, puedes predecir con exactitud el estado en cualquier otro instante tt, **hacia adelante o hacia atrás en el tiempo**.

---

##  2. ¿Qué significa que sea reversible?

Significa que **puedes invertir el proceso**: si sabes el estado en el tiempo tt, puedes calcular perfectamente cuál era el estado en t0t_0.  
Esto es porque la evolución está gobernada por una **operación unitaria**:

∣ψ(t)⟩=U(t)∣ψ(0)⟩conU(t)=e−iH^t/ℏ|\psi(t)⟩ = U(t)|\psi(0)⟩ \quad \text{con} \quad U(t) = e^{-i\hat{H}t/\hbar}

Y **toda matriz unitaria** UU tiene una inversa U†U^\dagger, que te permite ir hacia atrás:

∣ψ(0)⟩=U†(t)∣ψ(t)⟩|\psi(0)⟩ = U^\dagger(t)|\psi(t)⟩

---

## ️ 3. ¿Qué papel juega el tiempo?

El tiempo no rompe la reversibilidad si el **Hamiltoniano** (la energía del sistema) **no cambia con el tiempo**. Es decir, si:

H^(t)=constante\hat{H}(t) = \text{constante}

Entonces la evolución cuántica es **tiempo-reversible**.  
Si el Hamiltoniano **sí cambia con el tiempo**, entonces sigue siendo reversible **matemáticamente**, pero la solución es más compleja (se necesita una evolución temporal ordenada, por ejemplo usando operadores de tiempo).

---

##  Contraste: la medición NO es reversible

Lo único **irreversible** en mecánica cuántica es la **medición**, porque colapsa el estado cuántico a un resultado clásico y **destruye información**.

---

##  En resumen

- La ecuación de Schrödinger es reversible porque su evolución es **unitaria** (no pierde información).
    
- Depender del tiempo **no impide la reversibilidad** si el sistema está bien definido.
    
- Lo que **sí rompe** la reversibilidad es **medir** el sistema.
    

---
***  todo sistema  determista en la ecuación schrödinger  pero al medirlo por el colapso de la función de onda es probabilistico
** los sistemas hibridos en el cual se combina POO con computación cuántico para hacer simulacion, es un enfoque muy ventajosos


En el algoritmo de grover 
- Pones todos los estados en **superposición** (todos tienen la misma amplitud).
    
- El **oráculo cambia la fase del estado correcto**:  
    ∣x⟩→−∣x⟩|x⟩ \rightarrow -|x⟩∣x⟩→−∣x⟩
    
- Luego aplicas el **difusor** (inversión sobre la media).
    
- Como ese estado tiene fase negativa, el difusor lo **refuerza** y le da **más amplitud**.
    
- Al final, **la probabilidad de medir ese estado aumenta mucho**.