---
description: Te explicamos como utilizar os formularios mediante Rest API.
---

# Formularios

Con nuestra Rest API de formularios podrás obtener los formularios diseñados en tu cuenta.

Los endpoints a continuación son públicos, es decir, se antepone `/public/` como medio diferenciador de endpoints privados.

{% hint style="info" %}
Para renderizar los formularios te sugerimos utilizar nuestro SDK de formulario.
{% endhint %}

## Formato

Nuestros formularios están cuidadosamente diseñados para presentar un formato amigable y flexible al mismo tiempo.

Todos los formularios que se envíen deben tener el siguiente esquema:

```javascript
[
    { "_id": String, "value": String || Array || Number }
]
```

Dentro de este `Array` debes añadir el listado de campos con su `_id` y `value`, siendo este último capaz de recibir tres tipos de datos: `String`, `Number` y `Array`.

El ID debe coincidir con los valores que se entregan al obtener un formulario, es decir, con el campo `_id`.

Debes considerar que los valores deben coincidir con los configurados en tu cuenta, sobre todo para los casos de selección única o múltiple.

Contamos con 3 niveles de validación:

1. Tipo de dato corresponde con el tipo de campo
2. Validación del valor por campo (built-in y/o personalizado)
3. Verificación de restricciones (máximo, mínimo, longitud, etc)

{% content-ref url="../sdks/forms.md" %}
[forms.md](../sdks/forms.md)
{% endcontent-ref %}

## Obtener formulario de un segmento

<mark style="color:blue;">`GET`</mark> `https://api.videsk.io/public/video-contact-center/forms/:segmentId`

Podrás obtener el formulario de un segmento mediante su ID

#### Path Parameters

| Name                                        | Type   | Description     |
| ------------------------------------------- | ------ | --------------- |
| segmentId<mark style="color:red;">\*</mark> | String | ID del segmento |

#### Query Parameters

| Name                                      | Type   | Description                           |
| ----------------------------------------- | ------ | ------------------------------------- |
| version<mark style="color:red;">\*</mark> | String | Tipo de formulario "base" o "contact" |

#### Headers

| Name                                            | Type   | Description      |
| ----------------------------------------------- | ------ | ---------------- |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer {token}   |
| Content-Type<mark style="color:red;">\*</mark>  | String | application/json |

{% tabs %}
{% tab title="200: OK Formulario" %}
```javascript
{
   "form":[
      {
         "_id":"60f652f1cfa34fc3157ef5c6",
         "type":"text",
         "name":"firstname",
         "label":"Nombre",
         "properties":{
            "required":true,
            "placeholder":"Ingrese su nombre..."
         },
         "options":[],
         "hint":""
      },
      {
         "_id":"61d25bc9294d18677ce6ef6f",
         "type":"text",
         "label":"Apellido",
         "properties":{
            "placeholder":"Ingrese su apellido",
            "maxlength":"50"
         },
         "name":"lastname",
         "hint":"",
         "options":[]
      },
      {
         "_id":"60f652f1cfa34fc3157ef5c7",
         "type":"email",
         "name":"email",
         "label":"Correo electrónico",
         "properties":{
            "required":true,
            "placeholder":"Ingrese su email..."
         },
         "options":[],
         "hint":""
      },
      {
         "_id":"60f654b4cfa34fc3157ef5cc",
         "type":"text",
         "label":"Nombre de la empresa",
         "properties":{
            "placeholder":"Ingrese nombre de la empresa...",
            "maxlength":"50",
            "required":true
         },
         "name":"company",
         "hint":"",
         "options":[]
      },
      {
         "_id":"60f654b4cfa34fc3157ef5cd",
         "type":"url",
         "label":"Sitio web",
         "properties":{
            "placeholder":"Ingrese un enlace con http://",
            "required":true
         },
         "name":"website",
         "hint":"Debe anteponer http:// o https://",
         "options":[
            
         ]
      },
      {
         "_id":"61d25bc9294d18677ce6ef73",
         "type":"text",
         "label":"Industria",
         "properties":{
            "placeholder":"Ingrese la industria del negocio",
            "maxlength":"100"
         },
         "name":"industry",
         "hint":"",
         "options":[]
      },
      {
         "_id":"60f654b4cfa34fc3157ef5ce",
         "type":"textarea",
         "label":"Mensaje",
         "properties":{
            "placeholder":"Déjanos tu mensaje y te contactaremos.",
            "maxlength":"250"
         },
         "name":"message",
         "hint":"",
         "options":[]
      }
   ],
   "siteKey":"XXXXXXXXXXXXXXX",
   "resource":"https://challenges.cloudflare.com/turnstile/v0/api.js",
   "provider":"turnstile"
}
```
{% endtab %}

{% tab title="400: Bad Request Error de entidad" %}
```javascript
{
    "name": "NotFound",
    "message": "The XXXX version of form not found.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Formulario no encontrado" %}
```javascript
{
    "name": "NotFound",
    "message": "Not form found in segment provided.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```

Considera que es posible que tu cuenta no tengas configurado un formulario base o de contacto.
{% endtab %}

{% tab title="401: Unauthorized API Key inválido" %}
Referencia de errores en [autorización](autorizacion.md).
{% endtab %}
{% endtabs %}

## Enviar encuesta

<mark style="color:green;">`POST`</mark> `https://api.videsk.io/public/video-contact-center/forms`

Podrás enviar un formulario el cuál se podrá adjuntar a una llamada o no.

#### Headers

| Name                                            | Type   | Description      |
| ----------------------------------------------- | ------ | ---------------- |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer {token}   |
| Content-Type<mark style="color:red;">\*</mark>  | String | application/json |

#### Request Body

| Name                                           | Type   | Description                               |
| ---------------------------------------------- | ------ | ----------------------------------------- |
| segment<mark style="color:red;">\*</mark>      | String | ID del segmento                           |
| type<mark style="color:red;">\*</mark>         | String | Tipo de formulario "contact" o "pre-call" |
| values<mark style="color:red;">\*</mark>       | Array  | Listado de campos                         |
| values.\_id<mark style="color:red;">\*</mark>  | String | ID del campo                              |
| values.value<mark style="color:red;">\*</mark> | String | Valor del campo                           |
| token                                          | String | Token captcha (no backend)                |

{% tabs %}
{% tab title="201: Created Encuesta recibida" %}
```json
{
   "message":"The form was saved successfully.",
   "success":true,
   "submission":"64a35822da9f12295c1d98dc"
}
```
{% endtab %}

{% tab title="400: Bad Request Captcha Inválido (no backend)" %}
```json
{
    "name": "Unprocessable",
    "message": "Your submit looks suspicious, not pass the captcha validation.",
    "code": 422,
    "className": "unprocessable",
    "data": {
        "extraData": "invalid-input-response"
    },
    "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Error en los campos enviados" %}
```json
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
```json
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

```json
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

{% tab title="400: Bad Request Captcha token requerido" %}
```json
{
    "name": "BadRequest",
    "message": "Please provide a valid \"token\", is mandatory.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request ID segmento inválido" %}
```json
{
    "name": "BadRequest",
    "message": "Please check the segment id provided.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request Tipo formulario inválido" %}
```json
{
    "name": "BadRequest",
    "message": "Provide a valid \"type\" form submission.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endtab %}

{% tab title="400: Bad Request No hay formulario configurado" %}
```json
{
    "name": "NotFound",
    "message": "Not form found in segment provided.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endtab %}
{% endtabs %}
