---
title: "Objetos Com"
date: 2026-01-26
tags:
  - ciberseguridad
  - ingenieria-inversa
---
Los **objetos COM (Component Object Model)** son una tecnología de Microsoft que permite que diferentes aplicaciones y componentes de software se comuniquen entre sí de forma reutilizable, incluso si están escritos en distintos lenguajes de programación.

---

###  ¿Qué es COM?


> **Relacionado**: [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[01-Ciberseguridad/Herramientas/Cobalt-Strike|Cobalt Strike]]. [[01-Ciberseguridad/Fundamentos/Conceptos-basicos-de-la-seguridad-en-el-software|Conceptos basicos de la seguridad en el software]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]]. [[01-Ciberseguridad/Desarrollo-Seguro/2025-02-20-Seguridad-iOS-memoria-permisos-y-sandboxing|2025 02 20 Seguridad iOS memoria permisos y sandboxing]].

COM es un modelo binario de componentes que define cómo los objetos pueden **exponerse y utilizarse en tiempo de ejecución** sin necesidad de conocer su código fuente. Fue una piedra angular del desarrollo de software en Windows durante décadas.

---

###  ¿Cómo funciona?

- Cada objeto COM **expone interfaces** (conjuntos de métodos).
    
- Las aplicaciones interactúan con los objetos **a través de estas interfaces**, no acceden directamente al objeto.
    
- Los objetos están registrados en el sistema mediante **CLSID** (identificador único) y pueden usarse mediante su nombre o GUID.
    
- El acceso se hace dinámicamente a través de funciones como `CoCreateInstance`.
    

Ejemplo simplificado:

```cpp
IUnknown* pObj;
HRESULT hr = CoCreateInstance(CLSID_MiObjeto, NULL, CLSCTX_INPROC_SERVER, IID_IMiInterfaz, (void**)&pObj);
```

---

###  Componentes clave

- **CLSID (Class ID)**: Identificador único de cada clase COM.
    
- **IID (Interface ID)**: Identificador de cada interfaz.
    
- **IUnknown**: La interfaz base de todos los objetos COM.
    
- **OLE / ActiveX**: Tecnologías basadas en COM.
    
- **DCOM (Distributed COM)**: Extiende COM para trabajar en red.
    

---

###  ¿Dónde se usan?

- En Windows, casi todo: **Explorer, Office, WMI, servicios del sistema**.
    
- Se usa en scripts (VBScript, PowerShell) para interactuar con aplicaciones (por ejemplo, Excel o Word).
    
- Muchos **malware** y herramientas ofensivas (como Cobalt Strike, Metasploit o Empire) lo usan para:
    
    - Ejecutar comandos de forma sigilosa
        
    - Bypassear UAC
        
    - Invocar funciones de forma indirecta (Living off the Land)
        

---

### ️ Seguridad y COM

- **Objetos COM vulnerables** pueden ser explotados para escaladas de privilegios, ejecución remota o persistencia.
    
- **COM hijacking**: Técnica de persistencia donde un atacante registra un objeto COM falso que será cargado por un proceso legítimo.
    
- Algunas herramientas de defensa, como Sysinternals o Autoruns, permiten revisar qué objetos COM están registrados y cargados por procesos.
    

---

Si quieres, puedo mostrarte un ejemplo real de cómo usar un objeto COM en PowerShell para ejecutar algo sin usar `cmd.exe`, o cómo detectar hijacking de COM en un sistema. ¿Te interesa esa parte práctica o quieres seguir con la parte teórica?