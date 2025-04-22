# Documentación de la API en PHP

## Estructura de la API
Esta API está diseñada para gestionar la información de estudiantes y profesores. A continuación se describen los principales archivos y clases:

### Clases y Archivos

- **estudiantes.class.php**: 
  - **Descripción**: Maneja la información de los estudiantes.
  - **Funciones**:
    - `listaEstudiantes($pagina)`: Recupera una lista de estudiantes paginada.
    - `nombreTrabajador($idtrabajador)`: Recupera el nombre de un trabajador específico.
    - `contarCuentasActivas()`: Cuenta el total de cuentas activas de estudiantes.
    - `obtenerEstudianteProfile($id)`: Recupera el perfil de un estudiante específico.
    - `listaEstudiantesActivosPorAño($ano)`: Recupera estudiantes activos por año.
    - `listaEstudiantesActivosPorCriterioYdevuelbeArrayDeIds($criterio)`: Recupera IDs de estudiantes activos que coinciden con un criterio de búsqueda.
    - `listaEstudiantesActivosPorCriterio($criterio)`: Recupera estudiantes activos que coinciden con un criterio de búsqueda.
    - `listaEstudiantesActivosPorIdes($ides)`: Recupera estudiantes activos por una lista de IDs.
    - `listaEstudiantesActivosTotales($pagina)`: Recupera todos los estudiantes activos.
    - `contarEstudiantesActivosPorAno()`: Cuenta estudiantes activos por año.
    - `listaAnos()`: Recupera la lista de años académicos.
    - `post($json)`: Maneja la creación y actualización de estudiantes.
    - `verificarAnoGrupo($grupo, $ano)`: Verifica si un grupo y año corresponden.
    - `actualizarPassword()`: Actualiza la contraseña de un estudiante.
    - `actualizarFoto($token, $idestudiante, $fotoBase64)`: Actualiza la foto de un estudiante.
    - `listaEstudiantesActivosPorCriterioYdevuelbeArrayDeIds($criterio)`: Recupera IDs de estudiantes activos que coinciden con un criterio de búsqueda.

- **profesores.class.php**: 
  - **Descripción**: Maneja la información de los profesores.
  - **Funciones**:
    - `listaProfesores($pagina)`: Recupera una lista de profesores paginada.
    - `nombreTrabajador($idtrabajador)`: Recupera el nombre de un trabajador específico.
    - `contarCuentasActivas()`: Cuenta el total de cuentas activas de profesores.
    - `obtenerProfesorProfile($id)`: Recupera el perfil de un profesor específico.
    - `post($json)`: Maneja la creación y actualización de profesores.
    - `actualizarEstado($token, $idtrabajador, $nuevoEstado)`: Actualiza el estado de un trabajador.
    - `actualizarAccesoGpp($token, $idtrabajador, $nuevoAccesoGpp)`: Actualiza el acceso GPP de un trabajador.
    - `listarTrabajadores($token)`: Lista todos los trabajadores.
    - `obtenerNombresDeGruposPorAno($ano)`: Recupera los nombres de grupos por año.
    - `getTrabajadorById($idtrabajador)`: Recupera los datos de un trabajador por su ID.
    - `crearTrabajador($token, $nombre, $departamento, $ano)`: Crea un nuevo trabajador.

- **auth.class.php**: 
  - **Descripción**: Maneja la autenticación de usuarios y la generación de tokens.
  - **Funciones**:
    - `login($json)`: Inicia sesión y genera un token para el usuario. Verifica el rol del usuario y valida las credenciales.
    - `exit($json)`: Cierra sesión invalidando el token.
    - `obtenerDatosUsuarioEstudiante($correo)`: Recupera los datos de un estudiante a partir de su correo electrónico.
    - `obtenerDatosProfesor($correo)`: Recupera los datos de un profesor a partir de su correo electrónico.
    - `insertarToken($usuarioid, $rol)`: Genera un nuevo token y lo inserta en la base de datos.
    - `inactivarToken($token)`: Cambia el estado de un token a "Inactivo".
    - `incrementarAcceso($id, $rol)`: Incrementa el contador de accesos de un usuario y actualiza la fecha de acceso.

