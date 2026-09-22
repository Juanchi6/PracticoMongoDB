# Práctico de MongoDB: Rocket Space

Registro del trabajo realizado siguiendo la guía `MongoDBRocketSpace.docx`. Los archivos de datos y las consultas de referencia pertenecen al [repositorio rocketLivestream](https://github.com/jayrunkel/rocketLivestream).

## 1. Creación del clúster en Atlas

Se creó el clúster **Aerospace** en MongoDB Atlas con el plan gratuito indicado en la guía. La figura 1 muestra el clúster disponible, todavía sin datos cargados.

![Clúster Aerospace creado en MongoDB Atlas](BIGDATA/Captura%20de%20pantalla%202026-09-15%20200924.png)

*Figura 1. Clúster Aerospace en MongoDB Atlas.*

## 2. Conexión desde MongoDB Compass

Se configuraron el usuario de base de datos y el acceso desde la IP del equipo. Luego se utilizó la cadena de conexión de Atlas para acceder desde MongoDB Compass. El mensaje **Connected to Aerospace** de la figura 2 confirma que la conexión se estableció correctamente.

![MongoDB Compass conectado a Aerospace](BIGDATA/Captura%20de%20pantalla%202026-09-15%20201148.png)

*Figura 2. Conexión exitosa desde Compass.*

## 3. Importación de los datos del cohete

Se creó la base **launchData** con la colección **rocketData**. Desde **Add Data → Import JSON or CSV file**, se importó el archivo `data/rocketData.json` del repositorio del práctico.

La importación finalizó con **120.791 documentos**, como muestra el aviso de la figura 3. También se observan los documentos almacenados, con campos de tiempo y mediciones del cohete.

![Importación de 120791 documentos en launchData.rocketData](BIGDATA/Captura%20de%20pantalla%202026-09-15%20205023.png)

*Figura 3. Importación de rocketData completada.*

## 4. Importación de la colección notes

Se incorporó la colección **notes** dentro de la misma base **launchData**. La figura 4 registra la colección ya disponible junto con los datos cargados previamente en **rocketData**.

![Colección notes importada en launchData](BIGDATA/Captura%20de%20pantalla%202026-09-15%20205542.png)

*Figura 4. Colección notes disponible en la base launchData.*

## 5. Livestream 1 – revisión de datos con consultas simples

Como evidencia representativa del uso de `simpleQueries.js`, se ejecutó en MongoDB Compass el filtro:

```json
{"meta.device": "truth"}
```

La figura 5 muestra la consulta sobre **Aerospace → launchData → rocketData** y el resultado obtenido: **79.998 documentos**. En los registros visibles aparecen el campo `time` y mediciones asociadas al dispositivo `truth`.

![Consulta de documentos del dispositivo truth](BIGDATA/Captura%20de%20pantalla%202026-09-21%20214554.png)

*Figura 5. Consulta de rocketData filtrada por meta.device = "truth".*


## 6. Livestream 1 – agregación por dispositivo

Siguiendo el bloque de agregaciones del Livestream 1, se ejecutó en **launchData.rocketData** un pipeline con `$group` para agrupar los documentos por el campo `meta.device` y contar la cantidad de lecturas de cada dispositivo.

```javascript
{
  _id: "$meta.device",
  readingsCount: {
    $count: {}
  }
}
```

La figura 6 muestra el resultado completo de la agregación: **dlc = 40.001**, **lidar = 792** y **truth = 79.998**.

![Agregación de lecturas por dispositivo](BIGDATA/Captura%20de%20pantalla%202026-09-21%20222200.png)

*Figura 6. Resultado del agrupamiento de rocketData por meta.device.*
