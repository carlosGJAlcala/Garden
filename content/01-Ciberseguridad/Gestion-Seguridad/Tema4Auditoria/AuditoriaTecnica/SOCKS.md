---
title: "Socks"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Aquí tienes una **nota técnica sobre SOCKS**, enfocada en su uso dentro de pentesting, Red Teaming y pivoting, pero también explicada desde sus fundamentos, para que puedas usarla tanto en informes como en formación técnica:

---

##  SOCKS — Proxy versátil para pentesting y pivoting


> **Relacionado**: [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Fundamentos/SQLMap|SQLMap]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/AuditoriaTecnica/Pivoting|Pivoting]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/proxychains|proxychains]].

###  ¿Qué es SOCKS?

**SOCKS** (Socket Secure) es un **protocolo de red** que permite **redirigir tráfico de red a través de un servidor proxy**, actuando a nivel de capa de sesión (modelo OSI). A diferencia de un proxy HTTP, **SOCKS es agnóstico del protocolo**, lo que significa que puede reenviar tráfico TCP o UDP de cualquier tipo, no solo web.

 En ciberseguridad ofensiva, **se usa para enrutar tráfico a través de una máquina comprometida** y realizar técnicas como _pivoting_ o _tunneling_ hacia redes internas no accesibles directamente.

---

### ️ Versiones principales

|Versión|Características|
|---|---|
|SOCKS4|Solo TCP, sin autenticación|
|SOCKS5|Soporta TCP y UDP, autenticación, DNS remota|

 Actualmente se usa **SOCKS5** casi exclusivamente por su flexibilidad.

---

###  ¿Para qué se usa en pentesting?

1. **Pivoting en redes internas**  
     Reenviar el tráfico a través de una máquina comprometida.
    
2. **Ocultación de origen**  
     Simular que el tráfico proviene de otro punto (ej. para evadir detecciones).
    
3. **Encadenar proxies**  
     Usar varias máquinas como “saltos” en una cadena de ataque.
    
4. **Escaneo interno desde fuera**  
     Nmap, curl, sqlmap y otras herramientas se pueden redirigir usando `proxychains`.
    

---

###  Casos de uso típicos

####  1. SSH como proxy SOCKS

```bash
ssh -D 1080 user@10.0.0.5
```

Esto crea un **proxy SOCKS en el puerto 1080 de tu máquina local**, enviando el tráfico a través del host `10.0.0.5`.

Luego puedes usar `proxychains`:

```bash
proxychains nmap -sT -Pn 192.168.100.10
```

---

####  2. Con Metasploit y `socks4a`

Metasploit puede exponer un **proxy SOCKS desde una sesión Meterpreter** con el módulo:

```bash
use auxiliary/server/socks4a
set SRVPORT 1080
run
```

Y luego, con `proxychains`, todo tu tráfico puede atravesar el host comprometido.

---

####  3. Otras herramientas útiles con soporte SOCKS

|Herramienta|Uso|
|---|---|
|**proxychains**|Redirige tráfico CLI a través de SOCKS|
|**Firefox**|Puede configurarse directamente con SOCKS5|
|**SQLmap**|Soporta `--proxy socks5://127.0.0.1:1080`|
|**Nmap**|Con `proxychains nmap ...`|
|**Burp Suite**|Puede configurarse en “Upstream proxy”|

---

###  Diferencias con túneles tradicionales (port forwarding)

|Técnica|Nivel|Soporte UDP|Requiere puerto fijo|
|---|---|---|---|
|Port forwarding|TCP (L4)|||
|SOCKS proxy|Sesión (L5)| (v5)| (más dinámico)|

---

### ️ Ejemplo práctico completo

1. Comprometes un host `10.0.0.5`
    
2. Lanzamos en Kali:
    

```bash
ssh -D 1080 user@10.0.0.5
```

3. En `/etc/proxychains.conf`, última línea:
    

```
socks5 127.0.0.1 1080
```

4. Escaneas red interna del cliente (accesible solo desde 10.0.0.5):
    

```bash
proxychains nmap -sT -Pn -p- 192.168.1.10
```

---

### ️ Riesgos para el Blue Team

- El tráfico puede estar **encapsulado y cifrado**, dificultando su detección.
    
- Un atacante puede **acceder a redes internas** usando SOCKS sin necesidad de explotar más máquinas.
    
- Muchas herramientas comunes **no loguean correctamente tráfico proxy** si no están bien configuradas.
    

 Defender implica monitorear conexiones inusuales salientes y entradas proxy (IDS/IPS, EDR, DNS tunneling detection...).

---

###  Recursos útiles

- [HackTricks – SOCKS Proxying](https://book.hacktricks.xyz/network-services-pentesting/pivoting#socks-proxy)
    
- [Proxychains GitHub](https://github.com/haad/proxychains)
    
- [SSH SOCKS examples](https://linux.die.net/man/1/ssh)
    

---

¿Te gustaría que te prepare un laboratorio práctico con `proxychains`, Nmap y una VM vulnerable? También puedo incluir una sección lista para pegar en un informe técnico de pentesting o Red Team.