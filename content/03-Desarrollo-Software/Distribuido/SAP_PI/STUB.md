---
title: "Stub"
date: 2026-01-26
tags:
  - desarrollo-software
  - distribuido
  - sap_pi
---


En el contexto de **SOAP, WSDL y Apache Axis**, los **stubs** son piezas de código **generadas automáticamente** que sirven de **puente** entre tu aplicación y el servicio web.

###  Explicación simple


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[02-Ciencias-Computacion/Redes/Herramientas|Herramientas]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

- Cuando tienes un **WSDL**, este describe cómo es el servicio: qué métodos tiene, qué parámetros recibe, qué devuelve.
    
- A partir de ese WSDL, Axis (u otras herramientas) puede **generar código en tu lenguaje** (por ejemplo, Java).
    
- Ese código son los **stubs**.
    

Los stubs te permiten llamar a un servicio web como si fuera una función normal de tu programa, sin tener que preocuparte por construir manualmente el XML SOAP ni enviar la petición HTTP.

---

###  Cómo funcionan

1. Tú llamas en tu código algo como:
    

```java
int resultado = calculadora.suma(2, 3);
```

2. El **stub** automáticamente convierte esa llamada en:
    
    - Construir el XML SOAP.
        
    - Enviarlo por HTTP al servidor.
        
    - Recibir la respuesta SOAP.
        
    - Parsear el XML y devolverte el resultado como un número entero (`5`).
        
3. Para ti, parece que llamaste a una función local, pero en realidad hiciste una **llamada remota a un servicio web**.
    

---

###  Ejemplo rápido (Java con Axis)

Supongamos que el WSDL describe un servicio de calculadora. Axis puede generar un stub en Java parecido a esto:

```java
CalculadoraService service = new CalculadoraServiceLocator();
Calculadora port = service.getCalculadora();

int resultado = port.suma(2, 3);
System.out.println("Resultado: " + resultado);
```

- `CalculadoraService` y `Calculadora` son **stubs generados a partir del WSDL**.
    
- Internamente, estos stubs se encargan de todo el trabajo sucio: crear el SOAP request, enviarlo por HTTP y procesar el response.
    

---

###  En resumen

Los **stubs** son código generado a partir del **WSDL** que actúa como **cliente automático** del servicio web.

- Te permiten **llamar métodos remotos como si fueran locales**.
    
- Evitan que tengas que **escribir a mano el XML SOAP y manejar HTTP**.
    

---

