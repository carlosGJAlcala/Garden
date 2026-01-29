---
title: "Ejemplo sacando la contraseña de un rar"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - elpscrk
---
### **¿Qué es John the Ripper? Una herramienta para el descifrado de contraseñas**

**John the Ripper** (también conocido como **John** o **JTR**) es una herramienta de software de código abierto utilizada principalmente para la **auditoría de seguridad**.

> **Relacionado**: Para cracking basado en GPU, ver [[HashCat]]. Para ataques en redes WiFi, ver [[Pyrit]]. Ver también [[Hydra]] para ataques de fuerza bruta online. Su función principal es descifrar contraseñas que están almacenadas como **hashes** (versiones cifradas de las contraseñas) en sistemas operativos, aplicaciones y servicios. Fue desarrollada originalmente para sistemas **UNIX**, pero con el tiempo se ha adaptado para trabajar en una variedad de plataformas, incluidos **Windows**, **Linux** y **macOS**.

#### **¿Cómo funciona John the Ripper?**

El objetivo de John the Ripper es **descifrar** o **"crackear"** contraseñas protegidas por hashes, para encontrar posibles vulnerabilidades en un sistema. Para hacerlo, la herramienta utiliza varios métodos de ataque que intentan adivinar la contraseña original a partir de su hash cifrado. Algunos de los métodos más comunes son:

1. **Ataque de Diccionario**: John the Ripper compara los hashes con una lista predefinida de palabras comunes, que suelen ser intentos de contraseñas frecuentemente utilizadas, como "123456", "password", "qwerty", etc. Si la contraseña está en el diccionario, el proceso de descifrado será rápido.

2. **Ataque de Fuerza Bruta**: En este ataque, John prueba todas las combinaciones posibles de caracteres hasta encontrar la correcta. Si bien este método es extremadamente efectivo, también es muy lento, especialmente cuando las contraseñas son largas y complejas.

3. **Ataque de Reglas**: Este método aplica transformaciones a las palabras del diccionario. Por ejemplo, puede agregar números al final de las palabras o cambiar letras por caracteres especiales, lo que aumenta las probabilidades de acertar contraseñas que son una variación de una palabra común.

4. **Ataques Híbridos**: Este ataque combina diccionarios con reglas de modificación. Por ejemplo, se puede probar una lista de palabras (como las del diccionario) y modificar cada una de ellas de acuerdo con ciertas reglas (como agregar números o cambiar caracteres), lo que aumenta las posibilidades de encontrar contraseñas más complejas.

5. **Ataques de Cracking Específicos para Algoritmos**: John the Ripper también tiene módulos que le permiten adaptarse a diferentes tipos de algoritmos de hash, como **MD5**, **SHA-1**, **bcrypt**, **NTLM** (usado en sistemas Windows), entre otros. Esto le permite atacar una gran variedad de sistemas y plataformas.

#### **¿Para qué se utiliza John the Ripper?**

John the Ripper se utiliza principalmente para **evaluar la seguridad de contraseñas**. Los administradores de sistemas y los expertos en seguridad lo usan para realizar auditorías y asegurarse de que las contraseñas almacenadas en un sistema no sean débiles o fáciles de adivinar. De esta manera, ayuda a identificar posibles vulnerabilidades y permite fortalecer la seguridad de las redes y sistemas informáticos.

Es importante destacar que, aunque John the Ripper es una herramienta legítima utilizada por profesionales de la seguridad, también puede ser utilizada con fines maliciosos por personas que intentan acceder a sistemas sin autorización. **El uso no autorizado** de esta herramienta para descifrar contraseñas es ilegal.

### **Ejemplo de funcionamiento de John the Ripper y su diferencia con Hashcat**

#### **¿Cómo funciona John the Ripper?**

Supongamos que tienes un archivo con hashes de contraseñas y quieres saber qué contraseñas están asociadas a esos hashes. Un administrador de sistemas podría tener un archivo de contraseñas de usuarios cifradas, y usar John the Ripper para descifrarlas y determinar si alguna contraseña es débil.

