---
description: Te explicamos como transaccionar con nuestra API mediante autorización.
---

# Autorización

La API de Videsk utiliza una autorización estándar basada en cabecera `Authorization`, usando el esquema `Bearer`.

No utilizamos definición de versionamiento en URL o cabeceras ya que se realiza de forma interna mediante configuración de cada cuenta, es decir, en tu propia cuenta podrás definir cual versión de API utilizar en caso de estar disponible.

{% hint style="info" %}
Existen ciertos endpoints que requerirán ciertos campos en el cuerpo (`body`) dependiendo del API Token que hayas creado, ya sea para usarlo de forma pública o en backend.

Este comportamiento se verá reflejado en las medidas de seguridad como captcha o similares.
{% endhint %}

{% swagger method="get" path="/public/video-contact-center/segments" baseUrl="https://api.videsk.io" summary="Ejemplo de autorización" expanded="true" %}
{% swagger-description %}
Obtener segmentos usando autorización con API Key
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="Bearer" required="true" %}
Bearer {API Key}
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="String" %}
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
