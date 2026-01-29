---
title: "Comandos Linux"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
  - unix
---


### Resumen de Comandos de Linux


> **Relacionado**: [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/Locate|Locate]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/comandos/chmod|chmod]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]]. [[08-Personal/Rutinas/Horario|Horario]].

**adduser**  
`adduser dsoneil` | Este comando añade automáticamente un nuevo usuario al sistema.  
*(El script de Bash se puede encontrar en /usr/sbin si necesita modificaciones)*

**alias**  
`alias ayuda=man` | El comando alias permite asignar un nuevo nombre a un comando.  
`alias largo=ls -al` | Un alias también puede incluir opciones de línea de comandos.  
*(A menos que el alias se incluya en tu archivo .login, será temporal)*

**apropos**  
`apropos palabra_clave` | Muestra nombres de comandos basados en una búsqueda por palabra clave.

**at**  
`at 1:23 lp /home/index.html` | Ejecuta una lista de comandos en un horario específico (ej., imprime a las 1:23).  
`at 1:50 echo “lp Trabajo Hecho”` | Usa el comando echo para enviar un mensaje a las 1:50 indicando que se ha terminado una impresión.  
`at -l` | Lista todos los trabajos programados; es un alias para el comando `atq`.  
`at -d 5555` | Cancela el trabajo número 5555; es un alias para el comando `atrm`.

**cat**  
`cat /etc/filename` | Imprime en pantalla el archivo especificado.  
`cat archivo.a > archivo.b` | Mueve el contenido de archivo.a a archivo.b.  
`cat archivo.a >> archivo.b` | Agrega el contenido de archivo.a al final de archivo.b.

**cd**  
`cd /home/dsoneil` | Cambia al directorio especificado.  
`cd ~usuario` | Lleva al usuario al directorio principal especificado.

**chfn**  
`chfn dsoneil` | Permite cambiar la información del usuario en el sistema (ej., cambiar dsoneil a Darcy S. O’Neil).

**chmod**  
`chmod 666 archivo` | Da permiso de Lectura y Escritura a todos.  
`chmod 777 archivo` | Da permiso de Lectura, Escritura y Ejecución a todos.  
`chmod a=rwx archivo` | Da permiso de Lectura, Escritura y Ejecución a todos los usuarios.  
*(Para una lista completa de los comandos de permisos chmod disponibles, consulte la página 4 - Tabla 1)*

**chown**  
`chown dso /home/html` | Cambia el propietario del directorio especificado a “dso”.  
`chown dso /home/archivo.a` | Cambia el propietario del archivo especificado a “dso”.

**clear**  
`clear` | Limpia la pantalla.

**cmp**  
`cmp -s archivo.a archivo.b` | Compara dos archivos de cualquier tipo. La opción -s no muestra nada si los archivos son iguales.

**cp**  
`cp archivo.a archivo.b` | Crea una copia de archivo.a con un nuevo nombre, archivo.b.

**cpio**  
`ls /home | cpio -o > /root` | Copia los archivos de /home al directorio /root.  
`cpio -it < /root > bk.indx` | Extrae todos los archivos a /root y crea un archivo índice llamado bk.indx.

**cron**  
| Pronto estará disponible.

**du**  
`du -k /home/html` | Proporciona un resumen del uso de espacio en disco, en kb, dentro de la ruta especificada.  
`du -k /home/html/archivo.a` | Proporciona un resumen del espacio en disco usado por un archivo en particular.

**df**  
`df -h` | Muestra el tamaño total, el espacio usado y disponible en todos los sistemas de archivos montados.

**fdformat**  
`fdformat /dev/fd0` | Formato de bajo nivel de un disquete en la unidad fd0.  
`fdformat /dev/fd0H1440` | Formatea un disco de alta densidad de doble cara.
Aquí va la siguiente parte de la traducción:

---

**file**  
`file archivo.a` | Intenta determinar el tipo de archivo que es archivo.a (ej., ejecutable, texto, etc.).  
`file -z archivo.a.tar` | Examina dentro de un archivo comprimido para determinar su tipo.  
`file -L archivo.a` | Sigue enlaces simbólicos para determinar el tipo de archivo.

