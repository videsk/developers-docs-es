---
description: Te explicamos como utilizar encuestas mediante Rest API.
---

# Encuestas

Con nuestra Rest API de formularios podrás obtener las encuestas diseñadas en tu cuenta.

Los endpoints a continuación son públicos, es decir, se antepone `/public/` como medio diferenciador de endpoints privados.

{% hint style="info" %}
Para mostrar las encuestas te sugerimos utilizar nuestro SDK de formulario.
{% endhint %}

{% content-ref url="../sdks/forms.md" %}
[forms.md](../sdks/forms.md)
{% endcontent-ref %}

{% swagger method="get" path="/public/video-contact-center/surveys/:id" baseUrl="https://api.videsk.io" summary="Obtener encuesta de un segmento o servicio" %}
{% swagger-description %}
Podrás obtener la encuesta de un segmento o servicio mediante su ID
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
ID de la entidad
{% endswagger-parameter %}

{% swagger-parameter in="query" name="type" type="String" required="true" %}
Tipo de entidad "segments" o "services"
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Encuesta" %}
```javascript
{
  "form": [
    {
      "deleted": false,
      "_id": "62703d9d3cf0565020ec9e3c",
      "type": "nps",
      "label": "En base a tu experiencia en la llamada. ¿Recomendaría nuestra video atención?",
      "properties": {
        "min": 0,
        "max": 10,
        "required": true
      },
      "colors": {
        "red": 6,
        "yellow": [
          7,
          8
        ],
        "green": 9
      },
      "name": "phpm5n07sc9",
      "hint": "0 (Nada probable) y 10 (Muy probable)",
      "options": []
    },
    {
      "deleted": false,
      "_id": "62703d9d3cf0565020ec9e3d",
      "type": "csat",
      "label": "¿Qué tan satisfecho estás hoy con la atención que te hemos entregado?",
      "properties": {
        "min": 1,
        "max": 5
      },
      "colors": "#3871f5",
      "name": "ne4333pn1re",
      "hint": "",
      "options": []
    },
    {
      "deleted": false,
      "_id": "62703d9d3cf0565020ec9e3e",
      "type": "ces",
      "label": " ¿Ha sido fácil acceder a la nuestra video atención?",
      "properties": {
        "min": 1,
        "max": 7
      },
      "colors": "#46c4ba",
      "name": "27quwqsoauh",
      "hint": "",
      "options": []
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error de entidad" %}
```javascript
{
  "name": "BadRequest",
  "message": "Provide a valid type, allowed are \"segments,services\".",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Encuesta no encontrada" %}
```javascript
{
  "name": "NotFound",
  "message": "We do not cannot find a survey for the {entity} id provided.",
  "code": 404,
  "className": "not-found",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en [autorización](autorizacion.md).
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/surveys" baseUrl="https://api.videsk.io" summary="Enviar encuesta" %}
{% swagger-description %}
Podrás enviar una encuesta asociado a una llamada o agendamiento.
{% endswagger-description %}

{% swagger-parameter in="body" name="call" type="String" %}
ID de la llamada
{% endswagger-parameter %}

{% swagger-parameter in="body" name="appointment" type="String" %}
ID de agendamiento
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values" type="Array" required="true" %}
Listado de respuestas
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values._id" required="true" type="String" %}
ID de la respuesta
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values.value" required="true" type="String" %}
Valor de la respuesta
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {token}
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Encuesta recibida" %}
```javascript
{
  "message": "The survey was saved successfully.",
  "success": true
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="ID entidad inválido" %}
```javascript
{
  "name": "BadRequest",
  "message": "Provide a call or appointment id.",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Encuesta respondida" %}
```javascript
{
  "name": "BadRequest",
  "message": "The call or appointment not exist or the survey was answered.",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error en los campos enviados" %}
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

{% swagger-response status="400: Bad Request" description="Campo inválido" %}
```javascript
{
  "name": "BadRequest",
  "message": "The maximum of value is 10 for element \"62703d9d3cf0565020ec9e3c\".",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Campo requerido" %}
Este es un campo vació requerido que funciona como honeypot a bots.

```javascript
{
  "name": "BadRequest",
  "message": "The element form \"videsk_essential\" is required, never delete.",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en [autorización](autorizacion.md).
{% endswagger-response %}
{% endswagger %}
