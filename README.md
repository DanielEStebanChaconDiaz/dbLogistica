# Casos de Uso para Sistema de Envíos

## Casos de Uso Básicos

### Caso de Uso 1: Registrar un Nuevo País

comando mongoDB:

```javascript
db.paises.updateOne(  { nombre: { $regex: ".*\\S.*", $options: "i" } },  { $set: { nombre: "Mexico" } },  { upsert: true })
```

Descripción: Un administrador desea agregar un nuevo país a la base de datos.

Recomendaciones: El nombre del país no pude repetirse y por ende tampoco su id.

### Caso de Uso 2: Registrar una Nueva Ciudad

Descripción: Un administrador desea agregar una nueva ciudad asociada a un país existente.

Comando mongoDB:

```javascript
db.ciudades.updateOne(  { nombre: { $regex: ".*\\S.*", $options: "i" } },  { $set: { nombre: "Ciudad de Mexico" } },  { upsert: true })
```

Descripción 

### Caso de Uso 3: Registrar una Nueva Sucursal

Descripción: Un administrador desea agregar una nueva sucursal asociada a una ciudad existente.

``````javascript
db.sucursales.updateOne( { nombre: { $regex: ".*\\S.*", $options: "i" } },  { $set: { nombre: "Sucursal Centro" } },  { upsert: true })
``````



### Caso de Uso 4: Registrar un Nuevo Cliente

Descripción: Un administrador desea registrar un nuevo cliente en la base de datos.

``````javascript
db.clientes.updateOne(  { nombre: { $regex: ".*\\S.*", $options: "i" } },  { $set: { nombre: "Maria Gonzales" } },  { upsert: true })
``````



### Caso de Uso 5: Registrar un Nuevo Teléfono para un Cliente

Descripción: Un administrador desea agregar un número de teléfono para un cliente existente.

``````javascript
db.clientes.updateOne(
  { _id: ObjectId("cliente_id") },
  { $push: { telefonos: { numero: "1234567890" } } }
)
``````



### Caso de Uso 6: Registrar un Nuevo Paquete

Descripción: Un administrador desea registrar un nuevo paquete en la base de datos.

``````javascript
db.clientes.updateOne(  { numero_seguimiento: { $regex: ".*\\S.*", $options: "i" } },  { $set: { numero_seguimiento: "TRACK123456" } },  { upsert: true })
``````



### Caso de Uso 7: Registrar un Nuevo Envío

Descripción: Un administrador desea registrar un nuevo envío, asociando un cliente, paquete, ruta y sucursal.

``````javascript
db.envios.insertOne({
  cliente_id: ObjectId("cliente_id"),
  paquete_id: ObjectId("paquete_id"),
  fecha_envio: new Date(),
  destino: "Avenida Principal 456",
  ruta_id: ObjectId("ruta_id"),
  sucursal_id: ObjectId("sucursal_id"),
  seguimiento: [
    {
      ubicacion: "Sucursal de origen",
      fecha_hora: new Date(),
      estado: "Registrado"
    }
  ]
})
``````



### Caso de Uso 8: Registrar un Nuevo Vehículo

Descripción: Un administrador desea agregar un nuevo vehículo a la base de datos.

``````javascript
db.clientes.updateOne(  { placa: { $regex: ".*\\S.*", $options: "i" } },  { $set: { placa: "ABC123" } },  { upsert: true })
``````



### Caso de Uso 9: Registrar un Nuevo Conductor

Descripción: Un administrador desea agregar un nuevo conductor a la base de datos.

``````javascript
db.clientes.updateOne(  { nombre: { $regex: ".*\\S.*", $options: "i" } },  { $set: { nombre: "Maria Gonzales" } },  { upsert: true })
``````



### Caso de Uso 10: Registrar un Nuevo Teléfono para un Conductor

Descripción: Un administrador desea agregar un número de teléfono para un conductor existente.

```javascript
db.conductores.updateOne(
  { _id: ObjectId("conductor_id") },
  { $push: { telefonos: { numero: "0987654321" } } }
)
```



### Caso de Uso 11: Asignar un Conductor a una Ruta y un Vehículo

Descripción: Un administrador desea asignar un conductor a una ruta específica utilizando un vehículo.

```javascript

```



### Caso de Uso 12: Registrar un Nuevo Auxiliar

Descripción: Un administrador desea agregar un nuevo auxiliar de reparto a la base de datos.

```javascript

```



### Caso de Uso 13: Asignar un Auxiliar a una Ruta

Descripción: Un administrador desea asignar un auxiliar de reparto a una ruta específica.

```javascript

```



