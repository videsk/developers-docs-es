---
description: >-
  A continuación te explicaremos ciertos conceptos importantes a considerar
  antes de integrar Videsk en tu sitio web.
---

# 💆‍♀️ Cabeceras

Dependiendo de la configuración de tu sitio web y dónde esté alojado deberás configurar ciertas cabeceras en tu servidor web.

{% hint style="info" %}
**Las cabeceras son opcionales**, pero son sugeridas para añadir mayor seguridad a tu sitio web. **Si no posees ninguna de ellas no es obligatorio añadirlas.**
{% endhint %}

## Feature-Policy o Permissions-Policy

Esta cabecera define donde y que tipos de características del navegador se pueden utilizan en tu sitio, como cámara, micrófono, GPS, giroscopio, batería, etc. Si tienes activada esta cabecera deberás añadir al listado:

```
Feature-Policy: microphone 'self'; camera 'self'; autoplay 'self'; ...
Permissions-Policy: autoplay=(self), camera=(self), fullscreen=(self), microphone=(self), picture-in-picture=(self)
```

## X-Frame-Options

Esta cabecera es vital en términos de seguridad, evita que embeban tu sitio web en uno externo suplantando tu identidad y potencialmente extraer datos de tus usuarios. Por ello, te sugerimos añadirla como mínimo en `SAMEORIGIN`.

```
X-Frame-Options: SAMEORIGIN;
```

{% hint style="info" %}
Si configuras el valor en `DENY` podrías perder ciertas funcionalidades de Videsk.
{% endhint %}

## Content-Security-Policy

Esta cabecera (CSP) permite definir que tipo de contenido se tiene permitido cargar para cada servicio y tipo de recursos registrados en esta cabecera.

```
Content-Security-Policy: connect-src 'self' *.videsk.io: script-src *.videsk.io; style-src *.videsk.io prefetch-src *.videsk.io media-src *.videsk.io;
```

{% hint style="warning" %}
Sin `connect-src 'self' *videsk.io` provocarás que las conexiones WebSocket sean bloqueadas.
{% endhint %}

## Content-Security-Policy-Report-Only

Esta cabecera permite experimentar con ciertas políticas de cabeceras antes de implementar oficialmente, sin generar necesariamente un impacto real sobre tu sitio, dando así la opción de monitorear el comportamiento.

Te sugerimos añadir lo mismo que en Content-Security-Policy (CSP).
