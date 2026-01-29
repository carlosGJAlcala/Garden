---
title: "Ssltrip"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---
**SSLStrip** es una herramienta que se utiliza en ataques de **Man-in-the-Middle (MITM)** con el fin de interceptar y modificar el tráfico de HTTPS (comunicaciones cifradas) entre un cliente y un servidor, y degradarlas a HTTP (sin cifrado). El ataque se lleva a cabo escuchando en un puerto específico y modificando las solicitudes HTTPS para que sean solicitudes HTTP, sin cifrar, lo que permite al atacante ver y modificar el tráfico entre el cliente y el servidor.

Aquí te explico en detalle lo que describes:

### ¿Cómo funciona SSLStrip?


> **Relacionado**: [[01-Ciberseguridad/Fundamentos/redes/IPTables|IPTables]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]].

1. **Previa condición de MITM**: Para ejecutar **SSLStrip**, es necesario que el atacante haya logrado previamente un ataque **Man-in-the-Middle (MITM)**. Esto significa que el atacante está interceptando la comunicación entre el cliente y el servidor.

2. **Escuchar en un puerto específico**: SSLStrip escucha en un puerto determinado (por lo general, el puerto **8080**) y redirige el tráfico entrante de HTTPS a HTTP. Esto lo hace cambiando las URLs de **HTTPS** a **HTTP** mientras el tráfico pasa a través del atacante.

3. **Redirección de tráfico (iptables)**: Para hacer que el tráfico que originalmente va a un servidor HTTPS (por ejemplo, en el puerto 443) sea redirigido al puerto en el que SSLStrip está escuchando (usualmente el puerto 8080), se utiliza el siguiente comando en el sistema del atacante:

   ```bash
   iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080
   ```

   Este comando realiza lo siguiente:
   - **`-t nat`**: Especifica que la acción se hará en la tabla de NAT (Network Address Translation), que es la que maneja las redirecciones de tráfico.
   - **`-A PREROUTING`**: Añade una regla en la cadena `PREROUTING`, que se aplica antes de que el tráfico sea procesado.
   - **`-p tcp`**: Aplica la regla a tráfico TCP.
   - **`--destination-port 80`**: Filtra el tráfico cuyo puerto de destino sea el puerto 80, es decir, el puerto estándar de HTTP.
   - **`-j REDIRECT`**: La acción que se tomará es redirigir el tráfico.
   - **`--to-port 8080`**: El tráfico redirigido será enviado al puerto 8080, donde SSLStrip está escuchando.

   Este comando esencialmente hace que todo el tráfico HTTP sea redirigido a un puerto donde el atacante puede manejarlo y alterar la solicitud.

4. **Cambio de HTTPS a HTTP**: SSLStrip realiza una modificación en las solicitudes, eliminando la "s" del protocolo HTTPS para hacer que la comunicación se realice en HTTP. Esto permite al atacante interceptar las credenciales, cookies y otros datos sensibles sin cifrado, ya que la conexión ya no es segura.

5. **Redirección a HTTPS (opcional)**: Aunque el atacante elimina el "s" de la URL, algunas veces también se puede hacer que el tráfico se redirija nuevamente a un servidor HTTPS legítimo después de que ha pasado por el atacante, sin que el cliente se dé cuenta de que el tráfico no fue seguro en el camino.

### Limitaciones y Mitigaciones

1. **HSTS (HTTP Strict Transport Security)**: Muchos navegadores modernos implementan **HSTS**, una política de seguridad que obliga a los sitios web a solo comunicarse a través de HTTPS después de la primera conexión exitosa. Si el navegador ve que el servidor envía la cabecera `Strict-Transport-Security`, no permitirá que se cambie la conexión a HTTP, lo que mitiga el ataque.

2. **Certificados SSL válidos**: Si el servidor usa un certificado SSL válido y el cliente verifica la validez del certificado, el atacante no podrá hacer que el tráfico se degrade a HTTP sin que el navegador muestre un error de certificado. En este caso, SSLStrip no podría realizar el ataque con éxito.

3. **Autenticación mutua y otros mecanismos de seguridad**: Algunos sistemas pueden usar autenticación mutua o incluso conexiones VPN para protegerse de ataques de este tipo.

### Consideraciones éticas

Es importante recordar que realizar ataques MITM, incluido el uso de herramientas como **SSLStrip**, es ilegal y está prohibido en la mayoría de las jurisdicciones sin el consentimiento explícito de las partes involucradas. Los ataques de este tipo se realizan con fines maliciosos, y su uso no autorizado puede tener consecuencias legales graves.

Este tipo de vulnerabilidad se puede mitigar con buenas prácticas como el uso de HTTPS en todas las páginas, habilitar HSTS, y educar a los usuarios sobre los riesgos de conexiones inseguras.