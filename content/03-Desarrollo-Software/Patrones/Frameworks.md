---
title: "Frameworks"
tags: [universidad, 4anyo, patrones]
date: 2026-08-12
lang: es
---
# Frameworks

Patrones Software: Introducción a los frameworks Web y de persistencia.

## Índice General

- Java EE
- JPA
- Frameworks Web
- Principios SOLID
- Microservicios
- Spring Framework

## Java EE

### Modelos de Desarrollo

- **Arquitectura Cliente/Servidor 3 capas**: Capa de presentación, Capa de lógica de negocio, Capa de datos, comunicadas a través de Internet.

*Diagrama de la diapositiva, con el texto interleaved carácter a carácter y no reconstruible con precisión: representa las tres capas (presentación, lógica de negocio, datos) conectadas a través de Internet.*

- **Arquitectura Cliente/Servidor N capas**: Capa de presentación, Capa de lógica de negocio, Capa de datos, con un Cliente accediendo a través de Internet a un Servidor Web y un Servidor de Aplicaciones que a su vez accede a los Datos.

*Diagrama de la diapositiva, con el texto interleaved carácter a carácter y no reconstruible con precisión: representa Cliente → Internet → Servidor Web / Servidor de Aplicaciones → Datos.*

- **Arquitectura Cliente/Servidor enterprise**: evolución de la arquitectura n capas. En la capa de lógica de negocio tenemos objetos de negocio (componentes de servidor) para compartir funcionalidad.

**Ventajas**: facilidad de desarrollo, escalabilidad, mantenibilidad, seguridad, tolerancia a fallos, integridad de datos, reutilización de código.

### Java EE (Jakarta EE)

JavaEE (Java Enterprise Edition), hoy conocida como Jakarta EE, es una arquitectura estándar que define el modelo de programación de aplicaciones en n capas. Pensada para implementar aplicaciones de tipo empresarial y aplicaciones basadas en la Web.

Esta tecnología soporta una gran variedad de tipos de aplicaciones, desde las de tipo Web de gran escala a las pequeñas de tipo cliente servidor.

Está basado en prácticas comunes y patrones de diseño que simplifican el desarrollo de aplicaciones empresariales separando los componentes que forman cada capa.

Cuando se realizan aplicaciones cliente/servidor el desarrollo se divide en un conjunto de capas, destacando principalmente las siguientes:

- **Capa de presentación**: Es aquella que le sirve al cliente para interactuar con la aplicación. En JEE se suelen utilizar Servlets o JSP para generarla o un framework web como JSF.
- **Capa de lógica de negocio**: En ella se implementan las principales funcionalidades de la aplicación. Dentro se encontrarían los EJB y los SW.
- **Capa de datos**: Encargada del almacenamiento y la gestión de los datos a través de un sistema gestor de bases de datos.

### MVC

Model-View-Controller (MVC): patrón que nos permite separar la lógica de control (qué cosas hay que hacer pero no cómo), la lógica de negocio (cómo se hacen las cosas) y la lógica de presentación (cómo interaccionar con el usuario).

Generalmente el uso del MVC es el siguiente:

- El **Controlador** gestiona el flujo de trabajo (workflow) de la aplicación. Es el encargado de redirigir o asignar a cada petición una operativa de negocio (caso de uso) y posee un "mapa" de correspondencias entre peticiones y respuestas para realizar su cometido.
- El **Modelo** o Sistema de Negocio encapsula las reglas de negocio. Sería la lógica de aplicación que responde a una petición.
- La **Vista** representa la interfaz de usuario. Una vez realizadas las operaciones necesarias para una petición el flujo vuelve al controlador y este devuelve los resultados a la vista correspondiente.

**Resumen**: el controlador recibe una orden y decide quién la lleva a cabo en el modelo. Una vez que el modelo (la lógica de negocio) termina sus operaciones devuelve el flujo al controlador y éste envía el resultado a la capa de presentación o vista.

*(la diapositiva "Aplicación del MVC en JEE" incluye una imagen no extraída como texto)*

## JPA

### ORM

El mapeo objeto-relacional, más conocido por su nombre en inglés, Object-Relational Mapping (o sus siglas O/RM, ORM, O/R Mapping), es una técnica de programación para convertir datos entre el sistema de tipos utilizado en un lenguaje de programación orientado a objetos y el utilizado en una base de datos relacional.