### Caso de Uso 14: Registrar un Evento de Seguimiento para un Paquete

Descripción: Un administrador desea registrar un evento de seguimiento para un paquete.

```javascript

```



### Caso de Uso 15: Generar un Reporte de Envíos por Cliente

Descripción: Un administrador desea generar un reporte de todos los envíos realizados por un cliente específico.

```javascript

```



### Caso de Uso 16: Actualizar el Estado de un Paquete

Descripción: Un administrador desea actualizar el estado de un paquete específico.

```javascript

```



### Caso de Uso 17: Rastrear la Ubicación Actual de un Paquete

Descripción: Un administrador desea rastrear la ubicación actual de un paquete específico.

```javascript

```



## Casos Multitabla

### Caso de Uso 1: Obtener Información Completa de Envíos

Descripción: Un administrador desea obtener la información completa de todos los envíos, incluyendo detalles del cliente, paquete, ruta, conductor, y sucursal.

```javascript

```



### Caso de Uso 2: Obtener Historial de Envíos de un Cliente

Descripción: Un administrador desea obtener el historial completo de envíos de un cliente específico, incluyendo detalles de los paquetes y los eventos de seguimiento.

```javascript

```



### Caso de Uso 3: Listar Conductores y sus Rutas Asignadas

Descripción: Un administrador desea obtener una lista de todos los conductores y las rutas a las que están asignados, incluyendo detalles del vehículo utilizado y la sucursal correspondiente.

```javascript

```



### Caso de Uso 4: Obtener Detalles de Rutas y Auxiliares Asignados

Descripción: Un administrador desea obtener detalles de todas las rutas, incluyendo los auxiliares asignados a cada ruta.

```javascript

```



### Caso de Uso 5: Generar Reporte de Paquetes por Sucursal y Estado

Descripción: Un administrador desea generar un reporte de todos los paquetes agrupados por sucursal y estado.

```javascript

```



### Caso de Uso 6: Obtener Información Completa de un Paquete y su Historial de Seguimiento

Descripción: Un administrador desea obtener la información completa de un paquete específico y su historial de seguimiento.

```javascript

```



## Casos de uso Between, In y Not In

### Caso de Uso 1: Obtener Paquetes Enviados Dentro de un Rango de Fechas

Descripción: Un administrador desea obtener todos los paquetes que fueron enviados dentro de un rango de fechas específico.

```javascript

```



### Caso de Uso 2: Obtener Paquetes con Ciertos Estados

Descripción: Un administrador desea obtener todos los paquetes que tienen ciertos estados específicos (por ejemplo, 'en tránsito' o 'entregado').

```javascript

```



### Caso de Uso 3: Obtener Paquetes Excluyendo Ciertos Estados

Descripción: Un administrador desea obtener todos los paquetes excluyendo aquellos que tienen ciertos estados específicos (por ejemplo, 'recibido' o 'retenido en aduana').

```javascript

```



### Caso de Uso 4: Obtener Clientes con Envíos Realizados Dentro de un Rango de Fechas

Descripción: Un administrador desea obtener todos los clientes que realizaron envíos dentro de un rango de fechas específico.

```javascript

```



### Caso de Uso 5: Obtener Conductores Disponibles que No Están Asignados a Ciertas Rutas

Descripción: Un administrador desea obtener todos los conductores que no están asignados a ciertas rutas específicas.

```javascript

```



### Caso de Uso 6: Obtener Información de Paquetes con Valor Declarado Dentro de un Rango Específico

Descripción: Un administrador desea obtener todos los paquetes cuyo valor declarado está dentro de un rango específico.

```javascript

```



### Caso de Uso 7: Obtener Auxiliares Asignados a Rutas Específicas

Descripción: Un administrador desea obtener todos los auxiliares de reparto que están asignados a ciertas rutas específicas.

```javascript

```



### Caso de Uso 8: Obtener Envíos a Destinos Excluyendo Ciertas Ciudades

Descripción: Un administrador desea obtener todos los envíos cuyos destinos no están en ciertas ciudades específicas.

```javascript

```



### Caso de Uso 9: Obtener Seguimientos de Paquetes en un Rango de Fechas

Descripción: Un administrador desea obtener todos los eventos de seguimiento de paquetes que ocurrieron dentro de un rango de fechas específico.

```javascript

```



### Caso de Uso 10: Obtener Clientes que Tienen Ciertos Tipos de Paquetes

Descripción: Un administrador desea obtener todos los clientes que tienen paquetes de ciertos tipos específicos (por ejemplo, 'nacional' o 'internacional').

```javascript

```

