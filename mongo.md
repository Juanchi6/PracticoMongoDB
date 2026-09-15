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

**Siguiente paso:** importar `data/notes.json` en la colección **notes** de la misma base y continuar con las consultas de la guía.