En la práctica esto crea una base de datos orientada a objetos virtual, sobre la base de datos relacional. Esto posibilita el uso de las características propias de la orientación a objetos (básicamente asociación, herencia y polimorfismo).

### Introducción a JPA

Antes de JPA, para gestionar una base de datos, se empleaba JDBC (usando métodos como "select", "insert", "update" y "delete").

Se delegan los servicios de persistencia a la Java Persistence API o JPA, la cual facilita el desarrollo de beans o POJOs para persistencia de datos.

El mapeo objeto-relacional (la relación entre entidades Java y tablas de la base de datos) se realiza mediante anotaciones en las propias clases de entidad.

Proporcionan independencia del proveedor de persistencia y del origen de datos, lo que permite desarrollar sistemas que acceden a bases de datos de cualquier proveedor (Oracle, PostgreSQL, MySQL, DB2, SQL Server...).

### Características de JPA

- Permite integrar fácilmente la capa de lógica de negocio con la capa de persistencia.
- El uso de anotaciones permite definir las relaciones existentes entre entidades como: OneToOne, OneToMany, ManyToOne y ManyToMany.
- JPA permite realizar el mapeo desde tablas de una base de datos existente creando las entidades necesarias y sus relaciones correspondientes.
- Requiere pocas líneas de código para realizar la implementación.
- Usa un EntityManager y un PersistenceContext para llevar a cabo las operaciones de inserción (persist), actualización (merge) y borrado (remove).
- Para las consultas se utiliza JPQL (Java Persistence Query Language), un lenguaje similar al SQL o el Criteria API.
- Las transacciones se pueden programar o realizar de forma automatizada.

JPA trabaja con anotaciones. Para mapear un bean (una clase Java) con una tabla de la base de datos tan solo tenemos que añadirle la anotación `@Entity`. La clase debe tener atributos y los métodos getters y setters y al menos un constructor. También debemos seleccionar uno de sus atributos como clave primaria con `@Id`.

Implementamos la interfaz `Serializable` para la persistencia. Sólo con esto, ya tendríamos creada una "entidad" y podríamos insertar, actualizar o eliminar entradas en una tabla.

Cuando tenemos relaciones con otras clases también definimos sus cardinalidades: `@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`. Estas relaciones se traducen en un nuevo atributo que representa la asociación entre las clases.

## Frameworks Web

### ¿Qué son los Frameworks Web?

El concepto framework se emplea en muchos ámbitos del desarrollo de sistemas software, no sólo en el ámbito de aplicaciones web.

De forma específica, podemos definirlo como un conjunto de componentes (por ejemplo, clases en Java y descriptores y archivos de configuración en XML) que componen un diseño reutilizable que facilita y agiliza el desarrollo de sistemas Web.

### Objetivos y Frameworks Web Más Utilizados

**Objetivos de los Frameworks Web**:

- Acelerar el proceso de desarrollo.
- Reutilizar código ya existente.
- Promover buenas prácticas de desarrollo, como el uso de patrones.

**Frameworks Web más utilizados**:

- Spring Framework (conocido simplemente como Spring).
- JavaServer Faces (JSF).
- Struts.

### Servicios REST

Transferencia de Estado Representacional (REST) es un estilo arquitectónico de software para diseñar sistemas distribuidos que forma parte de la arquitectura cliente servidor, definiendo una manera de comunicación y el intercambio de datos entre componentes y sistemas web. Definido por Roy Fielding en el año 2000.

REST es un estándar para el intercambio de datos a través de la Web en aras de la interoperabilidad entre sistemas informáticos. Los servicios web que se ajustan al estilo arquitectónico REST se denominan servicios web RESTful, los cuales permiten a los sistemas solicitantes acceder y manipular los datos utilizando un conjunto uniforme y predefinido de operaciones.

Los servicios REST son actualmente la forma más utilizada para que las aplicaciones se comuniquen entre sí y dentro de un sistema, son definidos como recursos web que poseen un identificador (URI) para ser accedidos. Esto es posible gracias a que estos servicios utilizan HTTP y HTTPS como protocolos de comunicación por defecto.

Al utilizar HTTP como protocolo de comunicación los servicios REST no poseen estado, lo que aumenta la escalabilidad ya que el servidor no tiene que mantener, actualizar o comunicar el estado de la sesión.

