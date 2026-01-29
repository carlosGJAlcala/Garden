---
title: "Hashcat"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - elpscrk
---
**Hashcat** es una de las herramientas más avanzadas y populares para el cracking de contraseñas, ampliamente utilizada en pruebas de penetración, auditorías de seguridad y recuperación de contraseñas. Su principal atractivo es su capacidad para aprovechar el poder de las **unidades de procesamiento gráfico (GPU)**, lo que lo convierte en una opción extremadamente eficiente y rápida en comparación con las herramientas que dependen solo de la **CPU**.

> **Relacionado**: Para cracking basado en CPU, ver [[John-the-Ripper]]. Para ataques en redes WiFi, ver [[Pyrit]].

### Características principales de Hashcat:

#### 1. **Soporte para una amplia variedad de algoritmos de hash**:
   Hashcat es compatible con una amplia gama de algoritmos de hash, lo que lo hace adecuado para muchas aplicaciones de seguridad. Algunos de los algoritmos más comunes que Hashcat puede manejar son:
   - **MD5**
   - **SHA-1, SHA-256, SHA-512**
   - **bcrypt, scrypt** (utilizados para hashes de contraseñas más seguros)
   - **NTLM** y **LM Hash** (para contraseñas de Windows)
   - **WPA/WPA2** (para redes Wi-Fi)
   - **MySQL, DES, MSSQL, etc.**

   Esto permite usar Hashcat no solo para auditorías de redes Wi-Fi, sino también para **cracking de contraseñas** almacenadas en bases de datos, sistemas de archivos y otros sistemas de autenticación.

#### 2. **Uso de GPU para el procesamiento paralelo**:
   Una de las principales ventajas de Hashcat es que está diseñado para aprovechar las **potentes capacidades de cálculo paralelo** de las **tarjetas gráficas (GPU)**. Esto permite realizar ataques de descifrado de contraseñas mucho más rápidos que si se usara solamente el **procesador central (CPU)**.
   
   - **GPU NVIDIA** (CUDA) y **AMD** (OpenCL) son ampliamente soportadas.
   - **Hashcat** puede usar múltiples GPUs de manera eficiente, lo que mejora significativamente el rendimiento y puede hacer el proceso de cracking exponencialmente más rápido.

#### 3. **Modos de ataque avanzados**:
   Hashcat es increíblemente versátil en cuanto a los tipos de **ataques** que soporta. Algunos de los modos de ataque más comunes son:

   - **Ataque de diccionario** (`-a 0`): Prueba todas las contraseñas contenidas en un archivo de diccionario predefinido. Es el ataque más simple y común.
   - **Ataque de fuerza bruta** (`-a 3`): Realiza un ataque de fuerza bruta en el que genera todas las combinaciones posibles de caracteres dentro de un rango específico de longitud.
   - **Ataque combinado** (`-a 1`): Combina contraseñas de dos diccionarios diferentes para generar nuevas contraseñas.
   - **Ataque de máscara** (`-a 3`): En un ataque de máscara, puedes especificar patrones de contraseñas. Por ejemplo, si sabes que la contraseña tiene una cierta estructura (como `ABC123`), puedes usar máscaras como `?u?u?d?d?d` para generar combinaciones con esa estructura.
   - **Ataques híbridos**: Hashcat también permite ataques híbridos, donde puedes combinar ataques de diccionario con máscaras, lo que puede mejorar significativamente las probabilidades de éxito sin tener que probar todas las combinaciones posibles de caracteres.
   
   Además, se pueden aplicar **reglas** para modificar contraseñas generadas en el diccionario, como añadir caracteres al final, invertir la palabra, etc.

#### 4. **Optimización y escalabilidad**:
   Hashcat está diseñado para ser **altamente eficiente** y **escalable**. No solo funciona bien en sistemas con una sola GPU, sino que también puede distribuir el trabajo entre múltiples GPUs y equipos en red, lo que permite atacar hashes de manera más rápida y efectiva.

   - **Distribución de cargas**: Hashcat permite distribuir el trabajo entre múltiples máquinas para aprovechar recursos adicionales si es necesario.
   - **Reinicios automáticos**: La herramienta puede **guardar el progreso** durante un ataque, por lo que si necesitas detenerlo y continuar más tarde, puedes hacerlo sin perder tiempo.

