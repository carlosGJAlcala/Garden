---
title: "Función para sumar dos números"
date: 2026-01-26
tags:
  - desarrollo-software
  - paradigmas
  - paradigmas-de-objectivos
---
### **Paradigma de Programación Funcional**


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

La **programación funcional** es un paradigma declarativo que se basa en el uso de **funciones matemáticas** para transformar datos, en lugar de depender de instrucciones secuenciales que modifican el estado del programa. En este paradigma, las funciones son tratadas como **ciudadanos de primera clase**, lo que significa que pueden ser pasadas como parámetros, devueltas como valores y almacenadas en variables. Es un enfoque que promueve un estilo de codificación limpio, modular y **sin efectos secundarios**.

#### **Características del Paradigma Funcional**

1. **Funciones como primeros ciudadanos**:
    
    - En la programación funcional, las funciones no solo son usadas para organizar el código, sino que se consideran **primeros ciudadanos**. Esto significa que las funciones pueden ser asignadas a variables, pasadas como argumentos y retornadas como valores de otras funciones.
        
2. **Inmutabilidad**:
    
    - En lugar de modificar el estado de las variables, los lenguajes funcionales fomentan la **inmutabilidad**. Las variables, una vez asignadas, no pueden cambiar su valor. Esto evita problemas comunes relacionados con los efectos secundarios, como las condiciones de carrera en sistemas concurrentes.
        
3. **Funciones puras**:
    
    - Una **función pura** es aquella que no tiene efectos secundarios y siempre produce el mismo resultado para los mismos argumentos. Esto hace que el código sea predecible y fácil de probar.
        
    - Las funciones puras no modifican el estado global ni afectan a otros valores fuera de su alcance.
        
4. **Recursión**:
    
    - En programación funcional, la **recursión** se utiliza como la principal forma de **iteración** en lugar de bucles. Esto se debe a que las funciones pueden llamarse a sí mismas, lo que permite la repetición de tareas de forma elegante.
        
5. **Evaluación perezosa**:
    
    - Algunos lenguajes funcionales, como **Haskell**, utilizan **evaluación perezosa** (lazy evaluation). Esto significa que las expresiones no se evalúan hasta que realmente se necesitan, lo que permite una mayor **eficiencia** y la creación de estructuras de datos infinitas.
        
6. **Composición de funciones**:
    
    - La programación funcional promueve la **composición de funciones**, donde las salidas de una función se pasan como entradas a otra función. Este enfoque facilita la creación de programas modulares y reutilizables.
        
7. **Funciones de orden superior**:
    
    - Las **funciones de orden superior** son funciones que toman otras funciones como argumentos o devuelven funciones como resultado. Esto permite una mayor abstracción y flexibilidad en la programación.
        

#### **Ventajas de la Programación Funcional**

1. **Mayor modularidad y reusabilidad**:
    
    - Las funciones en programación funcional son generalmente **pequeñas** y tienen **responsabilidades bien definidas**, lo que facilita la creación de código **modular** y **reutilizable**.
        
2. **Menos errores de estado**:
    
    - Al promover la **inmutabilidad**, los lenguajes funcionales eliminan muchos errores comunes relacionados con el manejo de estados compartidos y la modificación no controlada de variables.
        
3. **Fácil de probar**:
    
    - Debido a que las funciones son puras (sin efectos secundarios), los programas funcionales son **más fáciles de probar**, ya que las pruebas pueden centrarse exclusivamente en los valores de entrada y salida de las funciones.
        
4. **Paralelismo y concurrencia**:
    
    - La inmutabilidad de los datos y la ausencia de efectos secundarios hace que los programas funcionales sean **más fáciles de paralelizar** y ejecutar en **entornos concurrentes**, ya que no hay problemas de **condiciones de carrera**.
        
5. **Expresividad y concisión**:
    
    - La programación funcional permite escribir código de manera muy **concisa** y **expresiva**. Las operaciones sobre datos se pueden realizar de manera muy eficiente utilizando funciones como **map**, **filter** y **reduce**.
        

#### **Desventajas de la Programación Funcional**

1. **Curva de aprendizaje empinada**:
    
    - Para los programadores acostumbrados a lenguajes **imperativos** o **orientados a objetos**, la programación funcional puede ser **difícil de aprender**, especialmente debido a conceptos como **recursión** y **funciones puras**.
        
2. **Eficiencia**:
    
    - Aunque los lenguajes funcionales pueden ser muy eficientes para ciertas tareas, algunos lenguajes funcionales pueden ser **menos eficientes** que los imperativos en términos de **rendimiento** debido a la falta de optimización en operaciones recursivas y la gestión de memoria.
        
3. **Falta de soporte para algunas operaciones**:
    
    - Algunos lenguajes funcionales no tienen un **soporte directo** para operaciones imperativas de bajo nivel o interactuar directamente con hardware o sistemas operativos, lo que puede limitar su uso en ciertos tipos de aplicaciones.
        
