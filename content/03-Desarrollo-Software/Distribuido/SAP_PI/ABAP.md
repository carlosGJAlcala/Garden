---
title: "1) Qué es ABAP y dónde se programa"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - sap_pi
---
¡Genial! Te doy una mini‑guía para empezar con **ABAP** desde cero y que puedas escribir tus primeros programas útiles en un sistema SAP.

# 1) Qué es ABAP y dónde se programa


> **Relacionado**: [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

ABAP es el lenguaje propio de SAP para desarrollar sobre el ERP (S/4HANA y clásicos ECC). Hoy se programa sobre todo en:

- **ADT (ABAP Development Tools) en Eclipse**: lo moderno, con autocompletado y pruebas.
- **SE80/SE38 en SAP GUI**: lo clásico.

Objetos típicos: programas (reports), clases, funciones, tablas de diccionario, vistas CDS, servicios OData, ampliaciones (BAdIs/Enhancements).

# 2) Sintaxis mínima que necesitas

Variables y tipos básicos:

```abap
DATA: lv_text TYPE string VALUE 'Hola ABAP',
      lv_num  TYPE i      VALUE 42.
WRITE: / lv_text, lv_num.
```

Estructuras y tablas internas (listas en memoria):

```abap
TYPES: BEGIN OF ty_mat,
         matnr TYPE matnr,
         mtart TYPE mtart,
       END OF ty_mat.

DATA: lt_mat TYPE STANDARD TABLE OF ty_mat WITH EMPTY KEY,
      ls_mat TYPE ty_mat.
```

Condicionales y bucles:

```abap
IF lv_num > 10.
  WRITE: / 'Mayor que 10'.
ENDIF.

DO 3 TIMES.
  WRITE: / 'Iteración'.
ENDDO.
```

# 3) Tu primer report con selección y lectura de datos

Un patrón muy común: pantalla de selección → consulta → mostrar resultados.

```abap
REPORT z_demo_materiales.

PARAMETERS p_mtart TYPE mtart OBLIGATORY.

TYPES: BEGIN OF ty_mat,
         matnr TYPE matnr,
         mtart TYPE mtart,
         ersda TYPE ersda,
       END OF ty_mat.

DATA: lt_mat TYPE STANDARD TABLE OF ty_mat WITH EMPTY KEY.

SELECT matnr mtart ersda
  FROM mara
  INTO TABLE @lt_mat
  WHERE mtart = @p_mtart
  UP TO 100 ROWS.

IF sy-subrc <> 0.
  WRITE: / 'Sin resultados'.
  LEAVE PROGRAM.
ENDIF.

LOOP AT lt_mat ASSIGNING FIELD-SYMBOL(<ls>).
  WRITE: / <ls>-matnr, <ls>-mtart, <ls>-ersda.
ENDLOOP.
```

Notas:

- `@` habilita _escaping_ para expresiones host (Open SQL moderno).
- `sy-subrc` es el código de retorno estándar.

# 4) Mostrar bonito: ALV rápido (CL_SALV_TABLE)

```abap
DATA lo_alv TYPE REF TO cl_salv_table.
cl_salv_table=>factory(
  IMPORTING r_salv_table = lo_alv
  CHANGING  t_table      = lt_mat ).
lo_alv->display( ).
```

Con esto obtienes ordenación, filtros y export a Excel sin esfuerzo.

# 5) Modulariza: formularios, métodos y funciones

Evita meter toda la lógica en un único bloque.

```abap
FORM cargar_datos USING    iv_mtart TYPE mtart
                  CHANGING ct_mat   TYPE STANDARD TABLE.
  SELECT matnr mtart ersda
    FROM mara
    INTO TABLE @ct_mat
    WHERE mtart = @iv_mtart
    UP TO 100 ROWS.
ENDFORM.
```

Orientado a objetos (recomendado):

```abap
CLASS lcl_repo DEFINITION.
  PUBLIC SECTION.
    METHODS get_by_type
      IMPORTING iv_mtart TYPE mtart
      EXPORTING et_mat   TYPE STANDARD TABLE OF ty_mat.
ENDCLASS.

CLASS lcl_repo IMPLEMENTATION.
  METHOD get_by_type.
    SELECT matnr mtart ersda
      FROM mara
      INTO TABLE @et_mat
      WHERE mtart = @iv_mtart.
  ENDMETHOD.
ENDCLASS.
```

# 6) Buenas prácticas actuales

- **Open SQL moderno** (uso de `@`, `INTO CORRESPONDING FIELDS OF TABLE`, `VALUE`, etc.).
- **ABAP OO** y pruebas unitarias con `ABAP Unit`.
- **CDS Views** y **OData** para exponer datos a Fiori.
- Evita `SELECT ... ENDSELECT` con I/O por iteración; usa `SELECT ... INTO TABLE`.

# 7) Ejercicio guiado (paso a paso)

1. Crea un **programa** Z en ADT o SE38.
2. Añade `PARAMETERS p_vkorg TYPE vkorg` (org. ventas).
3. Lee ventas de `VBAK` filtrando por `vkorg` (máx. 200 filas).
4. Muestra el resultado en **ALV**.
5. Extra: cuenta cuántos pedidos por **canal** (`VTWEG`) usando `GROUP BY`:
    
    ```abap
    SELECT vtweg, COUNT( * ) AS cnt
      FROM vbak
      WHERE vkorg = @p_vkorg
      GROUP BY vtweg
      INTO TABLE @DATA(lt_cnt).
    ```
    

# 8) Roadmap de aprendizaje en corto

1. Sintaxis base y tablas internas
2. Open SQL y rendimiento (seleccionar lo necesario)
3. ALV, mensajes, pantallas de selección
4. ABAP OO, excepciones y unit tests
5. CDS + OData + Fiori (lectura y servicios)
6. Ampliaciones: BAdIs, User‑Exits, Enhancements
7. Integración: RFCs, BAPIs, IDocs

# 9) ¿Seguimos?

Dime qué prefieres ahora:

- montar el **ALV** del ejercicio,
- crear una **vista CDS** simple,
- o ver cómo exponer datos como **servicio OData** para una app Fiori.