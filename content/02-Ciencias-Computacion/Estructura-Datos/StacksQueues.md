# Pilas y Colas

Estructuras de Datos
Otoño 2021
Luis de Marcos Ortega
luis.demarcos@uah.es

## Índice

- TAD Pila
- Implementación de pilas
- Aplicaciones de pilas
- TAD Cola
- Implementación de colas
- Aplicaciones de colas

## Bibliografía

- Capítulo 2 de:
  A.V. AHO., J.E. HOPCROFT., J.D. ULLMAN. 1987. "Data Structures and Algorithms." Addison-Wesley.

## Pilas

- Secuencia lineal de elementos
- Un extremo se llama tope (top)
- El otro extremo se llama fondo
- La inserción y eliminación de elementos ocurren ÚNICAMENTE en el extremo superior (tope)
- Otros nombres:
  - Lista Pushdown
  - LIFO (Last In, First Out - Último en Entrar, Primero en Salir)
- Ejemplos de pilas:
  - Libros en una pila en el piso
  - Platos en una repisa
  - …
  - Cualquier situación donde solo es conveniente remover el objeto superior de la pila o añadir uno nuevo encima del tope

## Ejemplo de pila

*(diagrama de dos pilas mostrando un estado antes/después: pila izquierda con A,B,C,D,E de abajo arriba y "top" en E; pila derecha con A,B,C,D,E,F de abajo arriba y "top" en F; la disposición exacta no se pudo recuperar de la extracción)*

- Añadir una taza a la pila
- Remover una taza de la pila

## Operaciones en pilas

- **push**: Insertar un elemento en el tope de la pila.
- **pop**: Eliminar el elemento en el tope de la pila y devolverlo.
  - Algunas implementaciones no lo devuelven.
- **top**: Devolver el elemento en el tope de la pila.
  - A veces también se llama peek.
- **makenull**: Hacer que la pila sea una pila vacía.
- **empty**: Devolver verdadero si la pila está vacía; falso en caso contrario.

## Especificación

```
spec STACK[ITEM]
genres stack, item
operations
push: stack item->stack
pop: stack->item
top: stack->item
makenull: stack->stack
empty: stack->boolean
endspec
```

## Ejemplo I: Procesamiento de editor de texto

- Un carácter de borrado (p. ej. backspace). Usaremos #.
  - `abc##d#e` → `ae`
- Un carácter de cancelación (@) cuyo efecto es descartar todos los caracteres anteriores en la línea actual.
  - `abc@de` → `de`
- Un editor de texto puede procesar una línea de texto usando una pila. Si el carácter leído es:
  - Ni # ni @ → hacer push en la pila
  - # → hacer pop de la pila (ignorar el elemento sacado)
  - @ → vaciar la pila

## Ejemplo II

```
void edit(l:line)
  var s:stack, c:char
  s.makenull()
  while not eonl
    read(c)
    if c='#' then
      s.pop()
    else if c='@' then
      s.makenull()
    else
      s.push(c)
    endif
  endwhile
  print s in reverse order
endproc
```

## Ejemplo: Invertir una lista

- Las pilas pueden usarse para invertir una lista de otros elementos (incluso otra pila).

```
stack reverse(s:stack)
  var e:item
  var rs:stack
  while not s.empty()
    e=s.pop()
    rs.push(e)
  endwhile
  return rs
endfunc
```

## Implementaciones de pilas

- Implementación con array (o implementación con vector)
- Implementación con punteros (o implementación con lista enlazada)

## Implementación con array de pilas

- Esta implementación aprovecha el hecho de que las inserciones y eliminaciones ocurren solo en el tope.
- Anclar el fondo de la pila en el extremo de alto índice del array.
- Dejar que la pila crezca hacia el tope del array (extremo de bajo índice).
- Un cursor indica el tope.

## Implementación con punteros de pilas

- Usar celdas dinámicas que incluyen un elemento de datos y un puntero a la siguiente celda
- La pila se representa como un puntero al tope

*(diagrama de una pila enlazada por punteros con 4 celdas de arriba abajo con valores 8 ( top), 7, 1, 6; la disposición exacta de los punteros no se pudo recuperar de la extracción)*

## Implementación con array vs. implementación con punteros

- Las operaciones son todas operaciones de tiempo constante O(1) en ambas implementaciones (array y punteros)
- Para la implementación con array, las operaciones se realizan en tiempo constante muy rápido
- Para la implementación con array, el tamaño de la pila debe definirse estáticamente (en tiempo de compilación)
  - Deben incluirse verificaciones para no desbordar la pila

## Aplicaciones de pilas

- Verificación de expresiones
- Conversión de expresiones (p. ej. infija a postfija)
- Evaluación de expresiones
- Invocación de métodos y retorno
- Backtracking (p. ej. en grafos)
- En general, las pilas son útiles siempre que una estructura/camino/secuencia deba realizarse o pueda realizarse posteriormente en orden inverso