- **seguridad.class.php**: 
  - **Descripción**: Se encarga de la seguridad de la API, incluyendo la verificación de tokens y el User-Agent.
  - **Funciones**:
    - `checkUserAgent()`: Verifica el User-Agent de la solicitud y redirige si no coincide.
    - `getEstudianteFromToken($token)`: Recupera los datos del estudiante asociado a un token activo.
    - `getTrabajadorFromToken($token)`: Recupera los datos del trabajador asociado a un token activo.
    - `AutorizarEstudianteCambiarSuPassword($token, $idEstudiante)`: Verifica si un estudiante tiene permiso para cambiar su contraseña.
    - `PermisoActualizarTrabajador($token, $idtrabajador)`: Verifica si un trabajador tiene permiso para actualizar los datos de otro trabajador.
    - `PermisoActualizarEstudiante($token, $idEstudiante)`: Verifica si un trabajador tiene permiso para actualizar los datos de un estudiante.
    - `PermisoActualizarCalificación($token, $idAsignatura, $grupo)`: Verifica si un trabajador tiene permiso para actualizar calificaciones.

- **respuestas.class.php**: 
  - **Descripción**: Estructura las respuestas que la API envía a los clientes.
  - **Funciones**:
    - `success($valor)`: Devuelve una respuesta de éxito con un mensaje personalizado.
    - `error_400($valor)`: Devuelve un error por datos incompletos.
    - `error_401($valor)`: Devuelve un error de no autorizado.
    - `error_403($valor)`: Devuelve un error de acceso prohibido.
    - `error_404($valor)`: Devuelve un error de no encontrado.
    - `error_500($valor)`: Devuelve un error interno del servidor.

- **token.class.php**: 
  - **Descripción**: Gestiona la creación, actualización y validación de tokens.
  - **Funciones**:
    - `actualizarTokens($horas_a_restar)`: Inactiva tokens que han expirado.
    - `getrecentusers($dias)`: Recupera usuarios recientes que han utilizado la API.
    - `crearTxt($direccion)`: Crea un archivo de texto para registrar las entradas de los registros.
    - `escribirEntrada($registros)`: Escribe una entrada en el archivo de registros cada vez que se actualizan los tokens.
    - `escribirTxt($direccion, $registros)`: Escribe un mensaje en el archivo de registros indicando cuántos registros se han modificado.

- **conexion/conexion.php**: 
  - **Descripción**: Maneja la conexión a la base de datos.
  - **Funciones**:
    - `__construct()`: Constructor que establece la conexión a la base de datos utilizando los datos de configuración.
    - `conectar()`: Establece la conexión a la base de datos y devuelve el objeto de conexión.
    - `obtenerDatos($query)`: Ejecuta una consulta y devuelve los datos obtenidos.
    - `nonQuery($query)`: Ejecuta una consulta que no devuelve datos (como INSERT, UPDATE, DELETE).
    - `datosConexion()`: Recupera los datos de conexión desde un archivo de configuración.
    - `convertirUTF8($array)`: Convierte un array a UTF-8.
    - `escapeString($str)`: Escapa cadenas para prevenir inyecciones SQL.
    - `ejecutarInsercion($sqlstr)`: Ejecuta una consulta de inserción y devuelve el resultado.
    - `obtenerDatosJoin($sqlstr)`: Ejecuta una consulta JOIN y devuelve los datos obtenidos.
    - `nonQueryBlob($sqlstr, $imagenBinaria, $idestudiante)`: Inserta un BLOB en la base de datos.
    - `nonQueryBlobTrabajador($sqlstr, $imagenBinaria, $idtrabajador)`: Inserta un BLOB para un trabajador en la base de datos.
    - `nonQueryBlobWithMIME($sqlstr, $imagenBinaria, $tipoMIME, $idestudiante)`: Inserta un BLOB con tipo MIME en la base de datos.
    - `nonQueryId($sqlstr)`: Ejecuta una consulta y devuelve el ID del último registro insertado.
    - `encriptar($string)`: Encripta una cadena utilizando MD5.

