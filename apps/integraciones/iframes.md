---
description: >-
  Requisitos de hosting que tu URL debe cumplir para poder embeberse como
  app en Videsk.
---

# Iframes

Las apps de Videsk se renderizan dentro de un `<iframe>` en [Consola](https://console.videsk.io/) y [Dashboard](https://app.videsk.io/). Para que el navegador permita embeber tu URL, ésta debe cumplir tres requisitos: HTTPS, cabeceras correctas y, si aplica, cookies con `SameSite=None`.

## `Content-Security-Policy` (CSP)

Configura la cabecera `Content-Security-Policy` en las respuestas de tu URL para autorizar a los dominios de Videsk a embeberte:

```
Content-Security-Policy: frame-ancestors 'self' https://*.videsk.io https://console.videsk.io;
```

Los dominios oficiales son:

* Consola: `https://console.videsk.io`
* Dashboard: `https://app.videsk.io`
* Wildcard recomendado: `https://*.videsk.io`

{% hint style="info" %}
Si actualmente usas la cabecera `X-Frame-Options`, está deprecada. Reemplázala por `Content-Security-Policy: frame-ancestors`.
{% endhint %}

## Cookies

Si tu app mantiene una sesión por cookies, confíguralas con `SameSite=None; Secure` para que el navegador no las bloquee al cargarse dentro del iframe:

```
Set-Cookie: session=xxx; SameSite=None; Secure; HttpOnly
```

De lo contrario, es típico caer en un loop de login porque la cookie de sesión nunca se persiste.

{% hint style="info" %}
Si tu app usa `localStorage` o `sessionStorage` en vez de cookies, omite este paso.
{% endhint %}

## HTTPS

Tu URL **debe** servirse por HTTPS. Contenido sobre `http://` será bloqueado por el navegador al estar embebido en un origen HTTPS.
