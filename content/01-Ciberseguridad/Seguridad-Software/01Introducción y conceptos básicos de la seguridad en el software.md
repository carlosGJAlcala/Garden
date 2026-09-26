# Introducción y conceptos básicos de la seguridad en el software
Fundamentos de la Seguridad en el Software y en los Componentes — Máster Universitario en Ciberseguridad. Susel Fernández Melián.
## Contenidos
- Seguridad en el software
- Importancia de la seguridad del software
- La seguridad y el ciclo de vida del desarrollo del software
- Objetivos principales del desarrollo de software seguro
- Principios de diseño seguro
- El ciclo de vida del desarrollo de software seguro
- Desafíos del desarrollo de software seguro
- Normativas y metodologías para el desarrollo de software seguro
- Actividades y buenas prácticas durante el ciclo de vida del desarrollo de software seguro
## Importancia de la seguridad del software
El software es crucial para todo lo que hacemos en el mundo moderno y está detrás de nuestros sistemas más críticos: energía, transporte, finanzas y banca, telecomunicaciones, salud pública, servicios de emergencia, agua, química, defensa, industria, alimentación, agricultura, etc. Cualquier cosa que amenace ese software, en efecto, representa una amenaza real para nuestra vida.
Más del 70% de las vulnerabilidades de seguridad empresarial se encuentran en las aplicaciones software en lugar de en los límites de la red. Esto revela las limitaciones del desarrollo de software comercial actual: prácticas comunes de ingeniería de software que permiten errores que comprometen millones de ordenadores, y falta de controles para producir software seguro y de calidad a un costo aceptable.
El software inseguro es la causa de la mayoría de los problemas de seguridad de la información que tenemos hoy, y el objetivo principal de los piratas informáticos, los ciberdelincuentes y los guerreros cibernéticos. Los fallos de seguridad de código en productos de software que ya se han lanzado al mercado constituyen el coste innecesario más alto para el desarrollo de software.
El coste de la resolución de problemas de seguridad crece en relación con el avance del ciclo de vida del desarrollo del software ( SDLC): cuanto más tarde se detecta un problema, más caro resulta corregirlo. Las implicaciones de detectar problemas de seguridad después de la implantación incluyen:
- Aumento en el alcance de la vulnerabilidad ( puede afectar a otros: software, servicios, aplicaciones de la nube...)
- Afectación significativa para la empresa
- Interrupciones en los ciclos de desarrollo de productos actuales
- Retrasos en las fechas de lanzamiento del producto
- Problemas legales y degradación de la reputación
> "La diferencia más crítica entre el software seguro y el software inseguro reside en la naturaleza de los procesos y prácticas utilizados para especificar, diseñar y desarrollar el software... corregir las vulnerabilidades potenciales lo antes posible en el ciclo de vida del desarrollo del software, a través de la adopción de procesos y prácticas mejoradas de seguridad, es mucho más rentable que el enfoque generalizado de desarrollo y liberación de parches frecuentes para el software operativo."
> — U.S. Department of Homeland Security, 2006 Draft, "Security in the Software Lifecycle"
## Seguridad en el software vs seguridad en aplicaciones
- Seguridad en el software**: crear software seguro. Diseñar e implementar software para que sea seguro, y educar a los desarrolladores, arquitectos y usuarios de software acerca de cómo construir la seguridad.
- Seguridad en aplicaciones**: proteger el software y los sistemas que se ejecutan de forma post facto, solo después de que se complete el desarrollo.
La industria de la seguridad de la información se ha centrado tradicionalmente en la seguridad de la red y las aplicaciones, suponiendo que el software era seguro. Pero la seguridad del software debe considerarse el primer paso en el ciclo de vida de seguridad de la información; la protección de la red y las aplicaciones debe venir más tarde, dentro de un programa de seguridad integral y en capas de defensa en profundidad.
## Calidad vs seguridad
- Software de calidad**: resultados esperados, eficiencia, facilidad de uso, reusabilidad, mantenimiento.
- Software seguro**: confidencialidad, integridad, disponibilidad.
## Objetivos principales del desarrollo de software seguro
Seguridad de la información: protección de la información y sistemas de información del acceso no autorizado, uso, divulgación, interrupción, modificación o destrucción.
- Confidencialidad**: evitar acceso y divulgación no autorizados.
- Integridad**: prevenir la modificación o destrucción.
- Disponibilidad**: garantizar el acceso fiable y el uso.
## Principios de diseño seguro
## # Las tres leyes de Adi Shamir ( uno de los creadores de RSA)
- No existe un sistema absolutamente seguro.
- Para reducir a la mitad las vulnerabilidades, hay que duplicar la inversión.
- "La criptografía habitualmente no se rompe, sino que se evita."
## # Defensa en profundidad
Disponer de distintas capas de protección "en serie": si alguno de los servicios de seguridad de las capas falla o es sorteado, se puede seguir defendiendo adecuadamente frente a las amenazas.
## # Los fallos del sistema deben desembocar en un estado seguro
Los sistemas van a fallar en algún momento ( por ejemplo, ante situaciones no previstas). Hay que asegurar que, ante fallos, el sistema se comporte de forma segura. Un punto clave es tener un estado fijo conocido al que dirigir el sistema tras un fallo. Ejemplo paradigmático: un cortafuegos que, ante la duda o ante un fallo, deniega todo.
## # Principio del mínimo privilegio
Los permisos o recursos asignados a una entidad deben ser los mínimos necesarios ( los justos para desempeñar la tarea) y deben mantenerse el menor tiempo posible. El objetivo es minimizar los daños derivados de un uso malintencionado, accidental o erróneo de los derechos de acceso, reduciendo así al mínimo posible los perjuicios derivados del compromiso de una cuenta de usuario o programa. Símil: "préstame tus llaves".
## # Separación de privilegios
Necesidad de que se verifiquen de forma simultánea varias condiciones antes de asignar permisos a una entidad. Ejemplos del sistema bancario: es común que las cajas de seguridad dispongan de dos candados cuyas llaves custodian personas distintas, o que los cheques por encima de cierto valor requieran dos firmas.
## # Economía de mecanismos
No incluir mecanismos de seguridad innecesarios: a mayor complejidad, mayor riesgo y mayores dificultades de mantenimiento. Hay que intentar que los mecanismos sean sencillos y fáciles de operar. "Si la seguridad es una cadena, mientras menos eslabones tenga, menos opciones habrá de romperla."
## # Compartición mínima de estado entre mecanismos
Existe peligro al compartir información de estado entre distintos programas: si un programa es capaz de corromper el estado compartido, puede llegar a afectar a otros programas que dependan del mismo. Ejemplo: carpetas compartidas.
## # Reticencia a confiar
Todos los elementos externos a nuestro sistema deben ser considerados inseguros por definición, reduciendo el conjunto de entidades en las que confiamos al mínimo necesario. La confianza es la evidencia suficiente sobre los requisitos del sistema; cabe preguntarse hasta qué punto podemos confiar en sistemas desarrollados por terceros o "en la nube".
## # Nunca asumas que tus secretos están a salvo
Hay que asumir que un atacante puede obtener suficiente información sobre nuestro sistema como para lanzar un ataque. Esto no significa que no publicar abiertamente los detalles del sistema no pueda ser un componente de una estrategia de defensa; solo que no puede ser nuestra única defensa.
## # Mediación completa
Cualquier acceso que cualquier individuo o entidad quiera realizar a un recurso debe ser verificado explícitamente. No debemos confiar en permisos que hayamos podido guardar en algún sistema de almacenamiento "estable" ( por ejemplo, una caché de permisos), sino verificar en el momento, como ocurre con los cambios de contraseña.
## # Usabilidad
La seguridad debe ser usable: los mecanismos de seguridad no deberían hacer el acceso al recurso más difícil de lo que era cuando no estaban presentes. En la práctica, incorporar seguridad siempre añade sobrecarga; el objetivo es que sea la mínima posible. Las interfaces y opciones de configuración deben ser sencillas e intuitivas, porque si un mecanismo de seguridad es incómodo, los usuarios encontrarán la forma de evitarlo.
## # Visibilidad y transparencia ( mantenerlo abierto)
Cualquier práctica de negocios o tecnología debe operar de acuerdo con las promesas y objetivos declarados. Sus partes componentes y operaciones deben permanecer visibles y transparentes a usuarios y proveedores. El sistema debe estar abierto a la verificación.
## # Enfoque centrado en el usuario
El usuario es el eslabón fundamental y el "más débil". Debe estar en el centro de las prioridades, ofreciéndole notificación apropiada, opciones amigables y predefinidos de privacidad robustos.
## # Fomento de la privacidad
Dar al usuario el control sobre su información personal: posibilidad de gestionar quién, cómo y para qué tiene acceso a información personal. En palabras de Bruce Schneier: "Privacy is an inherent human right, and a requirement for maintaining the human condition with dignity and respect."
Principios básicos de privacidad desde la fase de diseño de cualquier producto:
- Privacidad incrustada en el diseño**: debe estar incrustada en el diseño y la arquitectura de los sistemas de TIC y en las prácticas de negocio, no como un añadido posterior. Tiene que ser un componente esencial de la funcionalidad central que se entrega, parte integral del sistema, sin disminuir su funcionalidad.
- Enfoque proactivo, no reactivo; preventivo, no correctivo**: anticipar y prevenir eventos de invasión de privacidad antes de que ocurran, sin esperar a que los riesgos se materialicen ni ofrecer remedios una vez ocurridas las infracciones. Su finalidad es prevenir que ocurran.
- Privacidad como configuración predeterminada**: ofrecer el máximo grado de privacidad asegurando que los datos personales estén protegidos automáticamente en cualquier sistema o práctica de negocio. Aunque una persona no tome ninguna acción, la privacidad debe mantenerse intacta.
- Funcionalidad total y privacidad**: la privacidad de un sistema no debe fundamentarse en concesiones o soluciones de compromiso en el contexto de una falsa dialéctica funcionalidad vs. privacidad. Se busca tener funcionalidad y privacidad al mismo tiempo.
- Seguridad extremo a extremo**: protección del ciclo de vida completo de la información. Garantizar que todos los datos sean almacenados con seguridad y luego destruidos con seguridad al final del proceso, sin demoras. Administración segura del ciclo de vida de la información, desde el principio hasta el final.
## Iniciativas para el desarrollo de software seguro
SDL ( Secure Development Lifecycle): ciclo de vida del desarrollo seguro. Modelos SDL: OWASP SDL, CISCO SDL ( SCISCO), Microsoft SDL.
**Microsoft SDL** ha evolucionado durante más de una década y es considerado el más maduro de todos los modelos. Facilita la implementación gradual, consistente y rentable del SDL por parte de organizaciones de desarrollo fuera de Microsoft, y ayuda a los responsables de seguridad a evaluar su estado actual y adoptar gradualmente el programa probado de Microsoft para producir software más seguro.
## Otros recursos para buenas prácticas SDL
- Modelos de madurez de seguridad de software**: proporcionan una forma eficaz y medible para que las organizaciones analicen y mejoren su postura en seguridad de software. Ejemplo: SAMM de OWASP ( https://owaspsamm.org/about/).
- ISO/IEC 27034** — Tecnologías de la información/Técnicas de seguridad/Seguridad de aplicaciones: estándar internacional para la seguridad de las aplicaciones.
- SAFECode** ( Software Assurance Forum for Excellence in Code): organización sin fines de lucro que reúne a líderes empresariales y expertos técnicos para intercambiar conocimientos e ideas sobre la creación, mejora y promoción de programas para la seguridad del software ( https://safecode.org/).
- Programa de Garantía de Seguridad del Software** del Departamento de Seguridad Nacional de EE. UU.: patrocinador de Build Security In ( BSI), que ofrece herramientas, pautas y principios para incorporar seguridad en el software en cada fase de su ciclo de desarrollo. Incluye distintos programas e iniciativas dirigidos a reducir las vulnerabilidades de software, y es co-patrocinador de CWE ( Common Weakness Enumeration).
- NIST** ( National Institute of Standards and Technology): NIST SAMATE ( Software Assurance Metrics And Tool Evaluation); NIST Special Publication, Security Considerations in the System Development Life Cycle ( https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-64r2.pdf); NVD ( The National Vulnerability Database); CVSS ( Common Vulnerability Scoring System).
- MITRE CVE** ( Common Vulnerabilities and Exposures): lista de vulnerabilidades de seguridad de la información que tiene como objetivo proporcionar nombres comunes para problemas conocidos públicamente. Estándar para la identificación y descripción de vulnerabilidades.
- Instituto SANS** ( SysAdmin Audit, Networking and Security), Top Cyber Security Risks: lista consensuada de las áreas problemáticas más críticas en seguridad de Internet.
- CERT** ( Computer Emergency Readiness Team, Carnegie Mellon): proporciona alertas sistemáticas sobre vulnerabilidades de seguridad, así como un boletín semanal resumido sobre vulnerabilidades.
## Operaciones y herramientas utilizadas en SDL
- Análisis estático ( SAST)**: analizar una versión del código fuente sin llegar a ejecutar el programa ( RATS, Coverity...).
- Fuzzing**: encontrar errores de implementación o fallas de seguridad inyectando datos malformados de manera automatizada ( Codenomicon, Peach Fuzzer...).
- Análisis dinámico ( DAST)**: ejecución de programas en un procesador real o virtual en tiempo real para encontrar errores de seguridad mientras se está ejecutando ( HP Webinspect, Whitehat Sentinel Source...).
## Métricas de seguridad
Son críticas a medida que las corporaciones lidian con los requisitos regulatorios y de gestión de riesgos. Permiten determinar la efectividad de los controles de seguridad. Es importante tener un mecanismo centralizado de informes de métricas para proporcionar una evaluación continua del estado de la seguridad del producto.
## Metodologías de desarrollo de software
## # Metodologías tradicionales
Desarrollo de software predecible y por ello eficiente: enfoque predictivo, donde se sigue un proceso secuencial en una sola dirección y sin marcha atrás. La estimación y captura de requisitos se realiza una única vez al principio del proyecto, con un proceso riguroso de captura de requisitos, análisis, diseño y desarrollo. Es útil cuando se tiene mucha experiencia con un determinado tipo de producto y ya se sabe estimarlo, y en proyectos donde los requisitos no cambian y las condiciones del entorno son conocidas y estables. Ejemplo: desarrollo en cascada ( planificación, construcción, evaluación, revisión, despliegue).
## # Metodologías de desarrollo ágil
Adaptativas y flexibles: los requisitos y funcionalidades pueden cambiar en cualquier momento. Se basan en la comunicación e implicación del cliente ( que suele ser parte del equipo). El trabajo se fragmenta en partes que se priorizan y desarrollan durante un periodo de tiempo corto, anteponiendo el valor aportado al producto sobre otras tareas. Son útiles en entornos cambiantes donde no está claro el problema a solucionar, ni la forma de hacerlo.
## # Diferencias entre metodologías tradicionales y ágiles
| | Metodologías tradicionales | Metodologías ágiles |
| --- | --- | --- |
- Base
 - Normas provenientes de estándares seguidos por el entorno de desarrollo
 - Heurísticas provenientes de prácticas de producción de código
- Cambios
 - Resistencia a los cambios
 - Especialmente preparadas para cambios
- Control
 - Más controlado, con numerosas políticas/normas
 - Menos controlado, pocas normas y más flexibles
- Cliente
 - Interactúa con el equipo de desarrollo mediante reuniones esporádicas
 - Es parte del equipo de desarrollo
- Equipo
 - Grupos grandes y posiblemente distribuidos
 - Grupos pequeños ( menos de 10 integrantes) trabajando en el mismo sitio
- Foco
 - Arquitectura del software, expresada mediante modelos
 - Funcionalidad por encima de la arquitectura ( menos modelos)
- Contrato
 - Existe un contrato prefijado
 - No existe contrato tradicional o es bastante flexible
## Actividades y buenas prácticas en SDL
¿En qué consiste una metodología SDL? En añadir a las metodologías existentes las acciones relacionadas con la seguridad en todas las fases del ciclo de vida del desarrollo: conceptual, planificación, diseño y desarrollo, puesta a punto, implantación, soporte y mantenimiento.
## # A1: Evaluación de la seguridad ( fase conceptual)
Se conforma el equipo de seguridad de software, que organiza una reunión de descubrimiento y crea un plan de proyecto de desarrollo del software, estableciendo el trabajo adicional a realizar. Se inicia el plan de evaluación de impacto de privacidad ( PIA).
Métricas: tiempo en semanas en que el equipo de seguridad de software fue involucrado; % de partes interesadas que participan en SDL; % de actividades SDL asignadas a actividades de desarrollo; objetivos de seguridad y % de objetivos de seguridad cumplidos.
## # A2: Arquitectura ( fase de planificación)
Modelado de amenazas y análisis de seguridad de la arquitectura, selección de código de terceros, recopilación y análisis de información de privacidad.
Métricas: modelo de amenazas comerciales, técnicas y actores involucrados; número de objetivos de seguridad no cumplidos después de esta fase; % de cumplimiento de las políticas de la empresa; número de puntos de entrada para el software; % de riesgo aceptado, mitigado y transferido; número de cambios de arquitectura del software necesarios según los requisitos de seguridad.
## # A3: Diseño y desarrollo ( parte 1)
Composición del plan de prueba de seguridad, análisis estático, actualización del modelo de amenazas, diseño de las pruebas de seguridad y revisión, evaluación de implementación de privacidad.
Métricas: amenazas, probabilidad y severidad; % de cumplimiento de las políticas de la empresa ( fase 2 frente a fase 3); puntos de entrada para el software; % de riesgo aceptado vs. mitigado; % de requisitos iniciales de software redefinidos; % de cambios en la arquitectura del software; número de líneas de código; defectos de seguridad y de alto riesgo encontrados en el análisis estático; densidad del defecto ( problemas de seguridad por 1000 líneas de código).
## # A4: Diseño y desarrollo ( parte 2, puesta a punto)
Ejecución de tests de casos de seguridad, análisis estático, análisis dinámico, fuzzing, revisión manual del código, validación de la privacidad y remediación.
Métricas: % de cumplimiento en la fase 3 vs. la fase 4; número de líneas de código probadas efectivamente con análisis estático; número de defectos de seguridad y de alto riesgo encontrados en análisis estático; densidad del defecto; número y tipos de problemas de seguridad encontrados en análisis estático, análisis dinámico, revisión manual de código y fuzzing; número de resultados de seguridad remediados; número, tipos y gravedad de los hallazgos pendientes; % de cumplimiento del plan de prueba de seguridad; número de casos de prueba de seguridad ejecutados.
## # A5: Montaje ( implantación)
Escaneo de vulnerabilidades, tests de penetración, revisión de las licencias de terceros, revisión final de seguridad, revisión final de privacidad.
Métricas: % de cumplimiento en la fase 5 vs. la fase 4; número, tipo y gravedad de los problemas de seguridad encontrados a través del escaneo de vulnerabilidades y las pruebas de penetración; número de resultados de seguridad remediados ( actualizado); número, tipos y gravedad de los hallazgos pendientes ( actualizado); % de cumplimiento de los requisitos de seguridad y privacidad.
## # Soporte post-lanzamiento
Respuesta de divulgación de vulnerabilidad externa, revisiones de terceros, certificaciones post-lanzamiento, revisión interna para nuevas combinaciones de productos o implementaciones en la nube, revisiones de arquitectura de seguridad y evaluaciones basadas en herramientas y soluciones actuales, heredadas y para fusiones y adquisiciones.
Métricas: tiempo en horas para responder a vulnerabilidades de seguridad divulgadas externamente; horas mensuales de trabajadores de tiempo completo requeridas para el proceso de divulgación externa; número de hallazgos de seguridad ( clasificados por gravedad) después de que el producto ha sido lanzado; número de problemas de seguridad informados por el cliente por mes.
## Conclusiones
El software es crucial para todo lo que hacemos y está detrás de nuestros sistemas más críticos. Cualquier cosa que amenace ese software representa una amenaza real para nuestra vida. La seguridad del software consiste en diseñar e implementar software para que sea seguro, siguiendo unos principios de diseño seguro. Existen herramientas y metodologías que facilitan el desarrollo de código seguro durante todo el ciclo de vida ( SDL).
