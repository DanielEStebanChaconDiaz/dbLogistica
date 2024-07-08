# Casos de Uso para Sistema de Envíos

## Casos de Uso Básicos

Entendido. Aquí están las consultas resueltas, manteniendo el formato original y evitando un tono artificial:

## Casos de Uso Básicos

### Caso de Uso 1: Registrar un Nuevo País

```javascript
db.paises.updateOne(
  { nombre: { $regex: ".*\\S.*", $options: "i" } },
  { $set: { nombre: "Mexico" } },
  { upsert: true }
)
```

Recomendaciones: Asegurar que el nombre del país sea único. Considerar agregar un campo para el código ISO del país.

### Caso de Uso 2: Registrar una Nueva Ciudad

```javascript
db.ciudades.updateOne(
  { nombre: { $regex: ".*\\S.*", $options: "i" } },
  { $set: { 
      nombre: "Ciudad de Mexico",
      pais_id: ObjectId("id_del_pais")
    }
  },
  { upsert: true }
)
```

Recomendaciones: Verificar que el país exista antes de crear la ciudad.

### Caso de Uso 3: Registrar una Nueva Sucursal

```javascript
db.sucursales.updateOne(
  { nombre: { $regex: ".*\\S.*", $options: "i" } },
  { $set: { 
      nombre: "Sucursal Centro",
      ciudad_id: ObjectId("id_de_la_ciudad"),
      direccion: "Dirección de la sucursal"
    }
  },
  { upsert: true }
)
```

Recomendaciones: Incluir la dirección completa de la sucursal.

### Caso de Uso 4: Registrar un Nuevo Cliente

```javascript
db.clientes.updateOne(
  { documento: "12345678" },
  { $set: { 
      nombre: "Maria Gonzales",
      documento: "12345678",
      direccion: "Dirección del cliente",
      email: "maria@ejemplo.com"
    }
  },
  { upsert: true }
)
```

Recomendaciones: Usar el documento de identidad como campo único.

### Caso de Uso 5: Registrar un Nuevo Teléfono para un Cliente

```javascript
db.clientes.updateOne(
  { _id: ObjectId("cliente_id") },
  { $push: { 
      telefonos: { 
        numero: "1234567890",
        tipo: "celular"
      } 
    } 
  }
)
```

Recomendaciones: Incluir un campo para el tipo de teléfono (celular o fijo).

### Caso de Uso 6: Registrar un Nuevo Paquete

```javascript
db.paquetes.updateOne(
  { numero_seguimiento: "TRACK123456" },
  { $set: { 
      numero_seguimiento: "TRACK123456",
      peso: 2.5,
      dimensiones: {
        largo: 30,
        ancho: 20,
        alto: 15
      },
      valor_declarado: 100.00,
      tipo: "nacional"
    }
  },
  { upsert: true }
)
```

Recomendaciones: Incluir campos para peso, dimensiones y valor declarado.

### Caso de Uso 7: Registrar un Nuevo Envío

```javascript
db.envios.insertOne({
  cliente_id: ObjectId("cliente_id"),
  paquete_id: ObjectId("paquete_id"),
  fecha_envio: new Date(),
  destino: {
    direccion: "Avenida Principal 456",
    ciudad_id: ObjectId("ciudad_id"),
    pais_id: ObjectId("pais_id")
  },
  ruta_id: ObjectId("ruta_id"),
  sucursal_origen_id: ObjectId("sucursal_id"),
  estado: "Registrado",
  seguimiento: [
    {
      ubicacion: "Sucursal de origen",
      fecha_hora: new Date(),
      estado: "Registrado"
    }
  ]
})
```

Recomendaciones: Estructurar la información de destino de manera detallada.

### Caso de Uso 8: Registrar un Nuevo Vehículo

```javascript
db.vehiculos.updateOne(
  { placa: "ABC123" },
  { $set: { 
      placa: "ABC123",
      tipo: "Camión",
      capacidad: 5000,
      modelo: "Modelo del vehículo",
      año: 2022
    }
  },
  { upsert: true }
)
```

Recomendaciones: Incluir campos para tipo, capacidad y modelo del vehículo.

### Caso de Uso 9: Registrar un Nuevo Conductor

```javascript
db.conductores.updateOne(
  { documento: "87654321" },
  { $set: { 
      nombre: "Juan Perez",
      documento: "87654321",
      licencia: "L12345678",
      fecha_nacimiento: new Date("1990-01-01"),
      fecha_contratacion: new Date()
    }
  },
  { upsert: true }
)
```

Recomendaciones: Incluir campos para licencia y fechas relevantes.

### Caso de Uso 10: Registrar un Nuevo Teléfono para un Conductor

```javascript
db.conductores.updateOne(
  { _id: ObjectId("conductor_id") },
  { $push: { 
      telefonos: { 
        numero: "0987654321",
        tipo: "celular"
      } 
    } 
  }
)
```

Recomendaciones: Similar al caso de uso 5 para clientes.

### Caso de Uso 11: Asignar un Conductor a una Ruta y un Vehículo