**find**  
`find /ruta -name passwd` | Ubica la cadena especificada (passwd), comenzando en el directorio especificado (/ruta).  
*(Todos los nombres de archivos o directorios que contengan la cadena se imprimirán en pantalla).*

**finger**  
`finger` | Lista todos los usuarios actualmente conectados en el sistema UNIX.

**free**  
`free -t -o` | Proporciona un resumen del uso de memoria del sistema.

**fsck**  
`fsck /hda` | Revisión y reparación del sistema de archivos.

**git**  
| Es un visor de sistema de archivos.

**grep**  
`cat /etc/passwd | grep dso` | Busca y limita la salida del comando a la palabra o patrón especificado.  
*(En este caso, se imprimen todas las instancias de "dso" en el archivo /etc/passwd).*  
`grep -i “Ejemplo” /home/dsoneil` | La opción -i hace que la búsqueda no distinga entre mayúsculas y minúsculas.

**groupadd**  
`groupadd sudos` | Crea un nuevo grupo llamado "sudos" en el sistema.

**groups**  
`groups` | Muestra los grupos a los que perteneces.

**gzip**  
`gzip archivo.a` | Comprime archivo.a y le añade la extensión archivo.a.gz.  
`gzip -d archivo.a.gz` | Descomprime el archivo archivo.a.gz.  
`tar -zxvf archivo.a.tar.gz` | La bandera z permite descomprimir el archivo tar en un solo paso.

**hostname**  
`hostname` | Obtiene o establece el nombre del host. Normalmente, el nombre del host se guarda en el archivo /etc/HOSTNAME.

**ifconfig**  
`ifconfig eth0` | Muestra el estado de la interfaz de red definida actualmente (ej., Tarjeta Ethernet 0).  
`ifconfig eth0 up` | Activa la interfaz especificada (use "down" para desactivarla).  
`ifconfig eth1 192.168.0.2 up` | Activa eth1 con la dirección IP 192.168.0.2.

**insmod**  
| Comando utilizado por el usuario root para instalar controladores de dispositivos modulares.

**installpkg**  
`installpkg -r nombre_paquete.tgz` | Instala un paquete de Slackware con el nombre especificado (opción -r).  
`removepkg nombre_paquete` | Elimina el paquete especificado pero hace una copia en el directorio /tmp.  
`rpm2targz nombre_archivo.rpm` | Convierte un archivo RPM a un paquete de Slackware .tgz.  
`upgradepkg nombre_paquete.tgz` | Actualiza un paquete de Slackware y elimina archivos obsoletos.

**jobs**  
`jobs` | Lista todos los trabajos que se están ejecutando actualmente en el sistema.

**kernelcfg**  
| Interfaz gráfica para agregar o eliminar módulos de kernel (requiere permisos de root en terminal X).

**kill**  
`kill 2587` | Finaliza el proceso especificado por el ID de proceso (PID) 2587.  
`kill -9 2587` | La opción -9 fuerza al proceso a detenerse.
Aquí está la siguiente parte de la traducción:

---

**last**  
`last -300` | Muestra en pantalla el nombre de usuario, ubicación, hora de inicio y cierre de sesión de las últimas conexiones al sistema.  
`last -5 nombre_usuario` | Muestra las últimas 5 veces que el usuario especificado ha iniciado sesión en el sistema.  
*(El comando last no es rastreable).*

**lastlog**  
`lastlog` | Muestra una lista de los intentos de inicio de sesión y las horas de todos los usuarios en el sistema (útil para comprobación de seguridad).

**less**  
`less /html/index.html` | Muestra la información una pantalla a la vez; permite avanzar y retroceder por el archivo.

**ln**  
`ln -s /usr/dso ./home/html` | Crea un enlace simbólico (enlace “suave”) desde el primer directorio o archivo al segundo.  
*(Un usuario que navegue a ./home/html será dirigido al directorio /usr/dso).*

**locate**  
`locate wordperfect` | El comando locate busca el archivo especificado y muestra su ruta de directorio.  
*(Ver comando `updatedb` para actualizar la base de datos de "locate").*

**lpr**  
`lpr /home/html/index.html` | Imprime el archivo index.html en la impresora.  
`lprm 12` | Cancela el trabajo de impresión número 12 en la cola de impresión.  
`lpq` | Muestra el contenido de la cola de impresión.

