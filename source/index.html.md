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

## Versión 2
17 de agosto, 2017

Cambios de la versión:

* Se corrigió la respuesta del endpoint de `pre-registro` ahora se indica que se devuelve la info del perfil de usuario.
* Se indica que el endpoint de `votacion` recibe un `Array` de valores, debido a que un usuario puede votar por varios workshops.
* Se agregó a los endpoints de registro el email del compañero de habitación que faltaba.
* Se añadió el endpoint de `reenviarCodigo`.
* Se añadió el `idUsuario` a las respuestas del registro.
* En los endpoints de `votacion` y `encuesta` se indica que si el key es `null` significa que la encuesta ya ha sido respondida por el usuario.
* En los endpoints de `votacion` y `encuesta` se envía un nuevo key `fechas` que indican los días en los que se tiene que mostrar la encuesta/votación.

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
  "codigo": "ABC123"
}
```

> Respuesta

```json
{
  "tokenSesion": "ABCDEFGH123456789",
  "usuario": {
    "idUsuario": 1,
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
  "usuario": {
    "nombre": "Juan",
    "apellidoPaterno": "Pérez",
    "apellidoMaterno": "Sánchéz",
    "email": "juan.perez@ejemplo.com",
    "idConcesionario": 1,
    "idPuesto": 1,
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
  "tokenSesion": "ABCDEFGH123456789",
  "usuario": {
    "idUsuario": 1,
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

Este endpoint guarda los datos del usuario para evitar que los tenga que volver a llenar en caso de no validar su correo inmediatamente.

### HTTP Request

`POST http://example.com/api/v1/usuario/registro`

### Body Parameters

Parámetro | Tipo | Requerido | Descripción
--------- | ----------- | ----------- | -----------
nombre | String | SI | Nombres del usuario
apellidoPaterno | String | SI | Apellido del Usuario
apellidoMaterno | String | SI | Segundo Apellido del usuario
email | String | SI | Email del usuario
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
      "descripción": "Descripción de la noticia",
      "urlImagen": "http://imagen.dominio.com/url"
    },
    {
      "titulo": "Noticia de Última Hora 2",
      "descripción": "Descripción de la noticia 2",
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
            "descripción": "Descripción del evento",
            "horaInicio": "11:00",
            "horaFin": "12:00",
            "adjunto": "http://archivos.dominio.com/url"
          },
          {
            "titulo": "Agenda 2",
            "descripción": "Descripción del evento",
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
            "descripción": "Descripción del evento",
            "horaInicio": "11:00",
            "horaFin": "12:00",
            "adjunto": "http://archivos.dominio.com/url"
          },
          {
            "titulo": "Agenda 4",
            "descripción": "Descripción del evento",
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

Sin parámetros

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
En progreso.
