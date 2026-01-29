---
title: "Modulo De Python3 Httpserver"
date: 2026-01-26
tags:
  - ciberseguridad
  - herramientas
---
Para crear un servidor HTTP simple en Python utilizando el módulo `http.server`, solo necesitas ejecutar un comando en tu terminal o línea de comandos.

### Pasos:


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[01-Ciberseguridad/Fundamentos/shred|shred]]. [[01-Ciberseguridad/Analisis-Datos/2025-03-05-Redes-Neuronales-y-Convoluciones|2025 03 05 Redes Neuronales y Convoluciones]].

1. **Abre una terminal o línea de comandos.**

2. **Navega a la carpeta** donde quieres que el servidor sirva los archivos (por ejemplo, documentos HTML, imágenes, etc.). Si quieres que el servidor sirva los archivos desde el directorio actual, no es necesario cambiar de carpeta.

3. **Ejecuta el siguiente comando:**

   ```bash
   python3 -m http.server
   ```

   Esto iniciará un servidor HTTP en el puerto **8000** de manera predeterminada, y servirá los archivos que estén en el directorio en el que ejecutas el comando.

4. **Accede a tu servidor en el navegador**:
   
   Abre tu navegador web y ve a:

   ```
   http://localhost:8000
   ```

   Verás una lista de archivos y carpetas dentro del directorio desde el que ejecutaste el servidor.

### Opcional: Cambiar el puerto

Si deseas que el servidor escuche en otro puerto, simplemente añades el número de puerto después del comando, por ejemplo:

```bash
python3 -m http.server 8080
```

Esto hará que el servidor esté disponible en:

```
http://localhost:8080
```

### Desactivar el servidor

Para detener el servidor, puedes presionar `Ctrl + C` en la terminal.

Este servidor es muy básico y está destinado principalmente para pruebas o desarrollo local. No es adecuado para producción.

cookies manager