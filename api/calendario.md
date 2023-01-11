---
description: Te explicamos como utilizar Calendario mediante Rest API.
---

# Calendario

Con nuestra Rest API de calendario podrás agendar citas o reuniones para tus clientes de forma fácil.

Los endpoints a continuación son públicos, es decir, se antepone `/public/` como medio diferenciador de endpoints privados.

{% hint style="info" %}
Te sugerimos revisar el [diagrama de flujos](../sdks/calendario/#flujos) para tener una vista del orden de peticiones a realizar, antes de utilizar nuestra API.
{% endhint %}

{% swagger method="get" path="/public/video-contact-center/services" baseUrl="https://api.videsk.io" summary="Obtener servicios de calendario" %}
{% swagger-description %}
Podrás obtener el listado de los servicios públicos disponibles
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de servicios" %}
{% code lineNumbers="true" %}
```javascript
{
   "total":1,
   "limit":10,
   "skip":0,
   "data":[
      {
         "users":[
            {
               "_id":"63bdbf3230013a2792550a1c",
               "firstname":"John",
               "lastname":"Doe"
            },
            {
               "_id":"63bdbf3b25ab497401602d07",
               "firstname":"Mark",
               "lastname":"Zuckerberg"
            }
         ],
         "title":"My service",
         "description":"Service description",
         "automatic":false,
         "id":"63bdbf49394aad976d4aa43b"
      }
   ]
}
```
{% endcode %}
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key invalido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/services/:id/dates" baseUrl="https://api.videsk.io" summary="Obtener días del mes disponibles por id de servicio" %}
{% swagger-description %}
Días del mes disponibles basado en el ID del servicio
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID del servicio
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Mes en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de días del mes" %}
```javascript
[
	"2023-02-01T03:00:00.000Z",
	"2023-02-02T03:00:00.000Z",
	"2023-02-03T03:00:00.000Z",
	"2023-02-04T03:00:00.000Z",
	"2023-02-05T03:00:00.000Z",
	"2023-02-06T03:00:00.000Z",
	"2023-02-07T03:00:00.000Z",
	"2023-02-08T03:00:00.000Z",
	"2023-02-09T03:00:00.000Z",
	"2023-02-10T03:00:00.000Z",
	"2023-02-11T03:00:00.000Z",
	"2023-02-12T03:00:00.000Z",
	"2023-02-13T03:00:00.000Z",
	"2023-02-14T03:00:00.000Z",
	"2023-02-15T03:00:00.000Z",
	"2023-02-16T03:00:00.000Z",
	"2023-02-17T03:00:00.000Z",
	"2023-02-18T03:00:00.000Z",
	"2023-02-19T03:00:00.000Z",
	"2023-02-20T03:00:00.000Z",
	"2023-02-21T03:00:00.000Z",
	"2023-02-22T03:00:00.000Z",
	"2023-02-23T03:00:00.000Z",
	"2023-02-24T03:00:00.000Z",
	"2023-02-25T03:00:00.000Z",
	"2023-02-26T03:00:00.000Z",
	"2023-02-27T03:00:00.000Z",
	"2023-02-28T03:00:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha está en el pasado" %}
```javascript
{
	"name": "BadRequest",
	"message": "The date can not be in the past.",
	"code": 400,
	"className": "bad-request",
	"data": "dateInPast",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key invalido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/services/:id/hours" baseUrl="https://api.videsk.io" summary="Obtener horas del día disponibles por id de servicio" %}
{% swagger-description %}
Horas del días disponibles basado en el ID del servicio
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID del servicio
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Hora en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de horas" %}
Las fechas están en ISO-8601, puedes utilizar nuestro [SDK de calendario](../sdks/calendario/) para formatear fechas en zona horaria local.

```javascript
[
	"2023-02-24T11:00:00.000Z",
	"2023-02-24T11:05:00.000Z",
	"2023-02-24T11:10:00.000Z",
	"2023-02-24T11:15:00.000Z",
	"2023-02-24T11:20:00.000Z",
	"2023-02-24T11:25:00.000Z",
	"2023-02-24T11:30:00.000Z",
	"2023-02-24T11:35:00.000Z",
	"2023-02-24T11:40:00.000Z",
	"2023-02-24T11:45:00.000Z",
	"2023-02-24T11:50:00.000Z",
	"2023-02-24T11:55:00.000Z",
	"2023-02-24T12:00:00.000Z",
	"2023-02-24T12:05:00.000Z",
	"2023-02-24T12:10:00.000Z",
	"2023-02-24T12:15:00.000Z",
	"2023-02-24T12:20:00.000Z",
	"2023-02-24T12:25:00.000Z",
	"2023-02-24T12:30:00.000Z",
	"2023-02-24T12:35:00.000Z",
	"2023-02-24T12:40:00.000Z",
	"2023-02-24T12:45:00.000Z",
	"2023-02-24T12:50:00.000Z",
	"2023-02-24T12:55:00.000Z",
	"2023-02-24T16:00:00.000Z",
	"2023-02-24T16:05:00.000Z",
	"2023-02-24T16:10:00.000Z",
	"2023-02-24T16:15:00.000Z",
	"2023-02-24T16:20:00.000Z",
	"2023-02-24T16:25:00.000Z",
	"2023-02-24T16:30:00.000Z",
	"2023-02-24T16:35:00.000Z",
	"2023-02-24T16:40:00.000Z",
	"2023-02-24T16:45:00.000Z",
	"2023-02-24T16:50:00.000Z",
	"2023-02-24T16:55:00.000Z",
	"2023-02-24T17:00:00.000Z",
	"2023-02-24T17:05:00.000Z",
	"2023-02-24T17:10:00.000Z",
	"2023-02-24T17:15:00.000Z",
	"2023-02-24T17:20:00.000Z",
	"2023-02-24T17:25:00.000Z",
	"2023-02-24T17:30:00.000Z",
	"2023-02-24T17:35:00.000Z",
	"2023-02-24T17:40:00.000Z",
	"2023-02-24T17:45:00.000Z",
	"2023-02-24T17:50:00.000Z",
	"2023-02-24T17:55:00.000Z",
	"2023-02-24T18:00:00.000Z",
	"2023-02-24T18:05:00.000Z",
	"2023-02-24T18:10:00.000Z",
	"2023-02-24T18:15:00.000Z",
	"2023-02-24T18:20:00.000Z",
	"2023-02-24T18:25:00.000Z",
	"2023-02-24T18:30:00.000Z",
	"2023-02-24T18:35:00.000Z",
	"2023-02-24T18:40:00.000Z",
	"2023-02-24T18:45:00.000Z",
	"2023-02-24T18:50:00.000Z",
	"2023-02-24T18:55:00.000Z",
	"2023-02-24T19:00:00.000Z",
	"2023-02-24T19:05:00.000Z",
	"2023-02-24T19:10:00.000Z",
	"2023-02-24T19:15:00.000Z",
	"2023-02-24T19:20:00.000Z",
	"2023-02-24T19:25:00.000Z",
	"2023-02-24T19:30:00.000Z",
	"2023-02-24T19:35:00.000Z",
	"2023-02-24T19:40:00.000Z",
	"2023-02-24T19:45:00.000Z",
	"2023-02-24T19:50:00.000Z",
	"2023-02-24T19:55:00.000Z",
	"2023-02-24T20:00:00.000Z",
	"2023-02-24T20:05:00.000Z",
	"2023-02-24T20:10:00.000Z",
	"2023-02-24T20:15:00.000Z",
	"2023-02-24T20:20:00.000Z",
	"2023-02-24T20:25:00.000Z",
	"2023-02-24T20:30:00.000Z",
	"2023-02-24T20:35:00.000Z",
	"2023-02-24T20:40:00.000Z",
	"2023-02-24T20:45:00.000Z",
	"2023-02-24T20:50:00.000Z",
	"2023-02-24T20:55:00.000Z",
	"2023-02-24T21:00:00.000Z",
	"2023-02-24T21:05:00.000Z",
	"2023-02-24T21:10:00.000Z",
	"2023-02-24T21:15:00.000Z",
	"2023-02-24T21:20:00.000Z",
	"2023-02-24T21:25:00.000Z",
	"2023-02-24T21:30:00.000Z",
	"2023-02-24T21:35:00.000Z",
	"2023-02-24T21:40:00.000Z",
	"2023-02-24T21:45:00.000Z",
	"2023-02-24T21:50:00.000Z",
	"2023-02-24T21:55:00.000Z",
	"2023-02-24T22:00:00.000Z",
	"2023-02-24T22:05:00.000Z",
	"2023-02-24T22:10:00.000Z",
	"2023-02-24T22:15:00.000Z",
	"2023-02-24T22:20:00.000Z",
	"2023-02-24T22:25:00.000Z",
	"2023-02-24T22:30:00.000Z",
	"2023-02-24T22:35:00.000Z",
	"2023-02-24T22:40:00.000Z",
	"2023-02-24T22:45:00.000Z",
	"2023-02-24T22:50:00.000Z",
	"2023-02-24T22:55:00.000Z",
	"2023-02-24T23:00:00.000Z",
	"2023-02-24T23:05:00.000Z",
	"2023-02-24T23:10:00.000Z",
	"2023-02-24T23:15:00.000Z",
	"2023-02-24T23:20:00.000Z",
	"2023-02-24T23:25:00.000Z",
	"2023-02-24T23:30:00.000Z",
	"2023-02-24T23:35:00.000Z",
	"2023-02-24T23:40:00.000Z",
	"2023-02-24T23:45:00.000Z",
	"2023-02-24T23:50:00.000Z",
	"2023-02-24T23:55:00.000Z",
	"2023-02-25T00:00:00.000Z",
	"2023-02-25T00:05:00.000Z",
	"2023-02-25T00:10:00.000Z",
	"2023-02-25T00:15:00.000Z",
	"2023-02-25T00:20:00.000Z",
	"2023-02-25T00:25:00.000Z",
	"2023-02-25T00:30:00.000Z",
	"2023-02-25T00:35:00.000Z",
	"2023-02-25T00:40:00.000Z",
	"2023-02-25T00:45:00.000Z",
	"2023-02-25T00:50:00.000Z",
	"2023-02-25T00:55:00.000Z",
	"2023-02-25T01:00:00.000Z",
	"2023-02-25T01:05:00.000Z",
	"2023-02-25T01:10:00.000Z",
	"2023-02-25T01:15:00.000Z",
	"2023-02-25T01:20:00.000Z",
	"2023-02-25T01:25:00.000Z",
	"2023-02-25T01:30:00.000Z",
	"2023-02-25T01:35:00.000Z",
	"2023-02-25T01:40:00.000Z",
	"2023-02-25T01:45:00.000Z",
	"2023-02-25T01:50:00.000Z",
	"2023-02-25T01:55:00.000Z",
	"2023-02-25T02:00:00.000Z",
	"2023-02-25T02:05:00.000Z",
	"2023-02-25T02:10:00.000Z",
	"2023-02-25T02:15:00.000Z",
	"2023-02-25T02:20:00.000Z",
	"2023-02-25T02:25:00.000Z",
	"2023-02-25T02:30:00.000Z",
	"2023-02-25T02:35:00.000Z",
	"2023-02-25T02:40:00.000Z",
	"2023-02-25T02:45:00.000Z",
	"2023-02-25T02:50:00.000Z",
	"2023-02-25T02:55:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha está en el pasado" %}
```javascript
{
	"name": "BadRequest",
	"message": "The date can not be in the past.",
	"code": 400,
	"className": "bad-request",
	"data": "dateInPast",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/users/:id/dates" baseUrl="https://api.videsk.io" summary="Obtener días del mes disponibles por id de usuario" %}
{% swagger-description %}
Días del mes disponibles basado en el ID del servicio
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID del usuario
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="Date" required="true" %}
Mes en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de días del mes" %}
Las fechas están en ISO-8601, puedes utilizar nuestro [SDK de calendario](../sdks/calendario/) para formatear fechas en zona horaria local.

```javascript
[
	"2023-02-01T03:00:00.000Z",
	"2023-02-02T03:00:00.000Z",
	"2023-02-03T03:00:00.000Z",
	"2023-02-04T03:00:00.000Z",
	"2023-02-05T03:00:00.000Z",
	"2023-02-06T03:00:00.000Z",
	"2023-02-07T03:00:00.000Z",
	"2023-02-08T03:00:00.000Z",
	"2023-02-09T03:00:00.000Z",
	"2023-02-10T03:00:00.000Z",
	"2023-02-11T03:00:00.000Z",
	"2023-02-12T03:00:00.000Z",
	"2023-02-13T03:00:00.000Z",
	"2023-02-14T03:00:00.000Z",
	"2023-02-15T03:00:00.000Z",
	"2023-02-16T03:00:00.000Z",
	"2023-02-17T03:00:00.000Z",
	"2023-02-18T03:00:00.000Z",
	"2023-02-19T03:00:00.000Z",
	"2023-02-20T03:00:00.000Z",
	"2023-02-21T03:00:00.000Z",
	"2023-02-22T03:00:00.000Z",
	"2023-02-23T03:00:00.000Z",
	"2023-02-24T03:00:00.000Z",
	"2023-02-25T03:00:00.000Z",
	"2023-02-26T03:00:00.000Z",
	"2023-02-27T03:00:00.000Z",
	"2023-02-28T03:00:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha está en el pasado" %}
```javascript
{
	"name": "BadRequest",
	"message": "The date can not be in the past.",
	"code": 400,
	"className": "bad-request",
	"data": "dateInPast",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key invalido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/users/:id/hours" baseUrl="https://api.videsk.io" summary="Obtener horas del día disponibles por id de usuario" %}
{% swagger-description %}
Horas del días disponibles basado en el ID del usuario
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID del usuario
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="query" name="date" type="String" required="true" %}
Hora en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="query" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Listado de horas" %}
Las fechas están en ISO-8601, puedes utilizar nuestro [SDK de calendario](../sdks/calendario/) para formatear fechas en zona horaria local.

```javascript
[
	"2023-02-24T11:00:00.000Z",
	"2023-02-24T11:05:00.000Z",
	"2023-02-24T11:10:00.000Z",
	"2023-02-24T11:15:00.000Z",
	"2023-02-24T11:20:00.000Z",
	"2023-02-24T11:25:00.000Z",
	"2023-02-24T11:30:00.000Z",
	"2023-02-24T11:35:00.000Z",
	"2023-02-24T11:40:00.000Z",
	"2023-02-24T11:45:00.000Z",
	"2023-02-24T11:50:00.000Z",
	"2023-02-24T11:55:00.000Z",
	"2023-02-24T12:00:00.000Z",
	"2023-02-24T12:05:00.000Z",
	"2023-02-24T12:10:00.000Z",
	"2023-02-24T12:15:00.000Z",
	"2023-02-24T12:20:00.000Z",
	"2023-02-24T12:25:00.000Z",
	"2023-02-24T12:30:00.000Z",
	"2023-02-24T12:35:00.000Z",
	"2023-02-24T12:40:00.000Z",
	"2023-02-24T12:45:00.000Z",
	"2023-02-24T12:50:00.000Z",
	"2023-02-24T12:55:00.000Z",
	"2023-02-24T16:00:00.000Z",
	"2023-02-24T16:05:00.000Z",
	"2023-02-24T16:10:00.000Z",
	"2023-02-24T16:15:00.000Z",
	"2023-02-24T16:20:00.000Z",
	"2023-02-24T16:25:00.000Z",
	"2023-02-24T16:30:00.000Z",
	"2023-02-24T16:35:00.000Z",
	"2023-02-24T16:40:00.000Z",
	"2023-02-24T16:45:00.000Z",
	"2023-02-24T16:50:00.000Z",
	"2023-02-24T16:55:00.000Z",
	"2023-02-24T17:00:00.000Z",
	"2023-02-24T17:05:00.000Z",
	"2023-02-24T17:10:00.000Z",
	"2023-02-24T17:15:00.000Z",
	"2023-02-24T17:20:00.000Z",
	"2023-02-24T17:25:00.000Z",
	"2023-02-24T17:30:00.000Z",
	"2023-02-24T17:35:00.000Z",
	"2023-02-24T17:40:00.000Z",
	"2023-02-24T17:45:00.000Z",
	"2023-02-24T17:50:00.000Z",
	"2023-02-24T17:55:00.000Z",
	"2023-02-24T18:00:00.000Z",
	"2023-02-24T18:05:00.000Z",
	"2023-02-24T18:10:00.000Z",
	"2023-02-24T18:15:00.000Z",
	"2023-02-24T18:20:00.000Z",
	"2023-02-24T18:25:00.000Z",
	"2023-02-24T18:30:00.000Z",
	"2023-02-24T18:35:00.000Z",
	"2023-02-24T18:40:00.000Z",
	"2023-02-24T18:45:00.000Z",
	"2023-02-24T18:50:00.000Z",
	"2023-02-24T18:55:00.000Z",
	"2023-02-24T19:00:00.000Z",
	"2023-02-24T19:05:00.000Z",
	"2023-02-24T19:10:00.000Z",
	"2023-02-24T19:15:00.000Z",
	"2023-02-24T19:20:00.000Z",
	"2023-02-24T19:25:00.000Z",
	"2023-02-24T19:30:00.000Z",
	"2023-02-24T19:35:00.000Z",
	"2023-02-24T19:40:00.000Z",
	"2023-02-24T19:45:00.000Z",
	"2023-02-24T19:50:00.000Z",
	"2023-02-24T19:55:00.000Z",
	"2023-02-24T20:00:00.000Z",
	"2023-02-24T20:05:00.000Z",
	"2023-02-24T20:10:00.000Z",
	"2023-02-24T20:15:00.000Z",
	"2023-02-24T20:20:00.000Z",
	"2023-02-24T20:25:00.000Z",
	"2023-02-24T20:30:00.000Z",
	"2023-02-24T20:35:00.000Z",
	"2023-02-24T20:40:00.000Z",
	"2023-02-24T20:45:00.000Z",
	"2023-02-24T20:50:00.000Z",
	"2023-02-24T20:55:00.000Z",
	"2023-02-24T21:00:00.000Z",
	"2023-02-24T21:05:00.000Z",
	"2023-02-24T21:10:00.000Z",
	"2023-02-24T21:15:00.000Z",
	"2023-02-24T21:20:00.000Z",
	"2023-02-24T21:25:00.000Z",
	"2023-02-24T21:30:00.000Z",
	"2023-02-24T21:35:00.000Z",
	"2023-02-24T21:40:00.000Z",
	"2023-02-24T21:45:00.000Z",
	"2023-02-24T21:50:00.000Z",
	"2023-02-24T21:55:00.000Z",
	"2023-02-24T22:00:00.000Z",
	"2023-02-24T22:05:00.000Z",
	"2023-02-24T22:10:00.000Z",
	"2023-02-24T22:15:00.000Z",
	"2023-02-24T22:20:00.000Z",
	"2023-02-24T22:25:00.000Z",
	"2023-02-24T22:30:00.000Z",
	"2023-02-24T22:35:00.000Z",
	"2023-02-24T22:40:00.000Z",
	"2023-02-24T22:45:00.000Z",
	"2023-02-24T22:50:00.000Z",
	"2023-02-24T22:55:00.000Z",
	"2023-02-24T23:00:00.000Z",
	"2023-02-24T23:05:00.000Z",
	"2023-02-24T23:10:00.000Z",
	"2023-02-24T23:15:00.000Z",
	"2023-02-24T23:20:00.000Z",
	"2023-02-24T23:25:00.000Z",
	"2023-02-24T23:30:00.000Z",
	"2023-02-24T23:35:00.000Z",
	"2023-02-24T23:40:00.000Z",
	"2023-02-24T23:45:00.000Z",
	"2023-02-24T23:50:00.000Z",
	"2023-02-24T23:55:00.000Z",
	"2023-02-25T00:00:00.000Z",
	"2023-02-25T00:05:00.000Z",
	"2023-02-25T00:10:00.000Z",
	"2023-02-25T00:15:00.000Z",
	"2023-02-25T00:20:00.000Z",
	"2023-02-25T00:25:00.000Z",
	"2023-02-25T00:30:00.000Z",
	"2023-02-25T00:35:00.000Z",
	"2023-02-25T00:40:00.000Z",
	"2023-02-25T00:45:00.000Z",
	"2023-02-25T00:50:00.000Z",
	"2023-02-25T00:55:00.000Z",
	"2023-02-25T01:00:00.000Z",
	"2023-02-25T01:05:00.000Z",
	"2023-02-25T01:10:00.000Z",
	"2023-02-25T01:15:00.000Z",
	"2023-02-25T01:20:00.000Z",
	"2023-02-25T01:25:00.000Z",
	"2023-02-25T01:30:00.000Z",
	"2023-02-25T01:35:00.000Z",
	"2023-02-25T01:40:00.000Z",
	"2023-02-25T01:45:00.000Z",
	"2023-02-25T01:50:00.000Z",
	"2023-02-25T01:55:00.000Z",
	"2023-02-25T02:00:00.000Z",
	"2023-02-25T02:05:00.000Z",
	"2023-02-25T02:10:00.000Z",
	"2023-02-25T02:15:00.000Z",
	"2023-02-25T02:20:00.000Z",
	"2023-02-25T02:25:00.000Z",
	"2023-02-25T02:30:00.000Z",
	"2023-02-25T02:35:00.000Z",
	"2023-02-25T02:40:00.000Z",
	"2023-02-25T02:45:00.000Z",
	"2023-02-25T02:50:00.000Z",
	"2023-02-25T02:55:00.000Z"
]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha está en el pasado" %}
```javascript
{
	"name": "BadRequest",
	"message": "The date can not be in the past.",
	"code": 400,
	"className": "bad-request",
	"data": "dateInPast",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/service/:id" baseUrl="https://api.videsk.io" summary="Agendar una hora por servicio" %}
{% swagger-description %}
Agendar una hora mediante un servicio con selección automáticamente de agente
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID de servicio
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startAt" type="Date" required="true" %}
Fecha en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="body" name="form" type="Array" required="true" %}
Campos de formulario
{% endswagger-parameter %}

{% swagger-parameter in="body" name="referrer" type="String" required="true" %}
Campaña o web referido
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Hora agendada" %}
```javascript
{
   "email":"john.doe@example.com",
   "service":"Service name",
   "startAt":"2023-02-01T03:00:00.000Z",
   "endAt":"2023-02-01T03:07:00.000Z",
   "duration":7,
   "timezone":"America/Santiago",
   "joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "message":"Your appointment was successfully scheduled."
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error en los campos de formulario" %}
```javascript
{
	"name": "BadRequest",
	"message": "You reach the max characters is 50 for element \"60dbe3416af0be33b8b372b1\".",
	"code": 400,
	"className": "bad-request",
	"errors": {}
}
```

```javascript
{
	"name": "BadRequest",
	"message": "Some element not as field, please check or try again",
	"code": 400,
	"className": "bad-request",
	"data": "Maybe the organization has changed the form and you're submit is not valid anymore.",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Hora no disponible" %}
```javascript
{
	"name": "Conflict",
	"message": "Sorry, the hour \"2023-02-07T03:56:00.000Z\" is unavailable.",
	"code": 409,
	"className": "conflict",
	"errors": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/user/:id" baseUrl="https://api.videsk.io" summary="Agendar una hora por servicio" %}
{% swagger-description %}
Agendar una hora mediante un agente
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID del usuario
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="service" type="String" required="true" %}
ID del servicio
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startAt" type="Date" required="true" %}
Fecha en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timezone" type="String" required="true" %}
Zona horaria en formato ISO-8601
{% endswagger-parameter %}

{% swagger-parameter in="body" name="form" type="Array" required="true" %}
Campos de formulario
{% endswagger-parameter %}

{% swagger-parameter in="body" name="referrer" type="String" required="true" %}
Campaña o web referido
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Hora agendada" %}
```javascript
{
   "email":"john.doe@example.com",
   "service":"Service name",
   "startAt":"2023-02-01T03:00:00.000Z",
   "endAt":"2023-02-01T03:07:00.000Z",
   "duration":5,
   "timezone":"America/Santiago",
   "joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "message":"Your appointment was successfully scheduled."
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="ID del servicio inválido" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid service id is required",
	"code": 400,
	"className": "bad-request",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Zona horaria inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"timezone\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "timezone",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error en los campos de formulario" %}
```javascript
{
	"name": "BadRequest",
	"message": "You reach the max characters is 50 for element \"60dbe3416af0be33b8b372b1\".",
	"code": 400,
	"className": "bad-request",
	"errors": {}
}
```

```javascript
{
	"name": "BadRequest",
	"message": "Some element not as field, please check or try again",
	"code": 400,
	"className": "bad-request",
	"data": "Maybe the organization has changed the form and you're submit is not valid anymore.",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key invalido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Hora no disponible" %}
```javascript
{
	"name": "Conflict",
	"message": "Sorry, the hour \"2023-02-07T04:24:00.000Z\" is unavailable.",
	"code": 409,
	"className": "conflict",
	"errors": {}
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/cancel" baseUrl="https://api.videsk.io" summary="Cancelar una hora" %}
{% swagger-description %}
Cancelar una hora usando 

`actionToken`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {actionToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancelReason" type="String" %}
Razón de cancelación
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Hora cancelada" %}
```javascript
{
	"service": "Service name",
	"message": "The appointment was successfully canceled"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Razón de cancelación inválido" %}
```javascript
{
	"name": "BadRequest",
	"message": "Cast to string failed for value \"[]\" (type Array) at path \"cancelReason\"",
	"code": 400,
	"className": "bad-request",
	"errors": {}
}
```

```javascript
{
	"name": "BadRequest",
	"message": "Validation failed: cancelReason: Path `cancelReason` (`...`) is longer than the maximum allowed length (1000).",
	"code": 400,
	"className": "bad-request",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Error cancelado" %}
Este error indica que la hora ya ha sido cancelada previamente, no es posible cancelar después del horario de inicio o ya ha finalizado.

```javascript
{
	"name": "NotAuthenticated",
	"message": "The token is not valid any more.",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Action token inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/schedule/reschedule" baseUrl="https://api.videsk.io" summary="Reagendar una hora" %}
{% swagger-description %}
Reagendar una hora usando 

`actionToken`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {actionToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="date" type="Date" required="true" %}
Fecha en formato ISO-8601
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Hora reagendada" %}
```javascript
{
   "email":"john.doe@example.com",
   "service":"Service name",
   "startAt":"2023-02-01T03:00:00.000Z",
   "endAt":"2023-02-01T03:07:00.000Z",
   "duration":5,
   "timezone":"America/Santiago",
   "joinURL":"https://example.com?v-schedule-action=join&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "rescheduleURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "cancelURL":"https://example.com?v-schedule-action=modify&v-schedule-auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "accessToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "actionToken":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
   "message":"Your appointment was successfully scheduled."
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Fecha inválida" %}
```javascript
{
	"name": "BadRequest",
	"message": "A valid \"date\" is required",
	"code": 400,
	"className": "bad-request",
	"data": "date",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Error reagendado" %}
Este error indica que la hora ya ha sido reagendada previamente, no es posible reagendar después del horario de inicio o ya ha finalizado.

```javascript
{
	"name": "NotAuthenticated",
	"message": "The token is not valid any more.",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Action token inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/public/video-contact-center/schedule/info" baseUrl="https://api.videsk.io" summary="Obtener información de una cita" %}
{% swagger-description %}
Obtener la información de una cita como agente, servicio fecha de inicio, fin y estado.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Información de la hora" %}
```javascript
{
   "id":"63be2378f0dd1fdbf86dac48",
   "service":{
      "id":"620fedcc8951823b744f3122",
      "title":"Service name",
      "description":"Service description"
   },
   "user":{
      "firstname":"Mark",
      "lastname":"Zuckerberg",
      "_id":"6179480f5aa331375394e6a9"
   },
   "startAt":"2023-02-07T05:13:00.000Z",
   "endAt":"2023-02-07T05:20:00.000Z",
   "status":"pending"
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Hora expirada" %}
Este error se arroja cuando se intenta obtener información de una hora que ya ha sido cancelada, reagendada o ha finalizado.

```javascript
{
	"name": "NotAuthenticated",
	"message": "The token is not valid any more.",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Action token inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}
