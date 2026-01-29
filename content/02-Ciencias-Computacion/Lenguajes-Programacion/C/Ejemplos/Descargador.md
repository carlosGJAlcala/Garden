---
title: "Descargador"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - c
---
Este código es un ejemplo de un **descargador paralelo** de archivos que descarga un archivo grande desde un servidor remoto, dividiéndolo en fragmentos para ser descargados por diferentes procesos en paralelo o de forma secuencial. Dependiendo de los parámetros de ejecución, el código puede descargar los fragmentos de forma **paralela** (varios procesos descargando al mismo tiempo) o **secuencial** (un proceso a la vez). Aquí te explico detalladamente cada parte del código.

### 1. **Inclusión de bibliotecas**

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-06-diseno-y-desarrollo-de-sistema|2025 03 06 diseno y desarrollo de sistema]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <sys/wait.h>
```
Estas bibliotecas permiten:
- **`unistd.h`**: Funciones como `fork()`, `exec()`, etc., necesarias para manejar procesos.
- **`stdlib.h`**: Proporciona funciones como `atoi()` para convertir cadenas a enteros.
- **`stdio.h`**: Para las funciones de entrada y salida, como `printf()`.
- **`sys/wait.h`**: Permite usar la función `wait()`, que se utiliza para que el proceso principal espere a que los procesos hijos terminen.

### 2. **Definición de constantes**
```c
#define TARGET_URL "http://212.128.69.216/lolo"
#define REMOTE_TARGET_SIZE_IN_BYTES 1047491658L
#define CHUNK_FILENAME_PREFIX "download"
```
- **`TARGET_URL`**: La URL desde la que se descargará el archivo.
- **`REMOTE_TARGET_SIZE_IN_BYTES`**: El tamaño total del archivo que se va a descargar (en bytes). En este caso, es un valor fijo de aproximadamente 1 GB.
- **`CHUNK_FILENAME_PREFIX`**: El prefijo para los nombres de los archivos fragmentados descargados.

### 3. **Funciones auxiliares**
#### 3.1 **`download_fragment()`**
```c
void download_fragment(char *url, long from, long to, char *outfile)
{
    char range[200];
    sprintf(range, "Range: bytes=%ld-%ld", from, to);
    printf("Testing %s\n", range);
    execlp("curl", "curl", "-s", "-H", range, url, "-o", outfile, NULL);
    perror("Error");
}
```
Esta función es responsable de descargar una parte del archivo usando **`curl`** con el encabezado HTTP `Range`, que le indica al servidor qué parte del archivo debe enviar.
- **`Range: bytes=from-to`**: Le dice a `curl` qué fragmento del archivo descargar.
- **`execlp("curl", "curl", "-s", "-H", range, url, "-o", outfile, NULL);`**: Ejecuta `curl` para descargar el fragmento en segundo plano. El `-s` hace que `curl` sea silencioso (no muestra la barra de progreso).
- **`perror("Error")`**: Si `execlp` falla, muestra un mensaje de error.

#### 3.2 **`are_arguments_correct()`**
```c
int are_arguments_correct(int argc, char *argv[])
{
    if (argc != 3)
    {
        printf("error: invalid number of arguments\n"
               "usage: %s processes {P/S} \n"
               "\tprocesses: number of download processes to fork \n"
               "\tdownload mode: (P) Parallel download (S) Sequential download\n",
               argv[0]);
        return 0;
    }
    char download_mode = argv[2][0];
    if (download_mode != 'P' && download_mode != 'S')
    {
        printf("error: invalid download mode. It has to be P or S\n");
        return 0;
    }
    int num_processes = atoi(argv[1]);
    if (num_processes <= 0)
    {
        printf("error: the number of processes has to be greater than 0\n");
        return 0;
    }
    return 1;
}
```
Esta función valida los argumentos de entrada:
- **`argc != 3`**: Verifica que haya exactamente tres argumentos: el número de procesos y el modo de descarga (P o S).
- **`argv[2]`**: Verifica que el modo de descarga sea `'P'` (paralelo) o `'S'` (secuencial).
- **`atoi(argv[1])`**: Convierte el número de procesos desde la cadena y verifica que sea mayor que 0.

### 4. **Función `main()`**
La función `main()` es el corazón del programa y maneja la lógica del proceso de descarga. Aquí es donde se configura todo y se manejan los procesos.

#### 4.1 **Inicialización de variables**
```c
int chunk_size;
int i;
long from, to;
int pid;
char outfile[20];
```
- **`chunk_size`**: Tamaño de cada fragmento que se descargará.
- **`from` y `to`**: Representan el rango de bytes que cada proceso descargará.
- **`pid`**: Identificador del proceso hijo.
- **`outfile`**: Nombre del archivo de salida para cada fragmento descargado.

#### 4.2 **Verificación de argumentos**
```c
if (!are_arguments_correct(argc, argv))
{
    return -1;
}
```
Verifica si los argumentos pasados a `main()` son correctos. Si no lo son, el programa termina.

#### 4.3 **Cálculo del tamaño de los fragmentos**
```c
int c = REMOTE_TARGET_SIZE_IN_BYTES / num_processes;
```
Calcula el tamaño de cada fragmento que se descargará, dividiendo el tamaño total del archivo entre el número de procesos.

#### 4.4 **Lógica de descarga por fragmentos**
```c
for (i = 1; i <= num_processes; i++)
{
    if (num_processes == 1)
    {
        from = 0;
        to = REMOTE_TARGET_SIZE_IN_BYTES;
    }
    else if (i < num_processes)
    {
        from = chunk_size * (i - 1);
        to = chunk_size * i - 1;
    }
    else
    {
        from = to + 1;
        to = REMOTE_TARGET_SIZE_IN_BYTES;
    }
```
Este bloque calcula los rangos de bytes para cada fragmento. Los procesos se distribuyen de la siguiente manera:
- **Si hay solo un proceso**, descargará todo el archivo.
- **Para otros casos**, se calculan los rangos de bytes que corresponden a cada proceso.

#### 4.5 **Creación de procesos hijos**
```c
pid = fork();
if (pid == 0)
{
    download_fragment(TARGET_URL, from, to, outfile);
    return (0);
}
```
- **`fork()`**: Crea un nuevo proceso hijo.
- Si el **`pid == 0`**, es el proceso hijo. Este proceso ejecutará la función `download_fragment()` para descargar su parte del archivo.

#### 4.6 **Modos de descarga: secuencial y paralelo**
```c
if (download_mode == 'S')
{
    if (pid != 0)
    {
        wait(NULL);  // El proceso padre espera que el hijo termine.
    }
}
```
Si el modo de descarga es **secuencial** (`S`), el proceso padre espera a que cada hijo termine antes de comenzar el siguiente.

```c
if (download_mode == 'P')
{
    if (pid != 0)
    {
        wait(NULL);  // El padre espera a que todos los hijos terminen.
    }
}
```
Si el modo de descarga es **paralelo** (`P`), el proceso padre espera a que todos los procesos hijos terminen antes de finalizar el programa.

### 5. **Explicación general del flujo del programa:**
1. El programa comienza verificando los argumentos pasados (número de procesos y modo de descarga).
2. Luego, calcula el tamaño de los fragmentos del archivo.
3. Para cada fragmento, crea un proceso hijo usando `fork()`. El proceso hijo descargará el fragmento correspondiente usando `curl` con un rango específico de bytes.
4. Dependiendo del modo de descarga:
   - En modo **secuencial**, el proceso principal espera a que cada proceso hijo termine antes de comenzar el siguiente.
   - En modo **paralelo**, el proceso principal espera a que todos los procesos hijos terminen antes de finalizar.

### Conclusión
Este programa permite descargar un archivo grande en fragmentos usando múltiples procesos. Utiliza **`fork()`** para crear procesos hijos que descargan cada fragmento usando **`curl`** con el encabezado **`Range`**. El programa soporta dos modos de descarga: secuencial y paralelo. En el modo secuencial, los fragmentos se descargan uno a la vez, mientras que en el modo paralelo, todos los fragmentos se descargan simultáneamente.