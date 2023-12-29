---
description: We explain how to use forms through Rest API.
---

# Forms

With our Rest API for forms, you can obtain the forms designed in your account.

The following endpoints are public, meaning `/public/` is prefixed as a differentiator from private endpoints.

{% hint style="info" %}
To render the forms, we suggest using our form SDK.
{% endhint %}

## Format

Our forms are carefully designed to present a friendly and flexible format at the same time.

All forms that are sent must have the following schema:

```javascript
[
    { "_id": String, "value": String || Array || Number }
]
```

Within this `Array`, you must add the list of fields with their `_id` and `value`, with the latter being capable of receiving three types of data: `String`, `Number`, and `Array`.

The ID must match the values provided when obtaining a form, that is, with the `_id` field.

Consider that the values must match those configured in your account, especially for cases of single or multiple selection.

We have 3 levels of validation:

1. Data type corresponds to the field type
2. Validation of the value per field (built-in and/or customized)
3. Verification of restrictions (maximum, minimum, length, etc.)

{% content-ref url="../sdks/forms.md" %}
[forms.md](../sdks/forms.md)
{% endcontent-ref %}

{% swagger method="get" path="/public/video-contact-center/forms/:segmentId" baseUrl="https://api.videsk.io" summary="Obtain a segment's form" %}
{% swagger-description %}
You will be able to obtain the form of a segment by its ID
{% endswagger-description %}

{% swagger-parameter in="path" name="segmentId" type="String" required="true" %}
Segment ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="version" type="String" required="true" %}
Type of form "base" or "contact"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Form" %}
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

{% swagger-response status="400: Bad Request" description="Entity error" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "NotFound",
"message": "The XXXX version of form not found.",
"code": 404,
"className": "not-found",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Form not found" %}
[REPLACE_CODE_FORMAT]javascript
{
"name": "NotFound",
"message": "Not form found in segment provided.",
"code": 404,
"className": "not-found",
"errors": {}
}
[REPLACE_CODE_FORMAT]

Consider that it is possible that your account does not have a base or contact form configured.
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in

[authorization](authorization.md)

.
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/public/video-contact-center/forms" baseUrl="https://api.videsk.io" summary="Send survey" %}
{% swagger-description %}
You will be able to send a form which can be attached to a call or not.
{% endswagger-description %}

{% swagger-parameter in="body" name="segment" type="String" required="true" %}
Segment ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" required="true" %}
Form type "contact" or "pre-call"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values" type="Array" required="true" %}
List of fields
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values._id" required="true" type="String" %}
Field ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="values.value" required="true" type="String" %}
Field value
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="String" %}
Captcha token (no backend)
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Survey received" %}
[REPLACE_CODE_FORMAT]json
{
"message":"The form was saved successfully.",
"success":true,
"submission":"64a35822da9f12295c1d98dc"
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="No form configured" %}
[REPLACE_CODE_FORMAT]json
{
"name": "NotFound",
"message": "Not form found in segment provided.",
"code": 404,
"className": "not-found",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Captcha token required" %}
[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "Please provide a valid \"token\", is mandatory.",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid Captcha (no backend)" %}
[REPLACE_CODE_FORMAT]json
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
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid segment ID" %}
[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "Please check the segment id provided.",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid form type" %}
[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "Provide a valid \"type\" form submission.",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Error in sent fields" %}
[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "Some element not as field, please check or try again",
"code": 400,
"className": "bad-request",
"data": "Maybe the organization has changed the form and you're submit is not valid anymore.",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid field" %}
[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "The maximum of value is 10 for element \"62703d9d3cf0565020ec9e3c\".",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Required field" %}
This is an empty required field acting as a honeypot for bots.

[REPLACE_CODE_FORMAT]json
{
"name": "BadRequest",
"message": "The element form \"videsk_essential\" is required, never delete.",
"code": 400,
"className": "bad-request",
"errors": {}
}
[REPLACE_CODE_FORMAT]
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in

[authorization](authorization.md)

.
{% endswagger-response %}
{% endswagger %}