##### **Ejemplo práctico con John the Ripper:**

1. **Archivo de Hashes (ejemplo):**
   Supón que tienes un archivo llamado `passwords.txt` que contiene hashes de contraseñas (por ejemplo, usando el algoritmo MD5).

   ```plaintext
   098f6bcd4621d373cade4e832627b4f6  user1
   5f4dcc3b5aa765d61d8327deb882cf99  user2
   ```

   En este caso, `098f6bcd4621d373cade4e832627b4f6` es el hash MD5 de la palabra "test", y `5f4dcc3b5aa765d61d8327deb882cf99` es el hash MD5 de la palabra "password".

2. **Ejecutando John the Ripper:**
   En una terminal, puedes ejecutar el siguiente comando para intentar crackear estos hashes:

   ```bash
   john --format=raw-md5 passwords.txt
   ```

   Aquí:
   - `--format=raw-md5` indica que los hashes están en formato MD5 (puedes especificar otros tipos de hash según el caso).
   - `passwords.txt` es el archivo que contiene los hashes.

3. **Proceso:**
   John the Ripper comenzará a probar una lista de posibles contraseñas (como las que contiene el diccionario por defecto o las configuradas por el usuario) y generará los hashes correspondientes. Luego, comparará estos hashes con los que están en el archivo `passwords.txt`.

4. **Resultado:**
   Si John encuentra una coincidencia entre un hash calculado y un hash en el archivo, mostrará el resultado. En este caso, debería encontrar las siguientes contraseñas:

   ```plaintext
   user1:test
   user2:password
   ```

   **John the Ripper** logró descifrar ambos hashes, mostrando que las contraseñas de `user1` y `user2` son "test" y "password", respectivamente.

#### **Diferencias entre John the Ripper y Hashcat**

Aunque tanto **John the Ripper** como **Hashcat** son herramientas de cracking de contraseñas, tienen diferencias clave en cuanto a su enfoque, rendimiento y capacidades:

1. **Arquitectura y Rendimiento:**
   - **John the Ripper**: Es principalmente una herramienta basada en CPU, aunque puede utilizar la aceleración de GPU en ciertas versiones (a partir de John the Ripper "Community Enhanced" y en versiones más recientes). Sin embargo, su enfoque principal sigue siendo la optimización para procesadores.
   
   - **Hashcat**: Está especialmente optimizado para usar **tarjetas gráficas (GPU)**, lo que lo hace mucho más rápido en comparación con herramientas basadas únicamente en CPU. Hashcat es conocido por su **altísimo rendimiento** en entornos de cracking masivo de contraseñas, especialmente cuando se usan múltiples GPUs.

2. **Algoritmos de Hash Soportados:**
   - **John the Ripper**: Inicialmente diseñado para **UNIX** y hashes relacionados con ese sistema, John the Ripper soporta una variedad de algoritmos de hash, incluidos MD5, SHA-1, bcrypt, entre otros. A medida que se ha ido desarrollando, ha agregado soporte para más tipos de hashes y sistemas operativos.
   
   - **Hashcat**: Hashcat soporta una **gran variedad de algoritmos** de hash, incluyendo algunos algoritmos avanzados de criptografía, como **bcrypt**, **scrypt**, **SHA-256**, **NTLM**, y muchos otros. Además, tiene soporte nativo para el cracking de **hashes de contraseñas de archivos** (como los de PDF, Office, etc.) y protocolos de red como **WPA/WPA2** (Wi-Fi).

3. **Facilidad de uso:**
   - **John the Ripper**: Es bastante fácil de usar para la mayoría de los usuarios, con un comando simple para comenzar el cracking. Tiene muchas configuraciones automáticas que permiten a los usuarios empezar sin mucha configuración avanzada.
   
   - **Hashcat**: Puede ser un poco más complejo de configurar, especialmente si se usa con múltiples GPUs. Hashcat requiere una buena comprensión de cómo funcionan los algoritmos y las optimizaciones disponibles, aunque tiene un buen soporte de documentación y ejemplos.

