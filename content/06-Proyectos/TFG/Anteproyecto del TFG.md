---
title: "Anteproyecto del TFG"
tags: [universidad, 4anyo, tfg]
date: 2026-08-12
lang: es
---
Trabajo Fin de Carrera 
Desarrollo de una aplicación web con tecnologías modernas, conectada a un sistema SCADA
Carlos Garrido Junco
Grado en Ingeniería en Computadores
Escuela Politécnica
Universidad de Alcalá 
e-mail@uah.es
**Palabras clave.** Trabajo Fin de Carrera, Ingeniería.
# Contenido
[1 Introducción [3](#introducción)](#introducción)
[2 Objetivos [5](#objetivos)](#objetivos)
[Objetivos específicos: [5](#objetivos-específicos)](#objetivos-específicos)
[3 Resultados [6](#resultados)](#resultados)
[4 Metodología [7](#metodología)](#metodología)
[5 Recursos [9](#recursos)](#recursos)
[6 Bibliografía [10](#bibliografía)](#bibliografía)
[7 Planificación [11](#planificación)](#planificación)
# 1 Introducción
El presente Trabajo de Fin de Grado ( TFG) se sitúa en el ámbito de las tecnologías de desarrollo web modernas, con un enfoque particular en la combinación de React y Spring para la creación de una aplicación web innovadora. Aunque el proyecto incluye elementos de Internet de las Cosas ( IoT), se pondrá especial énfasis en la aplicación efectiva de estas tecnologías ( React y Spring) en un entorno práctico.
La evolución de nuevas tecnologías, como los frameworks de JavaScript, como React, combinados con marcos de trabajo como Spring, ha resultado en la creación de un entorno sólido y escalable. Este enfoque no solo se limita a la interacción web, sino que se extiende a plataformas como Arduino, facilitando la creación de sistemas embebidos que pueden incorporar fácilmente sensores y actuadores. Estos sistemas embebidos pueden tomar decisiones y recopilar datos, funcionando efectivamente como un sistema SCADA.
Estas tecnologías se usaron para el desarrollo de un huerto automatizado el cual tendrá actuadores y sensores que gestionaran la maceta. Los sensores medirán la luz humedad del suelo y la temperatura y se intentará determinar el estado de las plantas a través de ellos.
**Antecedentes**
La unión de las tecnologías web y del internet de las cosas, han dado fruto a numerosos proyectos como puede ser algunos de los siguientes.
Automated irrigation system with Arduino: Un sistema en el cual se irriga cultivos utilizando la plataforma de Arduino: GUIJARRO-RODRÍGUEZ, Alfonso A., et al. Sistema de riego automatizado con Arduino. Sistema, 2018, vol. 39, no 37, p. 27.Available: <https://revistaespacios.com/a18v39n37/a18v39n37p27.pdf>
Smart Home Automation Systems: proyecto que integran React con Spring para la automatización del hogar con los cuales se pueden controlar la climatización ,iluminación y diferentes aparatos electrónicos:ASADULLAH, Muhammad; RAZA, Ahsan. An overview of home automation systems. En 2016 2nd international conference on robotics and artificial intelligence ( ICRAI). IEEE, 2016. p. 27-31**.**
Integration of the vacuum scada with cern’s enterprise asset management system. Proyecto, para el cern el cual se ha integrado un Sistema SCADA con el framework de spring para el control y la supervision para el control de las cámaras de vacio del CERN: ROCHA, André, et al. INTEGRATION OF THE VACUUM SCADA WITH CERN’S ENTERPRISE ASSET MANAGEMENT SYSTEM. En 16th Int. Conf. on Accelerator and Large Experimental Control Systems ( ICALEPCS'17), Barcelona, Spain, 8-13 October 2017. JACOW, Geneva, Switzerland, 2018. p. 490-494.
Implementación de un sitema SCADA, con un Arduino: HERRERA, Jean; BARRIOS, Mauricio; PÉREZ, Saúl. Diseño e implementación de un sistema scada inalámbrico mediante la tecnología zigbee y arduino. *Prospectiva*, 2014, vol. 12, no 2, p. 65-72.
# 2 Objetivos 
Esta aplicación estará enfocada en el cuidado de cultivos, analizando variables como la humedad, luminosidad y condiciones climáticas. En función de estos datos, se asignarán comportamientos específicos al sistema. Finalmente, el usuario podrá monitorear el estado de sus cultivos directamente desde la aplicación.
## Objetivos específicos:
- Desarrollar un sistema de adquisición de datos controlado por un backend Spring, que almacenará la información en una base de datos.
- Familiarizarse con la creación de aplicaciones web utilizando tecnologías modernas como React,Tailwind CSS y Spring
- Manejo de datos y tomas de decisión en tiempo real.
- Estudio de desarrollo de aplicaciones SCADA en sistemas de cloud computing
- Optimización de procesos como este caso el de la agricultura.
# 3 Resultados
El principal resultado de la realización del proyecto será desarrollar una aplicación destinada a recopilar datos ambientales, en este caso, específicamente de un huerto. Posteriormente, estos datos se exhibirán en una aplicación web que permitirá al usuario realizar acciones, ya sea eligiendo manualmente o a través de procesos automatizados.
La aplicación sigue una estructura de Modelo-Vista-Controlador ( MVC), dividiendo claramente las responsabilidades entre la parte del backend y la del frontend. Para la implementación del backend, se empleará Spring, mientras que React será la tecnología utilizada en la parte del frontend. La totalidad de la aplicación se desplegará en la plataforma RailWay, mediante el uso de contenedores. Este enfoque asegura una separación clara de las funciones y una eficiente gestión del ciclo de vida de la aplicación.
Como se puede observar en la imagen hay dos formas en las que se capta los datos de los sensores se hace através de un Arduino que no tiene modulo de red y se envia los datos através de puerto COM3 con 9600 baudios, y un servidor hecho en node recoge los datos los transforma en json y los manda al backen en srping y la otra opción es hacerlo através de una esp32 que tiene tarjeta de red y un modulo de wifi, y por lo tanto mandaría lo datos por el solo.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/CarlosGarridoJuncoAnteproyecto/media/image1.png]]
Ilustración 1 Diagrama de despliegue de la aplicación
# 4 Metodología
Se ha adoptado una metodología Waterfall para el desarrollo del proyecto, comenzando con la fase de análisis. Este proceso se divide en dos secciones: el análisis de la aplicación frontend y backend. Esta división permite abordar de manera independiente el desarrollo del backend y el frontend. Durante el análisis, se detallarán los requisitos y casos de uso de la aplicación, registrándolos adecuadamente en la documentación. También se explorará el uso de Jenkins, Docker y Azure, aunque su implementación no está establecida de manera rígida en esta etapa.
En la fase de diseño, se seguirá un enfoque secuencial. Se comenzará con el diseño de la base de datos, seguido por el diseño del modelo de dominio de la aplicación y, finalmente, el diseño de la aplicación frontend.
La etapa de configuración abordará aspectos como la configuración del servidor en Azure, la gestión del DNS, y la configuración y despliegue de contenedores en Azure. Además, se utilizará Jenkins para facilitar la integración continua, automatizando el proceso de carga, prueba y despliegue en Azure cada vez que se realiza un push en la cuenta de Git.
En la fase de desarrollo, se empleará la metodología TDD ( Desarrollo Guiado por Pruebas). La codificación se dividirá en cinco partes, comenzando con el desarrollo de la base de datos y su despliegue en un contenedor. A continuación, se abordará el desarrollo de la parte de Spring, centrándose en la creación de servicios REST utilizando TDD y patrones de software como el patrón estrategia. La tercera parte involucra el desarrollo del código de React, elegido por su capacidad para crear aplicaciones escalables mediante el uso de componentes y la implementación de SPA ( Single Page Application).
Para el sistema de adquisición de datos, se ha seleccionado un Arduino UNO. Inicialmente, se simularán los actuadores y sensores con LEDs y botones antes de sustituirlos por componentes correspondientes. Arduino se eligió por su facilidad de programación, precio asequible y amplia documentación disponible.Aunque al final se ha decidido usar una ESP32 porque se puede conectar directamente.
En la última etapa, se llevará a cabo la maquetación de la aplicación web de React utilizando Bootstrap CSS, un framework de maquetación CSS elegido por su novedoso enfoque.
Las pruebas, aunque representadas en el diagrama Gantt ( se muestra en la planificación), se realizarán de manera continua, las pruebas unitarias estarán presentes durante todo el proceso de Desarrollo.
# 5 Recursos
Se emplearán diversos medios para la implementación del proyecto, entre los cuales se destaca la plataforma Arduino, de cual se utilizará la siguiente guía: ARDUINO, Store Arduino. Arduino. *Arduino LLC*, 2015, vol. 372. ,para el desarrollo del código y su implementación en el dispositivo. Asimismo, se utilizará la plataforma Azure en conjunto con Docker y Jenkins para el despliegue del código, asegurando una integración continua eficiente. Para los cuales se utilizarán las siguientes referencias para construer el entorno:
CHAPPELL, David, et al. Introducing the windows azure platform. *David Chappell & Associates White Paper*, 2010.
DOCKER, Inc. Docker. *lınea\].\[Junio de 2017\]. Disponible en: https://www. docker. com/what-docker*, 2020.
MOUTSATSOS, Ioannis K., et al. Jenkins-CI, an open-source continuous integration system, as a scientific data and image-processing platform. *SLAS DISCOVERY: Advancing Life Sciences R&D*, 2017, vol. 22, no 3, p. 238-249.
En el ámbito del desarrollo de software, se recurrirá a IDEs como Visual Studio Code y IntelliJ para facilitar la creación del código. Se utilizará la última versión del JDK para el desarrollo del código Java y npm será la herramienta empleada para gestionar las dependencias y ejecutar scripts en el entorno de React.
# 6 Bibliografía
1. FEDOSEJEV, Artemij. *React. js essentials*. Packt Publishing Ltd, 2015.
2. Johnson, R., Hoeller, J., Donald, K., Sampaleanu, C., Harrop, R., Risberg, T., ... & Webb, P. ( 2004). The spring framework-reference documentation. Available*:* [*https://docs.spring.io/spring-framework/docs/3.2.17.RELEASE/spring-framework-reference/pdf/spring-framework-reference.pdf*]( https://docs.spring.io/spring-framework/docs/3.2.17.RELEASE/spring-framework-reference/pdf/spring-framework-reference.pdf)
3. ARDUINO, Store Arduino. Arduino. *Arduino LLC*, 2015, vol. 372.
4. CHAPPELL, David, et al. Introducing the windows azure platform. *David Chappell & Associates White Paper*, 2010.
5. DOCKER, Inc. Docker. *lınea\].\[Junio de 2017\]. Disponible en: https://www. docker. com/what-docker*, 2020.
6. MOUTSATSOS, Ioannis K., et al. Jenkins-CI, an open-source continuous integration system, as a scientific data and image-processing platform. *SLAS DISCOVERY: Advancing Life Sciences R&D*, 2017, vol. 22, no 3, p. 238-249.
7. ASADULLAH, Muhammad; RAZA, Ahsan. An overview of home automation systems. En *2016 2nd international conference on robotics and artificial intelligence ( ICRAI)*. IEEE, 2016. p. 27-31.
8. GUIJARRO-RODRÍGUEZ, Alfonso A., et al. Sistema de riego automatizado con Arduino. *Sistema*, 2018, vol. 39, no 37, p. 27.Available: https://revistaespacios.com/a18v39n37/a18v39n37p27.pdf
9. ROCHA, André, et al. INTEGRATION OF THE VACUUM SCADA WITH CERN’S ENTERPRISE ASSET MANAGEMENT SYSTEM. En *16th Int. Conf. on Accelerator and Large Experimental Control Systems ( ICALEPCS'17), Barcelona, Spain, 8-13 October 2017*. JACOW, Geneva, Switzerland, 2018. p. 490-494.
HERRERA, Jean; BARRIOS, Mauricio; PÉREZ, Saúl. Diseño e implementación de un sistema scada inalámbrico mediante la tecnología zigbee y arduino. *Prospectiva*, 2014, vol. 12, no 2, p. 65-72.
# 7 Planificación
En el apartado se mostrará la plafinicacion prevista con la duración en la que se ha estimado las diferentes tareas.
En cuanto a las fechas establecidas en el diagrama Gantt, se destaca que el proyecto no puede comenzar hasta su aprobación. La importancia de las fechas radica en la duración estimada de cada tarea. Para estimar los tiempos, se ha empleado una media ponderada con el tiempo optimista,más cuatro veces el tiempo realista más el tiempo pesimista, dividido entre 6. Este enfoque proporcionará una estimación más precisa de la duración de las tareas.
| Tarea | Tiempo Optimista | Tiempo Realista | Tiempo Pesimista | Tiempo Estimado |
|----------------------------------|------------------|-----------------|------------------|-----------------|
| Análisis Aplicación front | 1 | 2 | 3 | 2 |
| Análisis de aplicación de backen | 2 | 4 | 6 | 4 |
| Diseño Aplicación Backend | 2 | 3 | 5 | 3,166666667 |
| Diseño Aplicación Fronted | 1 | 2 | 4 | 2,166666667 |
| Configuración Azure | 1 | 2 | 4 | 2,166666667 |
| Configuración de Jenkins | 1 | 2 | 3 | 2 |
| Configuracion de docker | 1 | 1 | 2 | 1,166666667 |
| Desarrollo Base de Datos | 2 | 4 | 6 | 4 |
| Desarrollo Backen Spring | 10 | 17 | 21 | 16,5 |
| Desarrollo front React | 6 | 12 | 17 | 11,83333333 |
| Desarrollo codigo Arduino | 1 | 3 | 4 | 2,833333333 |
| Enmaquetación de La PaginaWeb | 1 | 3 | 7 | 3,333333333 |
| | | | | |
A continuación, se mostrará como quedan reflejadas la diferentes tareas en el diagrama Gantt: 
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/CarlosGarridoJuncoAnteproyecto/media/image2.png]]
Ilustración 2 Diagrama Gantt
