---
title: "Encriptacion Homomorfica"
date: 2026-01-26
tags:
  - ciberseguridad
  - criptografia
---
### **Cifrado Homomórfico: Procesamiento Seguro de Datos Cifrados**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Criptografia/OpenSSL|OpenSSL]]. [[01-Ciberseguridad/Fundamentos/SSLTRIP|SSLTRIP]]. [[01-Ciberseguridad/Fundamentos/ELPSCRK/HashCat|HashCat]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]].

El **cifrado homomórfico** es un tipo de cifrado que permite realizar operaciones matemáticas sobre datos cifrados sin necesidad de descifrarlos. Una vez se descifran los resultados, estos coinciden con los que se habrían obtenido si las operaciones se hubieran realizado sobre los datos en texto claro.

Este enfoque permite delegar cálculos a terceros sin comprometer la confidencialidad de la información, lo que lo hace ideal para aplicaciones en **computación en la nube, análisis de datos y seguridad en el procesamiento de información sensible**.

---

## **Características Principales del Cifrado Homomórfico**

1. **Operaciones sobre datos cifrados:** Se pueden realizar **sumas, multiplicaciones u otras funciones** sin necesidad de descifrar los datos.
2. **Confidencialidad Garantizada:** Los datos permanecen protegidos incluso cuando se procesan en servidores externos.
3. **Reducción de Riesgos de Seguridad:** Minimiza la exposición a ataques en entornos de terceros, como la nube.
4. **Aplicaciones en Big Data y Machine Learning:** Permite analizar información privada sin comprometer la privacidad del usuario.

---

## **Tipos de Cifrado Homomórfico**

Dependiendo del conjunto de operaciones que se pueden realizar sobre los datos cifrados, el cifrado homomórfico se clasifica en distintos tipos:

### **1. Cifrado Homomórfico Parcial (PHE - Partial Homomorphic Encryption)**

Permite realizar solo un tipo de operación (suma o multiplicación) de forma ilimitada.

- **Ejemplo:** **RSA** admite multiplicaciones, mientras que **Paillier** permite sumas.
- **Uso:** Aplicaciones específicas como votaciones electrónicas y micropagos.

### **2. Cifrado Homomórfico Algo Parcial (SHE - Somewhat Homomorphic Encryption)**

Permite tanto sumas como multiplicaciones, pero con un número limitado de operaciones antes de que el ruido acumulado haga inservible el mensaje cifrado.

- **Ejemplo:** **BFV y BGV**, basados en teoría de números y álgebra lineal.
- **Uso:** Análisis de datos médicos y financieros en la nube.

### **3. Cifrado Homomórfico Completamente (FHE - Fully Homomorphic Encryption)**

Permite realizar **cualquier número de sumas y multiplicaciones** sin necesidad de descifrar los datos en ningún momento.

- **Ejemplo:** **Gentry (2009)** fue la primera implementación práctica de FHE.
- **Uso:** Computación segura en la nube y análisis de datos sin exponer información sensible.

---

## **Ejemplo de Funcionamiento del Cifrado Homomórfico**

Supongamos que queremos realizar la suma de dos números sin revelar su valor.

1. **Cifrado de los datos:**
    - Usuario cifra `5` y `3` con un esquema homomórfico, obteniendo `E(5)` y `E(3)`.
2. **Operación sobre datos cifrados:**
    - Se realiza la operación `E(5) + E(3) = E(8)`.
3. **Descifrado del resultado:**
    - El usuario descifra `E(8)`, obteniendo `8`, sin que el servidor haya conocido los valores originales.

Este mismo proceso se puede extender a cálculos más complejos en bases de datos cifradas y modelos de inteligencia artificial.

---

## **Aplicaciones del Cifrado Homomórfico**

1. **Computación en la Nube Segura:** Permite procesar datos en servidores externos sin exponer información confidencial.
2. **Sanidad y Datos Médicos:** Permite análisis estadísticos y entrenamientos de modelos de IA en datos de pacientes sin violar la privacidad.
3. **Banca y Finanzas:** Facilita la auditoría de transacciones y cálculos de riesgos sin necesidad de compartir información sensible.
4. **Machine Learning sobre Datos Cifrados:** Modelos de inteligencia artificial pueden entrenarse sobre datos cifrados sin comprometer la privacidad de los usuarios.
5. **Votaciones Electrónicas:** Se puede contar votos sin revelar individualmente qué opción eligió cada votante.

---

## **Desafíos del Cifrado Homomórfico**

- **Altos Costes Computacionales:** Los cálculos sobre datos cifrados son significativamente más lentos que los cálculos convencionales.
- **Complejidad Matemática:** Requiere estructuras algebraicas avanzadas para su implementación eficiente.
- **Ruido en los Cálculos:** Algunos esquemas homomórficos acumulan ruido en cada operación, lo que limita la cantidad de cálculos posibles antes de necesitar un proceso de "limpieza" de ruido.

---

## **Conclusión**

El cifrado homomórfico es una tecnología revolucionaria que permite procesar datos sin comprometer su confidencialidad. Aunque aún presenta desafíos en términos de rendimiento, su potencial para aplicaciones en seguridad, privacidad y computación en la nube lo convierte en una de las áreas más prometedoras en el campo de la criptografía.