4. **Modos de ataque:**
   - **John the Ripper**: Utiliza principalmente ataques de diccionario, fuerza bruta, híbridos y ataques basados en reglas. Es bastante eficaz para hashes sencillos o comunes, pero no está tan optimizado para ataques a gran escala como Hashcat.
   
   - **Hashcat**: Soporta una amplia gama de **modos de ataque avanzados** como:
     - Ataques de **máscara** (mask attack), donde se pueden definir patrones de caracteres (como contraseñas con un formato específico).
     - Ataques **combinados** que combinan varias estrategias.
     - Ataques utilizando **GPU** para acelerar enormemente el proceso de cracking.

5. **Flexibilidad y Adaptabilidad:**
   - **John the Ripper**: Aunque es muy flexible y permite personalizar el proceso de cracking (como agregar diccionarios personalizados o reglas específicas), su rendimiento sigue estando centrado en la CPU.
   
   - **Hashcat**: Es muy flexible, soportando una gran cantidad de configuraciones para personalizar ataques y optimizar el uso de hardware, especialmente en entornos con múltiples GPUs.

#### **Resumen de las diferencias:**

| Característica          | **John the Ripper**                                      | **Hashcat**                                            |
|-------------------------|-----------------------------------------------------------|--------------------------------------------------------|
| **Rendimiento**          | Basado en CPU, soporte parcial de GPU.                    | Optimizado para GPUs, alto rendimiento con múltiples GPUs. |
| **Facilidad de uso**     | Relativamente fácil de usar para principiantes.           | Requiere más configuración, pero es muy potente y flexible. |
| **Soporte de algoritmos**| Amplio, especialmente en sistemas UNIX.                   | Soporta muchos más algoritmos, incluyendo WPA/WPA2 y otros hashes complejos. |
| **Tipos de ataques**     | Diccionario, fuerza bruta, reglas, híbrido.               | Máscara, diccionario, híbrido, combinados, GPU optimizados. |
| **Uso principal**        | Auditoría de contraseñas en sistemas UNIX, hashes comunes. | Cracking masivo de contraseñas, especialmente en entornos con GPUs. |

### **Conclusión**

- **John the Ripper** es ideal para auditorías de seguridad simples y medianas, especialmente cuando se trata de hashes más tradicionales y en sistemas UNIX.
- **Hashcat** es más adecuado para proyectos de cracking a gran escala, aprovechando el poder de las GPUs para acelerar el proceso, y es más flexible en cuanto a los tipos de ataques que puedes realizar.

Ambas son herramientas poderosas y se pueden utilizar en conjunto dependiendo del escenario, pero la elección entre una u otra depende del tipo de tarea que quieras realizar y los recursos de hardware disponibles.

# Ejemplo sacando la contraseña de un rar

### **¿Qué es `rar2john`?**

**`rar2john`** es una herramienta incluida en **John the Ripper** que se utiliza para **extraer el hash** de un archivo RAR protegido por contraseña. Este hash es lo que **John the Ripper** necesita para intentar descifrar la contraseña del archivo RAR. En otras palabras, **`rar2john`** convierte un archivo RAR protegido por contraseña en un formato que **John the Ripper** puede procesar.

### **Pasos para usar `rar2john` y John the Ripper para crackear un archivo RAR**

Si tienes un archivo RAR protegido por contraseña y deseas intentar descifrar su contraseña utilizando **John the Ripper** y la herramienta **`rar2john`**, sigue estos pasos:

---

#### **1. Instalar John the Ripper**

Si no tienes **John the Ripper** instalado, puedes hacerlo fácilmente.

- **En Linux (Debian/Ubuntu)**:

  ```bash
  sudo apt-get install john
  ```

- **En macOS** (usando **Homebrew**):

  ```bash
  brew install john
  ```