**ls**  
`ls -al` | Lista toda la información sobre todos los archivos en el directorio actual en una sola línea.  
*(Incluye permisos, propietarios, hora de modificación, tamaño de archivo y nombre).*  
`ls -F` | Marca los directorios con un /, los ejecutables con un *, y los enlaces simbólicos con un @.

**lsmod**  
| Utilizado por el usuario root para mostrar los módulos del kernel cargados actualmente.

**make**  
`make mrproper` | Limpia los archivos temporales dejados por el equipo de desarrollo.  
`make xconfig` | Presenta una serie de preguntas sobre el sistema y los requisitos de los controladores.  
`make dep` | Establece dependencias.  
`make clean` | Limpia archivos innecesarios en el directorio de compilación.  
`make bzImage` | Comienza el proceso de compilación de un nuevo kernel.  
`make lnx` | Especifica que la fuente se compilará bajo un sistema Linux.  
`make install` | Tras el comando make, instala los binarios compilados en sus directorios.  
*(Para crear un registro de programas instalados, utiliza: `make install > /root/install_logs/program-1.0`)*

**man**  
`man vi` | Muestra la página del manual sobre el tema especificado (vi) en pantalla.  
*(Usa la barra espaciadora para desplazarte hacia abajo, la letra b para retroceder y la tecla q para salir).*

**mkdir**  
`mkdir pascal` | Crea un nuevo directorio (pascal) en el directorio actual.

**mkfs**  
`mkfs -t msdos -c -v /unidad_dos` | Formatea una partición y construye un nuevo sistema de archivos en ella.  
*(La opción -t especifica el tipo de sistema de archivos, -v produce salida detallada, y -c verifica bloques defectuosos).*

**more**  
`more /home/html/index.htm` | Muestra el archivo especificado línea por línea (usa Enter para avanzar) o pantalla por pantalla (usa la barra espaciadora para avanzar).  
*(Usa la tecla b para retroceder y q para salir).*

**mount**  
`mount -t msdos /dev/hda5 /dos` | Monta la partición msdos en la unidad de disco duro (hda5) al directorio /dos.  
`mount -t iso9660 /dev/sr0 /cd` | Monta el CD-ROM en el directorio /cd.  
`mount -t msdos /dev/fd0 /mnt` | Monta la unidad de disquete con un sistema de archivos msdos en /mnt.  
`mount -a /etc/fstab` | Intenta montar todos los sistemas de archivos listados en el archivo /etc/fstab.

Aquí está la continuación de la traducción:

---

**mv**  
`mv ./home/archivo ./dso/archivo` | Mueve el archivo especificado a otro directorio.

**nice**  
`nice -5 sort uno.a > dos.b` | Ajusta la prioridad de un proceso antes de que comience.  
*(Cuanto mayor sea el número, menor será la prioridad. Todos los procesos comienzan en 10).*

**nohup**  
| Este comando permite que un proceso continúe ejecutándose después de cerrar sesión.

**passwd**  
`passwd` | Inicia el programa de cambio de contraseña para que el usuario modifique su contraseña.

**ps**  
`ps` | Lista todos los procesos actuales en ejecución, sus IDs de proceso (PIDs) y su estado.  
`ps -ef | grep dsoneil` | Encuentra todos los procesos para el usuario “dsoneil”.

**pstree**  
`pstree -p` | Proporciona una lista de procesos en ejecución en una estructura de árbol.

**pwd**  
`pwd` | Imprime el directorio de trabajo actual.

