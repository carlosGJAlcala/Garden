---
title: "Ecuaciones Diofanticas Lineales"
date: 2026-01-26
tags:
  - ciencias-computacion
  - matematicas
  - aritmetica-entera
---
### Ecuaciones diofánticas lineales – Nota explicada y su aplicación en programación


> **Relacionado**: [[02-Ciencias-Computacion/Matematicas/Aritmetica-entera/Congruencias|Congruencias]]. [[02-Ciencias-Computacion/Matematicas/Aritmetica-entera/Aritmetica-entera|Aritmetica entera]].

Una **ecuación diofántica lineal** es una ecuación de la forma:

ax+by=cax + by = c

donde:

- a,b,c∈Za, b, c \in \mathbb{Z} (enteros),
    
- y **las soluciones buscadas también deben ser enteras**: x,y∈Zx, y \in \mathbb{Z}.
    

---

##  ¿Cuándo tiene solución?

La ecuación ax+by=cax + by = c **tiene solución entera si y solo si**:

MCD(a,b)∣c\text{MCD}(a, b) \mid c

Es decir, **si el máximo común divisor de `a` y `b` divide a `c`**.

---

## ️ En programación: resolverla con el algoritmo extendido de Euclides

###  Algoritmo extendido de Euclides

Además de calcular el MCD de dos números `a` y `b`, este algoritmo **encuentra enteros `x` y `y` tales que**:

ax+by=MCD(a,b)ax + by = \text{MCD}(a, b)

Por lo tanto, **para resolver ax+by=cax + by = c**:

1. Calculamos el MCD.
    
2. Si `d = MCD(a, b)` divide a `c`, multiplicamos la solución por `c/d`.
    

---

###  Ejemplo en Python

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    else:
        d, x1, y1 = extended_gcd(b, a % b)
        x = y1
        y = x1 - (a // b) * y1
        return d, x, y

def solve_diofantica(a, b, c):
    d, x0, y0 = extended_gcd(a, b)
    if c % d != 0:
        return None  # No hay solución
    factor = c // d
    return x0 * factor, y0 * factor  # Solución particular
```

### Uso:

```python
a, b, c = 30, 50, 40
x, y = solve_diofantica(a, b, c)
print(f"Solución: x = {x}, y = {y}")
```

---

##  Aplicaciones en programación

###  1. **Criptografía: inverso modular**

En RSA o Diffie-Hellman necesitas calcular el **inverso de `e` módulo `φ(n)`**:

ex≡1mod  ϕ(n)ex \equiv 1 \mod \phi(n)

→ Es una ecuación diofántica: ex+ϕ(n)y=1ex + \phi(n)y = 1

---

###  2. **Optimización de recursos**

- Problemas de distribución: encontrar combinaciones exactas de elementos con múltiplos fijos.
    
- Por ejemplo: ¿cómo llenar una mochila con paquetes de 7 kg y 11 kg para llegar exactamente a 100 kg?
    

---

###  3. **Teorema chino del resto**

- En la versión extendida, si los módulos **no son coprimos**, se recurre a ecuaciones diofánticas para combinar soluciones.
    
- Importante en **criptografía, sincronización de relojes y comunicaciones distribuidas.**
    

---

### ️ 4. **Motores de álgebra simbólica**

- Sistemas como **SymPy**, **SageMath**, **Mathematica** resuelven ecuaciones diofánticas automáticamente.
    
- Se usan en **CAS** (Computer Algebra Systems), motores de demostración matemática, cálculo simbólico y asistentes automatizados.
    

---

###  5. **Programación competitiva**

- En problemas de **construcción de números enteros**, divisibilidad, combinación de múltiplos o en tareas de **scheduling** con restricciones.
    
- También en juegos tipo "¿se puede sumar 17 usando solo múltiplos de 4 y 7?".
    

---

##  Solución general

Si (x0,y0)(x_0, y_0) es una solución particular de ax+by=cax + by = c, entonces **todas las soluciones** se pueden describir como:

x=x0+bdt,y=y0−adt,t∈Zx = x_0 + \frac{b}{d}t, \quad y = y_0 - \frac{a}{d}t, \quad t \in \mathbb{Z}

Esto permite generar **todas las soluciones enteras**, lo cual es útil para búsquedas o para contar soluciones en programación.

---

##  Conclusión

Las ecuaciones diofánticas lineales **son simples pero poderosas**, y aparecen en programación cuando:

- Necesitas **resolver congruencias** (clave en seguridad).
    
- Buscas **combinaciones exactas** con restricciones.
    
- Calculas **inversos, sincronizaciones, alineaciones** o distribución de recursos.
    

Con el algoritmo extendido de Euclides puedes resolverlas **de forma eficiente**, y aplicarlas directamente en muchos contextos reales de software.

---

¿Quieres que prepare un ejemplo más avanzado donde calculamos el inverso modular y lo usamos para implementar una parte del cifrado RSA?