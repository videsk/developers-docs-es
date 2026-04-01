---
description: >-
  En esta documentación podrás conocer cómo integrar aplicaciones web
  incrustadas (embebidas) en nuestros aplicativos.
---

# Iframes

Las aplicaciones integrables de Videsk se incorporan principalmente mediante iframes en nuestros productos, como [Consola](https://console.videsk.io/) y [Dashboard](https://app.videsk.io/).

Para ello, se deben considerar los detalles requeridos para que resulte viable.

## Permisos de cabeceras

La cabecera (header) principal es `Content-Security-Policy`. Esta cabecera permite indicar las políticas de seguridad del contenido de tu web, en este caso para autorizar a sitios externos a tu dominio o subdominio a embeber tu web.

{% hint style="info" %}
Es posible que actualmente estés utilizando la cabecera `X-Frame-Options` El cual está deprecado; lo recomendable es eliminarlo a favor de CSP.
{% endhint %}

### `Content-Security-Policy` (CSP)

Los dominios utilizados para nuestros aplicativos son:

* Consola: https://console.videsk.io
* Dashboard: https://app.videsk.io
* Autorizar ambos (wildcard): https://\*.videsk.io

```
Content-Security-Policy: frame-ancestors 'self' https://*.videsk.io https://console.videsk.io;
```

{% hint style="info" %}
Es recomendable, para una mejor experiencia, permitir el uso de nuestros subdominios wildcard.
{% endhint %}

## Cookies

En caso de que la aplicación a embeber tenga un inicio de sesión para acceder, lo recomendable es configurar las cookies de la siguiente manera:

```
Set-Cookie: session=xxx; SameSite=None; Secure; HttpOnly
```

Esto evita que el navegador bloquee las cookies de sesión, evitando un loop infinito de inicio de sesión en el que no se almacenen dichas cookies.

{% hint style="info" %}
Si el mecanismo de sesión utiliza almacenamiento local (localStorage, sessionStorage u otro mecanismo), omitir la configuración de cookies.
{% endhint %}

## Cifrado

Es mandatorio que la aplicación a embeber sea servida cifrada (TLS), es decir, `https://` no `http://` . De lo contrario, el contenido será bloqueado por el navegador.

***

## Compatibilidad

En las apps embebidas se pueden configurar los valores de `allow` que el iframe debe tener; de esa manera, la aplicación tendrá acceso al micrófono, la cámara, el GPS, etc.

Los atributos por defecto que se inyectan son:

```html
<iframe
  src="https://app.example.com/embed"
  allow="camera; microphone; display-capture; clipboard-write; autoplay"
  sandbox="allow-scripts allow-same-origin allow-forms allow-popups allow-popups-to-escape-sandbox allow-downloads"
  referrerpolicy="no-referrer"
  loading="lazy"
></iframe>
```
