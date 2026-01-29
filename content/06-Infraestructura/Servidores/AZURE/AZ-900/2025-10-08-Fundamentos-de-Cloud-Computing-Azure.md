---
title: "APUNTES"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - azure
---

La nube es la proveción de servicios de computo a traves de internet:
[[Video-de-youtube]]
# APUNTES


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[03-Desarrollo-Software/Bases-Datos/MongoDB|MongoDB]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Herramientas/HTTP-Parameter-Pollution-HPP|HTTP Parameter Pollution HPP]].

## CapEX (Capital Expenditure) gastos de capital

Nube privada 
ambiente local 
on premises


## Nube hibrida

Es una combinación esto se usa para aumtentar tu rendimiento y por tema de reglamento, si tu pais no tiene una regíon de azure
## OpEX(Opertainoal Expenditure)Gasto operativo 

Pagas por el servicio pero no  es tuya


# Modelo de responsabilidades compartida 



![[Pasted image 20251008120304.png]]

El azul relata  la responsabilidad que tienes  ,

IaaS  Infrastructure como servicio azure, solo se encarga de los físico
PaaS plataforma como servicio azure te da un servicio como windows y linux 
SaaS software terminado, el adroid studio sería tambien un SaaS, te encargas de la información de los datos de las cuentas.

# Regiones de Azure

Una región es una area geográfico donde azure tiene un cpd

## zona de disponibilidad
Aportan seguridad a base de redundancia , las zonas de disponibilidad viene en trío.
![[Pasted image 20251008120911.png]]
Lo más importante en la nube es la disponibilidad viene a palanacado a esto un SLA  ( porcentaje de rendimiento que te firma azure que te va a dar , esto quiere decir que por ejemplo te dan un 99% de rendimiento en  un mes solo puede fallar el servicio durante el 1 por cieento de tiempo ) por ejemplo 7 horas te pu


en el app servicio  si fallan te dan un descuento en creditos

## Tolerancia a fallos 

Los datos estan disponibles a pesar de se caigan  los servidiroes
## Agilidad

## Elasticidad 
Es automatica en cambio la escalibilidad es manual ( puede ser vertica( crece un unico recurso de zure) y horizontal ) 
### Economía de escala 
Cuando usas más un recurso cuesta menos por recurso , ( compra por mayor)

# Servicios de azure 

# Servicio de compute
### Azure Virtual Machine
Modelo de servio Iaass

Los recursos de azure te piden:
- subscrición  (donde se cobra)
- grupo de recursos: es una carpeta donde va el recurso un recurso va en un grupo de recursos
- Nombre de la máquina 
- Region
te pide otras cosas que son opcionales:
- (opcional) también puedes configurar las zonas de disponibilidad 
- SKU (Tamaño) que tan potente quieres la máquina  
- Si quieres acceder  de forma remota escoge windows 10 pro
### Azure virtual Machines scales set

Es para automatizar la escala de máquinas virtualaes , puedes replicar máquinas virtuales pero no se puede automatizar esa replicación
### Azure batch
Informática de alto rendimiento HPC 
para trabajar con lotes de información  en paralelo
### Azure App Service

Esto es un PaaS , habilia servico  web para azure cualquier cosa con http  y https (WebJobs)
En un pass te deja elegir que stack de tecnologia usar  java node , pero no el sistema operativo
#### crear aplicacion web
puedes elegir el escalado de la aplicación virtutal esto lo puedes hacer porque es un pass en iass no puedes hacerlo de forma automatico
#### Azure container instances
También  es un pass , es para la ejecución de contenedores de azure
### Azure Kubernetes Servicies
Es le manejador de los conten edroes  controla los contenederos  autoe escala los contenedores dirige le trafico  , reduce la app y implementa nuevos nodos
### Azure Functions 
Es un PaaS - Serveles , te cobran por evento, sin servidor sin servidor esto quiero decir que solo se sube el código y ya está, está pensando para tener un api y que te cobre por evento a diferencia del app service que te cobra por hora, funciona por disparadores.

### Azure Logic Function
Parecido al anteroiro pero este tiene conectores ofciales, sus conectores son visuaels

### Azurete Virtual Desktop 
Es un servicio PasS, que virtualiza aplicaciones, es para usuario final a diferencia de la máquina virtual es para crear soluciones, es por ejemplo para autocad para renderizaciones que no puede tu pc.

### Azure virutal network
Es una IaaS es para comunicar los servicios que tenemos en azure.  te crear un interfaz red.
Cuando crear las interfaz de red te genera la cable de red .
Dirección ip pública ( lo puedes deshabilidata), el grupo de seguridad de red fucnióna como un firewall 
el disco es donde se gurada  la información 
y la red virtual es tu red interna
## Azure VPN Gateway

Te crea una vpn  para conectarlo con tu azure virtual network, de tu onpremise para contar

### Azure Exprees Router

Hace una conexión fisica de tu datacentre a azure

### Azure Aplicacation gateway  
es un balancedador de carga

### Azure CDN
 Entrega el contendio , hace un replica del servicio en un sitio cercano  para poder mejorar la 
 
 latencia
 
### Azure FRONT DOOR

Es un banlanceador de carga a nivel mundial (como el aplication gateway)

### Azure Traffic Manager 
Une regiones 


---- 
# servicios storage 

Almacena objetos, 
los archivos , las fotos  y lo que se guarda en la base de datos se guarda donde se hizo la foto los likes 

son todos IaaS 
### la cuenta de almacenamiento
Es dodn de se maneja

El Azure cloud shell es la temina de la nube 

puedes hacer un 
### Azure blob storage 
es para laacenar obtengo gradnes como videos 
para crear un blob storage tenemos que darle alamcenamisnto y crear contenedor con blob pueden acceder pero te pueden hacer una enumeración, si es privado necesitas o bien loguearte o un token SaaS está optimizado para streaming de video

### Azure file storage
es para compartir archivos entre  lás mauina virtuales 

### Azure disk storage 
dispos para las máinas virtuales
### Azure queue storage 

Es una cola de mensajes , encola en fucuíon fifo

---- 
# servicios de base de datos

### Azure sql database 
 teutilma la última versicón de microsfot sql server
#### azure data base migration service
hacen la migración de unos disco a otras 

### Azure comos DB
Base de datos no relación  (azure puede hacer una traducón de consultas sql a no sql si tienes elnúcleo d ) soporta mongodb, cassandra  y gemlin
