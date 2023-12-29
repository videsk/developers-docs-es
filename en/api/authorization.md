---
description: We explain how to transact with our API using authorization.
---

# Authorization

The Videsk API uses a standard authorization based on the `Authorization` header, using the `Bearer` scheme.

We do not use versioning definition in URL or headers since it is done internally through the configuration of each account, that is, in your own account you will be able to define which API version to use if available.

{% hint style="info" %}
There are certain endpoints that will require certain fields in the body (`body`) depending on the API Token you have created, either for public use or backend.

This behavior will be reflected in security measures such as captcha or similar.
{% endhint %}

{% hint style="info" %}
Until the year 2023, we maintain only one version.
{% endhint %}

{% swagger method="get" path="/public/video-contact-center/segments" baseUrl="https://api.videsk.io" summary="Authorization example" expanded="true" %}
{% swagger-description %}
Get segments using authorization with API Key
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="Bearer" required="true" %}
Bearer {API Key}
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="" %}
application/json
{% endswagger-parameter %}

{% swagger-response status="401: Unauthorized" description="Invalid JWT" %}
```javascript
{
  "name": "NotAuthenticated",
    "message": "Authorization header with valid JWT is required.",
    "code": 401,
    "className": "not-authenticated",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="JWT malformed" %}
```javascript
{
  "name": "NotAuthenticated",
    "message": "jwt malformed",
    "code": 401,
    "className": "not-authenticated",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid signature" %}
```javascript
{
  "name": "NotAuthenticated",
    "message": "invalid signature",
    "code": 401,
    "className": "not-authenticated",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Expired JWT" %}
```javascript
{
  "name": "NotAuthenticated",
    "message": "jwt expired",
    "code": 401,
    "className": "not-authenticated",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Infected JWT" %}
```javascript
{
  "name": "NotAuthenticated",
    "message": "Unexpected token � in JSON at position 6",
    "code": 401,
    "className": "not-authenticated",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Integration key was removed" %}
```javascript
{
  "name": "Forbidden",
    "message": "The integration token it's invalid or was removed.",
    "code": 403,
    "className": "forbidden",
    "errors": {}
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="API Key don't have permissions to CRUD" %}
```javascript
{
  "name": "Forbidden",
    "message": "You don't have access to /public/video-contact-center/segments. Please contact to your administrator.",
    "code": 403,
    "className": "forbidden",
    "errors": {}
}
```
{% endswagger-response %}
{% endswagger %}
