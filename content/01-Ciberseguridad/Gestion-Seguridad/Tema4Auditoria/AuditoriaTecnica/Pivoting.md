---
title: "Pivoting"
date: 2026-01-26
tags:
  - ciberseguridad
  - gestion-seguridad
  - tema4auditoria
---
Perfecto. Aquí tienes una **nota técnica completa y práctica sobre _Pivoting_**, basada en el documento _Auditoría Técnica de Seguridad.pdf_, y ampliada con contexto profesional, ejemplos y herramientas actuales utilizadas en Red Teaming y pentesting:

---

##  Pivoting — Movimiento lateral en redes comprometidas


> **Relacionado**: [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Fundamentos/owasp|owasp]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

###  ¿Qué es Pivoting?

**Pivoting** es una técnica utilizada durante un pentest o un ejercicio de Red Team para **utilizar un equipo comprometido como trampolín** para acceder a **otros sistemas dentro de una red interna**. Se basa en que, una vez que el atacante tiene acceso a una máquina, puede usarla como “pivote” para lanzar nuevos ataques desde ahí, especialmente hacia **redes internas inaccesibles desde el exterior**.

 Es clave en el movimiento lateral: el atacante expande su presencia más allá del primer punto de entrada.

---

###  Tipos de pivoting

| Tipo                 | Descripción                                                                      |
| -------------------- | -------------------------------------------------------------------------------- |
| **Pivoting directo** | Reenvío de puertos desde la máquina comprometida (ej. `portfwd`, `ssh -L`)       |
| **Pivoting inverso** | La víctima establece conexiones salientes hacia el atacante (usado en redes NAT) |
| **Proxy pivoting**   | Encadenar herramientas como [[SOCKS]], [[proxychains]], Metasploit, Chisel, etc. |

---

###  ¿Cuándo se usa?

- Cuando hay **segmentación de red** y desde el atacante original **no se puede llegar directamente a ciertos recursos internos.**
    
- Cuando se desea **explotar sistemas sensibles (servidores, controladores de dominio, SCADA, etc.)** que no son expuestos públicamente.
    
- Cuando se realiza **reconocimiento de redes privadas internas.**
    

---

### ️ Herramientas comunes para Pivoting

####  Con Metasploit (Meterpreter)

```bash
meterpreter > portfwd add -l 8080 -p 5000 -r 172.18.0.5
```

Explicación:

- `-l`: puerto local del atacante
    
- `-p`: puerto objetivo de la máquina interna
    
- `-r`: IP interna a la que solo la víctima tiene acceso
    

---

####  Con **Autoroute** de Metasploit

Permite enrutar automáticamente tráfico hacia subredes internas.

```bash
meterpreter > run autoroute -s 172.18.0.0/24
```

Y luego configurar **proxychains** en Kali para enrutar tráfico a través de esa sesión.

---

####  Con SSH (SOCKS proxy simple)

```bash
ssh -D 1080 user@pivot-machine
```

Luego usar en Kali con:

```bash
proxychains nmap -sT -Pn 10.0.1.10
```

---

####  Otras herramientas útiles

|Herramienta|Descripción|
|---|---|
|**Chisel**|Tunelización TCP/UDP mediante HTTP|
|**SocksOverRDP**|Proxy SOCKS a través de RDP|
|**frp**|Túneles reversos TCP sobre NAT|
|**Ligolo-NG**|Framework moderno para pivoting|

---

###  Ejemplo práctico (como en el documento)

1. Se compromete una máquina expuesta (por ejemplo, una web vulnerable en `10.0.0.5`)
    
2. Desde ella se observa que puede acceder a `172.18.0.0/24`, donde está el servidor de BBDD
    
3. Se ejecuta:
    

```bash
meterpreter > run autoroute -s 172.18.0.0/24
```

4. Se configura Kali con:
    

```bash
proxychains curl http://172.18.0.10:8000
```

5. Se lanza un Nmap:
    

```bash
proxychains nmap -p- -sT -Pn 172.18.0.10
```

 Ahora el atacante puede mapear y atacar redes internas gracias al pivoting.

---

###  Riesgos y contramedidas

|Riesgo|Contramedida|
|---|---|
|Acceso lateral a zonas críticas|Segmentación de red con firewall y VLANs|
|Movimiento indetectado|EDRs, alertas de actividad sospechosa en endpoints internos|
|Uso de herramientas tipo proxy|Detección de túneles reversos (deep packet inspection, DLP)|
|Persistencia post-pivoting|Monitoreo de conexiones persistentes y revisión de tráfico proxy|

---

###  Recursos útiles

- [HackTricks – Pivoting](https://book.hacktricks.xyz/network-services-pentesting/pivoting)
    
- [PayloadsAllTheThings – Pivoting Techniques](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Post%20Exploitation/Pivoting)
    
- [Ligolo-NG](https://github.com/sensepost/ligolo-ng)
    

---

###  ¿Quieres...?

- Que prepare un **laboratorio práctico de pivoting con Kali + máquinas virtuales**
    
- Una plantilla de informe técnico de explotación con pivoting paso a paso
    
- Un ejemplo más avanzado con movimiento lateral en Windows AD
    

Solo dímelo y te lo armo.