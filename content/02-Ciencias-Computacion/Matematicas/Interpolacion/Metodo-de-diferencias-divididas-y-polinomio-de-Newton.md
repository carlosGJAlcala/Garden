---
title: "Metodo De Diferencias Divididas Y Polinomio De Newton"
date: 2025-01-01
tags:
  - ciencias-computacion
---

# Método de diferencias divididas y polinomio de Newton

El **método de diferencias divididas** permite construir de forma eficiente un polinomio interpolador que pase por un conjunto de puntos conocidos $$(x_0, y_0), (x_1, y_1), ..., (x_n, y_n)$$.

Es una alternativa más eficiente al método de Lagrange, y permite **añadir nuevos puntos sin recalcular todo desde cero**.

---

##  Polinomio de Newton

La forma general del polinomio de Newton es:

$$
P(x) = f[x_0] + f[x_0, x_1](x - x_0) + f[x_0, x_1, x_2](x - x_0)(x - x_1) + \dots + f[x_0, ..., x_n](x - x_0)(x - x_1)...(x - x_{n-1})
$$

---

##  Diferencias divididas

El **método de diferencias divididas** permite construir **de forma eficiente** un polinomio interpolador que pase por un conjunto de puntos conocidos (x0,y0),(x1,y1),...,(xn,yn)(x_0, y_0), (x_1, y_1), ..., (x_n, y_n). A diferencia de otros métodos como Lagrange, este:

- Permite **añadir puntos sin recalcular todo desde cero**.
    
- Es más eficiente computacionalmente.
    
- Se adapta bien a cálculos simbólicos y numéricos. 

Las **diferencias divididas** se calculan recursivamente:

- Primer orden:

$$
f[x_i] = y_i
$$

$$
f[x_i, x_{i+1}] = \frac{f[x_{i+1}] - f[x_i]}{x_{i+1} - x_i}
$$

- Segundo orden:

$$
f[x_i, x_{i+1}, x_{i+2}] = \frac{f[x_{i+1}, x_{i+2}] - f[x_i, x_{i+1}]}{x_{i+2} - x_i}
$$

Y así sucesivamente hasta completar el grado deseado.

---

##  Ejemplo paso a paso

Dado el conjunto de puntos:

$$
(1, 2),\quad (2, 3),\quad (4, 10)
$$

1. Calcular:

$$
f[1] = 2,\quad f[2] = 3,\quad f[4] = 10
$$

$$
f[1,2] = \frac{3 - 2}{2 - 1} = 1
$$

$$
f[2,4] = \frac{10 - 3}{4 - 2} = 3.5
$$

$$
f[1,2,4] = \frac{3.5 - 1}{4 - 1} = \frac{2.5}{3} \approx 0.8333
$$

2. Polinomio de Newton:

$$
P(x) = 2 + 1(x - 1) + 0.8333(x - 1)(x - 2)
$$

---

##  Implementación en Python

