# 📌 Comandos Básicos en MongoDB

## 🔹 1. Conectar a MongoDB
```sh
mongosh
```
Si estás en una versión antigua:  
```sh
mongo
```
Si necesitas conectarte a un servidor remoto:  
```sh
mongosh "mongodb+srv://usuario:contraseña@servidor.mongodb.net/"
```

---

## 🔹 2. Mostrar bases de datos disponibles
```sh
show dbs
```

---

## 🔹 3. Seleccionar (o crear) una base de datos
```sh
use nombre_de_la_base
```

---

## 🔹 4. Mostrar colecciones (tablas) en la base de datos actual
```sh
show collections
```

---

## 🔹 5. Crear una colección
```sh
db.createCollection("nombre_coleccion")
```

---

## 🔹 6. Insertar un documento (registro)
✅ **Un solo documento**  
```sh
db.nombre_coleccion.insertOne({nombre: "Juan", edad: 25, ciudad: "Lima"})
```
✅ **Varios documentos**  
```sh
db.nombre_coleccion.insertMany([
  {nombre: "Ana", edad: 30, ciudad: "Quito"},
  {nombre: "Carlos", edad: 28, ciudad: "Bogotá"}
])
```

---

## 🔹 7. Mostrar todos los documentos de una colección
```sh
db.nombre_coleccion.find()
```
📌 Para formatear la salida:  
```sh
db.nombre_coleccion.find().pretty()
```

---

## 🔹 8. Buscar documentos con filtros
🔍 **Buscar por un campo específico**  
```sh
db.nombre_coleccion.find({nombre: "Juan"})
```
🔍 **Buscar con operadores (ejemplo: edad mayor a 25)**  
```sh
db.nombre_coleccion.find({edad: {$gt: 25}})
```
🔍 **Buscar documentos donde la edad esté entre 20 y 30 años**  
```sh
db.nombre_coleccion.find({edad: {$gte: 20, $lte: 30}})
```
🔍 **Buscar documentos donde la ciudad NO sea "Lima"**  
```sh
db.nombre_coleccion.find({ciudad: {$ne: "Lima"}})
```
🔍 **Buscar documentos donde la ciudad sea "Lima" o "Quito"**  
```sh
db.nombre_coleccion.find({ciudad: {$in: ["Lima", "Quito"]}})
```
🔍 **Buscar documentos donde la ciudad NO sea "Lima" ni "Quito"**  
```sh
db.nombre_coleccion.find({ciudad: {$nin: ["Lima", "Quito"]}})
```
🔍 **Buscar documentos con un campo específico** (mostrar solo nombre y edad, ocultar el ID)
```sh
db.nombre_coleccion.find({}, {nombre: 1, edad: 1, _id: 0})
```
🔍 **Buscar con múltiples condiciones (AND lógico)**
```sh
db.nombre_coleccion.find({nombre: "Carlos", edad: 28})
```
🔍 **Buscar con OR lógico**
```sh
db.nombre_coleccion.find({$or: [{ciudad: "Lima"}, {edad: {$lt: 30}}]})
```

---

## 🔹 9. Documentos Incrustados (Embebidos)
MongoDB permite almacenar documentos dentro de otros documentos para representar relaciones anidadas.

✅ **Ejemplo de documento incrustado**
```sh
db.usuarios.insertOne({
  nombre: "Juan",
  edad: 25,
  direccion: {
    calle: "Av. Siempre Viva",
    ciudad: "Lima",
    pais: "Perú"
  }
})
```

🔍 **Buscar usuarios que viven en Lima**
```sh
db.usuarios.find({"direccion.ciudad": "Lima"})
```

🔄 **Actualizar el país de un usuario**
```sh
db.usuarios.updateOne(
  {nombre: "Juan"},
  {$set: {"direccion.pais": "Argentina"}}
)
```

🚀 **Agregar un nuevo campo dentro del documento incrustado**
```sh
db.usuarios.updateOne(
  {nombre: "Juan"},
  {$set: {"direccion.codigo_postal": "15001"}}
)
```

🗑 **Eliminar un campo dentro del documento incrustado**
```sh
db.usuarios.updateOne(
  {nombre: "Juan"},
  {$unset: {"direccion.codigo_postal": ""}}
)
```

---

## 🔹 10. Operadores en MongoDB
### 📌 Operadores de comparación
- `$eq` → Igual a
- `$ne` → Diferente de
- `$gt` → Mayor que
- `$gte` → Mayor o igual que
- `$lt` → Menor que
- `$lte` → Menor o igual que
- `$in` → En una lista de valores
- `$nin` → No en una lista de valores

Ejemplo:
```sh
db.nombre_coleccion.find({edad: {$gte: 25}})
```

### 📌 Operadores lógicos
- `$and` → AND lógico
- `$or` → OR lógico
- `$not` → Negación lógica
- `$nor` → Ninguna de las condiciones es verdadera

Ejemplo:
```sh
db.nombre_coleccion.find({$and: [{ciudad: "Lima"}, {edad: {$gt: 20}}]})
```
