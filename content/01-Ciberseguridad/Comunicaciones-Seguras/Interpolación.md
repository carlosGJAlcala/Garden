### Interpolación – Explicación y su aplicación en programación

La **interpolación** es una técnica matemática para **estimar valores intermedios** dentro del rango de un conjunto de datos discretos conocidos. En programación, se usa en **gráficos, simulaciones físicas, videojuegos, procesamiento de imágenes, audio, inteligencia artificial, compresión, predicción, y más**.

## ¿Qué es la interpolación?

Dado un conjunto de puntos conocidos $(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)$, la **interpolación** busca una función $f(x)$ tal que:

$$
f(x_i) = y_i \quad \text{para todo } i
$$

Y que además permita **estimar valores intermedios**: $f(x)$ para $x$ entre los $x_i$.

## Tipos comunes de interpolación

### 1. Interpolación lineal (la más básica y usada)

Entre dos puntos:

$$
f(x) = y_0 + \frac{y_1 - y_0}{x_1 - x_0}(x - x_0)
$$
#### Programación:

```python
def interp_lineal(x0, y0, x1, y1, x):
    return y0 + (y1 - y0) * (x - x0) / (x1 - x0)
```

#### Usos:

- Movimiento suave en videojuegos.
- Animaciones (tweening).
- Audio: interpolación de muestras.
- Ajuste de sensores.

### 2. Interpolación polinómica (Lagrange, Newton)

Encuentra un polinomio P(x)P(x) que pase por todos los puntos.

#### Ejemplo (Lagrange):

$$
P(x) = \sum_{i=0}^n y_i \cdot \ell_i(x) \quad \text{con } \ell_i(x) = \prod_{j \ne i} \frac{x - x_j}{x_i - x_j}
$$

#### Usos:

- Sistemas de computación simbólica.
- Criptografía (ej. **Shamir's Secret Sharing**).
- Reconstrucción de curvas o funciones.

### 3. Interpolación cúbica / spline

Divide los datos en segmentos y ajusta polinomios suaves de grado 3 que se unan con continuidad.

#### Usos:

- Modelado 3D.
- Generación de caminos suaves en IA y robótica.
- Edición gráfica y CAD.

## Aplicaciones en programación

### 1. **Interpolación lineal (lerp) en gráficos y juegos**

```python
def lerp(a, b, t):
    return a + (b - a) * t
```

- `a`, `b`: valores inicial y final.
- `t`: parámetro entre 0 y 1.
- Usado para: colores, posiciones, tamaños, rotaciones...

### 2. **Interpolación de señales (DSP)**

- Audio digital, imagen, vídeo.
- Interpolar entre muestras para reescalar, suavizar, sintetizar.
- Ej.: **upsampling** o reconstrucción de datos faltantes.

### 3. **Interpolación de claves secretas (Shamir's Secret Sharing)**

- Usa **interpolación polinómica** para dividir un secreto en partes.
- Solo si tienes suficientes fragmentos puedes reconstruirlo con **Lagrange**.
- Seguridad distribuida: útil en **criptografía avanzada, HSMs y recuperación tolerante a fallos**.

### 4. **Machine Learning / IA**

- Interpolación en regresión (curvas de predicción).
- Estimación de valores faltantes en datasets.
- Generación de datos artificiales entre puntos conocidos.

### 5. **Interpolación geográfica**

- En sistemas de mapas o GPS:
    - Calcular posición intermedia entre dos puntos.
    - Interpolar elevaciones, temperaturas o rutas.

## Conclusión

La **interpolación permite construir o estimar datos continuos a partir de valores discretos**, y es una técnica omnipresente en programación moderna. Desde **animación, gráficos, predicción, cifrado, hasta diseño CAD o inteligencia artificial**, es una herramienta **simple en principio, pero potentísima en la práctica**.
