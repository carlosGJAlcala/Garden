---
title: "Snort - Sistema de Detección de Intrusiones"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - ids-ips
---

# Snort - Sistema de Detección de Intrusiones


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

> **Alternativas**: [[suricata|Suricata]] (más rápido, multihilo), [[ZEEK|Zeek]] (análisis de protocolo). Ver [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|Splunk]] para correlación de logs. Ver también [[Instalacion-y-Configuracion-de-Splunk-Universal-Forwarder-con-Snort-en-Windows-y-Ubuntu|Integración Snort+Splunk]].

# INSTALACIÓN

La instalación se ha realizado en el sistema operativo Ubuntu, que se ejecuta de forma dual con Windows y no en una máquina virtual.

Se han utilizado los siguientes comandos para su configuración:

Primero, he usado *ipconfig* para ver la IP y poder observar la interfaz de red y la dirección IP.

Luego, establecemos el comando para poner la tarjeta de red en modo promiscuo:

*sudo ip link set wlo1 promisc on*

![[Pasted image 20241028233419.png]]

He instalado "Snort v3". Para instalar Snort, utilicé el siguiente comando:

*sudo apt install snort -y*

También usé el siguiente comando para instalar DAQ.

Descargué libdaq:

*git clone [https://github.com/snort3/libdaq.git](https://github.com/snort3/libdaq.git)* 

El DAQ es el encargado de recoger los paquetes de red y formatearlos para que Snort los pueda procesar.

![[Pasted image 20241029131453.png]]

También es necesario crear el archivo `libdaq3.conf` con el siguiente texto, para indicarle a Snort dónde se aloja el DAQ descargado en “/usr/local/lib/daq-s3/lib”. Para ello, puedes usar el siguiente comando:

*echo "usr/local/lib/daq-s3/lib" >> /etc/ld.so.conf/etc/libdaq3.conf*

También hay que crear una subcarpeta dentro de la carpeta `log` para que Snort pueda guardar los registros. La ruta debe ser:

*/var/log/snort*

![[Pasted image 20241030101002.png]]

Una vez hecho esto, comprobamos que se ejecuta correctamente usando el siguiente comando:

*sudo snort -q -A console --daq-dir /usr/local/lib/daq/ -c /etc/snort/snort.conf -i wlo1*

Los parámetros que permite Snort son los siguientes:

- `-q`: no muestra demasiada información (quick).
- `-v`: como en tcpdump, muestra los paquetes recibidos en pantalla.
- `-A console`: muestra todas las alertas en la consola.
- `--daq-dir`: directorio donde tenemos instalados los módulos DAQ.
- `-c`: ruta al archivo de configuración de Snort.
- `-i`: interfaz de red que se utiliza para Snort.

![[Pasted image 20241029125820.png]]
![[Pasted image 20241029125832.png]]

Para realizar pruebas y verificar que funciona correctamente, comenté las reglas que vienen por defecto en el directorio `/etc/snort/snort.conf` y creé dos reglas.

![[Pasted image 20241029131123.png]]

También se deben comentar las siguientes líneas:

![[Pasted image 20241029131209.png]]
![[Pasted image 20241029131240.png]]

Una vez que hemos comprobado que funciona perfectamente, vamos a probar a usar un preprocesador. En este caso, utilizaremos el preprocesador `frag3`, que se encarga de ensamblar paquetes que son demasiado grandes.

![[Pasted image 20241030111241.png]]

La primera línea indica cuántos paquetes fragmentados almacena. En caso de que esté muy fragmentado, utilizamos el siguiente comando `prealloc_memcap`.

# Reglas

Vamos a configurar cinco reglas. Primero, descomentamos la línea de `local.rules`.

![[Pasted-image-20241030112234.png]]
![[Pasted image 20241030112345.png]]

Las reglas que creamos antes las borramos y las subimos en el archivo `local.rules` para tenerlas mejor organizadas.

Las reglas configuradas en el archivo `local.rules` son las siguientes:

He creado las dos primeras para comprobar que Snort funciona correctamente; las siguientes son para detectar inyecciones SQL y `path traversal`, y por último descargué, desde el siguiente enlace, reglas para detectar ataques de denegación de servicio y el `ping de la muerte` (link: https://github.com/maj0rmil4d/snort-ddos-mitigation/blob/main/dos.rules).

El archivo queda de la siguiente manera:

![[Pasted image 20241104132132.png]]

Me ha llamado la atención el concepto `ping de la muerte`, que es un ping de tamaño muy grande que excede el búfer y provoca errores en el sistema de destino.

Ejecutamos el siguiente comando y comprobamos que Snort se ejecuta correctamente:

*sudo snort -q -A console --daq-dir /usr/local/lib/daq/ -c /etc/snort/snort.conf -i wlo1*

![[Pasted image 20241030130236.png]]

# Probar las reglas

La primera y segunda reglas han sido probadas:

Serían las siguientes reglas, y las pruebas están en capturas anteriores.

```plaintext
alert udp any any -> any any (msg:"Es un paquete increíble UDP"; sid:1000000;)
alert icmp any any -> any any (msg:"Mira, esto es un ping"; sid:1000001; rev:1; content:"1234567";)
```

También podemos usar Snorpy para crear reglas.

![[snorpy.png]]

La regla de `path traversal` se ejecuta correctamente. Para hacer la prueba, utilicé `curl`.

![[culpahttraversal.png]]
![[pathtraversal.png]]

La configuración de la alerta es la siguiente:

```plaintext
alert tcp any any -> any any (msg:"Detectar path traversal"; content:"GET"; http_method; pcre:"/(\/\.)*/"; sid:1000003;)
```

Hemos utilizado `pcre`, en el cual se pueden usar expresiones regulares. Para poder escapar caracteres especiales, se utiliza `/`.

Al hacer un `curl` con una ruta que no existe, nos devuelve un `404`:

![[Pasted image 20241104120429.png]]

Lo cual hace que se active la regla de que no se ha encontrado el servicio:

```plaintext
alert tcp any any -> any any (msg:"No se encuentra el servicio"; content:"404"; http_stat_code; sid:1000007;)
```

![[Pasted image 20241104120543.png]]

Implementamos una regla para detectar SQLi.

La regla es la siguiente:

```plaintext
alert tcp any any -> any any (msg:"SQL INJECTION"; content:"GET"; http_method; pcre:"/.*UNION.+SELECT.*/"; pcre:"/.*1=1.*/"; pcre:"/SELECT.+FROM/"; sid:1000004;)
```

Para probarla, ejecutamos un `curl`.

![[Pasted image 20241104125958.png]]
Y el resultado en Snort.

![[Pasted image 20241104125728.png]]

![[Pasted image 20241104131306.png]]

La siguiente regla sirve para detectar si se está buscando contenido malicioso:

```plaintext
alert tcp any any -> any any (msg:"Búsqueda de contenido malicioso"; content:"GET"; http_method; content:"hacking"; http_uri; sid:1000005;)
```

![[Pasted image 20241104131727.png]]
![[Pasted image 20241104131230.png]]

También podemos implementar reglas de terceros, como en este caso, para detectar ataques de DDoS. Probamos un ataque de denegación de servicio usando `hping3`.

![[Pasted image 20241030164913.png]]

El archivo de configuración de reglas locales queda de la siguiente manera:

![[Pasted image 20241104132121.png]]

--- 

para bajar reglas podemos usar emergency 