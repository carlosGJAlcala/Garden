---
title: "2025 01 30 Arbol De Ataque"
date: 2026-01-26
tags:
  - ciberseguridad
  - desarrollo-seguro
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[01-Ciberseguridad/Fundamentos/seguridadWebYAuditoria/seguridad-web-y-auditoria|seguridad web y auditoria]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[01-Ciberseguridad/Criptografia/12-Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

- Desvelar un mensaje privado
	- Recoger datos antes de cifrarse.  (Aceptar)
		- Infectar a la victima (Aceptar)
			- Hacer campaña de Phishing  (Aceptar)  
				- Proporcionar el enlace de la pagina web falsa para descargar app  (Mitigar) 
					- Fingir ser soporte técnico   (Mitigar)  
						- Hacer spoffing suplantando la identidad de la pagina web oficial  ( Mitigar)
							- Troyenizar la aplicación de MailBox (Mitigar)  
								- Crear un Keyloger. (Mitigar)
				-  Pasarle la aplicación por mensajería (Aceptar)
					- Troyenizar la aplicación de MailBox (Aceptar)  
						- Crear un Keyloger. (Aceptar)
					- Troyenizar aplicación de un tercero (Aceptar)
						- Spyware(Aceptar)
				
	- Conseguir Copia de seguridad  (Transferir)
		- Claves de acceso del correo  (Transferir)
			- Ataque de Phishing para conseguir credenciales  (Transferir)
	- Conseguir claves del poder judicial  (Transferir)
		-  Acceder al dispositivo que estén guardado las claves (Transferir)
			-  Repartir Pendrives infectados a los empleados que trabajan donde esta guardado las claves (Eliminar)
				- Crear un  virus que busque claves ssh y las exporte a un servidor en tor (Eliminar)
			- Ataque de Phishing a los agentes del poder judicial con la idea de infectarlos con el virus anterior  (Mitigar)
				- Crear un  virus que busque claves ssh y las exporte a un servidor en tor  (Mitigar)

- Se han **categorizado** las acciones con colores distintos según sus estados:
    **Aceptar** verde
    **Transferir** amarillo
	**Eliminar**  rojo
    **Mitigar** azul
    

```mermaid
graph TD;
    A[Desvelar un mensaje privado] --> B[Recoger datos antes de cifrarse];
    B --> C[Infectar a la víctima];
    C --> D[Hacer campaña de Phishing];
    D --> E[Proporcionar el enlace de la página web falsa para descargar la app];
    E --> F[Fingir ser soporte técnico];
    F --> G[Hacer spoofing suplantando la identidad de la página web oficial];
    G --> H[Troyanizar la aplicación d e MailBox];
    H --> I[Crear un Keylogger];
 
    C --> J[Pasarle la aplicación por mensajería];
    J --> K[Troyanizar la aplicación de MailBox];
    K --> L[Crear un Keylogger];
    J --> M[Troyanizar aplicación de un tercero];
    M --> N[Instalar Spyware];

    A --> O[Conseguir copia de seguridad];
    O --> P[Obtener claves de acceso del correo];
    P --> Q[Ataque de Phishing para conseguir credenciales];

    A --> R[Conseguir claves del poder judicial];
    R --> S[Acceder al dispositivo donde están guardadas las claves];
    S --> T[Repartir Pendrives infectados a empleados con acceso a las claves];
    T --> U[Crear un virus que busque claves SSH y las exporte a un servidor en Tor];

    S --> V[Ataque de Phishing a agentes del poder judicial];
    V --> W[Crear un virus que busque claves SSH y las exporte a un servidor en Tor];



    D:::mitigar
    E:::mitigar
    F:::mitigar
    G:::mitigar
    H:::mitigar
    I:::mitigar
    J:::aceptar
    K:::aceptar
    L:::aceptar
    M:::aceptar
    N:::aceptar
    O:::transferir
    P:::transferir
    Q:::transferir


    T:::eliminar
    U:::eliminar
    V:::mitigar
    W:::mitigar

    classDef aceptar fill:#aaffaa,stroke:#228b22;
    classDef transferir fill:#ffffaa,stroke:#ffaa00;
    classDef eliminar fill:#ffaaaa,stroke:#ff0000;
    classDef mitigar fill:#aaaaff,stroke:#0000ff;
````





