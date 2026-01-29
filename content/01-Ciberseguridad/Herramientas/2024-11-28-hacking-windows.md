---
title: "Active Directory y Kerberos"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---

# Active Directory y Kerberos

> **Relacionado**: [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Herramientas/Reconocimiento/DCsync|DCsync]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/NMAP|NMAP]].

![[Pasted image 20250727203426.png]]
Active Directory funciona de la siguiente manera: utiliza **Kerberos**, un protocolo que usa **Windows** para autenticarse. Su funcionamiento es el siguiente:

1. **Envío de Solicitud TGT**: Se envía una solicitud TGT (Ticket Granting Ticket).
2. **Controlador de Dominio**: El controlador de dominio gestiona el acceso y se divide en dos partes:
    - **AS (Autenticación)**: Se encarga de la autenticación del usuario.
    - **TGS (Ticket Granting Service)**: Da acceso a los diferentes servicios que ofrece el dominio.
3. **Servidor de Servicios (SS)**: Solicita al servidor un ticket TGT. Si es correcto, se envía el TGT más una clave de sesión.
4. **Solicitud TGS**: El cliente luego envía una solicitud TGS para poder acceder a los servicios. Esta solicitud está autenticada con un "ticket hash".

---

## Ataque Golden Ticket

Un **Golden Ticket** se compone de un ticket TGS más un ticket TGT. El ticket TGT es el que solicita el ticket TGS.

**Debilidades** de Kerberos:

- La seguridad depende del **TGT**. Si tienes acceso al TGT, el sistema está comprometido.
- La clave **KRBTGT** es la más importante. Si obtienes esta clave, tienes control total del dominio, ya que esta clave es la que gestiona todos los tickets.
- Las claves de usuario también son importantes, así como la clave de servicio que reside en el servidor que presta el servicio.

El cifrado que utiliza Kerberos presenta debilidades. Utiliza algoritmos como **RC4-HMAC** o **DES** para cifrar las contraseñas, lo que es vulnerable a ataques. Se puede usar **Mimikatz** para obtener los **hashes** de las contraseñas.

---

## Problemas con KRBTGT

- **KRBTGT** nunca cambia, excepto en casos de actualización de dominio o si el sistema está comprometido. Si tienes acceso a esta cuenta, puedes controlar todo el dominio, sin que el resto de los usuarios se enteren, aunque cambien sus credenciales.

---

## Conclusión

Una vez que se obtiene un ticket **TGT**, se puede obtener un **TGS** cuando se monta un **Active Directory**.

- El servicio TGS no valida la información más allá de 20 minutos después de que se emite el TGT. En Windows, este tiempo es de 10 horas.
- Un atacante puede generar tickets TGT y acceder a otros servicios, sin que se detecte, ya que los tickets no dejan registros visibles.

---

## Kerberos y Fuerza Bruta

Kerberos es susceptible a **ataques de fuerza bruta**. Herramientas como **Kerbrute** pueden ser utilizadas para intentar adivinar contraseñas. Un comando de ejemplo sería:

```bash
python3 kerbrute -d -ip 192.168.109.128 -domain tfm.ucj -user usuarios -outputuser cnum_user.txt
```

El parámetro **usuarios** se usa para guardar los posibles usuarios que existen, incluso si no se tiene la contraseña.

---

## Ataques Adicionales

1. **ASREPRoast**: Existen cuentas que no requieren autenticación Kerberos. Se pueden buscar estas cuentas que no realizan este tipo de autenticación.
    
2. **Tools**: Herramientas como **BloodHound** y **Mimikatz** pueden ser utilizadas para obtener hashes de usuarios que no necesitan autenticación Kerberos.
    

---

## Pass the Hash

**Pass the Hash** es una técnica en la que se inyecta un **hash** de una contraseña, permitiendo el acceso a otros equipos. Con la herramienta **Mimikatz**, se pueden extraer hashes dentro de un servidor de dominio.

---

## Enlaces de Referencias

