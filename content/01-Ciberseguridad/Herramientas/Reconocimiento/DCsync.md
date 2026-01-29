---
title: "Dcsync"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - reconocimiento
---

> **Relacionado**: [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

¡Muy bien! Vamos a explicar DCsync, que es una de las técnicas más poderosas y peligrosas en un entorno de Active Directory. Aquí tienes unas notas detalladas y didácticas para tus apuntes de pentesting:


---

 DCsync

 ¿Qué es DCsync?

DCsync es una técnica que permite a un atacante solicitar a un Domain Controller (DC) que le envíe los hashes de contraseña de cuentas del dominio, incluyendo cuentas privilegiadas como krbtgt y Administrator.

Es una técnica "fileless": no se ejecuta directamente en el Domain Controller, sino que emula el comportamiento de un controlador de dominio legítimo desde otro equipo.



---

 Contexto técnico

Active Directory replica información entre sus controladores de dominio mediante el protocolo Directory Replication Service Remote Protocol (MS-DRSR).

El comando GetNCChanges permite a un DC solicitar datos sobre objetos del directorio (como credenciales) desde otros DCs.


 Si el atacante compromete una cuenta con permisos suficientes para replicar datos de directorio, puede usar esta funcionalidad legítima para "pedir" hashes de usuarios al DC.


---

 ¿Qué permisos necesita el atacante?

No cualquier usuario del dominio puede ejecutar DCsync.

Se requiere pertenecer a grupos como:

Domain Admins

Enterprise Admins

Administrators

Group con permisos de replicación (como Replicator)



 Si el atacante compromete una de esas cuentas → puede extraer todos los hashes del dominio de forma remota y silenciosa.


---

 Cómo funciona en pentesting

1️⃣ El atacante obtiene control sobre una cuenta con privilegios suficientes (por ejemplo tras una escalada de privilegios lateral).
2️⃣ Utiliza herramientas como mimikatz para ejecutar el ataque DCsync.


---

 Comando típico con mimikatz

lsadump::dcsync /user:<nombre_usuario>

Ejemplos:

Obtener el hash del administrador del dominio:

mimikatz # lsadump::dcsync /user:Administrator

Obtener el hash de la cuenta krbtgt:

mimikatz # lsadump::dcsync /user:krbtgt



---

 Impacto

Compromiso total del dominio:

Permite al atacante obtener los hashes NTLM de cualquier usuario.

Si obtiene el hash de krbtgt, puede emitir tickets Kerberos falsos (Golden Ticket), lo que significa persistencia indefinida y acceso total a cualquier recurso del dominio.




---

 Detección

Aunque el ataque no requiere ejecutar nada en el propio DC, puede dejar trazas en los logs del controlador de dominio:

Event ID 4662: acceso a objetos del directorio.

Event ID 4661: solicitud de permisos sobre atributos sensibles.



 Sin embargo, estos eventos no son triviales de interpretar → importante correlacionar correctamente logs para detectarlo.


---

 Mitigaciones

 Hardening Active Directory:

Minimizar el número de cuentas con permisos de replicación.

Revisar membresías de grupos privilegiados (Domain Admins, Administrators, Enterprise Admins).

Implementar Tiering model (separación de cuentas de administración de dominio y usuarios estándar).


 Monitorización proactiva:

Alertar cuando cuentas no estándar realicen solicitudes de replicación (GetNCChanges).

Revisión de eventos 4662/4661 anómalos.


 MFA para cuentas privilegiadas:

Para reducir riesgo en caso de robo de credenciales.



---

 Resumen rápido para recordar:

>  DCsync = El atacante finge ser un controlador de dominio → pide al DC hashes de usuarios → obtiene todos los hashes, incluyendo krbtgt y Administrator → compromiso total.




---

Si quieres puedo prepararte:

 Laboratorio paso a paso para probar DCsync en entorno seguro.

 Checklist de mitigación y auditoría de cuentas con permisos de replicación en AD.


Solo dime .

