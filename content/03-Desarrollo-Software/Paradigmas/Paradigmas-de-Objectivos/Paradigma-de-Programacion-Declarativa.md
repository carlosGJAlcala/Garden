---
title: "Paradigma De Programacion Declarativa"
date: 2026-01-26
tags:
  - desarrollo-software
  - paradigmas
  - paradigmas-de-objectivos
---
### **Paradigma de Programación Declarativa**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]].

La **programación declarativa** es un paradigma de programación en el que el programador **especifica qué** desea lograr, sin detallar cómo se debe realizar esa tarea. A diferencia de los paradigmas imperativos, donde se define paso a paso el flujo de control para lograr un resultado, en la programación declarativa se define más el **resultado deseado** que el proceso para llegar a él.

Este estilo de programación se basa en **expresiones** o **declaraciones** que describen lo que el programa debe hacer, sin definir de manera explícita cómo hacerlo. La responsabilidad de decidir cómo obtener el resultado recae en el **sistema** o **motor de ejecución**, que interpreta las instrucciones y las lleva a cabo de la manera más eficiente.

#### **Características del Paradigma Declarativo**

1. **Abstracción del "cómo"**:
    
    - En la programación declarativa, el **"cómo"** se hace la tarea no es especificado. El programador solo se preocupa por definir **qué** debe ocurrir. La implementación interna de las acciones está gestionada por el entorno de ejecución o el lenguaje.
        
2. **Lenguajes de Alto Nivel**:
    
    - Los lenguajes declarativos permiten trabajar a un **nivel de abstracción alto**, lo que simplifica la escritura y comprensión del código. No es necesario conocer los detalles internos de cómo se gestionan los recursos del sistema.
        
3. **Foco en el resultado**:
    
    - El objetivo de un programa declarativo es **lograr un resultado**, no describir las instrucciones paso a paso para llegar a ese resultado. El **estado final** es más importante que las operaciones individuales realizadas para alcanzarlo.
        
4. **Automatización de la ejecución**:
    
    - Los lenguajes declarativos delegan en el sistema la **decisión de los pasos de ejecución**, optimizando el rendimiento y liberando al programador de tareas tediosas como la gestión de recursos y la optimización del código.
        
5. **Estilo Funcional o Lógico**:
    
    - Muchos lenguajes declarativos siguen los estilos **funcionales** o **lógicos**. En el paradigma funcional, las funciones son tratadas como ciudadanos de primera clase, y en el lógico, se usan hechos y reglas para expresar relaciones entre objetos.
        

#### **Tipos de Programación Declarativa**

1. **Programación Funcional**:
    
    - En este estilo, los programas se componen de **funciones puras** que transforman datos de entrada en salida sin causar efectos secundarios. Es un subconjunto de la programación declarativa que se enfoca en la evaluación de expresiones matemáticas y la manipulación de funciones.
        
    - **Características**:
        
        - Uso de funciones **puras**, sin efectos secundarios.
            
        - **Inmutabilidad** de los datos, lo que asegura que no haya cambios de estado inesperados.
            
        - Uso intensivo de **recursión** y de operaciones como **map**, **filter** y **reduce**.
            
    - **Ejemplo**: **Haskell**, **Lisp**, **Scala**.
        
2. **Programación Lógica**:
    
    - En la programación lógica, el enfoque está en la **descripción de hechos y relaciones**. En lugar de definir un conjunto de pasos para resolver un problema, se declaran **hechos** (información sobre el dominio del problema) y **reglas** (relaciones entre hechos), y el sistema intenta **razonar** y encontrar soluciones.
        
    - **Características**:
        
        - Se usan **hechos** y **reglas** para expresar relaciones.
            
        - El sistema intenta encontrar las soluciones **mediante inferencia lógica**.
            
        - La consulta se hace declarando la propiedad que debe ser verdadera, no los pasos a seguir.
            
    - **Ejemplo**: **Prolog**.
        
3. **Lenguajes de Consulta y Especificación**:
    
    - Los lenguajes de consulta declarativa, como **SQL** (Structured Query Language), permiten al programador **especificar** qué datos se desean obtener de una base de datos, sin detallar cómo se deben buscar. El motor de la base de datos se encarga de optimizar y ejecutar las consultas.
        
    - **Características**:
        
        - **Consultas declarativas** donde solo se especifica lo que se necesita.
            
        - El sistema se encarga de encontrar la **mejor estrategia** para recuperar la información.
            
    - **Ejemplo**: **SQL**, **XPath**.
        

#### **Ventajas de la Programación Declarativa**

