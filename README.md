# Curso CoderHouse BackEnd

👋 Bienvenido/da

# Desafios

- Los desafios del Curso completados son los siguientes:

# Entrega Final

- Archivos en carpeta:
https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/

Usuarios creados para realizar Test:

    - role: admin
    - email: edusolis@yahoo.com.ar
    - password: 12345
    
    - role: user
    - email: eduardo@gmail.com
    - password: 12345

    - role: premium
    - email: ingedusolis@gmail.com
    - password: 12345


- Requerimientos:

    - Desde el router de /api/users, crear dos rutas:

        - GET: deberá obtener todos los usuarios, éste sólo debe devolver los datos principales como nombre, correo, tipo de cuenta (rol).

        - DELETE: deberá limpiar a todos los usuarios que no hayan tenido conexión en los últimos 2 días. (puedes hacer pruebas con los últimos 30 minutos, por ejemplo). Deberá enviarse un correo indicando al usuario que su cuenta ha sido eliminada por inactividad.
  
![ecommerceCoderHouse-AllUsers](https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/assets/72393640/fd885304-8dc5-481b-b8fc-2036d5d1d184)

-
    - Desde el router de /api/users, crear una vista para poder visualizar, modificar el rol y eliminar un usuario. Esta vista únicamente será accesible para el administrador del ecommerce

![ecommerceCoderHouse-Admin_Eliminar](https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/assets/72393640/bf366eff-dd29-4905-9233-17d1a3b75411)


![ecommerceCoderHouse-Admin_Modificar](https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/assets/72393640/1669dc69-f491-44df-9a77-75896081b99e)

-
    - Modificar el endpoint que elimina productos, para que, en caso de que el producto pertenezca a un usuario premium, le envíe un correo indicándole que el producto fue eliminado.

![ecommerceCoderHouse-Premium_EnviarMail](https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/assets/72393640/96707538-e45a-4411-b011-791d070ccf7a)

-
    - Finalizar las vistas pendientes para la realización de flujo completo de compra. NO ES NECESARIO tener una estructura específica de vistas, sólo las que tú consideres necesarias para poder llevar a cabo el proceso de compra.