#### 5. **Interfaz de línea de comandos (CLI)**:
   Hashcat funciona principalmente a través de la **línea de comandos** (CLI), lo que lo hace flexible y adecuado para entornos de servidor o sistemas remotos. Aunque puede ser intimidante para los usuarios novatos, la documentación es completa y la comunidad es muy activa, lo que facilita aprender a usarlo.

   Ejemplo de un comando básico para ejecutar un ataque de diccionario en un hash MD5:

   ```bash
   hashcat -m 0 -a 0 hash.txt diccionario.txt
   ```

   - `-m 0`: Especifica que el hash es MD5.
   - `-a 0`: Define el ataque como un ataque de diccionario.
   - `hash.txt`: Es el archivo que contiene los hashes a romper.
   - `diccionario.txt`: Es el archivo que contiene las contraseñas posibles a probar.

#### 6. **Soporte para archivos "pot"**:
   Hashcat puede guardar las contraseñas que ha descifrado en un archivo llamado **potfile**. Esto significa que si un hash ya ha sido roto, Hashcat no necesitará intentar romperlo de nuevo en futuras ejecuciones, lo que ahorra tiempo.

#### 7. **Reglas avanzadas**:
   Hashcat permite usar **reglas** para modificar el contenido de un diccionario y generar contraseñas variantes. Las reglas son patrones que alteran las palabras del diccionario para crear nuevas combinaciones. Esto es útil para aumentar la efectividad de un ataque sin tener que generar un diccionario mucho más grande.

   Las reglas pueden ser simples, como añadir un número al final de una palabra, o complejas, como realizar combinaciones con mayúsculas, caracteres especiales y sustituciones.

#### 8. **Compatibilidad con diferentes plataformas**:
   Hashcat es compatible con **Windows**, **Linux** y **macOS**, lo que lo hace muy accesible. Sin embargo, se recomienda el uso de **Linux** para aprovechar mejor la aceleración de hardware y la configuración avanzada.

---

### Ejemplo de uso de Hashcat

Supongamos que quieres realizar un ataque de diccionario sobre un hash **SHA-256**. Para hacerlo, el comando sería algo como:

```bash
hashcat -m 1400 -a 0 hashes.txt diccionario.txt
```

- `-m 1400`: Especifica que el hash es SHA-256.
- `-a 0`: Ataque de diccionario.
- `hashes.txt`: Contiene los hashes a romper.
- `diccionario.txt`: Contiene las posibles contraseñas.

Si deseas realizar un ataque de **fuerza bruta** con una máscara que define contraseñas de exactamente 6 caracteres (solo números), el comando sería:

```bash
hashcat -m 0 -a 3 hashes.txt ?d?d?d?d?d?d
```

- `-m 0`: Especifica que el hash es MD5.
- `-a 3`: Ataque de fuerza bruta.
- `?d?d?d?d?d?d`: Es una máscara que representa un número de 6 dígitos (d para dígitos).

### Consideraciones de uso

1. **Potencia de hardware**:
   Para obtener el máximo rendimiento de Hashcat, es recomendable tener una **GPU potente**. Las **NVIDIA** y **AMD** son las más populares, especialmente las tarjetas gráficas de gama alta (por ejemplo, las series **RTX** de NVIDIA o las **Radeon** de AMD).

2. **Legalidad y ética**:
   El uso de Hashcat debe estar **limitado a entornos legales y éticos**. Solo debes usar Hashcat para romper contraseñas de redes o sistemas que poseas o para los cuales tengas autorización explícita (por ejemplo, durante una auditoría de seguridad). El cracking de contraseñas sin permiso es **ilegal** y puede tener consecuencias graves.

---

### Resumen

**Hashcat** es una herramienta extremadamente poderosa y flexible para **cracking de contraseñas**. Su capacidad para usar GPUs y su soporte para una amplia gama de algoritmos de hash la convierten en una de las mejores opciones para realizar ataques de cracking de manera eficiente y rápida. Además, sus múltiples modos de ataque y soporte para ataques distribuidos la hacen adecuada tanto para principiantes como para expertos en seguridad informática. Si bien la curva de aprendizaje puede ser un poco empinada debido a su interfaz de línea de comandos, su capacidad y versatilidad lo convierten en una herramienta esencial para cualquier profesional de la seguridad.