1. **Mayor abstracción y simplicidad**:
    
    - El programador se enfoca en **qué** desea lograr, no en los detalles de **cómo** lograrlo, lo que lleva a una mayor simplicidad en el código y menor complejidad en el proceso de desarrollo.
        
2. **Mejor mantenimiento y legibilidad**:
    
    - Dado que los programas declarativos tienden a ser más concisos, su **mantenimiento** es más sencillo. La lógica se centra en los **resultados** y las relaciones, lo que hace que el código sea fácil de leer y entender.
        
3. **Optimización automática**:
    
    - Los sistemas que ejecutan código declarativo suelen ser responsables de la optimización interna. Esto permite a los programadores escribir código más eficiente sin preocuparse por las optimizaciones de bajo nivel.
        
4. **Menos errores de manejo de estado**:
    
    - Dado que los lenguajes declarativos no permiten modificar el estado de las variables o estructuras de datos de manera directa (como ocurre en los lenguajes imperativos), se minimiza el riesgo de **errores de estado** o **efectos secundarios**.
        
5. **Adaptabilidad**:
    
    - Los lenguajes declarativos pueden ser más fáciles de **adaptar** o **extender**, ya que suelen ser más generales y menos rígidos en cuanto a la implementación de detalles de ejecución.
        

#### **Desventajas de la Programación Declarativa**

1. **Menos control sobre el rendimiento**:
    
    - Dado que el sistema se encarga de la ejecución, a veces es difícil **controlar** el rendimiento de un programa declarativo. Las optimizaciones automáticas pueden no ser siempre las más adecuadas para ciertos casos de uso.
        
2. **Curva de aprendizaje**:
    
    - Los paradigmas declarativos, especialmente la **programación funcional** o **lógica**, pueden tener una curva de aprendizaje más pronunciada para los programadores acostumbrados a enfoques **imperativos**.
        
3. **Menos flexibilidad**:
    
    - La **flexibilidad** de un lenguaje declarativo puede verse reducida en comparación con los lenguajes imperativos. Esto se debe a que los programadores tienen menos control sobre el flujo de ejecución, lo que puede ser un inconveniente en sistemas muy específicos.
        

#### **Ejemplos de Lenguajes Declarativos**

1. **Haskell (Funcional)**:
    
    - Haskell es un lenguaje **funcional** puramente declarativo que se utiliza ampliamente en **matemáticas** y **procesamiento simbólico**. El lenguaje se basa en funciones matemáticas y asegura que el estado nunca se modifica (inmutabilidad), lo que reduce los efectos secundarios y mejora la fiabilidad del código.
        
2. **Prolog (Lógico)**:
    
    - Prolog es un lenguaje de programación lógica que permite declarar hechos y reglas sobre un dominio específico. El sistema trata de deducir la respuesta mediante inferencia lógica, es decir, resolviendo consultas sobre hechos definidos.
        
3. **SQL (Consulta Declarativa)**:
    
    - SQL es un lenguaje **declarativo** utilizado para gestionar bases de datos. Permite especificar qué información se desea obtener de una base de datos, sin especificar cómo debe obtenerse. El motor de la base de datos optimiza y ejecuta la consulta.
        

#### **Ejemplo en Haskell (Programación Funcional Declarativa)**

```haskell
-- Definir una función que calcule la suma de una lista de números
sumarLista :: [Int] -> Int
sumarLista = sum

-- Usar la función en un programa
main = print (sumarLista [1, 2, 3, 4, 5])
```

En este ejemplo de Haskell, no se especifica cómo se debe recorrer la lista ni cómo se deben acumular los valores; simplemente se **declara** que la función `sumarLista` debe sumar los elementos de la lista.

#### **Ejemplo en Prolog (Programación Lógica Declarativa)**

```prolog
% Hechos
padre(john, mary).
padre(john, mike).
madre(susan, mary).
madre(susan, mike).

% Regla
hermano(X, Y) :- padre(P, X), padre(P, Y), X \= Y.

% Consulta
?- hermano(mary, mike).
```

En este ejemplo de Prolog, se definen hechos (por ejemplo, `padre(john, mary)`) y reglas (por ejemplo, `hermano(X, Y)`), y el sistema puede deducir respuestas a consultas como `hermano(mary, mike)`.

### **Conclusión**

La **programación declarativa** es ideal para aquellos casos en los que el enfoque del programador se centra en **especificar qué** debe hacerse, y el **sistema** se encarga de determinar el **cómo**. Este enfoque reduce la complejidad de la programación, mejorando la **legibilidad**, **mantenibilidad** y **fiabilidad** del código. Sin embargo, puede ser menos flexible y menos eficiente en términos de control de rendimiento, especialmente en aplicaciones que requieren una optimización específica del proceso de ejecución.