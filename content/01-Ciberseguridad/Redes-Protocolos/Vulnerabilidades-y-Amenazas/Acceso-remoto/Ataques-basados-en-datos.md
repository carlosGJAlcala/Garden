---
title: "Ataques Basados En Datos"
date: 2026-01-26
tags:
  - ciberseguridad
  - redes-protocolos
  - vulnerabilidades-y-amenazas
---
### Ataques basados en datos – Nota expandida


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/shellcode|shellcode]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Los **ataques basados en datos** son un conjunto de técnicas que **explotan la forma en que una aplicación procesa los datos que recibe**, en lugar de vulnerar directamente la infraestructura del sistema operativo o la red. Estos ataques se centran en **errores de programación, validación deficiente o uso inseguro de funciones estándar**.

Son extremadamente comunes y peligrosos, ya que permiten:

- **Ejecución de código arbitrario**.
    
- **Acceso a información sensible**.
    
- **Desbordamientos y corrupción de memoria**.
    
- **Compromiso total del sistema o aplicación**.
    

---

###  ¿Qué caracteriza un ataque basado en datos?

- El atacante **no necesita acceso previo** al sistema.
    
- Se aprovecha del **contenido del input**, no de la configuración del sistema.
    
- Puede lanzarse de forma **remota o local**.
    
- Suele implicar **inyección de datos** o manipulación de estructuras de memoria.
    

---

###  Tipos principales de ataques basados en datos

#### 1. **Errores de validación de entrada**

Aplicaciones que no verifican si los datos introducidos tienen el formato, longitud o contenido esperado.

 Ejemplo:  
Una aplicación espera un número y se le envía una cadena (`"abc"`), provocando un fallo de tipo o lógica.

 Consecuencias:

- Denegación de servicio (DoS).
    
- Escalada de privilegios.
    
- Ejecución de comandos arbitrarios.
    

---

#### 2. **Buffer overflow**

Cuando un dato sobrepasa el espacio asignado en memoria (como una cadena que no cabe en un buffer de 512 bytes).

 Código vulnerable:

```c
char buffer[512];
strcpy(buffer, input); // sin comprobar longitud
```

 Consecuencias:

- Se sobrescribe la **dirección de retorno** de la función.
    
- Se ejecuta código malicioso cargado en el buffer (shellcode).
    
- Vulnerabilidad crítica, especialmente en binarios SUID o servicios.
    

---

#### 3. **Format string vulnerabilities**

Uso inseguro de funciones como `printf()` en C/C++ cuando el formato de impresión es controlado por el usuario.

 Ejemplo:

```c
printf(user_input);  // ¡peligroso!
```

 Posibilidades:

- Volcado de memoria (`%x`, `%s`)
    
- Lectura/escritura arbitraria (`%n`)
    
- Ejecución de código si se manipulan punteros.
    

---

#### 4. **Integer overflows / underflows**

Errores al realizar operaciones con enteros, especialmente cuando se mezclan tipos con y sin signo o longitudes distintas.

 Ejemplo:

```c
if ((len1 + len2) > 256) return -1;
memcpy(buf, data1, len1);
memcpy(buf + len1, data2, len2);
```

 Riesgo:

- Si `len1 + len2` provoca un desbordamiento aritmético, puede eludir la validación y **escribir fuera de los límites del buffer**.
    

---

### ️ Consecuencias generales

- **DoS (Denegación de servicio)**: caídas de servicio o aplicación.
    
- **Información sensible expuesta**: volcados de memoria, variables de entorno, contraseñas.
    
- **Ejecución de código remoto o local**.
    
- **Escalada de privilegios**.
    
- **Persistencia en el sistema comprometido**.
    

---

### ️ Contramedidas para prevenir ataques basados en datos

#### En desarrollo seguro:

- Validar y sanear todas las entradas del usuario.
    
- Usar funciones seguras (`strncpy` en lugar de `strcpy`, `snprintf` en lugar de `sprintf`).
    
- Limitar y verificar los tamaños antes de operaciones de copia o cálculo.
    
- Usar herramientas como **ASan**, **Valgrind**, **fuzzers**.
    

#### A nivel de sistema operativo:

- **Stack canaries**: detectan desbordamientos antes de retornar.
    
- **DEP/NX (No-eXecute)**: evita ejecutar código en zonas de datos.
    
- **ASLR**: aleatoriza direcciones de memoria para dificultar explotación.
    
- **Fortify Source, StackGuard, FormatGuard**: protecciones en tiempo de compilación.
    

#### En auditoría y pentesting:

- Uso de herramientas como:
    
    - **Metasploit** para explotación de buffer overflows.
        
    - **AFL, LibFuzzer** para fuzzing.
        
    - **Checksec**, **Ghidra**, **radare2** para análisis binario.
        

---

###  Ejemplo práctico: Exploit PHF

Uno de los ataques más conocidos (1996):

```url
http://victima.com/cgi-bin/phf?Qalias=x%0a/bin/cat%20/etc/passwd
```

- El parámetro `Qalias` era insertado sin sanear en una llamada a `popen()`.
    
- `%0a` representa un salto de línea, lo que terminaba el comando original y ejecutaba uno nuevo.
    
- El atacante podía leer el contenido de `/etc/passwd` y acceder a otros archivos.
    

---

### Conclusión

Los **ataques basados en datos son silenciosos, potentes y muy comunes**. No requieren explotación del sistema operativo en sí, sino que aprovechan errores en el desarrollo de software. Por eso, tanto en desarrollo como en defensa, es crítico **adoptar buenas prácticas de codificación, hacer pruebas de robustez y revisar el código y las bibliotecas empleadas**.

---

¿