**quota**  
`quota` | Muestra las cuotas de usuario tanto para ada (/home/ada/a#/nombre_usuario) como para amelia (/var/spool/mail/nombre_usuario), indicando el número de bloques usados y la cuota del usuario.

**renice**  
`renice -5 12345` | Ajusta la prioridad del proceso en ejecución con el ID 12345 (el valor 5 disminuye la prioridad).

**rm**  
`rm archivo.a` | Elimina el archivo especificado en el directorio actual.  
`rm -i archivo.a` | Elimina el archivo especificado, pero solicita confirmación antes de borrarlo.  
`rm -r /home/dso` | Elimina el directorio especificado y todos los archivos en ese directorio.

**rmdir**  
`rmdir pascal` | Elimina el directorio especificado si está vacío; de lo contrario, muestra un error.  
`rmdir -r pascal` | Elimina el directorio y todos los archivos contenidos en él.

**route**  
`route -n` | Muestra la tabla de enrutamiento IP del Kernel de Linux.  
`route add -net 192.168.0.0 eth0` | Informa a otros sistemas de la red a la que debe enrutar tu sistema.  
`route add default gw 192.168.0.5 eth0` | Indica a tu sistema dónde se encuentra la puerta de enlace a Internet.  
*(Esta información se puede añadir a los archivos del sistema /etc/rc.d/rc.local en Slackware).*

**rpm**  
`rpm -i archivo.2.0-i386.rpm` | Desempaqueta un archivo RPM. Es el método básico de instalación.  
`rpm -U archivo.2.0-i386.rpm` | Instala una actualización para un paquete RPM anterior.  
`rpm -i --force archivo.rpm` | La opción --force obliga a reinstalar el paquete.  
`rpm -e archivo.2.0-i386.rpm` | Elimina un paquete RPM (sin necesidad de usar el nombre completo).  
`rpm -i --nodeps archivo.rpm` | Usa la opción “sin dependencias”.  
`rpm -qa` | Muestra en pantalla todos los paquetes instalados (q es para consulta).  
`rpm -qa | grep gtk` | Imprime todos los paquetes RPM que contengan “gtk” en el nombre.  
`rpm -qi archivo.2.0-i386.rpm` | Proporciona información sobre el paquete que estás a punto de instalar.  
`rpm --rebuild archivo.2.0.rpm` | Reconstruye un paquete si se ha dañado por otro proceso de instalación.

**su**  
`su nombre_usuario` | Permite acceder a privilegios de superusuario. Escribe `exit` para volver a los permisos normales.

**shutdown**  
`shutdown -t 10:00` | Notifica a todos los usuarios conectados que el sistema se apagará a las 10:00 AM.  
`shutdown -r -t 20:00` | Reinicia el sistema a las 8:00 PM.  
`shutdown -t +10 buen día` | Apaga el sistema en 10 minutos con el mensaje “buen día” enviado a los usuarios.  
`shutdown -f` | La opción -f hace que Linux realice un reinicio rápido.

**tar**  
`tar -cf /usuario/dso /home` | Copia el directorio /home al directorio /usuario/dso.  
`tar cvf /backup.tar /dso` | Crea un archivo tar de todo el contenido en el directorio /dso.  
`tar -xvf archivo.a.tar` | Extrae un archivo tar.  
`tar -tvf archivo.a.tar | more` | Permite verificar si el archivo tar comienza con un directorio.  
`tar -zxvf archivo.a.tgz` | Descomprime y extrae el archivo en un solo paso, en lugar de usar gzip.

**top**  
`M` para información de uso de memoria | Este programa muestra mucha información sobre el sistema.  
`P` para información de CPU | Dentro del programa, puedes escribir `q` para salir.

**touch**  
`touch archivo.a` | Crea un archivo vacío en el directorio actual con el nombre especificado.
Aquí está la última parte de la traducción:

---

**uname**  
`uname -a` | Muestra en pantalla la información sobre el kernel de Linux que se está utilizando en el sistema.

**updatedb**  
`updatedb` | Actualiza la base de datos utilizada por el comando `locate`.

**userdel**  
`userdel -r dsoneil` | Elimina al usuario dsoneil del sistema. La opción `-r` borra también el directorio /home del usuario.

**w**  
`w` | Lista todos los usuarios actualmente conectados en el sistema UNIX, proporcionando información como el nombre de usuario, hora de inicio de sesión, tiempo de inactividad y acción actual.

**which**  
`which -a nombre_archivo` | Busca en todos los directorios en tu ruta actual y encuentra todos los archivos llamados nombre_archivo.

**who**  
`who` | Lista a los usuarios actualmente conectados, mostrando el nombre de usuario, el puerto y la hora de inicio de sesión.

**whoami**  
`whoami` | Informa al usuario bajo qué nombre está actuando, usualmente el propio nombre de usuario.

---
