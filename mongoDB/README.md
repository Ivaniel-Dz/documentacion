# MongoDB
>[Documentación](https://www.mongodb.com/docs/manual/reference/)

## Instalación
1.  MongoDB Shell <br>
https://www.mongodb.com/try/download/shell

2. Instalar MongoDB Enterprise Server Download  <br>
https://www.mongodb.com/try/download/enterprise

3. Instalar Robo 3T y Studio 3T *(Opcional alternativa de Compass y recomendado)*<br>
https://studio3t.com/download/

4. Verificar la disponibilidad del puerto ``27017``  <br>
http://portquiz.net:27017

## Documentos
![alt text](/img/estructura.png)

- Formato JSON
- cada documentos se identifica por el campo ``_id``
    - los valores ``_id`` deben ser todos únicos

## Tipos de datos
- Cadenas de caracteres (``string``)
- Enteros (``int32``)
- Decimales (``double``)
- Fechas (``dates``)
- Documentos (``Object`` - ``Document``)
- Vectores (``Array``)
- *Sistemas de coordenadas Geoespaciales

## Consultas
### Filtro de Igualdad
citibike.trips -> 'end station name'

### JSON (JavaScript Object Notation)
   1. {}
   2. campos (2 partes)
   3. clave : valor
   4. :
   5. 'valor' 

### FILTROS DE RANGO
 ```json
  {'birth year': {$gte: 1985, $lt: 1990}}
```

## JSON
- **J**ava**S**cript **O**bject **N**otation
- Formato ligero de intercambio de datos.
    - fácil de leer y editar para los humanos
    - fácil de interpretar y generar para los ordenadores
- Extension.json
- MongoDB es una BD orientado a documentos
    -documentos JSON = Objeto JSON

{clave: 'valor'}

## Comandos de Mongo
```bash
## Ingresa al shell de mongo
mongosh --nodb
```

```bash
mongosh cluester
```

```bash
# Muestra las base datos
show dbs
# Muestra las colecciones
show collections
# Ingresa a la base datos
use nameDB
```
## Lenguajes de Consultas de Datos
### Crear Documentos
#### **insertOne()**
- Método para insertar un solo documento en una colección
- Si la colección no existe actualmente, el método creara la colección.
    - ``use nombre_BD``
    - ``db.nombreColección.insertOne({campo1: "valor", campo2: "valor", ...})``

>ejemplo:
```shell
 use movies
 db.peliculaBasura.insertOne( 
     {
   "title":"Kill Bill: Vol. 1",
   "year":2003,
   "imdb":"tt0266697",
   "director":"Quentin Tarantino"
     }
 )
```

#### **insertMany()**
- Método para insertar mas de un documentos en una colección.
- Si la colección no existe actualmente, el método crearan la colección.
    - ``use db``
    - ``db.nombreColección.insertMany([{documento1}, {documento2}, ...])``

>Ejemplos:
```shell
use movies

db.peliculaBasura.insertMany(
    [
        {
        "_id" : "tt0110912",
        "title" : "Pulp Fiction",
        "year" : 1994,
        "director" : "Quentin Tarantino"
        },
        {
        "_id" : "tt0266697",
        "title":"Kill Bill: Vol. 1",
        "year":2003,
        "director":"Quentin Tarantino"
        },
        {
        "_id" : "tt1853728",
        "title" : "Django Unchained",
        "year" : 2012,
        "director" : "Quentin Tarantino"
        }
    ]
)
```

### Leer Documentos:
#### **find()**
``db.nombreColección.find()``

>ejemplo:
```shell
# Muestra todo los documentos de la colección
db.peliculaBasura.find()

# Muestra un documento especifico con el clave que se cumpla de la colección
db.peliculaBasura.find( {"title": "Django Unchained"})

# Muestra dos documento especifico con el clave que se cumpla de la colección
db.peliculaBasura.find( {"year": 2012, "director": "Quentin Tarantino"})
```
>si va mas de una palabra la clave poner en "doble comillas"

#### **Cursores  en el método find()**
 
#### **Proyecciones en el método find()**

- db.nombreColec.find ( query, projection)
```shell
db.usuarios.find(
    {edad: {$gt: 18}},      #Query (muestra edad > 18)
    {nombre: 1, edad: 1}    #Projection (mostrar solo nombre y edad)
).limit(5)
```
- ``QUERY``, Permite filtrar los resultados utilizados operadores de consultas.
- ``PROJECTION``, Permite indicar los campos a mostrar ``{field:<value>, field2:<value> ...}``
- Donde si ``<valor> `` es ``1`` se *incluye* el campo y si es ``0`` se *excluye*.
- ``limit``, limita la cantidad de documentos a mostrar.


### Actualizar Documentos
#### **updateOne()**
actualiza un único documento dentro de la colección basado en el filtro.
``db.nombreColec.updateOne(filter, update, options)``
- ``filter``: especifica los documentos a actualizar
- ``update``: especifica que vamos a modificar
    - Se debe aplicar algún tipo de operador de actualización.
- operador $set
    - ``{ $set: {<field1>: <value1>, ...} }``
    - Toma un documento como argumento.
    - Actualiza el documento que coincide con el filtro con los campos indicados dentro del documento ``#set``.

>**Ejemplo:** recomendación filtrar por el id
```shell
db.movieDetails.updateOne ( 
 {title: "The Martian"} , 
 {$set: 
  { poster: "https://pics.filmaffinity.com/Marte_T..."}
 }
)
```

```shell
# Actualizar campos de tipo Vector
db.movieDetails.updateOne ( 
 {title: "The Martian"} , 
 {$set: 
  { cast: ["Matt Damon", "Jessica Chastain","Michael Peña","Kate Mara"]}
 }
)
```

```shell
# Actualizar campos de tipo Documento
db.movieDetails.updateOne ( 
 {title: "The Martian"} , 
 {$set: 
  { awards: 
   {wins: 8,
    nominations: 14,
    text: "Nominated for 3 Golden Globes. Another 8 wins & 14 nominations"
   } 
  }
 }
)
```

#### **updateMany()**
Actualiza todo los documentos que coinciden con el filtro especificado para una colección.
``db.nombreColec.updateMany (filter, update, options)``

>Ejemplo:
```shell
#Muestra los campos con su valor sea null
db.movieDetails.find({rated: null})

# Eliminar el campo rated de todos los documentos si su valor es null
db.movieDetails.updateMany ( 
 {rated: null} , 
 {$unset: { 
  rated: ""
  }
 })
```

#### **ReplaceOne**
Reemplaza un solo documento dentro de la colección basado en el filtro.

``db.nombColec.replaceOne(filter,replacement,options)``

```shell
db.pelisBasura.replaceOne(
 {title: "Django Unchained"}, 
 {
  "title":"Django Unchained",
  "director":"Quentin Tarantino",
  "cast": ["Jamie Foxx","Christoph Waltz","Leonardo  DiCaprio","Kerry Washington"]
 })
```

``` shell
# Uso de variable
let filter = { title: "Pulp Fiction" }
let doc = {   
    "title":"Pulp Fiction",
    "year":1994,  
    "director":"Quentin Tarantino"  
    }

db.pelisBasura.replaceOne(filter, doc);
```


#### **Operadores de actualización**
**Campo:**
- ``$set`` *establece el valor de un campo en un documento.*
- ``$unset`` *elimina el campo especificado de un documento.*
- ``$rename`` *cambia el nombre de un campo.*
- ``$min`` *multiplica el valor del campo por la cantidad especificada.*
- ``$max`` *solo actualiza el campo si el valor especificado es mayor que el valor del campo existente.*
- ``$inc`` *incrementa el valor del campo en la cantidad especificada.*

**Array:**
- ``addToSet`` *agrega elementos a una matriz solo si aún no existen en el conjunto.*
- ``$push`` *agrega un elemento a una matriz.*
- ``$pop`` *elimina el primer o último elemento de una matriz.*
- ``$pull`` *elimina todos los elementos de la matriz que coinciden con una consulta especificada.*
- ``$pullAll`` *elimina todos los valores coincidentes de una matriz*

**Modificadores:**
- ``$each`` *modifica los operadores ``$push`` y ``$addToSet`` para agregar varios elementos para las actualizaciones de la matriz.* ``{ $push:{ field: { $each: [ v1, v2 ... ] } } }``

- ``$position`` *modifica el operador ``$push`` para especificar la posición en la matriz para agregar elementos.*

#### **upserts()**
Si ``upsert: true`` y ningún documento coincide con el filtro, ``db.collection.updateOne()`` crea un nuevo documento basado en los criterios del filtro y las modificaciones de actualización. Consulte Actualizar con ``Upsert``.

Si especifica `upsert`: true en una colección fragmentada, debe incluir la clave de partición completa en el filtro. Para obtener más información sobre db.collection.
Comportamiento de ``updateOne()`` en una colección fragmentada, consulte Colecciones fragmentadas.

>Ejemplo:
```shell
db.pelisBasura.updateOne ( 
 {_id: "tt0110913"} , 
 {$set: { 
  "title":"Pulp Fiction",
  "year":1994,  
  "director":"Quentin Tarantino"  
  },
  {upsert: true}
)
```

### Eliminar Documentos
#### **deleteOne()**
``db.nombColec.deleteOne (filter,options)``
>Ejemplo:
```shell
db.pelisBasura.deleteOne( {_id: "tt0110912" } )
db.pelisBasura.deleteOne( {title: "Django Unchained" } )

# Con Operador
db.pelisBasura.deleteOne ( {year: {$gt:2000}} )
```

#### **deleteMany()**
``db.nombColec.deleteMany(filter,options)``
>Ejemplo:
```shell
db.pelisBasura.deleteMany( {director: "Quentin Tarantino"} )
db.pelisBasura.deleteOne ( {director: "Quentin Tarantino"} )

# Con Operadores
db.pelisBasura.deleteMany( {year: {$gt:2000}} )
```

## Operadores de consultas
### Operadores de Comparación
| Operador  | Descripción                                                                 | Ejemplo                                        | Operador en Signo   |
|-----------|-----------------------------------------------------------------------------|------------------------------------------------|---------------------|
| `$eq`     | Igual a                                                                     | `{ campo: { $eq: valor } }`                    | `=`                 |
| `$ne`     | No igual a                                                                  | `{ campo: { $ne: valor } }`                    | `!=`                |
| `$gt`     | Mayor que                                                                   | `{ campo: { $gt: valor } }`                    | `>`                 |
| `$gte$`   | Mayor o igual que                                                           | `{ campo: { $gte: valor } }`                   | `>=`                |
| `$lt`     | Menor que                                                                   | `{ campo: { $lt: valor } }`                    | `<`                 |
| `$lte`    | Menor o igual que                                                           | `{ campo: { $lte: valor } }`                   | `<=`                |
| `$in$`    | Pertenece específicos                                       | `{ campo: { $in: [ valor1, valor2, ... ] } }`  | `IN`                |
| `$nin$`   | No pertenece específicos                                    | `{ campo: { $nin: [ valor1, valor2, ... ] } }` | `NOT IN`            |

>**Ejemplo:** Muestra todas las películas que no contenga el rated: 'UNRATED', no mostrada id, solo, titulo y rated
```shell
db.movie.find( {rated: {$ne: 'UNRATED'}}, {_id: 0, title:1, rated: 1} )
```

```shell
# Muestra valores entre rango de mayo que 90
db.movie.find( {runtime: {$gt: 90}}, {_id: 0, title:1, runtime: 1} )
```

```shell
# Muestra valores entre rango de mayo que 90 y menor que 120
db.movie.find( {runtime: {$gt: 90, $lt: 120}}, {_id: 0, title:1, runtime: 1} )
```

```shell
# Muestra valores entre rango de mayo o igual 90 y menor o igual 120
db.movie.find( {runtime: {$gte: 90, $lte: 120}}, {_id: 0, title:1, runtime: 1} )
```

```shell
# Utilizar Operadores de comparación en varios campos
db.movie.find( 
    {runtime: {$gte: 180}, 'tomato.meter':{$gte:95}}, 
    {_id: 0, title:1, runtime: 1, 'tomato.meter':1} )
```

```shell
# Muestra los documentos que contenga del campo rated el valor: G o PG
db.movie.find( 
    {rated: {$in: ['G', 'PG'] }}, 
    {_id: 0, title:1, rated: 1} 
    )
```

```shell
# Muestra los documentos que no contenga del campo rated el valor: G o PG o PG-13
db.movie.find( 
    {rated: {$nin: ['G', 'PG', 'PG-13'] }}, 
    {_id: 0, title:1, rated: 1} 
    )
```

### Operadores de Elementos
- ``$exists`` coincide con documentos que tienen el campo especificado.
- ``$type`` selecciona documentos si un campo es del tipo de datos especificado.

`` $exists  -  { field: { $exists: boolean } } ``
- true :  documentos que contienen el campo (null)
- false:  documentos que no contienen el campo 

`` $type    -  { field: { $type: BSON type } ``

### Operadores de Lógicos
- ``$or`` une las cláusulas con un OR lógico
<br>
``{ $or: [ { selector1 }, { selector2 }, ... ] }``

- ``$nor`` une cláusulas de consulta con un NOR lógico 
<br>
``{ $nor: [ { selector1 }, { selector2 }, ... ] }``

 - ``$and ``une cláusulas de consulta con un AND lógico 
 <br>
``{ $and: [ { selector1 }, { selector2 }, ... ] }``

 - ``$not`` invierte el efecto de una expresión de consulta.
 <br>
``{ campo: { $not: { selector } } }``

![alt text](/img/tabla.png)

### Operadores de Vectores
- ``$all`` solo Documentos que contienen el campo vector con todos los valores
<br>
``{ campo: {$all: [valor1, valor2, ...] } }``
   - Pueden tener más valores, nunca menos
   - No tienen que estar en el mismo orden

 - ``$size`` solo Documentos que contienen el campo vector con el tamaño indicado.
 <br>
`` ({ campo: { $size: 2 } } )`` 
   - no acepta rangos de valores. 

- ``$elemMatch`` solo Documentos que contienen un elemento del campo vector que coincide con todas las condiciones especificadas.
<br>
``{ campo: { $elemMatch: { selector1 , selector2 , ... } } }``

>Ejemplos:

```shell
# $all
db.movie.find( 
    {countries:{$all: ['USA', 'SPAIN'] } },
    {_id:0, title:1, "title":1, countries:1}
)
```

```shell
# $size
db.movie.find( 
    {countries:{$size: 2}},
    {_id:0, title:1, "title":1, countries:1}
)
```

```shell
# $elemMatch
db.movies.find( {boxOffice: {$elemMatch: {"pais": "España", "ingreso": {$gt: 20}}}} )
```

### Operadores de Evaluación
- ``$regex`` selecciona documentos cuyos valores coinciden con una expresión regular especificada.

``{campo: { $regex: /pattern/ options } }``

``/ /`` *para delimitar la expresión regular* <br>
``^``   *significa comenzar desde el principio* <br>
``. ``  *comodín (cualquier carácter)* <br>
``* ``  *cualquier carácter varias veces* <br>

>Ejemplos:
```shell
db.movies.find(
    {"awards.text": { $regex: /^Won 1 Oscar.* / }},
    {_id: 0, title: 1, "awards.text": 1}
    )
```