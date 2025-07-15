# Ranking Garka API 🧐

Ranking Garka es una API con la finalidad de poder recopilar la mayoría de los "10 DE LA C\*NCHA' LA MADRE" que fueron trasmitidos en Radio Garka. <br>

> [!NOTE]
> Este proyecto está en constante evolución, y en el futuro se planea agregar nuevas funcionalidades que amplíen la experiencia y capacidades de la API.

<img src="./recursos/Ranking_Garka_API.jpg" alt="Logotipo de Ranking Garka API" width="250">

## Desarrollador 👨‍💻:

- **Desarrollador:** Matías Di Risio 👍
- **GitHub:** [DiriARG](https://github.com/DiriARG)

## Tabla de contenidos 📚:

- [Previo a iniciar](#previo-a-iniciar-)
- [Instalación](#instalación-)
- [Configuración de la Base de Datos](#configuración-de-la-base-de-datos-️)
- [Iniciando el proyecto](#iniciando-el-proyecto-)
- [Configuración del archivo .env (Environment Variables)](#configuración-del-archivo-env-environment-variables-%EF%B8%8F)
- [Estructura del proyecto](#estructura-del-proyecto-)
- [Descripción de archivos](#descripción-de-archivos-)
- [Inicialización del servidor](#inicialización-del-servidor-️)
- [Rutas de la API](#rutas-de-la-api-%EF%B8%8F)
- [Ejemplos de uso](#ejemplos-de-uso-)
- [Recursos](#recursos-)

## Previo a iniciar 🕒:

- **Descarga e instala** Visual Studio Code, el editor de código recomendado para abordar este proyecto.
- **Descarga e instala** Node.js, un entorno de ejecución de JavaScript de código abierto y multiplataforma que permite crear servidores, aplicaciones web, APIs, herramientas de línea de comandos y scripts. Asegúrate de seleccionar la versión LTS (Long Term Support) para garantizar la estabilidad.
- **Crea una cuenta** en MongoDB y **descarga e instala** Compass, que es una herramienta gráfica interactiva para consultar, optimizar y analizar datos en MongoDB.
- **Git Bash**: Si decides clonar el repositorio en lugar de descargar los archivos individualmente, asegúrate de tener **instalado** Git Bash en tu computadora.

## Instalación 📥:

1. **Fork** del repositorio: Haz un _fork_ del repositorio desde [este enlace](https://github.com/DiriARG/Ranking_Garka_API/fork).
2. **Clona** tu fork en tu máquina local:
> [!NOTE]
> No es necesario crear una carpeta manualmente para clonar el proyecto. Al ejecutar el siguiente comando, Git creará automáticamente una carpeta con el nombre del repositorio y descargará ahí todos los archivos.

- Navega hasta la ubicación donde deseas clonar el proyecto.
- Haz clic derecho en la carpeta y selecciona **"Open Git Bash here"** para abrir Git Bash en esa ubicación.
- Luego, ejecuta:

```bash
git clone https://github.com/tu-usuario/tu-repositorio-fork.git
```

3. Ahora **abre** Visual Studio Code y la carpeta correspondiente (Ranking_Garka_API).
4. **Inicia** una nueva terminal y escribe `npm install`, este comando en un directorio que ya contiene el archivo `package.json` genera que <u>npm</u> instale las dependencias especificadas en ese `package.json` y actualice el `package-lock.json` con las versiones exactas de esas dependencias.

> [!TIP]
> Si seguiste estas instrucciones de instalación mediante forkear el repositorio y clonandolo a tu máquina local, evita el apartado [Iniciando el proyecto](#iniciando-el-proyecto-), ya que esta orientado a las personas que simplemente han descargado algunos archivos individuales del proyecto.

## Configuración de la Base de Datos 🗄️:

1. **Crea** una nueva base de datos en MongoDB Compass:
   - Abre MongoDB Compass.
   - En el panel izquierdo, sobre la "connection string", haz click en **Create database**.
   - Dale un nombre significativo a tu base de datos, por ejemplo: `RankingGarka`.
   - Crea también una colección inicial llamada `trailerazos` o cualquier otro nombre que prefieras.
2. **Importa** los archivos JSON que se encuentran en la carpeta "datos_json":
   - Ve a la colección que acabas de crear.
   - Haz click en "ADD DATA" --> "Import JSON or CSV file" y selecciona el archivo correspondiente a esta colección, en este caso, "10_TRAILERAZOS.json".
   - Repite este proceso para cada archivo JSON que necesites importar, creando una nueva colección para cada archivo. Es recomendable nombrar cada colección en base a su contenido, por ejemplo: `trailerazos`, `guitarristas`, etc.
3. **Verifica** que las colecciones hayan sido creadas correctamente:
   - Una vez importados los archivos, revisa cada colección en MongoDB Compass para asegurarte de que los documentos JSON se hayan importado correctamente.
   - Asegúrate de que no haya duplicados ni problemas de formato en los documentos importados.

## Iniciando el proyecto 🚀:

Este apartado esta orientado a las personas que simplemente quieran descargar los archivos individualmente sin forkear el repositorio, por lo tanto, los archivos que son necesarios para el correcto funcionamiento de la API son los siguientes:

```plaintext
/src
  /config
    - base_de_datos.js
    - swagger_config.js
  /controladores
    - controlador_principal.js
    - controlador_ranking.js
    - controlador_secreto.js
  /datos_json
    - 10_ACTORAZOS.json
    - 10_ARTISTAS_SOBREVALORADOS.json
    ... (TODOS los otros archivos JSON restantes)
  /modelos
    - actorazos.js
    - artistas_sobrevalorados.js
    ... (TODOS los otros modelos restantes)
    - modelos_de_ranking.js
  /rutas
    - ruta_principal.js
    - ruta_secreta.js
    - rutas_ranking.js
  /tests
    - api.http
    - Ranking_Garka_API.postman_collection.json
/.env-copia
/app.js

```

> [!IMPORTANT]
> Antes de comenzar, **asegúrate** de haber completado la [Configuración de la Base de Datos](#configuración-de-la-base-de-datos-️). <br>

Si ya realizaste estos pasos y tienes la estructura del proyecto como se muestra arriba, puedes continuar con lo siguiente:

- Abre la terminal e inicializa un nuevo proyecto con `npm init -y`. Esto creará el archivo `package.json`.
> [!CAUTION]
> A partir de la versión `5.0.0` , esta API migra de **CommonJS** a **ES Modules (ECMAScript Modules)**.
> Para que funcione correctamente, asegurate de tener un entorno compatible con **Node.js 14 o superior** y de incluir la siguiente línea en tu ``package.json``: "type": "module"
- Luego, instala las dependencias necesarias: **Express JS** (entorno para desarrollar la API), **Mongoose** (biblioteca de modelado de objetos para MongoDB y Node.js), **Morgan** (middleware de registro de solicitudes HTTP), **swagger-jsdoc** (genera documentación de API a partir de comentarios JSDoc en el código) y **Swagger UI Express** (sirve una interfaz visual para interactuar con la documentación generada) con el siguiente comando:

```bash
   npm i express mongoose morgan swagger-jsdoc swagger-ui-express
```

Al instalar estos paquetes, se creará el archivo `package-lock.json` y la carpeta `node_modules`.

## Configuración del archivo .env (Environment Variables) ⚙️:

1. **Renombra** el archivo llamado `.env_copia` a `.env`, y luego **modifica** su contenido según tu entorno:
   - MONGODB_URLSTRING: Copiamos la cadena de conexión desde la pagina de MongoDB o propiamente desde el MongoDB Compass.
   - PUERTO: Escribimos el puerto que se va a usar para conectar a la API.
   - NOMBRE_BASE_DE_DATOS: Escribimos el nombre de la base de datos en la cual vamos a acceder.
2. **Configura las colecciones** correspondientes a los rankings que se importarán en MongoDB:
   - NOMBRESRANKINGS_COLLECTION = Escribe el nombre de la colección que contendrá todos los nombres de los rankings de la API.
   - CATEGORIASRANKINGS_COLLECTION = Indica el nombre de la colección que contendrá las diferentes categorías a las cuales pertenecen los rankings.
   - TRAILERAZOS_COLLECTION = Define el nombre de la colección que nos permitirá obtener los datos del ranking "TRAILERAZOS".
   - COMIDASDEGIRA_COLLECTION = Asigna el nombre de la colección correspondiente a "COMIDAS DE GIRA". <br>

Y así, de manera similar, configura todas las colecciones necesarias **para cada colección creada** en MongoDB.

## Estructura del proyecto 📂:

Esta es la estructura del proyecto en el editor de código fuente (en este caso, Visual Studio Code). Puede variar si los archivos se han descargado de forma individual.

```plaintext
/node_modules
  - (Contiene todos los módulos y bibliotecas necesarias para el proyecto)
/recursos
  - Ranking_Garka_API.jpg
  - Ranking_Garka.jpg
/src
  /config
    - base_de_datos.js
    - swagger_config.js
  /controladores
    - controlador_principal.js
    - controlador_ranking.js
    - controlador_secreto.js
  /datos_json
    - 10_ACTORAZOS.json
    - 10_ARTISTAS_SOBREVALORADOS.json
    ... (TODOS los otros archivos JSON restantes)
  /modelos
    - actorazos.js
    - artistas_sobrevalorados.js
    ... (TODOS los otros modelos restantes)
    - modelos_de_ranking.js
  /rutas
    - ruta_principal.js
    - ruta_secreta.js
    - rutas_ranking.js
  /tests
    - api.http
    - Ranking_Garka_API.postman_collection.json
/.env
/.gitignore
/app.js
/fechas_rankings.txt
/LICENSE
/package-lock.json
/package.json
/README.md

```

## Descripción de archivos 📄:

- **/node_modules**: Carpeta generada automáticamente al instalar las dependencias del proyecto. Contiene todos los módulos y bibliotecas necesarias para el funcionamiento de la aplicación.

- **/recursos**: Carpeta que centraliza y organiza elementos visuales del proyecto, como imágenes, además de otros posibles archivos de apoyo.

  - **Ranking_Garka_API.jpg**: Logotipo actual de la API, diseñado para reflejar la identidad actualizada de Ranking Garka, usado preferentemente en documentación y otros materiales.
  - **Ranking_Garka.jpg**: Primer logotipo de la API, representando la identidad visual inicial de Ranking Garka, conservado para registrar los cambios visuales de la API.

- **/src**: Carpeta principal que contiene el código fuente de la aplicación.

  - **/config**: Carpeta que contiene las configuraciones generales del proyecto.

    - **base_de_datos.js**: Archivo que establece y configura la conexión a la base de datos MongoDB usando Mongoose.
    - **swagger_config.js**: Archivo que configura Swagger para documentar la API.

  - **/controladores**: Carpeta que contiene la lógica de los controladores que manejan las diferentes rutas de la API.

    - **controlador_principal.js**: Controlador que maneja la ruta de bienvenida a la API, proporcionando información general sobre la misma.
    - **controlador_ranking.js**: Controlador que maneja todas las rutas relacionadas con los rankings, como obtener nombres de rankings y buscar el top de un ranking específico.
    - **controlador_secreto.js**: Controlador que maneja la ruta "secreta" como un easter egg, redirigiendo al usuario a un enlace oculto.

  - **/datos_json**: Carpeta que contiene los conjuntos de datos (datasets) en formato JSON.

    - **10_ACTORAZOS.json**: Archivo de formato JSON que contiene el ranking de "ACTORAZOS" que se utiliza en la base de datos.
    - **10_ARTISTAS_SOBREVALORADOS.json**: Archivo de formato JSON que contiene el ranking de "ARTISTAS SOBREVALORADOS" que se utiliza en la base de datos.
    - **... y otros archivos JSON** que representan diferentes rankings utilizados por la API.

  - **/modelos**: Carpeta que contiene los modelos Mongoose para cada ranking y el archivo "modelos_de_ranking.js".

    - **actorazos.js**: Archivo que define el esquema (schema) y el modelo (model) para los actores.
    - **artistas_sobrevalorados.js**: Archivo que define el esquema (schema) y el modelo (model) para las bandas y/o cantantes.
    - **y otros modelos** que representan distintos rankings en la API.
    - **modelos_de_ranking.js**: Archivo que contiene el mapeo dinámico de todos los modelos de los rankings utilizados por la API.

  - **/rutas**: Carpeta que contiene los archivos relacionados con las rutas de la API.

    - **ruta_principal.js**: Archivo que contiene la ruta de bienvenida a la API, proporcionando un mensaje informativo.
    - **ruta_secreta.js**: Archivo que contiene la ruta "secreta".
    - **rutas_ranking.js**: Archivo que contiene todas las rutas relacionadas con los rankings, definiendo los endpoints para consultar, buscar y obtener el top de los rankings.

  - **/tests**: Carpeta que contiene archivos para pruebas de las rutas de la API.
    - **api.http**: Archivo de la extensión "REST Client" para VS Code, utilizado para probar las solicitudes HTTP de la API.
    - **Ranking_Garka_API.postman_collection.json**: Colección de Postman que contiene ejemplos de las solicitudes a la API para facilitar pruebas y desarrollo.

- **.env**: Archivo que almacena las variables de entorno utilizadas en la configuración del proyecto, como la conexión a la base de datos y las colecciones de los rankings.

- **.gitignore**: Archivo que le indica a Git qué archivos o carpetas deben ser ignorados por el sistema de control de versiones.

- **app.js**: Archivo principal de la aplicación donde se inicializa el servidor y se configuran las rutas y los middlewares.

- **fechas_rankings.txt**: Archivo que contiene la información necesaria para ver los rankings del programa, ya sea a través de la app oficial del bana (Radio Garka) o, en algunos casos particulares, mediante enlaces de YouTube.

- **LICENSE**: Archivo que especifica los términos y condiciones bajo los cuales el software de este repositorio puede ser utilizado, copiado, modificado o distribuido por otras personas.

- **package-lock.json**: Archivo que asegura la reproducibilidad y consistencia de las instalaciones de paquetes en el proyecto con Node.js.

- **package.json**: Archivo de configuración de npm que describe el proyecto, incluyendo metadatos como nombre, versión, descripción, scripts, dependencias y más.

- **README.md**: Archivo guía para entender y comenzar a trabajar con este proyecto.

## Inicialización del Servidor 🖥️:

El archivo `app.js` es el punto de entrada de la aplicación y se encarga de inicializar el servidor, configurando las rutas y los middlewares necesarios para que la API funcione correctamente.

Para iniciar el servidor, puedes usar uno de los siguientes comandos en la terminal:

- **`npm run dev`**: Este comando inicia la aplicación en modo de desarrollo. Utiliza la opción `--watch`, lo que significa que el servidor se reiniciará automáticamente cada vez que realices cambios en el código. Esto es útil para el desarrollo, ya que no tendrás que reiniciar manualmente el servidor cada vez.

- **`npm start`**: Este comando inicia la aplicación en modo producción. Ejecuta `node app.js`, lo que inicia el servidor sin las características de reinicio automático. Es ideal para entornos en los que deseas que el servidor se ejecute de manera estable sin interrupciones.

- **`node app.js`**: Este comando también puede utilizarse para iniciar la aplicación directamente, funcionando igual que `npm start`, pero sin los scripts de npm.

- **`node --watch app.js`**: Similar a `npm run dev`, este comando inicia el servidor en modo de desarrollo y se reiniciará automáticamente al detectar cambios en el código.

> [!IMPORTANT]
> Asegúrate de haber configurado correctamente el archivo `.env` antes de iniciar el servidor, ya que contiene las variables de entorno necesarias para la conexión a la base de datos y otras configuraciones importantes.

## Rutas de la API 🛤️:

Para poder comprobar la funcionalidad de cada ruta de la API vamos a utilizar la extensión `REST Client` del marketplace de Visual Studio Code o cualquier otra herramienta que tenga como finalidad el testeo de una API, como puede ser `Postman`.

> [!TIP]
> Los links de descarga se encuentran en [Recursos](#recursos-).

Si prefieres utilizar **Postman**, en el proyecto se incluye un archivo dentro de la carpeta `/tests` llamado `Ranking_Garka_API.postman_collection.json`. **Importando este archivo en Postman**, tendrás acceso a todas las rutas de la API preconfiguradas para su fácil testeo. <br>
Además, este proyecto incluye la **documentación interactiva de la API** mediante `Swagger`, a la cual se puede acceder cuando la aplicación está corriendo, utilizando la ruta `/api-docs`. Después de ejecutar la aplicación, verás un mensaje en la terminal como este:

```bash
   Servidor escuchando en: http://localhost:<PORT>
   Documentación Swagger de la API en: http://localhost:<PORT>/api-docs
```

Dentro del archivo `api.http` (archivo funcional si utilizamos `REST Client`) se van a encontrar rutas con las siguientes finalidades:
| PETICIÓN | URL | DESCRIPCIÓN |
|:--------:|-----|-------------|
| GET | **/** | Ruta principal (Devuelve un mensaje de bienvenida y un poco de información sobre la API). |
| GET | **/nombres-rankings** | Ruta para devolver todos los nombres de los rankings disponibles. |
| GET | **/categorias** | Ruta para obtener todas las categorías de los rankings disponibles. |
| GET | **/ranking** | Ruta para buscar un ranking completo por su nombre (se debe incluir el parámetro `nombre` en la query string). |
| GET | **/ranking/:nombre/top** | Ruta para devolver el "top" de un ranking (No devuelve menciones honorificas). Se puede especificar un límite de resultados mediante un parámetro opcional `limite` en la query string (por defecto, se devuelve el top 5). |
| GET | **/secreto** | Ruta que redirige al usuario a un enlace oculto. Debido al tipo de contenido, es recomendable probarlo en un navegador (como Chrome o Firefox) ya que en herramientas como REST Client o Postman no se realizará la redirección correctamente para ver el contenido.

## Ejemplos de uso 🧪:

> [!NOTE]
> Estas acciones se realizan en el archivo `api.http`. Cabe aclarar que el puerto puede variar según su configuración; en este caso, se está utilizando el 3000: <br>

**GET**: **Entramos a la ruta principal**.

**Ejemplo de solicitud**:

```json

GET http://localhost:3000/

```

**Respuesta exitosa (200):** Mensaje de bienvenida y descripción de la API.

```json
{
  "mensaje": "Bienvenido a la API de Ranking Garka! 🍌",
  "descripcion": "Esta API te permite consultar los diferentes rankings '10 DE LA C*NCHA' LA MADRE' transmitidos en Radio Garka.",
  "rutas": {
    "/nombres-rankings": "Devuelve todos los nombres de rankings disponibles.",
    "/categorias": "Devuelve todas las categorías de los rankings disponibles",
    "/ranking?nombre={NOMBRE_DEL_RANKING}": "Busca un ranking específico por su nombre.",
    "/ranking/{NOMBRE_DEL_RANKING}/top": "Devuelve el top de un ranking especifico, por defecto devuelve el top 5.",
    "/secreto": "Redirige al usuario a un enlace oculto. Recomendable probarlo en un navegador."
  },
  "instrucciones": "Para obtener más información sobre el uso de la API, por favor revisa el archivo README.md"
}
```

**GET**: **Devolvemos todos los nombres de los rankings disponibles**.

**Ejemplo de solicitud**:

```json

GET http://localhost:3000/nombres-rankings
```

**Respuesta exitosa (200):** Lista de todos los nombres de rankings disponibles en formato JSON.

```json
[
  [
    "10 ACTORAZOS",
    "10 ARTISTAS SOBREVALORADOS",
    "10 BALADAS DEL ROCK",
    "10 CANCIONES CON IRA",
    "10 CANCIONES DE COCAINA",
    "10 CANCIONES DEDICADAS",
    "10 CANCIONES MARIHUANAS",
    "10 CANTANTES DE ROCK",
    "10 CERVEZAS",
    "10 CHUP4PIJ45",
    "10 COMEDIAS +18",
    "..."
  ]
]
```

**Posibles errores**: <br>
**Código 404**:

- **Descripción**: No se encontraron nombres de rankings.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontraron los nombres de los rankings 🕵️❗"
}
```

**Código 500**:

- **Descripción**: Error del servidor al obtener los nombres de los rankings.
- **Ejemplo de respuesta**:

```json
{
  "error": "Error del servidor al devolver todos los nombres de los rankings 🚫⚙️"
}
```

**GET**: **Devolvemos todas las categorías de los rankings disponibles**.

**Ejemplo de solicitud**:

```json

GET http://localhost:3000/categorias
```

**Respuesta exitosa (200):** Lista de categorías de rankings devuelta con éxito.

```json
[
  {
    "_id": "677ee136441d685c5ed32f4b",
    "musica": [
      "10 ARTISTAS SOBREVALORADOS",
      "10 BALADAS DEL ROCK",
      "10 CANCIONES CON IRA",
      "..."
    ],
    "cine_series_y_mas": [
      "10 ACTORAZOS",
      "10 COMEDIAS +18",
      "10 DOCUMENTALES",
      "..."
    ],
    "temas_generales": [
      "10 CERVEZAS",
      "10 COMIDAS DE GIRA",
      "10 DROGAS",
      "..."
    ],
    "misterios_y_conspiraciones": [
      "10 LEYENDAS URBANAS",
      "10 MITOS Y RUMORES",
      "10 TEORIAS CONSPIRATIVAS"
    ],
    "otros": ["10 CHUP4PIJ45", "10 ESPECIAL FAVORITOS", "10 TRAILERAZOS"]
  }
]
```

**Posibles errores**: <br>
**Código 404**:

- **Descripción**: No se encontraron las categorías de los rankings.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontraron categorías disponibles 🕵️❗"
}
```

**Código 500**:

- **Descripción**: Error del servidor al devolver todas las categorías de los rankings.
- **Ejemplo de respuesta**:

```json
{
  "error": "Error del servidor al devolver las categorías 🚫⚙️"
}
```

**GET**: **Buscamos un ranking completo por su nombre**.

Acá algunos ejemplos con los rankings "10 TRAILERAZOS", "10 COMIDAS DE GIRA" y "10 COMEDIAS +18":

**Ejemplos de solicitud**:

```json

GET http://localhost:3000/ranking/?nombre=10%20TRAILERAZOS

```

```json

GET http://localhost:3000/ranking/?nombre=10%20COMIDAS%20DE%20GIRA

```

```json

GET http://localhost:3000/ranking?nombre=10%20COMEDIAS%20%2B18

```

_Como podemos observar los espacios en una URL se codifican como "%20" y el signo "+" se codifica como "%2B"._

**Respuesta exitosa (200):** Ranking devuelto con éxito.

```json
[
  {
    "_id": "66fae767150b1877dbbc20d4",
    "numero": "10",
    "nombre": "SUPERMAN AMA A BATMAN",
    "año": 2018
  },
  {
    "_id": "66fae767150b1877dbbc20d5",
    "numero": "9",
    "nombre": "EL HOMBRE QUE ARAÑA - 'EL MULTIVERGAZO'",
    "año": 2021
  },
  {
    "_id": "66fae767150b1877dbbc20d6",
    "numero": "8",
    "nombre": "HARRY 'EL ALCOHOLICO' POTTER",
    "año": 2021
  },
  {
    "continúa": "..."
  }
]
```

**Posibles errores**: <br>
**Código 400**:

- **Descripción**: El parámetro "nombre" es obligatorio..
- **Ejemplo de respuesta**:

```json
{
  "error": "El parámetro 'nombre' es obligatorio ⚠️"
}
```

**Código 404**:

- **Descripción**: No se encontró el ranking con el nombre especificado.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontró el ranking llamado ${nombre} 🕵️❗"
}
```

**Código 404**:

- **Descripción**: El ranking especificado no contiene datos.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontraron datos para el ranking ${nombre} 🕵️❗"
}
```

**Código 500**:

- **Descripción**: Error interno del servidor al procesar la solicitud.
- **Ejemplo de respuesta**:

```json
{
  "error": "Error del servidor al devolver el ranking 🚫⚙️"
}
```

**GET**: **Devolvemos el "top" de un ranking. El usuario puede establecer el limite de registros a devolver que desee**. <br>

Para obtener el Top 5 (por defecto):

**Ejemplos de solicitud**:

```json

GET http://localhost:3000/ranking/10 TRAILERAZOS/top

```

```json

GET http://localhost:3000/ranking/10 COMIDAS DE GIRA/top

```

```json

GET http://localhost:3000/ranking/10 COMEDIAS +18/top

```

_En esta ruta no es necesario utilizar el "%20" para los espacios ni el "%2B" para el "+", simplemente escribimos correctamente el nombre del ranking._

**Respuesta exitosa (200):** Lista de los elementos del top especificado en formato JSON.

```json
[
  {
    "_id": "66fae767150b1877dbbc20de",
    "numero": "1",
    "nombre": "HARRY 'EL SUCIO' POTTER",
    "año": 2007
  },
  {
    "_id": "66fae767150b1877dbbc20dc",
    "numero": "2",
    "nombre": "JOHN SALCHICHON RAMBO",
    "año": 2008
  },
  {
    "_id": "66fae767150b1877dbbc20db",
    "numero": "3",
    "nombre": "EL HOMBRE QUE ARAÑA",
    "año": 2007
  },
  {
    "_id": "66fae767150b1877dbbc20da",
    "numero": "4",
    "nombre": "EL IMPOTENTE HULK",
    "año": 2009
  },
  {
    "_id": "66fae767150b1877dbbc20d9",
    "numero": "5",
    "nombre": "HARRY 'EL DROGADICTO' POTTER",
    "año": 2016
  }
]
```

Para obtener el Top 3:

**Ejemplos de solicitud**:

```json

GET http://localhost:3000/ranking/10 TRAILERAZOS/top?limite=3

```

```json

GET http://localhost:3000/ranking/10 COMIDAS DE GIRA/top?limite=3

```

```json

GET http://localhost:3000/ranking/10 COMEDIAS +18/top?limite=3

```

**Respuesta exitosa (200):** Utilizando el parámetro limite para establecer la cantidad de registros a traer, en este caso 3.

```json
[
  {
    "_id": "66fae767150b1877dbbc20de",
    "numero": "1",
    "nombre": "HARRY 'EL SUCIO' POTTER",
    "año": 2007
  },
  {
    "_id": "66fae767150b1877dbbc20dc",
    "numero": "2",
    "nombre": "JOHN SALCHICHON RAMBO",
    "año": 2008
  },
  {
    "_id": "66fae767150b1877dbbc20db",
    "numero": "3",
    "nombre": "EL HOMBRE QUE ARAÑA",
    "año": 2007
  }
]
```

**Posibles errores**: <br>
**Código 404**:

- **Descripción**: No se encontró el ranking especificado.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontró el ranking llamado ${nombre} 🕵️❗"
}
```

**Código 404**:

- **Descripción**: El ranking especificado no contiene datos.
- **Ejemplo de respuesta**:

```json
{
  "error": "No se encontraron datos del ranking ${nombre} 🕵️❗"
}
```

**Código 500**:

- **Descripción**: Error del servidor al intentar devolver el top del ranking.
- **Ejemplo de respuesta**:

```json
{
  "error": "Error del servidor al devolver el top del ranking 🚫⚙️"
}
```

**GET**: **Redirige al usuario a un enlace oculto**. <br>

> [!NOTE]
> Es recomendable probar la ruta `/secreto` en un navegador, ya que en herramientas como Postman o REST Client no se realizará la redirección correctamente y no se podrá acceder al contenido.

**Ejemplos de solicitud**:

```json

GET http://localhost:3000/secreto

```

**Respuesta exitosa (302):** Redirección a el enlace oculto.

## Recursos 🧰

Aquí encontrarás enlaces útiles para aprender más sobre las tecnologías utilizadas en este proyecto:

### Entorno de Desarrollo

- **Visual Studio Code**: [Visual Studio Code](https://code.visualstudio.com/) - Un editor de código fuente popular que ofrece extensiones útiles para desarrollo web.

### Control de Versiones

- **Git**: [Git](https://git-scm.com/) - Sistema de control de versiones distribuido utilizado para rastrear cambios en el código, colaboraciones y gestión de repositorios.

### Tecnologías de Backend

- **Node.js**: [Node.js](https://nodejs.org/) - Un entorno de ejecución para JavaScript en el lado del servidor.
- **Express**: [Express](https://expressjs.com/) - Un marco de aplicación web para Node.js, diseñado para construir aplicaciones y APIs web.
- **Morgan**: [Morgan](https://www.npmjs.com/package/morgan) - Middleware para registrar solicitudes HTTP en Node.js.

### Bases de Datos

- **MongoDB**: [MongoDB](https://www.mongodb.com/es) - Base de datos NoSQL orientada a documentos.
- **MongoDB Compass**: [MongoDB Compass](https://www.mongodb.com/products/tools/compass) - Herramienta de GUI para interactuar con bases de datos MongoDB.

### Modelado de Datos

- **Mongoose**: [Mongoose](https://mongoosejs.com/) - Biblioteca de modelado de objetos para MongoDB y Node.js.

### Herramientas de Prueba

- **REST Client**: [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) - Extensión de VS Code para probar APIs directamente desde el editor.
- **Postman**: [Postman](https://www.postman.com/) - Herramienta para realizar pruebas y desarrollo de APIs.
- **Swagger**: [Swagger](https://swagger.io/) - Conjunto de herramientas que permite diseñar, construir y documentar APIs. En este proyecto, utilizamos `swagger-jsdoc` para generar documentación a partir de comentarios en el código y `swagger-ui-express` para visualizar esta documentación en la aplicación.
