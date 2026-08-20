## **Apuntes completos de MongoDB**

**¿Qué es MongoDB?**

- El nombre viene de _"humongous"_ (enorme), porque está diseñado para manejar grandes volúmenes de datos.
- Es una **base de datos NoSQL orientada a documentos**, que almacena datos en formato **BSON** (JSON binario).
- Se ejecuta como servicio, similar a MySQL.
- Para iniciarlo:
    - `mongod` → levanta el servidor de base de datos.
    - `mongo` → abre la consola interactiva del cliente para ejecutar comandos.

### **Herramientas**

- **Robo 3T**: Cliente gráfico para interactuar con MongoDB.
- En Linux, para instalar paquetes comprimidos:

    ```bash
    tar -zvfx archivo.tar.gz
    ```

### **Características importantes**

- En MongoDB, **una colección puede contener documentos con estructuras diferentes**.
- Si un documento no tiene un campo presente en otros, Mongo lo considera como `undefined`.

### **Operaciones básicas**

#### **1. Crear documentos**

```js
db.<colección>.insertOne(
    { <objeto JSON> }
)
```

Ejemplo:

```js
db.usuarios.insertOne({
    nombre: "Juan",
    edad: 25
});
```

#### **2. Consultar documentos (`find`)**

- La consulta (`query`) tiene dos partes:
    1. **Condición** → `{age: {$gt: 18}}`
    2. **Proyección** (qué campos mostrar) → `{name: 1, address: 1}`
- Ejemplo:

```js
db.users.find(
    { age: { $gt: 18 } },  // Filtro
    { name: 1, address: 1 } // Proyección
).limit(5); // Limitar resultados
```

#### **3. Seleccionar base de datos**

```js
use nombredatabase
```

#### **4. Actualizar documentos (`update`)**

```js
db.getCollection('usuarios').update(
    { "rides": { $eq: 0 } },               // Filtro
    { $set: { "status": "fault" } },       // Cambios
    { multi: true }                        // Actualizar varios
)
```

- `$set` añade o modifica campos si se cumple la condición.
- Si no se usa `$set`, Mongo reemplaza todo el documento.

#### **5. Insertar con Write Concern y Ordered**

```js
db.collection.insert(
    { /* documento o array de documentos */ },
    {
        writeConcern: { w: 1, j: true, wtimeout: 5000 },
        ordered: true
    }
)
```

- **`w`** → Confirma la escritura cuando se replica en el número de nodos indicado (`0`, `1` o `"majority"`).
- **`j`** → Guarda en el _journal_ (registro binario secuencial para recuperación en caso de fallo).
- **`wtimeout`** → Tiempo máximo para esperar confirmación de escritura.
- MongoDB admite hasta **100 000 escrituras por operación**.

#### **6. Agregaciones (`aggregate`)**

- Para filtrar, agrupar y calcular estadísticas.

```js
db.orders.aggregate([
    { $match: { status: "A" } },
    { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
])
```

- `$match` filtra datos.
- `$group` agrupa resultados y aplica operaciones como `$sum`, `$avg`, `$max`, etc.

#### **7. Recorrer y actualizar con `forEach`**

```js
db.getCollection('usuarios').find({}).forEach((doc) => {
    db.getCollection('usuarios').update(
        { _id: doc._id },
        { $set: { rides: NumberInt(doc.rides) } }
    );
});
```

- Útil para hacer conversiones o actualizaciones masivas.

---

**Notas clave:**

- MongoDB **no requiere esquema fijo** (schema-less).
- Los datos se guardan en **colecciones** (equivalente a tablas en SQL).
- Las consultas se parecen a JSON, pero con operadores especiales (`$gt`, `$lt`, `$eq`, `$in`, etc.).
- Es ideal para datos flexibles y grandes volúmenes con alta velocidad de lectura/escritura.
