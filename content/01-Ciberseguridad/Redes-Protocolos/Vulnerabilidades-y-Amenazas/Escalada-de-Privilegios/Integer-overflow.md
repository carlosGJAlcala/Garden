---
title: "whoami"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Escalada de privilegios mediante Integer Overflow – Nota técnica completa


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/shellcode|shellcode]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/Escalada-de-Privilegios/Escalada-de-Privilegios|Escalada de Privilegios]].

Un **integer overflow (desbordamiento de enteros)** ocurre cuando una operación aritmética produce un valor **fuera del rango permitido por su tipo de dato**. Por ejemplo, si un entero de 32 bits sin signo (`unsigned int`) almacena un número mayor que `2³² - 1`, "vuelve a cero" y empieza desde el principio.

Un atacante puede **aprovechar este comportamiento para evadir validaciones de seguridad** y provocar acciones inesperadas, como **escrituras fuera de límites, bypass de controles, ejecución de código y escalada de privilegios**.

---

##  ¿Cómo se escala con Integer Overflow?

Se escala privilegios cuando el overflow:

- Permite **escribir en memoria privilegiada** (como `/etc/passwd`, buffers del kernel, punteros de funciones).
    
- **Engaña validaciones** del sistema que revisan tamaños, límites o rangos.
    
- Se encuentra en **programas SUID root** que luego ejecutan acciones privilegiadas con datos manipulados.
    

---

##  Ejemplo práctico: overflow al calcular tamaño de buffer

###  Código vulnerable

```c
int copiar_datos(char *buf1, char *buf2, unsigned int len1, unsigned int len2) {
    char buffer[256];
    if ((len1 + len2) > 256) {
        return -1;
    }
    memcpy(buffer, buf1, len1);
    memcpy(buffer + len1, buf2, len2);
    return 0;
}
```

###  El fallo

El atacante pasa:

```c
len1 = 0xFFFFFFF0;   // valor muy grande
len2 = 0x00000020;   // 32

// len1 + len2 = 0x100000010  => truncado a 0x10 = 16 (!)
```

 Resultado: pasa el `if`, pero `memcpy` escribe más allá del buffer.

###  Consecuencia

- Puede sobrescribir variables sensibles, punteros de retorno, estructuras del stack.
    
- Si el programa tiene privilegios elevados (SUID), esta escritura **modifica el control de flujo del programa** y permite ejecución de shellcode → **root shell**.
    

---

##  Otro ejemplo: kernel integer overflow (real)

### CVE-2008-0600 – Escalada a root

- Vulnerabilidad en el kernel Linux 2.6.17–2.6.24.
    
- Un `integer signedness bug` en `vmsplice()` permitía a un usuario sin privilegios **escribir en memoria del kernel**.
    
- Resultado: **escalada directa a root sin necesidad de credenciales**.
    

Exploit real: [`exploit-db 5092`](https://www.exploit-db.com/exploits/5092)

```bash
gcc -o r00t exploit.c
./r00t
# whoami
root
```

---

##  Otras formas de explotar integer overflows

|Técnica|Impacto|
|---|---|
|**Bypass de validación**|Se elude un `if` de seguridad que depende de un cálculo con enteros.|
|**Desbordamiento de buffer**|Se calcula mal el tamaño de un buffer o un desplazamiento.|
|**Escritura en memoria crítica**|Se puede modificar punteros, direcciones de retorno, estructuras privilegiadas.|
|**Kernel / Driver**|Si ocurre en código del kernel, puede modificar estructuras del SO.|
|**Archivos manipulados**|Muchos formatos (ZIP, imágenes, PDF) incluyen campos numéricos que al desbordar permiten ejecución remota o local.|

---

## ️ Contramedidas

|Nivel|Acción|
|---|---|
|**Código**|Validar explícitamente que no haya overflow: `if (len1 > MAX - len2)`.|
|**Compilación**|Usar `-ftrapv` o `-fsanitize=undefined` para detectar desbordamientos.|
|**Sistemas**|Usar stack canaries, DEP/NX, ASLR para dificultar explotación.|
|**Auditoría**|Buscar funciones que hagan operaciones con entrada externa: `malloc(len1 + len2)`, `memcpy`, etc.|
|**Análisis estático**|Herramientas como **Coverity**, **cppcheck**, **clang static analyzer**.|

---

##  Conclusión

La escalada de privilegios mediante **integer overflow** ocurre cuando una variable controlada por el atacante desborda un límite interno, y el sistema **toma decisiones incorrectas de seguridad** (por ejemplo, permitir escritura en zonas privilegiadas). Si el código vulnerable pertenece a un binario con privilegios (como SUID root o kernel), puede derivar en **una shell de root directa**.

Estos errores son **difíciles de detectar manualmente**, pero muy peligrosos, especialmente en software heredado, controladores, firmware o código en C/C++ sin protecciones.

---