---
title: "Proxychains"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
### **Proxychains**: ¿Qué es y cómo se usa?


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/AuditoriaTecnica/SOCKS|SOCKS]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

**`proxychains`** es una herramienta que permite forzar que el tráfico de una aplicación en tu sistema pase a través de uno o varios servidores proxy (como SOCKS5, SOCKS4 o HTTP). Es útil para realizar pruebas de penetración, navegar de forma anónima o evadir restricciones de acceso a internet. 

**`proxychains`** funciona como un "túnel" para redirigir el tráfico de las aplicaciones de tu sistema a través de servidores proxy. Puedes usarlo con herramientas como `nmap`, `curl`, `dirb`, `ffuf`, etc., para ocultar tu dirección IP y proteger tu identidad mientras realizas pruebas o actividades de investigación en la red.

### **Instalación**

En **Kali Linux** y otras distribuciones basadas en Debian, puedes instalar `proxychains` usando el siguiente comando:

```bash
sudo apt update
sudo apt install proxychains
```

### **Configuración de `proxychains`**

El archivo de configuración de `proxychains` se encuentra en `/etc/proxychains.conf`. Aquí es donde puedes agregar los proxies que utilizarás. El archivo se puede editar con un editor de texto como `nano` o `vim`.

1. **Edita el archivo de configuración**:
   ```bash
   sudo nano /etc/proxychains.conf
   ```

2. **Configuración básica**:
   Dentro de `proxychains.conf`, busca la sección donde se configuran los proxies. Hay dos modos principales:
   - **Dynamic Chain**: Los proxies se usan de manera dinámica. Si un proxy falla, se puede usar el siguiente en la lista.
   - **Strict Chain**: Los proxies se usan en un orden estricto. Si uno falla, todo el proceso se detiene.

   En la parte inferior de `proxychains.conf`, verás algo como esto:

   ```
   # This is the default configuration for proxychains
   # [ProxyList]
   # Format:  type  host  port [user pass]
   ```

   Aquí puedes agregar tus proxies. Los proxies pueden ser de varios tipos, como SOCKS4, SOCKS5 o HTTP. Ejemplo de cómo agregar proxies:

   ```
   # Socks5 proxy
   socks5  127.0.0.1 9050

   # HTTP proxy
   http    192.168.1.1 8080

   # Socks4 proxy
   socks4  10.10.10.10 1080
   ```

   En este caso, `127.0.0.1 9050` podría ser el proxy de **Tor**, por ejemplo. Si usas Tor, asegúrate de que Tor esté corriendo en el puerto adecuado (por defecto 9050 para SOCKS5).

3. **Elige el modo de encadenado (Chain Mode)**:
   - **Dynamic Chain**: Si deseas usar varios proxies y que se intenten en caso de que uno falle, descomenta (quita el `#`) la línea `dynamic_chain` en la configuración. Es el modo más común para proxychains.
   - **Strict Chain**: Si prefieres que el tráfico pase por los proxies en un orden específico, descomenta `strict_chain` y usa ese modo.

### **Uso básico de `proxychains`**

Una vez que hayas configurado tus proxies en el archivo `proxychains.conf`, puedes usar `proxychains` para ejecutar una aplicación a través de los proxies que configuraste.

#### Ejemplo de uso con `curl`:

```bash
proxychains curl http://example.com
```

Esto ejecutará `curl` para acceder a `http://example.com`, pero el tráfico se enviará a través de los proxies que hayas configurado en `proxychains.conf`.

#### Ejemplo con `nmap`:

```bash
proxychains nmap -sT -Pn -p 80 192.168.1.100
```

Este comando ejecuta un escaneo TCP de los puertos de la dirección IP `192.168.1.100`, pero el tráfico de escaneo se envía a través del proxy.

#### Ejemplo con `dirb` o `ffuf`:

Si quieres usar `proxychains` con herramientas como **`dirb`** o **`ffuf`** para hacer un escaneo de directorios, solo debes anteponer `proxychains` al comando de la herramienta.

```bash
proxychains dirb http://example.com /usr/share/wordlists/dirb/common.txt
```

```bash
proxychains ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

### **Comprobando el funcionamiento**

Si quieres verificar que tu tráfico realmente pasa a través de los proxies, puedes utilizar herramientas como `curl` para hacer una consulta a tu IP pública:

```bash
proxychains curl ifconfig.me
```

Esto te mostrará la dirección IP pública desde la cual se realiza la solicitud. Si está configurado correctamente, debería mostrarte la IP del proxy (en lugar de tu IP real).

### **Uso con Tor**

Si quieres usar **Tor** con `proxychains`, debes asegurarte de tener **Tor** corriendo en tu máquina. Tor por defecto usa el puerto `9050` para SOCKS5, lo cual es fácil de configurar con `proxychains`.

1. **Instalar Tor**:

   En **Kali Linux**, puedes instalar Tor con el siguiente comando:

   ```bash
   sudo apt install tor
   ```

2. **Iniciar Tor**:

   Después de instalar Tor, puedes iniciar el servicio Tor con:

   ```bash
   sudo systemctl start tor
   ```

3. **Configurar `proxychains` para usar Tor**:

   Abre el archivo de configuración de `proxychains`:

   ```bash
   sudo nano /etc/proxychains.conf
   ```

   Luego, agrega la siguiente línea al final del archivo (si no está ya configurado):

   ```
   socks5  127.0.0.1 9050
   ```

4. **Verificar con Tor**:

   Ahora puedes usar `proxychains` junto con cualquier herramienta para navegar de forma anónima a través de Tor. Por ejemplo:

   ```bash
   proxychains curl ifconfig.me
   ```

   Esto debería mostrarte la IP de la red Tor, en lugar de tu dirección IP real.

---

### **Problemas comunes y soluciones**

1. **La aplicación no se conecta**:
   - Asegúrate de que Tor o el servidor proxy esté funcionando correctamente.
   - Revisa que hayas configurado correctamente el archivo `proxychains.conf` y que no haya errores de sintaxis.
   - Verifica que el puerto del proxy no esté bloqueado por un firewall.

2. **El tráfico sigue sin pasar por el proxy**:
   - Comprueba si la herramienta que estás usando es compatible con el uso de `proxychains` (algunas aplicaciones no funcionan bien con proxies).
   - Intenta usar `proxychains` con la opción `-f` para forzar el uso del proxy.

3. **Problemas con proxies HTTP**:
   - Algunos proxies HTTP pueden no ser compatibles con ciertos tipos de tráfico. Intenta usar SOCKS5 en su lugar si es posible.

---

### **Conclusión**

**`proxychains`** es una herramienta poderosa para realizar pruebas de penetración o navegar de forma anónima a través de proxies. Es especialmente útil cuando se realiza un escaneo o un ataque y se desea ocultar la dirección IP o evadir restricciones de acceso a internet. Asegúrate de configurar correctamente los proxies en `proxychains.conf` y usa el comando `proxychains` antes de las aplicaciones que desees redirigir.

Si tienes más preguntas o necesitas ayuda adicional, ¡no dudes en preguntar!