![ecommerceCoderHouse-ProcesoCompra](https://github.com/IngLuissolis/ProyectoFinalCoderHouseBackEnd/assets/72393640/9b8a67ae-0811-4f4d-8efd-e5c6e913de65)

-
    - Realizar el despliegue de tu aplicativo en la plataforma de tu elección (Preferentemente Railway.app, pues es la abarcada en el curso) y corroborar que se puede llevar a cabo un proceso de compra completo.

        - link Railway: https://proyectofinalcoderhousebackend-production.up.railway.app/api/views

## Desafio Cuarta Practica Integradora

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora


Usuarios creados para realizar Test:

    - role: user

        - _id: 648b7fece5c1bba269de770f
        - password: 12345

    - role: premium

        - _id: 648b5b7b35f4b8ff1c5f8fc1
        - password: 12345

    - role: admin

        - _id: 648b8020e5c1bba269de7711
        - password: 12345

    ruta de Test petición POST para subir archivos con mulder:

        - http://localhost:3000/users/648b8020e5c1bba269de7711/documents

        Configuración:

            - Headers:
                - header: multipart/form-data
            - Body:
                - Files
                    - profileImage: profileImageTest.png
                    - document: DocumentTest.png
                    -productImage: CamisetasJpegTest.jpg

- Requerimientos:

    - Mover la ruta suelta /api/users/premium/:uid a un router específico para usuarios en /api/users/

        - Archivo de Implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/routes/usersPremium.router.js

            - Dicho archivo se llama desde https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/routes/users.router.js

    - Modificar el modelo de User para que cuente con una nueva propiedad “documents” el cual será un array que contenga los objetos con las siguientes propiedades:
            name: String (Nombre del documento).
            reference: String (link al documento).

    - Además, agregar una propiedad al usuario llamada “last_connection”, la cual deberá modificarse cada vez que el usuario realice un proceso de login y logout
        
        - Archivo de Implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/persistence/models/users.model.js

        - La modificación de "last_connection" se realizar en archivo 
            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/services/users.service.js

            cuando el usuario realiza proceso de login, falta implementar para proceso de logout.

    - Crear un endpoint en el router de usuarios users/:id/documents con el método POST que permita subir uno o múltiples archivos. Utilizar el middleware de Multer para poder recibir los documentos que se carguen y actualizar en el usuario su status para hacer saber que ya subió algún documento en particular.

        - Archivos de Implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/routes/users.router.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/middlewares/multer.middleware.js

        - Tener en cuenta que solo se puede cargar un archivo. Para subir mas archivos modificar variable maxCount en ruta:

            - router.post('/:id/documents', upload.fields([
    { name: 'document', maxCount: 1 },
    { name: 'profileImage', maxCount: 1 },
    { name: 'productImage', maxCount: 1 }
  ]), uploadDocumentsController);

  - El middleware de multer deberá estar modificado para que pueda guardar en diferentes carpetas los diferentes archivos que se suban. Si se sube una imagen de perfil, deberá guardarlo en una carpeta profiles, en caso de recibir la imagen de un producto, deberá guardarlo en una carpeta products, mientras que ahora al cargar un documento, multer los guardará en una carpeta documents.

    - Archivo de Implementación:

        - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/4taPracticaIntegradora/src/middlewares/multer.middleware.js

 - Modificar el endpoint /users/premium/:id para que sólo actualice al usuario a premium si ya ha cargado los siguientes documentos:
    - Identificación, Comprobante de domicilio, Comprobante de estado de cuenta.
    - En caso de llamar al endpoint, si no se ha terminado de cargar la documentación, devolver un error indicando que el usuario no ha terminado de procesar su documentación. (Sólo si quiere pasar de user a premium, no al revés)


        - No implementado, no se entiende requerimiento.

## Desafio Modulo Testing para Proyecto Final

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora

- Requerimientos:

    - Se deben incluir por lo menos 3 tests desarrollados para
        - Router de products.
        - Router de carts.
        - Router de users.
    
    - Archivo implementado:

        - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora/test/supertest.test.js

        - script: "npm test" (tener en cuenta que servidor se debe estar ejecutando en otro terminal (script: "npm start"))


## Desafio Documentar API

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora

- Requerimientos:

    - Realizar la configuración necesaria para tener documentado tu proyecto final a partir de Swagger.

        - ruta: http://localhost:3000/docs/

        - Archivos de Implementación en carpeta:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora/src/docs/routes
            - https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora/src/utils/swaggerSpecs.js

    - Se debe tener documentado el módulo de productos.
        - Archivo de Implementación en carpeta: 
        https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora/src/docs/routes/products/products.yaml

    - Se debe tener documentado el módulo de carrito
        - Archivo de Implementación en carpeta:
        https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora/src/docs/routes/products/carts.yaml

    - Consideraciones:
        - Tener en cuenta que para crear producto y acceder a ruta:
         router.post('/addProduct', authorize(['admin', 'premium']), createProductController);
         se requiere token de autorizacion, es decir, hay que logearse con email y password valido y tener rol admin o premium.
        - Lo mismo para rutas:
            - router.delete('/:id', authorize(['admin', 'premium']), deleteOneProductController);
            - router.put('/:id', authorize(['admin']),updateOneProductController);

## Desafio 3era Practica Integradora

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raPracticaIntegradora

- Requerimientos:

    - Realizar un sistema de recuperación de contraseña, la cual envíe por medio de un correo un botón que redireccione a una página para restablecer la contraseña (no recuperarla).

        - link del correo debe expirar después de 5 min de enviado.
        - Si se trata de restablecer la contraseña con la misma contraseña del usuario, debe impedirlo e indicarle que no se puede colocar la misma contraseña
        - Si el link expiró, debe redirigir a una vista que le permita generar nuevamente el correo de restablecimiento, el cual contará con una nueva duración de 5 min.

        - Archivos de implementación:
            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/utils/nodemailer.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/routes/messages.router.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/routes/views.router.js

            -  https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/controllers/views.controller.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/views/linkReestablecer.handlebars

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/routes/cambiarPassword.router.js

    - Establecer un nuevo rol para el schema del usuario llamado “premium” el cual estará habilitado también para crear productos:

        - Archivos de implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/persistence/models/users.model.js

    - Modificar el schema de producto para contar con un campo “owner”, el cual haga referencia a la persona que creó el producto
        - Si un producto se crea sin owner, se debe colocar por defecto “admin”.
        - El campo owner deberá guardar sólo el correo electrónico (o _id, lo dejamos a tu conveniencia) del usuario que lo haya creado (Sólo podrá recibir usuarios premium)

        - Archivos de implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/persistence/models/products.model.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/persistence/DAO/productsDAO/productsMongo.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/routes/products.router.js

    - Modificar los permisos de modificación y eliminación de productos para que:
        - Un usuario premium sólo pueda borrar los productos que le pertenecen.
        - El admin pueda borrar cualquier producto, aún si es de un owner.

        - Archivos de implementación: 

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/controllers/products.controller.js 
            (function deleteOneProductController)

    - Además, modificar la lógica de carrito para que un usuario premium NO pueda agregar a su carrito un producto que le pertenece. (No implentado)

    - Implementar una nueva ruta en el router de api/users, la cual será /api/users/premium/:uid la cual permitirá cambiar el rol de un usuario, de “user” a “premium” y viceversa.

        - Archivos de implementación:

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/routes/users.router.js

            - https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/3raPracticaIntegradora/src/controllers/users.controller.js
            (function changeRoleController)
        

## Desafio Implementación de Logger

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega

    - Se define un sistema de niveles que tenga la siguiente prioridad (de menor a mayor):
    debug, http, info, warning, error, fatal

    - Se implementa un logger para desarrollo y un logger para producción, el logger de desarrollo loggea a partir del nivel debug, sólo en consola

    - el logger del entorno productivo loggea sólo a partir de nivel info.

            - Archivo de implementación:
        https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/utils/winston.js

    - el logger envia en un transporte de archivos a partir del nivel de error en un nombre “errors.log”

            - Archivo 'errors.log' se guarda en carpeta: 
        https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/logs

    - Se agregan logs de valor alto en los puntos importantes del servidor (errores, advertencias, etc) y se modifican los console.log() habituales que tenemos para que se muestren todo a partir de winston.

    - Se Crea un endpoint /loggerTest que permite probar todos los logs.

            - Archivo de implementación: 
        https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/app.js


## Desafio Mocking y manejo de errores

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega

    - Se genera módulo de Mocking para el servidor, con el fin de que, al inicializarse pueda generar y entrega 100 productos con el mismo formato que entregaría una petición de Mongo. Endpoint (‘/mockingproducts’)

        - Archivo https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/services/mocking.router.js

    - Se genera un customizador de errores y crea un diccionario para los errores más comunes al crear un producto.

        - Archivo https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/test/checkRequiredFieldsProducts.test.js


    Archivo anterior se utiliza como middleware en endpoint '/products/addProducts' de: 
        - Archivo https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega/src/routes/products.router.js

## Desafio 3ra Entrega

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/3raEntrega

- Requerimientos:

    - Modificar nuestra capa de persistencia para aplicar los conceptos de Factory (opcional), DAO y DTO. (Cumplido - Sin Factory)
    - El DAO seleccionado (por un parámetro en línea de comandos como lo hicimos anteriormente) será devuelto por una Factory para que la capa de negocio opere con él. (Factory puede ser opcional) (Cumplido - Sin Factory)
    - Implementar el patrón Repository para trabajar con el DAO en la lógica de negocio. (Cumplido - Se utiliza Service)
    - Modificar la ruta  /current Para evitar enviar información sensible, enviar un DTO del usuario sólo con la información necesaria. (Cumplido - Se utiliza RTO)
    - Realizar un middleware que pueda trabajar en conjunto con la estrategia “current” para hacer un sistema de autorización y delimitar el acceso a dichos endpoints:
        - Sólo el administrador puede crear, actualizar y eliminar productos. (Cumplido - rol 'admin')
        - Sólo el usuario puede enviar mensajes al chat. (No Implementado)
        - Sólo el usuario puede agregar productos a su carrito. (No Implementado)
    - Crear un modelo Ticket el cual contará con todas las formalizaciones de la compra. (Cumplido)
    - Implementar, en el router de carts, la ruta /:cid/purchase, la cual permitirá finalizar el proceso de compra de dicho carrito.La compra debe corroborar el stock del producto al momento de finalizarse:
        - Si el producto tiene suficiente stock para la cantidad indicada en el producto del carrito, entonces restarlo del stock del producto y continuar. (Cumplido)
        - Si el producto no tiene suficiente stock para la cantidad indicada en el producto del carrito, entonces no agregar el producto al proceso de compra. (Cumplido)
        - Al final, utilizar el servicio de Tickets para poder generar un ticket con los datos de la compra. (Cumplido)
        - En caso de existir una compra no completada, devolver el arreglo con los ids de los productos que no pudieron procesarse. (Cumplido)
        - Una vez finalizada la compra, el carrito asociado al usuario que compró deberá contener sólo los productos que no pudieron comprarse. Es decir, se filtran los que sí se compraron y se quedan aquellos que no tenían disponibilidad. (Cumplido)

    Observaciones: Ahora cada vez que se logea un usuario, se crea un carrito y se guarda el _id dentro de user.cart.


## Desafio Arquitectura modelo de Capas

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/ArquitecturaCapas

- Requerimientos:

    - El proyecto debe contar con capas de routing, controlador, dao, con nuestras vistas bien separadas y con las responsabilidades correctamente delegadas.
    - Además, mover del proyecto todas las partes importantes y comprometedoras en un archivo .env para poder leerlo bajo variables de entorno en un archivo config.js

## Desafio Segunda Practica Integradora

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/SegundaEntrega

- Requerimientos:

    - Crear un modelo User el cual contará con los campos:
        - first_name:String,
        - last_name:String,
        - email:String (único)
        - age:Number,
        - password:String(Hash)
        - cart:Id con referencia a Carts
        - role:String(default:’user’)

    - Desarrollar las estrategias de Passport para que funcionen con este modelo de usuarios.

    - Modificar el sistema de login del usuario para poder trabajar con session o con jwt (a tu elección).

    - Agregar al router /api/sessions/ la ruta /current, la cual utilizará el modelo de sesión que estés utilizando, para poder devolver en una respuesta el usuario actual.

## Desafio Refactor a nuestro Login

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/SegundaEntrega

- Requerimientos:

    - Se deberá contar con un hasheo de contraseña utilizando bcrypt
    - Se deberá contar con una implementación de passport, tanto para register como para login.
    - Implementar el método de autenticación de GitHub a la vista de login.

    La implementación de los requerimientos se encuentra en archivo https://github.com/IngLuissolis/CoderHouseBackEnd/blob/main/ProyectoFinal/SegundaEntrega/src/passport/passportStrategies.js


## Desafio Login por Formulario

- Archivos en carpeta:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/SegundaEntrega

- Requerimientos:

    - Se genera registro en vista /login utilizando librerias passport, express-session y bcrypt.

    - Al realizar el login se redirecciona directamente a la vista de productos. Se agrega mensaje de bienvenida con datos del usuario.

    - Se agrega rol "administrador" para login email: "adminCoder@coder.com, password:"adminCod3r123".

    - Se implementa boton "logout" que destruye sesión y redirige a la vista login.



## Desafio Segunda pre-entrega Proyecto Final

- Archivos en carpeta:

https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/SegundaEntrega

- Requerimientos:

    - Se recibe por query params un limit (opcional), una page (opcional), un sort (asc / desc por precio) y un query (grupo)

        Devuelve un objeto con formato que se ve en ejemplo

        Ejemplo: petición GET http://localhost:3000/api/products?sort=desc&query=GrupoC&limit=2

    - Además, se agrega router de carts los siguientes endpoints:

        - DELETE http://localhost:3000/api/carts/:cid/products/:pid elimina del carrito el producto seleccionado.

        - PUT http://localhost:3000/api/carts/:cid actualiza el carrito con un arreglo de productos con el formato especificado arriba.

        - PUT http://localhost:3000/api/carts/:cid/products/:pid actualiza SÓLO la cantidad de ejemplares del producto por cualquier cantidad pasada desde req.body

        - DELETE http://localhost:3000/api/carts/:cid elimina todos los productos del carrito.

    - Se crea una vista en el router de views ‘/products’ (archivo products.handlebars) para visualizar todos los productos con su respectiva paginación. Cada producto mostrado puede resolverse de dos formas:

        - Se crea nueva vista con el producto seleccionado con su descripción completa, detalles de precio, categoría, etc. Además de un botón para agregar al carrito.

        - Contar con el botón de “agregar al carrito” directamente, sin necesidad de abrir una página adicional con los detalles del producto.

        - Además, agregar una vista en ‘/carts/:cid (archivo carts.handlebars) para visualizar un carrito específico, donde se deberán listar SOLO los productos que pertenezcan a dicho carrito. Se agrega boton eliminar al lado de cada producto, se elimina de un producto en uno en el caso de tener mas de un producto. 

## Desafio Primera Practica Integradora

- Archivos en carpeta:

https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/Desafios/DesafioPrimeraPracticaIntegradora

- MongoDB:

    - Se crea en Atlas DataBase ecommerceCoderHouse
        - Collections:
            - products
            - carts
            - messages

    - Se separa los Managers de fileSystem de los Managers de MongoDB en carpeta dao.

    - Se codifica estructura models donde se guardan los esquemas de MongoDB

    - En collection "carts" se guarda "_id" y "quantity" de product. "quantity" se incrementa en 1 cada vez que se guarda mismo _id de product.

- Chat Handlebars:

    - ruta: http://localhost:3000/chat

    - Los mensajes se guardan en MongoDB, estructura "user" y "message"

    - Los mensajes se pueden visualizar con una petición GET con la siguiente estructura:
        -       GetAllMessages: ruta: http://localhost:3000/viewsMessages/
        -       getMessageById: ruta: http://localhost:3000/viewsMessages//id


- Corrección Desafio WebSocket

    - Se corrigue eliminación de productos, anteriormente se eliminaban y no se volvian a enlistar a partir de ahi.
    Faltaba la instrucción:
    products = JSON.parse(fs.readFileSync(productsFilePath));


## Desafio WebSocket

- Archivos en carpeta:

https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/Desafios/DesafioWebSocket

- Handlebars: se generaron los archivos
    - src/views/home.handlebars: En navegador se encuentra en direccion web http://localhost:8080/
    - src/views/realTimeProducts.handlebars: En navegador se encuentra en direccion web http://localhost:8080/realtimeproducts .
    En dicha pagina se puede agregar o eliminar producto, utilizando websocket.

- Archivo src/server.js
    - se agrego configuración de websocket para interactuar con archivo public/js/index.js del lado del frontEnd

## Desafio Primera Entrega
-Archivos en carpeta:

https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/PrimeraEntrega

- Archivo server.js:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/PrimeraEntrega/src/server.js

- Archivo products.router.js:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/PrimeraEntrega/src/routes/products.router.js

- Archivo carts.router.js:
https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/ProyectoFinal/PrimeraEntrega/src/routes/carts.router.js

- Se utiliza archivo adicional utils.js para generar ruta relativa


### Desafio 03 - Servidor con Express
    - Archivos en carpeta 
    https://github.com/IngLuissolis/CoderHouseBackEnd/tree/main/Desafios/Desafio03ServidorConExpress/src
        -- /app.js
        -- /ProductManager.js
        -- /products.json

### Desafio 02 - Manejo de Archivos
    - Archivo: Desafios/Desafio02ProductManager.js
    - Archivo Forma Asincronica: Desafio/Desafio02ProductManagerAsync.js

### Desafio 01 - Clases ECMAScript y ECMAScript avanzado
    - Archivo: Desafios/Desafio01ECMAScript.js

# Descripción del Proyecto:

Proyecto para la venta de camisetas de los paises que jugaron el campeonato mundial de futbol Qatar 2022 desarrollado con tecnologia React (frontEnd)

# Estado del Proyecto

- Completar

# Tecnologias utilizadas

- express

# Librerias utilizadas

- Completar

# Customer Homepage

Animación Gif ecommerce

# Firebase - collection orders

Imagen CartContainer

# Sitio Deployed



# Feedback

Any suggestion and feedback is welcome. You can message me on email

`edusolis@yahoo.com.ar`
