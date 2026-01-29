---
title: "Instalacion Y Configuracion De Splunk Universal Forwarder Con Snort En Windows Y Ubuntu"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
  - ids-ips
---


Este procedimiento detalla los pasos para instalar y configurar el **Splunk Universal Forwarder** en sistemas Windows y Ubuntu, con el objetivo de enviar logs desde un sistema remoto hacia un servidor Splunk, utilizando Snort para capturar eventos de red.

#### 1. **Instalación de Splunk Enterprise (versión Enterprise)**  

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Herramientas/SIEM/SPLUNK|SPLUNK]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]].

   - **Descarga**: Primero, necesitas obtener la versión de **Splunk Enterprise** desde la página oficial de Splunk. Asegúrate de elegir la versión que mejor se adapte a tu entorno.
   - **Addon para Windows**: Si estás utilizando Windows, es necesario instalar un complemento (addon) adicional para que Splunk funcione correctamente en el entorno de Windows.
   - **Selección de Descarga e Instalación**: En la página de Splunk, selecciona **Download** y luego elige la opción de instalación que corresponda a tu sistema operativo.

#### 2. **Instalación de Splunk Universal Forwarder en Windows**  
   - **Descargar**: El **Splunk Universal Forwarder** es el agente encargado de recoger y enviar los datos desde el sistema hacia el servidor Splunk.
   - **Instalación en Windows**: 
     1. Descarga el instalador para Windows desde la página oficial de Splunk.
     2. Ejecuta el instalador y sigue los pasos guiados para completar la instalación.
     3. Es recomendable no utilizar el puerto por defecto de Splunk, aunque el **HEADER** indique este valor. Cambiar el puerto por seguridad es una buena práctica.
  
#### 3. **Configuración del Splunk Universal Forwarder**  
   Una vez instalado, el Universal Forwarder necesita ser configurado para enviar datos al servidor Splunk.

   1. **Ubicación de Archivos**:  
      Los archivos del Splunk Universal Forwarder se encuentran típicamente en la siguiente ruta:
      ```
      C:\Program Files\SplunkUniversalForwarder\etc\apps
      ```
   2. **Descomprimir el Addon de Splunk para Windows**:  
      - Descomprime el addon de Splunk para Windows dentro de la carpeta mencionada previamente.
   3. **Configuración de Archivos `input.conf`**:
      - Dentro de la carpeta **default** del addon, encontrarás un archivo llamado **input.conf**.
      - Copia este archivo a la carpeta **local** que has creado dentro de **apps**.
   4. **Modificación de `input.conf`**:  
      Abre el archivo **input.conf** en un editor de texto y realiza las siguientes modificaciones:
      - Cambia `disable = 1` a `disable = 0` para habilitar la entrada de logs.
      - Modifica `renderXML = true` a `renderXML = false` si es necesario (dependiendo de la configuración de tu entorno).
  
#### 4. **Instalación y Configuración de Snort**  
   **Snort** es una herramienta de detección de intrusiones en redes (IDS) que se utilizará para capturar eventos de seguridad y enviarlos a Splunk. La configuración correcta de Snort es crucial para la recopilación de logs.

   - **Instalación de Snort en Windows**:  
     Si deseas instalar Snort en Windows, asegúrate de seguir los pasos específicos para la instalación de esta herramienta. En general, necesitarás descargar los binarios desde el sitio oficial de Snort y configurar los archivos de reglas para monitorear el tráfico de red.

   - **Instalación de Snort en Ubuntu**:  
     En sistemas Ubuntu, puedes instalar Snort utilizando los siguientes comandos:
     ```bash
     sudo apt update
     sudo apt install snort
     ```
     Después de instalar Snort, configura las reglas para capturar el tráfico deseado.

#### 5. **Configuración en Ubuntu**  
   En **Ubuntu**, los pasos son prácticamente los mismos que en Windows:

   - **Instalar Splunk Universal Forwarder**:
     1. Descarga el archivo `.tar` de Splunk Universal Forwarder para Linux desde la página oficial.
     2. Extrae el archivo y sigue las instrucciones para completar la instalación.
   - **Configurar `input.conf`**: Al igual que en Windows, configura el archivo **input.conf** en Ubuntu para habilitar la entrada de logs y ajustarlo a tus necesidades específicas.

#### 6. **Configuración de Fuentes de Logs**  
   Una vez que Splunk Universal Forwarder y Snort estén configurados, puedes indicarle al sistema desde dónde recoger los logs. Esto puede hacerse configurando los parámetros de **inputs.conf** para especificar las ubicaciones de los archivos de logs generados por Snort y otras fuentes que desees monitorear.

   - **Prueba de Captura de Logs**:
     Para asegurarte de que todo está funcionando correctamente, realiza una prueba de captura de logs. Puedes ejecutar comandos como:
     ```bash
     testmynids
     ```
     Esto te permitirá verificar que Snort esté correctamente configurado para enviar los logs a Splunk.

#### 7. **Conclusión**  
La configuración de **Splunk Universal Forwarder** junto con **Snort** te permitirá realizar una monitorización efectiva de los eventos de seguridad en tu red, enviando todos los logs a tu servidor Splunk para su análisis y visualización. Recuerda modificar siempre las configuraciones predeterminadas de puertos y opciones de seguridad, y asegurarte de que las rutas de los archivos de logs estén correctamente configuradas en **input.conf**.

---

Este procedimiento proporciona una guía paso a paso para instalar y configurar el **Splunk Universal Forwarder** en **Windows y Ubuntu**, integrando **Snort** para la recopilación de eventos de red.