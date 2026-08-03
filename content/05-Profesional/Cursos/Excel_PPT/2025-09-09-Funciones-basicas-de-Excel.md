---
title: "Excels"
date: 2026-01-26
tags:
  - profesional
  - cursos
  - excel_ppt
---
# Excels

> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/ARIN|ARIN]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

![[assets/Pasted image 20250909093052.png]]


los dolares  es para fija fija  la columna facilita mucho trabajo


![[assets/Pasted image 20250909095948.png]]



---

## **Funciones básicas de Excel**

- **SUMA**: devuelve la suma de un rango de datos.  
    Uso: `=SUMA(A1:A10)`  
    Recomendación: útil para sumar grandes volúmenes de datos.
    
- **PROMEDIO**: calcula la media de un rango de datos.  
    Uso: `=PROMEDIO(A1:A10)`  
    Recomendación: medir tendencia central en conjuntos de datos.
    
- **MAX / MIN**: obtiene el valor máximo o mínimo de un rango.  
    Uso: `=MAX(A1:A10)` o `=MIN(A1:A10)`  
    Recomendación: identificar valores extremos.
    
- **CONTAR**: cuenta las celdas que contienen números.  
    Uso: `=CONTAR(A1:A10)`  
    Recomendación: útil para contar registros en tablas.
    

---

## **Funciones condicionales**

- **SI**: permite devolver un valor u otro en función de una condición.  
    Uso: `=SI(A1>10,"Alto","Bajo")`  
    Recomendación: crear nuevas columnas dinámicas basadas en condiciones.
    
- **SI.CONJUNTO**: permite evaluar varias condiciones a la vez.  
    Uso: `=SI.CONJUNTO(A1>10,"Alto",A1<=10,"Bajo")`  
    Recomendación: útil cuando hay múltiples criterios.
    
- **CONTAR.SI**: cuenta cuántas celdas cumplen una condición.  
    Uso: `=CONTAR.SI(A1:A10,">10")`
    
- **CONTAR.SI.CONJUNTO**: cuenta celdas que cumplen varias condiciones.  
    Uso: `=CONTAR.SI.CONJUNTO(A1:A10,">10",B1:B10,"Rojo")`
    
- **SUMAR.SI / SUMAR.SI.CONJUNTO**: suman valores que cumplen una o varias condiciones.  
    Uso: `=SUMAR.SI(A1:A10,">10",B1:B10)`
    
- **SI.ERROR**: devuelve un valor alternativo si la fórmula genera error.  
    Uso: `=SI.ERROR(A1/B1,"Error")`
    
- **Y / O**: evalúan condiciones lógicas.
    
    - `=Y(A1>10, B1<5)` → verdadero si ambas se cumplen.
        
    - `=O(A1>10, B1<5)` → verdadero si al menos una se cumple.
        

---

## **Funciones de búsqueda y referencia**

- **BUSCARV (VLOOKUP)**: busca un valor en la primera columna de una tabla y devuelve datos de otra columna.  
    Uso: `=BUSCARV(123, A2:D10, 2, FALSO)`
    
- **BUSCARH (HLOOKUP)**: igual que BUSCARV, pero en filas.
    
- **INDICE**: devuelve el valor de una celda específica de una matriz.  
    Uso: `=INDICE(A1:C10,2,3)` → fila 2, columna 3.
    
- **COINCIDIR**: devuelve la posición de un valor en un rango.  
    Uso: `=COINCIDIR(50,A1:A10,0)`
    

 Consejo: combinar **INDICE + COINCIDIR** es mucho más flexible que BUSCARV.

---

## **Funciones de utilidad**

- **ALEATORIO**: genera un número decimal entre 0 y 1.  
    Uso: `=ALEATORIO()`
    
- **SUBTOTALES**: devuelve la suma, promedio u otras operaciones sobre un rango filtrado.  
    Uso: `=SUBTOTALES(9,A1:A10)` (9 = suma).
    


## **Funciones de manejo de texto**

- **REGEXTRACT (Extraer con expresiones regulares)**
    
    - **Uso**: `=REGEXTRACT(texto, expresión_regular)`
        
    - Sirve para extraer parte de un texto siguiendo un **patrón** definido (expresiones regulares).
        
    - Ejemplo: `=REGEXTRACT("Pedido: 12345", "\d+")` devuelve `12345`.
        
    - Muy útil para separar códigos, números o formatos dentro de cadenas largas.
        
- **CONCAT (Concatenar)**
    
    - **Uso**: `=CONCAT(texto1, texto2)`
        
    - Une dos cadenas de texto en una sola.
        
    - Ejemplo: `=CONCAT("Hola ", "Mundo")` → devuelve `Hola Mundo`.
        
    - Variantes más potentes:
        
        - `CONCATENAR` (varios argumentos).
            
        - `TEXTJOIN` (permite añadir separadores y omitir vacíos).
            

---

## **Funciones de obtención de información**

- **FILTER (Filtrar)**
    
    - **Uso**: `=FILTER(rango, condición)`
        
    - Devuelve las filas de un rango que cumplen con una condición específica.
        
    - Ejemplo:
        
        - Si en A1:A5 tienes nombres y en B1:B5 edades, puedes usar:  
            `=FILTER(A1:A5, B1:B5>18)` → devuelve los nombres de mayores de 18.
            
    - Es muy potente porque reemplaza el uso de filtros manuales y permite análisis dinámicos.
        

---





---

## **Errores comunes en Excel y su significado**

- **#N/A (No disponible)**
    
    - **Significado**: el valor no existe en el rango especificado.
        
    - **Motivo**: suele aparecer en funciones de búsqueda (**BUSCARV, BUSCARH, COINCIDIR**) cuando no encuentran el dato buscado.
        
    - **Solución**: verificar que el dato existe en la tabla y usar `SI.ERROR` o `SI.ND` para controlar el error.
        
