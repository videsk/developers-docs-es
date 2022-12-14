---
description: >-
  Ver谩s de forma breve como realizar la integraci贸n de nuestros widgets en tu
  sitio web.
---

# 馃攲 Instalaci贸n

La forma base de integraci贸n es mediante un script. Este script carga recursos necesarios para renderizar el widget los cuales se componen de HTML, CSS y Javascript.

## Script de integraci贸n

{% hint style="info" %}
No somos compatibles con [SRI (Subresource Integrity)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource\_Integrity), de lo contrario no podr铆amos ofrecer actualizaciones y mejoras de forma constante los cuales son cada semana.
{% endhint %}

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://assets.videsk.io/js/videsk-widget.min.js" videsk-token="REPLACE_TOKEN" async></script>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const script = document.createElement("script");
script.src = "https://assets.videsk.io/js/videsk-widget.min.js";
script.setAttribute("videsk-token", "REPLACE_TOKEN");
document.body.appendChild(script);
```
{% endtab %}
{% endtabs %}

Puedes acceder a la documentaci贸n de nuestra API en el siguiente enlace:

{% content-ref url="../api/" %}
[api](../api/)
{% endcontent-ref %}