## Verificación de expresiones

### Ejemplo: Balanceo de símbolos

- Verificar que cada llave derecha, corchete y paréntesis corresponda a su contrapartida izquierda
- Por ejemplo: `[( )]` es legal, pero `[(])` es ilegal

## Verificación de expresiones: Ejemplo de balanceo de símbolos

```
void checkexpression(l:line)
  var s:stack, c,d:char
  s.makenull()
  while not eonl
    read(c)
    if c=openingsymbol then
      s.push(c)
    if c=closingsymbol then
      if s.empty() then
        error()
      else
        d=s.pop()
        if d is not the corresponding closing symbol of c then
          error()
        endif
      endelse
    endif
  endwhile
endproc
```

## Invocación de métodos y retorno

```
public void a()
{ …; b(); …}

public void b()
{ …; c(); …}

public void c()
{ …; d(); …}

public void d()
{ …; e(); …}

public void e()
{ …; c(); …}
```

*(la cadena de llamadas es a() → b() → c() → d() → e() → c(); el original mostraba además, junto a cada llamada, la "dirección de retorno" en la pila de llamadas — probablemente como un diagrama visual de la pila — pero el orden en que la extracción OCR recuperó esas anotaciones ("return address in ...") no se corresponde de forma fiable con cada función, así que se omiten en vez de arriesgar una asociación incorrecta)*

## Invocación de métodos y retorno

```cpp
#include <iostream>

using namespace std;
int fac(int n){
  int product;
  if (n <= 1)
    product = 1;
  else
    product = n * fac(n-1);
  return product;
}
void main(){
  int number;
  cout << "Enter a positive integer : " << endl;;
  cin >> number;
  cout << fac(number) << endl;
}
```

## Invocación de métodos y retorno

Supongamos que el número escrito es 3.

`fac(3)` tiene el valor final devuelto 6:
- ¿3 <= 1? No.
- `product = 3 * fac(2)` → `product = 3 * 2 = 6`, devuelve 6

`fac(2)`:
- ¿2 <= 1? No.
- `product = 2 * fac(1)` → `product = 2 * 1 = 2`, devuelve 2

`fac(1)`:
- ¿1 <= 1? Sí.
- Devuelve 1

## Invocación de métodos y retorno: Pila de llamadas

- Una llamada es un push, un retorno es un pop

Estado de la pila (tope/top):
- `fac(1)` — `prod1 = 1`
- `fac(2)` — `prod2 = 2 * fac(1)`
- `fac(3)` — `prod3 = 3 * fac(2)`

- La pila de programa puede desbordarse

## Evaluación de expresiones

- Expresión infija (completamente entre paréntesis)
- Entrada: Expresión
- Cinco tipos de caracteres de entrada:
  - Paréntesis de apertura: `(`
  - Números 0..9
  - Operadores: `+`, `-`, `*` y `/`
  - Paréntesis de cierre: `)`
  - Carácter de nueva línea
- Salida: Valor de la expresión
- Asunción: La expresión es correcta

## Algoritmo de evaluación de expresiones

```
real evaluateexpression(e:expresion)
  var s:stack; op1, op2, op:char
  makenull(s)
  while not eonl
    read(c)
    case
      c=opening bracket
        s.push(c)
      c=number
        s.push(c)
      c=operation
        s.push(c)
      c=closing bracket
        op2 = s.pop()
        op = s.pop()
        op1 = s.pop()
        s.pop()  [discard opening bracket]
        s.push(Evaluate(op1 op op2))
      end c=closing bracket
    endcase
  endwhile
  return s.pop()
endproc
```

## Evaluación de expresiones: Ejemplo

Entrada: `(( 2 * 5) - ( 1 * 2))`

*(tabla de traza con columnas "Input Symbol", "Stack ( from bottom to top)" y "Operation" para la evaluación de la expresión (( 2 * 5) - ( 1 * 2)); la extracción OCR entremezcló las tres columnas y no fue posible determinar con certeza a qué columna pertenece cada fragmento, así que se conserva el texto extraído íntegro y en su orden original sin reordenar)*

| Símbolo de entrada | Pila (de abajo a arriba) | Operación |
|---|---|---|
| `(` | `(` | |
| `(` | `( (` | |
| `2` | `( ( 2` | |
| `*` | `( ( 2 *` | |
| `5` | `( ( 2 * 5` | |
| `)` | `( 10` | `2 * 5 = 10` y hacer push |
| `-` | `( 10 -` | |
| `(` | `( 10 - (` | |
| `1` | `( 10 - ( 1` | |
| `*` | `( 10 - ( 1 *` | |
| `2` | `( 10 - ( 1 * 2` | |
| `)` | `( 10 - 2` | `1 * 2 = 2` y hacer push |
| `)` | `8` | `10 - 2 = 8` y hacer push |
| Nueva línea | Vacía | Pop y devuelver |

