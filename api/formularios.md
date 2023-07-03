---
description: Te explicamos como utilizar os formularios mediante Rest API.
---

# Formularios

Con nuestra Rest API de formularios podrás obtener los formularios diseñados en tu cuenta.

Los endpoints a continuación son públicos, es decir, se antepone `/public/` como medio diferenciador de endpoints privados.

{% hint style="info" %}
Para renderizar los formularios te sugerimos utilizar nuestro SDK de formulario.
{% endhint %}

{% content-ref url="../sdks/forms.md" %}
[forms.md](../sdks/forms.md)
{% endcontent-ref %}

{% swagger method="get" path="/public/video-contact-center/forms/:segmentId" baseUrl="https://api.videsk.io" summary="Obtener formulario de un segmento" %}
{% swagger-description %}
Podrás obtener el formulario de un segmento mediante su ID
{% endswagger-description %}

{% swagger-parameter in="path" name="segmentId" type="String" required="true" %}
ID del segmento
{% endswagger-parameter %}

{% swagger-parameter in="query" name="version" type="String" required="true" %}
Tipo de formulario "base" o "contact"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Formulario" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error de entidad" %}
```javascript
{
    "name": "NotFound",
    "message": "The XXXX version of form not found.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Formulario no encontrado" %}
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
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="API Key inválido" %}
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/forms" baseUrl="https://api.videsk.io" summary="Enviar encuesta" %}
{% swagger-description %}
Podrás enviar un formulario el cuál se podrá adjuntar a una llamada o no.
{% endswagger-description %}

{% swagger-parameter in="body" name="segment" type="String" required="true" %}
ID del segmento
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" required="true" %}
Tipo de formulario "contact" o "pre-call"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values" type="Array" required="true" %}
Listado de campos
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values._id" required="true" type="String" %}
ID del campo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values.value" required="true" type="String" %}
Valor del campo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="String" %}
Token captcha (no backend)
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Encuesta recibida" %}
```json
{
   "message":"The form was saved successfully.",
   "success":true,
   "submission":"64a35822da9f12295c1d98dc"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="No hay formulario configurado" %}
```json
{
    "name": "NotFound",
    "message": "Not form found in segment provided.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Captcha token requerido" %}
```json
{
    "name": "BadRequest",
    "message": "Please provide a valid \"token\", is mandatory.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Captcha Inválido (no backend)" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="ID segmento inválido" %}
```json
{
    "name": "BadRequest",
    "message": "Please check the segment id provided.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Tipo formulario inválido" %}
```json
{
    "name": "BadRequest",
    "message": "Provide a valid \"type\" form submission.",
    "code": 400,
    "className": "bad-request",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error en los campos enviados" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Campo inválido" %}
```json
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

```json
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
Referencia de errores en 

[autorización](autorizacion.md)

.
{% endswagger-response %}
{% endswagger %}
