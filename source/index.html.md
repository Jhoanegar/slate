---
title: API Audi Evoluciona

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='http://rokode.com'>Proyecto de Rokode</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Versiones

## Versión 9
6 de septiembre, 2017

* Se vuelve opcional el `idUsuario` en endpoint de [historial](#historial) y se agrega el parámetro opcional `idChat`. [Ver más](#historial)


## Versión 8
4 de septiembre, 2017

* Añade el endpoint de [nueva-imagen](#nueva-imagen)

## Versión 7
30 de agosto, 2017

* Se añadió el parémetro de respuesta `esSuperChat` al endpoint e [chats activos](#chats-activos)
* Ahora el endpoint de `login` y `validarCodigo` devuelven un estatus `400` en lugar de `401` para que caiga en el caso de error que se muestra al usuario mediante un popup como lo indica la sección de [errores](#errores)
* Añade [feed de noticias](#feed-de-noticias)
* Por seguridad, los endpoints de [developer](#developer) ahora requieren el mismo api token que la app.
* Añade endpoint de [enviar push](#enviar-push)

**UPDATE 1**

* Se vuelve opcional el `idUsuario` en endpoint de [enviar mensaje](#enviar-mensaje) y se agrega el parámetro opcional `idChat`. [Ver más](#enviar-mensaje)

## Versión 6

29 de agosto (2), 2017


* Se añadió el parámetro de respuesta `idChat` a la respuesta de [chats activos](#chats-activos)
* Se añadió el parámetro de respuesta `idChat` a la respuesta de [enviar mensaje](#enviar-mensaje)
* Se añadió el parámetro de respuesta `idChat` a la respuesta de [historial](#historial)
* Ahora se requiere el parámetro `idChat` en el endpoint de [ultimo-visto](#ultimoVisto), el parámetro `idUsuario` ya no se requiere
* Se añadió endpoints de developer


## Versión 5
29 de agosto (1), 2017

* Se añadió endpoint de [ultimo visto](#ultimo-visto)
* Se añadió endpoint de [actualizar perfil](#actualizar-perfil)
* Se añadió el parámetro `imagenUrl` al endpoint de [`pre-registro`](#pre-registro)
* Se añadió la sección de [notificaciones push](#notificaciones-push)
* Se añadió la sección de [stickers](#stickers)

## Versión 4
28 de agosto, 2017

Cambios de la versión:

* Se añadió endpoint de [chats activos](#chats-activos)
* Se añadió endpoint de [enviar mensaje](#enviar-mensaje)
* Se añadió endpoint de [historial](#historial)

## Versión 3
21 de agosto, 2017

Cambios de la versión:

* Se añadió endpoint de contactos en chat.
* Se añadió el campo `udid` a los endpoints de [`pre-registro`](#pre-registro), [login](#login) y [validación de código](#validar-codigo).
* Se añadió el campo `esSuperUsuario` a los endpoints de [`pre-registro`](#pre-registro), [login](#login) y [validación de código](#validar-codigo). Indica si es el usuario Tron.
* Se añadió el campo `imagenUrl` al endpoint de [`pre-registro`](#pre-registro).
* Se especificó qué hacer con el status code 400 en la sección de [errores](#errores)
* Se quitaron los acentos de los keys `descripcion`. Por ejemplo en [agenda](#agenda)

## Versión 2
17 de agosto, 2017

Cambios de la versión:

* Se corrigió la respuesta del endpoint de [`pre-registro`](#pre-registro) ahora se indica que se devuelve la info del perfil de usuario.
* Se indica que el endpoint de [`votacion`](#enviar-votacion) recibe un `Array` de valores, debido a que un usuario puede votar por varios workshops [Ver].
* Se agregó a los endpoints de [login](#login) y [registro](#pre-registro) el email del compañero de habitación que faltaba.
* Se añadió el endpoint de [`reenviarCodigo`](#reenviar-codigo).
* Se añadió el `idUsuario` a las respuestas del [registro](#pre-registro) y [login](#login).
* En los endpoints de [`votacion`](#votacion) y [`encuesta`](#encuesta) se indica que si el key es `null` significa que la encuesta ya ha sido respondida por el usuario.
* En los endpoints de [`votacion`](#votacion) y [`encuesta`](#encuesta) se envía un nuevo key `fechas` que indican los días en los que se tiene que mostrar la encuesta/votación.

## Versión 1
15 de agosto, 2017

Esta versión incluye una descripción de todos los endpoints excepto los que tienen que ver con el chat
# Introducción

Documentación para la conexión de las apps de Audi Evoluciona. 


# Autenticación

> Para autorizar las peticiones, utilizar el token que se te ha hecho llegar por correo en los headers de cada petición

```json
{
  "authorization": "token_ejemplo"
}
```

> Reemplazar `token_ejemplo` con el API KEY.

La API de Audi Evoluciona espera que cada petición contenga el token en el siguiente header.

`Authorization: token_ejemplo`

<aside class="notice">
Reemplazar <code>token ejemplo</code> con el API key correspondiente.
</aside>

El token será un API SECRET en el caso de endpoints que no requieran sesión y un token de sesión cuando se tenga.

# Login y Registro

## Login
> Body petición:

```json
{
  "email": "email@ejemplo.com",
  "codigo": "ABC123",
  "udid": "1234567890ABCDEFGHIJKL"
}
```

> Respuesta

```json
{
  "tokenSesion": "ABCDEFGH123456789",
  "usuario": {
    "idUsuario": 1,
    "esSuperUsuario": false,
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "email": "juan.perez@ejemplo.com",
    "imagenUrl": "http://example.com",
    "concesionario": {
      "idConcesionario": 1,
      "nombre": "Audi Center Pedregal"
    },
    "puesto": {
      "idPuesto": 1,
      "nombre": "Gerente de Ventas"
    },
    "fechaCumple": "1980-06-30",
    "alergias": "",
    "viaLlegada": {
      "idViaLlegada": 1,
      "nombre": "Terrestre"
    },
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.ramirez@gmail.com"
    }
  }
}
```
> Responde toda la información del usuario para llenar el perfil

> Roomie podría ser null si no se tiene un compañero de habitación

Inicia la sesión de un usuario y devuelve todo el contenido que se requiere para completar el perfil.

<aside class="info">Para todas las peticiones sucesivas se deberá de usar el token de sesión devuelto por este endpoint</aside>

### HTTP Request

`POST http://example.com/api/v1/usuario/login`

### Body Parameters

Parámetro | Tipo | Requerido | Description
--------- | ----------- | ----------- | -----------
email | String | SI | Email del usuario
codigo | String | SI | El código alfanumérico que le llegó al usuario por correo
udid | String | SI | Token para envío de notificaciones push. Si el usuario no acepta el envío de push enviar el identificador único del dispositivo.

## Catálogos registro

> Body petición:

```json
{
}
```
> Body vacío

> Respuesta

```json
{
  "concesionarios": [
    {
      "idConcesionario": 1,
      "nombre": "Audi Center Condesa"
    },
    {
      "idConcesionario": 2,
      "nombre": "Audi Center Satélite"
    }
  ],
  "puestos": [
    {
      "idPuesto": 1,
      "nombre": "Gerente de Ventas"
    },
    {
      "idConcesionario": 2,
      "nombre": "Gerente de Compras"
    }
  ],
  "vias": [
    {
      "idVia": 1,
      "nombre": "Terrestre"
    },
    {
      "idVia": 2,
      "nombre": "Aérea"
    }
  ]
}
```

Este endpoint obtiene los catálogos necesarios para llenar el formulario de registro y el perfil de usuario

### HTTP Request

`GET http://example.com/api/v1/catalogos/`

### Body Parameters

Sin parámetros


## Pre-Registro

> Body petición:

```json
{
  "udid": "ABCDEFGHIJKL",
  "usuario": {
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "email": "juan.perez@ejemplo.com",
    "idConcesionario": 1,
    "idPuesto": 1,
    "fechaCumple": "1980-06-30",
    "imagenUrl": "http://..."
    "alergias": "",
    "idViaLlegada": 1,
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.gonzalez@gmail.com"
    }
  }
}
```
> Roomie será null si elije la opción "No"

> Respuesta

```json
{
  "tokenSesion": "ABCDEFGH123456789",
  "usuario": {
    "idUsuario": 1,
    "esSuperUsuario": false,
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "imagenUrl": "http://imagen.ejemplo.com",
    "email": "juan.perez@ejemplo.com",
    "concesionario": {
      "idConcesionario": 1,
      "nombre": "Audi Center Pedregal"
    },
    "puesto": {
      "idPuesto": 1,
      "nombre": "Gerente de Ventas"
    },
    "fechaCumple": "1980-06-30",
    "alergias": "",
    "viaLlegada": {
      "idViaLlegada": 1,
      "nombre": "Terrestre"
    },
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.ramirez@gmail.com"
    }
  }
}
```

Este endpoint guarda los datos del usuario para evitar que los tenga que volver a llenar en caso de no validar su correo inmediatamente.

### HTTP Request

`POST http://example.com/api/v1/usuario/registro`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
udid | String | SI | Token para envío de notificaciones push. Si el usuario no acepta el envío de push enviar el identificador único del dispositivo.
nombre | String | SI | Nombres del usuario
apellidoPaterno | String | SI | Apellido del Usuario
apellidoMaterno | String | SI | Segundo Apellido del usuario
email | String | SI | Email del usuario
imagenUrl | String | SI | Url de la imagen del usuario
idConcesionario | Int | SI | Id del concesionario elegido por el usuario
idPuesto | Int | SI | Id del puesto elegido por el usuario
fechaCumple | String | SI | Fecha de nacimiento del usuario en formato "YYYY-MM-DD"
alergias | String | NO | Alergías del usuario
idViaLlegada | String | SI | Id de la vía de llegada del usuario
llegada | Object | SI | Objeto con la vía de llegada del usuario
llegada.fecha | String | SI | Fecha de llegada del usuario en formato "YYYY-MM-DD"
llegada.vuelo | String | SI | Texto que describe el transporte del usuario
salida | Object | SI | Objeto con la vía de salida del usuario
salida.fecha | String | SI | Fecha de salida del usuario en formato "YYYY-MM-DD"
salida.vuelo | String | SI | Texto que describe el transporte del usuario
roomie | Object | NO | Contiene la información del compañero de habitación del usuario
roomie.nombre | Object | SI | Nombre del compañero de habitación del usuario
roomie.apellidoPaterno | Object | SI | Primer apellido del compañero de habitación del usuario
roomie.apellidoMaterno | Object | SI | Segundo apellido del compañero de habitación del usuario
roomie.email | Object | SI | Email del compañero de habitación del usuario

## Validar email

> Body petición:

```json
{
  "email": "email@ejemplo.com"
}
```

> Respuesta

```json
{
  "ocupado": true|false
}
```

Durante el registro es necesario mandar a llamar este endpoint con el fin de verificar si el usuario ya realizó previamente su registro. En caso de que `ocupado` tenga el valor `true` se deberá mostrar la alerta correspondiente

### HTTP Request

`POST http://example.com/api/v1/usuario/validarEmail`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
email | String | SI | Email a validar


## Validar código
<aside class="info">
Este endpoint es un alias del endpoint de login.
</aside>

> Body petición:

```json
{
  "udid": "123456789ABCDEFJ"
  "email": "email@ejemplo.com",
  "codigo": "ABC123"
}
```

> Respuesta

```json
{
  "tokenSesion": "ABCDEFGH123456789",
  "usuario": {
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "email": "juan.perez@ejemplo.com",
    "concesionario": {
      "idConcesionario": 1,
      "nombre": "Audi Center Pedregal"
    },
    "puesto": {
      "idPuesto": 1,
      "nombre": "Gerente de Ventas"
    },
    "fechaCumple": "1980-06-30",
    "alergias": "",
    "viaLlegada": {
      "idViaLlegada": 1,
      "nombre": "Terrestre"
    },
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.ramirez@gmail.com"
    }
  }
}
```

Valida el email perteneciente al usuario y devuelve su información de perfil.

### HTTP Request

`POST http://example.com/api/v1/usuario/validarCodigo`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
udid | STRING | SI | Token para envio de push. Si el usuario no acepta el envío enviar el identificador único del dispositivo
email | String | SI | Email a validar
codigo | String | SI | Código a validar

<aside class="notice">
Es necesario almacenar y enviar el valor del <code>email</code> aún cuando no lo introduzca el usuario (por ejemplo, el caso de registro)
</aside>

## Reenviar código

> Body petición:

```json
{
  "email": "email@ejemplo.com",
}

{
  "tokenSesion": "ABCDEFGHIJKLMNOPQ123456",
}
```

> Respuesta

```json
{
  "recibido": true
}
```

Reenvía al usuario su código de verificación
<aside class="notice">
Por seguridad, este endpoint no indica si el email se encontró en nuestra BD, sólo responde si se procesó la petición.
</aside>
### HTTP Request

`POST http://example.com/api/v1/usuario/reenviarCodigo`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
email | String | SI | Email del usuario
tokenSesion | String | SI | Token de sesión del usuario

<aside class="notice">
No es necesario enviar ambos simultáneamente pero sí es necesario enviar uno
</aside>


## Actualizar Perfil

> Body petición:

```json
{
  "usuario": {
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "email": "juan.perez@ejemplo.com",
    "idConcesionario": 1,
    "idPuesto": 1,
    "imagenUrl": "http://",
    "fechaCumple": "1980-06-30",
    "alergias": "",
    "idViaLlegada": 1,
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.gonzalez@gmail.com"
    }
  }
}
```
> Roomie será null si elije la opción "No"

> Respuesta

```json
{
  "usuario": {
    "idUsuario": 1,
    "esSuperUsuario": false,
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "imagenUrl": "http://imagen.ejemplo.com",
    "email": "juan.perez@ejemplo.com",
    "concesionario": {
      "idConcesionario": 1,
      "nombre": "Audi Center Pedregal"
    },
    "puesto": {
      "idPuesto": 1,
      "nombre": "Gerente de Ventas"
    },
    "fechaCumple": "1980-06-30",
    "alergias": "",
    "viaLlegada": {
      "idViaLlegada": 1,
      "nombre": "Terrestre"|
    },
    "llegada": {
      "fecha": "2017-08-01",
      "vuelo": "AM 209"
    },
    "salida": {
      "fecha": "2017-08-02",
      "vuelo": "AM 209"
    },
    "roomie": {
      "apellidoPaterno": "González",
      "apellidoMaterno": "Ramírez",
      "nombre": "Alberto",
      "email": "alberto.ramirez@gmail.com"
    }
  }
}
```

Permite actualizar la información de perfil del usuario. Los parámetros son idénticos al registro.

### HTTP Request

`POST http://example.com/api/v1/usuario/perfil`

## Actualizar Token Push

> Body petición:

```json
{
  "udid": "ABCDEFGHI12345"
}
```
> Roomie será null si elije la opción "No"

> Respuesta

```json
{
  "enviado": true
}
```

<aside class="notice">Es necesario contar con sesión para utilizar este endpoint e identificar correctamente al usuario</aside>


En el caso de que un usuario no haya aceptado las push en primera instancia y después las acepte, se deberá de actualizar el udid del dispositivo.

### HTTP Request

`POST http://example.com/api/v1/usuario/actualizarToken`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
udid | Sring | SI | Nuevo udid del dispositivo


#Contenidos
<aside class="success">Para todas las peticiones sucesivas se deberá de usar el token de sesión devuelto anteriormente en el header <code>authorization</code></aside>

## Feed de Noticias
> Body petición:

```json
{
}
```

> Respuesta

```json
{
  "noticias": [
    {
      "titulo": "Noticia de Última Hora",
      "descripcion": "Descripción de la noticia",
      "urlImagen": "http://imagen.dominio.com/url"
    },
    {
      "titulo": "Noticia de Última Hora 2",
      "descripcion": "Descripción de la noticia 2",
      "urlImagen": "http://imagen.dominio.com/url2"
    }
  ]
}
```
> Las noticias no están paginadas, mostrar tantas como el endpoint devuelva.

Devuelve las últimas noticias publicadas por los administradores.

### HTTP Request

`GET http://example.com/api/v1/noticias/`

### Body Parameters

Sin parámetros

## Feed de Imágenes
> Body petición:

```json
{
}
```
> Query petición:

```json
{
  "pagina": 1
}
```
> El parámetro `página` tiene como default `1`


> Respuesta

```json
{
    "feed": [
        {
            "idFeed": 2,
            "urlImagen": "https://www.diariomotor.com/imagenes/2012/10/audi-marca-dm-7.jpg\r",
            "usuario": {
                "id": 1,
                "nombre": "Tron"
            }
        }
    ],
    "meta": {
        "paginaActual": 1,
        "paginaSiguiente": null,
        "registrosEncontrados": 1,
        "registrosTotales": 1
    }
}
```
> Las imágenes están paginadas, más info ver [historial](#historial)

Devuelve las últimas imágenes publicadas por los usuarios.

### HTTP Request

`GET http://example.com/api/v1/feed/`

### Body Parameters

Sin parámetros

## Nueva imágen
> Body petición:

```json
{
  "urlImagen": "http://..."
}
```

> Respuesta

```json
{
    "feed": {
        "idFeed": 9,
        "idUsuario": 2,
        "urlImagen": "lol"
    }
}
```

Publica una nueva imagen en el feed de imágenes

### HTTP Request

`POST http://example.com/api/v1/feed/nueva`

### Body Parameters

Sin parámetros

## Agenda
> Body petición:

```json
{
}
```

> Respuesta

```json
{
  "fechaEvento": "2017-11-01T09:00:00-06:00"
  "agenda": [
    {
      "dia": "2017-10-01",
      "eventos": [
          {
            "titulo": "Agenda 1",
            "descripcion": "Descripción del evento",
            "horaInicio": "11:00",
            "horaFin": "12:00",
            "adjunto": "http://archivos.dominio.com/url"
          },
          {
            "titulo": "Agenda 2",
            "descripcion": "Descripción del evento",
            "horaInicio": "13:00",
            "horaFin": "14:00",
            "adjunto": null
          }
      ]
    },
    {
      "dia": "2017-10-02",
      "eventos": [
          {
            "titulo": "Agenda 3",
            "descripcion": "Descripción del evento",
            "horaInicio": "11:00",
            "horaFin": "12:00",
            "adjunto": "http://archivos.dominio.com/url"
          },
          {
            "titulo": "Agenda 4",
            "descripcion": "Descripción del evento",
            "horaInicio": "13:00",
            "horaFin": "14:00",
            "adjunto": null
          }
      ]
    }
  ]
}
```
> El adjunto deberá estar disponible una vez concluido el evento

Devuelve la agenda del evento, separada en días.

### HTTP Request

`GET http://example.com/api/v1/agenda/`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
urlImagen | Sring | SI | Url de la imagen publicada en AWS

## Sede
> Body petición:

```json
{
}
```

> Respuesta

```json
{
  "evento": {
    "tituloEvento": "Audi Evoluciona",
    "descripcionEvento": "Descripción Audi Evoluciona",
  },
  "vestimenta": {
    "descripcion": "Casual Formal",
    "imagenUrl": "http://imagen.example.com/url"
  },
  "sede": {
    "direccion": "Av. 5 de mayo. Ciudad de México",
    "latitud": 21.323223,
    "longitud": -12.15465,
    "descripcion": "Estaciones cercanas: (...)"
  }
}
```
> El adjunto deberá estar disponible una vez concluido el evento

Devuelve información del evento.

### HTTP Request

`GET http://example.com/api/v1/sede/`

### Body Parameters

Sin parámetros


## Votación
> Body petición:

```json
{
}
```

> Respuesta

```json
{
  "fechas": [
    "2017-10-01",
    "2017-10-02"
  ],
  "workshops": [
    {
      "id": 1,
      "nombre": "Nombre Workshop"
    },
    {
      "id": 2,
      "nombre": "Otro Workshop"
    },
    {
      "id": 3,
      "nombre": "El Workshop"
    },
    {
      "id": 4,
      "nombre": "El Workshop"
    },
    {
      "id": 5,
      "nombre": "La Workshop"
    }
  ]
}
```

Al concluir los días del evento indicados en el key `fechas` se mostrará un link para que los usuarios voten por sus talleres favoritos (3).

Si el key `workshops` es `null` la votación ya ha sido enviada.

### HTTP Request

`GET http://example.com/api/v1/votacion/`

### Body Parameters

Sin parámetros

## Enviar Votación
> Body petición:

```json
{
  "idsWorkshop": [1,2,5]
}
```

> Respuesta

```json
{
  "enviado": true
}
```

Al concluir todos los días del evento se mostrará un link para que los usuarios voten por su taller favorito.

### HTTP Request

`POST http://example.com/api/v1/votacion/`

### Body Parameters


Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
idWorkshop | Int | SI | Id del workshop seleccionado

## Encuesta
> Body petición:

```json
{
}
```

> Respuesta

```json
{
  "fechas": [
    "2017-10-01"
  ],
  "encuesta": [
    {
      "idPregunta": 1,
      "numero": 1,
      "pregunta": "Menciona lo que más te gustó del evento",
      "abierta": true,
      "opciones": null,
      "estrellas": null
    },
    {
      "idPregunta": 2,
      "numero": 2,
      "pregunta": "Cómo calificarías el evento",
      "abierta": false,
      "opciones": ["Bueno", "Regular", "Malo"],
      "estrellas": null
    },
    {
      "idPregunta": 3,
      "numero": 3,
      "pregunta": "En una escala del 0 al 5, ¿qué valoración le das al evento",
      "abierta": false,
      "opciones": null,
      "estrellas": true
    }
  ]
}
```

Es necesario mostrar la encuesta al final de los días que indica el key `fechas`. Si el key `encuesta` es null, la encuesta ya ha sido respondida por el usuario y no se deberá pedir que se responda.

### HTTP Request

`GET http://example.com/api/v1/encuesta/`

### Body Parameters
Sin parámetros

## Enviar Encuesta
> Body petición:

```json
{
  "encuesta": [
    {
      "idPregunta": 1,
      "respuesta" "Los autos"
    },
    {
      "idPregunta": 2,
      "respuesta": "Bueno"
    },
    {
      "idPregunta": 3,
      "respuesta": "5"
    }
  ]
}
```

> Respuesta

```json
{
  "enviada": true
}
```

Las respuestas deberán de enviarse como texto.

### HTTP Request

`POST http://example.com/api/v1/encuesta/`

### Body Parameters
Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
encuesta | Array | SI | Objeto que contiene las respuestas
encuesta[] | Object | SI | Contiene una respuesta
encuesta[].idPregunta | Int | SI | Id de pregunta
encuesta[].respuesta | String | SI | Texto de respuesta

#Chat
La aplicación integra un chat que se divide en dos partes. Un grupo público del cual nadie se puede salir y al cual sólo el usuario Administrador (Tron) puede publicar. Y un chat entre cualquier par de usuarios de la aplicación. En este momento no se soportan grupos arbitrarios de usuarios.


## Contactos
> Body petición:

```json
{
}
```

> Respuesta

```json
{
    "usuarios": [
        {
            "id": 1,
            "nombre": "Tron",
            "apellidoPaterno": "Evoluciona",
            "apellidoMaterno": "",
            "imagenUrl": "http://tron",
            "concesionario": {
                "id": 1,
                "nombre": "Audi Center Aguascalientes",
                "codigo": "0151"
            }
        }
    ]
}
```

Es necesario llamar este endpoint cada vez que el usuario entra a la sección de chat.

### HTTP Request

`GET http://example.com/api/v1/contactos/`

### Body Parameters
Ninguno

## Chats activos
> Body petición:

```json
{
}
```

> Respuesta

```json
{
    "chats": [
        {
            "idChat": "1",
            "esSuperChat": true,
            "usuario": {
                "idUsuario": 1,
                "nombre": "Jhoan",
                "imagenUrl": "http://tron"
            },
            "ultimoMensaje": {
                "idMensaje": 34,
                "mensaje": "Perfecto, espero",
                "fecha": "2017-08-28T18:22:54.217Z"
            }
        }
    ]
}
```

Devuelve un `array` con todas las conversaciones activas del usuario ordenadas de la más reciente a la más antigua.

### HTTP Request

`GET http://example.com/api/v1/chats/activos/`

### Respuesta
Parámetro | Tipo | Descripción
--------- | ----------- | ----------- | -----------
chats | Array | Array que contiene los chats activos
chats[] | Object | Objeto que representa un chat activo
chats[].idChat | Object | Identificador del chat. Se utiliza en el endpoint [ultimo visto](#ultimo-visto)
chats[].esSuperChat | Object | Indica si es necesario ser super usuario para mandar mensajes en el chat. La propiedad es super usuario es devuelta en [pre-registro](#pre-registro) y [login](#login)
chats[].usuario | Object | Objeto que representa el usuario con el quien se tiene la conversacion
chats[].usuario.idUsuario | Int | Id del usuario con quien se tiene la conversacion
chats[].usuario.nombre | String | Nombre que se la da al chat y que coincide con el nombre de la persona con quien se tiene al chat
chats[].usuario.imagenUrl | Int | Url de la imagen del usuario
chats[].ultimoMensaje | Object | Objeto que contiene el último mensaje que se envió en esa conversación
chats[].ultimoMensaje.idMensaje | Int | Id del mensaje
chats[].ultimoMensaje.mensaje | String | Contenido del mensaje
chats[].ultimoMensaje.fecha | Date | Fecha de envío del mensaje


## Enviar mensaje
> Body petición:

```json
{
  "idUsuario": 1,
  "mensaje": "Hola",
  "idChat": null
}
```

> Respuesta

```json
{
    "enviado": true,
    "idChat": 15
}
```

Envía un mensaje a un usuario. En este proceso se crea internamente el chat y el cliente no necesita saber la existencia de este. Al haber al menos un mensaje entre dos usuarios el chat se es devuelto por el endpoint de chats activos.

### Update

En general, los usuarios normales envían el id del usuario con el que quieren hablar puesto que no hay chats grupales, sin embargo, para el caso de los superusuarios, deben tener una manera de enviar el mensaje sin tener un id de usuario concreto, es por esto que se debe enviar el `idChat` (devuelto por [chats activos](#chats-activos)) en lugar del `idUsuario`. Este caso sólo debería de aplicar para *superusuarios* que mandan mensajes a *superchats*

### HTTP Request

`POST http://example.com/api/v1/chats/mensajes/nuevo/`

### Body Petición
Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
idUsuario | Int | Id del usuario al que se le desea enviar el mensaje. Este id se obtiene de la lista de [contactos](#contactos)
mensaje | Str | Contenido del mensaje a enviar

## Historial

> Body petición:

```json
{
}
```


> Query Petición:

```json
{
  "idUsuario": 1,
  "idChat": null
  "pagina": 1,
  "desde": "2017-01-01T00:00:00.000Z"
}
```
<aside class="notice">
Nótese que los parámetros en este endpoint se envían como <code>query string</code> y no en el body.
</aside>

> Respuesta

```json
{
    "idChat": 15,
    "mensajes": [
        {
            "mensaje": "Bien y tú?",
            "idMensaje": 22,
            "idUsuario": 1,
            "idChat": 15,
            "fecha": "2017-08-28T18:21:57.006Z",
            "usuario": {
                "idUsuario": 1,
                "nombre": "Tron",
                "apellidoPaterno": "Evoluciona",
                "apellidoMaterno": "",
                "imagenUrl": "http://tron"
            }
        },
        {
            "mensaje": "Cómo estás?",
            "idMensaje": 21,
            "idUsuario": 2,
            "idChat": 15,
            "fecha": "2017-08-28T18:21:49.614Z",
            "usuario": {
                "idUsuario": 2,
                "nombre": "Jhoan",
                "apellidoPaterno": "García",
                "apellidoMaterno": "Cruz",
                "imagenUrl": "http://lol.com"
            }
        },
        {
            "mensaje": "Hola Jhoan",
            "idMensaje": 18,
            "idUsuario": 1,
            "idChat": 15,
            "fecha": "2017-08-25T18:15:46.945Z",
            "usuario": {
                "idUsuario": 1,
                "nombre": "Tron",
                "apellidoPaterno": "Evoluciona",
                "apellidoMaterno": "",
                "imagenUrl": "http://tron"
            }
        },
        {
            "mensaje": "Hola Tron!",
            "idMensaje": 17,
            "idUsuario": 2,
            "idChat": 15,
            "fecha": "2017-08-25T18:15:44.665Z",
            "usuario": {
                "idUsuario": 2,
                "nombre": "Jhoan",
                "apellidoPaterno": "García",
                "apellidoMaterno": "Cruz",
                "imagenUrl": "http://lol.com"
            }
        }
    ],
    "meta": {
        "paginaActual": 4,
        "paginaSiguiente": 5,
        "registrosEncontrados": 2,
        "registrosTotales": 10
    }
}
```
Devuelve el historial de mensajes en una conversación. Cuando se intente obtener el historial de un *superchat* se deberá de enviar el `idChat` en lugar del `idUsuario`

<aside class="success">
Este endpoint está paginado.
</aside>

### HTTP Request

`GET http://example.com/api/v1/chats/mensajes/historial/`

### Query String
Parámetro | Tipo | Requerido |Descripción
--------- | ----------- | ----------- | -----------
idUsuario | Int | NO | Usuario del cual se desea obtener el historial
idChat | Int | NO | idChat del cual se desea obtener el historial. Valído para *superchats*
pagina | Int | NO | Pagina que se desea obtener del historia. Default `1`
desde | Date | NO | Fecha desde la cual se desea obtener el historial. Default `NOW() / new Date`

### Respuesta
Parámetro | Tipo | Descripción
--------- | ----------- | -----------
mensajes | Array | Contiene el historial de mensajes
mensajes[] | Object | Contiene los mensajes ordenados del más reciente al más antiguo
mensajes[].mensaje | String | Contenido del mensaje
mensajes[].idMensaje | Int | Id del mensaje
mensajes[].idUsuario | Int | Id del usuario que envió el mensaje. El objeto `usuario` contiene información adicional sobre éste
mensajes[].fecha | Date | Fecha de envío del mensaje
mensajes[].usuario | Object | Contiene información adicional sobre la persona que envío el mensaje
mensajes[].usuario.idUsuario | Object | Id del usuario que envió el mensaje
mensajes[].usuario.nombre | String | Nombre del usuario que envió el mensaje
mensajes[].usuario.apellidoPaterno | String | Apellido Paterno del usuario que envió el mensaje
mensajes[].usuario.apellidoMaterno | String | Apellido Materno del usuario que envió el mensaje
mensajes[].usuario.imagenUrl | String | Imagen del usuario que envió el mensaje
meta | Object | Contiene información sobre la paginación
meta.paginaActual | Int | La página que se devolvió
meta.paginaSiguiente | Int | La página siguiente o bien `null` si no existe una página siguiente
meta.registrosEncontrados | Int | El total de registros que se devolvieron en esta petición.
meta.registrosTotales | Int | El total de mensajes que existen en esta conversación


## Ultimo visto
> Body petición:

```json
{
  "idMensaje": 42,
  "idChat": 15
}
```

> Respuesta

```json
{
    "enviado": true
}
```

Para poder agrupar las notificaciones push es necesario que las apps notifiquen en todo momento cuál es el último mensaje que han visto. Idealmente se envía esta información cada vez que se actualice el layout de chat en los clientes, por ejemplo, al enviar o visualizar un mensaje a la conversación. NOTA: no incluir en la vista de la app el estatus del mensaje.

### HTTP Request

`POST http://example.com/api/v1/chats/mensajes/ultimoVisto/`

### Body Petición
Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
idMensaje | Int | SI | Id del ultimo mensaje.
idUsuario | Int | SI | Id del usuario con el cual se tiene la conversación.


# Notificaciones Push

## Chat
Se enviará una notificación por cada nuevo mensaje que se reciba. Siguiendo el patrón de WhatsApp/Messenger, se deberán de mostrar todas las notificaciones en el caso de iOS y agrupar las notificaciones por conversación en el caso de Android.

> Estructura iOS:

```json
{
  "payload": {
    "idUsuario": 12,
    "mensajesNuevos": 1
  }
}
```
<aside class="notice">
Cabe destacar que el json de iOS hace referencia únicamente a la propiedad <code>payload</code> del objeto de notificación, esto quiere decir que se envían a parte las propiedades <code>title</code>, <code>alert</code>, <code>sound</code>, <code>badge</code>, etcétera.
</aside>

> Estructura android:

```json
{
  "payload": {
    "idUsuario": 12,
    "mensajesNuevos": 1
  }
}
```
<aside class="notice">
De igual forma en android, los datos necesarios para mostrar correctamente la notificación se envían a parte. El json hace referencia únicamente a la propiedad <code>payload</code>.
</aside>

## Noticia
Notificación de nueva noticia. Al hacer clic, deberá de abrirse la aplicación en la sección de noticias.
> Estructura ambas plataformas:

```json
{
  "payload": {
    "tipo": "noticia"
  }
}
```

## Agenda
Notificación de agenda actualizada. Al hacer clic, deberá de abrirse la aplicación en la sección de agenda o actualizar el contenido de la vista. También se utilizará para avisar de encuestas o votaciones con el título y mensaje correspondiente pero es importante que se abra la sección de agenda.
> Estructura ambas plataformas:

```json
{
  "payload": {
    "tipo": "agenda"
  }
}
```

## Sede
Notificación de sede actualizada. Al hacer clic, deberá de abrirse la aplicación en la sección de sede o actualizar el contenido de la vista.
> Estructura ambas plataformas:

```json
{
  "payload": {
    "tipo": "sede"
  }
}
```

## General
Notificación general. Al hacer clic, deberá de abrirse la aplicación o mostrarse al usuario. Para casos no contemplados.
> Estructura ambas plataformas:

```json
{
  "payload": {
    "tipo": "general"
  }
}
```


# Stickers

## Stickers
Los stickers deberán ser reemplazados por el cliente en la vista de chat. **No enviar urls o imágenes**. Los stickers sólo pueden ser enviados en un mensaje autocontenido, es decir **no es posible enviar stickers en medio de un mensaje**.

Existirán 8 stickers y el texto a reemplazar seguirá este formato **::sticker_X::**, donde `X` va del `1` al `8`. Ejemplo: `::sticker_1::`


# Developer
Los siguientes endpoints sólo están disponibles en tiempo de desarrollo y su objetivo es ayudar en las pruebas de la app, se desactivarán en producción.

## Eliminar Usuario
Elimina por completo un usuario de la base para permitir volver usar su correo

> Body Petición

```json
{
  "idUsuario": 2
}
```
<aside class="error">
Por favor, no borrar usuarios no creados por uno mismo.
</aside>

> Respuesta:

```
"OK"
```

## Enviar push
Le envía una notificación push personalizada a un usuario identificado por el email

> Body Petición

```json
{
  "email": "tron@evoluciona.com",
  "titulo": "titulo",
  "mensaje": "mensaje",
  "payload": {
    "test": "foo"
  }
}
```
<aside class="success">
Payload puede tener una cantidad arbitraria de llaves
</aside>

> Respuesta:

```
"OK"
```

### HTTP Request

`POST http://example.com/api/v1/developer/enviarPush`