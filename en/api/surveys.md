---
description: Here's how to use forms through the Rest API.
---

# Forms

With our Rest API for forms, you can get the forms designed in your account.

The following endpoints are public, meaning `/public/` is prefixed as a differentiator from private endpoints.

{% hint style="info" %}
To render forms, we suggest using our form SDK.
{% endhint %}

## Format

Our forms are carefully designed to present a friendly and flexible format at the same time.

All forms sent must have the following schema:

```javascript
[
    { "_id": String, "value": String || Array || Number }
]
```

Within this `Array`, you must add the list of fields with their `_id` and `value`, the latter being able to receive three types of data: `String`, `Number`, and `Array`.

The ID must match the values delivered when obtaining a form, that is, with the `_id` field.

You should consider that the values must match those configured in your account, especially for single or multiple selection cases.

We have 3 levels of validation:

1. Data type corresponds with the field type
2. Value validation per field (built-in and/or custom)
3. Verification of restrictions (maximum, minimum, length, etc.)

{% content-ref url="../sdks/forms.md" %}
[forms.md](../sdks/forms.md)
{% endcontent-ref %}

{% swagger method="get" path="/public/video-contact-center/forms/:segmentId" baseUrl="https://api.videsk.io" summary="Obtain form of a segment" %}
{% swagger-description %}
You can obtain the form of a segment using its ID.
{% endswagger-description %}

{% swagger-parameter in="path" name="segmentId" type="String" required="true" %}
Segment ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="version" type="String" required="true" %}
Form type "base" or "contact"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Form" %}
```javascript
{
   "form":[
      {
         "_id":"60f652f1cfa34fc3157ef5c6",
         "type":"text",
         "name":"firstname",
         "label":"First name",
         "properties":{
            "required":true,
            "placeholder":"Enter your first name..."
         },
         "options":[],
         "hint":""
      },
      {
         "_id":"61d25bc9294d18677ce6ef6f",
         "type":"text",
         "label":"Last name",
         "properties":{
            "placeholder":"Enter your last name",
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
         "label":"Email",
         "properties":{
            "required":true,
            "placeholder":"Enter your email..."
         },
         "options":[],
         "hint":""
      },
      {
         "_id":"60f654b4cfa34fc3157ef5cc",
         "type":"text",
         "label":"Company name",
         "properties":{
            "placeholder":"Enter the company name...",
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
         "label":"Website",
         "properties":{
            "placeholder":"Enter a link with http://",
            "required":true
         },
         "name":"website",
         "hint":"Must prefix with http:// or https://",
         "options":[
            
         ]
      },
      {
         "_id":"61d25bc9294d18677ce6ef73",
         "type":"text",
         "label":"Industry",
         "properties":{
            "placeholder":"Enter the business industry",
            "maxlength":"100"
         },
         "name":"industry",
         "hint":"",
         "options":[]
      },
      {
         "_id":"60f654b4cfa34fc3157ef5ce",
         "type":"textarea",
         "label":"Message",
         "properties":{
            "placeholder":"Leave us a message and we'll get back to you.",
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
```javascript
{
    "name": "NotFound",
    "message": "The XXXX version of the form not found.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Form not found" %}
```javascript
{
    "name": "NotFound",
    "message": "Not form found in segment provided.",
    "code": 404,
    "className": "not-found",
    "errors": {}
}
```

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
You can send a form which can be attached to a call or not.
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
```json
{
   "message":"The form was saved successfully.",
   "success":true,
   "submission":"64a35822da9f12295c1d98dc"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="No form configured" %}
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

{% swagger-response status="400: Bad Request" description="Captcha token required" %}
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

{% swagger-response status="400: Bad Request" description="Invalid captcha (no backend)" %}
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

{% swagger-response status="400: Bad Request" description="Invalid segment ID" %}
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

{% swagger-response status="400: Bad Request" description="Invalid form type" %}
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

{% swagger-response status="400: Bad Request" description="Error in sent fields" %}
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

{% swagger-response status="400: Bad Request" description="Invalid field" %}
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

{% swagger-response status="400: Bad Request" description="Required field" %}
This is a required empty field that works as a honeypot for bots.

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

{% swagger-response status="401: Unauthorized" description="Invalid API Key" %}
Error reference in

[authorization](authorization.md)

.
{% endswagger-response %}
{% endswagger %}
