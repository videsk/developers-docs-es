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

## Ejemplo de autorización

<mark style="color:blue;">`GET`</mark> `https://api.videsk.io/public/video-contact-center/segments`

Obtener segmentos usando autorización con API Key

#### Headers

| Name                                            | Type   | Description      |
| ----------------------------------------------- | ------ | ---------------- |
| Authorization<mark style="color:red;">\*</mark> | Bearer | Bearer {API Key} |
| Content-Type<mark style="color:red;">\*</mark>  | String | application/json |

{% tabs %}
{% tab title="401: Unauthorized Invalid JWT" %}
```javascript
{
	"name": "NotAuthenticated",
	"message": "Authorization header with valid JWT is required.",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endtab %}

{% tab title="401: Unauthorized JWT malformed" %}
```javascript
{
	"name": "NotAuthenticated",
	"message": "jwt malformed",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endtab %}

{% tab title="401: Unauthorized Invalid signature" %}
```javascript
{
	"name": "NotAuthenticated",
	"message": "invalid signature",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endtab %}

{% tab title="401: Unauthorized Infected JWT" %}
```javascript
{
	"name": "NotAuthenticated",
	"message": "Unexpected token � in JSON at position 6",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endtab %}

{% tab title="401: Unauthorized Expired JWT" %}
```javascript
{
	"name": "NotAuthenticated",
	"message": "jwt expired",
	"code": 401,
	"className": "not-authenticated",
	"errors": {}
}
```
{% endtab %}

{% tab title="403: Forbidden API Key don't have permissions to CRUD" %}
```javascript
{
	"name": "Forbidden",
	"message": "You don't have access to /public/video-contact-center/segments. Please contact to your administrator.",
	"code": 403,
	"className": "forbidden",
	"errors": {}
}
```
{% endtab %}

{% tab title="403: Forbidden Integration key was removed" %}
```javascript
{
	"name": "Forbidden",
	"message": "The integration token it's invalid or was removed.",
	"code": 403,
	"className": "forbidden",
	"errors": {}
}
```
{% endtab %}
{% endtabs %}
