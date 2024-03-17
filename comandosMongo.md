<!-- Titulos -->
# Mongo

### Términos de Mongo DB vs SQL:
|         SQL        |          Mongo DB         | 
|--------------------|---------------------------|
| Base de datos      | Base de datos             | 
| Tabla o relaciones | Colecciones               | 
| index              | index                     | 
| Fila               | Documentos                | 
| Columna            | Campo                     | 
| Joins              | Integrados en el documento| 

JSON: Java Script Object Notation.  
Los datos se separan por clave valor aunque no son de tipo clave valor, son documentales.

### Estructura de un JSON:
```JSON
{
  "clave1": "valor1",
  "clave2": "valor2",
  "clave3": {
    "clave3-1": "valor3-1",
    "clave3-2": "valor3-2"
  },
  "clave4": ["valor4-1", "valor4-2", "valor4-3"]
}
```

### Significados de la estructura JSON anterior:
<!-- Listas desordenadas (solo con viñetas) -->
* Cada par de "clave: valor" está separado por una coma (,).
* Las claves son strings y deben estar entre comillas dobles (").
* Los valores pueden ser strings, números, booleanos, arrays (listas) u otros objetos JSON.
* Los arrays se representan con corchetes ([  ]) y pueden contener valores de cualquier tipo, incluidos otros arrays u objetos JSON.
* Los objetos JSON se representan con llaves ({}) y contienen pares de "clave: valor".
* Este es solo un ejemplo básico; los JSON pueden ser mucho más complejos dependiendo de los datos que necesites almacenar.

### Ahora para meter multiples documentos en una sola colección:
En este ejemplo, cada objeto dentro del array (los corchetes) representa un documento que podría ser insertado en una colección de una base de datos, por ejemplo. Cada documento tiene sus propias claves y valores que representan los campos y sus valores respectivos.

```JSON
[
  {
    "Categoria1": "John",
    "apellido": "Doe",
    "edad": 30,
    "direccion": "123 Avenida Principal"
  },
  {
    "nombre": "Alice",
    "apellido": "Smith",
    "edad": 28,
    "direccion": "456 Calle Secundaria"
  },
  {
    "nombre": "Bob",
    "apellido": "Johnson",
    "edad": 32,
    "direccion": "789 Calle Terciaria"
  }
]

```

**NOTA:** En mongo tenemos que poner los id con (-id), si no lo ponemos se va a generar solito.

Otro ejemplo de multiples documentos:
```JSON
[
    {
    "-id": 1,
    "nombre": "Linea Blanca",
    "Productos":{
		  "nombre": "Refrigerador",
		  "stock": 17,
           } 
    },
    {
    "-id": 2,
    "nombre": "Lacteos",
    "Productos": [
            {
            "nombre": "Leche de burra fresca",
            "stock": 22,
            },
            {
            "nombre": "Leche de burra fresca",
            "stock": 22,
            }
            ]
    },
]

```

---

*COMANDOS PARA MONGO SHELL*
## `Show databases` en MongoDB

### Descripción
El comando `show databases` se utiliza en la interfaz de línea de comandos de MongoDB para mostrar una lista de todas las bases de datos disponibles en el servidor MongoDB actual.

### Sintaxis
```shell
show databases

show dbs
```

Parámetros: Ninguno.

Devuelve: Una lista de las bases de datos disponibles en el servidor MongoDB actual.

Ejemplo:
```javascript
show databases
```

## `use databases` en MongoDB

### Descripción
El comando `use nombreDeLaBaseDeDatos` se utiliza en la interfaz de línea de comandos de MongoDB para cambiar la base de datos en la que se trabajará.

### Sintaxis
```shell
use nombreDeLaBaseDeDatos
```

Parámetros: El nombre de la base de datos a la que se desea cambiar.

Devuelve: Nada, este comando simplemente cambia el contexto de la base de datos a la especificada.

Ejemplo:
```javascript
use mydatabase
```

## `db.createCollection` En MongoDB

### Descripción
El método `db.createCollection("nombreDeLaColeccion")` se utiliza en la interfaz de línea de comandos de MongoDB para crear una nueva colección en la base de datos actual.

### Sintaxis
```javascript
db.createCollection("nombreDeLaColeccion", <opciones>)
```
Parámetros:

1. "nombreDeLaColeccion": El nombre de la colección que se desea crear.

2. "opciones" (opcional): Un documento que contiene opciones de configuración para la colección, como el tamaño del almacenamiento o el límite de documentos.

Devuelve: Nada, este método simplemente crea una nueva colección en la base de datos actual.

Ejemplo:
```javascript
db.createCollection("nuevaColeccion")
```

## **Para limpiar la pantalla de nuestro shell:**
```
cls
```

## `insertOne` en MongoDB

### Descripción
El método `insertOne` se utiliza para insertar un solo documento en una colección de MongoDB.

### Sintaxis
```javascript
db.collection.insertOne(
   <document>,
   {
      writeConcern: <document>
   }
)
```
Parámetros:
1. documento: El documento que se va a insertar en la colección.

2. writeConcern (opcional): Especifica el nivel de confirmación que se requiere para la operación. Es un documento que especifica el nivel de garantía de escritura.

3. bypassDocumentValidation (opcional): Permite omitir la validación de documentos durante la operación de inserción. Por defecto es false.

Devuelve: Un objeto InsertOneResult que proporciona información sobre la operación de inserción, incluido el ID del documento insertado.

Ejemplo:
```javascript
db.inventory.insertOne(
   {
      item: "caja",
      qty: 100,
      status: "A"
   }
)
```

## `db.nombreDeLaColeccion.find()` en MongoDB

### Descripción
El método `find()` se utiliza en MongoDB para recuperar documentos de una colección que coincidan con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.find(<consulta>, <proyección>)
```
Parámetros:
1. "consulta" (opcional): Especifica los criterios de selección de documentos. Si se omite, devuelve todos los documentos de la colección.

2. "proyección" (opcional): Define qué campos incluir o excluir en los resultados de la consulta.

Devuelve: Un cursor que puede iterarse para acceder a los documentos que coinciden con los criterios de consulta.

Ejemplo:
```javascript
db.miColeccion.find({}, { _id: 0, campo1: 1, campo2: 1 })
```

## `db.dropDatabase()` En MongoDB

### Descripción
El método `db.dropDatabase('nombreDeLaDataBase')` se utiliza en MongoDB para eliminar una base de datos completa.

### Sintaxis
```javascript
db.dropDatabase('nombreDeLaDataBase')
```
Parámetros:
1. "nombreDeLaDataBase": El nombre de la base de datos que se desea eliminar.

Devuelve: Nada, este método elimina la base de datos especificada.

Ejemplo:
```javascript
db.dropDatabase('mydatabase')
```

## `db.nombreDeLaColeccion.insertMany([{  }])` en MongoDB

### Descripción
El método `insertMany([{  }])` se utiliza en MongoDB para insertar múltiples documentos en una colección.

### Sintaxis
```javascript
db.nombreDeLaColeccion.insertMany([
   { documento1 },
   { documento2 },
   ...
])
```

Parámetros:
1. [{ }]: Un arreglo de documentos que se desean insertar en la colección.

Devuelve: Un objeto InsertManyResult que proporciona información sobre la operación de inserción, incluidos los IDs de los documentos insertados.

Ejemplo: Este comando inserta dos documentos en la colección "miColeccion".

```javascript
db.miColeccion.insertMany([
   { campo1: "valor1", campo2: "valor2" },
   { campo1: "valor3", campo2: "valor4" }
])
```
## `db.libros.find({ })` En MongoDB

### Descripción
El método `find({ })` se utiliza en MongoDB para realizar consultas en una colección, recuperando documentos que coincidan con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.find({ <filtro> })
```
Parámetros:
1. "filtro" (opcional): Especifica los criterios de selección de documentos. Si se omite, devuelve todos los documentos de la colección.

Devuelve: Un cursor que puede iterarse para acceder a los documentos que coinciden con los criterios de consulta que nosotros especifiquemos.

Ejemplo: Este comando busca todos los libros en la colección "libros" escritos por Gabriel García Márquez.
```javascript
db.libros.find({ autor: "Gabriel García Márquez" })
```

Ejemplo 2: Este comando busca todos los libros en la colección "libros" que se hayan publicado en 1990 o después.
```javascript
db.libros.find({ año_publicación: { $gte: 1990 } })
```

### Para las consultas con filtro tenemos la siguiente tabla con `selectores de comparacion`:

| Nombre |                             Descripción                                     |
|--------|-----------------------------------------------------------------------------|
|  $eq   | Coincide con valores que son iguales a un valor especificado.               |
|  $gt   | Coincide con valores que son mayores que un valor especificado.             |
|  $gte  | Coincide con valores que son mayores o iguales que un valor especificado.   |
|  $in   | Coincide con cualquiera de los valores especificados en una matriz.         |
|  $lt   | Coincide con valores que son menores que un valor especificado.             |
|  $lte  | Coincide con valores que son menores o iguales que un valor especificado.   |
|  $ne   | Coincide con todos los valores que no son iguales a un valor especificado.  |
|  $nin  | No coincide con ninguno de los valores especificados en una matriz.         |

### Para las consultas con filtro tenemos la siguiente tabla con `selectores logicos`:

| Nombre | Descripción                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| $and   | Une cláusulas de consulta con una lógica AND que devuelve todos los documentos que coinciden con las condiciones de ambas cláusulas.                                   |
| $not   | Invierte el efecto de una expresión de consulta y devuelve documentos que no coinciden con la expresión de consulta.                                            |
| $nor   | Une cláusulas de consulta con una lógica NOR que devuelve todos los documentos que no coinciden con ambas cláusulas.                                           |
| $or    | Une cláusulas de consulta con una lógica OR que devuelve todos los documentos que coinciden con las condiciones de cualquiera de las cláusulas.                |

### Para las consultas con filtro tenemos la siguiente tabla con `selectores  de elementos`:

| Nombre  | Descripción                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| $exists | Coincide con documentos que tienen el campo especificado.                                           |
| $type   | Selecciona documentos si un campo es del tipo especificado.      

## `db.nombreDeLaColeccion.findOne()` en MongoDB

### Descripción
El método `findOne()` se utiliza en MongoDB para recuperar un solo documento de una colección que coincida con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.findOne(<consulta>, <proyección>)
```

Parámetros:

1. "consulta" (opcional): Especifica los criterios de selección de documentos. Si se omite, devuelve el primer documento que encuentre en la colección.

2. "proyección" (opcional): Define qué campos incluir o excluir en el resultado del documento.

Devuelve: El primer documento que coincide con los criterios de consulta o null si no se encuentra ningún documento que coincida.

Ejemplo: 

Este comando busca y devuelve el primer documento en la colección "miColeccion" donde el campo es igual a "valor", excluyendo el campo "_id" y mostrando solo los campos "campo1" y "campo2".

```javascript
db.miColeccion.findOne({ campo: "valor" }, { _id: 0, campo1: 1, campo2: 1 })
```

## `db.nombreDeLaColeccion.updateOne()` en MongoDB

### Descripción
El método `updateOne()` se utiliza en MongoDB para actualizar un solo documento en una colección que coincida con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.updateOne(
   <filtro>,
   <actualización>,
   {
      upsert: <boolean>,
   }
)
```
Parámetros:

1. "filtro": Especifica los criterios de selección de documentos para la actualización.
2. "actualización": Define las modificaciones a realizar en el documento.
3. { upsert: "boolean" } (opcional): Si se establece en true, crea un nuevo documento si no se encuentra ningún documento que coincida con los criterios de consulta.

Devuelve: Un objeto UpdateResult que proporciona información sobre la operación de actualización, como el número de documentos afectados.

Ejemplo: 

Este comando busca un documento en la colección "miColeccion" donde el campo "nombre" sea "Ejemplo". Si lo encuentra, actualiza el campo "edad" a 30. Si no encuentra ningún documento que cumpla con la condición de búsqueda, crea un nuevo documento con los campos "nombre" y "edad".

```javascript
db.miColeccion.updateOne(
   { nombre: "Ejemplo" },
   { $set: { edad: 30 } },
   { upsert: true }
)
```

## `db.nombreDeLaColeccion.updateMany()` en MongoDB

### Descripción
El método `updateMany()` se utiliza en MongoDB para actualizar múltiples documentos en una colección que coincidan con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.updateMany(
   <filtro>,
   <actualización>,
   {
      upsert: <boolean>,
   }
)
```

Parámetros:
1. "filtro": Especifica los criterios de selección de documentos para la actualización.

2. "actualización": Define las modificaciones a realizar en los documentos seleccionados.

3. { upsert: <boolean> } (opcional): Si se establece en true, crea nuevos documentos si no se encuentra ninguno que coincida con los criterios de consulta.

Devuelve: Un objeto UpdateResult que proporciona información sobre la operación de actualización, como el número de documentos afectados.

Ejemplo: 

Este comando busca todos los documentos en la colección "miColeccion" donde el campo "tipo" sea "A". Para cada documento encontrado, establece el campo "cantidad" en 100. Si no encuentra ningún documento que cumpla con la condición de búsqueda, crea un nuevo documento con los campos "tipo" y "cantidad".

```javascript
db.miColeccion.updateMany(
   { tipo: "A" },
   { $set: { cantidad: 100 } },
   { upsert: true }
)
```
## `db.nombreDeLaColeccion.deleteOne()` en MongoDB

### Descripción
El método `deleteOne()` se utiliza en MongoDB para eliminar un solo documento de una colección que coincida con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.deleteOne(<filtro>)
```

Parámetros:
1. "filtro": Especifica los criterios de selección de documentos para la eliminación.

Devuelve: Un objeto DeleteResult que proporciona información sobre la operación de eliminación, como el número de documentos eliminados (que puede ser 0 o 1).

Ejemplo:

Este comando busca y elimina el primer documento en la colección "miColeccion" donde el campo "nombre" sea "Ejemplo".

```javascript
db.miColeccion.deleteOne({ nombre: "Ejemplo" })
```

## `db.nombreDeLaColeccion.deleteMany()` en MongoDB

### Descripción
El método `deleteMany()` se utiliza en MongoDB para eliminar múltiples documentos de una colección que coincidan con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.deleteMany(<filtro>)
```

Parámetros:
1. "filtro": Especifica los criterios de selección de documentos para la eliminación.

Devuelve: Un objeto DeleteResult que proporciona información sobre la operación de eliminación, como el número de documentos eliminados.

Ejemplo:

Este comando busca y elimina todos los documentos en la colección "miColeccion" donde el campo "tipo" sea "A".

```javascript
db.miColeccion.deleteMany({ tipo: "A" })
```

## `db.nombreDeLaColeccion.replaceOne()` en MongoDB

### Descripción
El método `replaceOne()` se utiliza en MongoDB para reemplazar un solo documento de una colección que coincida con ciertos criterios de consulta.

### Sintaxis
```javascript
db.nombreDeLaColeccion.replaceOne(
   <filtro>,
   <documento>,
   {
      upsert: <boolean>,
   }
)
```

Parámetros: 
1. "filtro": Especifica los criterios de selección de documentos para la sustitución.

2. "documento": El nuevo documento que reemplazará al documento seleccionado.

3. "{ upsert: <boolean> }" (opcional): Si se establece en true, crea un nuevo documento si no se encuentra ninguno que coincida con los criterios de consulta.

Devuelve: Un objeto UpdateResult que proporciona información sobre la operación de actualización, como el número de documentos afectados.

Ejemplo: 

Este comando busca y reemplaza el primer documento en la colección "miColeccion" donde el campo "nombre" sea "Ejemplo". Si lo encuentra, lo reemplaza con el documento especificado. Si no encuentra ningún documento que cumpla con la condición de búsqueda, crea un nuevo documento con los campos "nombre" y "tipo".

```javascript
db.miColeccion.replaceOne(
   { nombre: "Ejemplo" },
   { nombre: "Nuevo Ejemplo", tipo: "B" },
   { upsert: true }
)
```
## Ahora pasamos a las `Agregaciones` en MongoDB

Las agregaciones en MongoDB son una poderosa herramienta que permite realizar operaciones de procesamiento de datos avanzadas en documentos de colecciones. Las agregaciones se utilizan para realizar transformaciones complejas, filtrados, agrupamientos, ordenamientos y operaciones de proyección en conjuntos de datos.

Las agregaciones en MongoDB se componen de una serie de etapas (stages) que se aplican secuencialmente a los documentos de una colección. Cada etapa realiza una operación específica en los datos y pasa el resultado a la siguiente etapa. Esto permite construir pipelines de agregación flexibles y escalables.

## `Ejemplos de Agregaciones` en MongoDB

1. Proyección:
La etapa $project se utiliza para incluir o excluir campos en los documentos de salida de la agregación. 

Por ejemplo: Esta agregación proyecta solo los campos "nombre" y "edad" de cada documento en la colección "miColeccion".

```javascript
db.miColeccion.aggregate([
   { $project: { nombre: 1, edad: 1 } }
])
```

2. Agrupación:
La etapa $group se utiliza para agrupar documentos según un campo específico y realizar operaciones de agregación en esos grupos. 

Por ejemplo: Esta agregación agrupa los documentos en la colección "miColeccion" por el campo "tipo" y calcula la suma de los valores del campo "cantidad" para cada grupo.

```javascript
db.miColeccion.aggregate([
   { $group: { _id: "$tipo", total: { $sum: "$cantidad" } } }
])
```

3. Ordenamiento:
La etapa $sort se utiliza para ordenar los documentos de salida de la agregación según uno o más campos. 

Por ejemplo: Esta agregación ordena los documentos en la colección "miColeccion" en orden ascendente según el campo "edad".

```javascript
db.miColeccion.aggregate([
   { $sort: { edad: 1 } }
])
```

4. Filtrado:
La etapa $match se utiliza para filtrar los documentos de entrada de la agregación según un criterio específico. 

Por ejemplo: Esta agregación filtra los documentos en la colección "miColeccion" para incluir solo aquellos con el campo "tipo" igual a "A".

```javascript
db.miColeccion.aggregate([
   { $match: { tipo: "A" } }
])
```

5. Limitación
La etapa $limit se utiliza para limitar el número de documentos de salida de la agregación. 

Por ejemplo: Esta agregación limita la cantidad de documentos de salida a 10 en la colección "miColeccion".

```javascript
db.miColeccion.aggregate([
   { $limit: 10 }
])
```

## `Pipeline 1` hecho en clase con 3 stages

`Filtrado, Proyección y Ordenamiento`:

Este pipeline filtra los documentos por la editorial "Biblio", luego proyecta solo los campos especificados y finalmente ordena los resultados por el campo "precio".

Explicación:

`$match`: Filtra los documentos por la editorial "Biblio".

`$project`: Proyecta solo los campos especificados en la salida, incluyendo el cálculo de la ganancia total.

`$sort`: Ordena los documentos por el campo "precio" en orden ascendente.

```javascript
[
  {
    $match:
      /**
       * query: The query in MQL.
       */
      {
        editorial: "Biblio",
      },
  },
  {
    $project:
      /**
       * specifications: The fields to
       *   include or exclude.
       */
      {
        _id: 0,
        titulo: 1,
        precio: 1,
        cantidad: 1,
        "Nombre editorial": "$editorial",
        "Total Ganancia": {
          $multiply: ["$precio", "$cantidad"],
        },
      },
  },
  {
    $sort:
      /**
       * Provide any number of field/order pairs.
       */
      {
        precio: 1,
      },
  },
]
```
## `Pipeline 2` hecho en clase con 2 stages

`Agrupación y Ordenamiento`:

Este pipeline agrupa los documentos por la editorial y cuenta cuántos documentos hay en cada grupo, luego los ordena por el número de documentos.

Explicación:

`$group`: Agrupa los documentos por la editorial y cuenta cuántos documentos hay en cada grupo.

`$sort`: Ordena los resultados por el número de documentos en orden ascendente.

```javascript
[
  {
    $group:
      /**
       * _id: The id of the group.
       * fieldN: The first field name.
       */
      {
        _id: "$editorial",
        "Numero Documentos": {
          $count: {},
        },
      },
  },
  {
    $sort:
      /**
       * Provide any number of field/order pairs.
       */
      {
        "Numero Documentos": 1,
      },
  },
]
```

## `Pipeline 3` hecho en clase con 2 stages

`Agrupación, Cálculo de Medias y Ordenamiento`

Este pipeline agrupa los documentos por la editorial y calcula el número de documentos, la media de los precios y el precio máximo en cada grupo, luego los ordena por el precio máximo.

Explicación:

`$group`: Agrupa los documentos por la editorial y calcula el número de documentos, la media de los precios y el precio máximo en cada grupo.

`$sort`: Ordena los resultados por el precio máximo en orden ascendente.

```javascript
[
  {
    $group:
      /**
       * _id: The id of the group.
       * fieldN: The first field name.
       */
      {
        _id: "$editorial",
        "Numero de Documentos": {
          $count: {},
        },
        media: {
          $avg: "$precio",
        },
        "Precio Maximo": {
          $max: "$precio",
        },
      },
  },
  {
    $sort:
      /**
       * Provide any number of field/order pairs.
       */
      {
        "Precio Maximo": 1,
      },
  },
]
```

## `Pipeline 4 con out` hecho en clase con 2 stages

`Agrupación, Cálculo de Medias y Salida a una Colección`

Este pipeline es similar al anterior, pero además de calcular la media de los precios, redondea la media a dos decimales y guarda los resultados en una nueva colección llamada "Media_Editoriales".

Explicación:

`$group`: Agrupa los documentos por la editorial y calcula el número de documentos y la media de los precios.

`$set`: Redondea la media de los precios a dos decimales.

`$out`: Guarda los resultados en una nueva colección llamada "Media_Editoriales".

```javascript
[
  {
    $group:
      /**
       * _id: The id of the group.
       * fieldN: The first field name.
       */
      {
        _id: "$editorial",
        Numero: {
          $count: {},
        },
        media: {
          $avg: "precio",
        },
      },
  },
  {
    $set:
      /**
       * field: The field name
       * expression: The expression.
       */
      {
        "Media Total": {
          $trunc: ["$media", 2],
        },
      },
  },
  {
    $out:
      /**
       * Provide the name of the output collection.
       */
      "Media_Editoriales",
  },
]
```

## `Pipeline 5 con unset y count` hecho en clase con 4 stages

`Agrupación, Cálculo de Medias, Eliminación de Campo y Count`

Este pipeline es similar al anterior, pero además de calcular la media de los precios, elimina el campo "media" y cuenta cuántos documentos hay en cada grupo.

Explicación:

`$group`: Agrupa los documentos por la editorial y calcula el número de documentos y la media de los precios.

`$set`: Redondea la media de los precios a dos decimales.

`$unset`: Elimina el campo "media" de los resultados.

`$count`: Cuenta cuántos documentos hay en cada grupo.

```javascript
[
  {
    $group:
      /**
       * _id: The id of the group.
       * fieldN: The first field name.
       */
      {
        _id: "$editorial",
        Numero: {
          $count: {},
        },
        media: {
          $avg: "precio",
        },
      },
  },
  {
    $set:
      /**
       * field: The field name
       * expression: The expression.
       */
      {
        "Media Total": {
          $trunc: ["$media", 2],
        },
      },
  },
  {
    $unset:
      /**
       * Provide the name of the output collection.
       */
      "media",
  },
]
```
Espero que te sirva :wink: :computer: :100:

Por: Benjamin Peña Marin :sunglasses: :+1:



















