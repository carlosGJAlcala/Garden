---
title: "Graphql"
date: 2025-01-01
tags:
  - desarrollo-software
---

**Apuntes completos sobre GraphQL con Node.js, Express y SQLite**

**Requisitos previos**

- **Node.js y Express**: Usamos Node.js con el framework Express para crear un servidor HTTP que pueda recibir y responder peticiones.
    
- **Base de datos SQLite**: Elegimos SQLite porque todo se guarda en un único archivo, lo que simplifica el desarrollo.
    
- **ORM Objection.js**: Para interactuar con la base de datos de manera más sencilla y estructurada.
    
- **Yarn**: Gestor de paquetes alternativo a npm, con algunas mejoras de velocidad y gestión de dependencias.
    
- **Nodemon**: Instalado como dependencia de desarrollo (`yarn add nodemon -D`) para reiniciar automáticamente la aplicación sin tener que ejecutar manualmente `node index.js` cada vez.
    
- **Casual**: Librería para generar valores aleatorios (mock data).
    

---

### **Pasos para montar el proyecto**


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[01-Ciberseguridad/Malware/Apuntes|Apuntes]]. [[02-Ciencias-Computacion/IA/Notas|Notas]].

1. **Inicializar el proyecto**
    
    ```bash
    yarn init -y
    ```
    
    Esto crea el archivo `package.json` con la configuración básica.
    
2. **Instalar Express**
    
    ```bash
    yarn add express
    ```
    
3. **Instalar body-parser**
    
    ```bash
    yarn add body-parser
    ```
    
    Permite procesar el cuerpo (`body`) de las peticiones HTTP en Express.
    
4. **Instalar dependencias de GraphQL**
    
    ```bash
    yarn add graphql express-graphql graphql-tools
    ```
    
    _Nota_: En Yarn se pueden instalar varias dependencias separadas por espacios.
    
5. **Crear el servidor HTTP**  
    Archivo `index.js` con la configuración de Express y la carga de GraphQL.
    
6. **Crear el esquema de GraphQL (`schema.js`)**
    
    - Importar `makeExecutableSchema` desde `graphql-tools`.
        
    - Definir `typeDefs` y `resolvers`.
        
    - Exportar el esquema.
        
7. **Configurar Express para GraphQL**
    
    - Importar `graphqlHTTP` desde `express-graphql`.
        
    - Añadir la ruta `/graphql`.
        
    - Activar `graphiql` para usar la interfaz interactiva de consultas.
        
8. **Definir el Query Type**
    
    - En GraphQL es como definir los endpoints en una API REST.
        
9. **Crear los resolvers**
    
    - Son las funciones que responden a las queries.
        
    - Ejemplo: `Query` es el tipo más genérico.
        
10. **Crear mocks de datos**
    
    - Importar `addMockFunctionsToSchema` de `graphql-tools`.
        
    - Asociar el esquema a funciones de mock.
        
    - Usar `casual` para generar valores aleatorios.
        
    - Activar `preserveResolvers` para dar prioridad a resolvers reales sobre mocks.
        
11. **Integrar la base de datos**
    
    - Instalar Knex:
        
        ```bash
        yarn add knex sqlite3
        ```
        
    - Crear scripts `db:migrate` y `db:seed` en `package.json`.
        
    - Carpeta `models` para modelos ORM y `db` para migraciones y seeds.
        
    - Crear `knexfile.js` con configuración para desarrollo y producción.
        
12. **Configurar Objection.js (ORM)**
    
    - Crear `setup.js` para la conexión usando `knexfile.js`.
        
    - Requerirlo en `index.js` para que esté disponible en cada request.
        
    - Importar modelos en los schemas.
        
    - Usar `Model.query()` para consultas.
        
    - Usar `eager()` para cargar relaciones.
        
13. **Modularizar el esquema y resolvers**
    
    - Exportar resolvers y schemas en archivos separados.
        
    - En `makeExecutableSchema`, pasar `typeDefs` como un array.
        
