---
description: >-
  Ejemplos copy/paste para los casos de uso más comunes al construir una app
  embebida en Videsk.
---

# Ejemplos

## Sandbox para QA

Antes de levantar tu propia app, puedes registrar estas URLs sandbox de Videsk como `iframe.url` para validar que tu cuenta, segmento y permisos están bien configurados. Te muestran en pantalla lo que recibe la app, así que sirven para depurar context, scopes y plantillas sin construir nada.

| URL | Para qué sirve |
| --- | --- |
| `https://sdbx.videsk.io/iframes/broker/postmessage` | Verifica el handshake del [broker](../broker.md): muestra el `videsk:init` recibido y el `context` resuelto. Es la versión hospedada del ejemplo [App mínima](app-minima.md). |
| `https://sdbx.videsk.io/iframes/query-params` | Muestra los query params resueltos por Handlebars en la URL. Útil para validar [Plantillas y contexto](../plantillas.md) sin un broker. |

{% hint style="info" %}
Cuándo conviene usarlos:

* Validar que tu app aparece en el launcher con la configuración correcta.
* Confirmar que `contextScopes` está entregando los bloques que esperas.
* Probar que tu plantilla Handlebars resuelve los valores correctos.
* Reproducir un bug antes de tocar código de tu lado.
{% endhint %}

## Ejemplos en código

{% content-ref url="app-minima.md" %}
[app-minima.md](app-minima.md)
{% endcontent-ref %}

{% content-ref url="sesion-externa.md" %}
[sesion-externa.md](sesion-externa.md)
{% endcontent-ref %}

{% content-ref url="eventos-en-vivo.md" %}
[eventos-en-vivo.md](eventos-en-vivo.md)
{% endcontent-ref %}
