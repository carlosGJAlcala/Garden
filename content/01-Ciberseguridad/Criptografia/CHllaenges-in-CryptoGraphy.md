---
title: "Chllaenges In Cryptography"
date: 2026-01-26
tags:
  - ciberseguridad
  - criptografia
---


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/ONOS|ONOS]]. [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]].

* La criptografía es un campo que reúne muchos aspectos tanto a nivel legislativo, matemático y de computer sciences, en una charla  de ellos puedes escuchar muchos temas
* Este articulo presenta grandes desafíos dentro del mundo de la criptografía

WHAT IS  CRYPTOGRAPHY
	* El corazón de la criptografía son los protocolos y los algoritmos que proporciona Confidencialidad, Integridad, fuente de Autentificación y firmados digitales
	* El más común de los requisitos es la de un canal seguro que proporcione  confidencialidad, integridad y la autentificación. Podría usar encriptación simétrica y verificar la integridad con HMAC, pero tiene el problema de como compartir la clave simétrica.
	* Este problema se ve aliviado con soluciones de encriptación asimétrica como puede ser usar elliptic curve diffie hellman ECDH o RSA.
	* otro problema que surge es cuando autentificas la clave publica con la cual quieres empezar hacer la comunicación y como se distribuyen esas, para eso se utiliza  PKI public key infraestructura en la que están los certificados firmados por la CA.
	* TLS sigue lo que hemos descripto anteriormente y es usado ampliamente. otro protocolo que utiliza encriptación punto a punto es signal que se usa por ejemplo en la aplicación de mensajería que es whasap, autentifica  los teléfonos moviles a sus proveedores, también se utiliza para securizar el emparejamiento en bluetooth
	* Los fundamentos de la encriptación proporciona una gran cantidad de solución tale como cifrar discos , firmas digitales y cripto monedas. Tambien hay primitivas más sofisticadas  autenticación basada en contraseñas cifradas, [[Encriptacion-homomorfica]], ofuscación y indistinguible
	* La criptografía es casi siempre necesario para el tema de la seguridad de datos sensibles, si embargo no es una igualdad de seguridad, ya que se puede dar caso de ataques de phising , de malware, ect que comprometa la seguridad del sistema.
	* aunque si se descubre una brecha en alguno de estos algoritmos de cifrado o se comprometieran por el tamaño de la clave, puede generar problemas muy graves.
CHALLENGES
		STANDARDIZED CRYPTOGRAPHY
			* Hay dos tipos de estándares el primero es el bloque de núcleo especifican primitivas criptográficas y protocolos básicos y luego están los de aplicación como puede ser TLS 1.3 , los estándares son bastante importante porque promociona el uso de criptográfica solida, pero estos estándares suelen tardar años en aprobarse
			* un hito fue la implementación del tls 1.3 que incorpora como obligatorio ECDH para cliente servidores, desde 1994 se sabe que los ordenares cuánticos pueden romper tanto como RSA como ECC, por lo que el NSI esta haciendo un gran esfuerzo por crear guantum safe key encapsulation and signature shecmes para remplazarlos.
		IMPLEMENTACION
			* Las operaciones criptográficas pueden tener un efecto muy grande en cuanto al rendimiento y muchas primitivas no se puede implementar en IOT como el internet de la cosas tal como las etiquetas de identificación de radiofrecuencia.
			* Dependiendo del entorno tambien hay que tener en cuenta que no se vulnerable ataques de side channel
			* Un ejemplo de parar un side channel es evitar que el tiempo de generación sea distinto dependiendo de la clave y que el número de operaciones sean constantes
		KEY MANAGEMENT
			* la distribución y alogamiento de la claves que no es algo sencillo, en algunos casos se utiliza la criptográfica simétrica como es GSM el sistema de comunicaciones móviles donde un fabricante de tarjetas sim selecciona una clave secreta y la inserta en una tarjeta sim que se entra a un cliente y tambien entrega de forma segura al fabricante,, esta clave se utiliza para autenticar que el móvil es cliente del proveedor de servicios, no van cifrados de punto a punto ya que los proveedores tienen acceso a los datos de voz.
			* TlS  provee punto a punto y la autentificación es una dirección el servidor se autentifica para el cliente pero no al revés , para esto se utiliza certificados que claves publicas firmadas por una CA .El funcionamiento de la CA consiste en que cuando se hace una petición al servidor este le envía el certificado firmado por una CA intermedia en el navegador hay un certificado raíz que autentifica la ca intermedia y con la ca intermedia se autentifica  el servidor.
			* Esto puede llevar a un problema en el cual un CA autentifique a cientos de CA maliciosos, esto paso en el 2011 en el cual se descubrió que DigiNotar tenía cientos de certificados falsos.
			* Hay muchas iniciativas para mejorar el tema de la seguridad de los certificados, por ejemplo está el foro CA/browser que hace una guía dentro de la industria relativas a la gestión y la emisión. Luego esta un proyecto de Google "Certifacte Transparency project". Tambien hay que gestionar el tema de la revocación de certificados CRL, ya que no debería confiarse mas en unos certificados después de una brecha , por ejemplo más 500,000 certificados fueron comprometidos debido [[Heartbleed-bug]]
		Advance Cryptography
			* El nucleo de la criptografía es entre dos, la criptografía puede ser usada entre mas de dos partes, por ejemplo el protocolo signal se utiliza para conversaciones grupales y ni la misma aplicación puede saber  que determinados  usuarios forman el grupo.
			* Tambien habido estudios teóricos que no se han empezado a usar hasta hora como son la privacidad diferencia (técnicas matemáticas que permiten analizar un conjunto de datos, manteniendo siempre la [privacidad de los datos](https://protecciondatos-lopd.com/empresas/privacidad-datos/))
			* Tambien está el estudio teórico de poder firmar mensajes con firmas compartidas por diferentes dispositivos 
			
			
