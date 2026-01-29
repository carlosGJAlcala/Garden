---
title: "Docker - Comandos esenciales"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
---

# Docker - Comandos esenciales

> **Relacionado**: Ver [[06-Infraestructura/Servidores/GestionServidores/CasaOS|CasaOS]] para gestión de contenedores. [[UNIX/Que-es-init-el-sistema-de-arranque-de-Linux|Sistema init Linux]]. [[02-Ciencias-Computacion/Redes/VAGRANT|Vagrant]] para VMs. [[03-Desarrollo-Software/Distribuido/Microservicios|Microservicios]].

## **1. Ejecutar un contenedor**

```bash
docker run nombre_imagen
```

- Crea y arranca un contenedor desde la imagen especificada.
    
- Si la imagen no está en local, la descarga de Docker Hub.
    

---

## **2. Ver el estado de los contenedores**

```bash
docker ps          # Solo los contenedores en ejecución
docker ps -a       # Todos, incluidos detenidos
```

---

## **3. Inspeccionar un contenedor**

```bash
docker inspect nombre_contenedor
```

- Muestra toda la configuración en formato JSON: red, volúmenes, variables de entorno, etc.
    

Filtrar solo variables de entorno:

```bash
docker inspect -f '{{json .Config.Env}}' nombre_contenedor
```

---

## **4. Abrir el STDIN de un contenedor (modo interactivo)**

```bash
docker run -it nombre_imagen
```

- `-i` → mantiene STDIN abierto.
    
- `-t` → asigna una pseudo-terminal.
    
- Útil para imágenes tipo Ubuntu, Alpine, etc., donde quieres una shell.
    

---

## **5. Ver procesos del host relacionados con Docker**

Si quieres ver todos los procesos (a nivel de host, no de contenedor):

```bash
ps -fea | grep docker
```

Si quieres ver procesos dentro de un contenedor:

```bash
docker exec nombre_contenedor ps -fea
```

---

## **6. Ejecutar en segundo plano y mapear puertos**

```bash
docker run -d --name hola -p 8080:80 nombre_imagen
```

- `-d` → _detached mode_ (en segundo plano).
    
- `--name hola` → nombre amigable para el contenedor.
    
- `-p 8080:80` → mapea el puerto 80 del contenedor al puerto 8080 del host.
    
