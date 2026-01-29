---
title: "Splunk"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - siem
---



> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-03-27-charla-seguridad-APIs-OAUTH20|2025 03 27 charla seguridad APIs OAUTH20]].

ejecutamos el siguiente comando 
```bash
sudo docker run -d -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_USER=root" -e "SPLUNK_PASSWORD=root" -p "8000:8000" splunk/splunk`

```
```bash 
sudo docker run -d -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_PASSWORD=changeme"  -e "SPLUNK_USER=root" -p "8000:8000" splunk/splunk


```
una vez que lo hemos ejecutado nos podemos meternos 
en la pagina web
![[Pasted image 20241204172607.png]]

al ejecutarlo ya tenemos haceso al servidor :

![[Pasted image 20241204181357.png]]
si queremos para el contedor podemos hacer un docker stop idcontenedor
y si queremos levantarlo hacemos docker y start 