| Operación | Descripción |
| --- | --- |
| GET | Se utiliza para obtener los recursos solicitados. |
| POST | Se utiliza para crear recursos con los datos enviados en el cuerpo de la llamada. |
| PUT | Se utiliza para actualizar los datos. |
| DELETE | Se utiliza para eliminar un recurso. |

## Principios SOLID

Acrónimo conformado por un conjunto de principios utilizados en la programación orientada a objetos que buscan que los desarrolladores escriban el código del sistema con gran calidad, con bajo acoplamiento, que se entienda por otros miembros del equipo y que pueda ser mantenido sin dificultad.

**Ventajas**:

- Mayor cohesión entre el código creado para realizar una funcionalidad. Mientras más alta sea la cohesión, más sencilla será la depuración y mantenimiento.
- Reutilización de las funcionalidades creadas sin la necesidad de ajustarla a cada bloque o módulo dentro de un sistema.
- Mayor robustez, permitiendo un manejo de errores, fallos y excepciones sencillo y eficiente.

### Single Responsibility Principle

Este principio establece que las clases, componentes o servicios creados por los desarrolladores deben tener una responsabilidad única sin importar lo simple o compleja que sea esa responsabilidad. Aplicación del divide y vencerás.

### Open-Close Principle

Establece que un módulo, clase o función debe abrirse para extensiones, pero cerrarse para modificaciones. Es decir, cuando las funcionalidades necesitan cambiar, esos cambios no deberían afectar la implementación existente, sino que debe existir la manera en que se pueda extender desde ella para añadir la actualización.

### Liskov Substitution Principle

Hace referencia específicamente a la herencia y al polimorfismo estableciendo que las instancias de las clases padres puedan reemplazar a las clases hijas sin afectar el funcionamiento de cualquier sistema que aplique la herencia entre clases.

### Interface Segregation

Las interfaces deben ser simples, pequeñas y cumplir con una única responsabilidad. Si existen clases hijas que implementen una interface y éstas no utilizan o implementen todos los métodos que posea dicha interface, la interfaz se debe segregar a través de la separación de las funcionalidades definidas, siendo colocada en otra interfaz que satisfaga todos los métodos de las clases que la implementen.

### Dependency Inversion

Establece que:

- Las clases de alto nivel no deberían depender de las clases de bajo nivel. Ambos deberían depender de abstracciones.
- Las abstracciones no deberían depender de los detalles. Los detalles deben depender de las abstracciones.

La aplicación de estos enunciados hace que sea posible mantener los módulos del sistema desacoplados, evitando la estrecha dependencia que comúnmente se produce al enlazar varios componentes, sobre todo entre los módulos de alto (clase abstracta o interfaz) y los de bajo nivel (implementación concreta de dicha interfaz o clase abstracta).

Este principio tiene como objetivo que el código desarrollado no dependa directamente de las clases de bajo nivel, sino que la dependencia se realice a las clases abstractas e interfaces.

## Microservicios

Componente de software que posee funcionalidades específicas para realizar operaciones y cumplir con la lógica de negocios que componen una plataforma web empresarial.

Debido a la dificultad de mantenimiento de los sistemas monolíticos surgió la arquitectura orientada al servicio (SOA), la cual planteaba descomponer ciertas partes de los sistemas en servicios bien definidos para reducir su tamaño y que estos establecieran comunicación entre sí.

La arquitectura orientada a microservicios es planteada como una evolución de la arquitectura SOA. La diferencia más importante entre SOA y microservicios es el nivel al que apunta la arquitectura: SOA para un sistema empresarial y los microservicios para un sistema individual a nivel de proyecto.

**Ventajas**: desacoplamiento, reducción de coste de cambio, diversidad de tecnologías, reutilización, tolerancia a fallos y escalabilidad.

Los microservicios constituyen un enfoque arquitectónico y organizativo en el desarrollo software donde las aplicaciones se basan en la creación de pequeños servicios independientes que se comunican a través de APIs bien delimitadas.

Nos permiten desarrollar aplicaciones con módulos físicamente separados, incluso pueden escribirse en distintos lenguajes de programación y con conexión a distintos tipos de bases de datos. La idea es que cada uno de ellos implemente una funcionalidad única y su despliegue sea de manera individual.

Amazon, Netflix y eBay son ejemplos de aplicación exitosa de esta arquitectura.

## Spring Framework

