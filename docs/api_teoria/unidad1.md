# UNIDAD 1

## COMPONENTES DE UN API REST

- **Endpoints (Punto de acceso):**  Es la combinación de una URL específica (ruta) y un método HTTP (verbo).
  - Ej: POST /api/users (Crear un usuario)

- **Router:** Mecanismo que recibe las peticiones entrantes y derivar el flujo hacia el controlador correspondiente.
  - Ej: Derivar el `POST /user` a la función `createUser()`

- **Middlewares:** Se ejecuta antes de que la petición llegue al controlador o después de generar la respuesta.
  Actua como un filtro o capas de seguridad, al formase una cadena de capas se llama **Pipeline**
  - Autenticación/Autorización: Verifica si el usuario esta logueado y tiene permisos para esa acción.
  - Logging: Registra la petición entrante.
  - Manejo de errores: Capturar fallos en los controladores y devolver una repsuesta JSON informando del error.
  - Edición de respuestas: Intercepta respuestas del controlador para modificar la respuesta.

- **Controllers:** Contiene la lógica de control para procesar una petición y generar una respuesta HTTP.
    1. Recibe datos de la petición (del cuerpo del JSON)
    2. Utiliza **DTOs** para validar el JSON recibido y estructurar los datos entrantes
    3. Llama y recibe un resultado de la capa lógica.
    4. Utiliza **Serializers** para formatear el resultado JSON y contruir la respuesta HTTP

- **Acceso a datos de la base de datos (Persistencia):** Capa encargada de interactuar con la Base de Datos (guardar,leer...)

### EJEMPLO TÉCNICO

1. Frontend envia una petición HTTP `POST /users`
2. La petición llega al servidor (Backend/API)
3. Pasa por el **pipeline**
4. Llega al Router y es derivado a la función `create()` del controlador  (`UserController`).
5. En el controlador se mapea el JSON a un DTO (`CreateUserDTO`) validando los datos
    y se llama servicio de usuarios (UserService.register(dto)) que recibe el DTO.
6. Se ejecuta el servicio y se guarda en la Base de Datos.
7. El servicio devuelve un objeto usuario, en el controlador el Serializer (`UserSerializer`)
   convierte el objeto usuario en un JSON y el controlador crea la repuesta HTTP.
8. La respuesta pasa por los middlewares (en caso de ser necesario) y se envia al cliente (Frontend)

Crear diagrama

## CONCEPTOS DE PROGRAMACIÓN
