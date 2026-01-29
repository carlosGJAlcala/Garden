---
title: "Linux: Conceptos Fundamentales para Automatización"
date: 2026-01-26
tags:
  - infraestructura
  - servidores
  - homelab
---
# Linux: Conceptos Fundamentales para Automatización


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[00-Inicio/HOME|HOME]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Redes/Nginx|Nginx]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]].

## Índice

- [[Permisos-en-Linux]]
- [[Rutas-Absolutas-vs-Relativas]]
- [[Cron-Tareas-Programadas]]
- [[Sudo-y-Sudoers]]
- [[Bash-Nociones-Basicas]]
- [[Mi-Setup-Conversion-de-EPUB-a-AZW3]]

---

## Permisos en Linux

### ¿Qué son los permisos?

Linux tiene un sistema de permisos de tres niveles:

1. **Usuario** (propietario del archivo)
2. **Grupo** (grupo del usuario)
3. **Otros** (el resto de usuarios del sistema)

### Visualizar permisos

Cuando ejecutas `ls -la`, ves algo como:

```
-rwxr-xr-x  1  carlos  users  1234  Jan 10 12:00  script.sh
```

#### Desglose:

**Primer carácter:**

- `-` = archivo regular
- `d` = directorio
- `l` = enlace simbólico

**Siguientes 9 caracteres (3 grupos de 3):**

```
rwxr-xr-x
│││││││││
│││││││└─ otros: ejecución (x)
││││││├── otros: lectura (r)
│││││└─── otros: sin escritura (-)
││││└──── grupo: ejecución (x)
│││├───── grupo: lectura (r)
││└────── grupo: sin escritura (-)
│└─────── usuario: ejecución (x)
└──────── usuario: lectura (r)
```

**Significado de cada letra:**

- `r` (read) = lectura (leer archivo / listar carpeta)
- `w` (write) = escritura (modificar / crear/borrar en carpeta)
- `x` (execute) = ejecución (ejecutar script / acceder a carpeta)
- `-` = sin permiso

### Cambiar permisos con chmod

```bash
chmod +x script.sh       # Añade permisos de ejecución a todos
chmod 755 script.sh      # Usuario: rwx, Grupo: rx, Otros: rx
chmod 700 script.sh      # Solo el usuario puede hacer todo
chmod u+w archivo.txt    # Añade escritura al usuario
chmod g-r archivo.txt    # Quita lectura al grupo
```

**Sistema numérico:**

- `7` = rwx (4+2+1)
- `5` = r-x (4+0+1)
- `4` = r-- (4+0+0)
- `0` = --- (sin permisos)

### Por qué necesitas `chmod +x` para scripts

Un script bash es un archivo de texto. Sin permisos de ejecución, Linux no te deja ejecutarlo incluso si contiene código válido.

```bash
# Esto falla
./script.sh
# bash: ./script.sh: Permission denied

# Después de chmod +x
./script.sh
# Ahora funciona
```

---

## Rutas Absolutas vs Relativas

### Rutas Relativas

Comienzan desde el directorio actual donde estás:

```bash
./scripts/mover_epub.sh      # en la carpeta actual
../documentos/archivo.txt    # una carpeta arriba
~/Descargas/archivo.zip      # desde tu home (~)
```

**Problema:** No funcionan en cron porque cron no sabe en qué directorio estás.

### Rutas Absolutas

Comienzan desde la raíz del sistema (`/`):

```bash
/home/carlos/scripts/mover_epub.sh
/DATA/Media/Books
/var/log/convertir_epub.log
```

**Ventaja:** Funcionan en cualquier contexto, incluso en cron.

### ¿Por qué cron necesita rutas absolutas?

Cron ejecuta comandos sin interacción humana y sin entorno de usuario. No tiene un "directorio actual". Si usas rutas relativas:

```bash
# En tu terminal (funciona porque estás en /home/carlos)
for file in *.epub; do ...

# En cron (falla porque no sabe dónde estás)
*/10 * * * * for file in *.epub; do ...
# Linux busca *.epub desde / o /root, no encuentra nada
```

### Solución

```bash
# En cron, SIEMPRE usa absolutas
*/10 * * * * for file in /DATA/Media/Books/*.epub; do ...
```

---

## Cron: Tareas Programadas

### ¿Qué es cron?

Cron es un **demonio** (servicio que corre en background) que ejecuta comandos en horarios específicos sin intervención del usuario.