Es un robusto Framework para el Desarrollo de Aplicaciones Empresariales en el lenguaje Java.

Uso de la inyección de dependencia y el contenedor de inversión de control; haciendo frente al conocido modelo EJB.

**Características**:

- Sencillo y excelente manejo de las transacciones de bases de datos.
- Integración con otros Frameworks Java, como es JPA, Hibernate ORM, Struts, JSF.
- Framework web MVC para crear aplicaciones web.
- Soporte para el almacenamiento de datos NoSQL, procesamiento en lote y big data.

Filosofía "convención sobre configuración": se reducen al mínimo los pasos que un desarrollador debe dar para configurar inicialmente el proyecto.

### Spring Boot

Es un sub-proyecto de Spring Framework que busca facilitarnos la creación de proyectos con Spring Framework eliminando la necesidad de crear largos archivos de configuración XML.

Posee un conjunto de bibliotecas llamadas starters que contienen una colección de todas las dependencias relevantes preconfiguradas que se necesitan para iniciar una funcionalidad particular.

- Implementa el principio de diseño de Abierto-Cerrado.
- Posee servidores de aplicaciones y contenedores de Servlet embebido.
- Elimina configurar la aplicación mediante código o XML: Ficheros `.properties` o `.yml`.
- Crear aplicaciones basadas en microservicios.
- Ofrece un amplio soporte a diferentes tecnologías.

#### Inversión de Control

Principio de diseño de la ingeniería de software: el control de los objetos de una aplicación se transfiere a un contenedor encargado de suplir la instancia que necesita el sistema para funcionar.

El contenedor Spring IoC tiene la responsabilidad de conectar los objetos definidos en el Framework para construir una aplicación y lo hace leyendo una configuración proporcionada por el desarrollador.

#### Inyección de Dependencias

Patrón de diseño OO que busca reducir notablemente el acoplamiento entre las estructuras del sistema, donde se establece que las instancias de los objetos son suministradas por otro componente o contenedor sin que la clase tenga que establecer una dependencia directa con ese objeto.

Para la implementación de este patrón es recomendable utilizar interfaces para definir el comportamiento que debe tener la clase concreta y abstraer la relación entre dicha clase concreta y el objeto que la requiere, logrando de esta manera, el desacoplamiento entre clases y las bases para una programación orientada a interfaces.

#### Persistencia de Datos con Spring Boot

- **Spring Data JPA**: Es un módulo de Spring Data para la gestión de acceso a datos que requieren las aplicaciones web de una manera sencilla, basada en las tecnologías y estructuras utilizadas por Spring. Crea una capa de abstracción al API de persistencia de Java (JPA), mejorando en gran medida los procesos utilizados para ejecutar consultas, manipular datos, realizar auditoría y reduciendo la cantidad de código repetitivo.

Utiliza dos patrones de diseño de persistencia:

- **Patrón Repositorio**: Un repositorio crea la ilusión de una colección en memoria de todos los objetos del tipo que maneja. Configura el acceso a través de una interfaz global, proporciona métodos para agregar y eliminar objetos y proporciona métodos que seleccionan objetos basados en algún criterio.
- **Patrón DAO**: Patrón estructural que establece que se debe utilizar un Objeto de Acceso a Datos para abstraer y encapsular el acceso a los datos. Este objeto gestiona la conexión con la base de datos para obtener y guardar los datos. De esta manera, los componentes de una aplicación se mantienen aislados de la capa de persistencia.

#### Spring MVC

Spring MVC utiliza una arquitectura de aplicaciones siguiendo el patrón de diseño MVC (Model View Controller). Es un framework web basado en Servlets que viene incluido en Spring Framework (spring-webmvc). Spring MVC está diseñado siguiendo el patrón de diseño de Front Controller.

En Spring MVC el Front Controller es conocido como `DispatcherServlet`. Funciones:

- Enviar las peticiones (requests) a los manejadores (handlers) para que sean procesadas.
- El default handler son los controladores (`@Controller`, `@RequestMapping`).
- Encargado de resolver las vistas (views).

Con la dependencia Spring Web se pueden crear RESTful Web Services utilizando la anotación `@Controller` y `@RequestMapping`. Basado en Spring IoC container (Inyección de Dependencias).

Spring MVC se integra con otros proyectos de Spring como pueden ser: Spring Data JPA, Spring Cloud y Spring Security.
