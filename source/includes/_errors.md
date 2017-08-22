# Errores

<aside class="notice">En todos los casos se enviará un key <code>mensaje</code> con más detalles sobre el error.</aside>

La API Audi Evoluciona utiliza códigos HTTP para diferenciar los mótivos de error


Error Code | Descripción
---------- | -------
400 | Bad Request -- Error genérico conocido. En este caso se envía un JSON con un key `mensaje` mismo que podrá ser mostrado al usuario con un popup. Por ejemplo, si se intenta registrar un email que ya existe en la base. En teoría, el error no debería de ocurrir puesto que se valida pero en general, todas las peticiones deberán manejar el status 400 y mostrar al usuario el mensaje de error.
401 | Unauthorized -- El API SECRET no se reconoce.
403 | Forbidden -- El token de sesión no es válido.
404 | Not Found -- No se encontró la URL.
422 | Unprocessable Entity -- Formato de parámetros incorrecto.
500 | Internal Server Error -- Error inesperado del servidor. Reportar e intentar más tarde.

