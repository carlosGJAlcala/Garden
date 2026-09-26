# Compiladores - Tema 10: Generación de código y optimización

## Contenidos
- Introducción
- Operaciones básicas
- Optimización del código
## Introducción
En el caso de los lenguajes de programación, la generación de código objetivo depende del código intermedio y de la plataforma de ejecución.
En general, puede funcionar de dos formas:
- Como una fase independiente, traduciendo el código intermedio al código objeto equivalente.
- Integrado con el análisis semántico, generando código objeto a medida que se encuentran construcciones semánticamente correctas. Es una opción más rápida pero también más compleja.
Se trata de una etapa de gran importancia: la ejecución de un código objeto eficiente es mucho más rápida que la de un código objeto de poca calidad.
Sin embargo, una optimización demasiado "agresiva" del código generado puede resultar incluso errónea:
```c
static int always = 1;
int main ( void) {
 while ( always) { }
}
```
frente a la versión optimizada ( incorrecta si `always` puede cambiar en tiempo de ejecución):
```c
int main ( void) {
 while ( 1) { }
}
```
### Tipos de código objeto
**Lenguaje ensamblador**. Al utilizar instrucciones simbólicas, simplifica el proceso de generación de código.
- Se necesita utilizar un ensamblador para obtener el código máquina.
**Lenguaje máquina absoluto**. Este código es directamente ejecutable, ya que utiliza direcciones de memoria absolutas ( fijas).
- Es un código eficiente, pero poco flexible.
- Muy utilizado por los compiladores antiguos, menos usado actualmente.
**Lenguaje máquina relocalizable**. Está constituido por módulos objeto. El código se genera con desplazamientos de direcciones, lo cual permite enlazar diferentes módulos objeto ( ej., bibliotecas).
- Flexible: permite compilar rutinas por separado y llamar a rutinas ya compiladas en otros módulos.
- Método más utilizado en compiladores comerciales.
- Es necesario un enlazador para crear el ejecutable.
## Operaciones básicas
### Generación automática de código
La conversión de código intermedio en forma de cuádruplas a código ensamblador es sencilla. Cada tipo de cuádrupla se sustituye por un conjunto de instrucciones equivalentes en código ensamblador.
Por ejemplo:
```
x = y + z
LOAD Reg1, y
LOAD Reg2, z
ADD Reg2, Reg1, Reg2
STR x, Reg2
```
Es necesario disponer de un conjunto de rutinas de ayuda que faciliten ciertas tareas propias de la generación de código ( escribir, cargar, etc.).
### Asignación
Para las instrucciones de asignación, `A = B`, el código en cuádruplas es del tipo `( assign, A, B, -)` y el código de ensamblador equivalente que hay que generar es el siguiente:
| Código de alto nivel | Código objeto de ensamblador |
|---|---|
| `a = b` | `LOAD Reg1, b` / `STR a, Reg1` |
### Condicionales
| Código de tres direcciones | Código objeto de ensamblador |
|---|---|
| `if false tmp1 goto L1` / `...` / `L1: ...` | `LOAD Reg1, tmp1` / `FJMP Reg1, L1` / `...` / `L1: ...` |
### Arrays
| Código de tres direcciones | Código objeto de ensamblador |
|---|---|
| `x = A[i]` | `LOAD Reg1, i` / `MULT Reg1, Reg1, 2 (*)` / `LOAD Reg2, A ( Reg1)` / `STR x, Reg2` |
(*) Suponiendo que A es un array cuyos elementos ocupan 2 bytes, por ejemplo, enteros.
### Otras consideraciones
Para obtener código de buena calidad:
- Evitar las cargas y descargas innecesarias desde/hacia memoria.
- Utilizar eficientemente los registros del procesador ( son más rápidos que la memoria convencional).
Las particularidades del hardware influyen en la calidad y eficiencia del código generado. Por ejemplo:
- INC es más eficiente que ADD cuando el incremento es 1.
- CLEAR es más eficiente que MOV para guardar el valor 0.
## Optimización del código
La velocidad de ejecución del código objeto creado es de especial importancia, sobre todo en aplicaciones de tiempo real y de cálculo intensivo.
Dado que el proceso de generación de código objeto es básicamente un proceso de sustitución de macros, el código generado puede acabar siendo de mala calidad.
La tarea del proceso de optimización es mejorar la calidad y eficiencia del código objeto para incrementar la velocidad de ejecución y reducir su espacio ocupado.
Las optimizaciones de espacio suelen ser incompatibles con las de velocidad: mejorar la velocidad suele aumentar el espacio requerido y viceversa.
El proceso de mejora de código se puede hacer sobre:
- El código intermedio generado tras el análisis semántico.
- El código objeto tras la fase de generación de código.
Las técnicas de optimización se basan en un análisis de la estructura del programa y del flujo de datos que subdividen el programa en regiones de optimización.
Las técnicas de mejora se pueden aplicar en dos ámbitos:
- Local, si solo utiliza información de un bloque básico ( ej., un bucle).
- Global, si utiliza información de un conjunto de bloques básicos.
### Bloques básicos de optimización
**Bloque básico**: unidad fundamental de código, una secuencia de instrucciones en la que el flujo de control entra en el inicio del bloque y sale al final.
En optimizaciones sobre un bloque básico, los valores de las variables a la entrada y salida del bloque deben coincidir con los del código sin transformar.
Las mejoras sobre bloques básicos permiten una optimización por partes completas, más eficiente que una optimización por líneas y menos compleja que una optimización global.
#### Ejemplo
```
Código de alto nivel Bloque
w = 0; 1
x = x + y;
y = 0;
if ( x>z) {
 y = x; 2
 x++;
} else { 3
 y = z;
 z++;
}
w = x + z; 4
```
### Eliminación de subexpresiones comunes
Si una expresión se calcula más de una vez, se puede utilizar el resultado obtenido la primera vez para reemplazar los cálculos posteriores SIEMPRE QUE los operandos involucrados no se hayan modificado entre ambas apariciones.
```
Antes: Después:
t1 = 4 − 2 t1 = 4 − 2
t2 = t1 / 2 t2 = t1 / 2
t3 = a * t2 t3 = a * t2
t4 = t3 * t1 t4 = t3 * t1
t5 = t4 + b t5 = t4 + b
t6 = t3 * t1 t6 = t4
t7 = t6 + b t7 = t6 + b
c = t5 * t7 c = t5 * t7
```
### Eliminación de código muerto
**Código muerto** se refiere a:
- Código que no se ejecutará nunca.
- Operaciones insustanciales, por ejemplo, declaraciones nulas o asignaciones de una variable a sí misma.
- Código no alcanzable.
Un identificador está vivo al final de un bloque básico si su valor es referenciado en otro bloque básico. Por el contrario, está muerto si no es referenciado en el resto del programa.
Ejemplo 1:
```
Antes: Después:
b := false; b := false;
if ( a AND b) then
 instrucciones
```
Ejemplo 2:
```
Antes: Después:
int global; int global;
void f () { void f () {
 int i; global = 2;
 i = 1; return;
 global = 1; }
 global = 2;
 return;
 global = 3;
}
```
### Propagación de copias
Después de ejecutar asignaciones de la forma `a = b`, `a` y `b` tienen el mismo valor y, por tanto, podemos reemplazar las apariciones de `a` por `b`. Los identificadores muertos, que aparecen como consecuencia de optimizaciones de propagación de copias, pueden ser eliminados.
```
Paso 0 Paso 1 Paso 2 Paso 3
t1 = 4 − 2 t1 = 4 − 2 t1 = 4 − 2 t1 = 4 − 2
t2 = t1 / 2 t2 = t1 / 2 t2 = t1 / 2 t2 = t1 / 2
t3 = a * t2 t3 = a * t2 t3 = a * t2 t3 = a * t2
t4 = t3 * t1 t4 = t3 * t1 t4 = t3 * t1 t4 = t3 * t1
t5 = t4 + b t5 = t4 + b t5 = t4 + b t5 = t4 + b
t6 = t3 * t1 t6 = t4 t6 = t4
t7 = t6 + b t7 = t4 + b t7 = t5
c = t5 * t7 c = t5 * t7 c = t5 * t5 c = t5 * t5
```
### Optimizaciones aritméticas
Se pueden aplicar transformaciones para reducir el número de operaciones o sustituir operaciones costosas por otras equivalentes más simples.
- Cálculo previo de constantes.
- Transformaciones algebraicas.
Cuando en una expresión aparecen diferentes constantes, se pueden combinar en tiempo de compilación para formar una sola.
```
t1 = 4 − 2 : t1 = 2
t2 = t1 / 2 : t2 = 1
t3 = a * t2 : t3 = a
t4 = t3 * t1 : t4 = a * 2
t5 = t4 + b : t5 = t4 + b
c = t5 * t7 : c = t5 * t5
```
Cuando en el código aparece una identidad algebraica, se puede simplificar. Las transformaciones más normales son las siguientes:
- Suma: `a + 0 = 0 + a = a`
- Resta: `a − 0 = a`
- Multiplicación: `a * 1 = 1 * a = a`
- División: `a / 1 = a`
### Reducción de fuerza
Esta técnica consiste en sustituir operaciones costosas por otras menos costosas equivalentes. Por ejemplo:
- La multiplicación es más costosa que la suma: `a * 2 : a + a`
- La elevación al cuadrado y el producto: `x² : x * x`
- La división y multiplicación por una potencia de dos es más fácil de implantar con desplazamientos binarios.
```
Antes: Después:
t4 = a * 2 t4 = a + a
t5 = t4 + b t5 = t4 + b
c = t5 * t7 c = t5 * t7
```
### Reorganizaciones
Con las propiedades asociativa y distributiva de las operaciones se puede variar el código de las expresiones aritméticas y reducir el número de identificadores involucrados en el cálculo.
```
x = x + y + x * y x = x * y + x + y
MOV Reg1, x MOV Reg1, x
MOV Reg2, y MOV Reg2, y
ADD Reg1, Reg2 MUL Reg2, Reg1
MOV Reg3, Reg1 ADD Reg2, Reg1
MOV Reg1, x MOV Reg1, y
MUL Reg1, Reg2 ADD Reg2, Reg1
ADD Reg1, Reg3 STR x, Reg2
STR x, Reg1
```
### Empaquetamientos temporales
Después de haber aplicado una técnica para mejorar el código, se puede reducir el número de identificadores temporales utilizados. Podemos reducir dos nombres temporales a uno solo, si no hay ningún punto en el que los dos estén "vivos" simultáneamente.
### Mejora de bucles
Uno de los puntos donde el programa suele consumir más tiempo de procesamiento es en los bucles.
- Pequeñas mejoras dentro de un bucle pueden representar grandes mejoras en la velocidad de ejecución.
Técnicas para mejorar la eficiencia de los bucles:
- Reducción de frecuencia o traslado de código.
- Optimización por combinación.
- Optimización por desarrollo.
#### Reducción de frecuencia
Consiste en mover de lugar ciertos cálculos para que se ejecuten con menos frecuencia.
```
Antes: Después:
i := 0 i := 0
repeat t1 := j−k
 x := x + h[i + j−k] t2 := max−3
 i := i + 3 repeat
until ( i > max−3) x := x + h[i + t1]
 i := i + 3
 until ( i > t2)
```
#### Optimización por combinación
Esta técnica se basa en transformar dos o más bucles consecutivos en uno solo equivalente que mejore la eficiencia y la velocidad.
```
Antes: Después:
for i:=1 to 10000 do for k:=1 to 10000 do
 A[i] := 1; A[k] := 1;
for j:=1 to 10000 do B[k] := k;
 B[j] := j;
```
#### Optimización por desarrollo
Cuando el cuerpo del bucle tiene pocas instrucciones y el número de repeticiones es pequeño y conocido en tiempo de compilación, es posible evitar todo el control del bucle y sustituirlo por instrucciones secuenciales individuales.
```
Antes: Después:
for i:=1 to 5 do h[1] := 1;
 h[i] := i; h[2] := 2;
 h[3] := 3;
 h[4] := 4;
 h[5] := 5;
```
## Lecturas
- Compiladores: Principios, técnicas y herramientas, 2ª Ed., A.V. Aho, Monica S. Lam, Ravi Sethi, Jeffrey D. Ullman, Addison Wesley, 2008. Cap. 8 y 9.
- K.C. Louden, Construcción de compiladores: principios y práctica. Ed. Thomson, 2004. Cap. 8, sección 8.2 a 8.10.
