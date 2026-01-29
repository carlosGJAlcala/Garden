---
title: "Zeek - Monitor de Seguridad de Red"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - ids-ips
---

# Zeek - Monitor de Seguridad de Red


> **Relacionado**: [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

> **Alternativas**: [[SNORT|Snort]] y [[suricata|Suricata]] (basados en firmas). Zeek se enfoca en análisis de protocolo y generación de logs detallados. Ver [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|Splunk]] para correlación de logs.

# INSTALACIÓN

Hacemos una descarga del repositorio de Git de Zeek:  
`git clone --recursive https://github.com/zeek/zeek`  
La opción `--recursive` es para que instale todos los submódulos.  

Accedo al subdirectorio:  
`cd zeek`  
Ejecuto `./configure` y luego `make` para poder compilar el programa e instalarlo.

En mi caso, me ha dado error al hacer el `./configure`, dando el siguiente error:  
![[Pasted image 20241114174604.png]]  
Para arreglarlo, comprobamos si tenemos instalado **swig**, que funciona como un compilador cruzado para comunicar diferentes lenguajes. En el caso de que lo tengamos instalado y salga este error, actualizamos **swig** haciendo un `sudo apt-get upgrade swig`. Si no lo tenemos, ejecutamos:  
`sudo apt-get install swig`.

Hacemos un `make` y luego:  
`sudo make install`.

Una vez instalado:  
Ejecutamos el siguiente comando:  
`/usr/local/zeek/bin/zeek -v`  
y nos muestra la versión.

![[Pasted image 20241114223636.png]]  
Le decimos qué interfaz de red usar:  
![[Pasted-image-20241114225623.png]]  

Ejecutamos el siguiente comando para que instale la configuración y arranque el servicio:  
![[Pasted-image-20241114225756.png]]  

Si nos metemos en el fichero de los logs, podemos ver que funciona correctamente:  
![[Pasted-image-20241114230236.png]]  

Ahora procederemos a crear un script para que recoja el tráfico de forma personalizada. Los scripts se crean en el siguiente directorio:  
`/usr/local/zeek/share/zeek/site/`  

Creamos el siguiente:  
![[Pasted-image-20241114231243.png]]  
Lo hemos llamado de la siguiente forma:  
![[Pasted-image-20241114231508.png]]  

En el fichero `local.zeek` cargamos nuestro script de la siguiente forma:  
![[Pasted-image-20241114231731.png]]  

Reiniciamos el servicio:  
![[Pasted-image-20241114231921.png]]  

Al ejecutar un `curl` a Google vemos que se refleja en nuestros logs:  
![[Pasted-image-20241114232307.png]]  

