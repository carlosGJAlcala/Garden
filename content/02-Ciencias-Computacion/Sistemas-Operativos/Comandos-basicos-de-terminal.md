---
title: "Escribe lo que quieras"
date: 2026-01-26
tags:
  - ciencias-computacion
  - sistemas-operativos
---
Te reordeno y amplío estos apuntes para que tengas una **chuleta de comandos básicos de Linux y Windows**, pero también con el contexto de para qué sirve cada cosa y algunos trucos.

---

## **Comandos básicos de terminal (Linux, macOS, Windows)**


> **Relacionado**: [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[00-Inicio/HOME|HOME]]. [[01-Ciberseguridad/Forense/guia/Lectura-y-escritura-coordinada-entre-procesos-sin-kernel|Lectura y escritura coordinada entre procesos sin kernel]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema3Gobierno_PoliticasSeguridad/Sistema-de-Gestion-de-la-Seguridad-de-la-Informacion|Sistema de Gestion de la Seguridad de la Informacion]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-13-TPM-UEFI-y-sistemas-Anticheat|2025 02 13 TPM UEFI y sistemas Anticheat]].

### **1. Ubicación y navegación**

- **Saber en qué carpeta estamos**
    
    ```bash
    pwd
    ```
    
    (_Print Working Directory_) → muestra la ruta actual.
    
- **Cambiar de carpeta**
    
    ```bash
    cd carpeta
    cd ..       # Subir un nivel
    cd ~        # Ir al directorio home
    cd /        # Ir a la raíz del sistema
    ```
    

---

### **2. Crear directorios y archivos**

- **Linux / macOS**:
    
    ```bash
    mkdir nombre_directorio
    touch archivo.txt
    ```
    
- **Windows (CMD)**:
    
    ```cmd
    md nombre_directorio
    type nul > archivo.txt
    ```
    

---

### **3. Listar contenido**

- **Básico**:
    
    ```bash
    ls
    ```
    
- **Con detalles y tamaño legible**:
    
    ```bash
    ls -lh
    ```
    
- **Incluir archivos ocultos**:
    
    ```bash
    ls -a
    ```
    

---

### **4. Mover, renombrar y copiar**

- **Mover o renombrar**:
    
    ```bash
    mv origen destino
    mv pruebas test   # Renombrar
    ```
    
- **Copiar**:
    
    ```bash
    cp origen destino
    cp archivo.txt ../   # Copiar a carpeta superior
    ```
    
- **Copiar recursivamente**:
    
    ```bash
    cp -r carpeta destino
    ```
    

---

### **5. Borrar**

- **Borrar archivos**:
    
    ```bash
    rm archivo.txt
    ```
    
- **Borrar recursivamente y forzar**:
    
    ```bash
    rm -rf carpeta
    ```
    

---

### **6. Ayuda y manuales**

- **Ver ayuda de un comando**:
    
    ```bash
    man ls
    ```
    
    Navegación dentro de `man`:
    
    - **Espacio** → Avanzar
        
    - **b** → Retroceder
        
    - **q** → Salir
        

---

### **7. Ver contenido de archivos**

- **Mostrar todo**:
    
    ```bash
    cat archivo.txt
    ```
    
- **Mostrar primeras líneas**:
    
    ```bash
    more archivo.txt
    less archivo.txt
    ```
    
- **Mostrar últimas líneas**:
    
    ```bash
    tail archivo.txt
    ```
    

**Truco**: Crear un archivo y escribir en él directamente:

```bash
cat > texto.md
# Escribe lo que quieras
# CTRL+D para guardar y salir
```

---

### **8. Pila de directorios**

- **Guardar ubicación y cambiar de carpeta**:
    
    ```bash
    pushd carpeta
    ```
    
- **Volver a la carpeta anterior**:
    
    ```bash
    popd
    ```
    

---

### **9. Abrir archivos**

- **macOS / Linux**:
    
    ```bash
    open archivo.txt         # macOS
    xdg-open archivo.txt     # Linux
    open -a "Programa" archivo.txt  # Abrir con programa específico
    ```
    
- **Windows (CMD)**:
    
    ```cmd
    start archivo.txt
    ```
    

---

### **10. Variables de entorno**

- **Ver dónde está un comando**:
    
    ```bash
    which comando
    ```
    
- **Ver el PATH**:
    
    ```bash
    echo $PATH
    ```
    
- **Definir variable temporal**:
    
    ```bash
    export VAR=valor
    ```
    
- **Variables persistentes**:
    
    - Editar `~/.bash_profile` o `~/.bashrc`.
        
    - Añadir:
        
        ```bash
        export VAR=valor
        ```
        
    - Guardar y aplicar:
        
        ```bash
        source ~/.bash_profile
        ```
        

---

 **Nota**: Cada vez que abres la terminal, se ejecuta un **shell** (como `bash`) que carga configuraciones desde archivos como `.bash_profile` o `.bashrc`, donde se definen variables, alias y funciones personalizadas.

---

Si quieres, puedo prepararte **una tabla comparativa con todos estos comandos en Linux/macOS y su equivalente en Windows**, así podrías usarla como guía rápida para ambos sistemas.  
¿Quieres que te la haga?