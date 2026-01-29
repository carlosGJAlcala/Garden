---
title: "Leer un archivo CSV con los datos de las IP y guardarlas en una lista"
date: 2026-01-26
tags:
  - ciencias-computacion
  - lenguajes-programacion
  - python
---

```python
import socket  
import csv  
  
# Leer un archivo CSV con los datos de las IP y guardarlas en una lista  

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[02-Ciencias-Computacion/Compiladores/Comprobacion-de-tipos/Comprobacion-de-codigo-comprobacion-de-tipos|Comprobacion de codigo comprobacion de tipos]].

def importar_ip_from_csv(csv_file):  
    lista = []  
    with open(csv_file, newline='') as csvfile:  
        lineas = csv.reader(csvfile, delimiter=';')  
        for linea in lineas:  
            if linea:  # Ignorar líneas vacías  
                # Añadir la primera columna (IP) como una cadena a la lista                lista.append(linea[0].strip())  
    return lista  
  
  
def nmapbasico(ip):  
    puertosAbiertos = []  
    puertos = [21, 22, 23, 25, 53, 67, 68, 80, 443]  
    for puerto in puertos:  
        try:  
            with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:  
                s.settimeout(1)  # Tiempo en segundos  
                # Verificar si el puerto está abierto                if s.connect_ex((ip, puerto)) == 0:  
                    puertosAbiertos.append(puerto)  
                else:  
                    print(f"No se pudo conectar al servidor {ip}:{puerto}")  
        except Exception as e:  
            print(f"Error al conectar al servidor {ip}: {e}")  
    return puertosAbiertos  
  
  
if __name__ == '__main__':  
    # Leer las IPs desde el archivo CSV  
    ips = importar_ip_from_csv("prueba.csv")  
    ipMasPuertosAbierto = []  
  
    # Escanear cada IP y guardar resultados  
    for ip in ips:  
        print(f"Analizando {ip}...")  
        puertos_abiertos = nmapbasico(ip)  
        ipMasPuertosAbierto.append((ip, puertos_abiertos))  
  
    # Mostrar resultados  
    for dato in ipMasPuertosAbierto:  
        ip, puertos = dato  
        print(f"IP: {ip} - Puertos abiertos: {puertos}")
```
Este ejemplo importa csv  recoge las ip y valida unas conexiones con un puerto