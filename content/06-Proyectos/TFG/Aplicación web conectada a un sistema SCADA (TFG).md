---
title: "Aplicación web conectada a un sistema SCADA (TFG)"
tags: [universidad, 4anyo, tfg]
date: 2026-08-12
lang: es
---
GRADO EN INGENIERÍA DE COMPUTADORES
**Trabajo Fin de Grado**
DESARROLLO DE UNA APLICACIÓN WEB CON TECNOLOGÍAS MODERNAS, CONECTADA A UN SISTEMA SCADA
**Autor:**
Carlos Garrido Junco
**Tutor:**
Salvador Otón Tortosa
2024
Universidad de Alcalá
Escuela Politécnica Superior
**UNIVERSIDAD DE ALCALÁ**
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image3.png]]**Escuela Politécnica Superior**
**Grado en Ingeniería Informática**
Trabajo Fin de Grado
<span class="smallcaps">Desarrollo de una aplicación web con tecnologías modernas, conectada a un sistema SCADA</span>
**Carlos Garrido Junco**
**Septiembre / 2024**
UNIVERSIDAD DE ALCALÁ
Escuela Politécnica Superior
<span class="smallcaps">Grado en Ingeniería Informática</span>
Trabajo Fin de Grado
<span class="smallcaps">DESARROLLO DE UNA APLICACIÓN WEB CON TECNOLOGÍAS MODERNAS, CONECTADA A UN SISTEMA SCADA</span>
**Autor: Carlos Garrido Junco**
**Tutor: Salvador Otón Tortosa**
Tribunal:
Presidente: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
Vocal 1º: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
Vocal 2º: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
FECHA: Septiembre / 2024
> Este trabajo se lo quiero dedicar a mis padres por el apoyo que me han dado a la hora de realizar este trabajo.
Índice Resumido
[Introducción [ix](#_Ref164860408)](#_Ref164860408)
[Objetivos del Proyecto [xii](#_Toc177296400)](#_Toc177296400)
[Presupuesto empleado [xiv](#_Toc177296403)](#_Toc177296403)
[Estado del arte [xvi](#_Toc177296404)](#_Toc177296404)
[Análisis de la aplicación [xxiv](#_Toc177296412)](#_Toc177296412)
[Diseño de la aplicación [xxix](#_Toc177296415)](#_Toc177296415)
[Desarrollo de la aplicación [xxxix](#_Toc177296421)](#_Toc177296421)
[Resultados [xciii](#_Toc177296460)](#_Toc177296460)
[Conclusión y mejoras [cvi](#_Toc177296465)](#_Toc177296465)
[Bibliografía [cviii](#_Toc177296469)](#_Toc177296469)
[Apéndice A. Enlaces [cxi](#_Toc177296470)](#_Toc177296470)
[Apéndice B. Glosario [cxiv](#_Toc157362734)](#_Toc157362734)
Índice Detallado
[Introducción [ix](#_Ref164860408)](#_Ref164860408)
[Objetivos del Proyecto [xii](#_Toc177296400)](#_Toc177296400)
[1.1.1. Introducción [xiii](#introducción)](#introducción)
[1.1.2. Objetivos específicos: [xiii](#objetivos-específicos)](#objetivos-específicos)
[Presupuesto empleado [xiv](#_Toc177296403)](#_Toc177296403)
[Estado del arte [xvi](#_Toc177296404)](#_Toc177296404)
[1.2. Introducción [xvii](#introducción-1)](#introducción-1)
[1.3. Arduino y ESP32 [xviii](#arduino-y-esp32)](#arduino-y-esp32)
[1.4. MySQL [xix](#mysql)](#mysql)
[1.5. Arquitectura Hexagonal y vertical Slicing [xx](#arquitectura-hexagonal-y-vertical-slicing)](#arquitectura-hexagonal-y-vertical-slicing)
[1.6. Backend Spring [xxi](#backend-spring)](#backend-spring)
[1.7. Front end React y Bootstrap [xxii](#front-end-react-y-bootstrap)](#front-end-react-y-bootstrap)
[1.8. Docker y Docker Hub [xxiii](#docker-y-docker-hub)](#docker-y-docker-hub)
[Análisis de la aplicación [xxiv](#_Toc177296412)](#_Toc177296412)
[1.9. Requisitos [xxv](#requisitos)](#requisitos)
[1.10. Diagrama de casos de usos [xxvii](#diagrama-de-casos-de-usos)](#diagrama-de-casos-de-usos)
[Diseño de la aplicación [xxix](#_Toc177296415)](#_Toc177296415)
[1.11. Diseño de la base de datos [xxxi](#diseño-de-la-base-de-datos)](#diseño-de-la-base-de-datos)
[1.12. Diagrama de clases [xxxii](#diagrama-de-clases)](#diagrama-de-clases)
[1.13. Modelo de interfaces de usuario [xxxiv](#modelo-de-interfaces-de-usuario)](#modelo-de-interfaces-de-usuario)
[1.14. Diagrama de implantación [xxxvi](#diagrama-de-implantación)](#diagrama-de-implantación)
[1.15. Diseño de la maceta. [xxxvii](#diseño-de-la-maceta.)](#diseño-de-la-maceta.)
[Desarrollo de la aplicación [xxxix](#_Toc177296421)](#_Toc177296421)
[1.16. Base de datos [xli](#base-de-datos)](#base-de-datos)
[1.16.1. Introducción [xli](#introducción-2)](#introducción-2)
[1.17. Back End [xlii](#back-end)](#back-end)
[1.17.1. Organización de las clases [xlii](#organización-de-las-clases)](#organización-de-las-clases)
[1.17.2. Patrones empleados [xliii](#patrones-empleados)](#patrones-empleados)
[1.17.2.1. DTO [xliii](#dto)](#dto)
[1.17.2.2. Inyección de dependencias [xliii](#inyección-de-dependencias)](#inyección-de-dependencias)
[1.17.2.3. State [xliii](#state)](#state)
[1.17.2.4. Observer o Publisher and subscribe [xlviii](#observer-o-publisher-and-subscribe)](#observer-o-publisher-and-subscribe)
[1.17.2.5. Mediador [lii](#mediador)](#mediador)
[1.18. Seguridad [lv](#seguridad)](#seguridad)
[1.18.1. JWT [lv](#jwt)](#jwt)
[1.18.2. SHA256 [lviii](#sha256)](#sha256)
[1.19. Front end [lx](#front-end)](#front-end)
[1.19.1. Estructura del proyecto [lx](#estructura-del-proyecto)](#estructura-del-proyecto)
[1.19.2. Maquetación con Bootstrap [lxix](#maquetación-con-bootstrap)](#maquetación-con-bootstrap)
[1.20. Despliegue usando Maven y Docker Compose. [lxxi](#despliegue-usando-maven-y-docker-compose.)](#despliegue-usando-maven-y-docker-compose.)
[1.20.1. Introducción [lxxi](#introducción-3)](#introducción-3)
[1.20.2. Base de datos [lxxi](#base-de-datos-1)](#base-de-datos-1)
[1.20.3. Back End [lxxii](#back-end-1)](#back-end-1)
[1.20.4. Front end [lxxiii](#front-end-1)](#front-end-1)
[1.20.5. Docker Compose [lxxiii](#docker-compose)](#docker-compose)
[1.21. Arduino Y Esp32 [lxxvi](#arduino-y-esp32-1)](#arduino-y-esp32-1)
[1.21.1. Componentes usados [lxxvi](#componentes-usados)](#componentes-usados)
[1.21.1.1. Temperatura [lxxvi](#temperatura)](#temperatura)
[1.21.1.2. Ultrasonidos [lxxvii](#ultrasonidos)](#ultrasonidos)
[1.21.1.3. Resistencia LDR [lxxviii](#resistencia-ldr)](#resistencia-ldr)
[1.21.1.4. Transistor NPN [lxxxi](#transistor-npn)](#transistor-npn)
[1.21.1.5. Humedad [lxxxii](#humedad)](#humedad)
[1.21.1.6. Código [lxxxii](#código-3)](#código-3)
[1.21.1.7. Bomba de agua [lxxxiii](#bomba-de-agua)](#bomba-de-agua)
[1.21.1.8. Pantalla LCD [lxxxiv](#pantalla-lcd)](#pantalla-lcd)
[1.21.2. ArduinoUNO [lxxxv](#arduinouno)](#arduinouno)
[1.21.2.1. Introducción [lxxxv](#introducción-10)](#introducción-10)
[1.21.2.2. Código para mandar los datos al servidor [lxxxvii](#código-para-mandar-los-datos-al-servidor)](#código-para-mandar-los-datos-al-servidor)
[1.21.3. ESP32 [lxxxviii](#esp32)](#esp32)
[1.21.3.1. Introducción [lxxxviii](#introducción-11)](#introducción-11)
[1.21.3.2. Código [lxxxviii](#código-6)](#código-6)
[Resultados [xciii](#_Toc177296460)](#_Toc177296460)
[1.22. Página Web [xciv](#página-web)](#página-web)
[1.22.1. Vistas de la aplicación [xciv](#vistas-de-la-aplicación)](#vistas-de-la-aplicación)
[1.23. Maceta [ci](#maceta)](#maceta)
[1.23.1. Vista de la Maceta [ci](#vista-de-la-maceta)](#vista-de-la-maceta)
[Conclusión y mejoras [cvi](#_Toc177296465)](#_Toc177296465)
[1.23.2. Uso de IA y cámara para detectar enfermedades [cvii](#uso-de-ia-y-cámara-para-detectar-enfermedades)](#uso-de-ia-y-cámara-para-detectar-enfermedades)
[1.23.3. Generador de codigo automático [cvii](#generador-de-codigo-automático)](#generador-de-codigo-automático)
[1.23.4. Conclusión [cvii](#conclusión)](#conclusión)
[Bibliografía [cviii](#_Toc177296469)](#_Toc177296469)
[Apéndice A. Enlaces [cxi](#_Toc177296470)](#_Toc177296470)
[Apéndice B. Glosario [cxiv](#_Toc157362734)](#_Toc157362734)
Índice de Figuras
[Figura 1 Arduino Figura 2 ESP32 [xviii](#_Toc177296359)](#_Toc177296359)
[Figura 3 Logo MySQL [xix](#_Toc177296360)](#_Toc177296360)
[Figura 4 Arquitectura Hexagonal Figura 5 Vertical Slicing [xx](#_Toc177296361)](#_Toc177296361)
[Figura 6 Módulos Spring [xxi](#_Toc177296362)](#_Toc177296362)
[Figura 7 Árbol de componentes React [xxii](#_Toc177296363)](#_Toc177296363)
[Figura 8 Logo de Docker [xxiii](#_Toc177296364)](#_Toc177296364)
[Figura 9 Diagrama Casos de uso Usuario [xxvii](#_Toc177296365)](#_Toc177296365)
[Figura 10 Diagrama de casos de uso administrador [xxviii](#_Toc177296366)](#_Toc177296366)
[Figura 11 Diseño de la base de datos. [xxxi](#_Toc177296367)](#_Toc177296367)
[Figura 12 Modelo de clases Back End [xxxii](#_Toc177296368)](#_Toc177296368)
[Figura 13 Árbol de componentes de React [xxxiii](#_Toc177296369)](#_Toc177296369)
[Figura 14 User Interface [xxxiv](#_Toc177296370)](#_Toc177296370)
[Figura 15 Diagrama de Implementación [xxxvi](#_Toc177296371)](#_Toc177296371)
[Figura 16 Vista Isométrica [xxxvii](#_Toc177296372)](#_Toc177296372)
[Figura 17 Ejemplo de script generado. [xli](#_Toc177296373)](#_Toc177296373)
[Figura 18 Estructura proyecto Back End [xlii](#_Toc177296374)](#_Toc177296374)
[Figura 19Bandeja de entrada de correos [liv](#_Toc177296375)](#_Toc177296375)
[Figura 20 Estructura proyecto en React [lx](#_Toc177296376)](#_Toc177296376)
[Figura 21 Árbol de directorio creación imagen base de datos [lxxii](#_Toc177296377)](#_Toc177296377)
[Figura 22 Docker Desktop resultado [lxxv](#_Toc177296378)](#_Toc177296378)
[Figura 23 Divisor de tensión fotorresistencia [lxxviii](#_Toc177296379)](#_Toc177296379)
[Figura 24Lux light Meter [lxxx](#_Toc177296380)](#_Toc177296380)
[Figura 25 login [xciv](#_Toc177296381)](#_Toc177296381)
[Figura 26 Menú principal [xciv](#_Toc177296382)](#_Toc177296382)
[Figura 27 Depósito de Agua Lista [xcv](#_Toc177296383)](#_Toc177296383)
[Figura 28 Huertos con numero de macetas [xcv](#_Toc177296384)](#_Toc177296384)
[Figura 29 Formulario de Huerto para añadir [xcvi](#_Toc177296385)](#_Toc177296385)
[Figura 30 Borrar Huerto [xcvi](#_Toc177296386)](#_Toc177296386)
[Figura 31 Lista de plantas con sus estados [xcvii](#_Toc177296387)](#_Toc177296387)
[Figura 32Formulario Añadir Planta [xcvii](#_Toc177296388)](#_Toc177296388)
[Figura 33 Formulario para borrar planta [xcviii](#_Toc177296389)](#_Toc177296389)
[Figura 34 Datos Personales [xcviii](#_Toc177296390)](#_Toc177296390)
[Figura 35Confirmación de baja [xcix](#_Toc177296391)](#_Toc177296391)
[Figura 36Lista de tipos de plantas [xcix](#_Toc177296392)](#_Toc177296392)
[Figura 37Lista de los sensores con las medidas obtenidas [c](#_Toc177296393)](#_Toc177296393)
[Figura 38 Vista desde arriba de la maceta [ci](#_Toc177296394)](#_Toc177296394)
[Figura 39 Sensor de Luz [cii](#_Toc177296395)](#_Toc177296395)
[Figura 40 Cantidad de Agua del deposito [ciii](#_Toc177296396)](#_Toc177296396)
[Figura 41 Nivel de humedad [civ](#_Toc177296397)](#_Toc177296397)
[Figura 42 Temperatura [cv](#_Toc177296398)](#_Toc177296398)
# <span id="_Ref164860408" class="anchor"></span>Introducción
Desde hace 10.000 años que comenzó la cosecha y recolección de alimentos, la agricultura ha sido la base de nuestras sociedades y en un mundo que cada vez, es más difícil cultivar debido al cambio climático y el auge de nuevas tecnologías que permite conectar sensores y actuadores a internet, abre una puerta a tener cultivos automatizados a nivel individual sin que estos suponga una gran carga de trabajo.
El presente Trabajo de Fin de Grado ( TFG) se sitúa en el ámbito de las tecnologías de desarrollo web modernas, con un enfoque particular en la combinación de React y Spring para la creación de una aplicación web innovadora. Aunque el proyecto incluye elementos de Internet de las Cosas ( IoT), se pondrá especial énfasis en la aplicación efectiva de estas tecnologías ( React y Spring) en un entorno práctico y en el despliegue en contenedores como Docker.
Este documento explorará la creación de un huerto con sensores de humedad, temperatura, luz y distancia, y actuadores como una bomba de agua. Dichos datos serán recolectados en un servidor programado en Java usando el framework Spring, y se mostrarán mediante una interfaz web hecha con React. En el documento también se explicará la creación de la maceta con los diferentes sensores y su depósito de agua.
**Palabras clave:** Spring, Java, React, JavaScript, Arduino UNO, ESP32 Wrover, C, C++, Node y Docker
Redes3# <span id="_Toc177296400" class="anchor"></span>Objetivos del Proyecto
## Introducción 
Esta aplicación estará enfocada en el cuidado de cultivos, analizando variables como la humedad, luminosidad y condiciones climáticas. En función de estos datos, se asignarán comportamientos específicos al sistema. Finalmente, el usuario podrá monitorear el estado de sus cultivos directamente desde la aplicación web hecha en Spring.
## Objetivos específicos:
- Desarrollar un sistema de adquisición de datos controlado por un back end Spring, que almacenará la información en una base de datos hecha en MySQL.
- Familiarización con la creación de aplicaciones web utilizando tecnologías modernas como React, Bootstrap y Spring.
- Manejo de datos y tomas de decisión en tiempo real.
- Estudio de desarrollo de aplicaciones SCADA.
- Familiarización con nuevas plataformas de desarrollo IoT vistas en la carrera como ESP32.
- Optimización de procesos como este caso el de la agricultura.
# <span id="_Toc177296403" class="anchor"></span>Presupuesto empleado
Para la creación de la maceta, se ha utilizado un recipiente de plástico grande con capacidad de 25 litros, al cual se le han hecho agujeros, para que pueda salir el agua. Este recipiente ha costado 12,99 euros. Además, se ha utilizado una pila de 9V que ha costado 5 euros, un táper pequeño de plástico que ha costado 2,25 euros, una bomba de agua con su sensor de humedad que ha costado 9,99 euros y un starter kit para una ESP32 valorado actualmente en 57,95 euros.
La tabla de costos es la siguiente:

| **Elementos** | **Costo en euros** |
|-------------------------------------|--------------------|
| Recipiente de plástico ( 25 litros) | 12,99 |
| Pila de 9V | 5,00 |
| Táper pequeño de plástico | 2,25 |
| Bomba de agua con sensor de humedad | 9,99 |
| Starter kit para ESP32 | 57,95 |
| Compo sana universal | 6,20 |
| Arlita 3 L | 3 |
| Manta térmica 1metro | 0,6 |
| Plantas ( Tomillo, Lavanda, Romero) | 5,10 |
| **Total:** | 103,8 |
# <span id="_Toc177296404" class="anchor"></span>Estado del arte
## Introducción
La unión de las tecnologías web y del internet de las cosas, han dado fruto a numerosos proyectos como puede ser algunos de los siguientes.
Automated irrigation system with Arduino: Un sistema en el cual se irriga cultivos utilizando la plataforma de Arduino, [( Guijarro-Rodríguez, 2018)](#gujarro)
Smart Home Automation Systems: proyecto que integran React con Spring para la automatización del hogar con los cuales se pueden controlar la climatización, iluminación y diferentes aparatos electrónicos, [( Asadullah, 2016)](#_Hlk159416839)
Integration of the vacuum scada with cern’s enterprise asset management system. Proyecto, para el cern el cual se ha integrado un Sistema SCADA con el framework de Spring para el control y la supervisión para el control de las cámaras de vacío del CERN. [( Rocha, 2018)](#rocha)
Implementación de un sistema SCADA, con un Arduino[: ( Herrera, 2014)](#herrera)
## Arduino y ESP32 
Los dos chips que se han utilizado: primero se trabajó con un Arduino y luego se cambió el proyecto por un ESP32 por los motivos que daré a continuación.
Por un lado, Arduino es la plataforma electrónica principal Open Source. Tiene la ventaja de que es capaz de leer fácilmente inputs de información. Dicha placa se ha utilizado en numerosos proyectos tanto en ámbitos estudiantiles como de profesionales y ha tenido mucho éxito llegando alcanzar en el 2011 en solo seis años desde su creación cifras de 300.000 unidades vendidas[. ( Introduction, 2017, August 29)](#ArduinoIntroduction), [( How many Arduinos are “in the wild?, 2011, May 15)](#manyArduinos)
Por el otro lado, el esp32 que es una familia de chips SOC ( System On Chip) de bajo coste, que cuenta con tecnologías de acceso a WiFi y Bluetooth. Lo cual le da una ventaja bastante significativa respeto a la plataforma de Arduino en términos de conectividad.
Al igual que Arduino se utiliza tanto en la industria como a nivel de proyectos individuales. Se pueden utilizar conjuntamente utilizando Arduino para captar los datos de los sensores y estos se mandan al esp32 a través de una conexión UART. El ESP32, a su vez, manda estos datos al servidor por WiFi o Bluetooth[. ( ESP32 Datasheet),](#esp32datasheet) [( ESP32 Overview)](#esp32Overvie).
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image5.jpeg]]
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image6.jpeg]]
<span id="_Toc177296359" class="anchor"></span>Figura Arduino Figura ESP32
## MySQL
MySQL es el más popular sistema de gestión de base de datos Open Source que hay actualmente, Basándose en un sistema de base de datos relacional en el cual los datos son almacenados en tablas y estas tablas pueden vincularse con otras a través de foreign keys[. ( MySQL?)](#whatirsMysq)
Se ha popularizado debido a su gran facilidad y su rápida puesta en marcha en sistemas. Se utiliza tanto para aplicaciones comerciales como para aplicaciones de entretenimiento.
Está disponible bajo una licencia GPL, pero también tiene una comercial, esto es debido a que el software que deriva de este y se quiere distribuir está obligado a publicar el código y a utilizar una licencia GPL.
[( MySQL, 2001)](#mysqlab)
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image7.png]]
<span id="_Toc177296360" class="anchor"></span>Figura Logo MySQL
## Arquitectura Hexagonal y vertical Slicing
En este punto se habla de tanto de la arquitectura hexagonal como del vertical Slicing porque se utilizan conjuntamente.
Por un lado, la arquitectura hexagonal estructura la aplicación principalmente en tres partes una parte más interna que sería el corazón de la aplicación que es el dominio en el cual va a estar el modelo de la aplicación escrito en clases y estas clases deben ser una representación de las entidades que forman la base de datos, la siguiente capa externa es la capa de servicios, esta capa contiene la lógica de negocio y utiliza la capa de dominio para ello. Por último, está la capa más externa que es la capa de controlador, esta capa maneja las conexiones fuera de la aplicación tanto para mostrar los datos a un usuario como para conectarse con la base de datos[. ( Cockburn, 2005, April 1)](#cockburn)
Cada capa Interna es agnóstica de su capa exterior, por ejemplo, el dominio no debe conocer ni de la capa de servicio ni del controlador. Y la del servicio solo conoce la capa de dominio, en cambio la del controlador conoce la capa de servicio. Esto con el motivo de aumentar la escalabilidad y el mantenimiento de la aplicación. También es conocida como arquitectura de puertos y adaptadores.
Por otro lado, el vertical Slicing se implementa conjuntamente con la arquitectura hexagonal, porque en lugar de estructurar el código en solo 3 capas, primero el código se divide según las entidades o el servicio que se requiere dar y luego dentro de este servicio se estructura usando la arquitectura hexagonal, esto permite facilitar el mantenimiento del código. [, ( Ratner, 2011)](#ratner)
![[image8.gif]]![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image9.png]]
<span id="_Toc177296361" class="anchor"></span>Figura Arquitectura Hexagonal Figura Vertical Slicing
## Backend Spring 
Spring Framework proporciona un modelo integral de programación y configuración para aplicaciones empresariales modernas basadas en Java, manejando la infraestructura para que los desarrolladores puedan enfocarse en la lógica de la aplicación. Entre sus ventajas destacan las siguientes:
- Permite ejecutar métodos de Java para transacciones de base de datos sin tener usar API de estas.
- Facilita la construcción de aplicaciones web mediante notaciones.
- Incluye un motor de inyección de dependencias lo cual permite desarrollar aplicaciones robustas y fáciles de mantener.
Spring está compuesto de los siguientes módulos que se puede observar en la siguiente imagen.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image10.jpeg]]
<span id="_Toc177296362" class="anchor"></span>Figura Módulos Spring
Utilizamos este entorno debido a las ventajas que incorporan como son la inyección de dependencias lo cual nos permite añadir la arquitectura hexagonal además de facilitarnos el acceso a las diferentes infraestructuras como api REST o API a la base de datos. [( Johnson, 2004)](#FEDOSEJEV)
## Front end React y Bootstrap
Para la parte de front end, he decidido escoger React y Bootstrap conjuntamente por los siguientes motivos:
Primero React, es una librería que ayuda a los desarrolladores a crear interfaces web como si fueran un árbol de componentes reutilizables. Estos componentes se pueden reutilizar para crear otras páginas web y se pueden importar componentes de terceros para crear nuestra página web. Además, React permite la creación de aplicaciones de una sola página ( SPA), donde los componentes se renderizan desde el lado del cliente sin tener que hacer peticiones HTTP GET al servidor para cargar nuevas vistas de la página web. [( What's new in React 19, 2024, May 12)](#whatnewinreact)
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image11.png]]
<span id="_Toc177296363" class="anchor"></span>Figura Árbol de componentes React
Por otro lado, Bootstrap es un producto de Open Source creado por trabajadores de Twitter, con la necesidad de crear un estándar de herramientas front end a lo largo de la empresa. Se lanzo en agosto del 2011 y ha ganado desde entonces una gran popularidad.
Bootstrap permite en maquetar aplicaciones de forma responsive y de una manera muy sencilla importando clases CSS, las cuales dan estilo a la aplicación sin que el desarrollador tenga que preocuparse por la maquetación[. ( Gaikwad, 2019)](#gaikwad)
Al desarrollar la aplicación en React y se utiliza el gestor de descargas de paquetes de Node el cual es npm que permite importar Bootstrap sencillamente.
## Docker y Docker Hub
Para facilitar la ejecución de la aplicación, se utilizado Docker y la creación de estas imágenes se han guardado en Docker hub.
Se ha escogido Docker porque permite de forma simplificada la creación, el desarrollo de aplicaciones en entornos virtuales. Con las dependencias que necesitan dichos programas, por lo tanto, si se ejecuta de manera local una imagen de nuestro proyecto en un contenedor podemos suponer que el futuro, si se despliega esa misma imagen en un contenedor de un servidor de terceros. La aplicación debería ejecutarse correctamente[. ( DOCKER, 2020)](#Docker)
Dicha imagen se tiene que guardar en un sitio que permita su compartición de forma fácil, por lo tanto, para dicho medio se utiliza Docker hub el cual es una página web parecida a Git Hub, pero en lugar de compartir código se comparte imágenes de contenedores[. ( Cook, 2017)](#cook)
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image12.png]]
<span id="_Toc177296364" class="anchor"></span>Figura Logo de Docker
# <span id="_Toc177296412" class="anchor"></span>Análisis de la aplicación
## Requisitos
En la siguiente tabla se muestra los requisitos que tienen que ser completados y los cuales se han completado.
| **Requisitos** | **Tipo** |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Se debe poder obtener datos del huerto como la temperatura, la humedad y el nivel de luz | Funcional |
| Se deberá poder ver los datos de una manera cómoda para el cliente | Funcional |
| El cliente puede observar el estado de las plantas | Funcional |
| El cliente puede observar desde la página web el estado del deposito | Funcional |
| Si el depósito de agua se quedará vacío el cliente recibiría una notificación | Funcional |
| El administrador debe poder ver el numero completo de personas registradas en la aplicación | Funcional |
| El administrador debe poder insertar, crear, actualizar usuarios en la aplicación | Funcional |
| El cliente o usuario pueden crear, actualizar y borrar plantas y huertos | Funcional |
| La maceta enseñará los datos de la maceta en una pantalla LCD a través una conexión i2c | No funcional |
| Se requiere de una base de datos relacional como MySQL | No funcional |
| Se requiere de una arquitectura en el proyecto que permita la pueda escalar fácilmente. | No funcional |
| Se requiere que la aplicación Back End y la base de datos este contenerizada para un mejor despliegue | No funcional |
| La cantidad de agua que haya en el depósito tendrá que ser medida | No funcional |
| Se requiere que el desarrollo de la aplicación sea hecho en Spring | No funcional |
| Se requiere que el front end sea desarrollado hecho en React para que se pueda reutilizar los componentes | No funcional |
| El huerto se podrá conectar vía wifi y podrá mandar los datos al servidor | Funcional |
| Existirá la otra modalidad de que se mande mediante una UART a un pc y este con un servidor hecho en Node recoja los datos y los mande al servidor | No funcional |
| El sensor de humedad solo se podrá activar cuando sea necesario la medición de este, en el caso de se dejará constantemente activado, la humedad con el flujo constante de electricidad oxidaría el sensor. | No funcional |
| La bomba de agua solo se activará cuando haya agua en el depósito y la humedad esté por debajo de los umbrales necesarios | Funcional |
| Cuando arranque el huerto este hará una consulta al servidor de la maceta en la que se encuentra y el servidor le proporcionará una media de la humedad mínima y máxima que las plantas necesitan. | No funcional |
| Se necesitará obtener a partir de la resistencia del termistor la temperatura en grados Celsius | No funcional |
| Se requiere obtener el valor de la luz en luxes a partir del valor de la fotorresistencia. | No funcional |
| Se requiere un planificador circular en la que tenga en cuenta el tiempo para mandar los datos al servidor cada minuto | No funcional |
| Se requiere crear una tabla que guarde el histórico con las cantidades medidas por tiempo | No funcional |
| La aplicación front diferenciará entre usuarios y administradores. | Funcional |
| Las llamadas HTTP utilizarán JWT | No funcional |
| Se requiere que las contraseñas se guarden utilizando sha256 por motivos de seguridad. | No funcional |
| Se requiere la creación de una biblioteca en la cual se guarde los diferentes tipos de planta, de la biblioteca se sacarán los datos necesarios para evaluar el estado de las plantas y la humedad que necesitan | Funcional |
| Se requiere que la aplicación pueda evaluar si las plantas están en buen estado dependiendo de factores, como la humedad, la luz y la temperatura. | Funcional |
## Diagrama de casos de usos
En el siguiente diagrama se muestra las acciones que pueden ejecutar los diferentes actores como son el usuario o el administrador. El administrador además puede hacer las acciones del usuario.
image13.emf
<span id="_Toc177296365" class="anchor"></span>Figura Diagrama Casos de uso Usuario
image14.emf
<span id="_Toc177296366" class="anchor"></span>Figura Diagrama de casos de uso administrador
# <span id="_Toc177296415" class="anchor"></span>Diseño de la aplicación
## Diseño de la base de datos
La base de datos se ha desarrollado en el motor de gestión de base de datos MySQL y para su diseño y desarrollo se ha utilizado la herramienta de MySQL Workbench, el diagrama de base de datos es el siguiente:
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image15.png]]
<span id="_Toc177296367" class="anchor"></span>Figura Diseño de la base de datos.
## Diagrama de clases
image16.emfEn la siguiente imagen se mostrará el diagrama de clases de la aplicación de la parte de Back End el cual sido hecha en Java usando Spring Boot:
<span id="_Toc177296368" class="anchor"></span>Figura Modelo de clases Back End
En la parte de Front End, hecho React se muestra a continuación el árbol de componentes.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image17.png]]
<span id="_Toc177296369" class="anchor"></span>Figura Árbol de componentes de React
## Modelo de interfaces de usuario
image18.emfEn este apartado se muestra el diagrama de interfaces de usuario. Dicho diseño se ha utilizado como modelo base para crear las diferentes vistas en React.
<span id="_Toc177296370" class="anchor"></span>Figura User Interface
Como se puede observar se creará vistas para cada entidad, además de la de login. Las vistas son las siguientes:
- Vista de Login: en ella el usuario iniciará sesión, y dependiendo si es administrador o usuario, le cargará unas vistas u otras.
- Vista de sensores: Dependiendo si es administrador o usuario, se muestra los datos que le proporcionan sus sensores que dispone el usuario, en cambio el administrador puede observar el estado de todos los sensores registrados en la aplicación, además en esta vista se incorpora la opción de poder dar de baja, añadir y modificar los sensores.
- Vista Maceta: En esta vista se proporcionará datos de las macetas, también dependiendo si es administrador o usuario, cambia, el usuario solo ve sus macetas, y que posición ocupan en el huerto. Además, cuenta con las funciones de añadir, borrar, ver y modificar.
- Vista Depósito de agua: El usuario puede ver el estado de su depósito y el porcentaje que está lleno, en cambio el administrador puede ver el estado de todos los depósitos. También, cuenta con las funciones de añadir, borrar, ver y modificar.
- Vista Plantas: Vista en la que se muestra las plantas que dispone el usuario y el estado de estas. El estado lo calcula a partir de los datos proporcionados por los sensores. El administrador puede ver todas las plantas registradas en la aplicación. También se puede añadir, borrar y modificar las plantas.
- Vista Biblioteca de plantas: En esta vista el usuario puede ver los tipos de plantas que están registrados en la aplicación y sus necesidades. El administrador además de esto podrá insertar, modificar y borrar tipos de plantas.
- Vista Datos personales, Para el administrador está vista es, la vista persona, en la cual se puede registrar personas, borrar, y modificar, solo el administrador puede añadir personas. Para el usuario esta vista solo muestra sus datos personales, como su nombre, correo su fecha de alta, también tiene la opción de darse de baja de la aplicación.
## Diagrama de implantación
En el siguiente diagrama se puede observar la implementación de la aplicación en un entorno real:
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image19.png]]
<span id="_Toc177296371" class="anchor"></span>Figura Diagrama de Implementación
Como se puede observar en el diagrama , puede haber dos modos de capturar los datos, en un principio se hizo un Arduino el cual no tenía módulo de wifi, ni tarjeta de red, por lo tanto los datos se le proporcionaba al servidor a través de un cable tipo UART que se conectaba a un portátil, también se podría haber utilizado una Raspberry pero para su desarrollo se utilizó un portátil en cual se ejecutaba un servidor escrito en Node que lee del puerto al que se conectaba el Arduino y transformaba esos datos en JSON para enviárselos al servidor. En el segundo modelo y el cual se decantó para el desarrollo de la maceta, se optó por utilizar una ESP32 la cual, si incluía un módulo de wifi, por lo tanto, manda directamente los JSON al servidor.
Por otro lado, como se puede observar tanto la base de datos, el Back End y el Front End están dentro de contenedores y comparten una red común de Docker, esto se ha hecho así para facilitar el despliegue de la aplicación.
## Diseño de la maceta.
Para el diseño de la maceta se ha utilizado Librecad un software de diseño Open Source. La maceta se compone, del depósito de agua, de la parte de electrónica y un tercer espacio con el tamaño suficiente para albergar dos plantas o tres.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image20.png]]
<span id="_Toc177296372" class="anchor"></span>Figura Vista Isométrica
La maceta es de tamaño de 30 de ancho, por 40 de largo y por 30 alto. Se separa en tres compartimentos el más grande es donde irán las plantas, el segundo de mayor tamaño es donde ira el depósito de agua y por último el más pequeño es donde va los sensores, el circuito y el ESP32 o Arduino.
En el recipiente de las plantas, se pondrá primero, una capa de arlita, es arcilla expandida que se utiliza en jardinería para evitar encharcamientos en la parte inferior de la maceta por exceso de riego, seguido a esta va una manta térmica de un metro cuadrado que sirve para separar el sustrato de la arlita, esta permite filtrar el agua. Con esta disposición nos aseguramos de que al sistema de drenaje no pasa la tierra solo pasa el agua. Por último, va la capa de sustrato con las plantas. A la hora de trasplantar una planta a nuestra maceta, si vemos que la parte inferior está llena de raíces que crecen de manera concéntrica porque la maceta anterior era pequeña para ellas, se cortara la capa más exterior de las raíces la que colinda con el fondo de la maceta, para que las nuevas raíces crezcan con dirección hacia el fondo de la nueva maceta, si no seguirían creciendo en círculos y les costaría más llegar al nuevo sustrato.
# <span id="_Toc177296421" class="anchor"></span>Desarrollo de la aplicación
## Base de datos
### Introducción 
Con el diseño anteriormente hecho en MySQL Workbench, desde la misma aplicación se puede generar un script que genera la base de datos, la base de datos estará dentro de un contenedor. Por lo tanto, solo generaremos el script desde la aplicación y no lo ejecutaremos sobre la base de datos.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image21.png]]
<span id="_Toc177296373" class="anchor"></span>Figura Ejemplo de script generado.
## Back End
### Organización de las clases
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image22.png]]
<span id="_Toc177296374" class="anchor"></span>Figura Estructura proyecto Back End
Como se puede observar en la imagen anterior, el proyecto se organiza siguiendo una arquitectura hexagonal con vertical Slicing. El vertical Slicing es por cada entidad de la base de datos, lo cual facilita el mantenimiento del código junto con la arquitectura hexagonal. En la arquitectura hexagonal separamos el proyecto por la capa de aplicación, dominio e infraestructura.
Y el proyecto sigue un enfoque de programación orientada a objetos sin caer en el antipatrón de functional decompositon ya que la aplicación no se enfocó en seguir una serie de paso para obtener un objetivo, este enfoque también se aplica a la parte de React, en cambio en la parte del Arduino o del ESP32 sí que se enfocó así porque el lenguaje que se utilizo es C y no es un lenguaje orientado a objetos aunque en este se han utilizado struct como sustitución de ellos como veremos más adelantes. Al seguir este enfoque conlleva a que lo primero que se desarrolla sean las entidades y la parte de acceso a la base de datos, y luego en la capa de aplicación creamos nuestros servicios que utilizan estas clases para conseguir los requisitos requeridos y por último esto servicios son expuestos a través de la capa del controlador como servicio web. Tanto el controlador como el acceso a la base de datos están dentro de la capa de infraestructura.
### Patrones empleados
#### DTO
Hemos utilizado el patrón “data transfer object ( DTO)”, para poder insertar atributos determinados para trabajar con ellos desde la capa de servicio como son el estado. Estos atributos no queremos que sean reflejados en la base de datos, ni en las entidades, por eso usamos DTO.
#### Inyección de dependencias
La ventaja de usar Spring es su motor de inyección de dependencias, facilitando el uso de la arquitectura hexagonal porque permite trabajar solo con las interfaces de las clases a utilizar y que sea el propio motor, durante la vida de la aplicación encargado de buscar y de instanciar las clases que se necesitan.
#### State
El patrón State lo hemos aplicado tanto con el depósito de agua, como para las plantas cuyos estados cambiarán dependiendo de los valores que les lleguen de los sensores.
Los estados están registrados en los DTO de cada uno.
Para el estado del depósito de agua, utiliza la siguiente interfaz:
```java
public interface Estado {
    public void ejecutar ( DepositoaguaDto t,Float medida);
    public boolean isAlerta ( DepositoaguaDto t,Float medida);
}
```
Tiene aparte un método que avisa si el depósito se está quedando sin agua, método que utilizaremos en el patrón Mediator para mandar correos al usuario para avisar que el depósito de agua no tiene agua.
Esta interfaz es implementada en la clase EstadoAgua la cual está definida como @componente para que pueda ser inyectada por Spring
```java
@Component
public class EstadoAgua implements Estado{
    Float porcentajeSinTruncar, profundidadDepo;
    public boolean isAlerta ( DepositoaguaDto t, Float medida) {
         this.profundidadDepo= t.getAlturaDeposito ();
        this.porcentajeSinTruncar= (( 1-( medida/profundidadDepo))*100);
        return porcentajeSinTruncar &lt; 25.0F;
    }
    @Override
    public void ejecutar ( DepositoaguaDto t, Float medida) {
        DecimalFormat df = new DecimalFormat ("#.00");
        this. profundidadDepo= t.getAlturaDeposito ();
         this.porcentajeSinTruncar= (( 1-( medida/profundidadDepo))*100);
        t.setEstado ( df.format ( porcentajeSinTruncar)+"% de agua");
    }
}
```
Ejecutar, recibe el DTO del depósito de agua y la medida que ha conseguido del sensor de distancia de ultrasonidos y con ello calcula la cantidad de agua que queda sabiendo la profundidad del depósito. Luego se registra en el DTO, utilizando un mapper lo transforma en la entidad que se guarda en la base de datos.
```
@Mapper ( unmappedTargetPolicy = ReportingPolicy.IGNORE, componentModel = MappingConstants.ComponentModel.SPRING)
public interface DepositoaguaMapper {
    DepositoaguaMapper mapper= Mappers.getMapper ( DepositoaguaMapper.class);
    DepositoAgua toEntity ( DepositoaguaDto depositoaguaDto);
    DepositoaguaDto toDto ( DepositoAgua depositoagua);
    @BeanMapping ( nullValuePropertyMappingStrategy = NullValuePropertyMappingStrategy.IGNORE)
    DepositoAgua partialUpdate ( DepositoaguaDto depositoaguaDto, @MappingTarget DepositoAgua depositoagua);
}
```
Para el estado de las plantas hemos primero creado la siguiente interfaz:
```java
public interface Estado {
    public void ejecutar ( PlantaDto t);
}
```
Esta interfaz solo tiene el método ejecutar que recibe como parámetro el método PlantaDTO, en este cambiaremos el estado. Se ha creado una clase por cada magnitud a medir que cambia el estado de la planta, se pondrá el estado feliz o triste dependiendo las cantidades mínimas o máximas que se obtienen de la tabla tipo de planta.
```java
@Component
public class EstadoCalor implements Estado{
    @Override
    public void ejecutar ( PlantaDto t) {
        Estado feliz = new EstadoFeliz ();
        Estado triste = new EstadoTriste ();
        Float nivelActual=t.getNivelActualTemperatura ();
        Float nivelMinimoRequerido=t.getNivelTemperaturaMIN ();
        Float nivelMaximoRequerido=t.getNivelTemperaturaMAX ();
        if ( nivelActual&gt;= nivelMinimoRequerido &amp;&amp; nivelActual &lt;= nivelMaximoRequerido) {
            t.setEstadoActual ( feliz);
        } else {
            t.setEstadoActual ( triste);
        }
    }
}
```
```java
@Component
public class EstadoHumedad implements Estado {
    @Override
    public void ejecutar ( PlantaDto t) {
        Estado feliz = new EstadoFeliz ();
        Estado triste = new EstadoTriste ();
        Float nivelActual=t.getNivelActualHumedad ();
        Float nivelMinimoRequerido=t.getNivelHumedadMIN ();
        Float nivelMaximoRequerido=t.getNivelHumedadMAX ();
        if ( nivelActual&gt;= nivelMinimoRequerido &amp;&amp; nivelActual &lt;= nivelMaximoRequerido) {
            t.setEstadoActual ( feliz);
        } else {
            t.setEstadoActual ( triste);
        }
    }
}
```
```java
@Component
public class EstadoLuz implements Estado{
    @Override
    public void ejecutar ( PlantaDto t) {
        Estado feliz = new EstadoFeliz ();
        Estado triste = new EstadoTriste ();
        Float nivelActual=t.getNivelActualLuminosidad ();
        Float nivelMinimoRequerido=t.getTipoplanta ().getNivelLuxNecesarioMinimo ();
        Float nivelMaximoRequerido=t.getTipoplanta ().getNivelLuxNecesarioMaximo ();
        if ( nivelActual&gt;= nivelMinimoRequerido &amp;&amp; nivelActual &lt;= nivelMaximoRequerido) {
            t.setEstadoActual ( feliz);
        } else {
            t.setEstadoActual ( triste);
        }
    }
}
```
Y por último los estados finales.
```java
@Component
public class EstadoFeliz implements Estado{
    @Override
    public void ejecutar ( PlantaDto t) {
        t.setEstado ( EstadoPlanta.FELIZ.toString ());
    }
}
```
```java
@Component
public class EstadoTriste implements Estado{
    @Override
    public void ejecutar ( PlantaDto t) {
        t.setEstado ( EstadoPlanta.TRISTE.toString ());
       }
}
```
Al igual que depósitodeaguadto, plantadto se carga en la base de datos utilizando mappers.
#### Observer o Publisher and subscribe 
El patrón Observe o Publisher and suscribe, se implementa de la siguiente manera, extendiendo de applicationEvent y utilizando la interfaz AplicationEventPublisher y el evento es escuchado a través de un EventListener, esta es la manera en la cual se implemente en Spring. Los observes observaran si se introducen un nuevo dato a través de los sensores para cambiar el estado de las plantas y del depósito. El código es el siguiente.
Para el depósito de agua:
```java
@Override
public boolean actualizarDepositoAgua ( SensorDto obj) {
    if ( dao.buscarPorID ( obj.getId ())!=null){
        sensorDepositoAguaPublisher.publish ( obj);
        dao.actualizar ( obj);
        return true;
    }
    return false;
}
```
Este método está dentro del service de sensor, cuando se ejecuta publica el evento pasando como argumento el objeto del sensor.
La clase que Publisher del depósito de agua es la siguiente:
```java
@Component
public class SensorDepositoAguaPublisher {
    private final ApplicationEventPublisher publisher;
    public SensorDepositoAguaPublisher ( ApplicationEventPublisher publisher) {
        this.publisher = publisher;
    }
    public void publish ( SensorDto sensor){
        System.out.println ("publicar sensor agua");
        publisher.publishEvent ( new SensorDepositoAguaAdapterObserver ( this,sensor));
    }
}
```
Y en la clase depositoAguaserviceImp implementamos la interfaz ApplicationListner
Que no os obliga a implementar el método que escucha el evento.
```java
public class DepositoAguaServiceImpl implements IDepositoAguaService, ApplicationListener&lt;SensorDepositoAguaAdapterObserver&gt; {
    .........
    .........
    @Override
    public void onApplicationEvent ( SensorDepositoAguaAdapterObserver event) {
        DepositoaguaDto depositoaguaDto;
        if ( dao.buscarPorIDSensor ( event.getSensorDto ().getId ()).getId () != null) {
            depositoaguaDto = dao.buscarPorIDSensor ( event.getSensorDto ().getId ());
            Estado estado = new EstadoAgua ();
            Float cantidadmedida = Float.parseFloat ( event.getSensorDto ().getCantidadMedida ());
            estado.ejecutar ( depositoaguaDto, cantidadmedida);
            dao.actualizar ( depositoaguaDto);
            if ( estado.isAlerta ( depositoaguaDto, cantidadmedida)){
                List&lt;HuertoHasUsuario&gt; huertosHasUsuarios = huertoHasUsuarioService.buscarPorIDHuerto ( depositoaguaDto.getHuertoIdhuerto ());
                for ( HuertoHasUsuario huertoHasUsuario:huertosHasUsuarios){
                    Integer idPersona=huertoHasUsuario.getId ().getUsuarioPersonaId ();
                    personaService.mandarEmail ( idPersona);
                }}}}}
```
Este método cambiará el estado del depósito de agua con los datos proporcionados por el sensor y también enviará un correo al usuario si el depósito de agua está vacío.
Para el cao de la planta es parecido en el servicio del sensor implementamos un Publisher en el actualizar y además utilizamos la clase fechahoraservice y la clase fechahorahassensorservice para tener un registro a lo largo del tiempo
```java
@Override
public boolean actualizar ( SensorDto obj) {
    Fechahora fechahora=fechahoraService.getTiempoActual ();
    if ( fechaHoraHasSensorService.isRegistrado ( fechahora,obj)){
        return false;
    }else{
        if ( dao.buscarPorID ( obj.getId ())!=null){
            sensorPublisher.publish ( obj);
            dao.actualizar ( obj);
            return true;
        }
        return false;
    }
}
```
El Publisher utiliza:
```java
@Component
public class SensorPublisher {
    private final ApplicationEventPublisher publisher;
    public SensorPublisher ( ApplicationEventPublisher publisher) {
        this.publisher = publisher;
    }
    public void publish ( SensorDto sensor){
        publisher.publishEvent ( new SensorAdapterObserver ( this,sensor));
    }
}
```
Y la clase plantaServiceImpl implementa el listener
```java
public class PlantaServiceImpl implements IPlantaService, ApplicationListener&lt;SensorAdapterObserver&gt; {
........
........
@Override
public void onApplicationEvent ( SensorAdapterObserver event) {
    int idSensor;
    idSensor = event.getSensorDto ().getId ();
    List&lt;MacetaHasSensor&gt; macetaHasSensor = macetaHasSensorDAO.buscarPorIDSensor ( idSensor);
    List&lt;Integer&gt; idMaceta, idPlanta;
    idMaceta = new ArrayList&lt;&gt;();
    String magnitudAMedir = event.getSensorDto ().getMagnitudAMedir ();
    String cantidad = event.getSensorDto ().getCantidadMedida ();
    Float cantidadFloat = Float.parseFloat ( cantidad);
    Estado estado = new EstadoFeliz ();
    for ( MacetaHasSensor macetasen : macetaHasSensor) {
        idMaceta.add ( macetasen.getMacetaIdmaceta ().getId ());
    }
    for ( Integer id : idMaceta) {
        List&lt;PlantaDto&gt; lista = plantaDAO.buscarPorMacetaID ( id);
        for ( PlantaDto plantaDto : lista
        ) {
            plantaDto= this.inicializarRangosMaxyMinimosMedidas ( plantaDto);
            if ("HUMEDAD".equalsIgnoreCase ( magnitudAMedir)) {
                plantaDto.setNivelActualHumedad ( cantidadFloat);
                plantaDAO.actualizarPlantaHumedad ( plantaDto);
                estado = new EstadoHumedad ();
            } else if (("TEMPERATURA".equalsIgnoreCase ( magnitudAMedir))) {
                plantaDto.setNivelActualTemperatura ( cantidadFloat);
                plantaDAO.actualizarPlantaTemperatura ( plantaDto);
                estado = new EstadoCalor ();
            } else if (("LUZ".equalsIgnoreCase ( magnitudAMedir))) {
                plantaDto.setNivelActualLuminosidad ( cantidadFloat);
                plantaDAO.actualizarPlantaLux ( plantaDto);
                estado = new EstadoLuz ();
            }
            estado.ejecutar ( plantaDto);
            plantaDto.resultado ();
            plantaDAO.actualizarPlantaEstado ( plantaDto);
        }
    }
}
}
```
Esta planta ejecuta además el state dependiendo del sensor correspondiente.
#### Mediador
Utilizamos este patron para mandar correos electrónicos entre la aplicación y los clientes dependiendo si el depósito de agua está vacío para ello hemos utilizado las siguientes clases.
```javascript
package es.uah.huertojpa.mensajería;
public interface IMediador {
    void enviarMensaje ( String correo,String asunto,String mensaje) throws Exception;
}
```
```javascript
@Component
public class Mediator implements IMediador {
    @Autowired
    private JavaMailSender mailSender;
    @Override
    public void enviarMensaje ( String correo, String asunto, String mensaje) throws Exception {
        SimpleMailMessage mailmensaje = new SimpleMailMessage ();
        mailmensaje.setTo ( correo);
        mailmensaje.setSubject ( asunto);
        mailmensaje.setText ( mensaje);
        mailmensaje.setFrom ("huertouah@gmail.com");
        mailSender.send ( mailmensaje);
    }
}
```
Que utiliza JavaMailSender para la cual hay que configurar previamente un correo electrónico que permita el acceso por aplicaciones. En nuestro caso hemos creado un correo para él, el cual utilizamos tanto para enviar como recibir correos.
Para poder mandar correos tenemos que configurar el application.properties
He insertado los siguientes valores:
```
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=huertouah@gmail.com
spring.mail.password=*****
spring.mail.protocol=smtp
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```
Como se puede comprobar en la siguiente captura el envió de correos funciona perfectamente:
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image23.png]]
<span id="_Toc177296375" class="anchor"></span>Figura Bandeja de entrada de correos
## Seguridad
### JWT
JWT son las siglas de JSON web token, las peticiones HTTP REST, llevan un token de tipo bearer, en las cabeceras dicho token es proporcionado por el login, en el Back End las peticiones antes de resolverlas se comprueba que lleven dicha autentificación. Dichos métodos de seguridad están dentro del paquete login y del paquete JWT y el paquete config.
Hay que definir una cadena de filtros de seguridad en la cual definiremos que rutas son validadas, además de desactivar el CSRF para que se puedan hacer peticiones desde servidores con otras IP. También en el sessionManager, crea una sesión que sea sin estado, ya que el servidor no va a guardar el estado de la sesión del usuario, esto será gestionado por el usuario.
```javascript
    @Bean
    public SecurityFilterChain securityFilterChain ( HttpSecurity http) throws Exception {
        return  http.csrf ( crsf-&gt;
                     crsf.disable ())
        .authorizeHttpRequests ( authRequest-&gt;
                     authRequest.requestMatchers ("/auth/**").permitAll ()
                             .anyRequest ().authenticated ()
             ).sessionManagement ( sesssionManager-&gt;
                     sesssionManager.sessionCreationPolicy ( SessionCreationPolicy.STATELESS))
                .authenticationProvider ( authProvider)
                .addFilterBefore ( jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class)
                .build ();
    }
```
El proceso de autentificación es el siguiente primero se pasa la petición por un filtro interno que hemos definido en el cual comprueba si tiene un token, si no lo tiene se retorna al filtro de seguridad anteriormente visto, si tiene token, se comprueba que este es válido y se permite hacer la consulta.
Al iniciar la aplicación en el login irá el token, de la siguiente manera:
```javascript
{
    "userName": "carlosg",
    "idUser": "3",
    "permisoAdmin": "0",
    "resultado": "Autentificiacion correcta",
    "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJjYXJsb3NnIiwiaWF0IjoxNzI1OTIwOTEyLCJleHAiOjE3MjU5MjIzNTJ9.Xlzp_jAidmcfAuN6I5-R4XayboLn01-LpPM5hDYQ6yI"
}
```
Luego desde la aplicación en React capturamos el token:
```javascript
  const onButtonClick = async () =&gt; {
    try {
      const msg = Login.fromJson ( formData);
      msg.password = await hash ( msg.password);
      const response = await postLog ( msg);
      const respuesta = LoginResp.fromJson ( response.data);
      setResp ( respuesta);
      localStorage.setItem ('authToken', respuesta.token);
      if (
        respuesta.idUser !== "-1" &amp;&amp;
        respuesta.permisoAdmin !== "-1"
      ) {
        const permisoAdmin = respuesta.permisoAdmin === "1";
        respuesta.permisoAdmin = permisoAdmin;
        onData ( respuesta);
        navigate ("/dashboard");
      } else {
        setFallo ( true); }
    } catch ( error) {
      console.error ("Error al iniciar sesión:", error);
      setFallo ( true);
    }
  };
```
El token es guardado utilizando localStorage, esto permite que pueda ser usado por componentes padres, hermanos o desde cualquier parte de la aplicación.
Para mandar las peticiones HTTP con el token utilizamos para ello Axios y creamos un interceptor de peticiones de http para que antes de ser mandadas se introduzca el token en la cabecera. Dicho interceptor va dentro del paquete security.
```javascript
import axios from 'axios';
const port='8080';
const ip='localhost';
const API_BASE_URL='http://'+ip+':'+port;
const api = axios.create ({
  baseURL: API_BASE_URL,
});
api.interceptors.request.use (
  ( config) =&gt; {
    const token = localStorage.getItem ('authToken');
    if ( token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  ( error) =&gt; {
    return Promise.reject ( error);
  }
);
export default api;
```
Luego en lugar de utilizar solamente Axios para hacer la petición utilizamos el módulo que acabamos de crear, en este caso se llama api como por ejemplo en la siguiente llamada:
```javascript
import api from '../../security/api';
const getAllPersonas = async () =&gt; {
    try {
        console.log ('getAllPersona');
        const response = await api.get ( apiRoutes.persona.getAll);
        return response;
    } catch ( error) {
        console.error ('Error al obtener los Personas', error);
        throw error;
    }
};
```
### SHA256
Las contraseñas son guardadas en la base de datos empleado el algoritmo de encriptación sha256 esto es con el motivo de sí robarán los datos de los usuarios, no se podría sacar las contraseñas en claro. En el login de la aplicación web también se manda de forma encriptada.
Desde el servidor Back End, el siguiente método viene especificado el servicio de persona.
Se obtiene la contraseña antes de que sea guardada en la base de datos, y se convierten en hash y luego se vuelve a guardar en el objeto persona sustituyendo a la anterior. Luego en el login solo compara si la contraseña ya pasada por el hash es igual hash que se le proporciona desde la aplicación web.
```javascript
public boolean guardarPersona ( Persona persona) {
    if ( personaDAO.buscarPorId ( persona.getId ())==null){
        String passSinHash =persona.getPasswordSHA256 ();
        String sha256hex = Hashing.sha256 ()
                .hashString ( passSinHash, StandardCharsets.UTF_8)
                .toString ();
        persona.setPasswordSHA256 ( sha256hex);
        personaDAO.guardarPersona ( persona);
        return true;
    }
    return false;
}
```
Para hacer el login desde apartado web, en la aplicación de React se convierte en hash la contraseña utilizando el siguiente método:
```javascript
const sha256=async ( message)=&gt; {
  const msgBuffer = new TextEncoder ().encode ( message);                    
  const hashBuffer = await crypto.subtle.digest ('SHA-256', msgBuffer);
  const hashArray = Array.from ( new Uint8Array ( hashBuffer));
  const hashHex = hashArray.map ( b =&gt; b.toString ( 16).padStart ( 2, '0')).join ('');
  return hashHex;
};
```
## Front end
### Estructura del proyecto
La estructura del proyecto es la siguiente, sigue una arquitectura hexagonal con vertical Slicing por cada entidad. La parte de aplicación contiene la lógica de la aplicación y es donde se encuentra los componentes, los cuales van a ser por cada entidad una lista con los elementos de esa entidad y un formulario por cada método de los siguiente: insertar, borrar y actualizar.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image24.png]]
<span id="_Toc177296376" class="anchor"></span>Figura Estructura proyecto en React
Las direcciones de llamadas las hemos centralizados en la clase apiRoutes.js para que sea más sencillo cambiar la dirección a la que apunta las peticiones REST, este contiene un array de objecto por el cual pueden recibir como parámetro los parámetros de URL para construirla como podemos comprobar en la siguiente parte del código de apir Routes.
```java
const port='8080';
const ip='localhost';
const API_BASE_URL='';
const API_BASE_URL_Login='http://'+ip+':'+port;
const apiRoutes={
    depositoAgua: {
        getAll: `${API_BASE_URL}/depositoagua`,
        getById: ( id) =&gt; `${API_BASE_URL}/depositoagua/${id}`,
        getByUserName: ( userName)=&gt;`${API_BASE_URL}/depositoagua/userName/${userName}`,
        getByIdOrchard: ( id) =&gt; `${API_BASE_URL}/depositoagua/huerto/${id}`,
        create: `${API_BASE_URL}/depositoagua`,
        update:  `${API_BASE_URL}/depositoagua`,
        delete: ( id) =&gt; `${API_BASE_URL}/depositoagua/${id}`
    },
………
………
    }
}
export default apiRoutes;
```
El fichero principal es el App.js que es el encargado de enrutar distinto los componentes dependiendo de la ruta, lo conseguimos con react-router-dom que dependiendo de la URL renderizara unos componentes u otros y para poder cambiar la URL utilizamos el componente Link el cual pulsando en dicho elemento cambia la URL.
Como se puede ver el siguiente fragmento de código del fichero que se muestra a continuación, el componente Dashboard, porque contiene el elemento Link que cambia la ruta dependiendo si se pincha en dicho elemento y se muestra un link u otro dependiendo si tiene permisos de administrador los cuales la aplicación las conoce mediante el login.
```java
import {
  BrowserRouter as Router,
  Routes, Route, Link
} from 'react-router-dom'
const Dashboard = ({perm ,userName}) =&gt; {
  const padding = {
    padding: 30
  }
  console.log ('renderiza');
  return (
    &lt;div  &gt;
      &lt;div className=' barraPrincipal p-3 mb-2 bg-success text-white'&gt;
        {perm ? &lt;Link style={padding} to="/DepositoAgua"&gt;Deposito Agua &lt;/Link&gt; : &lt;Link style={padding} to={`/DepositoAgua/${userName}`}&gt;Mi deposito de agua &lt;/Link&gt; }
        {perm ? &lt;Link style={padding} to="/Huerto"&gt;Huerto &lt;/Link&gt; : &lt;Link style={padding} to={`/Huerto/${userName}`}&gt;Mis huertos &lt;/Link&gt;}
        {perm ? &lt;Link style={padding} to="/Maceta"&gt;Maceta &lt;/Link&gt; : &lt;Link style={padding} to={`/Maceta/${userName}`}&gt;Mis macetas &lt;/Link&gt;}
        {perm ? &lt;Link style={padding} to="/Persona"&gt;Persona &lt;/Link&gt; : &lt;Link style={padding} to={`/Persona/${userName}`}&gt;Mis datos &lt;/Link&gt;}
        {perm ? &lt;Link style={padding} to="/Planta"&gt;Planta &lt;/Link&gt; : &lt;Link style={padding} to={`/Planta/${userName}`}&gt; Mis plantas &lt;/Link&gt;}
        {perm ? &lt;Link style={padding} to="/Sensor"&gt;Sensor &lt;/Link&gt; : &lt;Link style={padding} to={`/Sensor/${userName}`}&gt;Mis sensores &lt;/Link&gt; }
        {perm ?&lt;Link style={padding} to="/TipoPlanta"&gt;Biblioteca de Plantas&lt;/Link&gt;:&lt;Link style={padding} to={`/TipoPlanta/${userName}`}&gt;Biblioteca de Plantas&lt;/Link&gt;}
       
       &lt;Link style={padding} to="/"&gt;Salir &lt;/Link&gt;
      &lt;/div&gt;
    &lt;/div&gt; );}
```
El encargado de llamar a un componente u otro es el componente Router, también para poder llamar en lugar de un componente desde una ruta, utilizo un tercer componente llamado ComponentComb, el cual recibe como parámetro los dos componentes que quiero mostrar, más los parámetros que necesitan dichos componentes, como se puede ver en el siguiente fragmento de código:
```java
const ComponenteComb = ({ Componente1, Componente2, basePath, padding, userName }) =&gt; (
  &lt;div&gt;
    &lt;Componente1 basePath={basePath} padding={padding} /&gt;
    &lt;div className='container'&gt;
      &lt;Componente2 userName={userName}/&gt;
    &lt;/div&gt;
  &lt;/div&gt;
)
const App = () =&gt; {
  const [permiso, setPermiso] = useState ( false);
  const [userName,setUserName]=useState ('');
  const handleData = ( data) =&gt; {
    const datos = LoginResp.fromJson ( data);
    setPermiso ( datos.permisoAdmin);
    setUserName ( datos.userName);
  }
  const padding = {
    padding: 30
  }
  const [email, setEmail] = useState ('')
  return (&lt;div&gt;
    &lt;Router&gt;
      &lt;div&gt;
        &lt;Routes&gt;
          &lt;Route path="/" element={&lt;Home onData={handleData} /&gt;} /&gt;
          &lt;Route path="/dashboard" element={&lt;Dashboard perm={permiso} userName={userName} /&gt;} /&gt;
        &lt;/Routes&gt;
      &lt;/div&gt;
```
Por último, para crear los formularios de añadir, borrar y actualizar hemos utilizado schema los cual nos permiten generar formularios de forma rápida y validar la entrada de los datos. Los datos conseguidos se guardan objetos de las clases del dominio que pertenece. Por ejemplo, es el caso de planta tiene su clase Planta.js.
```javascript
// Planta.js
class Planta {
    constructor ( id, nombrePlanta, fechaPlantacion, estado, tipoplantaIdtipoplanta, macetaIdmaceta, nivelActualHumedad, nivelActualLuminosidad, nivelActualTemperatura) {
        this.id = id;
        this.nombrePlanta = nombrePlanta;
        this.fechaPlantacion = new Date ( fechaPlantacion[0], fechaPlantacion[1] - 1, fechaPlantacion[2]);
        this.estado = estado;
        this.tipoplantaIdtipoplanta = tipoplantaIdtipoplanta;
        this.macetaIdmaceta = macetaIdmaceta;
        this.nivelActualHumedad = nivelActualHumedad;
        this.nivelActualLuminosidad = nivelActualLuminosidad;
        this.nivelActualTemperatura = nivelActualTemperatura;
    }
    static fromJSON ( json) {
        return new Planta (
            json.id,
            json.nombrePlanta,
            json.fechaPlantacion,
            json.estado,
            json.tipoplantaIdtipoplanta,
            json.macetaIdmaceta,
            json.nivelActualHumedad,
            json.nivelActualLuminosidad,
            json.nivelActualTemperatura
        );
    }
}
export default Planta;
```
Luego el schema:
```javascript
export const plantaSchema = {
    title: 'Planta',
    type: 'object',
    required: [
        'id',
        'nombrePlanta',
        'fechaPlantacion',
        'estado',
        'tipoplantaIdtipoplanta',
        'macetaIdmaceta',
        'nivelActualHumedad',
        'nivelActualLuminosidad',
        'nivelActualTemperatura'
    ],
    properties: {
        id: {
            type: 'integer',
            title: 'ID',
            description: 'ID único de la planta'
        },
        nombrePlanta: {
            type: 'string',
            title: 'Nombre de la Planta',
            description: 'Nombre de la planta'
        },
        fechaPlantacion: {
            type: 'string',
            format: 'date',
            title: 'Fecha de Plantación',
            description: 'Fecha en que se plantó la planta'
        },
        estado: {
            type: 'string',
            title: 'Estado',
            description: 'Estado actual de la planta',
            enum: ['ALEGRE', 'TRISTE', '']
        },
        tipoplantaIdtipoplanta: {
            type: 'integer',
            title: 'ID del Tipo de Planta',
            description: 'ID del tipo de planta asociada'
        },
        macetaIdmaceta: {
            type: 'integer',
            title: 'ID de la Maceta',
            description: 'ID de la maceta donde está plantada la planta'
        },
        nivelActualHumedad: {
            type: 'number',
            title: 'Nivel Actual de Humedad',
            description: 'Nivel actual de humedad ( en porcentaje)'
        },
        nivelActualLuminosidad: {
            type: 'number',
            title: 'Nivel Actual de Luminosidad',
            description: 'Nivel actual de luminosidad ( en lux)'
        },
        nivelActualTemperatura: {
            type: 'number',
            title: 'Nivel Actual de Temperatura',
            description: 'Nivel actual de temperatura ( en grados Celsius)'
        }
    }
};
```
En la aplicación o en la parte de servicio Plantacomponent.js creamos los componentes utilizan dicha entidad.
Porque ejemplo plantaLista que nos proporciona una lista de todas las plantas
```javascript
export const PlantaLista = () =&gt; {
    const [plantas, setPlantas] = useState ([]);
    useEffect (() =&gt; {
        console.log ('useEffect');
        getAllPlantas ().then ( response =&gt; {
            console.log ( response.data);
            setPlantas ( response.data);
        });
    }, []);
    return (
        &lt;div&gt;
            &lt;h1&gt;Plantas&lt;/h1&gt;
            &lt;table class="table"&gt;
                &lt;thead&gt;
                    &lt;CabeceraPlanta /&gt;
                &lt;/thead&gt;
                &lt;tbody&gt;
                    {plantas.map ( json =&gt; (
                        &lt;PlantaComponente key={json.id} planta={Planta.fromJSON ( json)} /&gt;
                    ))}
                &lt;/tbody&gt;
            &lt;/table&gt;
        &lt;/div&gt;
    );
};
```
En el siguiente ejemplo vemos como se crea un formulario. Los datos introducidos en este se introducen en un objecto de la clase Planta y se envía utilizando los métodos creados en la infraestructura.
```javascript
import Form from '@rjsf/core';
import validator from '@rjsf/validator-ajv8'
export const CreateFormPlanta = () =&gt; {
  const [resultado, setResultado] = useState ( null);
  const mandarDatosPost = ( planta) =&gt; {
      createPlanta ( planta).then ( response =&gt; {
          const resultboolean = Boolean ( response.data);
          console.log ( resultboolean);
          setResultado ( resultboolean);
      });
  }
  const addPlanta = ({ formData }, e) =&gt; {
      e.preventDefault ();
      console.log ("Data submitted: ", formData);
      const planta = Planta.fromJSON ( formData);
      mandarDatosPost ( planta);
  }
  return (
      &lt;div&gt;
          &lt;h1&gt;Formulario Planta&lt;/h1&gt;
          &lt;Form
              schema={plantaSchema}
              validator={validator}
              onChange={log ('changed')}
              onSubmit={addPlanta}
              onError={log ('errors')}
          /&gt;
          {resultado === true &amp;&amp; &lt;div&gt;El formulario fue enviado con éxito.&lt;/div&gt;}
          {resultado === false &amp;&amp; &lt;div&gt;Hubo un problema al enviar el formulario.&lt;/div&gt;}
      &lt;/div&gt;
  );
};
```
El hecho de cómo se envía esta explicado en la parte de seguridad.
### Maquetación con Bootstrap 
Para maquetar el proyecto hemos usado Bootstrap porque permite que la aplicación sea responsive y facilita su maquetación. Los estilos son puestos como clases en el JSX, devuelto de los componentes, como por ejemplo en el caso de componente NavigationBar.
```javascript
const NavigationBar = ({ basePath, padding }) =&gt; {
  return (
    &lt;div className='barraPrincipal p-3 mb-2 bg-success text-white'&gt;
      &lt;Link style={padding} to={`${basePath}/list`}&gt;List&lt;/Link&gt;
      &lt;Link style={padding} to={`${basePath}/create`}&gt;Create&lt;/Link&gt;
      &lt;Link style={padding} to={`${basePath}/update`}&gt;Update&lt;/Link&gt;
      &lt;Link style={padding} to={`${basePath}/delete`}&gt;Delete&lt;/Link&gt;
      &lt;Link style={padding} to={`/Dashboard`}&gt;Dashboard&lt;/Link&gt;
    &lt;/div&gt;
  );
};
```
## Despliegue usando Maven y Docker Compose.
### Introducción 
En este apartado necesitamos tener Maven, Docker y aunque no es necesario tener Docker Desktop para ver si los contenedores se ejecutan correctamente, es aconsejable porque facilita el poder ver el estado de los contenedores. Este apartado se divide por las siguientes partes base de datos, back-end y front-end.
### Base de datos
Para base de datos primero exportamos la base de datos creada en MySQL Workbench. y la guardamos dentro de una carpeta llamada scripts, para cuando se ejecute la imagen, ejecute todo los scripts que hay en ella. También se ha guardado en ella, un script con los datos de base de datos para ahorrar tiempo y no tener que cargar los datos para poder hacer las pruebas.
Creamos el siguiente DockerFile:
```dockerfile
FROM mysql
COPY ./scripts/ /docker-entrypoint-initdb.d/
```
Y ejecutamos el siguiente script, el cual creará una imagen de la base de datos y la subirá al Dockerhub para que pueda ser compartida. Además, para probar que funciona ejecutamos un contenedor con la imagen.
```shell
docker build -t dbhuerto ./
docker tag dbhuerto carlosgjuah/huertodb:latest
docker push carlosgjuah/huertodb:tagname
docker run -d -p 3306:3306 --name dbHuerto -e MYSQL_ROOT_PASSWORD=**** -e MYSQL_DATABASE=demo carlosgjuah/huertodb:latest
```
Recuerda cambiar los asteriscos por la contraseña.
El árbol de directorios debería quedarnos de la siguiente manera.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image25.png]]
<span id="_Toc177296377" class="anchor"></span>Figura Árbol de directorio creación imagen base de datos
### Back End 
Primero necesitamos tener Maven instalado en nuestro pc, porque utilizaremos este para compilar el proyecto en un jar utilizando los siguientes comandos.
```shell
mvn clean
mvn compile
mvn package
```
Una vez compilado el proyecto en un jar, el cual se ha llevado por comodidad a otra carpeta y creamos el siguiente Dockerfile, que utiliza como base un JDK y copiamos el jar cargado anteriormente.
```
# Usar una imagen base de OpenJDK 21
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY huertojpa-0.0.1-SNAPSHOT.jar /app/huertojpa.jar
EXPOSE 8080
ENTRYPOINT ["Java", "-jar", "/app/huertojpa.jar"]
```
Ejecuto los siguientes scripts para crear la imagen.
```
docker build -t huertojpa ./
docker tag huertojpa carlosgjuah/huertojpa:latest
docker push carlosgjuah/huertojpa:latest
```
### Front end
Para crear la imagen de React creo un dockerfile dentro de la carpeta del proyecto de Huerto-tfg-front, tiene de imagen base a Node.
```
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
CMD ["npm", "start"]
```
A continuación, ejecutamos los siguientes scripts:
```
docker build -t huertofront ./
docker tag huertofront carlosgjuah/huertofront:latest
docker push carlosgjuah/huertofront:latest
```
### Docker Compose
Por último, con las imágenes que hemos creado las juntamos utilizando Docker compose, ya no solo por comodidad, sino porque la base de datos y el backend tienen que estar en la misma red para poder comunicarse llamada en este caso huertonet.
Nuestro fichero Docker compose es el siguiente.
```Dockerfile
version: '3.8'
services:
  huertodb:
    image: carlosgjuah/huertodb:latest
    container_name: db
    environment:
      MYSQL_ROOT_PASSWORD: ****
      MYSQL_DATABASE: huertodbdev
    ports:
      - "3306:3306"
    networks:
      - huertonet
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 30s
      timeout: 10s
      retries: 5
  huertojpa:
    image: carlosgjuah/huertojpa:latest
    container_name: jpa
    depends_on:
      huertodb:
        condition: service_healthy
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://huertodb:3306/huertodbdev?useSSL=false&amp;serverTimezone=Europe/Madrid&amp;allowPublicKeyRetrieval=true
      SPRING_DATASOURCE_USERNAME: ****
      SPRING_DATASOURCE_PASSWORD: ****
      SPRING_JPA_PROPERTIES_HIBERNATE_DIALECT: org.hibernate.dialect.MySQLDialect
    ports:
      - "8080:8080"
    networks:
      - huertonet
  huertofront:
    image: carlosgjuah/huertofront:latest
    container_name: front
    ports:
      - "3000:3000"
    networks:
      - huertonet
networks:
  huertonet:
    driver: bridge
```
Ejecutamos el siguiente script:
| docker compose -p mihuerto up |
|-------------------------------|
Y en Docker desktop podemos comprobar que se ha ejecutado correctamente:
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image26.png]]
<span id="_Toc177296378" class="anchor"></span>Figura Docker Desktop resultado
## Arduino Y Esp32
### Componentes usados
#### Temperatura
##### Introducción 
La temperatura la obtenemos de un termistor el cual es una resistencia variable a la temperatura, la resistencia de un termistor viene dado por la siguiente formula:
$$RT = R + e^{B*\left ( \frac{1}{T2} - \frac{1}{T1} \right)}$$
- Rt es la resistencia del termistor bajo la temperatura T2.
- R es la resistencia del termistor bajo la temperatura T1.
- B es valor que nos da el fabricante.
El fabricante en la documentación nos dice que T1=25 grados Celsius que en grados kelvin son 297 grados, B es 3950 y R es 10k que es la resistencia que utilizamos además del termistor para la creación del circuito.
La temperatura que queremos obtener es T2 despejamos la formula anterior utilizando las propiedades del logaritmo natural, nos da como resultado la siguiente expresión:
$$T2 = \frac{1}{\frac{1}{T1} + \frac{\ln\left ( \frac{Rt}{R} \right)}{B}}$$
##### Código 
El código sería el siguiente:
```
double conseguirTemperatura () {
  const float V_ref = 3.3;
  int adcValue = analogRead ( PIN_ANALOG_IN);                        
  double voltage = ( float)adcValue / 4095.0 * V_ref;              
  double Rt = 10 * voltage / ( 3.3 - voltage);                    
  double tempK = 1 / ( 1 / ( 273.15 + 25) + log ( Rt / 10) / 3950.0);  
  double tempC = tempK - 273.15;                                  
  return tempC;}
```
#### Ultrasonidos
##### Introducción
El sensor de ultrasonidos lo utilizaremos para calcular la cantidad de agua que hay en el depósito de agua. Debido a porque podemos calcular la distancia con este. El funcionamiento es el siguiente el sensor de ultrasonido tiene un disparador que manda una onda de ultrasonido por encima del umbral auditivo del ser humano y este es recibido por el hecho y con el tiempo que tarda entre desde que es mandado y es recibido y sabiendo que la velocidad del sonido es 340m/s podemos calcular la distancia al obstáculo que se encuentra.
El sensor solo funciona para distancias entre 2cm y 200cm. Funciona de la siguiente manera, activa el pin del disparador con un voltaje alto durante 10us para que se mande la onda. Después el sensor activa el pin echo con alto voltaje hasta que vuelva a recibir la onda de sonido manda, en el que vuelve a cero
##### Código 
El código es el siguiente:
```
long getSonar () {
  float timeOut = MAX_DISTANCE * 60;  
  const float soundVelocity = 340.0;
  unsigned long pingTime;
  float distance;
  digitalWrite ( trigPin, LOW);
  delayMicroseconds ( 2);
  digitalWrite ( trigPin, HIGH);
  delayMicroseconds ( 10);
  digitalWrite ( trigPin, LOW);
  pingTime = pulseIn ( echoPin, HIGH, timeOut);
  if ( pingTime == 0) {
    return -1;
  }
  distance = ( float)pingTime * soundVelocity / 2 / 10000.0;
  return distance;  
}
```
#### Resistencia LDR
##### Introducción 
Una fotorresistencia es básicamente una resistencia que reacciona a la luz. Es un componente que reduce su resistencia cuando recibe luz en su superficie sensible. La resistencia de una fotorresistencia cambia según la cantidad de luz que detecta. Gracias a esto, podemos usarla para medir la intensidad de la luz.
##### Obtención de parámetros de la foto resistencia
Podemos calcular la resistencia variable de la foto resistencia a partir de un divisor de voltaje como se muestra en la siguiente imagen donde el pin se encarga de medir el voltaje.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image27.png]]
<span id="_Toc177296379" class="anchor"></span>Figura Divisor de tensión fotorresistencia
En la siguiente formula se muestra que a partir del divisor del voltaje podemos deducir la resistencia de la fotorresistencia.
$$Vout = \frac{Vref*Rldr}{2Rldr + 10k} = > Rldr = \frac{10k}{(\frac{Vref}{Vout} - 1)}$$
Sabiendo el valor de la resistencia variables podemos deducir el valor en lux sabiendo que el lux y la resistencia variables se relacionan de la siguiente manera [( OPTOELECTRONICA)](#materiales):
$$Rldr = A{*L}^{- B}$$
- L es el valor en lux que queremos obtener.
- Rldr es la resistencia de la fotorresistencia.
- A y B son parámetros que desconocemos que son propios del fabricante.
Debido a que faltan tanto el parámetro A y B, linealizamos primero la expresión utilizando las propiedades de los logaritmos
$$Log ( Rldr) = Log ( A) + B*Log ( L)$$
- Log ( A) es nuestro origen de coordenadas.
- B es la pendiente.
Podemos obtener dichos datos haciendo una regresión lineal a partir de los puntos que podemos obtener de forma experimental. Para ello hemos utilizado la aplicación móvil Lux Light meter y hemos obtenido los datos de la resistencia de la fotorresistencia a través de la esp32.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image28.png]]
<span id="_Toc177296380" class="anchor"></span>Figura Lux light Meter
Al hacer la medición hemos obtenido la siguiente tabla. Además, dichos valores para la regresión tienen que estar de forma logarítmica.
| L | Log ( L)=x | Rldr | Log ( Rldr)=y |
|-----|----------|-------|-------------|
| 658 | 2.81 | 1464 | 3.165 |
| 386 | 2.58 | 3256 | 3.512 |
| 316 | 2.499 | 3618 | 3.55 |
| 55 | 1.74 | 11395 | 4.036 |
| 71 | 1.85 | 10112 | 4.004 |
| 33 | 1.55 | 26174 | 4.417 |
Al hacer la regresión lineal salen que los valores son los siguientes:
$$a = \frac{n\Sigma xy - \sum\gamma\sum y}{n\Sigma x^{2} - (\Sigma x)^{2}}$$
$$b = \frac{\Sigma y - a\sum x}{n}$$
$$El\ origen\ = 5.62 = Log ( A) = > \ A = 10^{5.62} = \ 423233$$
$$La\ pendiente = B = 0.84$$
Teniendo A y B, el sensor capta perfectamente los valores de la luz en unidades Luxes.
##### Código 
El código para obtener los Luxes sería el siguiente:
```
float conseguirLuz () {
    const float V_ref = 3.3;
    const float A = 423233;
    const float B = 0.84;
    const float R_fix = 10000.0;  
 
    int adcValue = analogRead ( PIN_ANALOGLUZ_IN);      
    float voltage = ( float)adcValue / 4095.0 * V_ref;  
    float R_ldr = R_fix / (( V_ref / voltage) - 1);    
    float L = pow (( R_ldr / A), -1 / B);                
    Serial.printf ("Resistencia: %.3f Voltaje: %.3f Adc: %3.f lux: %3.f \n", R_ldr, voltage, adcValue, L);
 
    return L;
  }
```
#### Transistor NPN
Es un dispositivo que controla la corriente. Se puede usar para amplificar señales débiles o también, como un interruptor, en nuestro proyecto será este el caso. Tiene tres pines: base ( b), colector ( c) y emisor ( e). Cuando pasa corriente entre "be", "ce" permite que pase una corriente mucho mayor ( lo que llamamos amplificación del transistor). En ese momento, el transistor está en modo de amplificación. Pero cuando la corriente entre "be" supera cierto nivel, "ce" ya no deja que la corriente siga aumentando, y el transistor pasa a estar en modo de saturación. Existen dos tipos de transistores: PNP y NPN.
En el proyecto utilizamos transistores NPN porqué se activan cuando reciben voltaje alto por base, en cambio los PNP es el caso contrario, cuando reciben un voltaje bajo se activa.
Los transistores los hemos utilizado para la bomba de agua que es un motor dc y para activar el sensor de humedad de suelo.
#### Humedad 
##### Introducción 
El funcionamiento del sensor de suelo o higrómetro es bastante se sencillo consiste en dos electrodos resistivos, que dependiendo de la humedad habrá menos o más resistencia porque se producirá un cortocircuito entre ellas debido al agua. También tiene un comparador que se conecta al Arduino o la ESP32, para leer el voltaje del sensor, de forma digital o de forma analógica. En nuestro caso lo utilizamos de forma analógica, porque de forma digital solo nos indica si está húmedo o no, y no podemos saber el porcentaje de cual húmedo está el suelo. Es desde el código que lo convertimos en forma digital. También utilizamos un transistor para activar el sensor solo cuando se vaya a medir la humedad, porque si el sensor se mantuviera siempre activo debido a la electricidad y la humedad que pasa por los dos terminales provocaría que se oxidase el sensor debido a la electrolisis, que haría que el oxígeno se separes del hidrogeno y este se juntase con el hierro formado hierro ferroso ( FeO). Al activarlo solo cuando se necesita la medida alargamos la vida del sensor.
##### Código 
El código del sensor de humedad es el siguiente:
```
float conseguirhumedad () {
  digitalWrite ( PIN_TRANSISTOR_HUMEDAD, LOW);
  delayMicroseconds ( 2);
  digitalWrite ( PIN_TRANSISTOR_HUMEDAD, HIGH);
  const float V_ref = 5;
  int adcValue = analogRead ( PIN_ANALOG_HUMEDAD_IN);  // Leer pin ADC
  float voltage = ( float)adcValue / 4095.0 * V_ref;  // Calcular voltaje
  float porcentaje = ( 1 - ( voltage / V_ref)) * 100;
  digitalWrite ( PIN_TRANSISTOR_HUMEDAD, LOW);
  return porcentaje;
}
```
#### 
#### Bomba de agua
##### Introducción 
Una bomba de agua es un motor eléctrico acoplado a un rodete que es el que proporciona, al girar, energía cinética a nuestro fluido.
La bomba de agua vence a la energía potencial de la gravedad, aumentado la presión y la energía cinética gracias a un impulsor.
En nuestro caso para activarla utilizamos otro transistor NPN, solo se activará en el caso que sea requerido el cual es cuando hay suficiente agua en el depósito y la humedad está por debajo de los umbrales mínimos.
##### Código 
```
void echarAgua ( float porcentajeAguaAguaRequeridad) {
  Serial.println ("Porcentaje");
  float distancia = getSonar ();
  porcentaje= 100 * ( 1 - ( distancia / profundidadMaceta));
  Serial.println ( porcentaje);
  if ( 10.0 &lt; porcentaje) {
    float porcentajeAgua = conseguirhumedad ();
    Serial.println ("Humedad");
    Serial.println ( porcentajeAgua);
    if ( porcentajeAgua &lt; porcentajeAguaAguaRequeridad|porcentajeAgua &lt; 10.0) {
      Serial.println ("activar");
      activarBombaAgua ();
      echarAgua ( porcentajeAguaAguaRequeridad);
    }
  }
}
void activarBombaAgua () {
  digitalWrite ( PIN_BOMBAAGUA_IN, HIGH);
  delay ( 4000);
  digitalWrite ( PIN_BOMBAAGUA_IN, LOW);
}
```
#### Pantalla LCD
##### Introducción 
La pantalla se comunica con el servidor utilizando una comunicación I2C ( Inter-Integrated Circuit) es un modo de comunicación serial de dos cables. Uno es para la transmisión de datos SDA y el otro es para comunicar SCL. Cada maquina conectada tiene una única dirección y puede transmitir y recibir información.
La pantalla LCD1602 puede mostrar 2 líneas de caracteres en 16 columnas puede mostrar símbolos y letras y códigos siguiendo los códigos ASCCI.
##### Código 
Este es el código que inicializa el sensor Led, Por defecto nuestra pantalla se encuentra en la dirección 0x3F.
```
# define SDA 13  
# define SCL 14  
LiquidCrystal_I2C lcd ( 0x3F, 16, 2);
void inicializarLCD () {
  Wire.begin ( SDA, SCL);
  lcd.init ();            
  lcd.backlight ();        
  lcd.setCursor ( 0, 0);    
  lcd.print ("Huerto: ");
}
```
### ArduinoUNO
#### Introducción 
En esta sección explicamos como se conecta el Arduino al servidor hecho en Spring.
Para ello hemos utilizado un servidor hecho en Node el cual lee del puerto del Arduino el cual está conectado y manda los mensajes al servidor.
```
const axios = require ('axios'); // Importar Axios
const { apiRoutes } = require ('./apiRoutes');
 const updateSensor = async ( sensor) =&gt; {
    try {
        const response = await axios.put ( apiRoutes.sensor.update,sensor);
        return response;
    } catch ( error) {
        console.error (`Error al actualizar el Sensor con id ${sensor.id}`, error);
        throw error;
    }
};
 const updateSensorDepositoAgua = async ( sensor) =&gt; {
    try {
        const response = await axios.put ( apiRoutes.sensor.updateSenDepAgua, sensor);
        return response;
    } catch ( error) {
        console.error (`Error al actualizar el Sensor con id ${sensor.id}`, error);
        throw error;
    }
};
module.exports = {
    updateSensor,
    updateSensorDepositoAgua
  };
```
Para que pueda leer los datos del Arduino se requiere que lea del puerto serie y para ello necesitamos importar la librería serialport y también el parser-realine para poder interpretar los datos.
El Arduino manda los datos por el puerto COM3 y a un baudrate de 9600. El código para leer los datos del Arduino son los siguientes, también, utilizamos una clase sensor que luego sus objectos son los que mandamos al servidor.
```
const portName = 'COM3';
const baudRate = 9600;
const serialPort = new SerialPort ({
    path: portName,
    baudRate: baudRate,
    autoOpen: false,
  })
  const parser = serialPort.pipe ( new ReadlineParser ());
serialPort.open (( err) =&gt; {
  if ( err) {
    return console.error ('Error abriendo el puerto:', err.message);
  }
  console.log ('Puerto serie abierto');
});
let arduinoData = '';
parser.on ('data', ( data) =&gt; {
  console.log ('Datos recibidos del Arduino:', data);
  arduinoData = JSON.parse ( data);
  const sensor = Sensor.fromJSON ( arduinoData);
  if ( sensor.nombreSensor==="Sensor de Distancia"){
    mandarDatosPutDepositoAgua ( arduinoData);
  }
  else{
   mandarDatosPut ( arduinoData);  
  }
});
```
#### Código para mandar los datos al servidor
Para mandar los datos utilizamos Axios, son dos peticiones una para actualizar el estado deposito del agua y la otra para actualizar el estado de cualquier otro sensor:
```
const mandarDatosPut = ( sensor) =&gt; {
  updateSensor ( sensor).then ( response =&gt; {
    const resultboolean = Boolean ( response.data);
    console.log ( resultboolean);
  });
}
const mandarDatosPutDepositoAgua = ( sensor) =&gt; {
  updateSensorDepositoAgua ( sensor).then ( response =&gt; {
    const resultboolean = Boolean ( response.data);
    console.log ( resultboolean);
<blockquote>
  });
</blockquote>
```
### ESP32 
#### Introducción 
En esta sección se muestra el código utilizado para el ESP32 este código también es compatible con el Arduino. En veremos cómo se conecta el esp32 al wifi y como es ciclo de vida de este y como se utiliza los timers para reducir el número de llamadas al servidor y que sea por cada minuto.
#### Código 
La función de inicio del código sería la siguiente
```
void setup () {
  Serial.begin ( 115200);
  if ( on_Wifi) {
    inicializarConexionWifi ();
  }
  inicializarBombaAgua ();  // Inicializa el pin de la bomba de agua
  inicializarUltrasonidos ();
  inicializarLCD ();
  inicializarSensorHumedad ();
  obtenerDatosMaceta ();
}
```
La función obtenerMaceta sirve para obtener el siguiente struct del servido backend que este le envié un JSON. Por el cual el backend sabiendo el tipo de plantas que hay en la maceta le dará una media de la humedad mínima y máxima que las plantas necesitan, esta medida se utilizará para activar luego la bomba de agua dependiendo de este valor, también dispone de un modo offline en el cual se activa si hay menos de un 10 por ciento de humedad.
```
struct Humedad {
  int idMaceta;
  float humedadMediaMinimaRequerida;
  float humedadMediaMaximaRequerida;
  int numeroPlantas;
  void fromJSON ( String jsonString) {
    StaticJsonDocument&lt;200&gt; doc;
    DeserializationError error = deserializeJson ( doc, jsonString);
    if (!error) {
      idMaceta = doc["idMaceta"];
      humedadMediaMinimaRequerida = doc["humedadMediaMinimaRequerida"];
      humedadMediaMaximaRequerida = doc["humedadMediaMaximaRequerida"];
      numeroPlantas = doc["numeroPlantas"];
    } else {
      Serial.println ("Failed to parse JSON");
    }
  }
};
```
El bucle principal es siguiente fragmento de código y utiliza una librería ”timer.h” que cuenta el tiempo desde que se le da a start. Entra en while del cual no sale hasta que haya pasado un minuto, en el cual solo muestra datos que recoge de los sensores, también dispone de un if el cual comprueba si la cantidad del agua es mayor al 10 por ciento, en el caso de que se cumpla está condición se puede ejecutar el método echarAgua ().
```
# include "Timer.h"
Timer timer;
void loop () {
  timer.start ();
  recogerDatos ();
  enviarDatos ();
  while ( timer.read () &lt; 60000) {
    Serial.println ( timer.read ());
    mostrarDatos ();
    recogerDatos ();
     porcentaje = 100 * ( 1 - ( sensorDistancia.cantidadMedida / profundidadMaceta));
    if ( 10.0 &lt;porcentaje) {
      Serial.println ("sensorDistancia.cantidadMedida");
      echarAgua ( humedad.humedadMediaMinimaRequerida);
    }
  }
```
Para enviar inicializar la conexión Wifi desde el esp32 es muy sencillo solo necesitamos la librería wifi y el SSID y la contraseña del Router. El método es el siguiente:
```
# include &lt;WiFi.h&gt;
# include &lt;HTTPClient.h&gt;
const bool on_Wifi = true;  //variable creada para activar y desactivar el envio de datos
const char *ssid_Router = "*****";                                      
const char *password_Router = "****";                                  
void inicializarConexionWifi () {
  delay ( 2000);
  Serial.println ("Setup start");
  WiFi.begin ( ssid_Router, password_Router);
  Serial.println ( String ("Connecting to ") + ssid_Router);
  while ( WiFi.status () != WL_CONNECTED) {
    delay ( 500);
    Serial.print (".");
  }
  Serial.println ("\nConnected, IP address: ");
  Serial.println ( WiFi.localIP ());
  Serial.println ("Setup End");
}
```
Para mandar datos al servicio de actualizar sensor utilizamos el siguiente método
```
void enviarSensorData ( String jsonData) {
  if ( on_Wifi) {//variable creada para activar y desactivar el envio de datos
    if ( WiFi.status () == WL_CONNECTED) {  
      HTTPClient http;
      http.begin ( serverURL);                              
      http.addHeader ("Content-Type", "application/json");  
      int httpResponseCode = http.PUT ( jsonData);  
      if ( httpResponseCode &gt; 0) {
        Serial.printf ("PUT se mando correctamente %d\n", httpResponseCode);
      } else {
        Serial.printf ("Fallo HTTP Response code: %d\n", httpResponseCode);
      }
      http.end ();  
    } else {
      Serial.println ("WiFi desconectado");
    }
  }
}
```
También hemos creado los siguientes struct que contienen un método que nos permite transformar esto en formato JSON para el envió.
```
struct Sensor {
  int id;
  String nombreSensor;
  String magnitudAMedir;
  float cantidadMedida;
  String unidades;
  String toJSON () {
    StaticJsonDocument&lt;200&gt; doc;
    doc["id"] = id;
    doc["nombreSensor"] = nombreSensor;
    doc["magnitudAMedir"] = magnitudAMedir;
    doc["cantidadMedida"] = cantidadMedida;
    doc["unidades"] = unidades;
    String output;
    serializeJson ( doc, output);
    return output;
  }
};
```
### 
<span id="_Toc177296460" class="anchor"></span>Resultados
## Página Web
### Vistas de la aplicación
En la siguiente sección se puede observar las diferentes vistas de la aplicación web.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image29.png]]
<span id="_Toc177296381" class="anchor"></span>Figura login
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image30.png]]
<span id="_Toc177296382" class="anchor"></span>Figura Menú principal
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image31.png]]
<span id="_Toc177296383" class="anchor"></span>Figura Depósito de Agua Lista
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image32.png]]
<span id="_Toc177296384" class="anchor"></span>Figura Huertos con numero de macetas
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image33.png]]
<span id="_Toc177296385" class="anchor"></span>Figura Formulario de Huerto para añadir
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image34.png]]
<span id="_Toc177296386" class="anchor"></span>Figura Borrar Huerto
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image35.png]]
<span id="_Toc177296387" class="anchor"></span>Figura Lista de plantas con sus estados
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image36.png]]
<span id="_Toc177296388" class="anchor"></span>Figura Formulario Añadir Planta
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image37.png]]
<span id="_Toc177296389" class="anchor"></span>Figura Formulario para borrar planta
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image38.png]]
<span id="_Toc177296390" class="anchor"></span>Figura Datos Personales
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image39.png]]
<span id="_Toc177296391" class="anchor"></span>Figura Confirmación de baja
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image40.png]]
<span id="_Toc177296392" class="anchor"></span>Figura Lista de tipos de plantas
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image41.png]]
<span id="_Toc177296393" class="anchor"></span>Figura Lista de los sensores con las medidas obtenidas
## Maceta
### Vista de la Maceta
En las siguientes imágenes se puede comprobar el resultado final de la maceta creada, así como un video demostrativo.
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image42.jpeg]]
<span id="_Toc177296394" class="anchor"></span>Figura Vista desde arriba de la maceta
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image43.jpeg]]
<span id="_Toc177296395" class="anchor"></span>Figura Sensor de Luz
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image44.jpeg]]
<span id="_Toc177296396" class="anchor"></span>Figura Cantidad de Agua del deposito
![[publico/ASIGNATURAS_GRADO_COMPU/TFG/_media/TFG_CarlosGarrido/media/image45.jpeg]]
<span id="_Toc177296397" class="anchor"></span>Figura Nivel de humedad
![[image46.jpeg]]
<span id="_Toc177296398" class="anchor"></span>Figura Temperatura
<span id="_Toc177296465" class="anchor"></span>Conclusión y mejoras
- 
### Uso de IA y cámara para detectar enfermedades
Una mejora sustancial sería incorporarle un cámara y mediante inteligencia artificial si tienen alguna enfermedad poder detectarla y poder tratarla y así podríamos saber más exactamente el estado de las plantas.
Ortega, B. R., Biswal, R. R., & Sánchez-Delacruz, E. ( 2019). Detección de enfermedades en el sector agrícola utilizando Inteligencia Artificial. *Res. Comput. Sci.*, *148*( 7), 419-427.
Beltrán Abreo, H. M. ( 2022). *Procesamiento de Imágenes Digitales para Detectar Enfermedades o Plagas en Plantaciones de Banano* ( Master's thesis).
### Generador de codigo automático
En el caso de que hubiera más personas utilizando la aplicación, una mejora importante sería crear un generador de código específico para cada esp32 de cada huerto, el cual el usuario podría descargar el código personalizado para su esp32 y conectarlo a internet. Porque, aunque fuera el mismo código hay datos que son individuales como es el id del huerto, y el SSID y la contraseña del router y cantidad de sensores.
### Conclusión
La creación de un huerto automático con sensores que guarda datos utilizando el framework spring, base de datos en MySQL y muestra los datos mediante una interfaz hecha en React y con Bootstrap. Tanto la base de datos como el Back End y Front End, están dentro de contenedores usando y comunicados con Docker compose.
Es un proyecto completo y variado por la cantidad de tecnologías que están implicadas en la creación de un sistema SCADA y tecnología moderna ampliamente requerida en el mundo laboral como son Docker, React y Spring.
Y personalmente es un trabajo que me ha gustado mucho poder desempeñar ya por la cantidad de conceptos que aprendido ya no solo a nivel de código y físicos si no a nivel de cómo cuidar las plantas.
<span id="_Toc177296469" class="anchor"></span>Bibliografía
- 
1. FEDOSEJEV, Artemij. React. js essentials. Packt Publishing Ltd, 2015.
2. <span id="FEDOSEJEV" class="anchor"></span>Johnson, R., Hoeller, J., Donald, K., Sampaleanu, C., Harrop, R., Risberg, T., ... & Webb, P. ( 2004). The spring framework-reference documentation. Available: <https://docs.spring.io/spring-framework/docs/3.2.17.RELEASE/spring-framework-reference/pdf/spring-framework-reference.pdf>
3. ARDUINO, Store Arduino. Arduino. Arduino LLC, 2015, vol. 372.
4. <span id="manyArduinos" class="anchor"></span>«How many Arduinos are “in the wild?” About 300,000». https://blog.adafruit.com ( en inglés). Adafruit Industries. 15 de mayo de 2011. Consultado el 20 de marzo de 2018.
5. <span id="ArduinoIntroduction" class="anchor"></span>Arduino - Introduction». www.arduino.cc ( en inglés). Archivado desde el original el 29 de agosto de 2017. Consultado el 22 de enero de 2018
6. "<span id="whatirsMysq" class="anchor"></span>What is MySQL?". MySQL 8.0 Reference Manual. Oracle Corporation. Retrieved 3 April 2020. The official way to pronounce "MySQL" is "My Ess Que Ell" ( not "my sequel"), but we do not mind if you pronounce it as "my sequel" or in some other localized way
7. <span id="mysqlab" class="anchor"></span>MySQL, A. B. ( 2001). MySQL.
8. «<span id="esp32datasheet" class="anchor"></span>ESP32 Datasheet». Espressif Systems. 6 de marzo de 2017. Consultado el 14 de marzo de 2017.
9. «<span id="esp32Overvie" class="anchor"></span>ESP32 Overview». Espressif Systems. Consultado el 1 de septiembre de 2016.
10. CHAPPELL, David, et al. Introducing the windows azure platform. David Chappell & Associates White Paper, 2010.
11. <span id="Docker" class="anchor"></span>DOCKER, Inc. Docker. lınea\].\[Junio de 2017\]. Disponible en: https://www. docker. com/what-docker, 2020.
12. <span id="cook" class="anchor"></span>Cook, J., & Cook, J. ( 2017). Docker hub. Docker for data science: building scalable and extensible data infrastructure around the Jupyter notebook server, 103-118.
13. <span id="_Hlk159416839" class="anchor"></span>ASADULLAH, Muhammad; RAZA, Ahsan. An overview of home automation systems. En 2016 2nd international conference on robotics and artificial intelligence ( ICRAI). IEEE, 2016. p. 27-31.
14. <span id="gujarro" class="anchor"></span>GUIJARRO-RODRÍGUEZ, Alfonso A., et al. Sistema de riego automatizado con Arduino. Sistema, 2018, vol. 39, no 37, p. 27.Available: <https://revistaespacios.com/a18v39n37/a18v39n37p27.pdf>
15. <span id="rocha" class="anchor"></span>ROCHA, André, et al. INTEGRATION OF THE VACUUM SCADA WITH CERN’S ENTERPRISE ASSET MANAGEMENT SYSTEM. En 16th Int. Conf. on Accelerator and Large Experimental Control Systems ( ICALEPCS'17), Barcelona, Spain, 8-13 October 2017. JACOW, Geneva, Switzerland, 2018. p. 490-494.
16. <span id="herrera" class="anchor"></span>HERRERA, Jean; BARRIOS, Mauricio; PÉREZ, Saúl. Diseño e implementación de un sistema scada inalámbrico mediante la tecnología zigbee y arduino. Prospectiva, 2014, vol. 12, no 2, p. 65-72.
17. <span id="cockburn" class="anchor"></span>Cockburn, Alistair ( 2005-04-01). ["Hexagonal architecture"]( https://alistair.cockburn.us/hexagonal-architecture/). alistair.cockburn.us. Retrieved 2020-11-18.
18. <span id="whatnewinreact" class="anchor"></span>What's new in React 19". Archived from the original on 2024-05-12. Retrieved 2024-05-12.
19. <span id="gaikwad" class="anchor"></span>Gaikwad, S. S., & Adkar, P. R. A. T. I. B. H. A. ( 2019). A review paper on bootstrap framework. IRE Journals, 2 ( 10), 349-351.
20. <span id="ratner" class="anchor"></span>Ratner, I. M., & Harvey, J. ( 2011, August). Vertical Slicing: Smaller is better. In 2011 Agile Conference ( pp. 240-245). IEEE
21. <span id="materiales" class="anchor"></span>Materiales eléctricos, ( pp 1-8),( 2024), https://catedras.facet.unt.edu.ar/me/wp-content/uploads/sites/62/2018/04/LDR.pdf
<span id="_Toc177296470" class="anchor"></span>Apéndice A. Enlaces
El objetivo de este apartado es mostrar los enlaces donde está el codigo y los enlaces de Docker hub para facilitar la prueba y el acceso al código, además de un enlace de un video demostrativo del proyecto.
- <https://github.com/carlosGJAlcala/GestionPlantasFront>
- <https://github.com/carlosGJAlcala/GestioPlantasBackend>
- <https://github.com/carlosGJAlcala/HuertoEsp32>
- <https://hub.docker.com/repository/docker/carlosgjuah/huertofront/general>
- <https://hub.docker.com/repository/docker/carlosgjuah/huertojpa/general>
- <https://hub.docker.com/repository/docker/carlosgjuah/huertodb/general>
- <https://github.com/carlosGJAlcala/NodeHuertoTfg>
Video demostrativo de la maceta:
- <https://www.youtube.com/watch?v=njfGcuCghKw>
<span id="_Toc157362734" class="anchor"></span>Apéndice B. Glosario
El objetivo de este glosario es facilitar el acceso a una definición de los principales términos que se mencionan a lo largo de este libro.
**A**
**Arduino UNO**. Una placa de desarrollo de electrónica la cual es muy popular para proyectos de electrónica y programación, especialmente en el ámbito educativo por su facilidad y bajo costo.
C
**C**. Lenguaje de programación muy eficiente y utilizado principalmente en sistemas de bajo nivel como sistemas operativos o controladores. Ofrece mucho control sobre el hardware.
**C++**. Una extensión de C que incluye características de programación orientada a objetos. Es ideal para proyectos grandes y más complejos, como videojuegos o sistemas embebidos.
**D**
**Docker**. Plataforma de virtualización ligera que permite empaquetar aplicaciones y sus dependencias en contenedores, facilitando su portabilidad y el despliegue en diferentes entornos.
**E**
**ESP32 Wrover**. Un microcontrolador con conectividad Wi-Fi y Bluetooth integrada. Es muy usado en proyectos de IoT ( Internet de las Cosas) debido a su buen rendimiento y precio accesible.
**J**
**Java**. Lenguaje de programación orientado a objetos, diseñado para ser multiplataforma gracias a la Máquina Virtual de Java ( JVM).
**JavaScript**. Lenguaje de programación usado principalmente en el desarrollo web para crear páginas dinámicas. Aunque comenzó siendo un lenguaje del lado del cliente, ahora también se usa en el lado del servidor con Node.js.
**L**
**LDR**. Resistencia que cambia su valor según la cantidad de luz que recibe. Se utiliza en aplicaciones como sensores de luz o sistemas automáticos de iluminación.
**N**
**Node**. Node.js es un entorno de ejecución que permite utilizar JavaScript en el servidor, facilitando la creación de aplicaciones web escalables y de alto rendimiento.
**R**
**React**. Biblioteca de JavaScript desarrollada por Facebook, utilizada para construir interfaces de usuario interactivas. Se centra en la creación de componentes reutilizables y en el manejo eficiente del estado de las aplicaciones web.
**Resistencia eléctrica**. Componente que limita el paso de corriente en un circuito. Se mide en ohmios y se usa tanto para controlar el flujo de corriente como para generar calor.
**S**
**Spring**. Framework de Java de código abierto que facilita la creación de aplicaciones empresariales. Simplifica la configuración y el desarrollo de aplicaciones escalables y robustas.
**U**
**Ultrasonido**. Sonido de alta frecuencia, inaudible para los humanos. Se usa en sensores para medir distancias mediante el rebote de las ondas sonoras en objetos.
Universidad de Alcalá
Escuela Politécnica Superior
> ![[image47.jpeg]]