Tu `crontab` es un archivo de configuración personal donde defines qué comandos ejecutar y cuándo.

### Acceder a crontab

```bash
crontab -e    # Editar tu crontab personal
crontab -l    # Listar jobs programados
crontab -r    # Eliminar todo el crontab
```

### Formato de crontab

```
┌───────────── minuto (0-59)
│ ┌───────────── hora (0-23)
│ │ ┌───────────── día del mes (1-31)
│ │ │ ┌───────────── mes (1-12)
│ │ │ │ ┌───────────── día de la semana (0-6, siendo 0 domingo)
│ │ │ │ │
│ │ │ │ │
* * * * * /comando/a/ejecutar
```

### Ejemplos de crontab

```bash
# Cada 10 minutos
*/10 * * * * /home/carlos/scripts/convertir_epub.sh

# Cada hora en punto
0 * * * * /home/carlos/scripts/limpieza.sh

# Todos los días a las 3:30 AM
30 3 * * * /home/carlos/scripts/backup.sh

# Cada lunes a las 9:00 AM
0 9 * * 1 /home/carlos/scripts/informe.sh

# Cada mes el primer día a las 00:00
0 0 1 * * /home/carlos/scripts/mes.sh

# Cada 5 minutos
*/5 * * * * /ruta/script.sh
```

### Limitaciones de cron

1. **Sin acceso a variables de entorno** → usa rutas absolutas
2. **Sin interfaz gráfica** → redirecciona salida a logs
3. **No puede pedir contraseña** → necesitas sudoers para `sudo`
4. **Ejecuta como usuario específico** → permisos limitados
5. **Salida limitada** → usa logs para auditar

### Ver logs de cron

```bash
# En sistemas Debian/Ubuntu
grep CRON /var/log/syslog | tail -20

# En Fedora/RHEL
sudo tail -f /var/log/cron
```

---

## Sudo y Sudoers

### ¿Qué es sudo?

`sudo` = "superuser do" = ejecutar un comando como administrador (usuario root).

```bash
sudo apt install paquete    # instala software (necesita permisos admin)
sudo systemctl restart nginx # reinicia servicios
sudo reboot                  # reinicia la máquina
```

Normalmente pide tu contraseña:

```
[sudo] password for carlos: ••••••
```

### El problema con cron y sudo

Cron **no puede escribir contraseñas** (no es interactivo). Si intentas:

```bash
*/10 * * * * sudo /home/carlos/scripts/convertir_epub.sh
```

Cron esperará indefinidamente pidiendo contraseña, **el script nunca ejecuta**.

### ¿Qué es sudoers?

`sudoers` es un archivo (`/etc/sudoers`) que define:

- Quién puede usar `sudo`
- Qué comandos pueden ejecutar
- Si necesitan contraseña
- Con qué permisos se ejecutan

### Estructura de sudoers

```bash
usuario ALL=(usuario_destino) OPCION: comando
```

- `usuario` = quién puede ejecutar
- `ALL` = en todos los hosts
- `(usuario_destino)` = se ejecuta como qué usuario (normalmente root)
- `OPCION` = `PASSWD` (pedir contraseña) o `NOPASSWD:` (sin contraseña)
- `comando` = qué comando específico

### Ejemplos de reglas en sudoers

```bash
# Usuario root puede hacer cualquier cosa
root ALL=(ALL) ALL

# Carlos puede usar sudo pero debe pedir contraseña
carlos ALL=(ALL) ALL

# Carlos puede ejecutar este script sin contraseña
carlos ALL=(ALL) NOPASSWD: /home/carlos/scripts/convertir_epub.sh

# Carlos puede instalar paquetes con apt sin contraseña
carlos ALL=(ALL) NOPASSWD: /usr/bin/apt install

# Carlos puede reiniciar nginx sin contraseña
carlos ALL=(ALL) NOPASSWD: /usr/sbin/systemctl restart nginx

# El grupo docker puede ver logs sin contraseña
%docker ALL=(ALL) NOPASSWD: /usr/bin/journalctl
```

### ¿Por qué usar NOPASSWD en cron?

Porque cron no puede escribir contraseñas interactivamente. Así:

```bash
# En sudoers
carlos ALL=(ALL) NOPASSWD: /home/carlos/scripts/convertir_epub.sh

# En crontab
*/10 * * * * sudo /home/carlos/scripts/convertir_epub.sh
# Se ejecuta sin pedir contraseña 
```

