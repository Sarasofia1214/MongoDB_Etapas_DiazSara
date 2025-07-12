## 🎯 Ejercicios Finales -- Sara Diaz

------

### 🧪 Taller

Realiza los siguientes ejercicios combinando múltiples etapas:

1. **Listar productos con más de 3 comentarios y cuyo precio supere $100**

```javascript
db.productos.aggregate([{ $match: { precio: { $gt: 100 } } },{ $match:{ $expr: {$gt: [{ $size: "$comentarios" }, 3] }}}])
```
2. **Buscar productos con nombre que comience con letra "A" o "P" usando REGEX**

```javascript
db.productos.find({ nombre: /^[AP]/i })

```
3. **Agrupar por categoría y obtener: cantidad, promedio de precio, y stock máximo**

```javascript
db.productos.aggregate([{ $group: {_id: "$categoria",cantidad: { $sum: 1 },promedio: { $avg: "$precio" },max: { $max: "$stock" }}}])
```

4. **Filtrar productos que tengan al menos un comentario con la palabra “recomendado” o “perfecto”**

```javascript
db.productos.find({"comentarios.comentario": /(recomendado|perfecto)/i })
```
5. **Mostrar los 5 usuarios con más comentarios hechos**

```javascript
db.productos.aggregate([ { $unwind: "$comentarios" },{ $group: { _id: "$comentarios.usuario", total: { $sum: 1 } } },{ $sort: { total: -1 } },{ $limit: 5 }])
```
