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

## Obtener encuesta de un segmento o servicio

<mark style="color:blue;">`GET`</mark> `https://api.videsk.io/public/video-contact-center/surveys/:id`

Podrás obtener la encuesta de un segmento o servicio mediante su ID

#### Path Parameters

| Name                                 | Type   | Description      |
| ------------------------------------ | ------ | ---------------- |
| id<mark style="color:red;">\*</mark> | String | ID de la entidad |

#### Query Parameters

| Name                                   | Type   | Description                             |
| -------------------------------------- | ------ | --------------------------------------- |
| type<mark style="color:red;">\*</mark> | String | Tipo de entidad "segments" o "services" |

#### Headers

| Name                                            | Type   | Description      |
| ----------------------------------------------- | ------ | ---------------- |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer {token}   |
| Content-Type<mark style="color:red;">\*</mark>  | String | application/json |

{% tabs %}
{% tab title="200: OK Encuesta" %}
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
{% endtab %}

{% tab title="400: Bad Request Error de entidad" %}
```javascript
{
  "name": "BadRequest",
  "message": "Provide a valid type, allowed are \"segments,services\".",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Encuesta no encontrada" %}
```javascript
{
  "name": "NotFound",
  "message": "We do not cannot find a survey for the {entity} id provided.",
  "code": 404,
  "className": "not-found",
  "errors": {}
}
```
{% endtab %}

{% tab title="401: Unauthorized API Key inválido" %}
Referencia de errores en [autorización](autorizacion.md).
{% endtab %}
{% endtabs %}

## Enviar encuesta

<mark style="color:green;">`POST`</mark> `https://api.videsk.io/public/video-contact-center/surveys`

Podrás enviar una encuesta asociado a una llamada o agendamiento.

#### Headers

| Name                                            | Type   | Description      |
| ----------------------------------------------- | ------ | ---------------- |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer {token}   |
| Content-Type<mark style="color:red;">\*</mark>  | String | application/json |

#### Request Body

| Name                                           | Type   | Description           |
| ---------------------------------------------- | ------ | --------------------- |
| call                                           | String | ID de la llamada      |
| appointment                                    | String | ID de agendamiento    |
| values<mark style="color:red;">\*</mark>       | Array  | Listado de respuestas |
| values.\_id<mark style="color:red;">\*</mark>  | String | ID de la respuesta    |
| values.value<mark style="color:red;">\*</mark> | String | Valor de la respuesta |

{% tabs %}
{% tab title="201: Created Encuesta recibida" %}
```javascript
{
  "message": "The survey was saved successfully.",
  "success": true
}
```
{% endtab %}

{% tab title="400: Bad Request Encuesta respondida" %}
```javascript
{
  "name": "BadRequest",
  "message": "The call or appointment not exist or the survey was answered.",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Error en los campos enviados" %}
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
{% endtab %}

{% tab title="400: Bad Request Campo inválido" %}
```javascript
{
  "name": "BadRequest",
  "message": "The maximum of value is 10 for element \"62703d9d3cf0565020ec9e3c\".",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Campo requerido" %}
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
{% endtab %}

{% tab title="401: Unauthorized API Key inválido" %}
Referencia de errores en [autorización](autorizacion.md).
{% endtab %}

{% tab title="400: Bad Request ID entidad inválido" %}
```javascript
{
  "name": "BadRequest",
  "message": "Provide a call or appointment id.",
  "code": 400,
  "className": "bad-request",
  "errors": {}
}
```
{% endtab %}
{% endtabs %}
