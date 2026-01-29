---
title: "Synology"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - gestionservidores
---

> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

Synology DSM (DiskStation Manager) es un sistema operativo basado en Linux desarrollado por Synology para sus dispositivos de almacenamiento en red NAS (Network Attached Storage). DSM proporciona una interfaz gráfica fácil de usar para administrar los recursos y servicios en los NAS de Synology, permitiendo a los usuarios gestionar su almacenamiento, configurar aplicaciones, establecer copias de seguridad, y mucho más.

Características principales de Synology DSM

1. Interfaz web intuitiva:

DSM ofrece una interfaz gráfica accesible desde un navegador web, similar a un sistema operativo de escritorio. Esta interfaz permite a los usuarios gestionar fácilmente sus NAS y acceder a las funciones del sistema sin necesidad de conocimiento técnico profundo.



2. Almacenamiento centralizado:

Los dispositivos Synology NAS con DSM permiten almacenar archivos y compartir datos de manera centralizada en la red local, proporcionando acceso fácil a documentos, fotos, videos, y otros archivos desde múltiples dispositivos.



3. Sistema de archivos Btrfs:

DSM soporta el sistema de archivos Btrfs, que es más robusto y seguro que otros sistemas de archivos tradicionales. Btrfs ofrece características como copias de seguridad en tiempo real, instantáneas (snapshots), y recuperación ante fallos.



4. Gestión avanzada de usuarios y permisos:

Permite crear y gestionar múltiples cuentas de usuario y grupos para controlar el acceso a los archivos y carpetas compartidas. Los administradores pueden establecer permisos detallados para cada usuario y grupo, y gestionar su acceso a recursos específicos en el NAS.



5. Funciones de seguridad avanzadas:

DSM incluye características de seguridad, como el cifrado de datos, la autenticación de dos factores (2FA), el cortafuegos incorporado y el sistema de protección contra intrusos para garantizar que los datos estén seguros.



6. Aplicaciones y servicios:

DSM ofrece una amplia gama de aplicaciones para aumentar la funcionalidad del NAS, como:

File Station: para gestión de archivos.

Photo Station y Video Station: para organizar y visualizar fotos y videos.

Surveillance Station: para gestionar cámaras de seguridad IP.

DSM Mobile App: para acceso remoto a los archivos.

Cloud Station Server: para sincronización de archivos y copias de seguridad en la nube.

Docker: para ejecutar contenedores y aplicaciones en el NAS.




7. Soporte de virtualización:

DSM también permite ejecutar máquinas virtuales a través de su aplicación Virtual Machine Manager (VMM). Esto permite usar el NAS para ejecutar máquinas virtuales (VMs) que pueden ejecutar otros sistemas operativos y aplicaciones, lo que lo convierte en una solución muy versátil.



8. Backup y recuperación:

DSM ofrece múltiples soluciones de copia de seguridad y recuperación, como Hyper Backup, que permite realizar copias de seguridad de datos en almacenamiento local o remoto, y Snapshot Replication, que permite crear copias de seguridad instantáneas y replicarlas a otro NAS para proteger los datos.



9. Compatibilidad con la nube:

DSM ofrece integración con soluciones de almacenamiento en la nube como Google Drive, Dropbox, y Microsoft OneDrive, permitiendo que los datos se sincronicen entre el NAS y la nube.





---

Beneficios de Synology DSM

1. Facilidad de uso:

La interfaz gráfica de DSM hace que incluso los usuarios sin experiencia técnica puedan configurar y gestionar un NAS Synology de manera sencilla.



2. Escalabilidad:

Synology ofrece una amplia gama de dispositivos NAS, desde soluciones pequeñas para usuarios individuales o pequeñas empresas hasta soluciones empresariales con gran capacidad de almacenamiento y características avanzadas.



3. Solución todo en uno:

DSM convierte un dispositivo NAS en una solución todo en uno, proporcionando almacenamiento, copias de seguridad, virtualización, gestión de archivos multimedia, y más, todo desde un único dispositivo.



4. Accesibilidad remota:

DSM ofrece acceso remoto a través de su aplicación Synology Drive o usando un navegador, lo que te permite acceder a tus archivos y servicios desde cualquier lugar con conexión a Internet.



5. Rendimiento eficiente:

DSM optimiza el rendimiento del hardware del NAS, asegurando que el dispositivo sea eficiente en cuanto a consumo de recursos, incluso en entornos de alto rendimiento.





---

Instalación y configuración básica de DSM

1. Instalación de DSM en un NAS Synology

La instalación de DSM en un dispositivo NAS Synology es muy sencilla, ya que los dispositivos Synology vienen con DSM preinstalado. Sin embargo, si estás configurando un NAS desde cero, puedes hacerlo siguiendo estos pasos:

1. Conecta tu NAS a la red:

Conecta tu NAS Synology a la red local mediante un cable Ethernet.



2. Accede a DSM:

En un navegador web, escribe http://find.synology.com o la dirección IP del NAS. Esto iniciará el proceso de instalación de DSM.



3. Sigue el asistente de instalación:

El asistente te guiará a través de la instalación de DSM, incluida la configuración de red, la creación de cuentas de usuario y la inicialización del disco duro.



4. Configura el almacenamiento:

Puedes elegir configurar volúmenes, crear almacenamiento RAID y configurar las opciones de redundancia para garantizar la seguridad de los datos.




2. Administración de DSM

3. Accede a la interfaz web de DSM:

Después de la instalación, puedes acceder al panel de administración a través de la interfaz web, utilizando la dirección IP de tu NAS: http://<IP_DEL_NAS>:5000.



2. Configura usuarios y permisos:

Desde el panel de administración, puedes crear cuentas de usuario, asignarles permisos específicos para acceder a diferentes carpetas y servicios dentro del NAS.



3. Instala aplicaciones adicionales:

Desde el Centro de Paquetes de DSM, puedes instalar aplicaciones adicionales según tus necesidades, como Docker, Photo Station, Surveillance Station, entre otras.





---

Conclusión

Synology DSM es un sistema operativo altamente funcional y fácil de usar para NAS que ofrece una solución centralizada para almacenamiento, administración de archivos, copias de seguridad, servicios multimedia, y más. Su capacidad para gestionar almacenamiento de manera eficiente, junto con sus potentes herramientas de virtualización y seguridad, lo convierten en una opción popular tanto para usuarios domésticos como para empresas.

Si tienes alguna pregunta adicional sobre la configuración de DSM o necesitas ayuda con alguna característica específica, no dudes en pedírmelo. ¡Estoy aquí para ayudarte!