- **.htaccess**: 
  - **Descripción**: Archivo de configuración para el servidor web Apache. Se utiliza para controlar la configuración del servidor, como la reescritura de URLs y la protección de directorios.
  - **Funciones**:
    - Puede incluir reglas para redirigir solicitudes, proteger archivos sensibles y mejorar la seguridad de la API.

- **cron/actualizar_tokens.php**: 
  - **Descripción**: Script que se ejecuta periódicamente para actualizar el estado de los tokens en la base de datos.
  - **Funciones**:
    - Actualiza los tokens que han expirado y registra la actividad.

- **configuracion.php**: 
  - **Descripción**: Archivo de configuración que puede contener parámetros de conexión a la base de datos y otras configuraciones generales de la API.

- **actividades.php**: 
  - **Descripción**: Maneja las actividades relacionadas con los estudiantes y profesores.
  - **Funciones**:
    - `agregarActividad($json)`: Agrega una nueva actividad.
    - `editarActividad($id, $json)`: Edita una actividad existente.
    - `eliminarActividad($id)`: Elimina una actividad.
    - `listaActividadesPorCategoria($id_estudiante, $idcatevent, $pagina)`: Recupera actividades por categoría.
    - `listaActividades($id_estudiante)`: Recupera todas las actividades de un estudiante.
    - `obtenerActividad($id)`: Recupera una actividad específica.
    - `obtenerPuntajeEscalafonYposicionPorEstudiante($ano, $id)`: Recupera puntajes y posiciones de un estudiante.
    - `obtenerPuntajeEscalafon($id_estudiante_puntaje_escalafon, $ano)`: Recupera puntajes de escalafón.
    - `obtenerPuntajeEscalafonPorAno($ano)`: Recupera puntajes de escalafón por año.
    - `obtenerCreditos($id_estudiante_creditos)`: Recupera créditos de un estudiante.
    - `obtenerDestacadoPorEsferaPorAno($ano_destacados_esfera, $esfera)`: Recupera destacados por esfera y año.

- **calificaciones.php**: 
  - **Descripción**: Maneja las calificaciones de los estudiantes.
  - **Funciones**:
    - `listaCalificaciones($id_estudiante, $pagina)`: Recupera calificaciones de un estudiante.
    - `obtenerCalificacion($id)`: Recupera una calificación específica.
    - `obtenerPromedioAno($id_estudiante_promedio, $ano)`: Recupera el promedio de calificaciones de un estudiante por año.
    - `obtenerPromedioGeneral($id_estudiante_promedio)`: Recupera el promedio general de calificaciones de un estudiante.
    - `obtenerAusenciasTotales($id_estudiante_ausencias)`: Recupera el total de ausencias de un estudiante.

- **estudiantes.php**: 
  - **Descripción**: Maneja la información de los estudiantes.
  - **Funciones**:
    - `listaEstudiantes($pagina)`: Recupera una lista de estudiantes paginada.
    - `nombreTrabajador($idtrabajador)`: Recupera el nombre de un trabajador específico.
    - `contarCuentasActivas()`: Cuenta el total de cuentas activas de estudiantes.

- **profesores.php**: 
  - **Descripción**: Maneja la información de los profesores.
  - **Funciones**:
    - `listaProfesores($pagina)`: Recupera una lista de profesores paginada.
    - `nombreTrabajador($idtrabajador)`: Recupera el nombre de un trabajador específico.
    - `contarCuentasActivas()`: Cuenta el total de cuentas activas de profesores.

## Funcionamiento de la Seguridad
La API utiliza tokens para autenticar a los usuarios. Los tokens se generan al iniciar sesión y se almacenan en la base de datos. La API verifica el estado del token en cada solicitud. Si el token es inválido o ha expirado, se deniega el acceso.