- [Kerberos Authentication Protocol](https://en.wikipedia.org/wiki/Kerberos_(protocol))
- [Mimikatz: A Post-Exploitation Tool](https://github.com/gentilkiwi/mimikatz)
- [Pass the Hash: Explanation and Methods](https://www.cyberark.com/resources/threat-research-blog/what-is-pass-the-hash)
¡Claro! Aquí tienes el texto corregido y con una estructura más clara, con el formato adecuado para Obsidian, como si fuera un documento de estudio:

---

# **Pass the Ticket y Golden Ticket**

**Pass the Ticket (PTT)** y **Golden Ticket** son técnicas utilizadas en el protocolo **Kerberos** para obtener acceso a los servicios de un dominio mediante la manipulación de tickets de autenticación.

## **Pass the Ticket (PTT)**

**Pass the Ticket** funciona de manera similar a **Pass the Hash**, pero en lugar de utilizar un hash de contraseña, se utilizan **tickets** de autenticación de **Kerberos**. La principal diferencia es que, en este caso, los atacantes manipulan los tickets de autenticación para acceder al dominio y servicios.

- **TGT (Ticket Granting Ticket)**: Con este ticket, el atacante puede acceder al dominio.
- **TGS (Ticket Granting Service)**: Con este ticket, el atacante puede acceder a un servicio específico dentro del dominio.

Los tickets de Kerberos tienen la extensión `.kirbi`. Una forma sencilla de inyectar estos tickets es utilizar una herramienta en **Kali Linux** para inyectar el ticket y obtener acceso al dominio.

### Ejemplo de comando para inyectar el ticket:

```bash
kerberos_ptt_dir ticket.kirbi
```

Una vez inyectado el ticket, el atacante obtiene acceso al dominio de manera similar a los ataques de **Pass the Hash**, pero en lugar de hashes de contraseñas, utiliza los tickets de Kerberos.


## **Golden Ticket**

El **Golden Ticket** es un tipo de ataque en el que el atacante crea un **TGT** falso, lo que le permite obtener acceso total al dominio, incluso sin tener una cuenta de usuario válida.

### **Componentes de un Golden Ticket**:

1. **Cuenta KRBTGT**: Esta es la cuenta crítica, ya que es responsable de la emisión de los tickets dentro del dominio.
2. **SID de dominio**: El **SID** (Security Identifier) es un identificador único de seguridad para identificar el dominio dentro de **Active Directory**.
3. **PAC (Privilege Attribute Certificate)**: El **PAC** contiene información sobre el usuario y sus privilegios. Este certificado es clave para generar un **Golden Ticket**.

### **¿Cómo Funciona?**

El atacante puede crear un **Golden Ticket** si obtiene el **hash de la cuenta KRBTGT**. Además, se necesita el **SID** del dominio y otros identificadores relacionados con el dominio, como el **ID del administrador**.

- Cuando un **administrador** inicia sesión en un sistema, puede obtener el hash de la cuenta **KRBTGT**, lo cual es esencial para crear un Golden Ticket.
- El **PAC** contiene atributos como el **nombre de usuario**, **SID de dominio**, **ID de administrador** y los **dominios de grupo** a los que pertenece el usuario.

### **Ventajas del Golden Ticket**:

La principal ventaja de un **Golden Ticket** es que permite al atacante acceder al dominio **sin necesidad de una cuenta válida**. El ticket creado parece legítimo, por lo que no genera alertas.

El **TGT** tiene una duración predeterminada de **10 horas**, lo que le da al atacante un tiempo considerable para realizar sus acciones sin ser detectado. A menos que se haya activado un sistema de detección de **anomalías en Kerberos**, este ataque puede pasar desapercibido. De forma predeterminada, no se activan estas medidas de detección, lo que hace necesario realizar un **hardening** de seguridad para proteger el entorno.

---

## **Detección y Mitigación**

Si no se ha configurado un sistema de **detección de Kerberos**, como un sistema de monitoreo avanzado, el **Golden Ticket** puede ser difícil de detectar. Sin embargo, si se implementan medidas de **hardening** en el entorno de **Active Directory**, se puede reducir el riesgo de este tipo de ataques.

---

## **Enlaces de Referencia**

- [Kerberos Authentication Protocol](https://en.wikipedia.org/wiki/Kerberos_(protocol))
- [Pass the Ticket: Explanation and Methods]([https://www.sans.org/](https://www.sans.org/)
### **Silver Ticket**

Un **Silver Ticket** es otro tipo de ataque relacionado con **Kerberos**, pero a diferencia del **Golden Ticket**, un **Silver Ticket** se utiliza para acceder a un servicio específico dentro de un dominio, en lugar de obtener acceso completo al dominio.

### **¿Cómo Funciona un Silver Ticket?**

Los **Silver Tickets** son similares a los **TGTs (Ticket Granting Tickets)**, pero están restringidos a un servicio específico, lo que significa que solo permiten el acceso a ese servicio y no al dominio en general. El atacante crea un ticket falso para un servicio específico, lo que le permite interactuar con ese servicio como si fuera un usuario legítimo.

El proceso de creación de un Silver Ticket implica los siguientes pasos:

1. **Obtención de la clave de servicio**: Para crear un Silver Ticket, el atacante necesita obtener la **clave del servicio** correspondiente al servicio que quiere acceder. Esta clave es compartida entre el servicio y el controlador de dominio.
    
2. **Generación del Silver Ticket**: Usando la clave de servicio obtenida, el atacante genera un **Silver Ticket** válido, que contiene información sobre el servicio al que se quiere acceder, como el nombre del servicio, el nombre del servidor y el nombre de dominio.
    
3. **Acceso al servicio**: El atacante inyecta el **Silver Ticket** en su sesión y lo usa para autenticarse con el servicio en cuestión. El ticket es enviado al servidor de destino, que lo valida usando la clave secreta del servicio.
    

### **Diferencias entre Silver Ticket y Golden Ticket**

- **Golden Ticket**: Un **Golden Ticket** permite acceso completo al dominio, ya que utiliza un **TGT** que es válido para cualquier servicio dentro del dominio. El atacante tiene control total y puede moverse libremente por el entorno.
    
- **Silver Ticket**: Un **Silver Ticket** solo permite acceso a un servicio específico y no al dominio completo. El atacante necesita obtener la **clave de servicio** correspondiente para crear el ticket.
    

### **Ventajas del Silver Ticket**

- **Acceso limitado**: A diferencia del Golden Ticket, un Silver Ticket no da acceso completo al dominio, lo que limita el impacto del ataque.
    
- **Más difícil de detectar**: Los **Silver Tickets** son más difíciles de detectar que otros ataques como el **Pass the Ticket**, porque se utilizan solo para servicios específicos y no afectan la autenticación a nivel de dominio.
    
- **No requiere control de la cuenta KRBTGT**: A diferencia de un Golden Ticket, un Silver Ticket no requiere la obtención del **hash de la cuenta KRBTGT** (la cuenta que controla los TGTs), lo que hace que el ataque sea más sencillo en términos de la cantidad de información que necesita ser comprometida.
    

### **Cómo Detectar un Silver Ticket**

La detección de un Silver Ticket puede ser más complicada debido a su naturaleza, pero existen algunas señales que pueden indicar un ataque de este tipo:

1. **Errores en el servicio**: Si un servicio empieza a generar errores inusuales en la autenticación, puede ser un signo de que un Silver Ticket ha sido utilizado para acceder de manera no autorizada.
    
2. **Inyección de tickets**: Los administradores deben monitorear la inyección de tickets Kerberos en las sesiones de los usuarios, ya que los Silver Tickets a menudo se inyectan manualmente en la memoria de un atacante.
    
3. **Revisión de logs**: Es importante revisar los registros de eventos de Kerberos en los controladores de dominio y servidores, ya que pueden haber registros que indiquen un uso indebido de tickets en servicios específicos.
    

### **Mitigación de Ataques con Silver Tickets**

1. **Hardening de los servicios**: Asegúrese de que los servicios clave estén configurados adecuadamente y que solo los usuarios autorizados tengan acceso a las claves de servicio.
    
2. **Monitoreo activo**: Implementar un sistema de monitoreo de Kerberos para detectar actividades sospechosas relacionadas con la autenticación.
    
3. **Rotación de claves**: Cambiar las claves de servicio regularmente para dificultar la generación de Silver Tickets.
    
4. **Protección de las cuentas privilegiadas**: Las cuentas privilegiadas, como los administradores del dominio, deben protegerse y monitorearse de cerca para evitar que los atacantes obtengan acceso a las claves necesarias para crear Silver Tickets.
    

### **Conclusión**

El **Silver Ticket** es una herramienta poderosa para los atacantes, ya que les permite acceder a servicios específicos dentro de un dominio de manera muy controlada y difícil de detectar. A diferencia de los Golden Tickets, los Silver Tickets no otorgan acceso completo al dominio, pero siguen siendo una amenaza importante en un entorno de red. La clave para defenderse de este tipo de ataques es aplicar buenas prácticas de seguridad, como la rotación de claves y el monitoreo continuo de la red.

¡Entendido! Voy a corregir el texto de manera más clara y sencilla, y a organizarlo para que sea fácil de entender y estudiar como estudiante. Aquí te dejo la corrección:

---

# Auditoría de Servicios y Herramientas Comunes

En una auditoría de seguridad, se utilizan diversas herramientas para identificar posibles vulnerabilidades. Aparte de **Nmap** para explorar los servicios en la red, existen técnicas y herramientas adicionales que permiten realizar ataques y descubrir más sobre la red.

## LLMNR Poisoning

**LLMNR (Link-Local Multicast Name Resolution)** es un protocolo de **Microsoft** similar al **DNS**. Si una red es vulnerable a LLMNR, puedes aprovecharlo para realizar un **ataque de Hombre en el Medio (MitM)**. Esto permite interceptar la comunicación entre los dispositivos y obtener las credenciales de los usuarios, como los **hashes** de las contraseñas.

### Herramientas útiles para LLMNR Poisoning:

- **Responder**: Esta herramienta permite realizar el ataque de **Hombre en el Medio** de manera automática. Puedes usar el siguiente comando para ejecutarla:
    
    ```bash
    responder -I eth0 -dx
    ```
    
- **Hashcat**: Después de capturar los hashes con **Responder**, puedes usar **Hashcat** para intentar **crackear** las contraseñas.
    

## Impacket

**Impacket** es una colección de herramientas utilizadas para realizar ataques en redes **Windows**. Puedes instalar **Impacket** con el siguiente comando:

```bash
sudo apt install impacket impacket-herramientas
```

Si prefieres la versión más actualizada, puedes descargar **Impacket** desde **GitHub**, aunque puede ser más complicado de configurar.

### Herramienta psexec.py

Una de las herramientas más conocidas dentro de **Impacket** es **psexec.py**, que permite ejecutar comandos remotamente en un sistema **Windows**. Para utilizarla, debes ejecutar el siguiente comando:

```bash
psexec.py user1:password@ip
```

Este comando te dará acceso a la terminal del sistema **Windows**.

### MSFConsole (Metasploit)

Otra opción es usar **Metasploit** (MSFConsole), que también permite ejecutar el comando **psexec** para obtener acceso a la máquina objetivo.

```bash
msfconsole
```

En **Metasploit**, puedes usar **PowerShell** para ejecutar comandos de forma remota en el sistema comprometido.
Aquí tienes tu texto corregido y formateado:

---

## NTLM Relay Attack

Un **NTLM Relay Attack** es una técnica en la que se intercepta una **solicitud de autenticación NTLM** y se redirige a un servidor objetivo. Para esto, es necesario modificar el archivo **responder.conf**. Puedes usar la herramienta **ntlmrelayx** (incluida en **Impacket**) para realizar este ataque. Esta herramienta también es compatible con **Samba**.

Ejemplo de uso:

```bash
ntlmrelayx.py -tf target.txt -smb2support
```

Este comando permite realizar el ataque **Relay** sobre los objetivos especificados.

---

## Password Spraying

El **Password Spraying** es una técnica en la que se intenta acceder a varias cuentas utilizando una misma contraseña común. Una herramienta útil para esta técnica es **CrackMapExec**, aunque actualmente está algo desactualizada. La herramienta más utilizada ahora es **Nets**.

Con **Nets**, puedes verificar si las máquinas en la red tienen servicios como **Samba**, que podrían ser vulnerables a este tipo de ataques.

---

## Volcado de Hashes

Si necesitas obtener los **hashes** de las contraseñas de una máquina **Windows**, puedes usar la herramienta **secretdump** de **Impacket**. Esta herramienta permite extraer los hashes de las contraseñas almacenadas en la máquina.

Ejemplo de uso:

```bash
secretdump.py -target <IP>
```

Otra herramienta útil para pruebas relacionadas con contraseñas es **kerbrute**, y **getuserspn** permite realizar consultas para obtener información sobre los servicios de un dominio. Por ejemplo, el parámetro `-O` en **getuserspn** se usa para optimizar y realizar la tarea con múltiples hilos.

---

## Dumping Hashes con Mimikatz

Con **Mimikatz**, puedes extraer hashes entrando en **modo debug**. Por ejemplo:

1. Habilita el modo debug con el comando:
    
    ```bash
    mimikatz privilege::debug
    ```
    
2. Extrae los hashes del archivo **SAM** o del Local Security Authority (LSA).
    

Si no puedes usar **Mimikatz**, otra opción es **Rubeus**. Con esta herramienta puedes ejecutar **DCSync** para obtener la cuenta **KRBTGT** y realizar ataques avanzados como **Over-Pass-The-Hash** (convirtiendo hashes en tickets).

---

## AS-REP Roasting

El **AS-REP Roasting** se utiliza para atacar cuentas de un dominio que no tienen habilitada la preautenticación en Kerberos. Con herramientas como **Rubeus**, puedes capturar los hashes necesarios sin necesidad de autenticación previa.

---

## MITM6

**mitm6** es una herramienta para realizar ataques de "hombre en el medio" (MITM) en redes IPv6.

---

## PowerView

**PowerView** es una herramienta de PowerShell que permite recopilar información sobre un dominio. Si tu script no está firmado y PowerShell te bloquea, puedes utilizar el siguiente comando para evitar restricciones:

```bash
powershell -ep bypass
```

Con **PowerView**, puedes interactuar con el dominio y el controlador de dominio. Por ejemplo:

- Usar `Get-NetUser` para enumerar usuarios.
- Consultar políticas de grupo (GPO) con `Get-NetGPO`.
- Analizar políticas de contraseñas del dominio.

También puedes utilizar **BloodHound** y su herramienta auxiliar **SharpHound** para recopilar datos sobre el dominio. BloodHound utiliza **Neo4j**, una base de datos de grafos, para representar gráficamente las relaciones entre usuarios, computadoras y permisos en el dominio.

---

Espero que este formato y correcciones sean útiles para ti. ¡Avísame si necesitas algo más!