---
title: "Laboratorio 2 Volatility"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---



> **Relacionado**: [[01-Ciberseguridad/Fundamentos/shellcode|shellcode]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/VirusTotal|VirusTotal]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

1. Analice el fichero con la imagen de memoria wxp.vmem, utilizando

los comandos correspondientes de volatility y responda:

a) Número total y listado de procesos (indicando si observa alguno sospechoso) y su

relación con otros.

**wxp.vmem**

Ejecutamos el siguiente comando y para obtener el número de líneas concatenamos su salido  
usando un pipe y utilizar el wc -l para contar las líneas

```
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.pslist
```

```
Ilustración 1 pslist
```

En la anterior imagen podemos observar el listado de proceso que son 34.

Si queremos ver la relación de unos con otros podemos usar el pstree que relaciona el  
proceso padre con sus hijos:

```
Ilustración 2 pstree
```

```
Ilustración 3 pstree
```

De los procesos que podemos ver, el que podemos considerar sospechoso es el  
relacionado con el explorer.exe ya que tiene de número de handles (el numero  
relacionado con los ficheros y los puertos) bastante alto. También vemos que este  
proceso tiene varios procesos hijos y uno de ellos es un cmd, puede ser que el  
explorador de carpetas esté troyenizado.

b) Número total y listado de conexiones (y procesos asociados a cada conexión).  
Ejecutamos el siguiente comando y hacemos lo mismo para mirar el número de líneas:  
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.netstat.NetStat

```
Ilustración 4 NetStat
```

Al ejecutarlo sale que no encuentra un fichero disponible para ver el tema de  
conexiones.

c) Número de dlls.  
**wxp.vmem**

```
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.dlllist.DllList
```

```
Ilustración 5 dlllist
```

Como podemos ver hay 1311 ficheros dll.

d) Número de ficheros.  
**wxp.vmem**

Para ver el número de ficheros usamos lo mismo ejecutamos el siguiente comando y lo  
concatenamos con wc -l.

```
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.filescan.FileScan
```

```
Ilustración 6 FileScan
```

En la imagen anterior salen que hay 1125 ficheros.

e) Número de variables de entorno.  
**wxp.vmem**  
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.envars.Envars

```
Ilustración 7 Envars
```

El número de variables en total son 545.

f) Número de servicios registrados.

Para ver los servicios registrados utilizamos el siguiente comando y lo concatenamos  
con wc -l  
python3 vol.py -f /home/carlos/Descargas/pruebamem/wxp.vmem windows.svcscan.SvcScan

```
Ilustración 8 SvcScan
```

El número de los servicios registrados como se puede observar en la captura anterior  
es de 245.

g) Con las verificaciones realizadas anteriormente ¿se podría identificar algún código  
malicioso?

Si funcionase correctamente el listado de puertos de la aplicación podríamos

comprobar que aplicaciones tienes conexiones abiertas y poder intuir si en alguna de  
las aplicaciones ejecutándose tiene una shellcode que abre una reverse Shell. Con el

pstree podemos intuir si hay algún código malicioso, pero no es suficiente para poder  
asegurarnos de ello, en la siguiente parte con el subcomando malfind podremos

encontrar más información sobre los procesos que se están ejecutando y con su hash

podemos averiguar en virus total si se trata de un virus.

Parte 2. Análisis de malware

Analice la imagen de memoria cridex.vmem utilizando el comando malfind e intente

averiguar lo máximo que pueda sobre los ficheros ejecutables maliciosos: procesos,  
tipo de malware, ficheros infectados.  
Utilizamos el comando malfind para buscar segmentos de memoria que contienen  
código ejecutable, el cual se basa en características como la etiqueta VAD (Virtual  
Address Descriptor) y los permisos de página.

El filtro grep –C 5 ‘MZ’ nos permite buscar la cadena "MZ" (que es el encabezado de un  
archivo ejecutable en Windows) y muestra 5 líneas de contexto antes y después de cada  
coincidencia.

Para ello ejecutamos el siguiente comando:

```
vol.py -f /home/alejandra/downloads/cridex.vmem windows.malfind
```

```
Ilustración 9 Malfind búsqueda de ejecutables 1 cridex
```

```
Ilustración 10 Malfind búsqueda de ejecutables 2 cridex
```

```
Ilustración 11 Malfind búsqueda de ejecutables 3 cridex
```

Posteriormente guardamos copias de los segmentos de memoria identificados por el  
comando malfind.

```
Ilustración 12 Guardar copias de los segmentos de memoria cridex
```

Analizamos cada fichero en la página de virus total y recamos en la siguiente imagen el  
fichero en el que detectó virus.

```
Ilustración 13 Ficheros de salida cridex
```

