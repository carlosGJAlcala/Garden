---
title: "Hacking Con Valentin"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---

## Explotación y Creación de Exploits


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/shellcode|shellcode]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/FOCA|FOCA]]. [[01-Ciberseguridad/Ingenieria-Inversa/MONA|MONA]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]].

**Plugin de Mona (conjuro de exploit)**  
Mona es un plugin para Immunity Debugger que permite automatizar y facilitar el desarrollo de exploits. Con Mona se pueden buscar patrones, direcciones de salto, crear “rop chains” y muchos otros recursos útiles para encontrar vulnerabilidades y generar código de explotación.

**Exploit-DB**  
[Exploit Database](https://www.exploit-db.com/) es un repositorio en línea de exploits públicos y vulnerabilidades conocidas. Es una herramienta fundamental para la investigación, ya que permite encontrar ejemplos de código, referencias a CVEs y vectores de ataque documentados.

**Desbordamiento de Memoria (Overflow)**  
Un desbordamiento de pila (stack overflow) se produce cuando se escribe más información en un búfer de la que puede almacenar, sobrescribiendo partes de la memoria adyacente. Esto puede ser aprovechado para ejecutar código arbitrario, por ejemplo, modificando la dirección de retorno de una función para saltar hacia nuestro payload. Al usar herramientas como Mona, se pueden encontrar patrones y generar exploits que aprovechen estas vulnerabilidades.

**Reverse Shell**  
Una “reverse shell” es un tipo de acceso remoto que se obtiene cuando la máquina víctima inicia la conexión hacia el atacante, facilitando así la elusión de cortafuegos que filtran conexiones entrantes. Con Mona u otras herramientas, se pueden generar shellcodes para invertir la conexión y obtener una shell interactiva.

---

## Hacking en Dispositivos Móviles (Android)

La plataforma Android utiliza ficheros APK para distribuir aplicaciones. Un archivo APK contiene todos los recursos, binarios y metadatos necesarios para ejecutar la aplicación.

- **AndroidManifest.xml**: Contiene información básica sobre la aplicación, como sus actividades, servicios, permisos requeridos, intent-filters y otras propiedades esenciales.
- **resources.arsc**: Archivo binario que contiene los recursos compilados de la aplicación, incluyendo textos, cadenas de caracteres, estilos y otros metadatos.
- **lib/**: Carpeta con las librerías nativas (por ejemplo, código compilado para distintas arquitecturas como ARM, x86, etc.).

Un atacante puede descompilar el archivo APK usando diferentes herramientas para obtener información sobre su funcionamiento interno y buscar vulnerabilidades.

**Problema de Arquitecturas y Emuladores**  
Android corre principalmente sobre arquitecturas ARM, pero cuando se utilizan emuladores en arquitecturas Intel x86 puede haber problemas de compatibilidad. Herramientas como Genymotion o Android Studio Emulator permiten emular diferentes dispositivos, aunque a veces es necesario instalar componentes adicionales o “opengapps” para disponer de las aplicaciones de Google y servicios básicos.

---

## Pruebas Estáticas de Aplicaciones Móviles

Para el análisis estático de APK se pueden usar diversas herramientas:

- **apktool**: Permite descompilar y volver a compilar APKs, extrayendo el código Smali y los recursos.
- **jadx / jd-gui**: Herramientas para descompilar y ver el código Java de las aplicaciones Android a partir de los archivos .class y .dex.
- **Bytecode Viewer**: Permite visualizar el bytecode de Java de forma gráfica.
- **MobSF (Mobile Security Framework)**: Herramienta todo-en-uno para el análisis estático y dinámico de aplicaciones móviles.
- **QARK**: Cuestiona la calidad del código de las aplicaciones Android, detectando vulnerabilidades de seguridad.
- **Yaazhini**: Otra herramienta útil para el análisis de seguridad en aplicaciones Android.

---

## Herramientas de Análisis Dinámico

- **FRIDA**: Framework para realizar instrumentación dinámica en tiempo de ejecución, permitiendo manipular el comportamiento de las aplicaciones sobre la marcha.
- **Objection**: Una utilidad que, basada en FRIDA, facilita la manipulación dinámica de las apps sin necesidad de modificar su código. Permite hacer “hooking” de funciones, manipular datos y saltarse verificaciones.

**Emuladores y Entornos Dinámicos**

- **Genymotion**: Emulador Android multiplataforma (Windows, Linux, macOS) basado en VirtualBox, muy rápido y personalizable. Permite crear múltiples dispositivos virtuales.
    
- **ADB (Android Debug Bridge)**: Herramienta de línea de comandos que permite conectarse a un dispositivo Android (físico o virtual) para instalar aplicaciones, acceder a la línea de comandos del dispositivo, extraer datos y realizar acciones de debugging.
    
    Ejemplo de conexión:
    
    ```bash
    adb connect 192.168.135.105
    ```
    
- **Drozer**: Herramienta antigua, pero útil, para realizar análisis de seguridad sobre aplicaciones Android, explorando actividades, servicios, receptores de broadcast y proveedores de contenido.
    

**Dependencias y Otras Herramientas**

- **Instalación de paquetería**: Para instalar, por ejemplo, el agente de Drozer, se puede usar:
    
    ```bash
    adb install drozer-agent.apk
    ```
    
- **Sieve**: Herramienta para poner a prueba la seguridad de gestores de contraseñas (como KeePass), permitiendo comprender vulnerabilidades relacionadas con el almacenamiento de credenciales.
    

---

## Conceptos Clave en Android

- **AndroidManifest.xml**: Define la estructura de la app, incluyendo:
    - **Activities**: Pantallas o interfaces de usuario.
    - **Services**: Servicios en segundo plano.
    - **Content Providers**: Abstracción para el acceso a datos estructurados (base de datos interna).
    - **Broadcast Receivers**: Permiten que la app responda a eventos del sistema o de otras apps.

Estos componentes son claves al momento de realizar pruebas de seguridad, ya que pueden presentar puntos de entrada para la manipulación, explotación de permisos o acceso indebido a datos.


Vamos a aclarar y estructurar mejor estos conceptos para que todo quede claro:

---

## SSL Pinning y Limitaciones

**SSL Pinning** es una técnica de seguridad utilizada en aplicaciones para asegurarse de que solo se puedan establecer conexiones HTTPS con certificados específicos. Esto puede ser un obstáculo al intentar interceptar el tráfico de una app para analizarlo o modificarlo. Herramientas como **Genymotion** pueden no funcionar correctamente si el tráfico está protegido con SSL Pinning, porque evita la utilización de certificados personalizados o proxys como Burp Suite.

### Solución para Bypass SSL Pinning

Para sortear este problema, puedes usar herramientas como:

- **FRIDA**: Permite inyectar código en tiempo de ejecución para deshabilitar el SSL Pinning en muchas aplicaciones.
- **Objection**: Facilita el bypass de SSL Pinning automáticamente al usar sus comandos preconfigurados.

---

## Genymotion y ARM Translation

Genymotion, por defecto, emula arquitecturas Intel (x86) en lugar de ARM, lo cual puede causar problemas al intentar ejecutar aplicaciones que dependen de código nativo compilado para ARM. Para solucionar esto, se puede instalar un paquete de traducción de ARM en el emulador de Genymotion:

1. Descarga el archivo **ARM Translation** correspondiente a tu versión de Android.
2. Arrastra el archivo al emulador Genymotion abierto.
3. Reinicia el emulador para aplicar los cambios.

Esto permite que aplicaciones diseñadas para ARM funcionen correctamente en el entorno emulado.

---

## Uso de Drozer

Drozer es una herramienta similar a Metasploit pero diseñada específicamente para analizar aplicaciones Android. Permite identificar y explotar superficies de ataque en una aplicación.

### Configuración y Ejecución

1. **Preparar conexión ADB:** Abre un puerto para la comunicación entre Drozer y el dispositivo/emulador:
    
    ```bash
    adb forward tcp:3115 tcp:3115
    ```
    
2. **Iniciar Drozer:**  
    Una vez que el puerto está configurado, ejecuta:
    
    ```bash
    drozer console connect
    ```
    
    Esto abrirá la consola interactiva de Drozer.
    

### Superficie de Ataque

Con Drozer, puedes analizar los componentes de una aplicación y detectar vulnerabilidades. Algunos comandos útiles incluyen:

- **Enumerar actividades (activities):**
    
    ```bash
    run app.activity.info -a <nombre_del_paquete>
    ```
    
    Esto muestra todas las actividades expuestas por la aplicación, que podrían ser puntos de entrada para un ataque.
    
- **Explorar la superficie de ataque:**
    
    ```bash
    run app.package.attacksurface <nombre_del_paquete>
    ```
    
    Este comando muestra qué componentes de la app están expuestos (activities, services, content providers, broadcast receivers).
    
- **Ejecutar una actividad específica:** Si encuentras una actividad que parece interesante o potencialmente explotable, puedes ejecutarla directamente:
    
    ```bash
    run app.activity.start --component <nombre_del_paquete> <actividad>
    ```
    

### Ejemplo de Uso con Content Providers

Si una app tiene un proveedor de contenido mal configurado, podrías listar y leer datos con:

```bash
run app.provider.query <uri_del_provider>
```

---

## Relación con Metasploit

Drozer y Metasploit comparten similitudes en su diseño modular y su enfoque en la explotación de vulnerabilidades. Drozer es como "el Metasploit de Android", pero orientado exclusivamente al análisis de aplicaciones móviles.

Algunas diferencias clave:

- **Drozer:** Enfocado en el análisis y explotación de aplicaciones Android.
- **Metasploit:** Enfocado en la explotación de vulnerabilidades en sistemas y redes generales.

---

Hacer un **bypass de Root Detection** en aplicaciones Android usando **Objection** y **FRIDA** es un enfoque común para sortear las protecciones diseñadas para impedir el uso en dispositivos rooteados. Estas técnicas son útiles para analizar aplicaciones que tienen restricciones adicionales cuando detectan un dispositivo con root.

---

### **¿Qué es Root Detection y por qué bypassearlo?**

Muchas aplicaciones utilizan mecanismos de detección de root para evitar que los usuarios ejecuten la app en dispositivos comprometidos. Esto puede incluir la búsqueda de binarios comunes como `su`, la verificación de permisos inusuales, o incluso detectar la presencia de herramientas como Magisk.

Para realizar un análisis dinámico de estas aplicaciones, es necesario desactivar o engañar a estos mecanismos.

---

### **Herramientas necesarias**

1. **FRIDA**: Framework para instrumentación dinámica, que permite modificar el comportamiento de las aplicaciones en tiempo real.
2. **Objection**: Herramienta basada en FRIDA que simplifica tareas comunes como bypass de root detection, SSL Pinning, y más.

---

### **Pasos para el bypass con Objection**

1. **Preparar el entorno:**
    
    - Asegúrate de tener FRIDA y Objection instalados en tu máquina:
        
        ```bash
        pip install frida-tools objection
        ```
        
    - Conecta tu dispositivo Android al PC y asegúrate de que está configurado para depuración ADB.
2. **Iniciar FRIDA-Server en el dispositivo:**
    
    - Descarga la versión adecuada de FRIDA-Server para tu arquitectura (ARM, ARM64).
    - Sube el archivo al dispositivo:
        
        ```bash
        adb push frida-server /data/local/tmp/
        ```
        
    - Dale permisos de ejecución y ejecútalo:
        
        ```bash
        adb shell
        chmod +x /data/local/tmp/frida-server
        ./data/local/tmp/frida-server
        ```
        
3. **Conectar Objection a la app objetivo:**
    
    - Conoce el identificador del paquete de la app que deseas analizar:
        
        ```bash
        adb shell pm list packages | grep <nombre_app>
        ```
        
    - Lanza la app y conéctate a ella usando Objection:
        
        ```bash
        objection -g <nombre_del_paquete> explore
        ```
        
4. **Bypass de Root Detection:**
    
    - Una vez dentro de la consola de Objection, ejecuta:
        
        ```bash
        android root disable
        ```
        
    - Esto buscará funciones y métodos relacionados con la detección de root y los desactivará automáticamente.

---

### **Pasos para el bypass manual con FRIDA**

Si prefieres un enfoque manual o si Objection no logra deshabilitar el root detection automáticamente, puedes usar FRIDA directamente.

1. **Conectar FRIDA a la app:** Ejecuta FRIDA con el paquete de la app:
    
    ```bash
    frida -U -n <nombre_del_paquete>
    ```
    
2. **Crear un script de bypass:** Identifica los métodos de detección de root en el código (por ejemplo, búsquedas de `su`, verificaciones de binarios, o llamadas específicas a métodos). Un ejemplo común podría ser:
    
    ```javascript
    Java.perform(function () {
        var RootDetectionClass = Java.use("com.ejemplo.seguridad.RootCheck");
        RootDetectionClass.isRooted.implementation = function () {
            console.log("Bypassing root detection");
            return false;
        };
    });
    ```
    
3. **Cargar el script en FRIDA:** Guarda el script en un archivo, por ejemplo, `bypass_root.js`, y cárgalo en FRIDA:
    
    ```bash
    frida -U -n <nombre_del_paquete> -s bypass_root.js
    ```
    
4. **Verificar el resultado:** Una vez cargado, FRIDA interceptará las funciones relacionadas con la detección de root y las modificará en tiempo real.
    

---

### **Conclusión**

- **Objection** es la opción más rápida y sencilla para la mayoría de los casos, pero puede fallar si la detección de root está muy personalizada.
- **FRIDA** permite un control más detallado y la capacidad de abordar escenarios más complejos, como root detection basada en múltiples técnicas.

Con cualquiera de estas herramientas, puedes superar la detección de root y continuar con tu análisis dinámico o pruebas de seguridad.