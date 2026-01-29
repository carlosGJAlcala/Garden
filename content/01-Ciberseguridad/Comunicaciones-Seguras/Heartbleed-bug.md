---
title: "Detalles técnicos"
date: 2026-01-26
tags:
  - ciberseguridad
  - comunicaciones-seguras
---

# Detalles técnicos


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[07-Investigacion/Cuantica/bibliografia/biblio|biblio]]. [[02-Ciencias-Computacion/Algoritmos-EEDD/Estructuras/Puntero|Puntero]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]].

## Introducción

Correspondiente al siguiente CVE code: CVE-2014-0160, con un CVScore de 7.5, es una vulnerabilidad en el protocolo TLS de [[OpenSSL]] en la cual se podía explotar código a través de un _buffer overflow_ en la entrada de los datos. Este bug fue liberado en el 2012, descubierto el 1 de abril de 2014 y solventado el 7 de ese mismo mes.

Esta vulnerabilidad era un agujero de seguridad en el código de OpenSSL en la versión 1.0.1, permitiendo leer la memoria del servidor por lo anteriormente dicho. Además, no dejaba pruebas sobre el ataque, por lo cual los investigadores fueron muy poco optimistas, ya que con este ataque se podían omitir todas las protecciones de TLS. Según los propios investigadores: "Nos atacamos desde afuera, sin dejar rastro", escribieron. "Sin utilizar ninguna información privilegiada o credenciales, pudimos robarnos las claves secretas utilizadas para nuestros certificados X.509, nombres de usuario y contraseñas, mensajes instantáneos, correos electrónicos y documentos críticos de negocios y comunicación."

A continuación, detallaremos cómo funciona dicha vulnerabilidad y cómo fue pasada por alto.

# Detalles técnicos

Para comprender el porqué, primero tenemos que ir a la RFC 6520, “Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS) Heartbeat Extension”, la cual los desarrolladores de OpenSSL intentaban habilitar. En este documento se describía una extensión del protocolo TLS para mantener un mecanismo de sesión de bajo costo en la capa de transporte.

La implementación de la RFC era sencilla: se mandaba un paquete de tipo `heartbeat_request` con un contenido arbitrario, y la respuesta sería una copia exacta del _payload_, con la misión de asegurar que la conexión seguía viva.

La solución fue tan sencilla como añadir una comprobación de la longitud del mensaje: si era más larga de lo requerido, se descartaba.

El error consistía en que, cuando en la cabecera se determinaba un espacio mayor al mensaje que realmente se enviaba, el servidor, además de devolver el _payload_ que se le había mandado, también enviaba los siguientes datos que estaban en memoria, realizando un volcado de esta.

Uno de los motivos por los cuales no se llegó a encontrar antes era, en parte, la creencia de que al ser _open source_ estaría protegido por la comunidad, ya que habría mucha gente pendiente de ello. Además, a los analizadores de código estático se les dificultaba el análisis, ya que el programa utilizaba punteros a otros punteros, y el tamaño del búfer no estaba en el puntero, sino que se almacenaba por separado, además del uso de punteros de función, lo cual hace que estas herramientas encuentren mayor dificultad.

Debido a las complicaciones del análisis estático, otro medio era utilizar _fuzzing_, el cual podría haber encontrado la vulnerabilidad fácilmente, según lo que opina mucha gente. Pero esto no es del todo correcto, ya que el _fuzzing_ se enfoca en la entrada de datos por parte de un usuario en la capa siete y no suele profundizar mucho en protocolos complejos.

Según James Kupsch y Barton Miller, identificaron cuatro factores que hacían OpenSSL difícil de analizar. El primero es el que describimos anteriormente: el uso de punteros. El uso de punteros hace que el análisis sea complicado, según sus palabras: "because the size of the buffer is not contained in the pointer but must be stored and managed separately from the pointer", y Heartbleed tenía muchos niveles de indirección. El segundo punto fue la complejidad de ejecución del búfer debido a un mal uso de su localidad. Con esto quiere decir que los búferes de memoria estaban en la caché y eran reutilizados, lo cual puede significar un aumento en el rendimiento, pero a cambio dificulta el análisis de la memoria. El tercer punto: los bytes válidos del mensaje TLS son un subconjunto del búfer asignado. Como afirman Kupsch y Miller, “los punteros al mensaje y la carga útil apuntan al centro de un búfer, y el contenido del mensaje no utiliza todo el búfer de memoria. La longitud de un mensaje es difícil de manejar porque depende de la semántica de este.