### ¿Cómo editar sudoers?

**SIEMPRE usa `visudo`**, nunca edites directamente:

```bash
sudo visudo
```

¿Por qué? Porque `visudo`:

1. Abre `/etc/sudoers` de forma segura
2. Verifica la sintaxis antes de guardar
3. Si hay error, NO guarda los cambios
4. Así no rompes sudo para todo el sistema

Si editaras con `nano /etc/sudoers` y cometes un error, podrías bloquear `sudo` permanentemente y no podrías arreglarlo.

---

## Bash: Nociones Básicas

### Variables

```bash
ORIGEN="/DATA/Media/Books"
DESTINO="/DATA/Media/Books/Azw3"
LOG="/var/log/convertir_epub.log"

# Usar variables
echo $ORIGEN
echo "$ORIGEN"  # Mejor con comillas
```

### Expansión de parámetros

Modificar variables sobre la marcha:

```bash
filename="libro.epub"

# Quitar extensión
${filename%.epub}  # Resultado: libro

# Quitar ruta
basename "/ruta/a/libro.epub"  # Resultado: libro.epub

# Construcción final
output="/carpeta/${filename%.epub}.azw3"
# /carpeta/libro.azw3
```

### Condicionales: if

```bash
# Verificar si una carpeta existe
if [ ! -d "$ORIGEN" ]; then
  echo "ERROR: Carpeta no existe"
  exit 1
fi

# Verificar si un archivo existe
if [ ! -f "$output" ]; then
  echo "Archivo no existe, proceder"
fi

# Verificar si un comando existe
if ! command -v ebook-convert &> /dev/null; then
  echo "ebook-convert no está instalado"
fi
```

**Operadores de test:**

- `-d` = es un directorio
- `-f` = es un archivo regular
- `-e` = existe (archivo o directorio)
- `-z` = cadena vacía
- `!` = negación (NO)

### Bucles: for

```bash
# Iterar sobre archivos
for file in "$ORIGEN"/*.epub; do
  echo "Procesando: $file"
done

# Iterar sobre números
for i in {1..5}; do
  echo "Número: $i"
done

# Bucle con lista manual
for color in rojo verde azul; do
  echo "Color: $color"
done
```

### Redirección de entrada/salida

```bash
# Redirigir salida a archivo (sobrescribir)
echo "Mensaje" > archivo.log

# Redirigir salida a archivo (añadir al final)
echo "Mensaje" >> archivo.log

# Redirigir salida y errores
comando >> archivo.log 2>&1
# 1 = salida estándar
# 2 = errores
# &1 = a donde va la salida estándar

# Descartar salida
comando &> /dev/null
```

### Tuberías y condiciones lógicas

```bash
# OR (O) - si el primero falla, ejecuta el segundo
[ -e "$file" ] || continue
# Si $file NO existe, continúa al siguiente

# AND (Y) - ejecuta el segundo si el primero tiene éxito
ebook-convert "$file" "$output" && echo "OK"
# Si la conversión es exitosa, imprime "OK"
```

### Obtener la salida de un comando

```bash
# Guardar fecha en variable
fecha=$(date '+%Y-%m-%d %H:%M:%S')
echo "$fecha"

# Usar directamente
echo "$(date '+%Y-%m-%d %H:%M:%S') - Mensaje"
```

---

## Mi Setup: Conversión de EPUB a AZW3

### Objetivo

Convertir automáticamente archivos .epub a .azw3 cada 10 minutos usando un script en cron.

### Herramientas necesarias

- **Calibre** (`ebook-convert`) para la conversión
- **Bash** para el scripting
- **Cron** para la automatización

### El script final