```javascript
db.asignaciones.insertOne({
  conductor_id: ObjectId("conductor_id"),
  ruta_id: ObjectId("ruta_id"),
  vehiculo_id: ObjectId("vehiculo_id"),
  fecha_inicio: new Date(),
  fecha_fin: null,
  estado: "Activo"
})
```

Recomendaciones: Usar una colección separada para asignaciones.

### Caso de Uso 12: Registrar un Nuevo Auxiliar

```javascript
db.auxiliares.updateOne(
  { documento: "98765432" },
  { $set: { 
      nombre: "Pedro Gomez",
      documento: "98765432",
      fecha_nacimiento: new Date("1995-05-05"),
      fecha_contratacion: new Date()
    }
  },
  { upsert: true }
)
```

Recomendaciones: Incluir campos similares a los del conductor.

### Caso de Uso 13: Asignar un Auxiliar a una Ruta

```javascript
db.asignaciones_auxiliares.insertOne({
  auxiliar_id: ObjectId("auxiliar_id"),
  ruta_id: ObjectId("ruta_id"),
  fecha_inicio: new Date(),
  fecha_fin: null,
  estado: "Activo"
})
```

Recomendaciones: Usar una colección separada para asignaciones de auxiliares.

### Caso de Uso 14: Registrar un Evento de Seguimiento para un Paquete

```javascript
db.envios.updateOne(
  { _id: ObjectId("envio_id") },
  { $push: { 
      seguimiento: {
        ubicacion: "Centro de distribución",
        fecha_hora: new Date(),
        estado: "En tránsito",
        descripcion: "El paquete ha llegado al centro de distribución"
      }
    }
  }
)
```

Recomendaciones: Incluir una descripción detallada del evento.

### Caso de Uso 15: Generar un Reporte de Envíos por Cliente

```javascript
db.envios.aggregate([
  { $match: { cliente_id: ObjectId("cliente_id") } },
  { $lookup: {
      from: "paquetes",
      localField: "paquete_id",
      foreignField: "_id",
      as: "paquete"
    }
  },
  { $unwind: "$paquete" },
  { $project: {
      fecha_envio: 1,
      destino: 1,
      estado: 1,
      "paquete.numero_seguimiento": 1,
      "paquete.peso": 1,
      "paquete.valor_declarado": 1
    }
  }
])
```

Recomendaciones: La presentación final del reporte debe manejarse en la capa de aplicación.

### Caso de Uso 16: Actualizar el Estado de un Paquete

```javascript
db.envios.updateOne(
  { _id: ObjectId("envio_id") },
  { $set: { estado: "Entregado" },
    $push: { 
      seguimiento: {
        ubicacion: "Dirección de destino",
        fecha_hora: new Date(),
        estado: "Entregado",
        descripcion: "El paquete ha sido entregado al destinatario"
      }
    }
  }
)
```

Recomendaciones: Mantener consistencia entre el estado general y el último evento.

### Caso de Uso 17: Rastrear la Ubicación Actual de un Paquete

```javascript
db.envios.findOne(
  { "paquete.numero_seguimiento": "TRACK123456" },
  { seguimiento: { $slice: -1 } }
)
```

Recomendaciones: Esta consulta devuelve el último evento de seguimiento.

## Casos Multitabla

### Caso de Uso 1: Obtener Información Completa de Envíos

```javascript
db.envios.aggregate([
  { $lookup: {
      from: "clientes",
      localField: "cliente_id",
      foreignField: "_id",
      as: "cliente"
    }
  },
  { $lookup: {
      from: "paquetes",
      localField: "paquete_id",
      foreignField: "_id",
      as: "paquete"
    }
  },
  { $lookup: {
      from: "rutas",
      localField: "ruta_id",
      foreignField: "_id",
      as: "ruta"
    }
  },
  { $unwind: "$cliente" },
  { $unwind: "$paquete" },
  { $unwind: "$ruta" },
  { $project: {
      "cliente.nombre": 1,
      "paquete.numero_seguimiento": 1,
      "ruta.nombre": 1,
      fecha_envio: 1,
      estado: 1
    }
  }
])
```

## Casos de uso Between, In y Not In

### Caso de Uso 1: Obtener Paquetes Enviados Dentro de un Rango de Fechas

```javascript
db.envios.find({
  fecha_envio: {
    $gte: ISODate("2023-01-01"),
    $lte: ISODate("2023-12-31")
  }
})
```

### Caso de Uso 2: Obtener Paquetes con Ciertos Estados

```javascript
db.envios.find({
  estado: { $in: ["en tránsito", "entregado"] }
})
```

### Caso de Uso 3: Obtener Paquetes Excluyendo Ciertos Estados

```javascript
db.envios.find({
  estado: { $nin: ["recibido", "retenido en aduana"] }
})
```

Nota: Algunas operaciones complejas podrían requerir procesamiento adicional en la capa de aplicación. Se recomienda crear índices en campos frecuentemente utilizados para optimizar el rendimiento.