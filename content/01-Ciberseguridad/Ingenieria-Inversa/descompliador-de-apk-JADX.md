---
title: "Descompliador De Apk Jadx"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
¡Perfecto ! Vamos a preparar unas **notas extensas, densas y técnicas sobre `jadx`**, una herramienta clave en **pentesting móvil y análisis de aplicaciones Android**. Ideal para incluir en tus apuntes avanzados sobre reversing y auditorías móviles.

---

###  **jadx**


> **Relacionado**: [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

####  **¿Qué es jadx?**

- **`jadx` es un descompilador open-source para archivos APK y DEX (Dalvik Executable) de Android**.
    
- Permite convertir los archivos `.dex` (código bytecode Dalvik) en:
    
    - **Java legible (descompilado).**
        
    - Representación Smali.
        
    - Árbol de clases para análisis estructural.
        

 Su objetivo principal es **permitir a auditores, investigadores y pentesters analizar el código fuente de apps Android incluso cuando no se dispone de los archivos originales `.java`.**

---

####  **¿Por qué es importante en pentesting móvil?**

En contextos de seguridad:  
 **`jadx` permite examinar el código fuente descompilado de APKs, lo que facilita detectar:**

- Secretos incrustados (`hardcoded secrets`).
    
- Claves API.
    
- URLs y endpoints de backend.
    
- Lógica de negocio oculta.
    
- Algoritmos criptográficos incorrectos.
    
- Validaciones en cliente (que podrían ser bypassed).
    
- Autenticaciones inseguras.
    
- “Obfuscation bypass” parcial en apps no muy protegidas.
    

 Muy útil en fases de:

- **Reconocimiento.**
    
- **Reversing.**
    
- **Análisis estático.**
    

---

####  **Características principales**

️ Funcionalidades clave de `jadx`:

- Descompila `.dex` directamente a **Java legible**.
    
- Analiza APK completos (extrae internamente `classes.dex` y recursos).
    
- Permite navegar clases y métodos fácilmente en su **versión GUI (`jadx-gui`)**.
    
- Exporta código fuente completo a un directorio para revisión offline.
    
- Soporta versiones modernas de Android bytecode.
    

---

####  **Cómo instalar `jadx`**

 **Método 1 - Linux (con `apt` en distribuciones como Kali):**

```bash
sudo apt install jadx
```

 **Método 2 - Descargar releases oficiales:**

- [https://github.com/skylot/jadx/releases](https://github.com/skylot/jadx/releases)
    
- Archivos `.zip` precompilados.
    

 **Método 3 - Compilación desde fuente:**

```bash
git clone https://github.com/skylot/jadx.git
cd jadx
./gradlew dist
```

---

####  **Modos de uso**

 **Modo CLI:**

- Descompilar APK completo:
    
    ```bash
    jadx -d output/ app.apk
    ```
    

 **Modo GUI (`jadx-gui`):**

- Interfaz gráfica muy útil para navegar clases, paquetes, métodos y revisar código manualmente:
    
    ```bash
    jadx-gui app.apk
    ```
    

---

####  **Salida típica**

- `jadx` crea una estructura de carpetas:
    
    ```
    output/
    ├── AndroidManifest.xml
    ├── resources/
    └── sources/
        ├── com/example/MainActivity.java
        └── com/example/utils/CryptoUtils.java
    ```
    

 **Muy útil para analizar la lógica de la app desde el punto de vista del atacante → sin código fuente original.**

---

####  **Ejemplo práctico en pentesting**

 **Escenario realista:**  
1️⃣ **El pentester recibe `app.apk` de una app Android objetivo.**

2️⃣ Descompila con `jadx`:

```bash
jadx -d salida/ app.apk
```

3️⃣ Navega el código fuente resultante:

- Busca hardcoded credentials:
    
    ```java
    String API_KEY = "sk_test_abc123";
    ```
    
- Detecta endpoints:
    
    ```java
    private String baseUrl = "https://api.example.com/v1/";
    ```
    
- Analiza la lógica de validación de JWT tokens, autenticación, cifrado simétrico mal implementado, etc.
    

4️⃣ **Encuentra contraseñas hardcodeadas o secretos que puede usar en etapas posteriores del ataque.**

---

####  **Limitaciones de `jadx`**

️ Puntos críticos:

- **`jadx` no es infalible → la calidad del código descompilado depende del grado de obfuscación usado por el desarrollador original**:
    
    - Proguard/R8 → nombres de clases y métodos pueden aparecer ofuscados (`a()`, `b()`), pero la lógica sigue legible.
        
    - Métodos nativos (`JNI` / `NDK` → `.so` libraries) → no se descompilan (análisis separado requerido con herramientas como Ghidra).
        
- No recupera exactamente el código original → **el resultado es una aproximación funcional** (en algunos casos errores de descompilación por bytecode no estándar).
    

---

####  **Comparativa con otras herramientas**

|Herramienta|Características|Ventaja de `jadx`|
|---|---|---|
|**apktool**|Recompila APKs, extrae resources, genera Smali|`jadx` devuelve código Java de alto nivel|
|**dex2jar + JD-GUI**|Exporta DEX a JAR, visualiza con JD-GUI|`jadx` es más directo y moderno|
|**bytecode-viewer**|Multi-backend decompilation|`jadx` más ligero y especializado|

 **`jadx` se usa habitualmente junto a `apktool`:**

- `apktool`: análisis de `resources` y `AndroidManifest.xml`.
    
- `jadx`: análisis de código fuente.
    

---

####  **Uso habitual en pentesting profesional**

 **Fase de análisis estático en auditoría móvil:**

- Inicia auditoría básica → extraer endpoints/backend API para fuzzing posterior.
    
- Identificar claves API para pruebas de API inseguras (`API Security Testing`).
    
- Analizar lógica de negocio para bypasses (`auth bypass`, `client-side validation`).
    
- Reconstruir algoritmos de cifrado personalizados que pueden ser débiles (`crypto flaws`).
    

---

####  **Mitigaciones para desarrolladores**

 Cómo mitigar riesgos que `jadx` expone:

- **Evitar hardcoding de secretos (usar Keystore, secure vaults).**
    
- **Aplicar ofuscación sistemática de código con herramientas como Proguard/R8.**
    
- Minimizar lógica sensible en cliente:
    
    - Validaciones críticas siempre en backend.
        
    - No almacenar claves privadas, secretos o datos sensibles en APK.
        

---

 **Resumen denso para recordar:**

>  **`jadx` = descompilador open-source moderno para APKs/DEX → convierte bytecode Dalvik a código Java legible.**  
> Usado en pentesting móvil para extraer lógica, secretos hardcoded, endpoints backend, algoritmos criptográficos y analizar la superficie de ataque de aplicaciones Android.  
> Muy potente, ideal en combinación con `apktool` para auditorías completas.

---

 Si quieres puedo prepararte:

-  **Checklist paso a paso para análisis de un APK con `jadx`.**
    
-  **Guía de análisis combinando `jadx` + `apktool` + `MobSF`.**
    

Solo dime  y lo preparo.