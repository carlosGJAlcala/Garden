---
title: "Pass The Hash Pth Pass The Ticket Ptt"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

# Pass-the-Hash (PtH) / Pass-the-Ticket (PtT)

> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/AuditoriaTecnica/Pivoting|Pivoting]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

---

## 1. Pass-the-Hash (PtH)

 ¿Qué es?

Técnica que permite autenticarse en sistemas Windows usando directamente el hash NTLM de la contraseña, sin conocer la contraseña en texto claro.


 Cómo funciona:

NTLM permite usar el hash como si fuera la contraseña en el proceso de autenticación.

El atacante necesita:

Hash NTLM (NTLM hash) de la cuenta objetivo.

Herramientas que permitan inyectarlo (ej.: mimikatz, wmiexec, psexec).



 Escenario típico:

Movimiento lateral en red interna → el atacante obtiene hashes de cuentas (por ejemplo tras dump con mimikatz) y se conecta a otros sistemas reutilizando el hash.


 Limitación:

Solo funciona en entornos que acepten autenticación NTLM.



---

2. Pass-the-Ticket (PtT)

 ¿Qué es?

Técnica que permite usar directamente un Ticket Granting Ticket (TGT) de Kerberos robado para autenticarse en servicios sin conocer contraseña ni hash.


 Cómo funciona:

El atacante obtiene un TGT válido de la cuenta objetivo (por ejemplo, exportado desde LSASS con mimikatz).

Carga ese ticket en su propio sistema (kerberos ticket injection).

Se autentica en servicios Kerberos (como SMB o HTTP) como si fuera el usuario legítimo.


 Ventaja:

No depende de NTLM → más sigiloso en redes modernas (Kerberos-first).


 Limitación:

TGT tiene una validez limitada (usualmente 10 horas por defecto).



---

3. Over-Pass-the-Hash (OPtH)

 ¿Qué es?

Variante avanzada de Pass-the-Hash que combina NTLM y Kerberos.


 Cómo funciona:
1. El atacante tiene hash NTLM de la cuenta objetivo. 2. En vez de autenticarse directamente vía NTLM, usa ese hash para solicitar un TGT al KDC:

Autenticación Kerberos, pero utilizando NTLM hash como prueba de posesión. 3️⃣ El atacante obtiene un TGT legítimo de Kerberos y puede usarlo en el dominio.


 Ventaja:

Eleva el uso de un hash NTLM a obtener tickets Kerberos válidos:

Permite autenticarse a servicios que no aceptan NTLM pero sí Kerberos.



 Herramientas:

mimikatz con el comando sekurlsa::pth.



---

4. Over-Pass-the-Ticket (OPtT)

 ¿Qué es?

Técnica menos común y más avanzada que implica usar un TGT robado y suplantar identidad para obtener nuevos tickets.


 Cómo funciona:

El atacante tiene un TGT válido, pero lo modifica o reutiliza para obtener tickets adicionales (TGS) en nombre de otros usuarios o para servicios adicionales.

Utiliza la relación de confianza en Kerberos para pivotar.


 Escenario:

Abuso de delegaciones (S4U2Self o S4U2Proxy), similar a abusos de Constrained Delegation.


 Ventaja:

Mayor flexibilidad en movimientos laterales.

Más difícil de detectar si se realiza correctamente.



---

 Comparativa rápida

Técnica	Usa hashes	Usa tickets	Protocolos afectados	Objetivo principal

Pass-the-Hash (PtH)			NTLM	Autenticarse con hash NTLM
Pass-the-Ticket (PtT)			Kerberos	Usar TGT robado para acceso
Over-Pass-the-Hash (OPtH)			NTLM + Kerberos	Obtener TGT usando hash NTLM
Over-Pass-the-Ticket (OPtT)			Kerberos avanzado	Obtener más tickets usando TGT robado



---

 Herramientas más usadas

 mimikatz: soporte completo para todas estas técnicas:

sekurlsa::pth → Over-Pass-the-Hash

kerberos::ptt → Pass-the-Ticket

sekurlsa::logonpasswords → Dump de credenciales / hashes


 Impacket:

psexec.py y wmiexec.py admiten autenticación Pass-the-Hash directamente.



---

 Mitigaciones generales

 Para defenderse de todas estas técnicas:

Activar Credential Guard en Windows 10/11/Server 2016+ para proteger LSASS.

MFA obligatoria siempre que sea posible (impide acceso solo con hash/ticket).

Minimizar privilegios y limitar cuentas con acceso remoto.

Deshabilitar NTLM en dominios modernos (NTLM blocking policy).

Monitorizar uso sospechoso de tickets (Event ID 4769).



---

 Resumen final:

>  PtH: reutilización directa de hash NTLM.
 PtT: reutilización directa de ticket Kerberos robado (TGT).
 OPtH: usar hash NTLM para obtener un TGT válido (eleva el hash a ticket).
 OPtT: usar TGT robado para obtener más tickets en nombre de otros usuarios/servicios (Kerberos pivoting).




---