En el resultado de virus total lo podemos observar en la siguiente imagen, donde 9 de los  
motores antivirus que participan en VirusTotal han encontrado que el archivo contiene  
código malicioso.

```
Ilustración 14 Resultado VirusTotal cargando el fichero cridex
```

Con el siguiente comando podemos extraer los hashes de los ficheros para luego  
comprobarlos en virus total:

```
certutil -hashfile “nombre de fichero”
```

```
Ilustración 15 Generando el MD5 del fichero infectado cridex
```

Generamos el fichero MD5 del fichero infectado para verificar que colocando este hash  
nos proporciona el mismo resultado.

```
Ilustración 16 VirusTotal mediante hash cridex
```

Complete el análisis de wxp.vmem, ahora utilizando malfind en busca de malware e  
intente averiguar lo máximo que pueda sobre los ficheros ejecutables maliciosos:

procesos, tipo de malware, ficheros infectados, etc.  
Repetimos el proceso anterior para el archivo wxp.vmem

```
Ilustración 17 grep –C 5 ‘MZ’ wxp 1
```

- Ilustración 18 grep –C 5 ‘MZ’ wxp
- Ilustración 19 grep –C 5 ‘MZ’ wxp
    - Ilustración 20 grep –C 5 ‘MZ’ wxp

```
Ilustración 21 grep –C 5 ‘MZ’ exp 5
```

```
Ilustración 22 grep –C 5 ‘MZ’ wxp 6
```

Procedemos a guardar los segmentos de memoria para analizarlos en VirusTotal.

```
Ilustración 23 malfind –d wxp
```

```
Ilustración 24 ficheros generados wxp
```

Vamos cargando uno por uno los archivos para identificar cual es el que contiene  
malware.

Como se puede observar en la siguiente imagen algunos de los archivos nos arrojaron el  
resultado “virus no detectado”

```
Ilustración 25 virus total
```

Hasta que encontramos el archivo que nos dio positivo “pid.17.vad.0x36e0000-  
0x3776fff.dmp” donde 52 motores de busqueda lo detectaron como un trojano zusy  
caphaw, como se puede observar en la siguiente imagen.

```
Ilustración 26 resultado VirusTotal fichero wxp
```

Este proceso de búsqueda también se puede realizar calculando su hash MD5 y luego  
buscándolo en virus total, lo que nos devuelve el mismo resultado.

```
Ilustración 27 Generando el MD5 wxp
```

```
Ilustración 28 resultado en VirusTotal por Hash
```

Parte 3. Parte opcional. Generación de archivo vmem

Explique el procedimiento que debería seguir para obtener este volcado de memoria de

una máquina virtual propia.  
Para la creación del volcado de memoria hemos utilizado Oracle virtual boxPrimero  
encendemos la máquina que en nuestro caso es una Kali Linux, no he ejecutado ningún  
programa de momento y para generar el volcado de memoria Ram

Y ejecutamos el siguiente comando:

```
C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" list vms
```

```
VBoxManage.exe debugvm "Kali" dumpvmcore --filename="C:\prueba\test.elf"
```

“Kali”: es el nombre de nuestra máquina.

Importante no poner la ruta relativa en filename o indicarle solo el nombre del archive ya  
que dará error.

Al ejecutarlo generará la siguiente imagen como se puede observer a generado un  
volcado de unas 8 gb de Ram que coincide con la ram que le hemos ajustado a la  
máquina:

_Ilustración 29 Resutado_

**Compruebe si puede realizar el análisis posterior de forma análogo a los  
apartados anteriores.**

¿Podría obtener esta información desde una máquina física (total o parcialmente)?  
Desarrolle la respuesta.  
Si que se puede hacer en el caso de sistemas linux se puede crear una copia utilizando  
dd del directorio /dev/mem que es donde está guardada la memoria ram y luego se  
puede analizar utilizando volatility tambien se puede utilizar LiME que trabaja a nivel de  
kernel del sistema operativo y es la opcion más rápida.  
Cuando generamos un volcado de memoria este archivo pesa lo mismo que la memoria  
RAM.

Lo intentamos hacer con dd porque así no hay que instalar programas terceros:

```
sudo dd if=/dev/mem of=volcado.mem bs=1M
```

```
Ilustración 30 comando dd
```

Pero al ejecutarlo como se puede ver en la imagen surge error ya que es una operación  
no permitida , para solucionarlo podemos ejecutar LiME que se ejecuta a nivel de  
Kernel.

Otra opción es utilizar FTK Imager como podemos ver en la siguiente imagen:

```
Ilustración 31 Captura de imagen mem
```

Y al pasarla en volatility podemos analizar como hacemos a continuación:

```
Ilustración 32 windows.pslist
```

```
Ilustración 33 windows.netsat
```