```bash
#!/bin/bash

# Configuración
ORIGEN="/DATA/Media/Books"
DESTINO="/DATA/Media/Books/Azw3"
LOG="/home/carlos/logs/convertir_epub.log"

# Validaciones iniciales
if [ ! -d "$ORIGEN" ]; then
  echo "$(date '+%Y-%m-%d %H:%M:%S') - ERROR: Carpeta origen no existe: $ORIGEN" >> "$LOG"
  exit 1
fi

# Crear destino si no existe
mkdir -p "$DESTINO"

# Verificar que ebook-convert existe
if ! command -v ebook-convert &> /dev/null; then
  echo "$(date '+%Y-%m-%d %H:%M:%S') - ERROR: ebook-convert no está instalado" >> "$LOG"
  exit 1
fi

# Generar el azw3
for file in "$ORIGEN"/*.epub; do
  # Saltar si no hay archivos .epub
  [ -e "$file" ] || continue
  
  filename=$(basename "$file")
  output="$DESTINO/${filename%.epub}.azw3"
  
  if [ ! -f "$output" ]; then
    echo "$(date '+%Y-%m-%d %H:%M:%S') - Convirtiendo: $filename" >> "$LOG"
    if ebook-convert "$file" "$output" >> "$LOG" 2>&1; then
      echo "$(date '+%Y-%m-%d %H:%M:%S') - OK: $filename" >> "$LOG"
    else
      echo "$(date '+%Y-%m-%d %H:%M:%S') - ERROR al convertir: $filename" >> "$LOG"
    fi
  else
    echo "$(date '+%Y-%m-%d %H:%M:%S') - Saltando $filename: ya existe" >> "$LOG"
  fi
done
```

### Instalación paso a paso

```bash
# 1. Crear carpeta de scripts
mkdir -p ~/scripts

# 2. Crear el script
nano ~/scripts/convertir_epub.sh
# Copiar el contenido anterior

# 3. Dar permisos de ejecución
chmod +x ~/scripts/convertir_epub.sh

# 4. Crear carpeta para logs
mkdir -p ~/logs

# 5. Probar el script manualmente
~/scripts/convertir_epub.sh

# 6. Ver el log
cat ~/logs/convertir_epub.log

# 7. Añadir a crontab
crontab -e
# Añadir: */10 * * * * /home/carlos/scripts/convertir_epub.sh
```

### ¿Por qué fallaba el script anterior?

El script original usaba rutas relativas:

```bash
# Fallaba
for file in *.epub; do
```

Cuando cron lo ejecutaba, no encontraba archivos porque:

- Cron no se posiciona en `/DATA/Media/Books`
- Busca `*.epub` desde `/root` o `/`
- Nunca encuentra nada

**Solución:** usar rutas absolutas

```bash
# Funciona
for file in "$ORIGEN"/*.epub; do
```

### Otros problemas

1. **Shebang incorrecto**: `!/bin/bash` → `#!/bin/bash`
2. **Sin validaciones**: no verificaba si las carpetas existían
3. **Sin manejo de errores**: si algo fallaba, silenciosamente no hacía nada
4. **Sin logs**: no había forma de auditar qué pasó
5. **Variables sin comillas**: problemas con espacios en nombres

---

## Checklist: Mi Setup Funcionando

- [ ] Calibre instalado (`ebook-convert` disponible)
- [ ] Script creado en `~/scripts/convertir_epub.sh`
- [ ] Script con permisos `chmod +x`
- [ ] Carpeta de logs creada `~/logs/`
- [ ] Carpeta destino `/DATA/Media/Books/Azw3` existe
- [ ] Script probado manualmente
- [ ] Crontab configurado (`*/10 * * * * /home/carlos/scripts/convertir_epub.sh`)
- [ ] Verificado con `crontab -l`
- [ ] Logs generándose correctamente

---

## Referencias Rápidas

### Comandos útiles

```bash
# Ver permisos
ls -la archivo.sh

# Cambiar permisos
chmod +x script.sh

# Ver crontab
crontab -l

# Editar sudoers
sudo visudo

# Ver logs de cron
grep CRON /var/log/syslog

# Ver logs de tu script
tail -f ~/logs/convertir_epub.log

# Crear carpetas
mkdir -p ~/ruta/profunda

# Buscar archivos
find /DATA/Media/Books -name "*.epub"

# Convertir con Calibre
ebook-convert entrada.epub salida.azw3
```

### Archivos importantes

|Archivo|Descripción|
|---|---|
|`/etc/sudoers`|Configuración de sudo (editar con `visudo`)|
|`~/.bashrc`|Configuración de tu shell|
|`~/.crontab`|Tu crontab personal (editar con `crontab -e`)|
|`/var/log/cron`|Logs de cron (en Fedora)|
|`/var/log/syslog`|Logs del sistema (en Debian/Ubuntu)|

---

**Última actualización:** Enero 2025 **Contexto:** Setup de Raspberry Pi 5 con CasaOS para automatización de media