14. **Agregar Mutations**
    
    - Convención: usar un verbo y un sustantivo (`createUser`, `updatePost`, etc.).
        
    - Todas las mutations devuelven el tipo que modifican.
        
    - Se puede usar `input` para agrupar parámetros.
        
    - Agregar la mutation en `resolvers`.
        
15. **Búsquedas avanzadas**
    
    - Usar `union` cuando un tipo puede resolver a varios tipos distintos.
        
16. **Errores de negocio**
    
    - Usar `throw new Error()` dentro de resolvers.
        
17. **Consumir una API GraphQL**
    
    - Se puede usar POST o GET.
        
    - Recomendado: clientes como **Apollo Client** o **Relay**.
        
18. **Recursos útiles**
    
    - GraphQL Cheatsheet
        
    - SWAPI GraphQL
        
    - GraphQL Voyager
        
    - Apollo Launchpad
        
    - GraphQL Anywhere
        
    - Graph.cool
        
    - Scaphold
        
    - Apollo Optics
        
    - Awesome GraphQL
        

---

**Notas adicionales**

- `package.json` define dependencias y scripts del proyecto.
    
- `yarn.lock` fija las versiones exactas de las dependencias para evitar problemas en despliegues.
    
- El script `start` es una convención en Node.js para iniciar la app.
    
- En GraphQL, los comentarios usan `#`.
    
- Migraciones en base de datos: control de versiones con `up` y `down`.
    
- Seeds: insertar datos falsos o iniciales en la base.
    
- Eager loading: cargar una entidad junto con sus relaciones en una sola consulta.
    

---
**Qué es GraphQL**  
GraphQL es un lenguaje de consulta y un entorno de ejecución creado por Facebook en 2012 y liberado como open source en 2015. Su propósito es optimizar cómo las aplicaciones cliente obtienen datos de una API, permitiendo que **el cliente especifique exactamente qué información quiere** y en qué formato, evitando datos innecesarios.

---

**Cómo funciona**

- El **cliente** envía una **query** (consulta) que describe los datos que quiere.
    
- El **servidor** tiene un **schema** (esquema) que define los tipos de datos disponibles y cómo obtenerlos.
    
- Los **resolvers** son funciones que el servidor ejecuta para devolver los datos solicitados.
    
- GraphQL **no depende de la base de datos**: puede usar SQL, NoSQL, APIs externas o incluso datos generados.
    

---

**Ventajas frente a REST**

- En REST, cada endpoint devuelve un formato fijo; en GraphQL, el cliente decide qué campos necesita.
    
- Una sola query puede reemplazar múltiples peticiones REST, reduciendo latencia.
    
- Es fuertemente tipado, lo que mejora la autocompletación y la validación.
    
- Facilita la evolución de la API sin romper compatibilidad.
    

---

**Elementos clave de GraphQL**

- **Schema**: Documento que define todos los tipos y operaciones disponibles.
    
- **Types**: Definen la estructura de los datos (por ejemplo `type User { id: ID, name: String }`).
    
- **Query**: Operaciones para **leer** datos.
    
- **Mutation**: Operaciones para **crear, modificar o borrar** datos.
    
- **Subscription**: Permite actualizaciones en tiempo real (normalmente vía WebSockets).
    
- **Resolvers**: Funciones que implementan la lógica para obtener los datos solicitados.
    

---

**Ejemplo básico**

_Schema_:

graphql

CopiarEditar

`type Query {   hello: String   user(id: ID!): User }  type User {   id: ID   name: String   email: String }`

_Query desde el cliente_:

graphql

CopiarEditar

`{   user(id: 1) {     name     email   } }`

_Respuesta del servidor_:

json

CopiarEditar

`{   "data": {     "user": {       "name": "Juan Pérez",       "email": "juan@example.com"     }   } }`