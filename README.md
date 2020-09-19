# Comandos basicos de MongoDB

## Para correr mongo

- Iniciar el proceso con `mongod.exe` (en windows) o `brew services start mongodb-community` (en Mac)

- Terminar el proceso desde el Administrador de Tareas (en windows) o con `brew services stop mongodb-community` (en Mac)

- Iniciar la consola de mongo con `mongo.exe` (en Windows) o `mongo` (en Mac)

- Cerrar mongo con `quit()`

## Usando la consola de mongo

- Crear una base de datos nueva, o ir a una ya existente: `use nombre-de-la-db`

- Ver todas las bases de datos: `show dbs`

- Ver en que base de datos estamos: `db`

- Ver las colecciones en la base de datos: `show collections`

## Crear documentos

Usamos la coleccion *gatitos* como ejemplo. 

### insertOne

`db.gatitos.insertOne()` --> recibe como parametro un objeto de JS. Por ejemplo:

`db.gatitos.insertOne({ nombre: 'Trufa', color: 'gris', edad: 6})`


### insertMany

`db.gatitos.insertMany()` ---> recibe como parametro un array de objetos de JS. Por ejemplo:

`db.gatitos.insertMany([{nombre: 'Rita', color: ['tricolor', 'blanco', 'naranja', 'negro'], edad: 7}, {nombre: 'Mischa', color: 'atigrado', edad: 5}])`

## Buscar documentos

### Todos los documentos de una colección

`db.gatitos.find()`

### Filtrar documentos por una propiedad

- Que sea exactamente lo que buscamos: `db.gatitos.find({nombre: 'Trufa'})`

- Agregando un operador numeral: 

`db.gatitos.find({edad: {$lte: 2}})`

`db.gatitos.find({edad: {$lt: 2}})`

`db.gatitos.find({edad: {$gt: 2}})`

`db.gatitos.find({edad: {$gte: 2}})`

- Encadenando condiciones de busqueda ("AND")

`db.gatitos.find({ nombre: 'Rita', edad: {$gte: 2}})`

- Encadenando condiciones de busqueda ("OR") 

`db.gatitos.find( {$or: [ {nombre: 'Rital'},  {edad: {$gte: 1}}]})`

## Actualizar documentos

### updateOne

Un solo documento. Si hay mas de uno, el primero que se encuentre: 

`db.gatitos.updateOne()`

`db.gatitos.updateOne( {nombre: 'Trufa'}, { $set: {color: 'crema'}} )`

### updateMany

Todos los documentos que cumplan el criterio de busqueda: 

`db.gatitos.updateMany()`

`db.gatitos.updateMany( {edad: {$gte: 1}}, { $set: {adoptable: true}} )`

## Reemplazar documentos 

### replaceOne

`db.gatitos.replaceOne({nombre: 'Rita'}, { nombre: 'No Rita', edad: 99, colores: ['rosa', 'verde']})`

### replaceMany

`db.gatitos.replaceMany({edad: {$gte: 1}}, { nombre: 'No Rita', edad: 99, colores: ['rosa', 'verde']})`

## Borarr documentos 

### deleteOne

`db.gatitos.deleteOne()`

`db.gatitos.deleteOne( {nombre: 'Mischa'})`

### deleteMany 

Usar con precaución!

`db.gatitos.deleteMany()`

`db.gatitos.deleteMany({edad: {$gte: 1}})`


