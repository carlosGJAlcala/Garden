---
title: "Contenidos"
date: 2026-01-26
tags:
  - ciberseguridad
  - fundamentos
---

# Contenidos


> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[02-Ciencias-Computacion/Sistemas-Operativos/UNIX/carpetas|carpetas]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]]. [[01-Ciberseguridad/Comunicaciones-Seguras/Practica-1-Apendice-Programacion-con-sockets-en-Python-Master-IoT-UCM-Practicas-RPIANIOTLSI-2425|Practica 1 Apendice Programacion con sockets en Python Master IoT UCM Practicas RPIANIOTLSI 2425]]. [[Introduccion-a-la-Criptografiaseguridad|12 Introduccion a la Criptografiaseguridad]].

1. **Seguridad en el software**
    1. **Importancia de la seguridad del software**
    2. **La seguridad y el ciclo de vida del desarrollo del software**
    3. **Objetivos principales del desarrollo de software seguro**
    4. **Principios de diseño seguro**
2. **El ciclo de vida del desarrollo de software seguro**
    1. **Desafíos del desarrollo de software seguro**
    2. **Normativas y metodologías para el desarrollo de software seguro**
    3. **Actividades y buenas prácticas durante el ciclo de vida del desarrollo de software seguro**

---

# Seguridad en el software

## Importancia de la seguridad del software

El software es crucial en nuestra vida, y cualquier amenaza a este representa una amenaza real para nuestra seguridad.  
El 70% de las vulnerabilidades se encuentran en el software, en lugar de los límites de la red. Sin embargo, el desarrollo de software comercial actual enfrenta varias limitaciones:

- Las prácticas comunes de los sistemas de información permiten errores que comprometen millones de ordenadores.
- Existe una falta de controles rigurosos para producir software seguro.

El software es la causa principal de la mayoría de los problemas de seguridad, convirtiéndose en el objetivo principal de los atacantes. Esto genera un coste innecesario elevado durante el desarrollo, ya que aumenta significativamente el coste en las etapas avanzadas del **[Ciclo de vida del desarrollo del software (SDLC)]**.

---

## La seguridad y el ciclo de vida del desarrollo del software

Históricamente, la industria se ha centrado en la seguridad de los sistemas en los límites de la red, ignorando en gran medida las aplicaciones. Sin embargo, la **seguridad del software** y la **seguridad de las aplicaciones** son conceptos distintos:

- **Seguridad del software:** Se refiere a diseñar e implementar software seguro desde el principio.
- **Seguridad en las aplicaciones:** Protege el software una vez que está en uso, aplicando capas de defensa en profundidad.

La mayoría de los diseños asumen que el software es intrínsecamente seguro y centran sus esfuerzos en los límites de la red o las aplicaciones, lo cual no siempre es suficiente. A menudo, la calidad y la seguridad parecen objetivos distintos, aunque ambos deberían complementarse.

### Diferencias clave:

- **Calidad del software:** Busca resultados esperados, eficiencia, facilidad de uso, reutilización y mantenimiento.
- **Seguridad del software:** Se centra en proteger los datos y sistemas contra amenazas específicas.

Ambos conceptos deberían retroalimentarse para lograr un desarrollo más eficiente y seguro.

---

## Objetivos principales del desarrollo de software seguro

El desarrollo de software seguro debe garantizar los tres pilares fundamentales de la seguridad, conocidos como **CID**:

- **Confidencialidad:** Evitar el acceso y la divulgación no autorizada de información.
- **Integridad:** Prevenir la modificación o destrucción no autorizada de datos.
- **Disponibilidad:** Garantizar un acceso fiable y continuo a los recursos.

---

## Principios de diseño seguro

* Las tres leyes de Adi Shamir (uno de los creadores de RSA):
	* No existe un sistema absolutamente seguro. 
	* Para reducir a la mitad las vulnerabilidades, hay que duplicar la inversión.
	* La criptografía habitualmente no se rompe, sino que se evita”.
* Defensa en profundidad
* Los fallos del sistema deben desembocar en un estado seguro
	* Ejemplo : Cortafuego denegar ante cualquier duda.
* Mínimo Privilegio
	* Los permisos tiene que ser los mínimos necesarios  y el menor tiempo posible
* Economía de mecanismos
* Compartición mínima de estado entre mecanismos 
	* Ejemplo carpetas compartidas
* Reticencia a confiar o Zero Trust 
* Nunca asumas que tu secretos están a salvo
* Mediación completa
	* Cualquier acceso debe ser verificado
* Usabilidad
	* La seguridad siempre añade una sobrecarga hay que intentar que sea la mínima posible
* Visibilidadl y transparencia (Que sea verificable)
* Enfoque centrado en el usuario (por que el usuario es el elemenot más debil de la cadena de seguirda)
* Fomento de la privacidad
	* Privacidad incrustada en el diseño
	* proactivo y preventivo
	* funcionalidad total y privacidad
# El ciclo de vida del desarrollo de software seguro

## Desafíos del desarrollo de software seguro

## Normativas y metodologías para el desarrollo de software seguro

### Modelos SDL 
Microsfot sdl ha envulaciaondo durante más de una década y es considerado el más maudro de todos  ayuda a los responsables a evaluar su estado actual y gradualmente adoptar el programa probado de microst para producr software más seguro.

   
## Actividades y buenas prácticas durante el ciclo de vida del desarrollo de software seguro