- **#VALOR! (Valor inválido)**
    
    - **Significado**: se está utilizando un tipo de dato incorrecto.
        
    - **Motivo**: introducir texto donde se esperan números, espacios ocultos o caracteres erróneos.
        
    - **Solución**: limpiar los datos (`LIMPIAR`, `ESPACIOS`) y comprobar formatos.
        
- **#REF! (Referencia no válida)**
    
    - **Significado**: la celda a la que se hace referencia ya no existe.
        
    - **Motivo**: se eliminó o movió una celda, fila o columna usada en una fórmula.
        
    - **Solución**: revisar las referencias y rehacer la fórmula.
        
- **#NAME? (Nombre no válido)**
    
    - **Significado**: Excel no reconoce la función o el nombre introducido.
        
    - **Motivo**: error de tipeo en la fórmula, falta de comillas en texto o referencia inexistente.
        
    - **Solución**: comprobar la sintaxis y el idioma de la función (ej. `=SUMA` en español, `=SUM` en inglés).
        
- **#DIV/0! (División por cero)**
    
    - **Significado**: intento de dividir entre 0 o entre una celda vacía.
        
    - **Motivo**: el denominador de la división no es válido.
        
    - **Solución**: usar `SI.ERROR(A1/B1,0)` para devolver 0 si ocurre el error.
        
- **###### (Celda no legible)**
    
    - **Significado**: Excel no puede mostrar el contenido.
        
    - **Motivo**: el ancho de la celda es demasiado pequeño.
        
    - **Solución**: ampliar la columna.
        
- **#NULL! (Intersección no válida)**
    
    - **Significado**: referencia de rango vacía o inexistente.
        
    - **Motivo**: usar rangos incorrectos en fórmulas.
        
    - **Solución**: verificar las referencias de rango.
        
- **#NUM! (Número inválido)**
    
    - **Significado**: resultado numérico imposible de mostrar.
        
    - **Motivo**: operaciones con valores demasiado grandes o pequeños, o cálculos imposibles (por ejemplo, raíz cuadrada de un número negativo sin usar complejos).
        
    - **Solución**: revisar la lógica del cálculo y los valores de entrada.
        


---

## **Atajos de teclado más usados en Excel**

- **Copiar y pegar**
    
    - `CTRL + C`: Copiar.
        
    - `CTRL + V`: Pegar.
        
- **Formato y edición**
    
    - `CTRL + 1`: Abrir el cuadro de **Formato de celdas**.
        
    - `CTRL + Z`: Deshacer la última acción.
        
    - `CTRL + Y`: Rehacer la última acción deshecha.
        
    - `CTRL + G`: Guardar.
        
    - `CTRL + B`: Poner o quitar **negrita**.
        
    - `CTRL + U`: Poner o quitar **subrayado**.
        
    - `CTRL + I`: Poner o quitar **cursiva**.
        
- **Búsqueda y reemplazo**
    
    - `CTRL + F`: Buscar.
        
    - `CTRL + H`: Reemplazar.
        
- **Navegación**
    
    - `CTRL + RePág / AvPág`: Moverse entre hojas del libro.
        
    - `CTRL + Flechas`: Ir hasta la primera o última celda con datos en una fila o columna.
        
    - `CTRL + INICIO`: Ir a la primera celda de la hoja (A1).
        
    - `CTRL + FIN`: Ir a la última celda con datos.
        
- **Selección de celdas**
    
    - `Shift + Flechas`: Seleccionar celdas contiguas.
        
    - `CTRL + Shift + Flechas`: Seleccionar hasta la última celda con datos.
        
- **Gestión de filas y columnas**
    
    - `CTRL + “+”`: Insertar filas o columnas.
        
    - `CTRL + “-”`: Eliminar filas o columnas.
        
- **Otros útiles**
    
    - `Fn + F4`: Fijar referencias de celda (absoluta, relativa, mixta) al arrastrar fórmulas.
        


---

### 1. **Referencia relativa (A1)**

- Por defecto, Excel cambia la referencia al arrastrar.
    
- Ejemplo: en la celda B1 escribes `=A1`.
    
    - Si arrastras hacia abajo a B2 → se convierte en `=A2`.
        
    - Si arrastras a la derecha a C1 → se convierte en `=B1`.  
         Es útil cuando quieres que la fórmula se adapte automáticamente.
        

---

### 2. **Referencia absoluta ($A$1)**

- La columna y la fila están “fijadas” con `$`.
    
- Ejemplo: en la celda B1 escribes `=$A$1`.
    
    - Si arrastras hacia abajo o a la derecha, **siempre apuntará a A1**.  
         Es útil cuando todas las fórmulas deben usar un mismo valor fijo (por ejemplo, el tipo de cambio, IVA, una constante).
        

---

### 3. **Referencia mixta ($A1 o A$1)**

- Solo se fija la fila o la columna:
    
    - `$A1`: siempre la columna A, pero la fila cambia al arrastrar.
        
    - `A$1`: siempre la fila 1, pero la columna cambia al arrastrar.  
         Es útil en tablas dinámicas de fórmulas, cuando quieres fijar solo una dimensión (fila o columna).
        

---

 **En resumen:**  
Fijar sirve para que tus fórmulas **no se rompan al copiarlas o moverlas**. Te da control sobre si quieres que la celda de referencia se actualice o no.


# Entregar caso 2
Marina Gomez Martin
Hugo hernandez martín


# Power point 
slide master
con el slide master se puede coger el slidedropper

![[assets/Pasted image 20250909154628.png]]
![[assets/Pasted image 20250909154648.png]]


![[assets/Pasted image 20250909154953.png]]
![[assets/Pasted image 20250909155015.png]]