4. **Complejidad en la optimización**:
    
    - Algunos programas funcionales pueden ser **difíciles de optimizar** debido a la **recursión** y a la **evaluación perezosa**, lo que puede resultar en un mayor uso de memoria o cálculos más lentos si no se manejan adecuadamente.
        

#### **Ejemplos de Lenguajes Funcionales**

1. **Haskell**:
    
    - **Haskell** es el lenguaje funcional por excelencia. Se caracteriza por su **pureza funcional** (casi todas las funciones son puras) y su **evaluación perezosa**. Haskell es ampliamente utilizado en programación matemática, ciencias de la computación y aplicaciones concurrentes.
        
2. **Lisp**:
    
    - **Lisp** es uno de los lenguajes más antiguos que soporta programación funcional. Aunque también tiene soporte para otros paradigmas, es conocido por su flexibilidad y por ser el primer lenguaje en incorporar el concepto de **funciones de primera clase**.
        
3. **Scala**:
    
    - **Scala** es un lenguaje que soporta tanto **programación funcional** como **orientada a objetos**. Combina características de ambos paradigmas, permitiendo a los desarrolladores elegir el enfoque más adecuado para su tarea.
        
4. **F#**:
    
    - **F#** es un lenguaje funcional que se ejecuta en la **.NET Framework**. Soporta programación funcional de manera extensiva, y al mismo tiempo permite la interoperabilidad con bibliotecas y herramientas de **C#** y otros lenguajes imperativos.
        

#### **Ejemplo en Haskell (Programación Funcional)**

Aquí tienes un ejemplo simple de **Haskell** que calcula la suma de los primeros 10 números enteros utilizando **recursión**:

```haskell
-- Definir la función suma que usa recursión
suma :: Int -> Int
suma 0 = 0
suma n = n + suma (n - 1)

-- Usar la función
main = print (suma 10)
```

**Explicación**:

- La función `suma` es recursiva y devuelve la suma de los números desde 1 hasta el número `n`. En lugar de usar un bucle, la función se llama a sí misma hasta llegar al caso base (`suma 0 = 0`).
    
- Haskell, al ser un lenguaje funcional puro, se enfoca en **funciones puras** y **recursión** como mecanismo de iteración.
    

#### **Ejemplo en Python (Programación Funcional)**

Aunque **Python** no es estrictamente un lenguaje funcional, soporta muchos conceptos de programación funcional. Aquí tienes un ejemplo que usa **`map`** y **`reduce`**:

```python
from functools import reduce

# Función para sumar dos números
def suma(x, y):
    return x + y

# Usar map para aplicar una función a cada elemento de una lista
numeros = [1, 2, 3, 4, 5]
resultado_map = list(map(lambda x: x * 2, numeros))  # Multiplica cada número por 2

# Usar reduce para aplicar la función de suma sobre todos los elementos
resultado_reduce = reduce(suma, numeros)  # Suma todos los números en la lista

print("Resultado de map:", resultado_map)
print("Resultado de reduce:", resultado_reduce)
```

**Explicación**:

- **`map`** aplica una función (`lambda x: x * 2`) a cada elemento de la lista `numeros`, resultando en `[2, 4, 6, 8, 10]`.
    
- **`reduce`** aplica la función `suma` de forma acumulativa a los elementos de la lista, lo que da como resultado `15` (la suma de los números de la lista).
    

#### **Aplicaciones de la Programación Funcional**

1. **Cálculos matemáticos y científicos**:
    
    - La programación funcional es ideal para tareas que requieren **cálculos matemáticos** complejos, como en el procesamiento de señales, estadísticas o análisis de datos.
        
2. **Sistemas concurrentes y paralelos**:
    
    - Gracias a su **inmutabilidad** y la ausencia de efectos secundarios, la programación funcional es altamente eficiente para **sistemas concurrentes** y distribuidos, ya que minimiza los problemas de sincronización y condiciones de carrera.
        
3. **Desarrollo de software modular**:
    
    - La naturaleza modular y de **funciones puras** hace que la programación funcional sea adecuada para desarrollar aplicaciones **modulares**, donde cada componente puede ser independiente y probado de forma aislada.
        
4. **Lenguajes de programación matemática**:
    
    - **Haskell**, **Lisp**, y otros lenguajes funcionales se utilizan en la **investigación matemática** y en el desarrollo de aplicaciones que manipulan grandes cantidades de datos simbólicos.
        

### **Conclusión**

La **programación funcional** es un paradigma poderoso que se centra en el uso de **funciones puras**, **inmutabilidad** y **recursión**. Su enfoque declarativo y matemático permite escribir programas más **limpios**, **predecibles** y fáciles de **probar**. Es especialmente adecuada para problemas que implican cálculos matemáticos, sistemas concurrentes y tareas de procesamiento de datos. Aunque puede ser difícil de aprender para programadores acostumbrados a enfoques imperativos, sus beneficios en **modularidad**, **escalabilidad** y **fiabilidad** la convierten en una opción ideal para muchos tipos de aplicaciones, especialmente aquellas que requieren **alto rendimiento** y **seguridad**.