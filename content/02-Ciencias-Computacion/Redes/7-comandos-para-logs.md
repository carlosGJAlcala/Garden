---
title: "7 Comandos Para Logs"
date: 2026-01-26
tags:
  - ciencias-computacion
  - redes
---

> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/Pila-de-protocolos-TCPIP|Pila de protocolos TCPIP]]. [[02-Ciencias-Computacion/Lenguajes-Programacion/Python/socket/socket-interfaz-de-red-de-bajo-nivel-documentacion-de-Python-31015|socket interfaz de red de bajo nivel documentacion de Python 31015]]. [[02-Ciencias-Computacion/Percepcion-Control/partes-principales-de-un-sistema-robotico|partes principales de un sistema robotico]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]]. [[01-Ciberseguridad/Fundamentos/shred|shred]].

7 comandos que marcan la diferencia entre usar el sistema... y dominarlo.  
  
 Potentes.  
 Precisos.  
 Inteligentes.  
  
1. awk '{print $1}' archivo.txt  
 Extrae columnas específicas. Brutal para logs.  
  
2. tcpdump -i eth0 port 80  
 Captura tráfico HTTP en tiempo real. Ideal para análisis de red.  
  
3. netstat -tulnp  
Ve qué servicios están escuchando y quién los ejecuta.  
  
4. ss -tulwn  
Alternativa más rápida a netstat. Te encantará.  
  
5. find / -type f -iname "*.log" -mtime -3  
 Encuentra logs modificados en los últimos 3 días. Top para forense.  
  
6. grep -r --color "error" /var/log  
Busca errores en todos los logs, resaltados. Rápido y útil.  
  
7. journalctl -xe | tail  
Mira los últimos logs del sistema con detalles extendidos.  
  
 Dominar estos comandos te permite auditar, analizar y mantener sistemas como un verdadero profesional.