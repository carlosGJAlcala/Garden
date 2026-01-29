---
title: "Pyrit"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
  - elpscrk
---
**Pyrit** es una herramienta utilizada principalmente para realizar ataques de fuerza bruta y descifrar contraseñas en redes Wi-Fi protegidas con el estándar WPA/WPA2.

> **Relacionado**: Ver [[HashCat]] y [[John-the-Ripper]] para cracking de otros tipos de hashes. Ver también [[01-Ciberseguridad/Criptografia/AES256|AES256]] para entender los algoritmos de cifrado. Pyrit se destaca por su capacidad de aprovechar el poder de procesamiento de múltiples CPUs y tarjetas gráficas (GPU) para acelerar el proceso de descifrado de contraseñas, lo que lo convierte en una herramienta muy eficaz para realizar ataques de diccionario o ataques de fuerza bruta en redes inalámbricas.

### Características principales de Pyrit:

1. **Aceleración por GPU**:
   Pyrit fue diseñado para utilizar las capacidades de procesamiento paralelo de las tarjetas gráficas (GPU) a través de las bibliotecas CUDA de NVIDIA o OpenCL para acelerar el cálculo de hashes de contraseñas. Esto permite realizar ataques mucho más rápidos que los que se pueden lograr solo con la CPU.

2. **Ataques de diccionario**:
   Pyrit puede utilizar un archivo de diccionario (una lista de contraseñas potenciales) para intentar hacer coincidir el hash de la contraseña capturada de un paquete de autenticación de una red Wi-Fi.

3. **Almacenamiento en bases de datos**:
   Pyrit puede almacenar hashes precomputados en bases de datos, lo que permite realizar ataques más rápidos en el futuro al evitar tener que calcular los mismos hashes una y otra vez.

4. **Soporte de hashes avanzados**:
   La herramienta soporta varios algoritmos de hashes utilizados en WPA/WPA2, como el algoritmo PBKDF2 (Password-Based Key Derivation Function 2).

### Cómo funciona Pyrit:

1. **Captura de paquetes**:
   Para usar Pyrit, primero se debe capturar el "handshake" de la red Wi-Fi, que es un intercambio de paquetes entre el cliente y el punto de acceso cuando un dispositivo se conecta a la red. Este intercambio contiene la información necesaria para intentar recuperar la contraseña.

2. **Precomputación de hashes**:
   Pyrit permite precomputar los hashes de un conjunto de contraseñas comunes, lo que hace que el ataque sea más rápido si se tienen muchos intentos. La idea es generar una base de datos de hashes posibles y luego compararlos con los que se han capturado.

3. **Ataque de fuerza bruta**:
   Si se quiere realizar un ataque de fuerza bruta, Pyrit genera combinaciones posibles de contraseñas y calcula su hash, buscando una coincidencia con el hash capturado.

### Requisitos:

- **Hardware adecuado**: Si bien Pyrit puede funcionar con la CPU, su verdadero potencial se alcanza al usar una tarjeta gráfica potente. Esto es especialmente útil si tienes una GPU de NVIDIA o una compatible con OpenCL.
- **Dependencias**: Pyrit requiere ciertas bibliotecas como CUDA (para tarjetas NVIDIA) o OpenCL (para tarjetas AMD) para aprovechar la aceleración por GPU.

### Uso en auditorías de seguridad:

Pyrit se usa principalmente en auditorías de seguridad para probar la robustez de las contraseñas de redes Wi-Fi. Sin embargo, su uso puede ser controvertido si no se tiene autorización para realizar un ataque, ya que en muchos lugares podría ser ilegal.

### Ejemplo de uso básico:

1. **Capturar un handshake**:
   Utilizando herramientas como `airodump-ng` de la suite de Aircrack-ng, se puede capturar el handshake de una red Wi-Fi.

2. **Convertir el handshake a un formato compatible con Pyrit**:
   Utilizar un comando de Pyrit para convertir el archivo de captura en un formato que la herramienta pueda procesar:
   ```bash
   pyrit -r captura.cap -o archivo.pyrit
   ```

3. **Iniciar el ataque**:
   A continuación, se puede utilizar Pyrit para intentar romper la contraseña utilizando un diccionario:
   ```bash
   pyrit -i diccionario.txt -r archivo.pyrit attack_passthrough
   ```

### Consideraciones éticas y legales:

Es importante tener en cuenta que el uso de herramientas como Pyrit para atacar redes Wi-Fi sin autorización es ilegal en muchos países. Solo se debe usar en redes propias o en un contexto de pruebas de penetración en las que se tenga permiso explícito para realizar auditorías de seguridad.