## Colas

- Secuencia lineal de elementos
- Un extremo se llama frente (front)
- El otro extremo se llama trasera (rear)
- Las inserciones se hacen solo en la trasera
- Las eliminaciones se hacen solo en el extremo frontal
- También se conocen como listas FIFO
- FIFO: First In, First Out (Primero en Entrar, Primero en Salir)

*(diagrama de una cola con las operaciones "Insert" en el extremo "Rear (Enqueue)" y "Remove" en el extremo "( Dequeue) Front"; la disposición exacta no se pudo recuperar de la extracción)*

## Ejemplos de colas

- Parada de autobús
- Cola de impresión
- Colas de solicitudes
  - Servidor web
  - Sistema operativo
  - …
- Cualquier cola de la vida real

## Colas vs. Pilas

- Las operaciones para una cola son análogas a las de una pila, siendo las diferencias sustanciales que las inserciones van al final de la lista, en lugar del principio.
- La terminología tradicional para pilas y colas es diferente

## Operaciones en colas

- **enqueue**: Insertar un elemento en la trasera de la cola.
- **dequeue**: Eliminar el elemento en el frente de la cola y devolverlo.
  - Algunas implementaciones no lo devuelven.
- **front**: Devolver el elemento en el frente de la cola.
- **makenull**: Hacer que la cola sea una cola vacía.
- **empty**: Devolver verdadero si la cola está vacía; falso en caso contrario.

## Especificación

```
spec QUEUE[ITEM]
genres queue, item
operations
enqueue: queue item->queue
dequeue: queue->item
front: queue->item
makenull: queue->queue
empty: queue->boolean
endspec
```

## Implementaciones de colas

- Implementación con array de colas
  - El frente siempre puede estar en la posición 1.
  - La trasera será un cursor al último elemento.
  - Enqueue tardará O(1).
  - Dequeue tardará O(n).
- Implementación con array circular de colas
- Implementación con punteros de colas

## Implementación con array circular de una cola

Pienso en un array como un círculo

*(diagrama de un array circular ( `queue[]`) con posiciones [0] a [5] dispuestas en círculo; la disposición exacta no se pudo recuperar de la extracción)*

## Implementación con array circular de una cola

- La cola se encuentra en algún lugar alrededor del círculo en posiciones consecutivas, con la trasera de la cola en algún lugar en el sentido de las agujas del reloj desde el frente.

*(diagrama circular con elementos A, B, C en las posiciones [1]-[3]; la disposición exacta no se pudo recuperar de la extracción)*

## Implementación con array circular de una cola

- Usar cursores para el frente y la trasera
  - El frente está una posición en sentido contrario a las agujas del reloj desde el primer elemento
  - La trasera da la posición del último elemento

*(diagrama circular con elementos A, B, C, cursores "front" y "rear" marcados; la disposición exacta no se pudo recuperar de la extracción)*

## Implementación con array circular de una cola

- Para hacer enqueue de un elemento:
  - Mover la trasera en el sentido de las agujas del reloj
  - Luego poner el nuevo elemento en `queue[rear]`
  - O(1)
- Para hacer dequeue de un elemento:
  - Mover el frente en el sentido de las agujas del reloj
  - Luego extraer de `queue[front]`
  - O(1)

## Implementación con array circular de una cola

- **Problema**: No hay forma de distinguir una cola vacía de una que ocupa todo el círculo

*(dos diagramas circulares comparando un estado casi lleno (D,E,C,F,B,A con front/rear adyacentes) frente a un estado casi vacío del mismo círculo; la disposición exacta no se pudo recuperar de la extracción)*

## Implementación con array circular de una cola: Soluciones

- **Problema**: No hay forma de distinguir una cola vacía de una que ocupa todo el círculo
- **Remedios**:
  - No dejar que la cola se llene completamente
  - Usar una variable booleana que sea verdadera si y solo si la cola está vacía

## Implementación con punteros de colas

- Mantener punteros al frente y al elemento trasero

*(diagrama de una cola enlazada por punteros: firstNode y lastNode apuntando a una lista de celdas a, b, c, d, e ( con null al final), y cursores front/rear; la disposición exacta no se pudo recuperar de la extracción)*

## Aplicaciones de colas

Las colas proporcionan muchos servicios en la informática, transporte, logística, investigación de operaciones, … donde varias entidades como datos, objetos, personas o eventos se almacenan y se mantienen para ser procesados posteriormente.

- Cualquier cosa que se sirva en base de primero en llegar, primero en ser servido puede modelarse como una cola

## Pilas y Colas

Luis de Marcos Ortega
luis.demarcos@uah.es