Y, por último, que el contenido del búfer no parecía provenir de un atacante, y muchas herramientas de análisis se fijan si los datos han sido corrompidos, y los asignadores de memoria personalizados dificultan la detección de esto. Además, el proceso de descifrado, descompresión y verificación de la integridad ya parecía suficiente.

Para poder realizar un ataque, una vez que se ha realizado la conexión, podemos comprobar si el servicio es vulnerable utilizando _nmap_. El comando sería el siguiente:

```
nmap -sV --script=ssl-heartbleed 192.168.31.1
```

Si es vulnerable, podemos explotar dicha vulnerabilidad utilizando Metasploit con el comando `msfconsole`, el cual abrirá una terminal en la que podemos usar el siguiente comando: `use auxiliary/scanner/ssl/openssl_heartbleed`. Para ver las opciones de dicho comando podemos ejecutar el subcomando `show options` y rellenar las opciones. Con esto podrás realizar el ataque.

# Conclusión

Después de este ataque, muchos certificados tuvieron que ser regenerados, ya que la mayoría de usuarios y _private keys_ de administradores fueron robados de forma pasiva, además de actualizar la lista de certificados. Para arreglar este bug, con actualizar la versión de OpenSSL es suficiente.

Las vulnerabilidades en la seguridad abren la puerta a ataques. Heartbleed fue uno de los más graves y dañinos de la historia de la web debido a que OpenSSL es una librería ampliamente usada sobre SSL/TLS. La facilidad con la que se podía explotar para conseguir información sensible sobre el login, credenciales e información personal en todo Internet hace evidente su gravedad.

Esta vulnerabilidad fue solucionada rápidamente por el equipo de OpenSSL una vez que se descubrió, ya que, como hemos visto en el documento, se debía simplemente a que no se comprobaba si la longitud que venía en la cabecera del mensaje correspondía con la longitud del mensaje. Esto no se llegó a detectar por la “espaguetización” del código mediante el uso de punteros.

En este documento hemos descrito en qué consiste la vulnerabilidad, en qué RFC está basada, por qué sucedió, por qué no se dieron cuenta de ello y cómo se puede explotar dicha vulnerabilidad utilizando _nmap_ y Metasploit.

También esto nos deja como conclusión que, aunque la implementación de una RFC parezca ser segura por ser _open source_, no significa que lo sea por muchos ojos que estén observándola.

# BIBLIOGRAFÍA

Gallagher, Sean (9 de abril de 2014). [«Heartbleed vulnerability may have been exploited months before patch [Updated]»](https://arstechnica.com/information-technology/2014/04/heartbleed-vulnerability-may-have-been-exploited-months-before-patch/). _Ars Technica_ (en inglés estadounidense). Consultado el 10 de noviembre de 2022  
[https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-0160](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-0160)  
[https://0x3zzat.medium.com/heartbleed-vulnerability-and-how-to-exploit-it-using-metasploit-afc044b3dcc5](https://0x3zzat.medium.com/heartbleed-vulnerability-and-how-to-exploit-it-using-metasploit-afc044b3dcc5)  
[https://xkcd.com/1354/](https://xkcd.com/1354/)

Carvalho, M., DeMott, J., Ford, R., & Wheeler, D. A. (2014). Heartbleed 101. _IEEE Security & Privacy_, _12_(4), 63-67.

Ghafoor, I., Jattala, I., Durrani, S., & Tahir, C. M. (2014, December). Analysis of OpenSSL Heartbleed vulnerability for embedded systems. In _17th IEEE International Multi Topic Conference 2014_ (pp. 314-319). IEEE.
