---
title: "2025 02 13 Tpm Uefi Y Sistemas Anticheat"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---
Quien vigilará a esto vigilante
- tpm
- uefi
- antimalware 
- anti cheats 
- drm


### Debate sobre si cada agente de seguridad es efectivo o tiene demasiado poder, y si puede limitar los privilegios sin reducir sus propiedades. Individualizar en 1 o 2 párrafos por tema


> **Relacionado**: [[01-Ciberseguridad/Redes-Protocolos/Vulnerabilidades-y-Amenazas/GanarAcceso/Rootkits|Rootkits]]. [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Forense/guia/Forense-de-memoria-de-sistema-completo|Forense de memoria de sistema completo]].

**TPM**  
Está basada en la seguridad del procesador y tiene partes criptográficas. Surgió en 1999, y en 2003 se generó un nuevo modelo. El modelo actual es el 2.0. Sus motivaciones eran asegurar el arranque seguro y detectar la autenticación.

El funcionamiento se basa en el procesador, el firmware y dos memorias. Guarda claves persistentes y valores temporales, compara los valores hash y, si detecta un cambio, se produce un bloqueo del sistema y se activan una serie de alertas.

**Protección de claves de cifrado**  
Los _Attestation Keys_ permiten la autenticación. TPM permite identificar un dispositivo en una red. Tiene una función que es...

---

**Anticheats**  
Los sistemas anticheat surgen como respuesta a la creciente problemática del fraude en videojuegos multijugador, donde hay jugadores que buscan obtener ventajas injustas mediante el uso de software de terceros, exploits o modificaciones en la memoria del juego. Este fenómeno, obviamente, afecta negativamente la experiencia de los jugadores que quieren jugar de manera legítima, compromete la integridad de las competiciones y puede tener implicaciones económicas significativas en títulos donde las principales fuentes de ingresos son las microtransacciones, las competiciones profesionales o los conocidos _juegos como servicio_.

Funciona como un antivirus.  
La detección se basa en firma, comportamiento y monitorización de memoria.

Los privilegios pueden ser en modo usuario o en modo kernel, que tiene permisos de root. Estos sistemas están en software como _Vanguard_ o _Easy Anti-Cheat_.

---

**Antimalware**  
Sirve para prevenir malware. El primero fue _Creeper_. Se puede clasificar en varias categorías:

- **Antivirus**
- **Antispyware**
- **Antiransomware**

Con herramientas avanzadas se puede detectar el comportamiento del malware. Luego está el tema del _sandboxing_.

Los privilegios que tiene el antimalware requieren permisos de root. Es una herramienta esencial, pero su funcionamiento depende de las actualizaciones.

---

DRM (Digital Rights Management)
El gestor de derechos digitales es un conjunto de tecnologías y mecanismos que buscan proteger los derechos de autor y evitar la distribución ilegal de contenidos digitales, como música, películas, libros electrónicos o software. Su objetivo principal es limitar las formas en que los usuarios pueden acceder, copiar o compartir contenidos, con la finalidad de combatir la piratería.

El DRM suele cifrar el contenido protegido y permitir su descifrado únicamente bajo condiciones autorizadas, por ejemplo, cuando el usuario tiene una licencia válida. En la actualidad, muchas soluciones DRM utilizan claves de producto y sistemas de verificación en línea, donde el dispositivo cliente consulta a servidores en la nube para validar permisos y autorizar el acceso al contenido. Algunos sistemas DRM incluso restringen el acceso a funciones básicas del dispositivo, como copiar archivos al sistema de archivos o ejecutar aplicaciones externas.

En algunos casos, los sistemas DRM han sido criticados porque funcionan de forma similar a un rootkit, insertándose profundamente en el sistema operativo, ocultando su presencia y operando con altos privilegios. Esto puede obligar al usuario a mantener una conexión permanente a Internet para verificar licencias, dificultar la compatibilidad con nuevas versiones de software o hardware, e impactar negativamente en la experiencia de usuario, incluso para quienes han adquirido legalmente los contenidos.

TPM (Trusted Platform Module)
El TPM es un chip dedicado a la seguridad que incorpora capacidades criptográficas y está diseñado para proteger la integridad del sistema desde el nivel más bajo. Su origen se remonta a 1999 y en 2003 se publicó un modelo revisado. El modelo actual es TPM 2.0, que incluye mejoras significativas en funcionalidad y seguridad respecto a versiones anteriores.

Entre las principales motivaciones de su desarrollo están la protección del arranque seguro (Secure Boot), asegurando que el sistema operativo y su configuración inicial no hayan sido manipulados antes de la ejecución, y la posibilidad de utilizar el TPM como módulo de autenticación que almacena claves criptográficas seguras.

El funcionamiento de un TPM se basa en una combinación de hardware especializado (el propio procesador del TPM), firmware y dos tipos de memoria:

Una memoria persistente donde almacena claves maestras y otros elementos críticos de forma duradera.

Una memoria volátil para valores temporales, como resultados de cálculos o estados intermedios.


El TPM mide y almacena valores hash de componentes críticos del sistema (por ejemplo, la configuración del firmware, bootloader, kernel). Si en una verificación posterior detecta que estos valores han cambiado de forma no autorizada, puede bloquear el sistema y emitir alertas, protegiendo así la integridad del arranque.

Uno de los problemas prácticos que plantea el TPM es que limita la instalación de sistemas operativos y de software, ya que para arrancar o instalar pueden requerirse configuraciones o firmas específicas. Esto puede restringir la libertad del usuario final, dificultar la instalación de distribuciones de Linux o versiones personalizadas de Windows en dispositivos donde el fabricante ha impuesto políticas estrictas basadas en TPM 2.0.


---

Sistemas anticheat
Los sistemas anticheat surgen para contrarrestar la creciente problemática del fraude en videojuegos multijugador, donde ciertos jugadores utilizan programas de terceros, exploits o modificaciones de memoria para obtener ventajas ilegítimas.

Este tipo de trampas afecta gravemente la experiencia de juego de usuarios legítimos, compromete la integridad de las competiciones online y puede tener un impacto económico significativo en videojuegos cuyo modelo de negocio depende de microtransacciones, competiciones profesionales o del modelo game-as-a-service.

Algunos anticheats funcionan en el nivel más bajo del sistema operativo, con capacidades semejantes a rootkits:

Monitorean el sistema en busca de procesos sospechosos o modificaciones en la memoria del juego.

Acceden a áreas sensibles del sistema, como el kernel, para dificultar que sean engañados o desactivados.


Esto genera un problema importante: amplían la superficie de ataque al ejecutarse con altos privilegios, lo que implica que una vulnerabilidad en el propio sistema anticheat podría ser aprovechada para comprometer el dispositivo del usuario. Además, afectan a la privacidad y la experiencia de usuario, ya que pueden generar conflictos de compatibilidad y forzar restricciones adicionales en el sistema