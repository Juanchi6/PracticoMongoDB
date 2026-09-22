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


## 6. Livestream 1 – agregación con filtro y relación con notes

Siguiendo el bloque de agregaciones del Livestream 1, se ejecutó en **launchData.rocketData** un pipeline compuesto por tres etapas: `$match`, `$group` y `$lookup`.

Primero se filtraron los registros posteriores a la fecha indicada en el ejercicio; luego se agruparon por `meta.device` para contar sus lecturas y, finalmente, se relacionó cada grupo con la colección **notes** mediante el campo `device`.

La figura 6 muestra el resultado final del pipeline. Para **dlc** se obtienen **762 lecturas** y un arreglo de **44 notes**; para **truth**, **1.522 lecturas** y un arreglo de **81 notes**.

![Resultado del pipeline match group lookup](BIGDATA/Captura%20de%20pantalla%202026-09-21%20223002.png)

*Figura 6. Resultado final de la agregación con $match, $group y $lookup sobre rocketData.*


## 7. Livestream 1 – gráfica en MongoDB Charts

Se creó en MongoDB Charts una visualización de tipo **Continuous Line** utilizando la colección **launchData.rocketData**. El eje X utiliza el campo `time` y se representan tres series de velocidad: `truth_vel_CON_ECEF_ECEF_MpS1`, `truth_vel_CON_ECEF_ECEF_MpS2` y `truth_vel_CON_ECEF_ECEF_MpS3`.

La figura 7 muestra el dashboard con la gráfica **Truth Velocity** ya guardada y las tres series visibles.

![Gráfica Truth Velocity en MongoDB Charts](BIGDATA/Captura%20de%20pantalla%202026-09-21%20224300.png)

*Figura 7. Gráfica Truth Velocity creada en MongoDB Charts.*


## 8. Livestream 2 – Atlas Search sobre notes

Se creó el índice de búsqueda **default** sobre la colección **launchData.notes**, utilizando los campos `notes` y `title` definidos en el ejercicio. Luego se ejecutó en MongoDB Compass el pipeline de `simpleSearchQuery.js`, compuesto por `$search` y `$addFields`.

La etapa `$search` realiza la búsqueda sobre `notes` y `title`, mientras que `$addFields` incorpora el campo `score` con la relevancia calculada por Atlas Search.

La figura 8 muestra el resultado del pipeline sobre la colección **notes**, con documentos devueltos por la búsqueda y el campo `score` visible.

![Resultado de Atlas Search sobre notes](BIGDATA/Captura%20de%20pantalla%202026-09-21%20230128.png)

*Figura 8. Ejecución de simpleSearchQuery.js con $search y $addFields sobre launchData.notes.*


## 9. Livestream 2 – gráfica embebida en la aplicación

Como último paso del ejercicio, se habilitó el acceso no autenticado al gráfico **Truth Velocity** y se configuró la aplicación `embedChartFinal` con el **Base URL** y el **Chart ID** correspondientes al gráfico creado en MongoDB Charts.

La aplicación React se ejecutó localmente y cargó correctamente la visualización mediante el SDK de MongoDB Charts. La figura 9 muestra la aplicación en `localhost:3000` con el título **Embedded MongoDB Chart** y la gráfica **Truth Velocity** embebida con sus tres series visibles.

![Gráfica Truth Velocity embebida en la aplicación React](BIGDATA/Captura%20de%20pantalla%202026-09-21%20233534.png)

*Figura 9. Resultado final del ejercicio: gráfica de MongoDB Charts embebida en la aplicación React.*
