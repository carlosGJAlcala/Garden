Voy a ayudarte a formatear y estructurar tu código, además de proporcionar las respuestas a las preguntas de las vulnerabilidades, las recomendaciones y cómo solucionar el problema.

### 1. **Código original (con vulnerabilidad de stack overflow)**:

El código original tiene una vulnerabilidad de **desbordamiento de pila (stack overflow)**. Esta vulnerabilidad ocurre porque se usa la función **`strcpy`**, que no comprueba si el tamaño del buffer es suficiente para almacenar el contenido de la cadena que se le pasa como argumento.

```c
#pragma check_stack(off)
#include <string.h>
#include <stdio.h>

void foo(const char* input)
{
    char buf[10];  // Buffer pequeño de solo 10 bytes.
    printf("My stack looks like:\n%p\n%p\n%p\n%p\n%p\n%p\n\n");
    strcpy(buf, input);  // Aquí puede ocurrir un desbordamiento si input es más grande que 10 bytes.
    printf("%s\n", buf);
    printf("Now the stack looks like:\n%p\n%p\n%p\n%p\n%p\n%p\n\n");
}

void bar(void)
{
    printf("Augh! I've been hacked!\n");
}

int main(int argc, char* argv[])
{
    // Impresión de las direcciones de las funciones foo y bar
    printf("Address of foo = %p\n", foo);
    printf("Address of bar = %p\n", bar);

    if (argc != 2)
    {
        printf("Please supply a string as an argument!\n");
        return -1;
    }

    foo(argv[1]);  // Llamada a foo con el argumento proporcionado
    return 0;
}
```

#### **Vulnerabilidades detectadas:**
- **Stack Overflow**: Usar `strcpy` sin comprobar que el tamaño del buffer es suficiente para almacenar los datos es un riesgo de **desbordamiento de pila**. Si el argumento `input` tiene más de 10 caracteres, sobrescribirá la memoria adyacente, lo que podría permitir la ejecución de código malicioso.
  
#### **Recomendaciones de RATS para solucionar las vulnerabilidades:**
- Utilizar funciones de manipulación de cadenas seguras que limiten el tamaño de los datos copiados al buffer, como `strncpy`, `snprintf` o `strlcpy`.
- Validar los tamaños de entrada antes de copiarlos en buffers para evitar desbordamientos.
  a) ¿Qué vulnerabilidades se detectan en este código?
hemos detectado un stack overflow 
![[practica1_old.png]]

---

### 2. **Código solucionado (sin vulnerabilidad de stack overflow):**

A continuación, te muestro el código corregido para evitar el desbordamiento de pila utilizando una función segura (`strlcpy`) y verificando el puntero de entrada:

```c
#include <string.h>
#include <stdio.h>

#define tamanio 10  // Definir un tamaño adecuado para el buffer

char buf[tamanio];  // Buffer de tamaño 10

void foo(const char* input)
{
    // Verificar si el puntero de entrada es NULL
    if (input == NULL) {
        fprintf(stderr, "Input is NULL!\n");
        return;
    }

    printf("My stack looks like:\n%p\n%p\n%p\n%p\n%p\n%p\n\n");
    
    // Usar strlcpy para evitar desbordamiento de buffer
    strlcpy(buf, input, sizeof(buf) - 1);  // Copiar seguro, limitando el tamaño
    printf("%s\n", buf);

    printf("Now the stack looks like:\n%p\n%p\n%p\n%p\n%p\n%p\n\n");
}

void bar(void)
{
    printf("Augh! I've been hacked!\n");
}

int main(int argc, char* argv[])
{
    // Blatant cheating to make life easier on myself
    printf("Address of foo = %p\n", foo);
    printf("Address of bar = %p\n", bar);

    if (argc != 2)
    {
        printf("Please supply a string as an argument!\n");
        return -1;
    }

    foo(argv[1]);  // Llamar a foo con el argumento proporcionado
    return 0;
}
```

#### **Cambios realizados**:
1. **Uso de `strlcpy`**: Esta función asegura que el número de caracteres copiados no exceda el tamaño del buffer. En lugar de usar `strcpy`, que no tiene control sobre el tamaño, `strlcpy` limita la copia al tamaño del buffer disponible, evitando desbordamientos de pila.
  
2. **Comprobación de puntero NULL**: Se agrega una comprobación para asegurarse de que `input` no sea `NULL`, lo que evitaría un posible fallo por acceso a memoria nula.
![[Pasted image 20241117121406.png]]
---

### 3. **Código vulnerable relacionado con TOCTOU (Time of Check to Time of Use)**:

El segundo código está relacionado con una vulnerabilidad de tipo **TOCTOU (Time of Check to Time of Use)**, que ocurre cuando hay una diferencia de tiempo entre la comprobación de una condición y el uso posterior de los resultados de esa comprobación.

En este caso, el código intenta abrir un archivo de manera atómica usando `open` con `O_EXCL`, pero no garantiza que el archivo no haya sido modificado entre el momento de la comprobación y la operación. Esto podría permitir a un atacante modificar el archivo durante el proceso.

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <errno.h>

void fopen_with_toctou(const char *file)
{
    // Intentar crear el archivo de manera atómica
    int fd = open(file, O_WRONLY | O_CREAT | O_EXCL, 0644);
    if (fd == -1)
    {
        // Manejar errores, como si el archivo ya existe u otros problemas
        if (errno == EEXIST)
        {
            fprintf(stderr, "File already exists: %s\n", file);
        }
        else
        {
            perror("Error creating file");
        }
        return;
    }

    // Cerrar el descriptor de archivo
    if (close(fd) == -1)
    {
        perror("Error closing file");
    }
}
```

#### **Vulnerabilidad TOCTOU**:
El código está sujeto a una condición de carrera, ya que un atacante podría crear el archivo entre la comprobación de si existe (`open` con `O_EXCL`) y el momento en que se usa el archivo (cuando se escribe en él).

#### **Solución**:
Una forma de prevenir TOCTOU es usar funciones que aseguren el acceso y modificación del archivo de forma atómica, o bien realizar una validación más rigurosa.

---

### 4. **Resultado después de la corrección:**

#### Antes de la corrección (con vulnerabilidad):

- **Resultado del análisis de seguridad**: El código presenta vulnerabilidades como **stack overflow** y problemas de manejo de archivos (TOCTOU), lo cual puede comprometer la seguridad de la aplicación.
  
#### Después de la corrección (sin vulnerabilidad):

- **Resultado del análisis de seguridad**: Las vulnerabilidades han sido corregidas. El uso de `strlcpy` elimina el desbordamiento de pila, y la validación del puntero NULL mejora la estabilidad. Sin embargo, para evitar el problema TOCTOU, es necesario considerar otras soluciones como el uso de técnicas para garantizar un acceso de archivo atómico.

---

Si necesitas más detalles sobre cómo implementar otras soluciones de seguridad o análisis de vulnerabilidades, no dudes en preguntar. ¡Estoy aquí para ayudarte!