### Verificación del User-Agent
La API verifica el User-Agent de la solicitud para asegurarse de que proviene de una fuente confiable. Si el User-Agent no coincide con el esperado, se redirige al usuario a la página de inicio.

## Base de Datos
La base de datos contiene las siguientes tablas relevantes:
- **usuarios_token**: Almacena los tokens generados para los usuarios, incluyendo su estado y fecha de creación.
- **estudiantes**: Contiene la información de los estudiantes, como nombre, estado y grupo.
- **trabajadores**: Contiene la información de los profesores, incluyendo permisos y asignaturas.

### Ejemplo de Estructura de Tablas
```sql
CREATE TABLE usuarios_token (
    TokenId INT AUTO_INCREMENT PRIMARY KEY,
    UsuarioId INT,
    Token VARCHAR(255),
    Estado ENUM('Activo', 'Inactivo'),
    Fecha DATETIME,
    Rol ENUM('Estudiante', 'Profesor')
);
```

## Realización de Solicitudes a la API
Las solicitudes a la API se realizan a través de JSON. A continuación se presentan ejemplos de cómo realizar solicitudes:

### Ejemplo de Login
```json
{
    "user": "usuario",
    "pin": "contraseña",
    "rol": "Estudiante"
}
```

### Ejemplo de Respuesta Exitosa
```json
{
    "status": "ok",
    "result": {
        "token": "4d9da913e4f11a717869b165ce7e8178",
        "id": "1",
        "name": "Juan Pérez",
        "foto": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
        "ano": "2023"
    }
}
```

## Uso del Token para Consultas Autenticadas

Para realizar consultas a la API que requieren autenticación, debes enviar el token recibido en el login en el header de la petición.

Ejemplo para listar estudiantes:

- Método: GET  
- URL: http://localhost/api-rest/estudiantes.php?page=1  
- Headers:  
  - User-Agent: DiGestion  
  - token: 4d9da913e4f11a717869b165ce7e8178  

## Ejemplos de Consultas GET

- Listar estudiantes paginados:

  GET http://localhost/api-rest/estudiantes.php?page=1

- Buscar nombre de trabajador por idtrabajador:

  GET http://localhost/api-rest/estudiantes.php?idtrabajador=5

- Contar cuentas activas:

  GET http://localhost/api-rest/estudiantes.php?contarCuentasActivas=1

## Ejemplos de Consultas POST, PUT y DELETE

- Crear estudiante (POST):

```json
{
  "token": "tu_token",
  "accion": "crear_estudiante",
  "nombre": "Nuevo Estudiante",
  "ci": "12345678",
  "grupo": "A",
  "ano": "2023",
  "modalidad": "Presencial",
  "sexo": "M",
  "celular": "5551234",
  "email": "nuevo@estudiante.com"
}
```

- Actualizar estudiante (PUT):

```json
{
  "token": "tu_token",
  "accion": "actualizar_todo",
  "idestudiante": 123,
  "nombre": "Nombre Actualizado",
  "grupo": "B"
}
```

- Eliminar estudiante (DELETE):

Headers:

- User-Agent: DiGestion  
- token: tu_token  
- idestudiante: 123  

O en Body JSON:

```json
{
  "token": "tu_token",
  "idestudiante": 123
}
```

## Interpretar Respuestas JSON

- Respuestas exitosas contienen `"status": "ok"` y un objeto `"result"` con los datos.
- En caso de error, se incluyen campos `"error_id"` y `"error_msg"`.
- El código HTTP indica éxito (200) o error (400, 401, 403, 500, etc.).

## Manejo de Errores Comunes

- Token inválido o caducado: haz login de nuevo para obtener un token válido.
- Campos faltantes o incorrectos: revisa el JSON enviado.
- Header User-Agent incorrecto o ausente: debe ser "DiGestion" para evitar redirecciones.

---