```python
def diferencias_divididas(x, y):
    n = len(x)
    coef = [yi for yi in y]
    for j in range(1, n):
        for i in range(n - 1, j - 1, -1):
            coef[i] = (coef[i] - coef[i - 1]) / (x[i] - x[i - j])
    return coef

def newton_evaluar(x, coef, x_val):
    n = len(coef)
    result = coef[-1]
    for i in range(n - 2, -1, -1):
        result = result * (x_val - x[i]) + coef[i]
    return result

---

## ¿Qué son las diferencias divididas?

Son valores que generalizan las derivadas finitas, y se calculan de manera recursiva:

- Primer orden:  $$
    f[xi]=yi $$f[x_i] = y_i  $$$$
    f[xi,xi+1]=f[xi+1]−f[xi]xi+1−xif[x_i, x_{i+1}] = \frac{f[x_{i+1}] - f[x_i]}{x_{i+1} - x_i}
    $$
- Segundo orden:  
    f[xi,xi+1,xi+2]=f[xi+1,xi+2]−f[xi,xi+1]xi+2−xif[x_i, x_{i+1}, x_{i+2}] = \frac{f[x_{i+1}, x_{i+2}] - f[x_i, x_{i+1}]}{x_{i+2} - x_i}
    
- Y así sucesivamente, hasta llegar al orden nn.
    

Esto genera una **tabla triangular de diferencias divididas**, cuya diagonal principal contiene los coeficientes del polinomio.

---

## Ejemplo simple paso a paso

Supón los puntos:

(1,2),(2,3),(4,10)(1, 2), (2, 3), (4, 10)

1. Calculamos:
    
    - f[1]=2,f[2]=3,f[4]=10f[1] = 2,\quad f[2] = 3,\quad f[4] = 10
        
    - f[1,2]=3−22−1=1f[1,2] = \frac{3 - 2}{2 - 1} = 1  
        f[2,4]=10−34−2=3.5f[2,4] = \frac{10 - 3}{4 - 2} = 3.5
        
    - f[1,2,4]=3.5−14−1=2.53≈0.8333f[1,2,4] = \frac{3.5 - 1}{4 - 1} = \frac{2.5}{3} \approx 0.8333
        
2. Polinomio:
    

P(x)=2+1(x−1)+0.8333(x−1)(x−2)P(x) = 2 + 1(x - 1) + 0.8333(x - 1)(x - 2)

---

## Implementación en programación (Python)

```python
def diferencias_divididas(x, y):
    n = len(x)
    coef = [yi for yi in y]  # copiar y

    for j in range(1, n):
        for i in range(n - 1, j - 1, -1):
            coef[i] = (coef[i] - coef[i - 1]) / (x[i] - x[i - j])
    
    return coef

def newton_evaluar(x, coef, x_val):
    n = len(coef)
    result = coef[-1]
    for i in range(n - 2, -1, -1):
        result = result * (x_val - x[i]) + coef[i]
    return result
```

### Uso:

```python
x = [1, 2, 4]
y = [2, 3, 10]

coeficientes = diferencias_divididas(x, y)
print("Coeficientes:", coeficientes)

valor = newton_evaluar(x, coeficientes, 2.5)
print("P(2.5) =", valor)
```

---

## Aplicaciones prácticas

- **Interpolación eficiente** de datos con posibilidad de añadir nuevos sin recalcular todo.
    
- **Reconstrucción de funciones** cuando se tienen muestras discretas.
    
- **Evaluación rápida** de polinomios por su forma escalonada (análoga a Horner).
    
- Adaptable para **cálculo simbólico** y sistemas algebraicos computacionales.
    
- En criptografía, puede usarse si se implementa en campos finitos.
    

---

## Ventajas

- Menos operaciones que Lagrange para muchos puntos.
    
- Puede construirse incrementalmente.
    
- Permite reutilizar trabajo previo si se añade un nuevo dato.
    
- Requiere solo una tabla de coeficientes y se puede evaluar con eficiencia.
    

---

## Desventajas

- El orden de los puntos importa: el polinomio cambia si se cambian.
    
- Menor estabilidad numérica en ciertos casos respecto a otras formas.
    

---

## Conclusión

El **método de diferencias divididas y el polinomio de Newton** ofrecen una forma potente, eficiente y reutilizable de construir polinomios interpoladores. Son ideales para aplicaciones donde:

- Se agregan datos dinámicamente.
    
- Solo se requiere evaluación rápida.
    
- Se busca optimizar espacio y tiempo en el cálculo.
    

Es uno de los métodos clásicos más usados en análisis numérico, ingeniería, gráficos computacionales y software simbólico.

---

¿Quieres que prepare también una tabla tipo plantilla para que la llenes a mano al resolver ejercicios con diferencias divididas? ¿O prefieres una versión Markdown lista para Obsidian con todo esto estructurado?