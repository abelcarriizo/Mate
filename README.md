![Titulo](img/title.png)

## 0. ANTES DE CONTINUAR...

Antes de avanzar, es crucial entender la estructura del repositorio.

- **/bibliografia**: Contiene recursos para profundizar en los conceptos presentados.

- **/database**: 

  - **/backup**: Copia de seguridad de la base de datos.
  
  - **/index**: Contiene consultas para utilizar índices en la base de datos.
  
  - **/performance**: Ofrece consultas para evaluar el rendimiento de cada colección, tanto antes como después de aplicar índices.

  - **/querys**:

    - **/create**: Incluye consultas y scripts en pymongo para crear las colecciones.

    - **/find**: Contiene consultas que extraen datos de las colecciones para su visualización.

  - **/schemas**: Contiene ideas sobre la estructura de la base de datos.

- **/figma**: Contiene archivos de Figma y PDF que presentan una previsualización del trabajo en Figma.

- **/img**: Almacena previsualizaciones de las vistas de la red social y ejemplos de rendimiento.

- **/teoria**: Contiene conceptos fundamentales sobre bases de datos NoSQL.

- **readme.md**: Este archivo.

### POBLAR LA BASE DE DATOS

Puedes poblar la base de datos utilizando las siguientes páginas:

1. [generatedata.com](https://generatedata.com/)
2. [faker.readthedocs.io](https://faker.readthedocs.io/en/master/)
3. [github.com/fzaninotto/Faker](https://github.com/fzaninotto/Faker)
4. [techtarget.com](https://www.techtarget.com/searchcio/definition/synthetic-data)
5. [mockaroo.com](https://mockaroo.com/)

**NOTA**: Algunas colecciones se crearon a partir de una ya poblada utilizando las páginas mencionadas anteriormente. Posteriormente, se utilizó pymongo para poblar el resto, siguiendo un proceso similar a ETL (Extract, Transform, Load).
Si estas interesado en utilizar la base de datos al final de este documento se explica como importarla.

### INSTALACIÓN DE PYMONGO

Antes de ejecutar el código, es fundamental instalar el módulo pymongo. Puedes hacerlo mediante el siguiente comando:

```bash
pip install pymongo
```

¡Claro! Aquí tienes un pequeño markdown para que puedas incluirlo en tu repositorio de GitHub:


## Respaldo con `mongodump`

1. Abre la terminal o línea de comandos.

2. Utiliza el siguiente comando para realizar un respaldo de la base de datos:
   ```bash
   mongodump --out /ruta/al/directorio/de/respaldo
   ```

## 1. INTRODUCCIÓN

Este documento describe el proceso de creación de la base de datos para "Mate", una red social inspirada en Threads. El proyecto tiene como objetivo proporcionar a los usuarios un espacio para compartir información y opiniones sobre temas de interés general, centrándose en la interacción con la base de datos.

## 2. DESCRIPCIÓN

La base de datos de Mate está diseñada para admitir las siguientes funcionalidades:
- **REGISTRO DE USUARIOS:** Los usuarios pueden registrarse proporcionando nombre, nombre de usuario, contraseña y correo electrónico.
- **EDITAR PERFIL:** Los usuarios pueden actualizar su información.
- **CREAR PUBLICACIONES:** Compartir pensamientos y opiniones.
- **COMENTARIOS:** Interactuar en las publicaciones de otros.
- **BÚSQUEDA DE USUARIOS:** Buscar por nombre de usuario, correo electrónico o intereses.
- **SEGUIR USUARIOS:** Seguir a otros usuarios para ver sus publicaciones.
- **RECIBIR NOTIFICACIONES:** Notificaciones sobre nuevas publicaciones, comentarios y mensajes privados.

## 3. OBJETIVOS

- Crear un espacio para la libre expresión e intercambio de ideas.
- Ofrecer una plataforma para que las personas compartan sus opiniones.

## 4. METODOLOGÍA

La base de datos de Mate se desarrolló utilizando MongoDB, un sistema de gestión de bases de datos no relacionales, elegido por su escalabilidad y flexibilidad.

## 5. ESTRUCTURA DE LA BASE DE DATOS

En esta sección, se presenta la estructura de las colecciones de la red social. Puedes consultar los esquemas en el [directorio database/schemas](./database/schemas). Si deseas conocer cómo se creó cada colección, puedes acceder al [directorio database/querys/create](./database/querys/create).

### USUARIOS
```json
{
  "_id": "ObjectId",
  "name": "nombre",
  "user_name": "username",
  "email": "name@email.com",
  "password": "password",
  "profile_picture": "ruta/a/imagen.jpg",
  "created_at": "ISODate('2023-10-26T21:30:00Z')"
}
```

### SEGUIDORES
```json
{
  "_id": "ObjectId",
  "user_id": "ObjectId",
  "follower_id": "ObjectId",
  "date": "ISODate('2023-10-26T21:30:00Z')"
}
```

### PUBLICACIONES
```json
{
  "_id": "ObjectId",
  "author": "ObjectId",
  "content": "Contenido de la publicación",
  "image": "ruta/a/imagen.jpg",
  "likes": ["user_id_1", "user_id_2"],
  "created_at": "ISODate('2023-10-26T21:30:00Z')",
  "updated_at": "ISODate('2023-10-26T21:30:00Z')",
  "comments": [
    {
      "_id": "ObjectId",
      "author": "ObjectId",
      "content": "Comentario 1",
      "image": "ruta/a/imagen.jpg",
      "likes": ["user_id_1", "user_id_2"],
      "created_at": "ISODate('2023-10-26T21:30:00Z')",
      "updated_at": "ISODate('2023-10-26T21:30:00Z')",
      "answers": [
        {
          "_id": "ObjectId",
          "author": "ObjectId",
          "content": "Comentario 1",
          "image": "ruta/a/imagen.jpg",
          "likes": ["user_id_1", "user_id_2"],
          "created_at": "ISODate('2023-10-26T21:30:00Z')",
          "updated_at": "ISODate('2023-10-26T21:30:00Z')"
        },
        {
          "_id": "ObjectId",
          "author": "ObjectId",
          "content": "Comentario 1",
          "image": "ruta/a/imagen.jpg",
          "likes": ["user_id_1", "user_id_2"],
          "created_at": "ISODate('2023-10-26T21:30:00Z')",
          "updated_at": "ISODate('2023-10-26T21:30:00Z')"
        }
      ]
    },
    {
      "_id": "ObjectId",
      "author": "ObjectId",
      "content": "Comentario 2",
      "image": "",
      "likes": [],
      "created_at": "ISODate('2023-10-26T21:30:00Z')",
      "updated_at": "ISODate('2023-10-26T21:30:00Z')",
      "comments": []
    }
  ]
}
```
Una publicacion tiene comentarios y estos comentarios pueden ser respondidos.

## 6. PREVISUALIZACIONES

A continuación, se presentan consultas sugeridas para cada vista. Además, puedes explorar algunas previsualizaciones construidas en Figma. Accede a ellas a través del [directorio /img](./img). Si deseas consultar las consultas, encontrarás los archivos en el [directorio database/querys/find/](./database/querys/find/).

![Previsualizacion de Mate](img/preview.png)

### INICIO DE SESIÓN
```javascript
db.users.findOne({
  "user_name": "username",
  "password": "password"
})
```

### REGISTRO DE USUARIOS
```javascript
db.users.insertOne({
  "name": "name",
  "user_name": "username",
  "email": "email@email.com",
  "password": "password",
  "profile_picture": "ruta/a/imagen.jpg",
  "created_at": new Date()
})
```

### PUBLICACIONES
```javascript
//Obtener las publicaciones segun su autor
db.posts.aggregate([
  {
    $match: { //Busca los usuarios en funcion de algun criterio
      author: ObjectId("653d33198da962044fa2337d")
    }
  },
  {
    $lookup: { //Union de dos documentos
      from: "users",
      localField: "author",
      foreignField: "_id",
      as: "author_info"
    }
  },
  {
    $unwind: "$author_info" //Divide un campo de matriz en varios documentos
  },
  {
    $project: { //Forma en la que se presentara la coleccion
      _id: 1,
      author_name: "$author_info.user_name",
      author_profile_picture: "$author_info.profile_picture",
      content: 1,
      created_at: 1,
      likesCount: { $size: "$likes" },
      commentsCount: { $size: "$comments" }
    }
  },
  {
    $sort: { created_at: -1 } // Ordenar por fecha de publicación, en este caso, de más reciente a más antigua
  },
])
```

### USUARIOS
Publicaciones realizadas por un usuario:
```json
db.users.aggregate([
  {
    $match: {
      _id: ObjectId("653d33198da962044fa2337a")
    }
  },
  {
    $lookup: {
      from: "followers",
      let: { userId: "$_id" },
      pipeline: [
        {
          $match: {
            $expr: { $eq: ["$user_id", "$$userId"] }
          }
        },
        {
          $count: "followersCount"
        }
      ],
      as: "seguidores"
    }
  },
  {
    $project: {
      _id: 0, // Excluye el campo "_id" del resultado
      user_name: 1,
      name: 1,
      followersCount: { $arrayElemAt: ["$seguidores.followersCount", 0] },
      profile_picture: 1
    }
  }
])
```

Comentarios realizados por el usuario a otras publicaciones:
```json
db.posts.aggregate([
  {
    $unwind: "$comments"
  },
  {
    $match: {
      "comments.author": ObjectId("653d33198da962044fa236ec")
    }
  },
  {
    $lookup: {
      from: "users",
      localField: "comments.author",
      foreignField: "_id",
      as: "commenter_info"
    }
  },
  {
    $unwind: "$commenter_info"
  },
  {
    $project: {
      _id: 1,
      author_name: "$commenter_info.user_name",
      author_profile_picture: "$commenter_info.profile_picture",
      content: "$comments.content", // El contenido del comentario
      created_at: "$comments.created_at", // La fecha de publicación del comentario
      likesCount: { $size: "$comments.likes" }, // Los "likes" del comentario
      answersCount: { $size: "$comments.answers" }, // La cantidad de comentarios del comentario
      parent_post: "$_id" // Esto indica que es una respuesta a una publicación de otro usuario
    }
  },
  {
    $sort: { created_at: -1 } // Ordena las respuestas por fecha de publicación, de más reciente a más antigua
  }
])
```

### NOTIFICACIONES
```json
{
  "_id": "ObjectId",
  "user_id": "ObjectId", 
  "sender_id": "ObjectId",
  "type": "nuevo_seguidor",
  "read": false,
  "message": "user te ha seguido",
  "created_at": "ISODate('2023-10-26T21:30:00Z')"
}
```

### BUSQUEDAS
```javascript
db.users.find({
  "user_name": "name"
})
```

### CONFIGURACIÓN
```javascript
db.users.update(
  { _id: ObjectId("653d33198da962044fa2337a") },
  {
    $set: {
      name: "name",
      user_name: "username",
      email: "e@email.com",
      profile_picture: "nueva/ruta/de/imagen.jpg",
    }
  }
)
```

### PUBLICAR
```javascript
db.users.find({
  "user_name": "name"
})
```

## 7. Importar Base de Datos

Cómo Respaldar y Restaurar una Base de Datos MongoDB

### Respaldo con `mongodump`

1. Abre la terminal o línea de comandos.

2. Utiliza el siguiente comando para realizar un respaldo de la base de datos:
   ```bash
   mongodump --out /ruta/al/directorio/de/respaldo
   ```

### Restauración con `mongorestore`

1. Abre la terminal o línea de comandos.

2. Utiliza el siguiente comando para restaurar la base de datos desde los datos respaldados:
   ```bash
   mongorestore /ruta/al/directorio/de/respaldo
   ```

### Importación desde un Archivo JSON o BSON

1. Abre la terminal o línea de comandos.

2. Utiliza el siguiente comando para importar datos desde un archivo JSON o BSON:
   ```bash
   mongoimport --db nombre_de_la_db --collection nombre_de_la_coleccion --file /ruta/al/archivo.json
   ```

Recuerda ajustar las rutas y nombres de archivos según tu configuración específica. Asegúrate de tener MongoDB instalado y en ejecución en tu sistema.

*Nota: Puedes encontrar más detalles y opciones en la documentación oficial de MongoDB para [mongodump](https://docs.mongodb.com/database-tools/mongodump/) y [mongorestore](https://docs.mongodb.com/database-tools/mongorestore/).*