- **En Windows**, puedes descargar la versión más reciente desde el [repositorio oficial en GitHub](https://github.com/magnumripper/JohnTheRipper).

---

#### **2. Obtener el archivo RAR**

Asegúrate de tener el archivo RAR cuya contraseña quieres descifrar. Por ejemplo, supongamos que tienes un archivo llamado `documento.rar`.

---

#### **3. Extraer el hash con `rar2john`**

Para poder utilizar **John the Ripper** en un archivo RAR, primero necesitas extraer el hash que protege ese archivo. Para ello, **`rar2john`** se encarga de hacerlo.

1. Abre una terminal o consola en la carpeta donde tienes el archivo RAR.
   
2. Ejecuta el siguiente comando para extraer el hash del archivo RAR:

   ```bash
   rar2john documento.rar > documento_hash.txt
   ```

   - **`documento.rar`** es el archivo protegido por contraseña.
   - **`documento_hash.txt`** es el archivo de salida que contendrá el hash que **John the Ripper** utilizará para intentar crackear la contraseña.

El archivo `documento_hash.txt` tendrá un aspecto similar a este:

```plaintext
documento.rar:$rar$2*0*0*18319522170*8b24b6d9f9fa3e1dbd9adff92e7d0f81*...
```

Este hash es el que necesitas para que **John the Ripper** intente descubrir la contraseña.

---

#### **4. Crackear la contraseña con John the Ripper**

Ahora que tienes el hash extraído, puedes usar **John the Ripper** para intentar crackear la contraseña.

Ejecuta el siguiente comando:

```bash
john documento_hash.txt
```

**John the Ripper** comenzará a probar una lista de contraseñas posibles, utilizando su diccionario por defecto, ataques de fuerza bruta o reglas de modificación de contraseñas.

---

#### **5. Ver los resultados**

Una vez que **John the Ripper** haya terminado de procesar el hash (o haya encontrado la contraseña), puedes ver el resultado con el siguiente comando:

```bash
john --show documento_hash.txt
```

Este comando mostrará la contraseña encontrada (si es que **John the Ripper** la ha descubierto). Ejemplo de salida:

```plaintext
documento.rar:mi_contraseña_secreta
```

---

### **Ejemplo completo**

Supongamos que tienes un archivo RAR llamado `documento.rar` y quieres crackear su contraseña. Los pasos serían:

1. **Generar el hash con `rar2john`**:

   ```bash
   rar2john documento.rar > documento_hash.txt
   ```

2. **Crackear el hash con John the Ripper**:

   ```bash
   john documento_hash.txt
   ```

3. **Ver la contraseña descifrada**:

   ```bash
   john --show documento_hash.txt
   ```

---

### **Consideraciones adicionales**

- **Tiempo de cracking**: Si la contraseña es compleja o larga, **John the Ripper** puede tardar mucho tiempo en encontrarla, especialmente si utilizas un ataque de fuerza bruta. En estos casos, puede ser más efectivo usar un **diccionario personalizado**.
  
- **Uso de diccionarios personalizados**: Si tienes alguna idea sobre cómo podría ser la contraseña (por ejemplo, palabras relacionadas con el archivo o nombres comunes), puedes acelerar el proceso usando un diccionario personalizado:
  
  ```bash
  john --wordlist=mi_diccionario.txt documento_hash.txt
  ```

- **Optimización con GPU**: Si tienes una tarjeta gráfica potente, puedes utilizar **Hashcat** (otra herramienta de cracking de contraseñas) que está optimizada para aprovechar la potencia de la GPU, lo que acelera considerablemente el proceso de cracking.

- **Legalidad**: Recuerda que el cracking de contraseñas de archivos RAR sin autorización es **ilegal** y puede tener consecuencias legales. Asegúrate de que tienes el permiso necesario para realizar esta tarea.

---

### **Resumen**

- **`rar2john`** se utiliza para extraer el hash de un archivo RAR protegido por contraseña.
- Una vez que tienes el hash, **John the Ripper** puede intentar crackear la contraseña utilizando ataques como diccionario, fuerza bruta o reglas.
- **John the Ripper** mostrará la contraseña si logra encontrarla, usando el comando `john --show`.

Este proceso es útil para realizar auditorías de seguridad en archivos RAR y verificar la fortaleza de las contraseñas utilizadas en los archivos comprimidos.