---
title: "Comandos Utiles De Vim"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---


## Modos en Vim


> **Relacionado**: [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]].

- **Modo Normal**: Comienza en este modo. Úsalo para navegar y manipular texto.
- **Modo de Inserción**: Para escribir o insertar texto.
    - `i`: Inserta en el cursor.
    - `I`: Inserta al inicio de la línea.
    - `a`: Inserta después del cursor.
    - `A`: Inserta al final de la línea.
- **Modo Visual**: Para seleccionar texto.
    - `v`: Selección de caracteres.
    - `V`: Selección de línea completa.
    - `Ctrl+v`: Selección en bloque.
- **Modo de Línea de Comando**: Para comandos específicos como guardar o salir.
    - `:`: Entra en el modo de línea de comandos.

---

## Navegación en Vim

- `h`, `j`, `k`, `l`: Mover el cursor a la izquierda, abajo, arriba y derecha.
- `w`: Ir al comienzo de la siguiente palabra.
- `b`: Ir al comienzo de la palabra anterior.
- `0`: Ir al comienzo de la línea.
- `$`: Ir al final de la línea.
- `gg`: Ir al inicio del documento.
- `G`: Ir al final del documento.

---

## Manipulación de Texto

- **Copiar y Pegar**:
    
    - `yy`: Copia la línea actual.
    - `yw`: Copia la palabra bajo el cursor.
    - `y$`: Copia desde el cursor hasta el final de la línea.
    - `p`: Pega después del cursor.
    - `P`: Pega antes del cursor.
- **Borrar y Cortar**:
    
    - `x`: Borra el carácter bajo el cursor.
    - `dd`: Borra la línea actual.
    - `dw`: Borra la palabra bajo el cursor.
    - `D`: Borra desde el cursor hasta el final de la línea.
- **Deshacer y Rehacer**:
    
    - `u`: Deshacer la última acción.
    - `Ctrl+r`: Rehacer la última acción.

---

## Comandos de Búsqueda y Reemplazo

- `/texto`: Buscar `texto` en el documento.
- `?texto`: Buscar `texto` hacia atrás en el documento.
- `n`: Ir a la siguiente coincidencia.
- `N`: Ir a la coincidencia anterior.
- `:%s/viejo/nuevo/g`: Reemplazar todas las ocurrencias de "viejo" por "nuevo".

---

## Guardar y Salir

- `:w`: Guardar el archivo.
- `:q`: Salir de Vim.
- `:wq`: Guardar y salir.
- `:q!`: Salir sin guardar.

---

## División de Ventanas

- `:split`: Dividir la ventana horizontalmente.
- `:vsplit`: Dividir la ventana verticalmente.
- `Ctrl+w, h/j/k/l`: Moverse entre ventanas (izquierda, abajo, arriba, derecha).

---

## Comandos Avanzados

- **Bloque Visual**:
    
    - `Ctrl+v` + seleccionar texto + `I` + `<texto>` + `Esc`: Insertar en múltiples líneas.
- **Ejecutar Comandos de Shell**:
    
    - `:!comando`: Ejecuta un comando de terminal, por ejemplo, `:!ls` para listar archivos.
- **Comandos Externos en el Documento**:
    
    - `:r !comando`: Inserta la salida de un comando en el documento, como `:r !date` para insertar la fecha actual